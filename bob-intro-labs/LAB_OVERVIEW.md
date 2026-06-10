# Bob Bootcamp Labs - Visual Overview

## Lab Journey Map

```mermaid
graph TB
    Start[Start: Prerequisites Check] --> Beginner[Beginner Track]
    Beginner --> Lab1[Lab 1: Build Todo App]
    Lab1 --> Lab2[Lab 2: Security Analysis]
    
    Lab2 --> Intermediate[Intermediate Track]
    Intermediate --> Lab3[Lab 3: Code Translation]
    Lab3 --> Lab4[Lab 4: BobShell & CLI]
    
    Lab4 --> Advanced[Advanced Track]
    Advanced --> Lab5[Lab 5: Java Modernization]
    Lab5 --> Lab6[Lab 6: MCP Server & Custom Modes]
    
    Lab6 --> Complete[Complete: Bob Mastery]
    
    Lab1 --> L1A[Learn: Modes]
    Lab1 --> L1B[Learn: Auto-approvals]
    Lab1 --> L1C[Learn: GitHub MCP]
    
    Lab2 --> L2A[Learn: Code Analysis]
    Lab2 --> L2B[Learn: Security]
    Lab2 --> L2C[Learn: Bug Fixing]
    
    Lab3 --> L3A[Learn: Translation]
    Lab3 --> L3B[Learn: Language Patterns]
    Lab3 --> L3C[Learn: Cross-platform]
    
    Lab4 --> L4A[Learn: CLI Automation]
    Lab4 --> L4B[Learn: CI/CD]
    Lab4 --> L4C[Learn: Batch Operations]
    
    Lab5 --> L5A[Learn: Refactoring]
    Lab5 --> L5B[Learn: Modern Java]
    Lab5 --> L5C[Learn: UI + CLI]
    
    Lab6 --> L6A[Learn: MCP Protocol]
    Lab6 --> L6B[Learn: Custom Modes]
    Lab6 --> L6C[Learn: Integrations]
    
    style Lab1 fill:#b3e5fc
    style Lab2 fill:#b3e5fc
    style Lab3 fill:#81d4fa
    style Lab4 fill:#81d4fa
    style Lab5 fill:#4fc3f7
    style Lab6 fill:#4fc3f7
    style Complete fill:#e1ffe1
    style Beginner fill:#e1f5ff
    style Intermediate fill:#fff4e1
    style Advanced fill:#ffe1f5
```

## Lab 1: Building with Bob

### What You'll Build
A full-stack Todo application with Python Flask backend and JavaScript frontend

### Bob Features Showcased
- 🎯 **Plan Mode**: Plan project structure and API design
- 💻 **Code Mode**: Implement backend and frontend
- ❓ **Ask Mode**: Get explanations and guidance
- ⚡ **Auto-approvals**: Rapid development workflow
- 📝 **Literate Coding**: Self-documenting code
- 🔗 **GitHub MCP**: Version control integration

### Technology Stack
```
Frontend:          Backend:           Tools:
- HTML5            - Python 3.8+      - Bob AI
- CSS3             - Flask            - Git/GitHub
- JavaScript       - SQLite           - MCP Servers
```

### Learning Flow
```mermaid
sequenceDiagram
    participant User
    participant Bob
    participant Code
    participant GitHub
    
    User->>Bob: Plan todo app (Architect)
    Bob->>User: Project structure & API design
    User->>Bob: Create backend (Code)
    Bob->>Code: Generate Flask app
    User->>Bob: Create frontend (Code)
    Bob->>Code: Generate HTML/JS/CSS
    User->>Bob: Setup version control
    Bob->>GitHub: Initialize repo & commit
    User->>Code: Test application
```

### Key Outcomes
✅ Functional todo application  
✅ Understanding of Bob modes  
✅ Experience with auto-approvals  
✅ GitHub integration knowledge  
✅ Full-stack development skills  

---

## Lab 2: Security & Analysis

### What You'll Analyze
A vulnerable todo application with intentional security flaws

### Bob Features Showcased
- ❓ **Ask Mode**: Understand existing code
- 🎯 **Plan Mode**: Plan security fixes
- 💻 **Code Mode**: Implement fixes
- 🔍 **Code Analysis**: Multi-file understanding
- 🛡️ **Security Awareness**: Vulnerability detection

