# Lab 4: BobShell and Command Line Usage

## Overview

In this lab, you'll learn how to use Bob's command-line interface (BobShell) to automate development tasks, integrate Bob into CI/CD pipelines, and create powerful automation scripts. BobShell allows you to leverage Bob's AI capabilities in scripts, build processes, and automated workflows.

> **🧠 Bob Differentiator: [Intelligent Resource Optimization](../bob-differentiators.md#2--intelligent-resource-optimization)**
> BobShell leverages Bob's [automatic model selection](../bob-differentiators.md#automatic-model-selection) to optimize every command. Simple tasks like code formatting use lighter models for speed, while complex analysis uses frontier-class models for accuracy. This happens automatically in the background, reducing costs by up to 60% while maintaining quality.

**Duration:** 45-60 minutes
**Difficulty:** Intermediate
**Prerequisites:** Completion of Labs 1-3, basic command-line knowledge

## Learning Objectives

By the end of this lab, you will be able to:

1. Use BobShell for interactive and non-interactive command execution
2. Create automation scripts that leverage Bob's AI capabilities
3. Integrate Bob into CI/CD pipelines
4. Use Bob for code generation, analysis, and refactoring via CLI
5. Implement automated code review and quality checks
6. Create custom workflows combining Bob with other CLI tools

## What is BobShell?

BobShell is Bob's command-line interface that provides:

- **Interactive Mode**: Chat with Bob directly from the terminal
- **Non-Interactive Mode**: Execute single commands for automation
- **Script Integration**: Use Bob in shell scripts and automation workflows
- **CI/CD Integration**: Incorporate Bob into build and deployment pipelines
- **Batch Processing**: Process multiple files or tasks in sequence

## Lab Structure

```
lab4/
├── README.md                 # This file
├── examples/                 # Example commands and use cases
│   ├── basic-commands.md     # Basic BobShell commands
│   ├── code-generation.md    # Code generation examples
│   └── analysis-examples.md  # Code analysis examples
├── scripts/                  # Automation scripts
│   ├── code-review.sh        # Automated code review script
│   ├── refactor-batch.sh     # Batch refactoring script
│   └── generate-docs.sh      # Documentation generation script
└── ci-cd/                    # CI/CD integration examples
    ├── github-actions.yml    # GitHub Actions workflow
    ├── gitlab-ci.yml         # GitLab CI configuration
    └── jenkins-pipeline.txt  # Jenkins pipeline example
```

## Part 1: Getting Started with BobShell

### Step 1.1: Install and Verify BobShell

**⚠️ Important for Windows Users:**

BobShell does not auto-install with Bob on Windows. You must install it separately by following the official installation guide:

👉 **[BobShell Installation Guide](https://internal.bob.ibm.com/docs/shell/install-and-setup)**

**📚 Note:** Public Bob documentation is available at: **https://ibm.biz/bob-doc**

**For all users**, verify that BobShell is installed and accessible:

```bash
# Check BobShell version
bob --version

# View help information
bob --help
```

**Expected Output:**
```
Bob CLI v1.x.x
Usage: bob [options] [command]
...
```

**If you see "command not found" or similar error:**
- Windows users: Follow the [installation guide](https://internal.bob.ibm.com/docs/shell/install-and-setup) to install BobShell
- macOS/Linux users: Verify Bob is installed and the shell component is enabled
- Check that BobShell is in your system PATH

**What's Happening:**
- The `--version` flag displays the installed version of BobShell
- The `--help` flag shows all available commands and options
- This confirms BobShell is properly installed and in your PATH

### Step 1.2: Interactive Mode

Launch Bob in interactive mode to chat directly from the terminal:

```bash
# Start interactive BobShell session
bob
```

**What Happens:**
- Simply typing `bob` launches an interactive BobShell session
- You'll see a prompt where you can chat with Bob directly
- All of Bob's capabilities are available through natural language commands

**Try These Commands in Interactive Mode:**

```
# Ask Bob to explain a concept
> Explain what a closure is in JavaScript

# Request code generation
> Create a Python function to calculate fibonacci numbers

# Ask for code review
> Review this code: [paste code here]
```

To exit the interactive mode, press `Ctrl+C` twice.

**📚 Learn More:** See the [BobShell Interactive Mode documentation](https://internal.bob.ibm.com/docs/shell/start-bobshell-interactive) for additional features and options.

**What's Happening:**
- Interactive mode provides a conversational interface in the terminal
- You can ask questions, request code, and get explanations
- Perfect for quick queries without opening the full IDE
- Session history is maintained during the conversation

### Step 1.3: Non-Interactive Mode

Execute single commands without entering interactive mode. Let's create a simple test file first:

```bash
# Create a simple Python file to work with
echo 'def add(a, b):
    return a + b

def multiply(x, y):
    return x * y' > calculator.py
```

Now try these non-interactive commands:

```bash
# Explain code in a file
bob "Explain what the calculator.py file does"

# Ask for code review
bob "Review calculator.py and suggest improvements"

# Generate new code
bob "Create a Python function that calculates the factorial of a number" --yolo --hide-intermediary-output > factorial.py

# Ask a quick question
bob "What is the difference between a list and a tuple in Python?"
```

**What's Happening:**
- Non-interactive mode executes a single command and exits
- Simply use `bob "your prompt"` for one-off commands
- For commands that requires explicit approval to call specific tools at Bob, you need to add --yolo argument for auto-approval.
- Perfect for automation and scripting
- Results are output to stdout for easy capture
- Can be chained with other CLI tools using pipes

### Step 1.5: Understanding Output Redirection

When using output redirection (`>`) with BobShell, you need to understand how Bob handles its output to get clean code files.

**⚠️ Important: Output Redirection Behavior**

By default, when you redirect Bob's output to a file, **Bob's thinking process and intermediary output will be included** in the file along with the generated code. To get only the code:

**Option 1: Use the `--hide-intermediary-output` flag**
```bash
# Generate code with clean output
bob "Create a Python function that calculates the factorial of a number" --yolo --hide-intermediary-output > factorial.py
```

**Option 2: Include file writing instruction in the prompt**
```bash
# Ask Bob to write directly to the file
bob "Create a Python function that calculates the factorial of a number and write it to factorial.py" --yolo
```

**What Gets Included Without These Approaches:**
- Bob's thinking process
- Tool usage messages
- Status updates
- The generated code

**What You Get With These Approaches:**
- Only the clean, generated code
- No intermediary messages
- Ready-to-use files

**Example Comparison:**

```bash
# ❌ This includes Bob's thinking in the file
bob "Create a sorting function" --yolo > sort.py

# ✅ This creates a clean code file
bob "Create a sorting function" --yolo --hide-intermediary-output > sort.py

# ✅ This also creates a clean code file
bob "Create a sorting function and write it to sort.py" --yolo
```

**💡 Best Practice:** Always use `--hide-intermediary-output` when redirecting to files, or explicitly ask Bob to write to the file in your prompt.

### Step 1.4: Using Session Resume

Bob automatically saves your interactive sessions, allowing you to resume previous conversations and continue where you left off.

**Resuming Sessions:**

```bash
# List available sessions
bob --list-sessions

# Resume the most recent session
bob --resume latest

# Resume a specific session by index
bob --resume 5
```

**Using Session Resume in Your Workflow:**

Bob automatically saves your conversation history, so you can return to previous work:

```
# Start a new session
bob

# Work on your code
> Review calculator.py and suggest improvements

# Bob provides suggestions...

# Exit the session (Ctrl+C twice)

# Later, resume the same session
bob --resume latest

# Continue from where you left off
> Let's implement those suggestions now
```

**How Session Resume Works:**

- Bob automatically saves all interactive sessions
- Each session is indexed and can be listed with `--list-sessions`
- Use `--resume latest` to continue your most recent work
- Use `--resume <index>` to return to a specific session
- Session history includes all conversation context

**Managing Sessions:**

```bash
# List all available sessions
bob --list-sessions

# Delete a specific session
bob --delete-session 3

# Resume and continue working
bob --resume latest
```

**When to Use Session Resume:**

1. **Continuing Work:** Pick up where you left off after a break
2. **Context Preservation:** Maintain conversation context across sessions
3. **Multiple Projects:** Switch between different project sessions
4. **Learning and Experimentation:** Return to previous explorations

**Example Workflow:**

```bash
# Start working on a feature
bob
> Analyze myapp.js for performance issues
# Bob identifies several issues
> Suggest optimizations for the database queries
# Exit session

# Later, resume to continue
bob --resume latest
> Let's implement those database optimizations now
# Bob remembers the previous analysis and continues
```

**💡 Tip:** Use `--resume latest` when you want to continue your most recent work, or `--list-sessions` to see all available sessions and choose a specific one.


## Part 2: Code Generation via CLI

### Step 2.1: Generate Individual Files

Use Bob to generate complete code files from the command line using natural language prompts:

```bash
# Generate a Python class (using --hide-intermediary-output for clean output)
bob "Create a Python class for managing a shopping cart with add, remove, and calculate total methods" --yolo --hide-intermediary-output > cart.py

# Generate a React component (asking Bob to write to file)
bob "Create a React component for a user profile card with avatar, name, and bio and write it to UserProfile.jsx" --yolo

# Generate a test file (using --hide-intermediary-output)
bob "Create unit tests for the cart.py file using pytest" --yolo --hide-intermediary-output > test_cart.py
```

**What's Happening:**
- Use natural language to describe what code you want
- Use `--hide-intermediary-output` flag with `>` redirection for clean code files
- Or include "write it to [filename]" in your prompt to have Bob write directly
- Bob analyzes the request and generates appropriate, working code
- Be specific about the language, framework, and requirements in your prompt

### Step 2.2: Generate Multiple Related Files

For complex projects with multiple files, describe the complete structure:

```bash
# Generate a complete API module
bob "Create a complete REST API for a todo application in Python with routes, models, and database setup. Provide all necessary files."

# Generate frontend components
bob "Create a set of React components for a dashboard: Header, Sidebar, MainContent, and Footer. Provide each component in a separate code block."
```

**What's Happening:**
- Describe the complete project structure in your prompt
- Bob will provide multiple code blocks or files
- You can save each part separately or ask Bob to organize them
- Include details about file organization in your prompt

**💡 Tip:** For multi-file projects, you can ask Bob to provide a file structure first, then generate each file individually.

### Step 2.3: Using Saved Prompts for Consistency

Save common prompts for repeated use:

```bash
# Create a prompt file for consistent API generation
cat > api-prompt.txt << 'EOF'
Create a REST API endpoint with:
- Request validation
- Error handling
- Response formatting
- Proper HTTP status codes
EOF

# Use the saved prompt with specific details (with clean output)
bob "$(cat api-prompt.txt) Create a POST endpoint at /api/users for creating new users" --yolo --hide-intermediary-output > user-endpoint.js

# Or combine with additional context (asking Bob to write to file)
bob "$(cat api-prompt.txt) Create a GET endpoint at /api/products for listing products with pagination and write it to products-endpoint.js" --yolo
```

**What's Happening:**
- Save common requirements in text files
- Combine saved prompts with specific details
- Ensures consistency across your codebase
- Reduces repetition in your prompts

## Part 3: Code Analysis and Review - Example Use Cases

**📝 Note:** This section demonstrates example prompts showing how BobShell can be used for code analysis and review in real projects. These are reference examples, not commands to run as part of this lab.

### Step 3.1: Code Quality Analysis Examples

BobShell can analyze code for quality issues using natural language prompts. Here are example prompts you might use in your projects:

```bash
# Example: Analyze a single file
bob "Analyze the code quality, performance, and security of ./src/app.js"

# Example: Analyze entire directory and save as JSON
bob "Analyze all files in ./src recursively and provide a detailed report" > analysis-report.json

# Example: Get specific metrics
bob "Analyze ./src and provide metrics on complexity, maintainability, and test coverage"
```

**How these work:**
- Use natural language to describe what you want Bob to analyze
- Be specific about aspects: quality, performance, security, etc.
- Mention if you want recursive directory analysis
- Use output redirection (`>`) to save results to files

### Step 3.2: Automated Code Review Examples

BobShell can perform comprehensive code reviews using conversational prompts. Example prompts:

```bash
# Example: Review changes in a branch
bob "Review the code changes between main and feature-branch"

# Example: Review specific files with style guide
bob "Review the React components in ./src/components following Airbnb style guide"

# Example: Review with specific focus
bob "Review ./src for code quality issues and provide suggestions in markdown format" > review-report.md
```

**How these work:**
- Describe what code you want reviewed (files, directories, git changes)
- Specify style guides or standards to follow (Airbnb, Google, etc.)
- Mention specific focus areas (security, performance, best practices)
- Use output redirection to save review reports

### Step 3.3: Security Analysis Examples

BobShell can scan code for security vulnerabilities using natural language. Example prompts:

```bash
# Example: Security scan with severity focus
bob "Scan ./src for high and critical security vulnerabilities"

# Example: Check for specific vulnerabilities
bob "Check ./src for SQL injection, XSS, and exposed secrets"

# Example: Generate security report
bob "Perform a comprehensive security analysis of ./src and generate an HTML report" > security-report.html
```

**How these work:**
- Ask Bob to scan or analyze for security issues
- Specify severity levels (high, critical) or vulnerability types
- Request specific output formats (HTML, markdown, JSON)
- Similar to vulnerabilities you fixed in Lab 2

**💡 When to use these prompts:**
- During code reviews before merging pull requests
- As part of CI/CD pipelines for automated quality checks
- When auditing existing codebases for security issues
- For generating compliance and security reports

## Part 4: Automation Scripts

### Step 4.1: Automated Code Review Script

Let's examine the automated code review script:

**File: `scripts/code-review.sh`**

This script performs automated code review on changed files:

```bash
#!/bin/bash
# Automated Code Review Script
# Reviews all changed files in the current branch

# Configuration
BRANCH="${1:-main}"
OUTPUT_DIR="./review-reports"
TIMESTAMP=$(date +%Y%m%d_%H%M%S)

# Create output directory
mkdir -p "$OUTPUT_DIR"

# Get list of changed files
echo "Comparing against branch: $BRANCH"
CHANGED_FILES=$(git diff --name-only "$BRANCH"...HEAD | grep -E '\.(js|jsx|ts|tsx|py|java)$')

if [ -z "$CHANGED_FILES" ]; then
    echo "No code files changed"
    exit 0
fi

echo "Files to review:"
echo "$CHANGED_FILES"

# Review each file
for file in $CHANGED_FILES; do
    if [ -f "$file" ]; then
        echo "Reviewing: $file"
        bob "Review $file for code quality, potential bugs, and best practices. Output in markdown format." > "$OUTPUT_DIR/${file//\//_}_review_$TIMESTAMP.md"
    fi
done

# Generate summary report
echo "Generating summary report..."
bob "Create a summary of all code reviews in $OUTPUT_DIR" > "$OUTPUT_DIR/summary_$TIMESTAMP.md"

echo "Review complete! Reports saved to $OUTPUT_DIR"
```

**Usage:**
```bash
# Review changes against main branch
./scripts/code-review.sh

# Review changes against different branch
./scripts/code-review.sh develop
```

**What's Happening:**
- Script identifies all changed code files using git diff
- Each file is reviewed individually by Bob
- Reviews are saved as markdown files with timestamps
- A summary report aggregates all findings
- Perfect for pre-commit or pre-merge checks

### Step 4.2: Batch Refactoring Script

**File: [`scripts/refactor-batch.sh`](scripts/refactor-batch.sh)**

This script safely refactors multiple files based on specified criteria using Bob's natural language interface.

**Features:**
- Automatic backup creation before refactoring
- Multiple refactoring types: modernize, optimize, cleanup, security
- Processes multiple files in batch
- Detailed logging and error handling
- Automatic restoration on failure
- Confirmation prompt before proceeding

**Usage:**
```bash
# Modernize code in current directory
./scripts/refactor-batch.sh modernize .

# Optimize performance in src directory
./scripts/refactor-batch.sh optimize ./src

# Clean up code
./scripts/refactor-batch.sh cleanup ./lib

# Fix security issues
./scripts/refactor-batch.sh security ./src
```

**Example Output:**
```
Batch Refactoring
================================
Refactor Type: modernize
Target Directory: ./src
Backup Directory: ./refactor-backups/20240202_143000

Creating Backup ... ✓ Done
Finding Files ... ✓ Found 15 file(s)

Refactoring Files
Processing: ./src/app.js ... ✓ Done
Processing: ./src/utils.js ... ✓ Done
...

Refactoring Complete
Successful: 15
Failed: 0
```

**What's Happening:**
- Script creates complete backup before any changes
- Uses Bob's natural language prompts for refactoring
- Each file is processed individually with error handling
- Failed files are automatically restored from backup
- Generates detailed report of all changes

**💡 Tip:** Review the [complete script](scripts/refactor-batch.sh) to see how Bob's natural language interface handles batch refactoring safely.

### Step 4.3: Documentation Generation Script

**File: [`scripts/generate-docs.sh`](scripts/generate-docs.sh)**

This comprehensive script automatically generates complete documentation for your codebase using Bob's natural language interface.

**Features:**
- Generates API documentation
- Creates architecture documentation
- Produces usage examples
- Generates README, CHANGELOG, CONTRIBUTING guide
- Creates FAQ and troubleshooting guides
- Supports markdown and HTML output formats
- Includes detailed logging and error handling

**Usage:**
```bash
# Generate docs for current directory (markdown format)
./scripts/generate-docs.sh

# Generate docs for specific directory
./scripts/generate-docs.sh ./src ./documentation

# Generate HTML documentation
./scripts/generate-docs.sh ./src ./docs html
```

**Example Output:**
```
Documentation Generation
================================
Source: ./src
Output: ./docs
Format: markdown

Generating API Documentation ... ✓ Done
Generating Architecture Documentation ... ✓ Done
Generating Usage Examples ... ✓ Done
Generating README ... ✓ Done
Generating Changelog ... ✓ Done
Generating Contributing Guide ... ✓ Done

Documentation Generation Complete
Generated 8 documentation file(s)
```

**What's Happening:**
- Script uses Bob's natural language prompts to generate each documentation type
- Creates comprehensive documentation suite automatically
- Generates README and changelog from git history
- Supports multiple output formats (markdown, HTML)
- Includes HTML index page for easy navigation
- Provides detailed logging for troubleshooting

**💡 Tip:** Review the [complete script](scripts/generate-docs.sh) to see how Bob's natural language interface is used for automated documentation generation.

## Part 5: CI/CD Integration

### Step 5.1: GitHub Actions Integration

See the complete GitHub Actions workflow configuration in [`ci-cd/github-actions.yml`](ci-cd/github-actions.yml).

**Key Features:**
- Runs on every pull request and push to main/develop
- Installs and configures Bob CLI in the CI environment
- Performs code review on changed files using natural language prompts
- Runs security scan and quality analysis
- Uploads reports as artifacts
- Posts review comments directly on pull requests
- Fails build if critical security issues are found

**Quick Start:**
1. Copy `ci-cd/github-actions.yml` to `.github/workflows/bob-ci.yml` in your repository
2. Add `BOB_API_KEY` to your repository secrets (Settings > Secrets and variables > Actions)
3. Customize quality thresholds and analysis levels as needed

### Step 5.2: GitLab CI Integration

See the complete GitLab CI configuration in [`ci-cd/gitlab-ci.yml`](ci-cd/gitlab-ci.yml).

**Key Features:**
- Multi-stage pipeline: setup, review, security, quality, documentation, report
- Each stage produces artifacts for review
- Security scan fails pipeline on critical issues
- Quality check enforces minimum quality score
- Complexity and dependency analysis for thorough checks
- Documentation generation on main branch
- Summary report generation with all results

**Quick Start:**
1. Copy `ci-cd/gitlab-ci.yml` to `.gitlab-ci.yml` in your repository root
2. Add `BOB_API_KEY` as a CI/CD variable (Settings > CI/CD > Variables)
3. Configure artifact retention and quality thresholds as needed

### Step 5.3: Jenkins Pipeline Integration

See the complete Jenkins pipeline configuration in [`ci-cd/jenkins-pipeline.txt`](ci-cd/jenkins-pipeline.txt).

**Key Features:**
- Multi-stage pipeline with Bob integration
- Credentials managed securely through Jenkins
- Code review runs only on pull requests using natural language prompts
- Security scan fails build on critical issues
- Quality analysis marks build as unstable if below threshold
- Complexity and dependency analysis stages
- Documentation generated and published on main branch
- Build parameters for customizable analysis levels
- Artifacts archived for all stages
- Workspace cleaned after execution

**Quick Start:**
1. Copy content from `ci-cd/jenkins-pipeline.txt` to a `Jenkinsfile` in your repository root
2. Add Bob API key as Jenkins credential with ID `bob-api-key` (Jenkins > Credentials > System > Global credentials)
3. Install required Jenkins plugins: Pipeline, Git, HTML Publisher, Email Extension
4. Configure webhook for automatic builds
5. Customize quality thresholds and analysis levels as needed

## Part 6: Advanced Workflows

### Step 6.1: Combining Bob with Other Tools

Create powerful workflows by combining Bob with other CLI tools:

```bash
# Find TODO comments and create tasks
grep -r "TODO" ./src | bob "Convert these TODO comments into GitHub issues with proper formatting in JSON format" --hide-intermediary-output > issues.json

# Analyze git history and generate insights
git log --since="1 month ago" --pretty=format:"%h %s" | bob "Analyze these commit messages and provide insights on development patterns in markdown format" --hide-intermediary-output > dev-insights.md

# Process test results
npm test -- --json | bob "Analyze these test results and suggest improvements in markdown format" --hide-intermediary-output > test-analysis.md

# Code coverage analysis
npm run coverage -- --json | bob "Create a coverage report with recommendations for improving test coverage in markdown format" --hide-intermediary-output > coverage-report.md
```

**What's Happening:**
- Pipes output from standard tools to Bob for AI analysis
- Converts unstructured data into actionable insights
- Generates reports and recommendations
- Integrates seamlessly with existing toolchains

### Step 6.2: Custom Workflow Example

Create a complete pre-commit workflow:

```bash
#!/bin/bash
# Pre-commit workflow with Bob

echo "Running pre-commit checks with Bob..."

# 1. Format code
echo "Formatting code..."
bob "Format all code in ./src directory using Prettier style guidelines"

# 2. Lint code
echo "Linting code..."
bob lint ./src --fix

# 3. Review changes
echo "Reviewing changes..."
bob "Review uncommitted changes (git diff HEAD) for code quality issues. Output in markdown format." --hide-intermediary-output > pre-commit-review.md

# 4. Security check
echo "Security scan..."
bob "Perform security scan of ./src focusing on high and critical severity vulnerabilities. Output in JSON format." --hide-intermediary-output > security-check.json

# 5. Check for critical issues
CRITICAL=$(jq '.critical | length' security-check.json)
if [ "$CRITICAL" -gt 0 ]; then
    echo "❌ Critical security issues found! Commit blocked."
    cat security-check.json
    exit 1
fi

# 6. Run tests
echo "Running tests..."
npm test

# 7. Generate commit message suggestion
echo "Generating commit message suggestion..."
bob "Based on the staged changes, suggest a conventional commit message" --hide-intermediary-output > suggested-commit.txt

echo "✅ Pre-commit checks passed!"
echo "Suggested commit message:"
cat suggested-commit.txt
```

**What's Happening:**
- Comprehensive pre-commit workflow
- Formats and lints code automatically
- Reviews changes before commit
- Blocks commits with security issues
- Runs tests to ensure functionality
- Suggests appropriate commit messages
- Ensures code quality at commit time

## Part 7: Best Practices

### 7.1: BobShell Best Practices

1. **Use Specific Commands**: Be specific in your requests for better results
   ```bash
   # Good
   bob generate "Create a React component for user authentication with email and password fields, validation, and error handling"
   
   # Less specific
   bob generate "Create a login form"
   ```

2. **Leverage Output Formats**: Use appropriate formats for different use cases
   ```bash
   # JSON for programmatic processing
   bob "Analyze ./src and provide results in JSON format" --hide-intermediary-output > analysis.json
   
   # Markdown for documentation
   bob "Review ./src for code quality and output in markdown format" --hide-intermediary-output > review.md
   
   # HTML for reports
   bob "Perform security scan of ./src and output in HTML format" --hide-intermediary-output > security-report.html
   ```

> **💡 Automatic Optimization**
> When you run BobShell commands, Bob's [intelligent resource optimization](../bob-differentiators.md#2--intelligent-resource-optimization) automatically selects the most appropriate model for each task. You don't need to specify which model to use—Bob handles this transparently, optimizing for both quality and cost.

3. **Use Git Integration**: Review only changed code
   ```bash
   # Review changes in current branch
   bob "Review code changes between main and HEAD branches"

   # Review uncommitted changes
   bob "Review uncommitted changes (git diff HEAD)"
   ```

4. **Implement Caching**: Cache Bob responses for repeated operations
   ```bash
   # Enable caching
   bob config set cache-enabled true
   bob config set cache-ttl 3600
   ```

### 7.2: Automation Best Practices

1. **Always Create Backups**: Before automated refactoring
2. **Use Version Control**: Commit before running automated changes
3. **Test After Automation**: Always verify automated changes work
4. **Log Everything**: Keep logs of automated operations
5. **Handle Errors Gracefully**: Implement proper error handling in scripts

### 7.3: CI/CD Best Practices

1. **Secure API Keys**: Use secrets management for Bob API keys
2. **Set Appropriate Thresholds**: Define quality and security thresholds
3. **Archive Reports**: Keep reports for audit and review
4. **Fail Fast**: Stop pipeline on critical issues
5. **Provide Feedback**: Comment on PRs with review results

> **🔍 Bob Findings in CI/CD**
> Integrate [Bob Findings](../bob-differentiators.md#3--bob-findings-automated-analysis-engine) into your CI/CD pipeline for automated security scanning and code quality checks. Bob can catch vulnerabilities and code issues before they reach production, with specific remediation recommendations included in your pipeline reports.

## Exercises

### Exercise 1: Create a Custom Review Script

Create a script that:
1. Reviews all Python files in a directory
2. Checks for PEP 8 compliance
3. Identifies potential bugs
4. Generates a summary report

### Exercise 2: Build a CI/CD Pipeline

Set up a complete CI/CD pipeline that:
1. Runs on pull requests
2. Performs code review
3. Runs security scan
4. Checks code quality
5. Posts results as PR comments

### Exercise 3: Automate Documentation

Create a workflow that:
1. Generates API documentation
2. Creates usage examples
3. Updates README
4. Commits documentation changes

## Troubleshooting

### Common Issues

1. **Bob CLI Not Found**
   ```bash
   # Verify installation
   which bob
   
   # Reinstall if needed
   npm install -g @ibm/bob-cli
   ```

2. **Authentication Errors**
   ```bash
   # Check API key configuration
   bob config get api-key
   
   # Reconfigure if needed
   bob config set api-key YOUR_API_KEY
   ```

3. **Rate Limiting**
   ```bash
   # Check rate limit status
   bob status
   
   # Use caching to reduce API calls
   bob config set cache-enabled true
   ```

## Summary

In this lab, you learned:

✅ How to use BobShell for interactive and non-interactive operations  
✅ Code generation, analysis, and review via command line  
✅ Creating automation scripts for common development tasks  
✅ Integrating Bob into CI/CD pipelines (GitHub Actions, GitLab CI, Jenkins)  
✅ Building custom workflows combining Bob with other tools  
✅ Best practices for CLI usage and automation

## Next Steps

- **Lab 5**: Learn how to modernize Java applications with Bob
- **Lab 6**: Create custom MCP servers and modes
- Explore advanced BobShell features in the documentation
- Share your automation scripts with the team

## Additional Resources

- [BobShell Documentation](https://ibm.com/bob/docs/cli)
- [CI/CD Integration Guide](https://ibm.com/bob/docs/cicd)
- [Automation Examples Repository](https://github.com/ibm/bob-automation-examples)
- [BobShell API Reference](https://ibm.com/bob/docs/api)

---

**Need Help?** If you encounter issues:
1. Check the troubleshooting section above
2. Review the BobShell documentation
3. Ask in the Bob community forums
4. Contact IBM support

**Feedback:** Help us improve this lab by providing feedback on what worked well and what could be better!
