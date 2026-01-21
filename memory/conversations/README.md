# Conversations Memory

This directory contains **interaction history** between you and the agent. This enables the agent to maintain context across multiple interactions and learn from past discussions.

## Purpose

- Remember past conversations for context
- Track feedback patterns over time
- Enable conversational continuity
- Build relationship context with users

## What Goes Here

The agent **automatically writes** to this directory:
- PR comment threads and discussions
- Issue conversations and resolutions
- Feedback received and how it was addressed
- Decision rationale and outcomes

## Structure

Conversations are organized by date and interaction type:

```
conversations/
├── 2025-11/
│   ├── pr-123-marketing-post-iteration.md
│   ├── pr-124-medium-article-feedback.md
│   ├── issue-45-content-request.md
│   └── ...
├── 2025-12/
│   └── ...
└── archive/
    └── 2025-10/
```

## Usage

**Writing** (automatic):
- Workflows save conversation context when processing feedback
- Includes original request, agent response, user feedback, final outcome

**Reading** (optional):
- Agent can reference past conversations for context
- Learn from previous feedback patterns
- Understand user communication preferences

## Entry Format

Each conversation file includes:
```markdown
# [Type] #[Number]: [Title]

**Date**: YYYY-MM-DD
**Skill**: [skill-name]
**Status**: [open/resolved]

## Original Request
[What was asked]

## Agent Response
[What the agent did]

## User Feedback
[What feedback was provided]

## Final Outcome
[How it was resolved]

## Learnings
[What was learned from this interaction]
```

---

**Note**: This directory is **dynamically populated** by workflows. You may want to periodically archive old conversations to keep the active set manageable.

## .gitignore Consideration

Depending on your needs, you might want to:
- **Commit conversations**: Keep full history in Git (good for learning continuity)
- **Ignore conversations**: Keep them local only (good for privacy)

Currently: **Committed** (agent learns from history across sessions)
