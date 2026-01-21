# Agent Skills Repository

This repository contains a collection of modular skills designed for AI agents. These skills provide structured instructions, workflows, and tools to enhance the capabilities of an AI agent in specific domains.

## Project Organization

The repository is organized by skill folders. Each folder represents a standalone capability and follows a standardized structure:

- **`skill-name/`**: Root directory of the skill.
  - **`SKILL.md`**: (Required) The main instruction file containing the skill's purpose, triggers, and core workflows. It includes a YAML frontmatter with the name and description.
  - **`reference.md`**: (Optional) Detailed documentation, technical specifications, or API references.
  - **`examples.md`**: (Optional) Practical usage examples and before/after scenarios.
  - **`scripts/`**: (Optional) Executable utilities or helper scripts to support the skill's operations.

### Current Skills

- **`analyzing-seo`**: Tools and workflows for auditing and improving website SEO.
- **`brainstorming`**: Structured methods for creative ideation and problem-solving.
- **`debugging-strategies`**: Systematic approaches to identifying and fixing software bugs.
- **`error_handling`**: Best practices for robust error management and reporting.
- **`gemini_skill_creator`**: A meta-skill that provides guidelines for building new skills.
- **`planning`**: Frameworks for breakdown and execution of complex tasks.

## How to Implement a New Skill

To add a new skill to this repository, follow these steps:

1. **Initialize the Directory**: Create a new folder with a descriptive, hyphenated name (e.g., `text-processing`).
2. **Create SKILL.md**: Define the skill name and description in a YAML frontmatter, then outline the core instructions.
3. **Follow the Guidelines**: Use the `gemini_skill_creator` skill as a reference for best practices, including:
   - **Conciseness**: Keep instructions sharp and avoid over-explaining.
   - **Progressive Disclosure**: Move detailed references to `reference.md`.
   - **Clear Workflows**: Provide step-by-step checklists for complex activities.
4. **Link Resources**: If the skill is complex, separate examples and references into their own files.

For more detailed instructions, refer to the [Gemini Skill Creator](gemini_skill_creator/SKILL.md).
