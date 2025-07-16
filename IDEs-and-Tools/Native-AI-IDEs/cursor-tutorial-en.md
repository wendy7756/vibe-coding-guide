<div align="center">

# Cursor IDE Tutorial (2025 Latest Version)

<a href="cursor-tutorial.md">中文</a> | English

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

Cursor is an AI-native IDE built on VS Code, developed by Anysphere. It's hailed as "the future of AI programming" and reached a valuation of $9 billion in 2025 with $300 million in annual revenue, making it one of the fastest-growing SaaS products.

### Core Features
- **AI-Native Design**: AI capabilities integrated from the ground up
- **Deep Codebase Understanding**: Complete project context awareness
- **Multi-Model Support**: Supports GPT-4.1, Claude 3.7, Gemini, and more
- **Agent Mode**: Automated programming agents
- **Real-time Collaboration**: Team AI programming support

## 2025 Latest Features

### 🚀 Cursor 1.0 Major Update
- **Release Date**: June 2025
- **New Agent Engine**: Smarter code generation and refactoring
- **BugBot**: Automated bug detection and fixing
- **One-Click MCP Install**: Simplified Model Context Protocol setup

### 🤖 Background Agents
- **Cloud Parallel Processing**: Multiple tasks running simultaneously
- **Automatic Branch Management**: Intelligent branch creation and switching
- **PR Automation**: Complete workflow from code to PR
- **Cost Optimization**: Uses Max Mode with pay-as-you-go pricing

### 🎯 Enhanced Composer Features
- **Multi-file Editing**: Edit multiple files simultaneously
- **Project-level Refactoring**: Large-scale code refactoring support
- **Real-time Preview**: Instant preview of changes
- **Smart Merging**: Automatic conflict resolution

### 🔧 Deep IDE Integration
- **VS Code Compatible**: Full extension ecosystem support
- **Native Terminal**: Enhanced terminal experience
- **Git Integration**: Deep version control support
- **Debugging Tools**: AI-assisted debugging features

## Pricing Plans

| Plan | Price | Features | Use Case |
|------|-------|----------|----------|
| **Hobby** | Free | 2000 completions, 50 slow requests | Personal learning and small projects |
| **Pro** | $20/month | Unlimited completions, 500 requests, unlimited slow requests | Professional developers |
| **Business** | $40/user/month | Team management, privacy mode, centralized billing | Teams and enterprises |

### Max Mode Pricing
- **Pay-as-you-go**: Billing based on token usage
- **Advanced Models**: Access to latest AI models
- **Suitable for**: Complex problem solving, large projects

## Installation and Setup

### 1. Download and Install
```bash
# Official website download
https://cursor.sh/

# Supported platforms
- Windows 10/11
- macOS 10.15+
- Linux (Ubuntu, CentOS)
```

### 2. Initial Setup
```bash
# First launch setup
1. Download and run Cursor installer
2. Choose theme and keyboard shortcuts
3. Login to GitHub account
4. Configure AI model preferences
5. Import VS Code settings (optional)
```

### 3. Basic Configuration
```json
// cursor.json recommended configuration
{
  "ai.model": "claude-3.7-sonnet",
  "ai.temperature": 0.3,
  "composer.enabled": true,
  "background.agents": true,
  "editor.tabSize": 2,
  "cursor.rules": [
    "Use TypeScript for all new files",
    "Follow React best practices",
    "Write comprehensive tests"
  ]
}
```

### 4. .cursorrules File
```bash
# Create .cursorrules file in project root
# Example configuration
Use TypeScript for all new JavaScript files
Follow ESLint configuration
Write JSDoc comments for all functions
Prefer functional components over class components
Use React hooks instead of lifecycle methods
Write unit tests for all utility functions
```

## Core Features

