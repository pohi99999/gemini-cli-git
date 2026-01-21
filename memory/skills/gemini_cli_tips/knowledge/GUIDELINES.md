# Gemini CLI Tips Skill

## Purpose

This skill analyzes the [Gemini CLI](https://github.com/google-gemini/gemini-cli) repository and generates daily tips, insights, and best practices for using Gemini CLI effectively.

**Example use case**: Daily tips on Gemini CLI features, configuration options, MCP server integrations, extensions, and productivity patterns.

## Skill Overview

This skill shows you how to:
- Clone and analyze the Gemini CLI repository
- Extract useful features and capabilities
- Identify productivity patterns and best practices
- Generate educational content about Gemini CLI usage
- Provide actionable tips for developers

## How to Execute This Skill

### 1. Repository Setup

Clone or update the Gemini CLI repository to analyze it:

```bash
# Define local clone location
REPO_DIR="/tmp/gemini-cli"

# Clone or update the repository
if [ -d "$REPO_DIR" ]; then
  cd "$REPO_DIR"
  git pull origin main
else
  git clone https://github.com/google-gemini/gemini-cli "$REPO_DIR"
fi

cd "$REPO_DIR"
```

### 2. Analysis Guidelines

When analyzing Gemini CLI:

**Focus Areas:**
- CLI commands and usage patterns
- Configuration options and settings
- MCP server integrations
- Extension system and available extensions
- Productivity features and shortcuts
- Tool capabilities and use cases
- Advanced features and customization
- Integration with development workflows
- Documentation and examples
- Recent updates and new features

**What to Extract:**
- Practical command examples
- Configuration patterns and best practices
- MCP server setup examples
- Extension installation and usage
- Hidden or lesser-known features
- Workflow optimization tips
- Common use cases and solutions
- Performance and efficiency tips

**What to Avoid:**
- Overly complex technical details without context
- Outdated information (always check latest main branch)
- Assumptions about user's setup or environment
- Recommending deprecated features or commands

### 3. Daily Tip Structure

Generate a daily tip following this structure:

```markdown
# Gemini CLI Daily Tip - [Date]

## Today's Tip: [Catchy Title]

### Overview
[2-3 sentence introduction explaining what this tip is about]

### The Feature/Pattern
[Detailed explanation of the feature, command, or best practice]

**Example Usage:**
```bash
[Relevant CLI command or code snippet]
```

**Configuration (if applicable):**
```json
[Relevant configuration from settings.json]
```

### Why This Matters
[Explain the benefits and practical applications]

### How to Use It
[Step-by-step guide or practical application]

1. [Step 1]
2. [Step 2]
3. [Step 3]

### Pro Tips
- [Additional tip or variation]
- [Common pitfall to avoid]
- [Related feature or workflow]

### Related Features
- [Related command or feature]
- [Documentation link]
- [MCP server or extension if relevant]

### Quick Takeaway
[One-liner summary that captures the essence of the tip]

---
*Source: [Link to relevant file/section in Gemini CLI repo or docs]*
*Generated on: [Date]*
```

### 4. Tip Selection Strategy

To ensure variety and educational value:

**Rotation Categories:**
1. **Basic Commands** (e.g., essential CLI operations)
2. **Configuration** (e.g., settings.json options)
3. **MCP Servers** (e.g., integrating external tools)
4. **Extensions** (e.g., available extensions and how to use them)
5. **Advanced Features** (e.g., custom prompts, hooks, workflows)
6. **Productivity Tips** (e.g., shortcuts, aliases, efficiency hacks)
7. **Integration Patterns** (e.g., CI/CD, development workflows)

**Selection Method:**
- Track previously covered tips in a metadata file
- Rotate through categories to ensure variety
- Prioritize recent changes or updates to the repository
- Focus on practical, immediately applicable knowledge
- Balance beginner and advanced topics
- Consider common user questions and pain points

### 5. Quality Standards

**Accuracy:**
- ✅ Verify all commands work with current version
- ✅ Test command examples for correctness
- ✅ Link directly to official documentation
- ✅ Mention version if feature is version-specific
- ✅ Check that MCP servers and extensions actually exist

**Clarity:**
- ✅ Use clear, beginner-friendly language
- ✅ Explain technical terms when first used
- ✅ Provide context for why something matters
- ❌ Don't assume deep CLI or Gemini knowledge

**Practicality:**
- ✅ Include working command examples
- ✅ Provide step-by-step instructions
- ✅ Link to official documentation
- ✅ Show real-world use cases
- ❌ Don't share theoretical concepts without application

**Engagement:**
- ✅ Use catchy, descriptive titles
- ✅ Start with the "why" before the "how"
- ✅ Include quick takeaways
- ✅ Add pro tips for advanced users
- ❌ Don't be overly technical or dry

## Output Requirements

### File Naming
Use descriptive, timestamped filenames:
- Format: `YYYY-MM-DD-tip.md`
- Example: `2025-11-22-tip.md`

### Location
Save all tips to: `memory/skills/gemini_cli_tips/output/`

### Metadata Tracking
Maintain a metadata file to track covered topics:
- File: `memory/skills/gemini_cli_tips/output/tip-history.json`
- Structure:
```json
{
  "tips": [
    {
      "date": "2025-11-22",
      "category": "MCP Servers",
      "title": "Integrating Slack with Gemini CLI",
      "file_reference": "docs/tools/mcp-server.md",
      "topics": ["mcp", "slack", "integration"]
    }
  ]
}
```

### Format
- Use Markdown format
- Include metadata (date, source links, category)
- Follow the structure template above
- Ensure code blocks have proper syntax highlighting
- Keep it readable and well-formatted

## When to Skip Execution

Skip tip generation if:
- Repository clone/update fails (network issues)
- No new content available that hasn't been covered recently (check tip-history)
- Repository has been archived or moved
- Less than 7 days since a tip on the same specific topic was generated

## Example Workflow

1. **Clone/update repository** from GitHub
2. **Review recent changes** using git log
3. **Check tip history** to avoid repetition
4. **Select category** for today (rotate through categories)
5. **Identify useful feature** in that category
6. **Extract command/configuration example** from repository or docs
7. **Generate tip** using the template structure
8. **Update tip history** with new entry
9. **Save to output directory** with proper filename
10. **Quality check** against standards above

## Tips for Success

- Start each tip with a compelling "why this matters"
- Use real commands that users can try immediately
- Link directly to official docs for deeper exploration
- Keep tips focused (one main concept per tip)
- Make examples copy-pasteable
- Include both the command and the explanation
- Vary difficulty levels across weeks
- Highlight lesser-known features
- Show practical workflow integrations

## Common Pitfalls to Avoid

- ❌ Covering the same topic too frequently
- ❌ Using outdated commands or syntax
- ❌ Making tips too long or complex
- ❌ Not providing enough context
- ❌ Ignoring beginner-friendly topics
- ❌ Forgetting to link to official documentation
- ❌ Not testing if commands actually work
- ❌ Recommending non-existent MCP servers or extensions

## Integration with Demands

This skill is referenced by demand files via frontmatter:

```yaml
---
skill: gemini_cli_tips
---
```

The demand file specifies WHEN to run (daily schedule) and any specific focus areas. This skill defines HOW to analyze the repository and generate tips.

## Additional Resources

When generating tips, consider linking to:
- [Gemini CLI Repository](https://github.com/google-gemini/gemini-cli)
- [Gemini CLI Documentation](https://github.com/google-gemini/gemini-cli/tree/main/docs)
- [MCP Server Documentation](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md)
- [Extensions Documentation](https://github.com/google-gemini/gemini-cli/blob/main/docs/extensions.md)
- [Gemini API Documentation](https://ai.google.dev/docs)
- Awesome MCP Servers list
- Community extensions and tools
