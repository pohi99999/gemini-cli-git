# Global Context Memory

This directory contains **shared knowledge** that all skills can access. Think of this as the agent's general knowledge base that applies across all specialized areas.

## Purpose

- Provides context that doesn't belong to a specific skill
- Shared guidelines, patterns, and reference material
- Project-wide information that informs all agent actions

## What Goes Here

- **Project information**: Mission, goals, target audience
- **Team guidelines**: Communication style, values, principles
- **Common patterns**: Reusable approaches across skills
- **Reference material**: Links, resources, documentation

## Usage

Workflows read from this directory to understand:
- Who the project is for
- What the overall goals are
- How to communicate and behave
- Common patterns to apply

## Files in This Directory

### workflow-guidelines.md ⚠️ **CRITICAL**
**Universal rules for working within GitHub Actions workflows.**

All skills MUST read this file before executing tasks. Contains:
- What git operations are forbidden (workflows handle these)
- How to properly write files
- The correct workflow execution model
- Common pitfalls to avoid

**Every skill prompt should reference this file.**

## Example Files (To Be Added)

- `project-info.md` - About the project, mission, audience
- `communication-style.md` - How to write, tone, voice
- `team-values.md` - Guiding principles
- `useful-resources.md` - Links, references, tools

---

**Note**: This is **manually curated** knowledge. Add files here when you want all skills to have access to specific context.
