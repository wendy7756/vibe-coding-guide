<div align="center">

# Claude Code Tutorial (2025 Latest Version)

<a href="claude-code-tutorial.md">中文</a> | English

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

Claude Code is an AI programming assistant developed by Anthropic, based on the Claude series of large language models. The 2025 version introduces revolutionary Computer Use API, hybrid reasoning capabilities, and extended thinking features, establishing itself as a new benchmark in AI programming.

### Core Features
- **Hybrid Reasoning Model**: Supports both fast inference and deep thinking modes
- **Computer Use API**: Direct computer interface manipulation
- **Multimodal Support**: Handles text, images, code, and documents
- **Extended Thinking**: Supports step-by-step complex problem solving
- **API Integration**: Flexible API interface supporting multiple programming languages

## 2025 Latest Features

### 🚀 Claude 3.7 Sonnet Release
- **Release Date**: February 24, 2025
- **Hybrid Reasoning**: Dual-mode operation with standard and extended thinking modes
- **200K Token Output**: Significantly increased output capacity
- **Programming Performance**: Achieves SOTA performance in programming tasks
- **Action Scaling**: Supports iterative function calls and environmental interactions

### 🤖 Claude 4 Sonnet and Opus 4
- **Claude 4 Sonnet**: Latest version balancing performance and speed
- **Claude Opus 4**: Most powerful model designed for complex problem solving
- **Vision Capabilities**: Improved image understanding and analysis
- **Tool Use**: Enhanced function calling and API integration

### 🖥️ Computer Use API
- **Screen Control**: Direct GUI interface manipulation
- **Automated Tasks**: Execute complex computer operations
- **Cross-platform Support**: Supports Windows, macOS, and Linux
- **Security Restrictions**: Strict permission control and security measures

### 🧠 Extended Thinking Capabilities
- **Deep Reasoning**: Supports multi-step analysis of complex problems
- **Chain of Thought**: Clear display of reasoning process
- **Self-correction**: Ability to check and correct own reasoning
- **Creative Thinking**: Supports creative problem solving

## Pricing Plans

### API Pricing (Token-based)

| Model | Input Price (per 1M tokens) | Output Price (per 1M tokens) | Use Case |
|-------|----------------------------|------------------------------|----------|
| **Claude 3 Haiku** | $0.25 | $1.25 | Simple tasks and quick responses |
| **Claude 3 Sonnet** | $3.00 | $15.00 | Balanced performance and cost |
| **Claude 3.5 Sonnet** | $3.00 | $15.00 | Enhanced balanced model |
| **Claude 3.7 Sonnet** | $3.00 | $15.00 | Latest hybrid reasoning model |
| **Claude 4 Sonnet** | $3.00 | $15.00 | Latest balanced model |
| **Claude 3 Opus** | $15.00 | $75.00 | Complex tasks and high-quality needs |
| **Claude Opus 4** | $15.00 | $75.00 | Most powerful model |

### Subscription Plans

| Plan | Price | Features | Use Case |
|------|-------|----------|----------|
| **Free Tier** | $0 | Limited requests, basic features | Trial and learning |
| **Pro Plan** | $20/month | More requests, priority queue | Individual developers |
| **Team Plan** | $25/user/month | Team collaboration, higher limits | Small teams |
| **Enterprise** | Custom | Unlimited, dedicated support | Enterprise clients |

## Installation and Setup

### 1. Get API Key
```bash
# Visit Anthropic official website
https://console.anthropic.com/

# Steps
1. Register Anthropic account
2. Verify email and phone
3. Enter API console
4. Create new API key
5. Save key securely
```

### 2. Environment Setup
```bash
# Install Python SDK
pip install anthropic

# Set environment variable
export ANTHROPIC_API_KEY="your_api_key_here"

# Or create .env file
echo "ANTHROPIC_API_KEY=your_api_key_here" > .env
```

### 3. Basic Configuration
```python
# Python configuration example
import anthropic
import os

# Initialize client
client = anthropic.Anthropic(
    api_key=os.getenv("ANTHROPIC_API_KEY")
)

# Basic configuration
default_config = {
    "model": "claude-3.7-sonnet",
    "max_tokens": 4096,
    "temperature": 0.3,
    "system": "You are a helpful AI programming assistant."
}
```

