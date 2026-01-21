# Skill Authoring Best Practices - Complete Reference

This document provides comprehensive best practices for designing Skills that are effective, discoverable, and robust, optimized for Claude to use correctly in real-world scenarios.

## Table of Contents

1. [Fundamental Principles](#1-fundamental-principles)
2. [Required Structure](#2-required-structure)
3. [Progressive Disclosure](#3-progressive-disclosure)
4. [Workflows and Feedback Loops](#4-workflows-and-feedback-loops)
5. [Content Guidelines](#5-content-guidelines)
6. [Skills with Executable Code](#6-skills-with-executable-code)
7. [Runtime and Filesystem](#7-runtime-and-filesystem)
8. [Evaluation and Iteration](#8-evaluation-and-iteration)
9. [Anti-Patterns](#9-anti-patterns)
10. [Final Checklist](#10-final-checklist)

---

## 1. Fundamental Principles

### 1.1. Conciseness is Critical

**The context window is a shared resource** containing:

- System prompt
- Conversation history
- Metadata from other Skills
- User request

**How Claude loads Skills:**

1. Preloads only `name` and `description` of all Skills
2. Reads `SKILL.md` only when the Skill is relevant
3. Reads additional files only if explicitly referenced

**Base rule:** Assume Claude is already intelligent. Add only information Claude cannot infer on its own.

**Control questions:**

- Does Claude really need this explanation?
- Does this justify its token cost?

**Example:**

```diff
- This skill helps you process PDF files by extracting text and images.
- It uses various libraries to parse PDF content and convert it to usable formats.
- You should use this when working with PDFs.
+ Extract text and tables from PDF files. Use when working with PDF files or when the user mentions PDFs.
```

### 1.2. Define the Right Degree of Freedom

Adjust specificity based on task fragility:

**High Freedom (textual instructions):**

- Multiple valid solutions exist
- Decisions depend on context
- Example: Code reviews, content analysis

**Medium Freedom (pseudocode/templates):**

- Recommended pattern exists
- Parameters are adjustable
- Example: Report generation, data formatting

**Low Freedom (exact scripts):**

- Fragile or critical operations
- Mandatory sequences
- Example: Database migrations, deployment scripts

**Analogy:**

- Narrow bridge → strict instructions
- Open field → general guidance

### 1.3. Test with All Target Models

Skills behave differently across models:

- **Haiku:** Needs more guidance and explicit instructions
- **Sonnet:** Balanced clarity and efficiency
- **Opus:** Avoid over-explaining; can infer more

**If the Skill will be used across multiple models, it must work well on all of them.**

---

## 2. Required Structure

### 2.1. YAML Frontmatter (Required in SKILL.md)

**Required fields:**

```yaml
---
name: skill_name
description: Description of what the skill does and when to use it
---
```

**Field requirements:**

**`name`:**

- Max 64 characters
- Lowercase, numbers, and hyphens only
- No reserved words (anthropic, claude)

**`description`:**

- Not empty
- Max 1024 characters
- Describes what it does AND when to use it

### 2.2. Naming Conventions

**Recommended:** Gerund form (verb + ing)

**Good examples:**

- `processing-pdfs`
- `analyzing-spreadsheets`
- `testing-code`
- `deploying-applications`

**Avoid:**

- Vague names: `helper`, `utils`, `tools`
- Generic names: `data`, `files`, `manager`
- Inconsistencies within your skill collection

### 2.3. Effective Descriptions

**Always use third person voice.**

**Must enable Claude to:**

1. Understand what the skill does
2. Know when to activate it among 100+ skills

**Include:**

- Main action
- Explicit contexts/triggers

**Examples:**

✅ **Good:**

```yaml
description: Extract text and tables from PDF files. Use when working with PDF files or when the user mentions PDFs, document parsing, or text extraction.
```

❌ **Bad:**

```yaml
description: Helps with PDFs.
```

❌ **Bad:**

```yaml
description: A utility for processing documents.
```

---

## 3. Progressive Disclosure

### 3.1. SKILL.md as Index

**SKILL.md should be an overview + navigation hub.**

- Details go in separate files
- Recommended limit: **< 500 lines**

**Typical structure:**

```
skill/
├── SKILL.md          # Overview + navigation
├── reference.md      # Detailed documentation
├── examples.md       # Practical examples
└── scripts/          # Executable utilities
```

**Claude only loads additional files when needed.**

### 3.2. Avoid Deep References

**Maximum one level of depth from SKILL.md.**

Deep references cause partial reads and incomplete information.

✅ **Correct:**

```
SKILL.md → reference.md
SKILL.md → examples.md
```

❌ **Incorrect:**

```
SKILL.md → advanced.md → details.md → appendix.md
```

### 3.3. Table of Contents for Long Files

**If a file exceeds ~100 lines:**

- Include a table of contents
- Allows Claude to understand scope without reading everything

**Example:**

```markdown
# Skill Name

## Table of Contents

1. [Overview](#overview)
2. [Installation](#installation)
3. [Usage](#usage)
4. [API Reference](#api-reference)
5. [Examples](#examples)
```

---

## 4. Workflows and Feedback Loops

### 4.1. Sequential Workflows

**For complex tasks, divide into clear steps:**

Use checklists that Claude can follow:

```markdown
## Workflow

1. **Analyze Requirements**
   - [ ] Read user request
   - [ ] Identify key parameters
   - [ ] Validate inputs

2. **Generate Plan**
   - [ ] Create step-by-step approach
   - [ ] Identify potential issues
   - [ ] Request user confirmation if needed

3. **Execute**
   - [ ] Implement solution
   - [ ] Validate each step
   - [ ] Handle errors gracefully

4. **Verify**
   - [ ] Test output
   - [ ] Compare against requirements
   - [ ] Report results
```

**Prevents Claude from skipping validations.**

### 4.2. Feedback Loops

**Recommended pattern:**

```
execute → validate → correct → repeat
```

**This significantly improves final quality.**

**Example:**

```markdown
## Code Generation Workflow

1. Generate initial code
2. Run linter and tests
3. If errors exist:
   - Analyze error messages
   - Fix issues
   - Go to step 2
4. If all tests pass, proceed to next step
```

---

## 5. Content Guidelines

### 5.1. Avoid Time-Dependent Information

❌ **Bad:**

```markdown
As of 2024, the recommended approach is...
```

✅ **Good:**

```markdown
The recommended approach is...
```

**If you need to document legacy patterns:**

```markdown
## Current Approach

[Current best practice]

## Legacy Patterns (Deprecated)

[Old approach for reference]
```

### 5.2. Maintain Consistent Terminology

**Use the same terms throughout all skill files.**

**Example:**

- If you use "workflow" in SKILL.md, don't switch to "process" in reference.md
- If you use "execute," don't alternate with "run"

### 5.3. Provide Templates and Examples

**When output should be structured:**

Provide templates:

```markdown
## Report Template
```

# Analysis Report

## Summary

[Brief overview]

## Findings

1. [Finding 1]
2. [Finding 2]

## Recommendations

- [Recommendation 1]
- [Recommendation 2]

```

```

**Provide real input/output examples:**

````markdown
## Example

**Input:**

```json
{ "name": "John", "age": 30 }
```
````

**Output:**

```
Name: John
Age: 30 years old
```

````

### 5.4. Avoid Multiple Options Without Clear Default

❌ **Bad:**
```markdown
You can use approach A, B, or C.
````

✅ **Good:**

```markdown
**Recommended:** Use approach A for most cases.

**Alternative approaches:**

- Approach B: Use when [specific condition]
- Approach C: Use when [specific condition]
```

---

## 6. Skills with Executable Code

### 6.1. Robust Error Handling in Scripts

**Scripts should handle errors, not delegate them to Claude.**

❌ **Bad:**

```python
def process_file(path):
    with open(path) as f:
        return f.read()
```

✅ **Good:**

```python
def process_file(path):
    try:
        with open(path, 'r', encoding='utf-8') as f:
            return f.read()
    except FileNotFoundError:
        print(f"Error: File not found: {path}")
        return None
    except PermissionError:
        print(f"Error: Permission denied: {path}")
        return None
    except Exception as e:
        print(f"Error reading file {path}: {str(e)}")
        return None
```

**Avoid magic numbers; justify constants:**

❌ **Bad:**

```python
timeout = 30
```

✅ **Good:**

```python
# Timeout in seconds - allows for slow network connections
TIMEOUT_SECONDS = 30
```

### 6.2. Utility Scripts

**Advantages:**

- More reliable than generated code
- Fewer tokens consumed
- Deterministic results

**Always clarify whether Claude should:**

1. Execute the script
2. Read it as reference
3. Modify it for specific use case

**Example:**

````markdown
## Using the Migration Script

**To execute:**

```bash
python scripts/migrate_database.py --config config.json
```
````

**To use as reference:**
View [scripts/migrate_database.py](scripts/migrate_database.py) for the migration pattern.

```

### 6.3. Intermediate Outputs for Verification

**For complex or destructive operations:**

Use intermediate files:
```

plan → validate → execute

````

**Example:**
```markdown
## Database Migration Workflow

1. **Generate migration plan**
   - Script creates `migration_plan.json`
   - Review the plan before proceeding

2. **Validate plan**
   - Run validation script
   - Checks for conflicts and issues

3. **Execute migration**
   - Only runs if validation passes
   - Creates backup before applying changes
````

---

## 7. Runtime and Filesystem

### 7.1. File Navigation

**Claude navigates skills like a filesystem.**

**Always use forward slashes (`/`):**

✅ **Correct:**

```markdown
See [reference documentation](reference.md)
See [examples](examples/basic.md)
```

❌ **Incorrect:**

```markdown
See [reference documentation](reference.md)
See [examples](examples\basic.md)
```

### 7.2. Descriptive File Names

**Use clear, descriptive names:**

✅ **Good:**

- `api_reference.md`
- `migration_examples.md`
- `error_handling_guide.md`

❌ **Bad:**

- `doc1.md`
- `misc.md`
- `stuff.md`

### 7.3. Organize by Domain

**Group related files:**

```
skill_name/
├── SKILL.md
├── core/
│   ├── workflow.md
│   └── concepts.md
├── api/
│   ├── reference.md
│   └── examples.md
└── scripts/
    ├── setup.sh
    └── validate.py
```

### 7.4. Large Files Don't Consume Tokens Until Read

**Large files are fine if they're not always needed.**

Claude only loads them when referenced.

---

## 8. Evaluation and Iteration

### 8.1. Evaluation-Driven Development

**Before documenting extensively:**

1. Detect real failures
2. Create evaluations
3. Measure baseline
4. Document minimum necessary
5. Iterate

**Don't over-document before testing.**

### 8.2. Iterative Development with Claude

**Recommended model:**

1. **Claude A:** Designs and refines the Skill
2. **Claude B:** Uses it in real tasks
3. **Observe** → **Adjust** → **Test again**

**This reveals gaps in documentation and workflow.**

### 8.3. Create Evaluations

**Test real-world scenarios:**

```markdown
## Evaluation Scenarios

### Scenario 1: Simple PDF Extraction

- Input: Single-page PDF with text
- Expected: Extracted text matches original
- Pass criteria: 100% text accuracy

### Scenario 2: Complex PDF with Tables

- Input: Multi-page PDF with tables
- Expected: Tables extracted as structured data
- Pass criteria: Table structure preserved

### Scenario 3: Scanned PDF

- Input: Image-based PDF
- Expected: OCR applied, text extracted
- Pass criteria: > 95% text accuracy
```

---

## 9. Anti-Patterns

### Common Mistakes to Avoid

❌ **Windows-style paths (`\`)**

- Use forward slashes (`/`) always

❌ **Assuming packages are installed**

- Check for dependencies or provide installation instructions

❌ **Too many alternatives without default**

- Provide clear recommendations

❌ **Deep references**

- Max one level from SKILL.md

❌ **Vague descriptions**

- Be specific about what and when

❌ **Over-explaining**

- Trust Claude's intelligence

❌ **Time-dependent information**

- Avoid "as of 2024" statements

❌ **Inconsistent terminology**

- Use same terms throughout

❌ **Missing error handling in scripts**

- Scripts should be robust

❌ **No table of contents for long files**

- Add TOC if > 100 lines

---

## 10. Final Checklist

Before publishing a skill, verify:

### Structure

- [ ] YAML frontmatter is valid (name, description)
- [ ] Name follows conventions (lowercase, hyphens, gerund form)
- [ ] Description is clear (what + when to use)
- [ ] SKILL.md is < 500 lines

### Content

- [ ] Progressive disclosure applied (details in separate files)
- [ ] No deep references (max one level from SKILL.md)
- [ ] Table of contents added to files > 100 lines
- [ ] Workflows are clear and sequential
- [ ] Examples include real input/output
- [ ] Templates provided for structured output
- [ ] No time-dependent information
- [ ] Consistent terminology throughout

### Code (if applicable)

- [ ] Scripts have robust error handling
- [ ] Magic numbers are justified
- [ ] Clear instructions on execute vs. reference
- [ ] Intermediate outputs for complex operations
- [ ] Dependencies are documented

### Testing

- [ ] Evaluations created for real-world scenarios
- [ ] Tested with Haiku (if targeting Haiku)
- [ ] Tested with Sonnet (if targeting Sonnet)
- [ ] Tested with Opus (if targeting Opus)
- [ ] Iterated based on failures

### Files

- [ ] All paths use forward slashes (`/`)
- [ ] File names are descriptive
- [ ] Files organized by domain
- [ ] No Windows-style paths

### Final Review

- [ ] Skill solves the intended problem
- [ ] Documentation is concise (no over-explaining)
- [ ] Claude can discover when to use it
- [ ] Degree of freedom matches task fragility
- [ ] Ready for production use

---

## Summary

**The golden rule:** Conciseness is critical. Every token counts. Only add what Claude cannot infer on its own.

**The workflow:** Plan → Structure → SKILL.md → Supporting Docs → Validate → Test → Iterate

**The goal:** Create skills that are effective, discoverable, and robust for real-world use.
