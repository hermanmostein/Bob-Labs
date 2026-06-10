# BobShell Code Analysis Examples

## Overview

This document provides comprehensive examples of using BobShell for code analysis, review, and quality assessment using natural language prompts. Learn how to identify issues, improve code quality, and maintain high standards across your codebase.

## Table of Contents

1. [Code Quality Analysis](#code-quality-analysis)
2. [Security Analysis](#security-analysis)
3. [Performance Analysis](#performance-analysis)
4. [Code Review](#code-review)
5. [Complexity Analysis](#complexity-analysis)
6. [Best Practices Checking](#best-practices-checking)

## Code Quality Analysis

### Basic Quality Check

```bash
# Analyze single file
bob "Analyze the code quality of ./src/app.js"

# Analyze with specific checks
bob "Analyze ./src/app.js for quality, maintainability, and readability issues"

# Analyze entire directory
bob "Analyze all files in ./src recursively for code quality issues"

# Get detailed report
bob "Perform a comprehensive code quality analysis of ./src and provide a detailed report" > quality-report.md
```

**Example Output:**
```markdown
# Code Quality Report

## Overall Score: 78/100

### Issues Found:
- **High Priority (3)**
  - Complex function with cyclomatic complexity of 15
  - Missing error handling in async function
  - Inconsistent naming conventions

- **Medium Priority (7)**
  - Long function (>50 lines)
  - Duplicate code blocks
  - Missing JSDoc comments

- **Low Priority (12)**
  - Console.log statements in production code
  - Unused variables
  - Magic numbers without constants
```

### Quality Metrics

```bash
# Get specific metrics
bob "Analyze ./src and provide metrics on complexity, maintainability, coverage, and code duplication"

# Set quality threshold
bob "Analyze ./src and ensure the code quality score is at least 80"

# Compare before and after
bob "Analyze ./src for code quality and output as JSON" > before.json
# Make changes
bob "Analyze ./src for code quality and output as JSON" > after.json
# Compare results
diff before.json after.json
```

### Code Smells Detection

```bash
# Detect code smells
bob "Detect code smells in ./src and provide detailed analysis"

# Focus on specific smells
bob "Check ./src for long methods, large classes, and duplicate code"

# Generate refactoring suggestions
bob "Analyze ./src for code smells and suggest refactoring strategies" > refactoring-plan.md
```

**Example Output:**
```markdown
# Code Smells Detected

## Long Method
**File:** src/services/userService.js
**Line:** 45-120
**Severity:** Medium
**Description:** Method `processUserData` is 75 lines long
**Suggestion:** Extract helper methods for validation, transformation, and persistence

## Duplicate Code
**Files:**
- src/utils/validator.js (lines 20-35)
- src/utils/sanitizer.js (lines 45-60)
**Severity:** High
**Suggestion:** Extract common validation logic into shared utility function
```

## Security Analysis

### Vulnerability Scanning

```bash
# Basic security scan
bob "Scan ./src for security vulnerabilities"

# Scan with severity focus
bob "Scan ./src for high and critical security vulnerabilities"

# Scan for specific vulnerabilities
bob "Check ./src for SQL injection, XSS, CSRF, and exposed secrets"

# Generate security report
bob "Perform a comprehensive security scan of ./src and generate an HTML report" > security-report.html
```

**Example Output:**
```
Security Scan Results
=====================

Critical Issues: 2
High Issues: 5
Medium Issues: 12
Low Issues: 8

CRITICAL: SQL Injection Vulnerability
File: src/api/users.js
Line: 45
Code: db.query(`SELECT * FROM users WHERE id = ${userId}`)
Fix: Use parameterized queries

CRITICAL: Hardcoded Secret
File: src/config/database.js
Line: 12
Code: const API_KEY = "sk_live_abc123xyz"
Fix: Use environment variables
```

### Common Vulnerability Checks

```bash
# Check for SQL injection
bob "Check ./src for SQL injection vulnerabilities and provide detailed examples"

# Check for XSS vulnerabilities
bob "Scan ./src for XSS vulnerabilities with examples of how to fix them"

# Check for exposed secrets
bob "Check ./src for exposed secrets, credentials, and API keys"

# Check authentication issues
bob "Analyze ./src for authentication, session management, and JWT security issues"
```

### Security Best Practices

```bash
# Check OWASP Top 10
bob "Scan ./src for OWASP Top 10 vulnerabilities"

# Check for insecure dependencies
bob "Check ./package.json for security vulnerabilities in dependencies"

# Validate security headers
bob "Review ./src/middleware for proper security headers implementation"

# Check for sensitive data exposure
bob "Check ./src for sensitive data exposure and logging issues"
```

## Performance Analysis

### Performance Profiling

```bash
# Analyze performance
bob "Analyze ./src for performance issues and provide detailed recommendations"

# Identify bottlenecks
bob "Identify performance bottlenecks in ./src"

# Memory leak detection
bob "Check ./src for memory leaks and resource leaks"

# Async/await optimization
bob "Analyze ./src for async/await performance issues and optimization opportunities"
```

**Example Output:**
```markdown
# Performance Analysis

## Performance Issues Found: 8

### High Impact (2)
1. **Synchronous File Operations**
   - File: src/utils/fileHandler.js
   - Line: 23
   - Issue: Using fs.readFileSync in async context
   - Impact: Blocks event loop
   - Fix: Use fs.promises.readFile

2. **N+1 Query Problem**
   - File: src/api/posts.js
   - Line: 67
   - Issue: Loading comments in loop
   - Impact: Multiple database queries
   - Fix: Use JOIN or batch loading

### Medium Impact (6)
- Inefficient array operations
- Missing database indexes
- Large bundle size
```

### Optimization Suggestions

```bash
# Get optimization recommendations
bob "Analyze ./src for performance and provide optimization recommendations" > optimizations.md

# Analyze bundle size
bob "Analyze ./src for bundle size issues and tree-shaking opportunities"

# Database query optimization
bob "Review ./src/models for database query optimization opportunities"

# Caching opportunities
bob "Identify caching opportunities in ./src"
```

## Code Review

### Automated Code Review

```bash
# Review single file
bob "Review ./src/components/UserForm.jsx for code quality and best practices"

# Review with style guide
bob "Review ./src following Airbnb style guide"

# Review git changes
bob "Review my uncommitted code changes"

# Review pull request
bob "Review the code changes between main and feature-branch" > pr-review.md
```

**Example Output:**
```markdown
# Code Review: UserForm.jsx

## Summary
- **Overall Rating:** B+
- **Issues Found:** 8 (2 high, 4 medium, 2 low)
- **Strengths:** Good component structure, proper prop types
- **Areas for Improvement:** Error handling, accessibility

## Detailed Review

### High Priority Issues

1. **Missing Error Boundary** (Line 15)
   ```javascript
   // Current
   const UserForm = () => {
     const [data, setData] = useState({});
   
   // Suggested
   const UserForm = () => {
     const [data, setData] = useState({});
     const [error, setError] = useState(null);
     
     if (error) return <ErrorDisplay error={error} />;
   ```

2. **Unvalidated User Input** (Line 45)
   - Input fields lack validation
   - Suggestion: Add validation library like Yup or Joi

### Medium Priority Issues

1. **Missing Accessibility Attributes** (Lines 30-40)
   - Form inputs missing aria-labels
   - No keyboard navigation support
   
2. **Inefficient Re-renders** (Line 25)
   - Component re-renders on every keystroke
   - Suggestion: Use debouncing or React.memo

### Positive Aspects
- Clean component structure
- Proper use of hooks
- Good naming conventions
```

### Review Specific Aspects

```bash
# Focus on specific aspects
bob "Review ./src focusing on security and performance"

# Review documentation
bob "Review ./src and check if documentation is adequate"

# Review test coverage
bob "Review ./tests and assess test coverage quality"

# Review API design
bob "Review ./src/api for API design and REST principles compliance"
```

### Style Guide Compliance

```bash
# Check Airbnb style guide
bob "Review ./src following Airbnb style guide and suggest fixes"

# Check Google style guide
bob "Review ./src following Google style guide"

# Check Standard JS
bob "Review ./src following Standard JS style guide"
```

## Complexity Analysis

### Cyclomatic Complexity

```bash
# Analyze complexity
bob "Analyze ./src for cyclomatic complexity metrics"

# Find complex functions
bob "Find functions in ./src with complexity greater than 10"

# Detailed complexity report
bob "Analyze ./src for complexity and provide a detailed report" > complexity-report.md
```

**Example Output:**
```markdown
# Complexity Analysis

## Functions Exceeding Threshold (Complexity > 10)

1. **processOrderData** - Complexity: 18
   - File: src/services/orderService.js
   - Lines: 45-120
   - Recommendation: Break into smaller functions
   - Suggested refactoring:
     - extractValidation()
     - calculateTotals()
     - applyDiscounts()
     - persistOrder()

2. **validateUserInput** - Complexity: 15
   - File: src/utils/validation.js
   - Lines: 30-85
   - Recommendation: Use validation library or extract rules

## Complexity Distribution
- Low (1-5): 145 functions (72%)
- Medium (6-10): 45 functions (22%)
- High (11-15): 10 functions (5%)
- Very High (>15): 2 functions (1%)
```

### Cognitive Complexity

```bash
# Analyze cognitive complexity
bob "Analyze ./src for cognitive complexity"

# Compare cyclomatic vs cognitive
bob "Analyze ./src and compare cyclomatic complexity with cognitive complexity"
```

### Maintainability Index

```bash
# Calculate maintainability index
bob "Calculate the maintainability index for ./src"

# Find hard-to-maintain code
bob "Find code in ./src with maintainability index below 65"

# Generate maintainability report
bob "Analyze ./src for maintainability and generate an HTML report" > maintainability.html
```

## Dependency Analysis

### Dependency Checking

```bash
# Analyze dependencies
bob "Analyze dependencies in ./package.json"

# Find outdated dependencies
bob "Check ./package.json for outdated dependencies"

# Security vulnerabilities in dependencies
bob "Check ./package.json for security vulnerabilities in dependencies"

# Unused dependencies
bob "Find unused dependencies in ./package.json"
```

**Example Output:**
```markdown
# Dependency Analysis

## Outdated Dependencies (12)
- express: 4.17.1 → 4.18.2 (minor update available)
- react: 17.0.2 → 18.2.0 (major update available)
- lodash: 4.17.20 → 4.17.21 (security patch)

## Vulnerable Dependencies (3)
- **minimist** (Critical)
  - Current: 1.2.5
  - Fixed in: 1.2.6
  - Vulnerability: Prototype pollution
  
## Unused Dependencies (5)
- moment (use date-fns instead)
- request (deprecated, use axios)
- gulp (not used in build process)

## Recommendations
1. Update lodash immediately (security)
2. Plan migration to React 18
3. Remove unused dependencies
4. Consider dependency size impact
```

### Import Analysis

```bash
# Analyze imports
bob "Analyze imports in ./src"

# Find circular dependencies
bob "Check ./src for circular dependencies"

# Unused imports
bob "Find unused imports in ./src"

# Import organization
bob "Check if imports in ./src are properly organized"
```

## Best Practices Checking

### Language-Specific Best Practices

```bash
# JavaScript/TypeScript best practices
bob "Check ./src for JavaScript and TypeScript best practices"

# Python best practices (PEP 8)
bob "Check ./src for Python best practices and PEP 8 compliance"

# Java best practices
bob "Check ./src for Java best practices"

# React best practices
bob "Check ./src for React best practices and patterns"
```

### Framework-Specific Checks

```bash
# Express.js best practices
bob "Check ./src for Express.js best practices"

# React best practices
bob "Analyze ./src React code for best practices and common patterns"

# Vue.js best practices
bob "Check ./src for Vue.js best practices"

# Django best practices
bob "Check ./src for Django best practices"
```

### Code Organization

```bash
# Check file structure
bob "Review the file structure of ./src and suggest improvements"

# Check naming conventions
bob "Check ./src for consistent naming conventions"

# Check module organization
bob "Analyze ./src for proper module organization"

# Check separation of concerns
bob "Check ./src for proper separation of concerns"
```

## Batch Analysis

### Analyzing Multiple Projects

```bash
# Analyze multiple directories
for dir in project1 project2 project3; do
    bob "Analyze ./$dir for code quality and output as JSON" > ${dir}-analysis.json
done
```

### Scheduled Analysis

```bash
# Create analysis script
cat > daily-analysis.sh << 'EOF'
#!/bin/bash
DATE=$(date +%Y%m%d)
bob "Analyze ./src for code quality and output as JSON" > reports/analysis-$DATE.json
bob "Analyze ./src for code quality and generate HTML report" > reports/analysis-$DATE.html

# Check for critical issues
if grep -q "CRITICAL" reports/analysis-$DATE.json; then
    echo "Critical issues found!" | mail -s "Code Analysis Alert" team@example.com
fi
EOF

# Schedule with cron
# 0 2 * * * /path/to/daily-analysis.sh
```

## Integration with CI/CD

### Pre-commit Analysis

```bash
# Pre-commit hook
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/bash
echo "Running code analysis..."

# Analyze staged files
STAGED_FILES=$(git diff --cached --name-only --diff-filter=ACM | grep -E '\.(js|jsx|ts|tsx)$')

if [ -n "$STAGED_FILES" ]; then
    for file in $STAGED_FILES; do
        bob "Analyze $file and fail if any high severity issues are found"
        if [ $? -ne 0 ]; then
            echo "Analysis failed for $file"
            exit 1
        fi
    done
fi

echo "Analysis passed!"
EOF

chmod +x .git/hooks/pre-commit
```

### Pull Request Analysis

```bash
# Analyze PR changes
bob review --git-diff origin/main...HEAD \
    --format markdown \
    --output pr-analysis.md

# Check for regressions
bob analyze ./src --compare-with baseline-analysis.json \
    --fail-on-regression
```

## Best Practices for Analysis

### 1. Regular Analysis

```bash
# Daily analysis
bob "Analyze ./src and provide comprehensive results in JSON format" > daily-$(date +%Y%m%d).json

# Weekly detailed report
bob "Analyze ./src with verbose details and provide comprehensive report in HTML format" > weekly-report.html
```

### 2. Focus on Critical Issues

```bash
### Pre-commit Analysis

```bash
# Pre-commit hook
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/bash
echo "Running code analysis..."

# Get staged files
STAGED_FILES=$(git diff --cached --name-only --diff-filter=ACM | grep -E '\.(js|jsx|ts|tsx)$')

if [ -n "$STAGED_FILES" ]; then
    for file in $STAGED_FILES; do
        bob "Analyze $file for critical issues" | grep -q "CRITICAL" && exit 1
    done
fi

echo "Analysis passed!"
EOF

chmod +x .git/hooks/pre-commit
```

### Pull Request Analysis

```bash
# Analyze PR changes
bob "Review the code changes between origin/main and HEAD" > pr-analysis.md

# Check for regressions
bob "Analyze ./src and compare with previous quality baseline"
```

## Best Practices for Analysis

### 1. Regular Analysis

```bash
# Daily analysis
bob "Analyze ./src for code quality" > daily-$(date +%Y%m%d).json

# Weekly detailed report
bob "Perform comprehensive analysis of ./src with detailed recommendations" > weekly-report.html
```

### 2. Focus on Critical Issues

```bash
# Prioritize critical and high severity
bob "Analyze ./src and focus on critical and high severity issues"

# Focus on security first
bob "Scan ./src for critical security vulnerabilities"
```

### 3. Track Improvements

```bash
# Baseline analysis
bob "Analyze ./src for code quality and output as JSON" > baseline.json

# After improvements
bob "Analyze ./src for code quality and output as JSON" > improved.json

# Compare manually or ask Bob
bob "Compare the code quality between baseline.json and improved.json"
```

### 4. Automate Everything

```bash
# Automated workflow
bob "Analyze ./src for code quality" > analysis.json && \
bob "Scan ./src for security vulnerabilities" > security.json && \
bob "Review my uncommitted changes" > review.md && \
bob "Create an executive summary from analysis.json, security.json, and review.md" > summary.md
```

## Tips for Better Analysis

1. **Be Specific**: Clearly state what aspects you want analyzed
2. **Provide Context**: Mention the technology stack and framework
3. **Set Priorities**: Focus on critical issues first
4. **Regular Checks**: Integrate analysis into your workflow
5. **Track Progress**: Save analysis results to track improvements over time

## Next Steps

- Review [Basic Commands](./basic-commands.md) for more prompt patterns
- Explore [Code Generation](./code-generation.md) for creating code
- Check the [Lab 4 README](../README.md) for complete workflows
- Practice with real-world code examples

## Additional Resources

- [BobShell Documentation](https://internal.bob.ibm.com/docs/shell)
- [Code Analysis Best Practices](https://internal.bob.ibm.com/docs/analysis)
- [Security Scanning Guide](https://internal.bob.ibm.com/docs/security)

---

**Pro Tip**: Use natural language to describe exactly what you want analyzed. The more specific your prompt, the better the analysis results!