### 1. Intelligent Code Completion
```python
# Example: Python Flask API auto-completion
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/api/users', methods=['POST'])
def create_user():
    # Cursor will automatically suggest complete user creation logic
    data = request.get_json()
    
    # Input validation
    if not data or 'username' not in data:
        return jsonify({'error': 'Username is required'}), 400
    
    # User creation logic
    user = {
        'id': generate_id(),
        'username': data['username'],
        'email': data.get('email'),
        'created_at': datetime.now().isoformat()
    }
    
    # Save to database
    db.users.insert_one(user)
    
    return jsonify(user), 201
```

### 2. Chat Functionality
```bash
# Keyboard shortcuts
Ctrl+L (Windows/Linux) or Cmd+L (Mac)  # Open Chat

# Common commands
@filename      # Reference specific file
@selection     # Reference selected code
@project       # Reference entire project
@docs          # Reference project documentation
```

### 3. Composer Mode
```bash
# Activate Composer
Ctrl+Shift+I  # Open Composer panel

# Composer capabilities
- Multi-file simultaneous editing
- Project-level refactoring
- Automatic test generation
- Documentation updates
- Dependency management
```

### 4. Agent Mode Usage
```bash
# Enable Agent Mode
1. Open Chat panel
2. Input complex task description
3. Agent will automatically:
   - Analyze project structure
   - Plan implementation steps
   - Generate complete code
   - Run tests for verification
   - Create PR
```

### 5. Background Agents Feature
```bash
# Using Background Agents
1. Enable Background Agents in settings
2. Assign tasks using screenshots or descriptions
3. Agents process in parallel in the cloud
4. View progress and results
5. Review and merge changes
```

## Use Cases and Examples

### Case 1: Full-Stack Application Development
```javascript
// Requirement: Create a complete Todo application
// Using Composer mode to generate frontend and backend code at once

// Frontend React Component
import React, { useState, useEffect } from 'react';
import axios from 'axios';

const TodoApp = () => {
  const [todos, setTodos] = useState([]);
  const [newTodo, setNewTodo] = useState('');

  useEffect(() => {
    fetchTodos();
  }, []);

  const fetchTodos = async () => {
    try {
      const response = await axios.get('/api/todos');
      setTodos(response.data);
    } catch (error) {
      console.error('Error fetching todos:', error);
    }
  };

  const addTodo = async () => {
    if (!newTodo.trim()) return;
    
    try {
      const response = await axios.post('/api/todos', {
        text: newTodo,
        completed: false
      });
      setTodos([...todos, response.data]);
      setNewTodo('');
    } catch (error) {
      console.error('Error adding todo:', error);
    }
  };

  return (
    <div className="todo-app">
      <h1>Todo List</h1>
      <div className="add-todo">
        <input
          type="text"
          value={newTodo}
          onChange={(e) => setNewTodo(e.target.value)}
          onKeyPress={(e) => e.key === 'Enter' && addTodo()}
          placeholder="Add a new todo..."
        />
        <button onClick={addTodo}>Add</button>
      </div>
      <ul className="todo-list">
        {todos.map(todo => (
          <li key={todo.id} className={todo.completed ? 'completed' : ''}>
            {todo.text}
          </li>
        ))}
      </ul>
    </div>
  );
};

export default TodoApp;
```

### Case 2: Code Refactoring and Optimization
```typescript
// Original code (needs refactoring)
class UserService {
  private users: any[] = [];
  
  public addUser(user: any) {
    this.users.push(user);
  }
  
  public getUser(id: number) {
    return this.users.find(u => u.id === id);
  }
}

// Cursor refactored code
interface User {
  id: number;
  username: string;
  email: string;
  createdAt: Date;
}

class UserService {
  private users: Map<number, User> = new Map();
  
  public addUser(user: Omit<User, 'id' | 'createdAt'>): User {
    const newUser: User = {
      id: Date.now(),
      ...user,
      createdAt: new Date()
    };
    
    this.users.set(newUser.id, newUser);
    return newUser;
  }
  
  public getUser(id: number): User | undefined {
    return this.users.get(id);
  }
  
  public getAllUsers(): User[] {
    return Array.from(this.users.values());
  }
  
  public deleteUser(id: number): boolean {
    return this.users.delete(id);
  }
}
```

