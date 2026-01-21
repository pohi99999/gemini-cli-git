---
skill: repo_health_check
---

# Task: Daily Health Check for mcp-brunella-core

## Role of this Demand File

This file defines the **WHAT** and the **WHEN** of the task.
- **WHAT**: Daily health check to ensure all processes in the mcp-brunella-core repository are working correctly
- **WHEN**: Every day at 22:00 (10 PM) UTC

The **HOW** is defined in the `repo_health_check` skill's guidelines.

## Task Instructions

Perform a comprehensive health check of the [mcp-brunella-core](https://github.com/[OWNER]/mcp-brunella-core) repository to identify any problems and provide actionable suggestions for fixes.

### Specifics

- **Target Repository**: https://github.com/[OWNER]/mcp-brunella-core
  - Note: Update [OWNER] with the actual repository owner/organization
- **Analysis Approach**: Clone/update the repository and perform comprehensive health checks
- **Output Location**: `memory/skills/repo_health_check/output/`
- **Output Filename**: Use format `YYYY-MM-DD-health-check.md` where date is the check execution date
- **Metadata File**: `memory/skills/repo_health_check/output/health-history.json`

### What to Check

Following the `repo_health_check` skill guidelines, perform checks in these areas:

1. **Build Status**
   - Check if the project builds successfully
   - Identify any build errors or warnings
   - Review build configuration files
   - Test build commands

2. **Test Status**
   - Run existing test suites if available
   - Check test coverage
   - Identify failing or flaky tests
   - Review test configuration

3. **Dependencies**
   - Check for outdated dependencies
   - Identify security vulnerabilities in dependencies
   - Review dependency update needs
   - Check for deprecated packages

4. **Code Quality**
   - Run linters if configured
   - Check code style consistency
   - Identify potential bugs or anti-patterns
   - Review code structure

5. **GitHub Actions/CI**
   - Review recent workflow runs
   - Check for failing workflows
   - Identify workflows that haven't run recently
   - Analyze workflow configuration

6. **Repository Health**
   - Check for stale branches
   - Review open PRs that need attention
   - Identify issues that need triage
   - Check for outdated documentation

7. **Security**
   - Check for security vulnerabilities
   - Review security advisories
   - Check for exposed secrets or credentials
   - Review security best practices

### What to Generate

Following the `repo_health_check` skill guidelines, create a health report that includes:

1. **Executive Summary**
   - Overall health status (Healthy/Issues/Critical)
   - Key findings summary
   - Quick overview of major issues

2. **Detailed Results**
   - Status for each health check area
   - Specific findings with context
   - Metrics and measurements

3. **Issues Found**
   - Clear description of each issue
   - Severity level (Critical/High/Medium/Low)
   - Impact analysis
   - **Actionable suggestions** with step-by-step solutions
   - Commands and code examples for fixes
   - Links to relevant documentation

4. **Recommendations**
   - Prioritized list of actions to take
   - Estimated effort for each recommendation
   - Resources and references

5. **Metadata Updates**
   - Update health-history.json with the check results
   - Track trends over time
   - Record key findings

### Quality Requirements

Follow all guidelines from `memory/skills/repo_health_check/knowledge/GUIDELINES.md`:
- Verify all issues found are real problems
- Provide clear, actionable solutions
- Include working commands and examples
- Link to relevant documentation
- Prioritize by severity and impact
- Be specific about impacts and risks
- Make suggestions copy-pasteable

### Skip Conditions

Skip execution if:
- **Repository unavailable**: Cannot clone or update the repository (network issues, access denied, repo deleted/archived)
- **Recent check**: A health check was completed within the last 6 hours
- **Maintenance mode**: Repository is in declared maintenance mode
- **System issues**: Git or file system errors prevent execution

When skipping, explain why in the workflow logs.

### Success Criteria

A successful execution produces:
- ✅ Comprehensive health report covering all check areas
- ✅ Clear identification of issues with severity levels
- ✅ Actionable suggestions with step-by-step solutions
- ✅ Working commands and examples for fixes
- ✅ Updated health-history.json with metadata
- ✅ Saved to correct location with proper filename
- ✅ Follows the skill's quality standards
- ✅ Provides value for maintaining repository health

### Important Notes

1. **Focus on Actionability**: Every issue found should have a clear, actionable solution
2. **Prioritize**: Focus on critical and high-priority issues first
3. **Be Specific**: Provide exact commands and steps to fix issues
4. **Verify**: Test suggested solutions when possible
5. **Context**: Explain why each issue matters and its impact
6. **Resources**: Link to relevant documentation and resources
7. **Trends**: Track health over time using the health-history.json file

### Example Output Structure

The health report should follow this general structure:

```markdown
# Repository Health Check - 2025-11-22

## Repository: mcp-brunella-core

**Last Checked:** 2025-11-22 22:00:00 UTC
**Status:** ⚠️ Issues Found

## Executive Summary

Found 3 issues requiring attention: 2 high-priority and 1 medium-priority...

## Health Check Results

### ✅ Build Status
...

### ⚠️ Dependencies
Found 5 outdated dependencies, including 1 with known security vulnerability...

## 🔍 Issues Found

### Issue 1: Security Vulnerability in Dependency
**Severity:** High
...
**Suggested Solution:**
1. Update the package to version X.Y.Z
2. Run: `npm update package-name@X.Y.Z`
...

## 💡 Recommendations
...
```

---

**Note**: This demand runs daily at 22:00 UTC to proactively monitor repository health and catch issues early. The agent performs comprehensive checks and provides actionable suggestions to maintain code quality, security, and overall project health.