### Vulnerabilities Included
```
1. SQL Injection
   Location: Backend database queries
   Risk: High
   
2. Cross-Site Scripting (XSS)
   Location: Frontend DOM manipulation
   Risk: High
   
3. Hardcoded Secrets
   Location: Configuration files
   Risk: Critical
   
4. Missing Input Validation
   Location: API endpoints
   Risk: Medium
```

### Analysis Flow
```mermaid
graph LR
    A[Vulnerable Code] --> B[Ask Mode: Understand]
    B --> C[Architect: Identify Issues]
    C --> D[Document Vulnerabilities]
    D --> E[Code Mode: Fix]
    E --> F[Verify Security]
    
    style A fill:#ffcccc
    style F fill:#ccffcc
```

### Security Fixes Applied
| Vulnerability | Fix Applied |
|--------------|-------------|
| SQL Injection | Parameterized queries |
| XSS | Input sanitization & textContent |
| Hardcoded Secrets | Environment variables |
| Input Validation | Schema validation |

### Key Outcomes
✅ Security vulnerability identification  
✅ Understanding of common attacks  
✅ Secure coding practices  
✅ Code analysis skills  
✅ Fix implementation experience  

---

## Lab 3: Code Translation

### What You'll Translate
A Python data processing script to JavaScript

### Bob Features Showcased
- ❓ **Ask Mode**: Analyze source code
- 🎯 **Plan Mode**: Plan translation strategy
- 💻 **Code Mode**: Implement translation
- 🔄 **Language Expertise**: Cross-language patterns
- 📚 **Documentation**: Maintain clarity

### Translation Challenge
```
Source Language:        Target Language:
Python 3.8+            Node.js JavaScript
- Type hints           - JSDoc comments
- List comprehensions  - Array methods
- Context managers     - Promises/async
- Built-in CSV         - csv-parser library
```

### Translation Process
```mermaid
graph TB
    A[Python Source] --> B[Analyze Structure]
    B --> C[Identify Patterns]
    C --> D[Map to JavaScript]
    D --> E[Implement Translation]
    E --> F[Test & Verify]
    F --> G[Compare Results]
    
    style A fill:#3776ab
    style G fill:#f7df1e
```

### Pattern Mapping Examples

#### List Comprehension
```python
# Python
values = [float(row[field]) for row in self.data]
```
```javascript
// JavaScript
const values = this.data.map(row => parseFloat(row[field]));
```

#### File Operations
```python
# Python
with open(filename, 'r') as file:
    data = file.read()
```

---

## Lab 4: BobShell & CLI Automation

### What You'll Build
Command-line automation scripts and CI/CD pipeline integrations using BobShell

### Bob Features Showcased
- 🖥️ **BobShell CLI**: Command-line interface mastery
- 🤖 **Automation**: Batch operations and scripting
- 🔄 **CI/CD Integration**: GitHub Actions, GitLab CI, Jenkins
- 📦 **Batch Processing**: Multi-file operations
- ⚙️ **Pipeline Development**: DevOps workflows

### Technology Stack
```
CLI Tools:          CI/CD:             Scripts:
- BobShell          - GitHub Actions   - Bash
- Bash/Shell        - GitLab CI        - Python
- Git               - Jenkins          - Node.js
```

### Learning Flow
```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Bob as BobShell
    participant CI as CI/CD Pipeline
    participant Code as Codebase
    
    Dev->>Bob: Execute command
    Bob->>Code: Generate/Analyze
    Dev->>Bob: Create automation script
    Bob->>Code: Generate script
    Dev->>CI: Integrate Bob
    CI->>Bob: Automated tasks
    Bob->>Code: Quality checks
```

### Automation Examples
```
1. Code Review Script
   - Analyze code quality
   - Generate review comments
   - Create improvement suggestions
   
2. Batch Refactoring
   - Process multiple files
   - Apply consistent patterns
   - Update documentation
   
3. Documentation Generator
   - Extract code structure
   - Generate API docs
   - Create usage examples
```

### CI/CD Integration Flow
```mermaid
graph LR
    A[Git Push] --> B[CI Trigger]
    B --> C[BobShell Analysis]
    C --> D{Quality Check}
    D -->|Pass| E[Deploy]
    D -->|Fail| F[Report Issues]
    F --> G[Developer Fix]
    G --> A
    
    style D fill:#fff4e1
    style E fill:#e1ffe1
    style F fill:#ffe1e1
```

