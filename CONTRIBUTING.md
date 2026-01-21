# Contributing to gemini-cli-git

Thank you for your interest in contributing! This is a **template repository** designed to help others build their own autonomous agent systems. Contributions should focus on improving the template itself, not adding specific use-case skills.

## What We're Looking For

### ✅ Great Contributions

- **Framework improvements**: Better agent routing, skill discovery, memory management
- **Workflow enhancements**: More efficient GitHub Actions, better caching, improved error handling
- **Bug fixes**: Issues with the core system, workflows, or agent logic
- **Documentation**: Clearer explanations, better examples, improved getting-started guides
- **Developer experience**: Setup scripts, testing utilities, debugging tools
- **Template features**: New capabilities that benefit all users (e.g., new trigger types, better logging)

### ❌ Not What This Repo Is For

- **Specific skills**: Your custom skills belong in your fork, not the template
- **Use-case specific demands**: These are personal to each implementation
- **Domain-specific content**: Blog posts, company-specific data, etc.

## How to Contribute

### Reporting Bugs

If you find a bug in the template, please open an issue with:
- Clear, descriptive title
- Steps to reproduce
- Expected vs actual behavior
- Environment details (OS, GitHub Actions logs)
- Relevant workflow run logs

### Suggesting Features

Feature suggestions should improve the template for everyone:
- Describe the feature and its benefits
- Explain the use case: how does it help template users?
- Provide implementation ideas if you have them

### Contributing Code

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/your-improvement`
3. **Make your changes** following existing patterns
4. **Test thoroughly**:
   - Run workflows with `gh workflow run`
   - Test on a clean fork if possible
   - Verify documentation changes render correctly
5. **Submit a pull request** with:
   - Clear description of changes
   - Why this improves the template
   - Testing evidence

## Development Guidelines

### Template Philosophy

Remember: users will fork this and customize it. Your changes should:
- ✅ Be generic and reusable
- ✅ Follow convention over configuration
- ✅ Maintain backward compatibility when possible
- ✅ Be well-documented
- ❌ Not hardcode specific business logic
- ❌ Not add dependencies unless absolutely necessary

### Code Standards

- **Workflows**: Keep them generic, use clear variable names, add helpful comments
- **Documentation**: Use clear language, include examples, think "first-time user"
- **Scripts**: Make them portable, handle errors gracefully, provide helpful output
- **Agent logic** (GEMINI.md): Clear instructions, consider edge cases, maintain consistency

### Testing Your Changes

Before submitting a PR:
1. Test workflows using `gh workflow run`
2. Verify on a clean fork if making structural changes
3. Check that documentation renders correctly
4. Ensure no secrets or personal data are included

## Areas Needing Help

We especially welcome contributions in these areas:
- Improved error messages and debugging
- Better first-run experience
- Performance optimizations
- Security enhancements
- Cross-platform compatibility
- Documentation improvements
- Example workflows and tutorials

## Code of Conduct

### Our Standards

- Be respectful and inclusive
- Welcome newcomers
- Provide constructive feedback
- Respect different perspectives

### Unacceptable Behavior

- Harassment or discrimination
- Publishing private information
- Trolling or insulting comments
- Unprofessional conduct

## Questions?

- Check existing issues and documentation
- Open an issue for questions about the template
- Start a discussion for broader topics

## License

By contributing, you agree that your contributions will be licensed under the Apache License 2.0.

---

Thank you for helping make this template better for everyone!
