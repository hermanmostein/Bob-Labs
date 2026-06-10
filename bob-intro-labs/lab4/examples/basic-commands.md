# BobShell Basic Commands Reference

## Overview

This document provides a comprehensive reference for using BobShell with natural language prompts. Use these examples as a starting point for your own automation and workflows.

## Installation and Setup

### Install BobShell

**⚠️ Important for Windows Users:**

BobShell does not auto-install with Bob on Windows. You must install it separately by following the official installation guide:

👉 **[BobShell Installation Guide](https://internal.bob.ibm.com/docs/shell/install-and-setup)**

**For all users**, verify that BobShell is installed:

```bash
# Verify installation
bob --version
```

## Interactive Mode

### Starting Interactive Mode

```bash
# Start interactive session
bob
```

**Note:** Simply typing `bob` starts an interactive BobShell session. See the [BobShell Interactive Mode documentation](https://internal.bob.ibm.com/docs/shell/start-bobshell-interactive) for more details.

### Interactive Mode Examples

```
# General questions
> What is the difference between let and const in JavaScript?

# Code explanation
> Explain this code: function debounce(func, wait) { ... }

# Code generation
> Create a Python function to validate email addresses using regex

# Code review
> Review this function for potential issues: [paste code]

# Refactoring suggestions
> How can I improve this code: [paste code]

# Exit interactive mode
> exit
> quit
> :q

### Using Checkpoints

Checkpoints allow you to save and restore conversation state in interactive mode. Enable checkpointing when starting Bob:

```bash
# Start Bob with checkpointing enabled
bob --checkpointing
```

Or enable it in Bob settings, then start normally with `bob`.

**How to Use Checkpoints:**

Once enabled, Bob automatically saves conversation states. You can naturally reference earlier points:

```
# Work on your code
> Analyze this code for issues
# Bob provides analysis

> Suggest fixes for the issues
# Bob suggests fixes

> Actually, let's go back to the analysis and try a different approach
# Bob restores to the analysis state

> Instead of fixing, suggest a complete refactor
# Bob provides refactoring suggestions
```

**Checkpoint Use Cases:**
- Experiment with different approaches
- Try multiple solution paths
- Return to earlier conversation states
- Explore alternatives without losing progress

```

## Non-Interactive Mode (Natural Language Prompts)

### Help and Information

```bash
# General help
bob --help
bob -h

# Version information
bob --version
bob -v
```

### Code Generation

```bash
# Generate code from description
bob "Create a REST API endpoint for user login"

# Generate and save to file (with clean output)
bob "Create a React component for a todo list" --yolo --hide-intermediary-output > TodoList.jsx

# Generate with specific language (asking Bob to write to file)
bob "Create a sorting algorithm in Python and write it to sort.py" --yolo

# Generate multiple related files (with clean output)
bob "Create a complete Express.js API with routes, controllers, and models for user management" --yolo --hide-intermediary-output > api-structure.txt

# Generate with specific framework (asking Bob to write to file)
bob "Create a Vue 3 component for user profile using Composition API and write it to UserProfile.vue" --yolo
```

### Code Analysis

```bash
# Analyze single file
bob analyze ./src/app.js

# Analyze with specific checks
bob "Analyze ./src/app.js focusing on quality, performance, and security issues"

# Analyze directory recursively
bob "Analyze all files in ./src directory recursively"

# Analyze with output format
bob "Analyze ./src and provide results in JSON format" --hide-intermediary-output > analysis.json
bob "Analyze ./src and provide results in markdown format" --hide-intermediary-output > analysis.md
bob "Analyze ./src and provide results in HTML format" --hide-intermediary-output > analysis.html

# Get specific metrics
bob "Analyze ./src and provide complexity, maintainability, and coverage metrics"

# Analyze with threshold
bob "Analyze ./src and fail if quality score is below 80"
```

### Code Review

```bash
# Review single file
bob review ./src/components/UserForm.jsx

### Code Analysis

```bash
# Analyze a single file
bob "Analyze the code quality and performance of ./src/app.js"

# Analyze entire directory
bob "Analyze all files in ./src recursively for quality issues"

# Get specific metrics
bob "Analyze ./src and provide complexity and maintainability metrics"

# Save analysis to file
bob "Perform a comprehensive code analysis of ./src" --hide-intermediary-output > analysis-report.json
```

### Code Review

```bash
# Review with style guide
bob "Review ./src following Airbnb style guide"
bob "Review ./src following Google style guide"

# Review git changes
bob "Review the uncommitted changes in my code"
bob "Review the code changes between main and feature-branch"

# Review with specific focus
bob "Review ./src focusing on security, performance, and maintainability" --hide-intermediary-output > review-report.md
```

### Code Explanation

```bash
# Explain code in file
bob "Explain what the code in ./src/utils/helper.js does"

# Explain specific function
bob "Explain the calculateTotal function in ./src/utils/helper.js"

# Detailed explanation
bob "Provide a detailed explanation of the algorithm in ./src/complex-algorithm.js" --hide-intermediary-output > explanation.md

# Explain in different language
bob "Explain the code in ./src/app.js in Spanish"
```

### Code Refactoring

```bash
# Refactor file
bob "Refactor ./src/legacy-code.js to use modern JavaScript patterns"

# Refactor for performance
bob "Refactor ./src/slow-function.js to improve performance"

# Remove dead code
bob "Identify and remove dead code from ./src/app.js"

# Fix style issues
bob "Fix all style issues in ./src/app.js following best practices"
```

### Security Scanning

```bash
# Basic security scan
bob "Scan ./src for security vulnerabilities"

# Scan with severity focus
bob "Scan ./src for high and critical security vulnerabilities"

# Scan for specific vulnerabilities
bob "Check ./src for SQL injection, XSS, exposed secrets, and CSRF vulnerabilities"

# Generate security report
bob "Perform a comprehensive security scan of ./src and generate a detailed report" --hide-intermediary-output > security-report.html
```

### Documentation Generation

```bash
# Generate API documentation
bob "Generate API documentation for the code in ./src" --hide-intermediary-output > api-docs.md

# Generate architecture documentation
bob "Create architecture documentation for ./src explaining the system design" --hide-intermediary-output > architecture.md

# Generate usage examples
bob "Generate usage examples for the functions in ./src" --hide-intermediary-output > examples.md

# Generate README
bob "Create a comprehensive README for this project based on ./src" --hide-intermediary-output > README.md
```

### Testing

```bash
# Generate tests for file
bob "Generate Jest unit tests for ./src/app.js" --yolo --hide-intermediary-output > ./tests/app.test.js

# Generate tests with specific framework
bob "Generate pytest tests for ./src/app.py with fixtures and mocks" --yolo --hide-intermediary-output > ./tests/test_app.py

# Suggest test improvements
bob "Review ./tests/app.test.js and suggest improvements for better coverage"
```

### Code Formatting

```bash
# Format file
bob "Format ./src/app.js following Prettier standards"

# Format with specific style
bob "Format ./src/app.py following Black formatting style"

# Check formatting
bob "Check if ./src follows proper formatting standards and suggest fixes"
```

## Working with Git

```bash
# Review uncommitted changes
bob "Review my uncommitted code changes"

# Review changes in branch
bob "Review the code changes between main and feature-branch"

# Generate commit message
bob "Generate a commit message for my staged changes"

# Generate changelog
bob "Generate a changelog for changes since v1.0.0" --hide-intermediary-output > CHANGELOG.md
```

## Batch Operations

### Processing Multiple Files

```bash
# Analyze all JavaScript files
for file in ./src/**/*.js; do
    bob "Analyze $file for code quality issues" --hide-intermediary-output >> analysis-results.txt
done

# Review all Python files
for file in ./src/**/*.py; do
    bob "Review $file for code quality and best practices in markdown format" --hide-intermediary-output > "reviews/$(basename $file).md"
done

# Generate tests for all files
bob test-generate ./src/**/*.js --output-dir ./tests

# Refactor all files in directory
bob "Refactor all files in ./src directory recursively using modern coding patterns and best practices"
```

## Output Formats

### Available Formats

```bash
# JSON output (for programmatic processing)
bob analyze ./src --format json

# Markdown output (for documentation)
bob review ./src --format markdown

# HTML output (for reports)
bob security-scan ./src --format html

# Plain text output (default)
bob explain ./src/app.js --format text

# YAML output
bob analyze ./src --format yaml
```

## Configuration Management

### Managing Configuration

```bash
# View current configuration
bob config list

# Get specific config value
bob config get api-key
bob config get default-mode

# Set configuration value
bob config set cache-ttl 3600
bob config set max-tokens 4096

# Reset configuration
bob config reset

# Review all Python files
for file in ./src/**/*.py; do
    bob "Review $file and suggest improvements" --hide-intermediary-output >> review-results.md
done
```

## Piping and Chaining

### Combining Commands

```bash
# Pipe code to Bob for explanation
cat ./src/app.js | bob "Explain this code"

# Chain with other tools
bob "Analyze ./src for quality issues and output as JSON" | jq '.issues[] | select(.severity == "high")'

# Use in scripts
if bob "Scan ./src for critical security vulnerabilities" | grep -q "CRITICAL"; then
    echo "Security issues found"
    exit 1
else
    echo "Security check passed"
fi

# Combine multiple Bob commands
bob "Analyze ./src for code quality" --hide-intermediary-output > analysis.json && \
bob "Review ./src for best practices" --hide-intermediary-output > review.md && \
bob "Scan ./src for security vulnerabilities" --hide-intermediary-output > security.html
```

## Tips and Tricks

### Productivity Tips

1. **Use Aliases**: Create shell aliases for common prompts
   ```bash
   alias bob-review='bob "Review my code changes for quality and best practices"'
   alias bob-scan='bob "Scan for high and critical security vulnerabilities"'
   ```

2. **Save Common Prompts**: Store frequently used prompts in files
   ```bash
   echo "Analyze this code for quality, performance, and security issues" > analyze-prompt.txt
   bob "$(cat analyze-prompt.txt) in ./src/app.js"
   ```

3. **Use Variables in Scripts**: Make prompts reusable
   ```bash
   FILE="./src/app.js"
   bob "Analyze $FILE for code quality and suggest improvements"
   ```

4. **Combine with Git**: Integrate Bob into your git workflow
   ```bash
   # .git/hooks/pre-commit
   #!/bin/bash
   bob "Review my uncommitted changes and check for issues" | grep -q "ERROR" && exit 1
   ```

## Common Patterns

### Useful Workflow Patterns

```bash
# Quick code review workflow
bob "Review my uncommitted changes" && \
bob "Scan for security vulnerabilities" && \
npm test

# Documentation update workflow
bob "Generate API documentation for ./src" --hide-intermediary-output > docs/api.md && \
bob "Create a comprehensive README for this project" --hide-intermediary-output > README.md

# Pre-deployment checks
bob "Analyze ./src and ensure code quality score is above 80" && \
bob "Scan for critical security vulnerabilities" && \
npm run test

# Code quality improvement workflow
bob "Analyze ./src for quality issues" --hide-intermediary-output > before-analysis.txt && \
bob "Refactor ./src to use modern best practices" && \
bob "Analyze ./src for quality issues" --hide-intermediary-output > after-analysis.txt
```

## Next Steps

- Explore the [Code Generation Examples](./code-generation.md)
- Learn about [Analysis Examples](./analysis-examples.md)
- Review the [Lab 4 README](../README.md) for complete workflows
- Check the [BobShell Documentation](https://ibm.com/bob/docs/cli)

---

**Quick Reference Card**: Print this page for a handy command reference at your desk!

## Next Steps

- Explore the [Code Generation Examples](./code-generation.md)
- Learn about [Analysis Examples](./analysis-examples.md)
- Review the [Lab 4 README](../README.md) for complete workflows
- Check the [BobShell Documentation](https://internal.bob.ibm.com/docs/shell)

---

**Quick Reference**: Bob uses natural language prompts instead of CLI flags. Be specific about what you want, mention file paths, and use output redirection (`>`) to save results!