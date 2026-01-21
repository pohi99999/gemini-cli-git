<!--
Copyright 2025 Google LLC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->

# gemini-cli-git 🧠 + 📂

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Built with Gemini](https://img.shields.io/badge/Built%20with-Gemini%20CLI-8E75B2)](https://github.com/google-gemini/gemini-cli)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
![Stars](https://img.shields.io/github/stars/eliasecchig/gemini-cli-git?color=yellow)


> **Gemini is the brain. Git is the backend.**

**📋 A template for turning any Git repo into a self-improving autonomous agent.** Click "Use this template" to get started.

## ✨ How It Works

**A simple but effective approach - using Git to interact with your agent:**
- 💬 **Need a task done?** → Open an Issue
- 🔧 **Need to give feedback?** → Comment on the PR
- 🧠 **Need it to learn permanently?** → Merge to `main`
- 📜 **Need to see why it decided something?** → Check the commit history

**Three ways to work:**
- ⏰ **Scheduled** - Cron jobs that run autonomously
- 💬 **On-demand** - Mention `@gemini` in GitHub issues
- 🔧 **Iterative** - Comment on PRs with `@gemini` for refinements

**Key features:**
- **Self-improving** - Can propose changes to its own code
- **Modular skills** - Teach it new capabilities by adding files

**Perfect for:** Anything you can think of! Extend with MCP servers and extensions.

**Example use cases:**<br>
🔍 Code Reviews • 📰 Daily Newsletter • 📝 Auto-sync Documentation • 📊 Weekly Reports • 🌤️ Weather Updates

**Sample included:** This template includes a [working example skill](memory/skills/gemini_cli_tips/) that generates daily tips about Gemini CLI. Use it as a reference for building your own skills!

**💬 Interactive mode:** You can also use [Gemini CLI](https://github.com/google-gemini/gemini-cli) in this same repo for real-time chat (`npm install -g @google/gemini-cli && gemini`). Autonomous for scheduled tasks, interactive for quick questions.

## 🚀 Quick Start

### 1. Use This Template

Click **"Use this template"** at the top of this page to create your own repository.

> 💡 **Tip:** You can create a **private repository** if you want to keep your agent's work confidential.

### 2. Get Gemini API Key

1. Visit [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Create API key → Copy it

### 3. Setup GitHub Secret

```bash
Settings → Secrets and variables → Actions → New repository secret
Name: GEMINI_API_KEY
Value: <your-api-key>
```

<details>
<summary>Or via CLI</summary>

```bash
gh secret set GEMINI_API_KEY
# Paste your key when prompted
```
</details>

### 4. Enable GitHub Actions Permissions

**Required for agent to create PRs:**

```bash
Settings → Actions → General → Workflow permissions
✓ Read and write permissions
✓ Allow GitHub Actions to create and approve pull requests
```

<details>
<summary>Or via CLI</summary>

```bash
gh api -X PUT /repos/:owner/:repo/actions/permissions/workflow \
  -f default_workflow_permissions=write \
  -F can_approve_pull_request_reviews=true
```
</details>

### 5. Create Your Own Skill

**Open an issue (any title) with `@gemini`:**

```
@gemini create a skill called "ai-news-digest" that generates a daily report of
interesting AI news using Google Search. Include a daily demand that runs each morning.
```

The agent will create a PR with the skill structure, guidelines, and demand file. Review, merge, and you're done! 🎉

<details>
<summary>Or use Gemini CLI directly</summary>

```bash
cd gemini-cli-git && gemini
```

Then describe the skill you want to create.

</details>

## 🧠 Understanding Agent Memory

This system uses Git history as persistent memory:

**Skills** (`memory/skills/`)
- Long-term knowledge (how to do things)
- Reusable expertise and guidelines
- Quality standards and best practices

**Learnings** (`memory/learnings/`)
- Insights from past executions
- Patterns and optimizations discovered
- Lessons to apply in future runs

**Conversations** (`memory/conversations/`)
- Multi-turn interaction context
- Maintains continuity across requests
- Tracks state for complex workflows

Every commit is a memory snapshot. The agent can:
- ✅ Learn from past mistakes (via learnings)
- ✅ Improve skills over time (via commits to knowledge)
- ✅ Maintain conversation context (via conversations)

## 🎯 How It Works

### Scheduled Execution (Daily/Weekly/etc.)

```
Cron Trigger
    ↓
Discover Demands
    ↓
For Each Demand:
    ↓
Read Demand File (specifies skill needed)
    ↓
Load Skill Knowledge
    ↓
Execute Demand Instructions
    ↓
Changes Made? ──→ Yes ──→ Create PR
    ↓
    No ──→ Skip
```

**Example**: `gemini-cli-tips-daily` demand runs daily, analyzing the Gemini CLI repository and creating a PR with an educational tip.

### On-Demand via Issues

```
User Creates Issue with @gemini
    ↓
Parse Request
    ↓
Identify Skills Needed
    ↓
Load Skill Knowledge
    ↓
Execute Request
    ↓
Create PR
    ↓
Comment on Issue with PR Link
```

**Example**: "Hey `@gemini`, generate a tip about using MCP servers with Gemini CLI"

### PR Iteration

```
User Comments "@gemini make this more concise"
    ↓
Checkout PR Branch
    ↓
Read Feedback + Current Files
    ↓
Apply Skill Knowledge
    ↓
Commit Changes to PR
    ↓
Comment Confirmation
```

## 🛠️ Customization

### Change Schedule

Edit `.github/workflows/agent-scheduler.yml`:
```yaml
on:
  schedule:
    - cron: '0 9 * * 1'  # 9 AM UTC every Monday
```

Use [crontab.guru](https://crontab.guru/) for custom schedules.

### Modify Skill Knowledge

Edit skill guidelines like `memory/skills/gemini_cli_tips/knowledge/GUIDELINES.md` to change:
- Execution methodology
- Quality standards
- Output requirements
- Best practices

Changes apply immediately to all future executions!

### Add MCP Servers or Extensions (Optional)

Extend the agent with external integrations like Slack, databases, browser automation, and more using MCP (Model Context Protocol) servers or Gemini CLI extensions.

**Note**: Gemini CLI already has native Google Search and filesystem access built-in.

**See `.gemini/README.md` for complete documentation** on:
- Adding MCP servers (Slack, PostgreSQL, Google Drive, etc.)
- Installing Gemini CLI extensions
- Configuring API keys and environment variables
- Examples of common integrations

### Add New Skills or Demands

**Easiest: Open an issue with `@gemini`**

```
@gemini create a skill called "code-review" that checks for security issues and code quality.
Also create a daily demand for it.
```

The agent creates a PR with everything ready to review and merge!

---

**Alternative methods:**

<details>
<summary>Use Gemini CLI directly</summary>

```bash
cd gemini-cli-git && gemini
```

Then describe the skill/demand you want to create. Gemini CLI will scaffold the files interactively.

</details>

<details>
<summary>Manual setup</summary>

**Create a skill:**
```bash
mkdir -p memory/skills/my-skill/{knowledge,output}
cat > memory/skills/my-skill/knowledge/GUIDELINES.md <<EOF
# Guidelines for my skill
EOF
```

**Create a demand:**
```bash
cat > memory/demands/my-demand.md <<EOF
---
skill: my-skill
---
Task instructions here...
EOF
```

Skills and demands are auto-discovered - no config needed!

</details>

---

<details>
<summary>📖 Usage Examples</summary>

### Request Task via Issue

```
Title: Task Request
Body: @gemini analyze our repository's PR merge time trends over the past 3 months
```

Agent will parse the request, load relevant skills, execute the task, and create a PR.

### Refine Content via PR Comment

```
@gemini this report is too technical, make it more accessible to non-developers
```

Agent will read your feedback, apply changes, commit to the PR, and comment confirmation.

### Scheduled Execution

Runs automatically based on cron schedule:
- Executes each demand in `memory/demands/`
- Creates PRs only if changes made
- Each demand specifies its required skill(s)

</details>

<details>
<summary>🐛 Troubleshooting</summary>

### No PR Created

**Possible reasons:**
- No changes detected (check logs for reasoning)
- Content not deemed worthy (demand decides)
- Error in execution (check workflow logs)
- Skip conditions met (e.g., no activity threshold)

**Debug**: Check workflow run logs for agent's reasoning

### `@gemini` Not Responding

**Checklist:**
- ✓ Comment starts with exactly `@gemini`
- ✓ Workflow permissions are correct (see Quick Start #3)
- ✓ `GEMINI_API_KEY` secret exists
- ✓ GitHub Actions are enabled for the repository

### Workflow Fails with Error

Check the improved error messages in workflow logs. Common issues:
1. **Invalid API key** - Verify `GEMINI_API_KEY` is set correctly
2. **Rate limits** - Check quota at [Google AI Studio](https://aistudio.google.com/)
3. **Permissions** - Ensure workflow has write permissions
4. **Syntax errors** - Verify YAML frontmatter in demand files

### Rate Limits

**Solutions:**
- Reduce schedule frequency (weekly instead of daily)
- Check Gemini API quota at [AI Studio](https://aistudio.google.com/)
- Consider upgrading to Gemini API Pro
- Optimize prompts to use fewer tokens

</details>

<details>
<summary>🏗️ Architecture Principles</summary>

### No Configuration Files

Skills are just knowledge directories. No YAML config needed!

### Convention Over Configuration

- Skills in `memory/skills/{name}/knowledge/`
- Demands in `memory/demands/{name}.md`
- Outputs in `memory/skills/{name}/output/`

Auto-discovered, zero setup.

### Demands Specify Skills

Each demand file starts with:
```yaml
---
skill: gemini_cli_tips
---
```

The demand knows what it needs. Workflows just execute.

### Workflows Are Generic

Workflows discover demands/skills automatically. No hardcoded business logic. Add new skills without touching workflows!

</details>

## 📚 Learn More

- [Gemini CLI Documentation](https://github.com/google-gemini/gemini-cli)
- [GitHub Actions Docs](https://docs.github.com/en/actions)
- [MCP Server Integration](.gemini/README.md)
- [Contributing Guidelines](CONTRIBUTING.md)

<details>
<summary>📁 Directory Structure</summary>

```
.
├── .github/
│   ├── workflows/
│   │   ├── agent-scheduler.yml    # Executes scheduled demands
│   │   └── agent.yml               # Handles @gemini mentions
│   └── actions/
│       └── run-gemini-cli-cached/  # Custom reusable action with caching (~40s faster)
│
├── memory/                         # 🧠 Agent's long-term memory
│   ├── demands/                    # 📋 Specific tasks to execute
│   │   ├── example-scheduled.md    # Template demand (replace me!)
│   │   └── gemini-cli-tips-daily.md # Example: Daily Gemini CLI tips
│   │
│   ├── skills/                     # 🎯 Specialized knowledge
│   │   ├── example_skill/          # Template skill (replace me!)
│   │   │   ├── knowledge/          # Pure expertise
│   │   │   │   └── GUIDELINES.md
│   │   │   └── output/             # Generated content
│   │   │
│   │   └── gemini_cli_tips/        # Example: Daily Gemini CLI tips
│   │       ├── knowledge/
│   │       │   └── GUIDELINES.md   # How to analyze and generate tips
│   │       └── output/             # Generated tips
│   │
│   ├── context/                    # 📚 Global shared knowledge
│   │   ├── GEMINI.md               # Agent entrypoint & routing
│   │   └── README.md
│   │
│   ├── learnings/                  # 💡 Extracted insights
│   │   └── README.md
│   │
│   └── conversations/              # 💬 Interaction history
│       └── README.md
│
├── CONTRIBUTING.md                 # How to contribute
└── README.md                       # This file
```

</details>

## 🤝 Contributing

This is a **template repository**. Contributions should improve the template for everyone, not add specific skills or use-cases.

**We welcome:**
- Framework improvements
- Bug fixes
- Documentation enhancements
- Developer experience improvements
- New template features

**See [CONTRIBUTING.md](CONTRIBUTING.md)** for guidelines.

## 📄 License

Apache License 2.0 - Use freely for your projects. See [LICENSE](LICENSE) for details.

---

**gemini-cli-git** - Gemini is the brain. Git is the backend.

Built with [Gemini CLI](https://github.com/google-gemini/gemini-cli)