### 4. Multi-language SDKs
```bash
# JavaScript/TypeScript
npm install @anthropic-ai/sdk

# Python
pip install anthropic

# Java
<dependency>
    <groupId>com.anthropic</groupId>
    <artifactId>anthropic-java</artifactId>
    <version>1.0.0</version>
</dependency>

# Go
go get github.com/anthropic/anthropic-go
```

## Core Features

### 1. Code Generation and Completion
```python
# Example: Generate complete API service
import anthropic

client = anthropic.Anthropic()

response = client.messages.create(
    model="claude-3.7-sonnet",
    max_tokens=2000,
    system="You are an expert Python developer. Generate clean, production-ready code.",
    messages=[
        {
            "role": "user",
            "content": "Create a FastAPI service for user management with CRUD operations, including authentication and input validation."
        }
    ]
)

print(response.content[0].text)
```

### 2. Hybrid Reasoning Mode
```python
# Enable extended thinking mode
response = client.messages.create(
    model="claude-3.7-sonnet",
    max_tokens=4000,
    system="Use extended thinking mode for complex problems.",
    messages=[
        {
            "role": "user",
            "content": "Design a distributed system architecture for a high-traffic e-commerce platform. Consider scalability, reliability, and performance."
        }
    ]
)
```

### 3. Computer Use API
```python
# Computer use example
def use_computer_api(task_description):
    response = client.messages.create(
        model="claude-3.7-sonnet",
        max_tokens=1000,
        tools=[
            {
                "type": "computer_20241022",
                "name": "computer",
                "display_width_px": 1920,
                "display_height_px": 1080
            }
        ],
        messages=[
            {
                "role": "user",
                "content": f"Please help me with this task: {task_description}"
            }
        ]
    )
    return response

# Usage example
result = use_computer_api("Open a text editor and create a simple HTML page")
```

### 4. Multimodal Processing
```python
# Image and code analysis
import base64

def analyze_code_screenshot(image_path):
    with open(image_path, "rb") as image_file:
        image_data = base64.b64encode(image_file.read()).decode()
    
    response = client.messages.create(
        model="claude-3.7-sonnet",
        max_tokens=1000,
        messages=[
            {
                "role": "user",
                "content": [
                    {
                        "type": "image",
                        "source": {
                            "type": "base64",
                            "media_type": "image/png",
                            "data": image_data
                        }
                    },
                    {
                        "type": "text",
                        "text": "Analyze this code screenshot and suggest improvements."
                    }
                ]
            }
        ]
    )
    
    return response.content[0].text

# Usage example
analysis = analyze_code_screenshot("code_screenshot.png")
```

### 5. Function Calling and Tool Use
```python
# Define tool functions
def get_weather(location):
    # Mock weather API call
    return f"Weather in {location}: 22°C, sunny"

# Configure tools
tools = [
    {
        "name": "get_weather",
        "description": "Get current weather for a location",
        "input_schema": {
            "type": "object",
            "properties": {
                "location": {
                    "type": "string",
                    "description": "City name"
                }
            },
            "required": ["location"]
        }
    }
]

# Use tools
response = client.messages.create(
    model="claude-3.7-sonnet",
    max_tokens=1000,
    tools=tools,
    messages=[
        {
            "role": "user",
            "content": "What's the weather like in San Francisco?"
        }
    ]
)
```

## Use Cases and Examples

### Case 1: Complex Algorithm Implementation
```python
# Requirement: Implement an efficient graph algorithm
prompt = """
Implement a graph algorithm for social network analysis, including:
1. Graph representation and storage
2. Shortest path algorithm
3. Community detection algorithm
4. Influence analysis
5. Parallel processing support
6. Complete test cases
"""

response = client.messages.create(
    model="claude-3.7-sonnet",
    max_tokens=4000,
    system="You are an expert in graph algorithms and parallel computing.",
    messages=[{"role": "user", "content": prompt}]
)

# Claude generates complete graph algorithm implementation
# (Full implementation would be quite lengthy)
```

