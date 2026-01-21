---
name: planning
description: Use when you have a spec or requirements for a multi-step task, before touching code. Creates comprehensive implementation plans with bite-sized tasks, exact file paths, and testing steps.
---

# Writing Implementation Plans

## Overview

Write comprehensive implementation plans assuming the engineer has zero context for the codebase. Document everything they need to know: which files to touch for each task, code examples, testing approach, and how to verify it works. Break work into bite-sized tasks following DRY, YAGNI, and TDD principles.

Assume the implementer is a skilled developer but knows almost nothing about the specific toolset or problem domain.

## When to Use

Use this skill when:

- You have a design or specification ready to implement
- Starting a multi-step task that needs coordination
- Need to break down complex work into manageable pieces
- Want to ensure nothing is missed during implementation
- Planning work that others (or future you) will execute

## Bite-Sized Task Granularity

**Each step should be one action (2-5 minutes):**

- "Write the failing test" - one step
- "Run it to make sure it fails" - one step
- "Implement the minimal code to make the test pass" - one step
- "Run the tests and make sure they pass" - one step
- "Commit the changes" - one step

**Why this granularity?**

- Easy to track progress
- Clear checkpoints for validation
- Simple to resume if interrupted
- Reduces cognitive load

## Plan Document Structure

### Header Template

Every plan MUST start with this header:

```markdown
# [Feature Name] Implementation Plan

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about the approach]

**Tech Stack:** [Key technologies/libraries being used]

---
```

### Task Structure Template

````markdown
### Task N: [Component/Feature Name]

**Files:**

- Create: `exact/path/to/file.py`
- Modify: `exact/path/to/existing.py` (lines 123-145)
- Test: `tests/exact/path/to/test.py`

**Step 1: Write the failing test**

```python
def test_specific_behavior():
    # Arrange
    input_data = create_test_data()

    # Act
    result = function_to_test(input_data)

    # Assert
    assert result == expected_output
```
````

**Step 2: Run test to verify it fails**

Run: `pytest tests/path/test.py::test_name -v`

Expected output: FAIL with "function_to_test not defined" or similar

**Step 3: Write minimal implementation**

```python
def function_to_test(input_data):
    # Minimal implementation to pass the test
    return expected_output
```

**Step 4: Run test to verify it passes**

Run: `pytest tests/path/test.py::test_name -v`

Expected output: PASS (1 test passed)

**Step 5: Commit the changes**

```bash
git add tests/path/test.py src/path/file.py
git commit -m "feat: add specific feature functionality"
```

---

````

## Planning Best Practices

### Be Specific

✅ **Good:** "Modify `src/utils/parser.py` lines 45-60 to add error handling"

❌ **Bad:** "Add error handling to the parser"

### Include Complete Code

✅ **Good:** Show the actual code to write

❌ **Bad:** "Add validation here"

### Specify Exact Commands

✅ **Good:** `npm test -- --coverage --verbose`

❌ **Bad:** "Run the tests"

### Define Expected Outputs

✅ **Good:** "Expected: Server starts on port 3000, logs 'Ready'"

❌ **Bad:** "Expected: It should work"

## Key Principles

- **DRY (Don't Repeat Yourself)** - Reuse code, avoid duplication
- **YAGNI (You Aren't Gonna Need It)** - Only build what's needed now
- **TDD (Test-Driven Development)** - Write tests first, then implementation
- **Frequent commits** - Commit after each completed task
- **Exact paths** - Always use complete, exact file paths
- **Complete code** - Include actual code in the plan, not placeholders
- **Clear validation** - Specify how to verify each step worked

## Plan Document Location

Save plans to an appropriate location:

- `docs/plans/YYYY-MM-DD-<feature-name>.md`
- `docs/implementation-plans/<feature-name>.md`
- Or project-specific planning directory

## After Writing the Plan

### Offer Execution Options

**"Plan complete and saved to `docs/plans/<filename>.md`.**

**Ready to proceed with implementation?**

**Options:**
1. **Immediate execution** - I can start implementing the plan now
2. **Review first** - You review the plan and provide feedback
3. **Delegate** - Someone else will implement using this plan

**Which approach would you prefer?"**

### If Proceeding with Implementation

- Follow the plan task by task
- Validate each step before moving to the next
- Update the plan if you discover issues or better approaches
- Keep the user informed of progress

## Example Plan Outline

```markdown
# User Authentication Implementation Plan

**Goal:** Add secure user authentication with JWT tokens

**Architecture:** REST API endpoints for login/logout, JWT middleware for protected routes, bcrypt for password hashing

**Tech Stack:** Node.js, Express, JWT, bcrypt, PostgreSQL

---

### Task 1: Database Schema

**Files:**
- Create: `db/migrations/001_create_users_table.sql`
- Create: `db/models/User.js`

[Steps 1-5 with code, commands, expected outputs]

---

### Task 2: Authentication Service

**Files:**
- Create: `src/services/authService.js`
- Create: `tests/services/authService.test.js`

[Steps 1-5 with code, commands, expected outputs]

---

### Task 3: API Endpoints

**Files:**
- Create: `src/routes/auth.js`
- Modify: `src/app.js` (add auth routes)
- Create: `tests/routes/auth.test.js`

[Steps 1-5 with code, commands, expected outputs]

---
````

## Anti-Patterns to Avoid

❌ Vague file references ("update the config")
❌ Missing test steps
❌ Assuming packages are installed
❌ Skipping expected outputs
❌ Too large task granularity (> 10 minutes per step)
❌ Incomplete code examples
❌ No commit strategy
