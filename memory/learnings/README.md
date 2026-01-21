# Learnings Memory

This directory contains **insights and patterns** that the agent extracts over time. This is where the agent becomes smarter through experience.

## Purpose

- Record what works and what doesn't
- Capture patterns discovered during execution
- Enable self-improvement through reflection
- Build institutional knowledge automatically

## What Goes Here

The agent can write to this directory to record:
- **Successful patterns**: Approaches that led to good outcomes
- **Mistakes to avoid**: What didn't work and why
- **Optimizations**: Performance improvements discovered
- **User preferences**: Patterns in feedback received
- **Meta-insights**: Learnings about learning

## Usage

**Writing**: Workflows can append to learnings when they:
- Receive positive feedback on outputs
- Identify a repeated pattern
- Notice something that could be optimized
- Make a mistake worth remembering

**Reading**: Before generating output, the agent reads learnings to:
- Apply successful patterns
- Avoid past mistakes
- Incorporate user preferences
- Build on previous insights

## Example Files

- `what-works.md` - Successful patterns and approaches
- `user-preferences.md` - Learned preferences from feedback
- `common-mistakes.md` - Errors to avoid
- `optimizations.md` - Performance improvements
- `meta-learnings.md` - Insights about the learning process

## Format

Entries should include:
- **Date**: When the learning occurred
- **Context**: What triggered this insight
- **Learning**: The actual insight or pattern
- **Application**: How to use this in future

Example:
```markdown
## 2025-11-03: LinkedIn posts under 1400 chars get better engagement

**Context**: Received feedback that post was too long
**Learning**: Sweet spot is 1200-1400 characters for LinkedIn
**Application**: Aim for this range in future LinkedIn content
```

---

**Note**: This is **dynamically populated** by the agent. You can also manually add learnings you want the agent to remember.