### Case 2: Automated DevOps Scripts
```python
# Requirement: Create automated deployment and monitoring system
prompt = """
Create a Python script that implements:
1. Automated application deployment
2. System monitoring and alerting
3. Log analysis
4. Automatic failure recovery
5. Performance metrics collection
6. Email notification system
"""

response = client.messages.create(
    model="claude-3.7-sonnet",
    max_tokens=3000,
    system="You are a DevOps expert specializing in automation and monitoring.",
    messages=[{"role": "user", "content": prompt}]
)

# Claude generates comprehensive DevOps automation script
# (Implementation details would be extensive)
```

### Case 3: Data Analysis and Visualization
```python
# Requirement: Create comprehensive data analysis tool
prompt = """
Create a Python data analysis tool including:
1. Data cleaning and preprocessing
2. Statistical analysis and hypothesis testing
3. Machine learning model training
4. Interactive data visualization
5. Report generation
6. Real-time data processing
"""

response = client.messages.create(
    model="claude-3.7-sonnet",
    max_tokens=4000,
    system="You are a data science expert with extensive Python analytics experience.",
    messages=[{"role": "user", "content": prompt}]
)

# Claude generates comprehensive data analysis framework
# (Would include pandas, scikit-learn, plotly implementation)
```

### Case 4: Natural Language Processing API
```python
# Requirement: Create text analysis API service
prompt = """
Create a FastAPI service providing NLP features:
1. Text sentiment analysis
2. Entity recognition
3. Text summarization
4. Keyword extraction
5. Text classification
6. Language detection
7. Text similarity computation
"""

response = client.messages.create(
    model="claude-3.7-sonnet",
    max_tokens=3000,
    system="You are an NLP expert specializing in text analysis and API development.",
    messages=[{"role": "user", "content": prompt}]
)

# Claude generates complete NLP API service
# (Would include FastAPI, spaCy, transformers implementation)
```

## Best Practices

### 1. Cost Optimization Strategies
```python
# Intelligent model selection
def choose_model_by_task(task_complexity):
    if task_complexity == 'simple':
        return 'claude-3-haiku'
    elif task_complexity == 'medium':
        return 'claude-3.7-sonnet'
    else:
        return 'claude-opus-4'

# Response caching
import hashlib
import json
import os

class ResponseCache:
    def __init__(self, cache_dir='cache'):
        self.cache_dir = cache_dir
        os.makedirs(cache_dir, exist_ok=True)
    
    def get_cache_key(self, prompt, model):
        content = f"{prompt}_{model}"
        return hashlib.md5(content.encode()).hexdigest()
    
    def get_cached_response(self, prompt, model):
        cache_key = self.get_cache_key(prompt, model)
        cache_file = os.path.join(self.cache_dir, f"{cache_key}.json")
        
        if os.path.exists(cache_file):
            with open(cache_file, 'r') as f:
                return json.load(f)
        return None
    
    def save_response(self, prompt, model, response):
        cache_key = self.get_cache_key(prompt, model)
        cache_file = os.path.join(self.cache_dir, f"{cache_key}.json")
        
        with open(cache_file, 'w') as f:
            json.dump(response, f)
```

### 2. Security and Privacy Protection
```python
# Data sanitization
import re

def sanitize_prompt(prompt):
    """Remove sensitive information"""
    # Remove emails
    prompt = re.sub(r'\S+@\S+\.\S+', '[EMAIL]', prompt)
    # Remove phone numbers
    prompt = re.sub(r'\b\d{3}-\d{3}-\d{4}\b', '[PHONE]', prompt)
    # Remove ID numbers
    prompt = re.sub(r'\b\d{15}|\d{18}\b', '[ID]', prompt)
    
    return prompt

# Request limiting
from functools import wraps
import time

class RateLimiter:
    def __init__(self, max_requests=100, time_window=3600):
        self.max_requests = max_requests
        self.time_window = time_window
        self.requests = {}
    
    def is_allowed(self, user_id):
        now = time.time()
        if user_id not in self.requests:
            self.requests[user_id] = []
        
        # Clean expired requests
        self.requests[user_id] = [
            req_time for req_time in self.requests[user_id]
            if now - req_time < self.time_window
        ]
        
        if len(self.requests[user_id]) >= self.max_requests:
            return False
        
        self.requests[user_id].append(now)
        return True
```

