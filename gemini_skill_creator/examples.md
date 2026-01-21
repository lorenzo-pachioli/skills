# Skill Creation Examples

This document provides practical examples of skill creation at different complexity levels.

## Table of Contents

1. [Simple Skill Example](#simple-skill-example)
2. [Medium Skill with Reference](#medium-skill-with-reference)
3. [Complex Skill with Scripts](#complex-skill-with-scripts)
4. [Before/After Comparisons](#beforeafter-comparisons)

---

## Simple Skill Example

### Use Case: Text Cleaning Skill

A simple skill that provides instructions for cleaning and formatting text.

**Directory structure:**

```
cleaning-text/
└── SKILL.md
```

**SKILL.md:**

```markdown
---
name: cleaning-text
description: Clean and format text by removing extra whitespace, fixing punctuation, and standardizing line breaks. Use when the user needs to clean up messy text, format documents, or prepare text for processing.
---

# Text Cleaning

This skill helps clean and format text to make it more readable and consistent.

## When to Use

- User has messy text with inconsistent formatting
- Text needs to be prepared for further processing
- Document requires standardization

## Cleaning Workflow

1. **Remove Extra Whitespace**
   - Remove leading/trailing whitespace
   - Replace multiple spaces with single space
   - Standardize line breaks (use \n)

2. **Fix Punctuation**
   - Add space after punctuation marks
   - Remove space before punctuation
   - Ensure sentences end with proper punctuation

3. **Standardize Formatting**
   - Consistent capitalization
   - Remove special characters if needed
   - Normalize quotes (" instead of " or ")

4. **Validate**
   - Check for remaining issues
   - Ensure readability
   - Confirm with user if major changes made

## Common Patterns

**Extra whitespace:**
```

Input: "Hello world. How are you?"
Output: "Hello world. How are you?"

```

**Punctuation:**
```

Input: "Hello,world.How are you ?"
Output: "Hello, world. How are you?"

```

**Line breaks:**
```

Input: "Line 1\r\n\r\nLine 2\n\n\nLine 3"
Output: "Line 1\n\nLine 2\n\nLine 3"

```

```

**Why this works:**

- Single file (< 200 lines)
- Clear workflow
- Practical examples
- No external dependencies

---

## Medium Skill with Reference

### Use Case: API Testing Skill

A skill for testing REST APIs with detailed reference documentation.

**Directory structure:**

```
testing-apis/
├── SKILL.md
└── reference.md
```

**SKILL.md:**

````markdown
---
name: testing-apis
description: Test REST APIs by sending requests, validating responses, and checking status codes. Use when the user needs to test API endpoints, debug API issues, or validate API behavior.
---

# API Testing

This skill guides you through testing REST APIs systematically.

## When to Use

- User needs to test API endpoints
- Debugging API integration issues
- Validating API responses
- Creating API test cases

## Quick Reference

**HTTP Methods:** GET, POST, PUT, PATCH, DELETE
**Common Status Codes:** 200 (OK), 201 (Created), 400 (Bad Request), 401 (Unauthorized), 404 (Not Found), 500 (Server Error)

## Testing Workflow

1. **Understand the API**
   - Review API documentation
   - Identify endpoint URL
   - Determine required headers and parameters

2. **Prepare Request**
   - Choose HTTP method
   - Set headers (Content-Type, Authorization, etc.)
   - Prepare request body (if needed)

3. **Send Request**
   - Execute the request
   - Capture response

4. **Validate Response**
   - Check status code
   - Validate response body structure
   - Verify data correctness
   - Check response headers

5. **Document Results**
   - Record test case
   - Note any issues
   - Suggest fixes if errors found

## Example Test Case

**Endpoint:** `POST /api/users`

**Request:**

```json
{
  "name": "John Doe",
  "email": "john@example.com"
}
```
````

**Expected Response:**

```json
{
  "id": 123,
  "name": "John Doe",
  "email": "john@example.com",
  "created_at": "2024-01-15T10:30:00Z"
}
```

**Validation:**

- Status code: 201
- Response contains `id` field
- `name` and `email` match request
- `created_at` is valid timestamp

## Additional Resources

See [reference.md](reference.md) for:

- Complete HTTP status code reference
- Common headers explained
- Authentication methods
- Error handling patterns

````

**reference.md:**
```markdown
# API Testing Reference

## HTTP Status Codes

### 2xx Success
- **200 OK:** Request succeeded
- **201 Created:** Resource created successfully
- **204 No Content:** Success, no response body

### 4xx Client Errors
- **400 Bad Request:** Invalid request format
- **401 Unauthorized:** Authentication required
- **403 Forbidden:** Authenticated but not authorized
- **404 Not Found:** Resource doesn't exist
- **422 Unprocessable Entity:** Validation failed

### 5xx Server Errors
- **500 Internal Server Error:** Server error
- **502 Bad Gateway:** Invalid response from upstream
- **503 Service Unavailable:** Server temporarily unavailable

## Common Headers

### Request Headers
- **Content-Type:** Format of request body (`application/json`, `application/xml`)
- **Authorization:** Authentication credentials (`Bearer token`, `Basic auth`)
- **Accept:** Expected response format
- **User-Agent:** Client identifier

### Response Headers
- **Content-Type:** Format of response body
- **Content-Length:** Size of response body
- **Cache-Control:** Caching directives
- **Location:** URL of created resource (for 201 responses)

## Authentication Methods

### Bearer Token
````

Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

```

### Basic Auth
```

Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=

```

### API Key
```

X-API-Key: your-api-key-here

````

## Error Handling Patterns

### Standard Error Response
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid email format",
    "field": "email"
  }
}
````

### Multiple Errors

```json
{
  "errors": [
    { "field": "email", "message": "Invalid format" },
    { "field": "age", "message": "Must be positive" }
  ]
}
```

```

**Why this works:**
- SKILL.md provides workflow and overview (< 500 lines)
- reference.md contains detailed documentation
- Progressive disclosure applied
- One level of depth

---

## Complex Skill with Scripts

### Use Case: Database Migration Skill

A complex skill with validation scripts and intermediate outputs.

**Directory structure:**
```

migrating-databases/
├── SKILL.md
├── reference.md
├── examples.md
└── scripts/
├── generate_plan.py
├── validate_plan.py
└── execute_migration.py

````

**SKILL.md:**
```markdown
---
name: migrating-databases
description: Safely migrate database schemas with validation and rollback support. Use when the user needs to modify database structure, add tables or columns, or update constraints. Always generates a plan before execution.
---

# Database Migration

This skill guides you through safe database schema migrations with validation.

## When to Use

- User needs to modify database schema
- Adding/removing tables or columns
- Updating constraints or indexes
- Database version upgrades

## Safety-First Workflow

1. **Analyze Requirements**
   - Understand desired changes
   - Identify affected tables
   - Check for dependencies

2. **Generate Migration Plan**
   - Run `scripts/generate_plan.py`
   - Creates `migration_plan.json`
   - **STOP:** Do not proceed without user review

3. **Validate Plan**
   - Run `scripts/validate_plan.py`
   - Checks for conflicts
   - Verifies rollback safety
   - Reports potential issues

4. **User Approval**
   - Present plan to user
   - Explain changes and risks
   - Get explicit approval

5. **Create Backup**
   - Automatic backup before execution
   - Stored in `backups/` directory

6. **Execute Migration**
   - Run `scripts/execute_migration.py`
   - Applies changes
   - Monitors for errors

7. **Verify**
   - Check schema changes
   - Run test queries
   - Confirm success

8. **Rollback (if needed)**
   - Automatic rollback on failure
   - Manual rollback option available

## Example Migration Plan

```json
{
  "migration_id": "add_user_email_column",
  "changes": [
    {
      "action": "add_column",
      "table": "users",
      "column": "email",
      "type": "VARCHAR(255)",
      "nullable": false,
      "default": ""
    }
  ],
  "rollback": [
    {
      "action": "drop_column",
      "table": "users",
      "column": "email"
    }
  ],
  "estimated_time": "< 1 second",
  "risk_level": "low"
}
````

## Scripts Usage

### Generate Plan

```bash
python scripts/generate_plan.py --config db_config.json --changes changes.json
```

**Output:** `migration_plan.json`

### Validate Plan

```bash
python scripts/validate_plan.py --plan migration_plan.json
```

**Output:** Validation report

### Execute Migration

```bash
python scripts/execute_migration.py --plan migration_plan.json --backup
```

**Output:** Migration results

## Additional Resources

- [reference.md](reference.md) - SQL syntax reference, common patterns
- [examples.md](examples.md) - Real migration examples
- [scripts/](scripts/) - Migration utilities

## Critical Reminders

⚠️ **Always create backup before migration**
⚠️ **Never skip validation step**
⚠️ **Get user approval for destructive changes**
⚠️ **Test rollback procedure**

````

**Why this works:**
- Clear safety-first workflow
- Intermediate validation steps
- Scripts handle complex logic
- User approval required for critical operations
- Progressive disclosure (details in reference.md and examples.md)

---

## Before/After Comparisons

### Example 1: Vague vs. Clear Description

❌ **Before:**
```yaml
---
name: file-helper
description: Helps with files.
---
````

✅ **After:**

```yaml
---
name: processing-files
description: Process files by reading, parsing, and transforming content. Use when the user needs to read file contents, convert file formats, or batch process multiple files.
---
```

### Example 2: Over-Explained vs. Concise

❌ **Before:**

```markdown
## Overview

This skill is designed to help you work with JSON data. JSON, which stands for JavaScript Object Notation, is a lightweight data interchange format that is easy for humans to read and write and easy for machines to parse and generate. This skill will guide you through various operations you can perform on JSON data, including parsing, validating, transforming, and formatting.

When you receive JSON data, you'll want to first validate it to ensure it's properly formatted. This involves checking that all brackets and braces are properly matched, that strings are properly quoted, and that the overall structure conforms to the JSON specification...
```

✅ **After:**

```markdown
## Overview

Parse, validate, and transform JSON data.

## When to Use

- User provides JSON data to process
- Need to validate JSON structure
- Transform JSON format
```

### Example 3: No Structure vs. Clear Workflow

❌ **Before:**

```markdown
# Code Review

Review code for issues. Check for bugs, style problems, and performance issues. Make suggestions for improvements.
```

✅ **After:**

```markdown
# Code Review

## Workflow

1. **Understand Context**
   - Review code purpose
   - Identify language and framework

2. **Check Correctness**
   - Logic errors
   - Edge cases
   - Error handling

3. **Evaluate Style**
   - Naming conventions
   - Code organization
   - Comments and documentation

4. **Assess Performance**
   - Algorithmic complexity
   - Resource usage
   - Optimization opportunities

5. **Provide Feedback**
   - Prioritize issues (critical → minor)
   - Suggest specific improvements
   - Explain reasoning
```

### Example 4: Deep References vs. Flat Structure

❌ **Before:**

```
skill/
├── SKILL.md → "See advanced.md for details"
└── advanced.md → "See appendix.md for examples"
    └── appendix.md → actual content
```

✅ **After:**

```
skill/
├── SKILL.md (overview + workflow)
├── reference.md (detailed docs)
└── examples.md (practical examples)
```

---

## Key Takeaways

1. **Simple skills** (< 200 lines) → Single SKILL.md file
2. **Medium skills** (200-500 lines) → SKILL.md + reference.md
3. **Complex skills** (> 500 lines or scripts) → Full structure with progressive disclosure
4. **Always** provide clear workflows, not just descriptions
5. **Always** include practical examples
6. **Always** keep SKILL.md under 500 lines
7. **Trust Claude's intelligence** - be concise

Use these examples as templates for your own skills!
