---
skill: example_skill
---

# Your Mission

This is an example demand file that demonstrates the structure of scheduled tasks.

## What to Do

Replace this section with specific instructions for your task:

**Target/Subject:**
- What resource, location, or data to analyze
- Who is the audience
- What is the expected outcome

**Task Requirements:**
- Specific criteria for the output
- Quality standards to meet
- Data sources to consult
- Output format and location

**Quality Standards:**
Follow all guidelines in `memory/skills/example_skill/knowledge/GUIDELINES.md` for:
- How to execute the task
- Quality criteria
- Output structure
- Best practices

## When to Execute

This demand runs based on the schedule defined in `.github/workflows/agent-scheduler.yml`

## Skip Conditions

Define when to skip execution:
- No changes detected
- Data not available
- Previous run too recent
- Other business logic

## Output Location

Specify where to save the results:
- `memory/skills/example_skill/output/`

Now proceed with executing the task!