### Key Outcomes
✅ BobShell command mastery  
✅ Automation script development  
✅ CI/CD pipeline integration  
✅ Batch operation skills  
✅ DevOps workflow understanding  

---

## Lab 5: Java Application Modernization

### What You'll Modernize
Legacy Java 8 e-commerce application upgraded to Java 17/21

### Bob Features Showcased
- 🎯 **Plan Mode**: Migration strategy planning
- 💻 **Code Mode**: Large-scale refactoring
- 🖥️ **UI Approach**: Interactive modernization
- 🖱️ **CLI Approach**: Automated refactoring
- 📊 **Pattern Recognition**: Identifying opportunities

### Technology Stack
```
Legacy:             Modern:            Tools:
- Java 8            - Java 17/21       - Bob AI
- POJOs             - Records          - Maven/Gradle
- Old patterns      - Sealed classes   - JUnit 5
                    - Pattern matching
```

### Modernization Journey
```mermaid
graph TB
    A[Java 8 Legacy Code] --> B[Analysis Phase]
    B --> C[Plan Migration]
    C --> D[Records Conversion]
    D --> E[Sealed Classes]
    E --> F[Pattern Matching]
    F --> G[Text Blocks]
    G --> H[Stream API Updates]
    H --> I[Modern Java 17/21]
    
    style A fill:#ffcccc
    style I fill:#ccffcc
```

### Modern Java Features Applied

#### Records (Java 14+)
```java
// Before: Java 8 POJO
public class Product {
    private final String id;
    private final String name;
    private final double price;
    
    // Constructor, getters, equals, hashCode, toString...
}

// After: Java 17 Record
public record Product(String id, String name, double price) {}
```

#### Sealed Classes (Java 17+)
```java
// Define permitted subclasses
public sealed interface Payment 
    permits CreditCardPayment, PayPalPayment, BankTransferPayment {}

public final class CreditCardPayment implements Payment { }
public final class PayPalPayment implements Payment { }
public final class BankTransferPayment implements Payment { }
```

#### Pattern Matching (Java 16+)
```java
// Before: Java 8
if (payment instanceof CreditCardPayment) {
    CreditCardPayment cc = (CreditCardPayment) payment;
    processCredit(cc);
}

// After: Java 17
if (payment instanceof CreditCardPayment cc) {
    processCredit(cc);
}
```

### UI vs CLI Approach
```mermaid
graph LR
    A[Modernization Task] --> B{Choose Approach}
    B -->|Learning| C[UI: Interactive]
    B -->|Production| D[CLI: Automated]
    
    C --> E[Step-by-step guidance]
    C --> F[Visual feedback]
    C --> G[Exploration]
    
    D --> H[Batch processing]
    D --> I[Repeatable]
    D --> J[CI/CD ready]
    
    style C fill:#e1f5ff
    style D fill:#fff4e1
```

### Key Outcomes
✅ Java 8 → 17/21 migration skills  
✅ Modern Java feature mastery  
✅ Large-scale refactoring experience  
✅ UI and CLI workflow understanding  
✅ Pattern recognition abilities  

---

## Lab 6: MCP Server & Custom Modes

### What You'll Build
Custom MCP server with JIRA integration and specialized DevOps mode

### Bob Features Showcased
- 🔌 **MCP Protocol**: Server development
- 🛠️ **Custom Tools**: External integrations
- 🎨 **Custom Modes**: Specialized workflows
- 🐳 **Docker Deployment**: Production setup
- 🔗 **API Integration**: Third-party services

### Technology Stack
```
Server:             Integration:       Deployment:
- Node.js           - JIRA API         - Docker
- MCP Protocol      - REST APIs        - Docker Compose
- Express           - OAuth            - Environment vars
```

### MCP Architecture
```mermaid
graph TB
    A[Bob Client] -->|MCP Protocol| B[Custom MCP Server]
    B -->|Tool: Create Issue| C[JIRA API]
    B -->|Tool: Search Issues| C
    B -->|Tool: Update Issue| C
    B -->|Tool: Add Comment| C
    
    D[Custom Mode Config] -->|Configures| A
    E[Docker Container] -->|Hosts| B
    
    C -->|Data| F[JIRA Cloud]
    
    style B fill:#4fc3f7
    style D fill:#ffe1f5
    style E fill:#e1f5ff
```