### Case 3: Automated Test Generation
```javascript
// Original function
function calculateTax(income, deductions) {
  const taxableIncome = Math.max(0, income - deductions);
  let tax = 0;
  
  if (taxableIncome <= 50000) {
    tax = taxableIncome * 0.1;
  } else if (taxableIncome <= 100000) {
    tax = 5000 + (taxableIncome - 50000) * 0.2;
  } else {
    tax = 15000 + (taxableIncome - 100000) * 0.3;
  }
  
  return Math.round(tax * 100) / 100;
}

// Cursor generated test cases
describe('calculateTax', () => {
  test('should calculate tax for income below 50000', () => {
    expect(calculateTax(40000, 5000)).toBe(3500);
    expect(calculateTax(30000, 10000)).toBe(2000);
  });
  
  test('should calculate tax for income between 50000 and 100000', () => {
    expect(calculateTax(75000, 5000)).toBe(9000);
    expect(calculateTax(100000, 10000)).toBe(13000);
  });
  
  test('should calculate tax for income above 100000', () => {
    expect(calculateTax(150000, 10000)).toBe(27000);
    expect(calculateTax(200000, 20000)).toBe(39000);
  });
  
  test('should handle edge cases', () => {
    expect(calculateTax(0, 0)).toBe(0);
    expect(calculateTax(50000, 60000)).toBe(0);
    expect(calculateTax(50000, 0)).toBe(5000);
  });
});
```

### Case 4: Automatic Documentation Generation
```python
# Original code
def process_order(order_data, customer_id):
    # Order processing logic
    pass

# Cursor generated documented code
def process_order(order_data: dict, customer_id: int) -> dict:
    """
    Process customer order
    
    Args:
        order_data (dict): Order data containing the following fields:
            - items (list): List of order items
            - shipping_address (str): Shipping address
            - payment_method (str): Payment method
        customer_id (int): Customer ID
    
    Returns:
        dict: Processing result containing the following fields:
            - order_id (str): Order ID
            - status (str): Order status
            - total_amount (float): Total order amount
            - estimated_delivery (str): Estimated delivery time
    
    Raises:
        ValueError: When order data is invalid
        CustomerNotFoundError: When customer doesn't exist
    
    Example:
        >>> order = {
        ...     "items": [{"id": 1, "quantity": 2}],
        ...     "shipping_address": "123 Main St",
        ...     "payment_method": "credit_card"
        ... }
        >>> result = process_order(order, 12345)
        >>> print(result['order_id'])
        ORD-2025-001
    """
    # Validate customer exists
    if not customer_exists(customer_id):
        raise CustomerNotFoundError(f"Customer {customer_id} not found")
    
    # Validate order data
    if not order_data or 'items' not in order_data:
        raise ValueError("Invalid order data")
    
    # Process order logic
    order_id = generate_order_id()
    total_amount = calculate_total(order_data['items'])
    
    # Create order record
    order = {
        'order_id': order_id,
        'customer_id': customer_id,
        'items': order_data['items'],
        'total_amount': total_amount,
        'status': 'pending',
        'created_at': datetime.now().isoformat()
    }
    
    # Save to database
    save_order(order)
    
    return {
        'order_id': order_id,
        'status': 'pending',
        'total_amount': total_amount,
        'estimated_delivery': calculate_delivery_date()
    }
```

## Best Practices

### 1. Project Setup Optimization
```bash
# Create high-quality .cursorrules file
echo "Use TypeScript for all new files
Follow project's ESLint configuration
Write comprehensive JSDoc comments
Prefer functional programming patterns
Use React hooks instead of class components
Write unit tests for all business logic
Follow REST API conventions
Use semantic commit messages" > .cursorrules
```

