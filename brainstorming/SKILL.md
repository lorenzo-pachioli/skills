---
name: brainstorming
description: Use before any creative work - creating features, building components, adding functionality, or modifying behavior. Explores user intent, requirements, and design through collaborative dialogue before implementation.
---

# Brainstorming Ideas Into Designs

## Overview

Help turn ideas into fully formed designs and specifications through natural collaborative dialogue.

Start by understanding the current project context, then ask questions one at a time to refine the idea. Once you understand what you're building, present the design in small sections (200-300 words), checking after each section whether it looks right so far.

## When to Use

Use this skill when:

- Starting a new feature or component
- User requests functionality changes or additions
- Beginning any creative or design work
- Need to explore requirements before coding
- Unclear about the full scope or approach

## The Process

### Understanding the Idea

1. **Check current project state first**
   - Review relevant files, documentation, recent changes
   - Understand existing architecture and patterns

2. **Ask questions one at a time to refine the idea**
   - Only one question per message
   - Prefer multiple choice questions when possible
   - Open-ended questions are fine when needed
   - If a topic needs more exploration, break it into multiple questions

3. **Focus on understanding:**
   - Purpose: What problem does this solve?
   - Constraints: Technical, time, or resource limitations
   - Success criteria: How do we know it works?

### Exploring Approaches

1. **Propose 2-3 different approaches with trade-offs**
   - Present options conversationally
   - Lead with your recommended option
   - Explain reasoning and trade-offs clearly

2. **Example format:**
   > "I see three approaches here:
   >
   > **Option 1 (Recommended): [Approach]**
   >
   > - Pros: [benefits]
   > - Cons: [drawbacks]
   > - Why I recommend it: [reasoning]
   >
   > **Option 2: [Alternative]**
   >
   > - Pros: [benefits]
   > - Cons: [drawbacks]
   >
   > **Option 3: [Another alternative]**
   >
   > - Pros: [benefits]
   > - Cons: [drawbacks]"

### Presenting the Design

1. **Once you understand what you're building, present the design**
   - Break it into sections of 200-300 words
   - Ask after each section whether it looks right so far
   - Be ready to go back and clarify if something doesn't make sense

2. **Cover these aspects:**
   - Architecture overview
   - Key components and their responsibilities
   - Data flow and interactions
   - Error handling approach
   - Testing strategy

## After the Design

### Documentation

1. **Write the validated design to a file**
   - Save to appropriate location (e.g., `docs/designs/YYYY-MM-DD-<topic>-design.md`)
   - Use clear, concise language
   - Include diagrams or examples where helpful

2. **Commit the design document**
   - Add to version control for future reference

### Implementation

1. **Ask: "Ready to proceed with implementation?"**

2. **If yes, transition to implementation planning:**
   - Create detailed implementation plan
   - Break down into specific tasks
   - Identify files to create/modify
   - Define testing approach

## Key Principles

- **One question at a time** - Don't overwhelm with multiple questions
- **Multiple choice preferred** - Easier to answer than open-ended when possible
- **YAGNI ruthlessly** - Remove unnecessary features from all designs (You Aren't Gonna Need It)
- **Explore alternatives** - Always propose 2-3 approaches before settling
- **Incremental validation** - Present design in sections, validate each
- **Be flexible** - Go back and clarify when something doesn't make sense
- **User-focused** - Keep the end user's needs central to all decisions

## Example Flow

```
1. Review project → 2. Ask clarifying questions (one at a time) →
3. Propose approaches → 4. Present design (in sections) →
5. Document design → 6. Plan implementation
```

## Anti-Patterns to Avoid

❌ Asking multiple questions at once
❌ Jumping to implementation without exploring alternatives
❌ Presenting entire design at once without validation
❌ Adding features "just in case" (violates YAGNI)
❌ Assuming requirements without asking
❌ Skipping documentation step