### MCP Server Development Flow
```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Bob as Bob Client
    participant MCP as MCP Server
    participant JIRA as JIRA API
    
    Dev->>Bob: Request JIRA operation
    Bob->>MCP: Call tool via MCP
    MCP->>JIRA: API request
    JIRA->>MCP: Response
    MCP->>Bob: Tool result
    Bob->>Dev: Formatted output
```

### Custom Tools Implemented

#### 1. Create JIRA Issue
```javascript
{
  name: "create_jira_issue",
  description: "Create a new JIRA issue",
  parameters: {
    project: "Project key",
    summary: "Issue summary",
    description: "Issue description",
    issueType: "bug | story | task"
  }
}
```

#### 2. Search Issues
```javascript
{
  name: "search_jira_issues",
  description: "Search JIRA issues with JQL",
  parameters: {
    jql: "JQL query string",
    maxResults: "Maximum results to return"
  }
}
```

#### 3. Update Issue
```javascript
{
  name: "update_jira_issue",
  description: "Update an existing JIRA issue",
  parameters: {
    issueKey: "Issue key (e.g., PROJ-123)",
    fields: "Fields to update"
  }
}
```

### Custom Mode Configuration

#### DevOps Mode Features
```json
{
  "name": "DevOps Mode",
  "slug": "devops",
  "systemPrompt": "Specialized for DevOps workflows",
  "tools": [
    "create_jira_issue",
    "search_jira_issues",
    "deploy_application",
    "check_pipeline_status"
  ],
  "preferences": {
    "codeStyle": "infrastructure-as-code",
    "focus": "automation and deployment"
  }
}
```

### Docker Deployment
```mermaid
graph LR
    A[Dockerfile] --> B[Build Image]
    B --> C[Docker Container]
    C --> D[MCP Server Running]
    
    E[docker-compose.yml] --> F[Multi-container Setup]
    F --> C
    F --> G[Environment Config]
    
    style C fill:#4fc3f7
    style D fill:#e1ffe1
```

### Key Outcomes
✅ MCP protocol understanding  
✅ Custom server development  
✅ External API integration  
✅ Custom mode creation  
✅ Docker deployment skills  

```javascript
// JavaScript
const data = await fs.promises.readFile(filename, 'utf8');
```

#### Class Structure
```python
# Python
class DataProcessor:
    def __init__(self, filename: str):
        self.filename = filename
```
```javascript
// JavaScript
class DataProcessor {
    constructor(filename) {
        this.filename = filename;
    }
}
```

### Key Outcomes
✅ Code translation skills  
✅ Language pattern understanding  
✅ Cross-platform development  
✅ Async/await mastery  
✅ Best practices in both languages  

---

## Overall Learning Progression

### Skill Development Path
```mermaid
graph LR
    A[Beginner] --> B[Lab 1: Building]
    B --> C[Intermediate]
    C --> D[Lab 2: Security]
    D --> E[Advanced]
    E --> F[Lab 3: Translation]
    F --> G[Expert]
    
    style A fill:#ffcccc
    style C fill:#ffffcc
    style E fill:#ccffcc
    style G fill:#ccccff
```

### Bob Mode Mastery
| Mode | Lab 1 | Lab 2 | Lab 3 | Total Usage |
|------|-------|-------|-------|-------------|
| Architect | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | High |
| Code | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | Very High |
| Ask | ⭐ | ⭐⭐⭐ | ⭐⭐ | Medium |

### Time Investment
```
Lab 1: Building          ████████████░░░░░░░░ 45 min
Lab 2: Security          ████████████░░░░░░░░ 45 min
Lab 3: Translation       ████████████░░░░░░░░ 45 min
                         ─────────────────────
Total Learning Time:     ████████████████████ 2h 15min
```

### Competency Matrix

After completing all labs, you will be able to:

| Skill | Proficiency |
|-------|-------------|
| Bob Mode Switching | ⭐⭐⭐⭐⭐ Expert |
| Auto-approvals | ⭐⭐⭐⭐⭐ Expert |
| Code Generation | ⭐⭐⭐⭐ Advanced |
| Security Analysis | ⭐⭐⭐⭐ Advanced |
| Code Translation | ⭐⭐⭐⭐ Advanced |
| GitHub Integration | ⭐⭐⭐ Intermediate |
| Literate Coding | ⭐⭐⭐⭐ Advanced |
| MCP Servers | ⭐⭐⭐ Intermediate |