### 2. Effective Prompt Engineering
```markdown
# Good prompt example
Create a user authentication system including:
- JWT token authentication
- Password hashing storage
- Login attempt limitation
- Password reset functionality
- Role-based permission management
- Use TypeScript and Express
- Include comprehensive error handling
- Write unit tests
```

### 3. Team Collaboration Configuration
```json
// Team shared configuration
{
  "team.shared.rules": [
    "Use consistent code formatting",
    "Follow team naming conventions",
    "Write descriptive commit messages",
    "Include tests for new features"
  ],
  "team.models": {
    "primary": "claude-3.7-sonnet",
    "fallback": "gpt-4.1"
  },
  "team.budget": {
    "monthly_limit": 1000,
    "per_user_limit": 100
  }
}
```

### 4. Cost Optimization Strategies
```bash
# Cost control best practices
1. Use free tier for learning and experimentation
2. Reserve Pro plan for complex tasks
3. Use Max Mode judiciously
4. Monitor usage regularly
5. Train team for efficient AI usage
```

## FAQ

### Q1: What's the difference between Cursor and VS Code?
**A**: Cursor is an AI-native IDE built on VS Code with deeply integrated AI features including complete codebase understanding, intelligent Agent mode, and real-time AI collaboration. VS Code requires extensions for AI functionality.

### Q2: Is the Background Agents feature secure?
**A**: Yes, Background Agents run in the cloud but code processing follows strict privacy policies. Enterprise users can enable privacy mode to ensure sensitive code isn't stored or shared.

### Q3: How to handle code quality issues with AI-generated code?
**A**: 
- Use detailed .cursorrules files
- Regular code reviews
- Establish test-driven development workflow
- Use static analysis tools
- Train team in AI collaboration skills

### Q4: What programming languages does Cursor support?
**A**: Cursor supports all major programming languages including JavaScript/TypeScript, Python, Java, C++, Rust, Go, etc. AI understanding may vary across languages.

### Q5: How to deploy Cursor in a team environment?
**A**: 
- Choose Business plan
- Configure team shared rules
- Establish usage guidelines
- Monitor usage and costs
- Provide team training

## References

### Official Resources
- [Cursor Official Website](https://cursor.sh/)
- [Cursor Documentation](https://docs.cursor.sh/)
- [Cursor Community Forum](https://forum.cursor.com/)

### Technical Deep Dive
- [How Cursor Works Internally](https://adityarohilla.com/2025/05/08/how-cursor-works-internally/)
- [AI Programming Tools Comparison](https://www.enginelabs.ai/blog/cursor-ai-an-in-depth-review-may-2025-update)
- [Background Agents Usage Guide](https://decoupledlogic.com/2025/05/29/background-agents-in-cursor-cloud-powered-coding-at-scale/)

### Latest Updates
- [Cursor 1.0 Update Changelog](https://forum.cursor.com/t/cursor-1-0-update-changelog/51000)
- [Background Agents Feature Release](https://cursor.sh/blog/background-agents)
- [MCP Integration Guide](https://cursor.sh/blog/mcp-integration)

### Community Resources
- [Cursor Tips and Tricks](https://forum.cursor.com/c/tips-and-tricks)
- [Project Templates Repository](https://github.com/cursor-templates)
- [User Success Stories](https://cursor.sh/stories)

### Learning Tutorials
- [Cursor Beginner's Guide](https://www.youtube.com/watch?v=rKDJs2TdMRA)
- [Advanced Features Tutorial](https://www.youtube.com/watch?v=5REHY4vxKSM)
- [Team Collaboration Practices](https://cursor.sh/blog/team-collaboration)

---

**Last Updated**: July 2025
**Version**: v2.0
**Author**: Vibe Coding Guide Team

**Other Language Versions**: [中文](cursor-tutorial.md) 