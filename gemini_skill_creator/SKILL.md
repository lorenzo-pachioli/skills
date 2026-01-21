---
name: gemini_skill_creator
description: Guides the creation of effective, discoverable, and robust Skills optimized for Claude. Use when creating new Skills or refactoring existing ones. Provides workflows, best practices, templates, and examples for skill authoring following progressive disclosure, conciseness, and proper structure.
---

# Gemini Skill Creator

This skill guides you through creating effective Skills that are optimized for Claude to use correctly in real-world scenarios.

## When to Use This Skill

Use this skill when:

- Creating a new Skill from scratch
- Refactoring or improving an existing Skill
- Reviewing a Skill for best practices compliance
- Uncertain about skill structure or naming conventions
- Need templates for quick skill scaffolding

## Core Principles (Quick Reference)

1. **Conciseness is critical** - Assume Claude is intelligent; only add what Claude cannot infer
2. **Define the right degree of freedom** - Match specificity to task fragility
3. **Test with all target models** - Skills behave differently across Haiku, Sonnet, and Opus
4. **Progressive disclosure** - Keep SKILL.md < 500 lines; details go in separate files
5. **Clear workflows** - Use step-by-step checklists for complex tasks

## Skill Creation Workflow

### Phase 1: Planning

1. **Define the Skill's Purpose**
   - What problem does it solve?
   - When should Claude activate it?
   - What are the expected inputs/outputs?

2. **Determine Complexity Level**
   - Simple (< 200 lines, single file) → SKILL.md only
   - Medium (200-500 lines) → SKILL.md + reference.md
   - Complex (> 500 lines or scripts) → SKILL.md + reference.md + examples.md + scripts/

3. **Choose the Right Degree of Freedom**
   - **High freedom** (textual instructions): Multiple valid solutions, contextual decisions
   - **Medium freedom** (pseudocode/templates): Recommended pattern with adjustable parameters
   - **Low freedom** (exact scripts): Fragile operations, mandatory sequences

### Phase 2: Structure Setup

4. **Create Directory Structure**

   ```
   skill_name/
   ├── SKILL.md          (required)
   ├── reference.md      (optional, for detailed docs)
   ├── examples.md       (optional, for examples)
   └── scripts/          (optional, for executable code)
   ```

5. **Name the Skill**
   - Use lowercase, numbers, and hyphens only
   - Prefer gerund form (verb + ing): `processing-pdfs`, `analyzing-spreadsheets`
   - Avoid: vague names (helper, utils), reserved words (anthropic, claude)
   - Max 64 characters

### Phase 3: SKILL.md Creation

6. **Write YAML Frontmatter** (required)

   ```yaml
   ---
   name: skill_name
   description: Third-person description of what it does and when to use it (max 1024 chars)
   ---
   ```

7. **Structure SKILL.md** (keep < 500 lines)
   - **Overview**: What the skill does (2-3 sentences)
   - **When to Use**: Explicit triggers and contexts
   - **Quick Reference**: Key concepts or commands
   - **Workflow/Instructions**: Step-by-step process
   - **References**: Links to reference.md, examples.md, scripts/
   - **Optional**: Table of contents if > 100 lines

8. **Write Effective Description**
   - Third person voice
   - Include: main action + contexts/triggers
   - Example: "Extract text and tables from PDF files. Use when working with PDF files or when the user mentions PDFs."
   - Avoid vague descriptions

### Phase 4: Supporting Documentation

9. **Create reference.md** (if needed)
   - Detailed explanations
   - API references
   - Configuration options
   - Anti-patterns
   - Only one level deep from SKILL.md (no nested references)

10. **Create examples.md** (if needed)
    - Real input/output examples
    - Before/after comparisons
    - Common use cases
    - Edge cases

11. **Add Scripts** (if needed)
    - Robust error handling (don't delegate to Claude)
    - Clear documentation on whether to execute or read as reference
    - Justify any magic numbers
    - Provide intermediate outputs for complex operations

### Phase 5: Validation

12. **Run the Checklist** (see [reference.md](reference.md#final-checklist))
    - [ ] Description is clear (what + when)
    - [ ] SKILL.md < 500 lines
    - [ ] Progressive disclosure applied
    - [ ] Workflows are clear
    - [ ] Scripts are robust (if applicable)
    - [ ] Tested with target models

13. **Test the Skill**
    - Create evaluations for real-world scenarios
    - Test with Haiku, Sonnet, and Opus
    - Iterate based on failures

## Quick Start Templates

Use the templates in the `templates/` directory:

- [SKILL_TEMPLATE.md](templates/SKILL_TEMPLATE.md) - Basic skill structure
- [REFERENCE_TEMPLATE.md](templates/REFERENCE_TEMPLATE.md) - Detailed documentation
- [EXAMPLES_TEMPLATE.md](templates/EXAMPLES_TEMPLATE.md) - Examples structure

## Additional Resources

- **[reference.md](reference.md)** - Complete best practices documentation (10 sections)
- **[examples.md](examples.md)** - Practical skill creation examples
- **templates/** - Ready-to-use templates for quick scaffolding

## Common Patterns

### Simple Skill (Textual Instructions)

```
skill_name/
└── SKILL.md (overview + instructions)
```

### Medium Skill (With Reference)

```
skill_name/
├── SKILL.md (overview + workflow)
└── reference.md (detailed docs)
```

### Complex Skill (Full Structure)

```
skill_name/
├── SKILL.md (overview + navigation)
├── reference.md (detailed docs)
├── examples.md (practical examples)
└── scripts/ (executable utilities)
```

## Anti-Patterns to Avoid

❌ Windows-style paths (`\`) - Use forward slashes (`/`)
❌ Assuming packages are installed - Check or provide installation instructions
❌ Too many alternatives without a default - Provide clear recommendations
❌ Deep references (SKILL.md → file1.md → file2.md) - Max one level
❌ Vague descriptions - Be specific about what and when
❌ Over-explaining - Trust Claude's intelligence

## Workflow Summary

```
Plan → Structure → SKILL.md → Supporting Docs → Validate → Test → Iterate
```

Remember: **Conciseness is critical**. Every token counts. Only add what Claude cannot infer on its own.
