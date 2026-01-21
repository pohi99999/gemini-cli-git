# Repository Health Check Skill

## Overview

This skill performs automated health checks on repositories to identify problems and provide actionable suggestions for fixes.

## Purpose

The skill is designed to:
- Monitor repository health on a scheduled basis
- Check build status, test status, dependencies, code quality, and more
- Identify issues and problems proactively
- Provide step-by-step suggestions for fixing issues
- Track health trends over time

## Usage

This skill is used by the `mcp-brunella-health-daily` demand, which runs daily at 22:00 UTC to check the health of the `mcp-brunella-core` repository.

### How It Works

1. **Schedule**: The workflow runs automatically at 22:00 UTC daily
2. **Execution**: The agent clones/updates the target repository
3. **Analysis**: Performs comprehensive health checks across multiple areas
4. **Reporting**: Generates a detailed health report with findings and suggestions
5. **PR Creation**: If issues are found, a PR is created with the health report

### What It Checks

- **Build Status**: Verifies the project builds successfully
- **Test Status**: Runs tests and checks coverage
- **Dependencies**: Identifies outdated packages and vulnerabilities
- **Code Quality**: Checks linting and code style
- **CI/CD**: Reviews GitHub Actions workflow status
- **Repository Health**: Checks for stale branches and PRs
- **Security**: Identifies security vulnerabilities and advisories

### Output

Health check reports are saved to:
- **Location**: `memory/skills/repo_health_check/output/`
- **Format**: `YYYY-MM-DD-health-check.md`
- **Metadata**: `health-history.json` tracks trends over time

## Configuration

### Target Repository

The target repository is specified in the demand file (`memory/demands/mcp-brunella-health-daily.md`). To monitor a different repository:

1. Edit the demand file
2. Update the `Target Repository` URL
3. Update the repository owner/organization
4. Commit the changes

### Schedule

The schedule is configured in `.github/workflows/agent-scheduler.yml`:

```yaml
schedule:
  - cron: '0 22 * * *'  # 10 PM UTC daily
```

To change the schedule, edit the cron expression. Use [crontab.guru](https://crontab.guru/) for help.

### Skip Conditions

The health check will be skipped if:
- Repository cannot be accessed (network issues, access denied)
- Repository has been archived or deleted
- Previous check completed within last 6 hours
- Repository is in maintenance mode

## Manual Execution

To manually trigger a health check:

```bash
gh workflow run agent-scheduler.yml -f demand=mcp-brunella-health-daily
```

Or use the GitHub Actions UI to manually trigger the workflow.

## Extending the Skill

To customize the health checks:

1. Edit `memory/skills/repo_health_check/knowledge/GUIDELINES.md`
2. Add or modify health check areas
3. Update the report structure
4. Commit the changes

The agent will automatically use the updated guidelines in the next run.

## Example Report

A typical health check report includes:

- Executive summary with overall status
- Detailed results for each check area
- List of issues found with severity levels
- Actionable suggestions with commands to fix
- Metrics and trends
- Links to relevant documentation

## Integration

This skill integrates with:
- GitHub Actions for scheduled execution
- GitHub API for workflow status and repository information
- Git for repository cloning and analysis
- Build tools (npm, pip, make, etc.) for testing
- Linters and code quality tools

## Troubleshooting

### No PR Created

If no PR is created after execution:
- Check workflow logs for reasoning
- Verify the target repository is accessible
- Ensure GEMINI_API_KEY is configured
- Check skip conditions in the logs

### Workflow Fails

If the workflow fails:
- Verify GEMINI_API_KEY is set correctly
- Check repository permissions
- Review workflow logs for specific errors
- Ensure the target repository exists

### False Positives

If health checks report false issues:
- Review the GUIDELINES.md for accuracy
- Update detection logic if needed
- Add skip conditions for known non-issues

## License

This skill is part of the gemini-cli-git template and follows the same Apache License 2.0.
