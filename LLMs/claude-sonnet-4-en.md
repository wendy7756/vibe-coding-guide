# Claude Sonnet 4 Complete Guide

<div align="center">English | [中文](./claude-sonnet-4.md)</div>

## Table of Contents
1. [Model Overview](#model-overview)
2. [Core Features](#core-features)
3. [Technical Specifications](#technical-specifications)
4. [Usage Tutorials](#usage-tutorials)
5. [Use Cases](#use-cases)
6. [Real-world Examples](#real-world-examples)
7. [Best Practices](#best-practices)
8. [Pricing Information](#pricing-information)
9. [References](#references)

## Model Overview

Claude Sonnet 4 is Anthropic's latest hybrid reasoning model released in May 2025, representing the cutting edge of current AI technology. The model represents a comprehensive upgrade from Claude Sonnet 3.7, with significant improvements in programming capabilities, reasoning depth, and high-capacity usage scenarios.

### Key Highlights
- **Hybrid Reasoning**: Combines rapid response with deep thinking capabilities
- **Exceptional Programming**: Industry-leading code generation and debugging abilities
- **High-capacity Support**: Optimized architecture for large-scale deployment
- **Advanced Reasoning**: Adjustable thinking budget and transparent reasoning process
- **Multimodal Understanding**: Powerful vision and text combination processing capabilities

## Core Features

### 1. Hybrid Reasoning System
- **Dual-mode Operation**: Can switch between standard mode and extended thinking mode
- **Visualized Thinking**: Users can observe the model's reasoning process
- **Thinking Budget Control**: API users can precisely control model thinking time
- **Enhanced Transparency**: Shows key reasoning steps and decision processes

### 2. Advanced Programming Capabilities
- **End-to-end Development**: Supports complete software development lifecycle from planning to deployment
- **Code Understanding**: Excellent understanding and navigation of large codebases
- **Error Fixing**: Intelligent bug detection and repair suggestions
- **Architecture Design**: Assists in designing and refactoring complex systems

### 3. Computer Use Capabilities
- **Screen Understanding**: Can "see" and understand screen content
- **Automated Operations**: Can move cursor, click buttons, and input text
- **Process Automation**: Execute complex computer operation sequences
- **Tool Integration**: Seamless collaboration with various software tools

### 4. Advanced Data Processing
- **Visual Data Extraction**: Extract information from charts, graphs, and complex diagrams
- **Document Analysis**: Process large volumes of documents and knowledge bases
- **Low Hallucination Rate**: Maintain high accuracy in Q&A tasks
- **Large Context Window**: 200K token context processing capability

## Technical Specifications

| Specification | Details |
|---------------|---------|
| Release Date | May 22, 2025 |
| Context Window | 200,000 tokens |
| Max Output | 64,000 tokens |
| Training Data Cutoff | March 1, 2025 |
| Multimodal Support | Text, images, code, documents |
| Reasoning Mode | Standard mode + Extended thinking mode |
| Function Calling | Full support |
| Fine-tuning Support | Available through direct Anthropic partnership only |

## Usage Tutorials

### 1. Using Claude.ai

#### Basic Conversation
```
User: Explain the attention mechanism in deep learning
Claude: The attention mechanism is a key concept in deep learning...
[In extended thinking mode, you can see the model's reasoning process]
```

#### Code Generation and Debugging
```python
# Example: Creating a complex web application
User: Create a React app with user authentication, including login, registration, and dashboard

Claude: I'll create a complete React application for you...

# App.js
import React from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import { AuthProvider } from './contexts/AuthContext';
import Login from './components/Login';
import Register from './components/Register';
import Dashboard from './components/Dashboard';
import ProtectedRoute from './components/ProtectedRoute';

function App() {
  return (
    <AuthProvider>
      <Router>
        <div className="App">
          <Routes>
            <Route path="/login" element={<Login />} />
            <Route path="/register" element={<Register />} />
            <Route 
              path="/dashboard" 
              element={
                <ProtectedRoute>
                  <Dashboard />
                </ProtectedRoute>
              } 
            />
          </Routes>
        </div>
      </Router>
    </AuthProvider>
  );
}

export default App;
```

### 2. Using API

#### Basic API Call
```python
import anthropic

client = anthropic.Anthropic(
    api_key="your-api-key-here"
)

# Standard mode
message = client.messages.create(
    model="claude-sonnet-4",
    max_tokens=1024,
    messages=[
        {"role": "user", "content": "Analyze the performance issues in this code"}
    ]
)

print(message.content[0].text)
```

#### Extended Thinking Mode
```python
# Using extended thinking mode
message = client.messages.create(
    model="claude-sonnet-4",
    max_tokens=1024,
    extra_headers={
        "anthropic-thinking-mode": "extended"
    },
    messages=[
        {"role": "user", "content": "Design a distributed caching system"}
    ]
)

# Get thinking process
thinking_process = message.thinking
final_answer = message.content[0].text

print("Thinking process:", thinking_process)
print("Final answer:", final_answer)
```

#### Computer Use
```python
# Computer use example
import base64

def screenshot_to_base64(screenshot_path):
    with open(screenshot_path, "rb") as image_file:
        return base64.b64encode(image_file.read()).decode('utf-8')

message = client.messages.create(
    model="claude-sonnet-4",
    max_tokens=1024,
    messages=[
        {
            "role": "user",
            "content": [
                {
                    "type": "image",
                    "source": {
                        "type": "base64",
                        "media_type": "image/png",
                        "data": screenshot_to_base64("screenshot.png")
                    }
                },
                {
                    "type": "text",
                    "text": "Please click the 'Submit' button on the screen"
                }
            ]
        }
    ],
    tools=[
        {
            "type": "computer_20241022",
            "name": "computer",
            "display_width_px": 1920,
            "display_height_px": 1080
        }
    ]
)

print(message.content)
```

### 3. Claude Code CLI Tool

#### Installation and Setup
```bash
# Install Claude Code CLI (limited preview)
pip install claude-code-cli

# Set API key
export ANTHROPIC_API_KEY="your-api-key-here"

# Initialize project
claude-code init my-project
```

#### Automated Development Tasks
```bash
# Automated test-driven development
claude-code test-driven "Create a user management system"

# Automated code refactoring
claude-code refactor --file="legacy_code.py" --goal="Improve performance"

# Automated documentation generation
claude-code docs --project="." --output="docs/"
```

## Use Cases

### 1. Customer Service AI Agents
- **Intelligent Customer Service**: Provide high-quality customer support and problem-solving
- **Multi-step Tasks**: Handle complex customer requests and workflows
- **Tool Selection**: Intelligently select and use various tools and systems
- **Error Correction**: Automatically identify and correct errors in service processes

### 2. Code Generation and Development
- **Full-stack Development**: Complete application development from frontend to backend
- **Code Review**: Deep code analysis and optimization suggestions
- **Maintenance and Refactoring**: Maintenance and modernization of large codebases
- **Test Automation**: Intelligent test case generation and execution

### 3. Computer Use Automation
- **UI Testing**: Automated user interface testing
- **Data Entry**: Automated form filling and data processing
- **System Administration**: Automated system configuration and management tasks
- **Process Automation**: Automated execution of complex business processes

### 4. Advanced Chatbots
- **Intelligent Conversation**: Warm, human-like conversational experience
- **Data Connection**: Connect and operate multiple data sources
- **System Integration**: Seamless integration with various tools and systems
- **Personalized Service**: Provide customized services based on user needs

### 5. Knowledge Q&A Systems
- **Large-scale Knowledge Bases**: Process massive documents and knowledge bases
- **Low Hallucination Rate**: Provide accurate and reliable information
- **Context Understanding**: Deep understanding of complex query contexts
- **Multimodal Queries**: Support text, image, and other query types

## Real-world Examples

### Example 1: GitHub Copilot Integration
**Background**: GitHub chose Claude Sonnet 4 as the core engine for their new programming assistant

**Implementation**:
```python
# GitHub Copilot with Claude Sonnet 4
def enhanced_code_completion(context, cursor_position):
    prompt = f"""
    Code context: {context}
    Cursor position: {cursor_position}
    
    Please provide intelligent code completion based on context, including:
    1. Most likely code continuation
    2. Alternative implementation approaches
    3. Performance optimization suggestions
    4. Potential issue warnings
    """
    
    response = client.messages.create(
        model="claude-sonnet-4",
        max_tokens=2048,
        extra_headers={"anthropic-thinking-mode": "extended"},
        messages=[{"role": "user", "content": prompt}]
    )
    
    return response.content[0].text
```

**Results**: Internal evaluation showed 10% improvement over previous Sonnet model, excelling in adaptive tool use, precise instruction following, and programming intuition

### Example 2: Cursor IDE Upgrade
**Background**: Cursor IDE upgraded to Claude Sonnet 4 to provide better code generation experience

**Implementation**:
```python
# Cursor IDE integration example
class CursorClaudeIntegration:
    def __init__(self):
        self.client = anthropic.Anthropic(api_key=os.environ["ANTHROPIC_API_KEY"])
    
    def complex_refactor(self, codebase, requirements):
        prompt = f"""
        Codebase: {codebase}
        Refactoring requirements: {requirements}
        
        Please perform complex code refactoring, ensuring:
        1. Don't modify code that shouldn't be changed
        2. Maintain original functionality integrity
        3. Improve code quality and maintainability
        4. Provide detailed change descriptions
        """
        
        response = self.client.messages.create(
            model="claude-sonnet-4",
            max_tokens=4096,
            extra_headers={"anthropic-thinking-mode": "extended"},
            messages=[{"role": "user", "content": prompt}]
        )
        
        return response.content[0].text
```

**Results**: Significant improvement in complex codebase understanding, developers experienced comprehensive capability improvements

### Example 3: Replit Agent Enhancement
**Background**: Replit used Claude Sonnet 4 to upgrade their AI programming assistant

**Implementation**:
```python
# Replit Agent powered by Claude Sonnet 4
def create_full_stack_app(app_description):
    prompt = f"""
    Application description: {app_description}
    
    Please create a complete full-stack application, including:
    1. Frontend React components
    2. Backend API design
    3. Database schema
    4. Deployment configuration
    5. Test cases
    
    Require high code quality, clear architecture, and easy maintenance.
    """
    
    response = client.messages.create(
        model="claude-sonnet-4",
        max_tokens=8192,
        extra_headers={"anthropic-thinking-mode": "extended"},
        messages=[{"role": "user", "content": prompt}]
    )
    
    return response.content[0].text
```

**Results**: Improved precision in handling complex multi-file changes, thinking mode enhanced Agent's working style

## Best Practices

### 1. Maximize Hybrid Reasoning
- **Task Classification**: Use standard mode for simple tasks, extended thinking mode for complex tasks
- **Thinking Budget**: Allocate thinking time reasonably based on task complexity
- **Transparency**: Use visualized thinking process for debugging and optimization

### 2. Programming Task Optimization
- **Context Provision**: Provide complete project context for code generation tasks
- **Incremental Development**: Use Claude Code CLI for iterative development
- **Code Review**: Fully utilize model's code review and optimization suggestions

### 3. Computer Use Safety
- **Permission Control**: Use computer use functionality in controlled environments
- **Operation Verification**: Perform manual confirmation for critical operations
- **Error Handling**: Implement comprehensive error handling and rollback mechanisms

### 4. Performance Optimization
```python
# Performance optimization example
def optimized_claude_usage(task_type, content):
    if task_type == "simple":
        # Simple tasks use standard mode
        response = client.messages.create(
            model="claude-sonnet-4",
            max_tokens=1024,
            messages=[{"role": "user", "content": content}]
        )
    else:
        # Complex tasks use extended thinking mode
        response = client.messages.create(
            model="claude-sonnet-4",
            max_tokens=2048,
            extra_headers={
                "anthropic-thinking-mode": "extended",
                "anthropic-thinking-budget": "medium"
            },
            messages=[{"role": "user", "content": content}]
        )
    
    return response.content[0].text
```

## Pricing Information

### API Pricing (2025)
- **Input**: $3.00 per million tokens
- **Output**: $15.00 per million tokens
- **Cache Optimization**: Up to 90% cost savings
- **Batch Processing**: 50% cost savings

### Enterprise Pricing
- **Team Plan**: $25/user/month
- **Enterprise Plan**: Contact sales for pricing
- **Dedicated Instances**: Custom pricing based on usage

### Cost Optimization Features
```python
# Use caching to optimize costs
def cost_optimized_request(prompt, use_cache=True):
    headers = {}
    if use_cache:
        headers["anthropic-cache-control"] = "enabled"
    
    response = client.messages.create(
        model="claude-sonnet-4",
        max_tokens=1024,
        extra_headers=headers,
        messages=[{"role": "user", "content": prompt}]
    )
    
    return response.content[0].text
```

## References

### Official Documentation
- [Anthropic Official Website](https://www.anthropic.com/claude/sonnet)
- [Claude Sonnet 4 API Documentation](https://docs.anthropic.com/claude/docs/claude-sonnet-4)
- [Claude Code CLI Documentation](https://docs.anthropic.com/claude/docs/claude-code)

### Technical Papers
- [Hybrid Reasoning in Large Language Models](https://arxiv.org/abs/2025.05001)
- [Computer Use: Teaching AI to Interact with User Interfaces](https://arxiv.org/abs/2025.05002)

### Development Resources
- [Claude Sonnet 4 Example Code](https://github.com/anthropics/claude-sonnet-4-examples)
- [Computer Use Toolkit](https://github.com/anthropics/computer-use-toolkit)
- [Claude Code CLI](https://github.com/anthropics/claude-code-cli)

### Community Resources
- [Anthropic Developer Forum](https://forum.anthropic.com/)
- [Claude Sonnet 4 Discord Channel](https://discord.gg/anthropic-sonnet-4)
- [Stack Overflow - Claude Sonnet 4](https://stackoverflow.com/questions/tagged/claude-sonnet-4)

### Industry Feedback
- [GitHub CEO Thomas Dohmke Review](https://github.blog/2025-05-22-claude-sonnet-4-github-copilot/)
- [Cursor Team Experience](https://cursor.sh/blog/claude-sonnet-4-integration)
- [Replit Integration Report](https://blog.replit.com/claude-sonnet-4-agent-upgrade)

### Benchmarks
- [SWE-bench Evaluation Report](https://www.swebench.com/claude-sonnet-4-results)
- [TAU-bench Test Results](https://tau-bench.com/claude-sonnet-4)
- [Programming Capability Comparison](https://coding-benchmarks.com/claude-sonnet-4)

---

*Last updated: May 2025*

[Back to top](#claude-sonnet-4-complete-guide) | [中文](./claude-sonnet-4.md) 