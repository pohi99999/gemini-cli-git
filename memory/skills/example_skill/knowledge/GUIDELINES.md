# Example Skill Guidelines

This is a template skill to demonstrate the structure of gemini-cli-git.

## Purpose

This skill serves as a reference example for creating your own custom skills.

## How Skills Work

Skills define the **HOW** - they contain specialized knowledge and guidelines for executing specific types of tasks.

## Structure

A skill consists of:

1. **knowledge/** - Contains guidelines, best practices, and domain expertise
   - `GUIDELINES.md` - Core guidelines for executing this skill
   - Additional reference files as needed

2. **output/** - Stores generated artifacts from skill execution
   - Structure depends on your use case
   - Can include subdirectories for organization

## Creating Your Own Skill

1. Create a new directory in `memory/skills/your_skill_name/`
2. Add `knowledge/GUIDELINES.md` with your expertise
3. Create `output/` directory for generated content
4. Reference this skill in your demand files

## Quality Standards

Define your quality standards here:
- Output format requirements
- Validation criteria
- Best practices
- Common pitfalls to avoid

## Example Use Cases

Replace this section with actual instructions for your skill:
- Code review guidelines
- Documentation standards
- Content creation rules
- Testing procedures
- Analytics methodologies

## Integration with Demands

Demands specify **WHAT** to do and **WHEN**. They reference skills in their frontmatter:

```yaml
---
skill: example_skill
---
```

The agent will load these guidelines when executing any demand that requires this skill.
