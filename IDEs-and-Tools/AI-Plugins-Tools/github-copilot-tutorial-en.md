<div align="center">

# GitHub Copilot Tutorial (2025 Latest Version)

<a href="github-copilot-tutorial.md">中文</a> | English

</div>

## Table of Contents
- [Introduction](#introduction)
- [2025 Latest Features](#2025-latest-features)
- [Pricing Plans](#pricing-plans)
- [Installation and Setup](#installation-and-setup)
- [Core Features](#core-features)
- [Use Cases and Examples](#use-cases-and-examples)
- [Best Practices](#best-practices)
- [FAQ](#faq)
- [References](#references)

## Introduction

GitHub Copilot is an AI programming assistant jointly developed by GitHub and OpenAI, hailed as the pioneer of "AI pair programming." The 2025 version brings revolutionary updates including multi-model support, Agent mode, and enterprise-grade features.

### Core Features
- **AI Code Completion**: Real-time intelligent code suggestions
- **Chat Functionality**: Multi-platform conversational programming support
- **Agent Mode**: Automated programming agents
- **Multi-Model Support**: Including GPT-4.1, o3, Claude Opus 4, and more
- **Enterprise Security**: GDPR compliant and enterprise-ready

## 2025 Latest Features

### 🚀 GitHub Copilot Pro+ Plan
- **Release Date**: April 4, 2025
- **Pricing**: $39/month or $390/year
- **Exclusive Features**: 
  - Priority access to latest models (GPT-4.5, etc.)
  - 1500 premium requests per month
  - Early access to new features

### 🤖 Copilot Coding Agent
- **New Agent Mode**: Full code project management support
- **Background Agents**: Cloud-based parallel task processing
- **Auto PR Creation**: Automated workflow from issue to PR
- **MCP Support**: Model Context Protocol integration

### 🎯 Enhanced Chat Features
- **Multi-Model Selection**: Choose different AI models in VS Code, GitHub, mobile
- **Image to Issue**: Generate bug reports directly from screenshots
- **Real-time Code Review**: Automated code quality checks

## Pricing Plans

| Plan | Price | Premium Requests | Use Case |
|------|-------|------------------|----------|
| **Copilot Free** | Free | 50/month | Personal learning and small projects |
| **Copilot Pro** | $10/month or $100/year | 300/month | Individual developers |
| **Copilot Pro+** | $39/month or $390/year | 1500/month | AI power users |
| **Copilot Business** | $19/user/month | 300/user/month | Teams and organizations |
| **Copilot Enterprise** | $39/user/month | 1000/user/month | Enterprise needs |

### Supported AI Models
- **GPT Series**: GPT-4.1, GPT-4o, o3, o3-mini, o4-mini
- **Claude Series**: Claude Opus 4, Claude Sonnet 3.5/3.7/4
- **Google Series**: Gemini 2.5 Pro, Gemini 2.0 Flash

## Installation and Setup

### 1. Get GitHub Copilot
```bash
# Method 1: Subscribe through GitHub website
https://github.com/features/copilot

# Method 2: Free access for students and teachers
https://github.com/education
```

### 2. IDE Integration

#### VS Code
```bash
# Install GitHub Copilot Extension
1. Open VS Code
2. Press Ctrl+Shift+X to open Extensions panel
3. Search for "GitHub Copilot"
4. Click Install
5. Restart VS Code and login to GitHub account
```

#### JetBrains IDEs
```bash
# Supports IntelliJ IDEA, PyCharm, WebStorm, etc.
1. Open IDE Settings (File → Settings)
2. Select Plugins
3. Search for "GitHub Copilot"
4. Install and restart IDE
5. Login to GitHub account for authorization
```

### 3. Basic Configuration
```json
// VS Code settings.json recommended configuration
{
  "github.copilot.enable": {
    "*": true,
    "yaml": false,
    "plaintext": false
  },
  "github.copilot.advanced": {
    "length": 500,
    "temperature": 0.1
  }
}
```

## Core Features

### 1. Code Completion
```python
# Example: Python function auto-completion
def calculate_fibonacci(n):
    # Copilot will automatically suggest complete Fibonacci implementation
    if n <= 1:
        return n
    return calculate_fibonacci(n-1) + calculate_fibonacci(n-2)
```

### 2. Chat Functionality
```bash
# Using in VS Code
Ctrl+Shift+I  # Open Copilot Chat

# Common Chat commands
/explain     # Explain code
/fix         # Fix code issues
/tests       # Generate test code
/doc         # Generate documentation
```

### 3. Agent Mode Usage
```bash
# Enable Copilot Coding Agent
1. Open project in VS Code
2. Use Ctrl+Shift+P to open command palette
3. Search for "Copilot: Enable Agent Mode"
4. Select task type to execute

# Tasks Agent can handle
- Complete feature implementation
- Multi-file refactoring
- Test case generation
- Code review and optimization
```

### 4. Useful Shortcuts
```bash
# VS Code shortcuts
Tab           # Accept suggestion
Ctrl+→        # Accept word suggestion
Ctrl+Enter    # View all suggestions
Alt+]         # Next suggestion
Alt+[         # Previous suggestion
Ctrl+Shift+I  # Open Copilot Chat
```

## Use Cases and Examples

### Case 1: Rapid Prototyping
```javascript
// Requirement: Create a React login component
// Just input comments, Copilot will generate complete component
// Create a React login component with username and password fields
import React, { useState } from 'react';

const LoginComponent = () => {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    // Login logic
    console.log('Login attempt:', { username, password });
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        placeholder="Username"
        value={username}
        onChange={(e) => setUsername(e.target.value)}
      />
      <input
        type="password"
        placeholder="Password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
      <button type="submit">Login</button>
    </form>
  );
};
```

### Case 2: Code Refactoring and Optimization
```python
# Using Chat for code refactoring
# Original code
def process_data(data):
    result = []
    for item in data:
        if item > 0:
            result.append(item * 2)
    return result

# Input in Chat: "/optimize this function for better performance"
# Copilot's optimized version
def process_data(data):
    return [item * 2 for item in data if item > 0]
```

### Case 3: Test Case Generation
```java
// Original method
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}

// Generate tests using /tests command
@Test
public void testAdd() {
    Calculator calc = new Calculator();
    assertEquals(5, calc.add(2, 3));
    assertEquals(0, calc.add(-1, 1));
    assertEquals(-5, calc.add(-2, -3));
}
```

### Case 4: Enterprise Code Review
```bash
# Using Copilot Code Review Agent
1. Create Pull Request
2. Enable automatic code review
3. Copilot will automatically check:
   - Code quality issues
   - Security vulnerabilities
   - Performance issues
   - Best practice compliance
```

## Best Practices

### 1. Prompt Engineering
```python
# Good prompt example
# Create a Python function that validates email addresses using regex
# Parameters: email (string)
# Returns: boolean (True if valid, False otherwise)
# Handle edge cases like empty strings and None values

def validate_email(email):
    # Copilot will generate more accurate implementation
    pass
```

### 2. Code Quality Assurance
```bash
# Configure code quality checks
1. Enable code reference filter
2. Set organization-level coding standards
3. Use custom instruction files (.copilotignore)
4. Regularly review AI-generated code
```

### 3. Team Collaboration
```markdown
# Team Copilot usage guidelines
- Use consistent model configurations
- Establish code review processes
- Share best practices regularly
- Monitor usage and costs
```

### 4. Security Considerations
```bash
# Enterprise security configuration
1. Enable content filters
2. Configure code exclusion rules
3. Monitor sensitive information leakage
4. Regular audit of usage logs
```

## FAQ

### Q1: Is GitHub Copilot compatible with other code repository platforms?
**A**: Yes, GitHub Copilot works in any code editor regardless of code hosting platform. However, using GitHub provides better integration experience.

### Q2: How to handle copyright issues with Copilot-generated code?
**A**: GitHub Copilot includes optional code reference filters that can detect and suppress suggestions matching public code on GitHub. Enterprise users can enable this feature.

### Q3: How is personal data and code privacy protected?
**A**: 
- Copilot Business and Enterprise data is not used for model training
- Privacy mode support
- GDPR and other data protection compliance
- Configurable content exclusion rules

### Q4: How to optimize Copilot usage costs?
**A**: 
- Choose appropriate plan based on needs
- Use premium request budget controls
- Optimize prompt quality to reduce repeated requests
- Monitor usage regularly

### Q5: What types of projects is Agent mode suitable for?
**A**: 
- Small to medium feature development
- Code refactoring projects
- Test case generation
- Documentation writing
- Not suitable for complex architectural design

## References

### Official Documentation
- [GitHub Copilot Official Documentation](https://docs.github.com/en/copilot)
- [Copilot API Reference](https://docs.github.com/en/rest/copilot)
- [Enterprise Deployment Guide](https://docs.github.com/en/enterprise-cloud@latest/copilot)

### Latest Updates
- [GitHub Copilot Pro+ Release Announcement](https://github.blog/changelog/2025-04-04-announcing-github-copilot-pro/)
- [Claude Sonnet 4 Support](https://github.blog/changelog/2025-06-25-anthropic-claude-sonnet-4-and-claude-opus-4-are-now-generally-available-in-github-copilot/)
- [MCP Support Release](https://github.blog/changelog/2025-07-14-model-context-protocol-mcp-support-in-vs-code-is-generally-available/)

### Community Resources
- [GitHub Copilot Community Forum](https://github.com/community/community/discussions/categories/copilot)
- [VS Code Copilot Extension Documentation](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)
- [Enterprise Success Stories](https://github.com/customer-stories)

### Learning Resources
- [GitHub Copilot Learning Path](https://github.com/skills/copilot-codespaces-vscode)
- [AI Programming Best Practices](https://github.blog/2023-06-20-how-to-write-better-prompts-for-github-copilot/)
- [Copilot Tips and Tricks](https://github.com/features/copilot#getting-started)

---

**Last Updated**: July 2025
**Version**: v2.0
**Author**: Vibe Coding Guide Team

**Other Language Versions**: [中文](github-copilot-tutorial.md) 