---

## Prerequisites Checklist

### Required Software
- [ ] Python 3.8 or higher
- [ ] Node.js 14 or higher
- [ ] Git 2.x or higher
- [ ] Bob installed and configured
- [ ] Text editor or IDE (VS Code recommended)

### Required Knowledge
- [ ] Basic Python syntax
- [ ] Basic JavaScript syntax
- [ ] HTML/CSS fundamentals
- [ ] REST API concepts
- [ ] Git basics
- [ ] Command line usage

### Optional but Helpful
- [ ] Flask framework familiarity
- [ ] SQL basics
- [ ] Security concepts
- [ ] Async programming

### Account Setup
- [ ] GitHub account created
- [ ] Bob account configured
- [ ] GitHub MCP server connected

---

## Quick Start Guide

### 1. Verify Prerequisites
```bash
python --version    # Should be 3.8+
node --version      # Should be 14+
git --version       # Should be 2.x+
```

### 2. Clone Repository
```bash
git clone <repository-url>
cd bootcamp_intro_lab
```

### 3. Start with Lab 1
```bash
cd lab1
# Follow instructions in lab1/README.md
```

### 4. Progress Through Labs
- Complete Lab 1 before moving to Lab 2
- Complete Lab 2 before moving to Lab 3
- Take breaks between labs to absorb concepts

### 5. Get Help
- Review troubleshooting guide in `resources/troubleshooting.md`
- Check Bob features guide in `resources/bob-features-guide.md`
- Use Ask mode in Bob for questions

---

## Success Indicators

### You're Ready to Move On When:

**After Lab 1:**
- ✅ You can switch between Bob modes confidently
- ✅ Your todo app runs without errors
- ✅ You understand auto-approvals
- ✅ Your code is on GitHub

**After Lab 2:**
- ✅ You can identify security vulnerabilities
- ✅ You understand SQL injection and XSS
- ✅ You've fixed all security issues
- ✅ You can explain secure coding practices

**After Lab 3:**
- ✅ You've successfully translated Python to JavaScript
- ✅ Both versions produce identical output
- ✅ You understand language-specific patterns
- ✅ You can explain translation decisions

**After Lab 4:**
- ✅ You can use BobShell commands effectively
- ✅ Your automation scripts work correctly
- ✅ CI/CD pipeline is integrated
- ✅ You understand batch operations

**After Lab 5:**
- ✅ Java code modernized to Java 17/21
- ✅ Records and sealed classes implemented
- ✅ You understand both UI and CLI approaches
- ✅ Modern Java patterns applied correctly

**After Lab 6:**
- ✅ Custom MCP server is running
- ✅ JIRA integration works
- ✅ Custom mode is configured
- ✅ Server deployed with Docker

---

## Next Steps After Completion

### Continue Learning
1. **Build Your Own Project**: Apply Bob to a personal project
2. **Explore More MCP Servers**: Try additional integrations
3. **Advanced Security**: Deep dive into OWASP Top 10
4. **Performance Optimization**: Use Bob for code optimization
5. **Team Collaboration**: Use Bob in team settings

### Share Your Experience
- Write a blog post about your learning journey
- Share your completed projects on GitHub
- Help others in the Bob community
- Provide feedback on the labs

### Certification Path
- Complete all three labs
- Build a capstone project
- Demonstrate Bob proficiency
- Earn Bob Developer certification

---

## Support & Resources

### Documentation
- Main README: Project overview
- Lab READMEs: Detailed instructions
- Architecture docs: Technical details
- Troubleshooting: Common issues

### Community
- Bob Community Forum
- GitHub Discussions
- Stack Overflow (tag: bob-ai)
- Discord Server

### Additional Learning
- Bob Official Documentation
- Security Best Practices Guide
- Python to JavaScript Translation Guide
- MCP Server Development Guide

---

## Feedback Welcome!

We're constantly improving these labs. Please share:
- What worked well
- What was confusing
- Suggestions for improvement
- Additional topics you'd like covered

Contact: [feedback email or form]

---

**Ready to start? Head to Lab 1 and begin your Bob journey!** 🚀