### 3. Error Handling and Retry Mechanisms
```python
import time
import random
from functools import wraps

def retry_with_backoff(max_retries=3, backoff_factor=1.5):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_retries):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_retries - 1:
                        raise e
                    
                    wait_time = backoff_factor ** attempt + random.uniform(0, 1)
                    time.sleep(wait_time)
            
        return wrapper
    return decorator

@retry_with_backoff(max_retries=3)
def call_claude_api(prompt, model='claude-3.7-sonnet'):
    response = client.messages.create(
        model=model,
        max_tokens=1000,
        messages=[{"role": "user", "content": prompt}]
    )
    return response.content[0].text
```

### 4. Performance Monitoring and Logging
```python
import logging
import time
from datetime import datetime

class APIMonitor:
    def __init__(self):
        self.setup_logging()
        self.metrics = {
            'request_count': 0,
            'total_tokens': 0,
            'total_cost': 0.0,
            'avg_response_time': 0.0
        }
    
    def setup_logging(self):
        logging.basicConfig(
            level=logging.INFO,
            format='%(asctime)s - %(levelname)s - %(message)s',
            handlers=[
                logging.FileHandler('claude_api.log'),
                logging.StreamHandler()
            ]
        )
        self.logger = logging.getLogger(__name__)
    
    def log_request(self, prompt, model, response_time, tokens_used):
        self.metrics['request_count'] += 1
        self.metrics['total_tokens'] += tokens_used
        self.metrics['avg_response_time'] = (
            (self.metrics['avg_response_time'] * (self.metrics['request_count'] - 1) + response_time) 
            / self.metrics['request_count']
        )
        
        self.logger.info(f"Request completed - Model: {model}, Response time: {response_time:.2f}s, "
                        f"Tokens used: {tokens_used}")
    
    def get_metrics(self):
        return self.metrics
```

## FAQ

### Q1: How to choose the right Claude model?
**A**: Choose based on task complexity:
- **Simple tasks**: Claude 3 Haiku (fast, low-cost)
- **Balanced needs**: Claude 3.7 Sonnet (performance-cost balance)
- **Complex tasks**: Claude Opus 4 (highest performance)

### Q2: How to control API usage costs?
**A**: 
- Implement request caching
- Choose appropriate models by task
- Set token limits
- Use batching to reduce requests
- Monitor and analyze usage

### Q3: What are the limitations of Computer Use API?
**A**: 
- Requires explicit permission authorization
- Cannot execute dangerous operations
- Has strict security checks
- Limited to specific use cases

### Q4: How to handle API limits and rate limiting?
**A**: 
- Implement retry mechanisms
- Use exponential backoff algorithms
- Monitor API usage
- Reserve buffer time
- Consider using multiple API keys

### Q5: How to ensure data security and privacy?
**A**: 
- Data sanitization
- Use HTTPS transmission
- Don't include sensitive info in prompts
- Regularly rotate API keys
- Follow data protection regulations

## References

### Official Documentation
- [Anthropic Official Documentation](https://docs.anthropic.com/)
- [Claude API Reference](https://docs.anthropic.com/claude/reference/)
- [Computer Use API Guide](https://docs.anthropic.com/claude/docs/computer-use)

### Pricing and Billing
- [API Pricing Page](https://www.anthropic.com/pricing)
- [Token Calculator](https://platform.anthropic.com/token-calculator)
- [Cost Optimization Guide](https://apidog.com/blog/claude-api-cost/)

### Technical Resources
- [Claude 3.7 Sonnet Release Notes](https://aimlapi.com/models/claude-3-7-sonnet-api)
- [Claude Code Tutorial](https://www.youtube.com/watch?v=P_pTypZZL4c)
- [Python SDK Documentation](https://github.com/anthropics/anthropic-sdk-python)

### Community and Support
- [Anthropic Community Forum](https://community.anthropic.com/)
- [Discord Server](https://discord.gg/anthropic)
- [GitHub Issues](https://github.com/anthropics/anthropic-sdk-python/issues)

### Best Practices
- [Prompt Engineering Guide](https://docs.anthropic.com/claude/docs/prompt-engineering)
- [Security Best Practices](https://docs.anthropic.com/claude/docs/safety-best-practices)
- [Performance Optimization Tips](https://docs.anthropic.com/claude/docs/performance-optimization)

---

**Last Updated**: July 2025
**Version**: v2.0
**Author**: Vibe Coding Guide Team

**Other Language Versions**: [中文](claude-code-tutorial.md) 