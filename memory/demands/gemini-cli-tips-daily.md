---
skill: gemini_cli_tips
---

# Task: Daily Gemini CLI Tips

## Role of this Demand File

This file defines the **WHAT** and the **WHEN** of the task.
- **WHAT**: Generate a daily tip about Gemini CLI features and best practices
- **WHEN**: Determined by the scheduling configuration (daily execution)

The **HOW** is defined in the `gemini_cli_tips` skill's guidelines.

## Task Instructions

Analyze the [Gemini CLI](https://github.com/google-gemini/gemini-cli) repository and generate a practical, educational daily tip for developers using Gemini CLI.

### Specifics

- **Target Repository**: https://github.com/google-gemini/gemini-cli
- **Analysis Approach**: Clone/update the repository and analyze current codebase and documentation
- **Output Location**: `memory/skills/gemini_cli_tips/output/`
- **Output Filename**: Use format `YYYY-MM-DD-tip.md` where date is the tip generation date
- **Metadata File**: `memory/skills/gemini_cli_tips/output/tip-history.json`

### What to Generate

Following the `gemini_cli_tips` skill guidelines, create a daily tip that includes:

1. **Tip Selection**
   - Rotate through categories (Basic Commands, Configuration, MCP Servers, Extensions, Advanced Features, Productivity Tips, Integration Patterns)
   - Check tip-history.json to avoid repetition
   - Prioritize recent changes or updates in the repository
   - Balance beginner and advanced topics

2. **Content Structure**
   - Catchy, descriptive title
   - Clear overview (2-3 sentences)
   - Detailed explanation of the feature/command/pattern
   - Working command examples or configuration snippets
   - "Why This Matters" section
   - Step-by-step "How to Use It" guide
   - Pro tips and related features
   - Quick takeaway one-liner

3. **Quality Requirements**
   - Use actual commands/configs from the latest version
   - Link directly to official documentation
   - Provide practical, actionable advice
   - Keep language clear and beginner-friendly
   - Ensure examples are tested and correct

4. **Metadata Updates**
   - Update tip-history.json with the new tip
   - Increment category rotation index
   - Track topics covered

### Quality Requirements

Follow all guidelines from `memory/skills/gemini_cli_tips/knowledge/GUIDELINES.md`:
- Use the standard tip structure
- Ensure accuracy of commands and configurations
- Provide both context and practical application
- Make it engaging and educational
- Link to official Gemini CLI documentation

### Skip Conditions

Skip execution if:
- **Repository unavailable**: Cannot clone or update the repository (network issues, repo moved/archived)
- **Recent duplicate**: A tip on the same specific topic was generated within the last 7 days
- **No new content**: All available topics have been covered recently (review tip-history)
- **System issues**: Git or file system errors prevent execution

When skipping, explain why in the workflow logs.

### Success Criteria

A successful execution produces:
- ✅ Well-formatted Markdown tip file
- ✅ Practical command/configuration examples
- ✅ Clear explanations and step-by-step guidance
- ✅ Updated tip-history.json with metadata
- ✅ Saved to correct location with proper filename
- ✅ Follows the skill's quality standards
- ✅ Provides educational value to Gemini CLI users

---

**Note**: This demand runs daily to provide continuous learning opportunities. The agent rotates through different categories and topics to ensure variety and comprehensive coverage of Gemini CLI features and capabilities.
