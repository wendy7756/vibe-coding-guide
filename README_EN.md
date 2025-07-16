<div align="center">

# Vibe Coding Guide

<a href="README.md">中文</a> | English

</div>

As a product manager with zero coding background, I successfully developed **6 iOS apps** and got them live on the App Store in the past three months with the help of ChatGPT and Cursor, and also launched **2 complete website projects**. Both website codes are open sourced: Global Travel Guide platform [Global Travel Guide](https://github.com/wendy7756/globaltravelguide), and social media follower analysis tool [FollowNet](https://github.com/wendy7756/FollowNet).

I still don't understand programming today, but AI wrote all the code for me. With AI, anyone can become an independent developer. Having personally experienced the power of AI programming, I created this open source project **Vibe Coding Guide** to help everyone with ideas create their own products using AI, ensuring technology is no longer a barrier to realizing creativity.

<div align="center">
<img src="my-experience/6apps.jpeg" alt="myapps" width="70%">
</div>

---

## Abstract

Vibe Coding is a revolutionary programming paradigm where AI takes the lead in code generation while developers guide the entire process in a "flow state"-like manner. Coined by OpenAI co-founder Andrej Karpathy in 2025, it emphasizes developers describing requirements through natural language (text or voice), while AI generates complete, runnable code. Developers only need to iterate, provide feedback, and test to complete project development.

## Table of Contents

- [What is Vibe Coding](#what-is-vibe-coding)
- [Core Workflow](#core-workflow)
- [Technical Principles and Implementation](#technical-principles-and-implementation)
- [Main Tools and Platforms](#main-tools-and-platforms)
- [Project Types and Examples](#project-types-and-examples)
- [Practical Tutorials](#practical-tutorials)
- [Best Practices](#best-practices)
- [Community and Resources](#community-and-resources)
- [References](#references)

## What is Vibe Coding

Vibe Coding is a revolutionary programming approach that transforms traditional hand-coding into collaborative dialogue with AI. Developers no longer need to write code line by line; instead, they describe desired functionality in natural language, and AI generates complete, runnable code.

### Core Definition

Vibe Coding can be defined as: **A collaborative programming approach where developers describe requirements through natural language (text or voice), AI (Large Language Models) generates complete runnable code, and developers enter a "flow state" through iterative feedback**.

### Origin and Development

The concept of Vibe Coding was introduced by Andrej Karpathy (OpenAI co-founder, former Tesla AI head) in early 2025. He described this approach as "fully giving in to the AI's vibe," emphasizing:
- **Natural Interaction**: Conversing with AI in natural language to describe desired functionality
- **Rapid Iteration**: AI generates code, developers test and provide feedback
- **Flow State**: Developers focus on creativity and logic rather than syntax details

### Technical Foundation

The technical foundation of Vibe Coding includes:
- **Large Language Models (LLMs)**: Such as GPT-4, Claude, Gemini, etc.
- **Natural Language Processing (NLP)**: Understanding developers' requirement descriptions
- **Code Generation Technology**: Converting requirements into executable code
- **Real-time Feedback Systems**: Supporting rapid iteration and correction

## Core Workflow

The core workflow of Vibe Coding is a continuous iterative loop with the following specific steps:

### 1. Natural Language Description (Natural Language Input)

Developers describe the functionality they want to implement using natural language:
- **Requirement Description**: Clearly express desired functionality and effects
- **Context Provision**: Provide relevant background information and constraints
- **Goal Clarification**: Specify expected output results

**Example**:
```
"Create a user registration page with username, email, and password input fields,
including form validation and submission functionality, using the right tech stack"
```

### 2. AI Code Generation (AI Code Generation)

AI analyzes the description and generates corresponding code:
- **Requirement Analysis**: Understand developer's intentions and requirements
- **Code Generation**: Create complete, runnable code
- **Best Practices**: Follow programming standards and security guidelines

### 3. Execute & Observe (Execute & Observe)

Developers run the AI-generated code:
- **Code Execution**: Run the generated code to view effects
- **Functionality Testing**: Verify if requirements are met
- **Issue Identification**: Discover potential bugs or improvement points

### 4. Feedback & Refinement (Feedback & Refinement)

Provide feedback based on test results:
- **Error Reporting**: Report discovered problems and errors
- **Functionality Adjustments**: Request modifications or feature enhancements
- **Optimization Suggestions**: Propose performance or user experience improvements

**Example Feedback**:
```
"The button color should be blue, and password validation should include special character requirements"
```

### 5. Iteration Loop (Iteration Loop)

Repeat the above process until requirements are satisfied:
- **Continuous Improvement**: Multiple iterations to refine functionality
- **Incremental Development**: Gradually add new features
- **Quality Assurance**: Ensure code quality and stability

## Technical Principles and Implementation

### Core Technical Architecture

#### Large Language Models (LLMs)
Vibe Coding relies on advanced large language models:
- **GPT-4/GPT-4o**: OpenAI's latest model with powerful code generation capabilities
- **Claude 3.5 Sonnet**: Anthropic's high-performance model, excellent at complex reasoning
- **Gemini Pro**: Google's multimodal model supporting text and image understanding


#### Natural Language Processing Pipeline
1. **Intent Recognition**: Understanding developers' real needs
2. **Context Analysis**: Considering project background and constraints
3. **Technology Selection**: Choosing appropriate tech stacks and frameworks
4. **Code Generation**: Producing structured, runnable code
5. **Quality Checking**: Automatically detecting potential issues and improvements

#### Real-time Feedback Mechanisms
- **Error Detection**: Real-time identification of syntax and logic errors
- **Performance Analysis**: Evaluating code efficiency and optimization suggestions
- **Security Scanning**: Detecting potential security vulnerabilities
- **Best Practices**: Ensuring code compliance with industry standards

### Implementation Methods

#### IDE-based Integration
- **Real-time Completion**: Providing intelligent code suggestions in editors
- **Context Awareness**: Understanding entire project code structure
- **Multi-file Coordination**: Handling cross-file code dependencies

#### Conversational Development
- **Chat Interface**: Developing through natural language conversations
- **Multi-turn Interaction**: Supporting continuous requirement clarification and code improvement
- **History Recording**: Remembering previous conversations and decisions

#### Autonomous Agent Systems
- **Task Decomposition**: Breaking complex requirements into manageable small tasks
- **Automatic Execution**: AI can autonomously complete certain development steps
- **Quality Assurance**: Built-in testing and validation mechanisms

## Main Tools and Platforms

### AI Programming Assistants

#### Mainstream AI Programming Tools
- **GitHub Copilot**: AI programming assistant jointly developed by GitHub and OpenAI
- **Cursor**: AI-native IDE based on VS Code, supporting complete conversational programming
- **Claude Code**: Anthropic's Claude model, excellent at code generation and debugging


#### Professional Programming Extensions
- **Cline**: Open-source VS Code extension supporting planning and executing development tasks
- **Roo Code**: Autonomous development agent capable of cycling through plan-code-test-debug
- **Tabnine**: AI-based code completion tool
- **CodeWhisperer**: Amazon's AI code generation service

### Conversational Development Platforms

#### No-Code AI Builders
- **Lovable**: Browser-based AI application building platform
- **Vitara**: Full-stack application generator supporting natural language descriptions
- **Bolt.new**: StackBlitz's AI-driven full-stack development environment
- **v0.dev**: Vercel's AI interface generation tool

#### Professional Development Environments
- **Replit**: Cloud IDE supporting AI collaboration
- **CodeSandbox**: Online code editor with integrated AI assistant
- **Gitpod**: Cloud development environment with AI-enhanced features

### Specialized AI Tools

#### Code Review and Testing
- **Sweep AI**: AI tool for automatically generating Pull Request fixes
- **Codium**: AI-driven testing generation and code review tool
- **DeepCode**: AI-based code quality analysis
- **Snyk Code**: AI-enhanced security vulnerability detection

#### Project Management and Collaboration
- **Linear**: Project management tool with integrated AI features
- **Notion AI**: Documentation and project management supporting AI collaboration
- **GitHub Issues AI**: Automatic analysis and handling of GitHub Issues

## Project Types and Examples

### Rapid Prototyping

#### 1. Flight Simulator Game Built in 3 Hours
- **Developer**: Pieter Levels (Independent developer)
- **Tools**: Cursor IDE + Grok-3 AI
- **Results**: 320,000 players in 17 days, $87,000 monthly revenue
- **Feature**: 3D multiplayer game built entirely through natural language descriptions
- **Case**: [fly.pieter.com](https://fly.pieter.com)

#### 2. LunchBox Buddy App
- **Developer**: Kevin Roose (Journalist, non-programmer)
- **Method**: Pure conversational development, no manual coding
- **Function**: Personalized lunch recommendation app
- **Significance**: Proves non-technical backgrounds can develop applications

### Startup Projects

#### 1. AI-Driven SaaS Applications
- **Statistics**: 25% of Y Combinator Winter 2025 batch startups
- **Feature**: 95% AI-generated codebases
- **Advantage**: Small teams (<10 people) achieving million-dollar revenue
- **Cases**: Multiple Y Combinator incubated projects

#### 2. Enterprise Application Development
- **ANZ Bank**: 7% of code in the past 6 months from AI pair programming
- **Citi Bank**: 40,000 developers using Copilot comprehensively
- **Effectiveness**: Significantly improved development efficiency and code quality

### Personal Creative Projects

#### 1. Personal Website Generator
- **Description**: "Create a modern personal portfolio website"
- **Generated**: Complete React + Tailwind CSS application
- **Time**: Less than 30 minutes from description to deployment
- **Features**: Responsive design, dark mode, animations

#### 2. Data Dashboard
- **Requirement**: "Create a real-time data dashboard for the sales team"
- **Implementation**: Next.js + Chart.js + API integration
- **Functions**: Real-time data updates, interactive charts, export functionality

### Learning and Educational Projects

#### 1. Programming Learning Assistant
- **Function**: Learn programming concepts through conversation
- **Implementation**: Natural language explanation of code logic
- **Features**: Personalized learning paths, real-time feedback

#### 2. Code Review Tool
- **Purpose**: Automatically review code quality and security
- **Capabilities**: Identify potential bugs, provide improvement suggestions
- **Integration**: Seamless integration with GitHub/GitLab platforms

### Creative and Art Projects

#### 1. Generative Art Project
- **Description**: "Create an interactive particle system artwork"
- **Technology**: P5.js + WebGL
- **Features**: Mouse interaction, real-time animation, audio response

#### 2. Music Visualizer
- **Requirement**: "Generate visual effects based on music beats"
- **Implementation**: Web Audio API + Canvas animation
- **Functions**: Spectrum analysis, dynamic colors, beat detection

### Enterprise Solutions

#### 1. Customer Service Chatbot
- **Scenario**: Create intelligent customer service for e-commerce platform
- **Capabilities**: Natural language understanding, order queries, problem solving
- **Integration**: Seamless connection with existing CRM systems

#### 2. Content Management System
- **Requirement**: "Build a multilingual content management platform"
- **Functions**: Article editing, user management, permission control
- **Features**: AI-based content recommendation and automatic translation

## Practical Tutorials

### Beginner Tutorial: Your First Vibe Coding Project

#### Step 1: Choose AI Programming Tools
Recommended tools for beginners:
- **Cursor**: Download and install Cursor IDE
- **GitHub Copilot**: Install Copilot extension in VS Code
- **Claude**: Visit claude.ai for conversational programming

#### Step 2: Create Project Prompts
Clear requirement descriptions are key to success:

**Effective Prompt Example**:
```
"I want to create a todo application with the following features:
1. Add, edit, delete todo items
2. Mark completion status
3. Sort by date
4. Use React and Tailwind CSS
5. Store data in localStorage
6. Include dark mode toggle"
```

#### Step 3: Collaborate with AI Development
Start the collaborative development process with AI:

**Conversation Flow**:
1. **Initial Requirements**: Describe the desired application
2. **AI Response**: AI generates code framework
3. **Run Tests**: Execute the generated code
4. **Feedback & Correction**: Report issues or request improvements
5. **Iterative Optimization**: Repeat until satisfied

**Example Conversation**:
```
You: "Help me create a simple calculator app"
AI: [Generates HTML+CSS+JavaScript code]
You: "The buttons are too small, can you make them bigger?"
AI: [Modifies CSS styles, increases button size]
You: "Add keyboard support"
AI: [Adds keyboard event listeners]
```

#### Step 4: Optimization and Deployment
Refine the project and deploy:

**Optimization Checklist**:
- [ ] Functional completeness testing
- [ ] Responsive design verification
- [ ] Performance optimization check
- [ ] Error handling improvement
- [ ] Code quality review

**Deployment Options**:
- **Vercel**: Best for React/Next.js applications
- **Netlify**: Static website deployment
- **GitHub Pages**: Free static hosting

### Advanced Tutorial: Complex Project Vibe Coding

#### Project Decomposition Strategy
Break large projects into manageable modules:

1. **User Interface Layer**:
   ```
   "Create the main application layout with navigation bar, sidebar, and main content area"
   ```

2. **Data Layer**:
   ```
   "Design user data models including registration, login, and profile management"
   ```

3. **Business Logic Layer**:
   ```
   "Implement core functionality logic such as search, filtering, and data processing"
   ```

#### Multi-round Conversation Management
Techniques for maintaining context continuity:

**Context Prompts**:
```
"Based on the user authentication system we created earlier, now add password reset functionality"
```

**Referencing Previous Code**:
```
"Modify the login component we discussed earlier to add a 'Remember Me' option"
```

#### Code Review and Refactoring
Using AI for code optimization:

**Refactoring Prompts**:
```
"Please review this code for performance and maintainability, and provide improvement suggestions"
```

**Security Check**:
```
 "Check this user input handling code for security vulnerabilities"
 ```

## Best Practices

### Effective Prompt Engineering

#### 1. Clear Requirement Descriptions
Good prompts should have the following characteristics:
- **Specific and Clear**: Avoid vague statements, provide concrete functional requirements
- **Technology Stack Declaration**: Clearly specify desired technologies and frameworks
- **Constraint Conditions**: Explain performance, compatibility, and other limitations
- **Expected Results**: Describe the expected final outcome

**Example Comparison**:
```
❌ Poor Prompt:
"Make a website"

✅ Good Prompt:
"Create a responsive personal blog website using React and Tailwind CSS,
including article list, detail pages, search functionality, and Markdown rendering support"
```

#### 2. Iterative Development
- **Small Steps**: Only request implementation of one small feature at a time
- **Gradual Improvement**: Propose improvements based on previous results
- **Maintain Context**: Reference previous code in conversations

### Code Quality Assurance

#### 1. Code Review Points
- **Functional Correctness**: Verify code implements expected functionality
- **Performance Optimization**: Check for potential performance bottlenecks
- **Security**: Review for potential security vulnerabilities
- **Maintainability**: Assess code readability and extensibility

#### 2. Testing Strategy
- **Unit Testing**: Request AI to generate corresponding test code
- **Integration Testing**: Verify collaboration between different modules
- **User Testing**: Test actual usage scenarios

### Team Collaboration Standards

#### 1. Prompt Standardization
Establish unified prompt templates for the team:
```
Project Background: [Project Overview]
Technology Stack: [Technologies Used]
Functional Requirements: [Specific Feature List]
Design Requirements: [UI/UX Requirements]
Performance Requirements: [Performance Metrics]
```

#### 2. Code Management
- **Version Control**: Use Git to manage AI-generated code
- **Branch Strategy**: Create branches for different AI experiments
- **Code Review**: Human review of all AI-generated code

### Security and Privacy

#### 1. Data Protection
- **Sensitive Information**: Avoid including sensitive data in prompts
- **Code Review**: Check generated code for information leakage
- **Local Deployment**: Consider using locally deployed AI models

#### 2. Intellectual Property
- **License Compliance**: Ensure used code complies with license requirements
- **Originality**: Verify originality of generated code
- **Attribution**: Properly attribute AI-generated code segments

### Common Issues and Solutions

#### 1. Poor AI-Generated Code Quality
**Problem**: Code contains bugs or doesn't follow best practices
**Solutions**:
- Provide more specific technical requirements
- Generate step-by-step, gradually improving
- Combine with human review and correction

#### 2. Context Loss
**Problem**: AI forgets previous conversation content
**Solutions**:
- Re-provide key information in new conversations
- Use code comments to record design decisions
- Maintain conversation continuity

#### 3. Over-reliance on AI
**Problem**: Team members lack basic programming skills
**Solutions**:
- Balance AI use with traditional learning
- Conduct regular technical training
- Establish code review mechanisms

## Community and Resources

### Learning Resources

#### Vibe Coding Specialized Resources
- **Vibe Coding Guide**: [https://ai-hive.net/datacenters/vibe-coding](https://ai-hive.net/datacenters/vibe-coding)
- **Andrej Karpathy's Blog**: [https://karpathy.ai](https://karpathy.ai)
- **MIT Technology Review**: [Vibe Coding Explained](https://www.technologyreview.com/2025/04/16/1115135/what-is-vibe-coding-exactly/)

#### AI Programming Tutorials
- **Prompt Engineering Guide**: [https://www.promptingguide.ai](https://www.promptingguide.ai)
- **OpenAI Cookbook**: [https://cookbook.openai.com](https://cookbook.openai.com)
- **Anthropic's Claude Documentation**: [https://docs.anthropic.com](https://docs.anthropic.com)

#### Video Tutorials
- **Cursor IDE Tutorials**: Official tutorials on YouTube
- **GitHub Copilot Best Practices**: Microsoft Learn
- **AI Programming Tips**: Fireship, Code with Antonio

#### Technical Blogs
- **Google Cloud AI Blog**: [https://cloud.google.com/blog/topics/ai-ml](https://cloud.google.com/blog/topics/ai-ml)
- **Hugging Face Blog**: [https://huggingface.co/blog](https://huggingface.co/blog)
- **OpenAI Research**: [https://openai.com/research](https://openai.com/research)

### Open Source Projects

#### Vibe Coding Related Projects
- **Aider**: [https://github.com/paul-gauthier/aider](https://github.com/paul-gauthier/aider) - Command-line AI programming assistant
- **Cline**: [https://github.com/cline/cline](https://github.com/cline/cline) - VS Code autonomous development extension
- **Devin**: [https://github.com/Cognition-AI/devin](https://github.com/Cognition-AI/devin) - AI software engineer

#### Prompt Engineering Libraries
- **LangChain**: [https://github.com/langchain-ai/langchain](https://github.com/langchain-ai/langchain)
- **Guidance**: [https://github.com/guidance-ai/guidance](https://github.com/guidance-ai/guidance)
- **Promptflow**: [https://github.com/microsoft/promptflow](https://github.com/microsoft/promptflow)

### Community Platforms

#### Discussion Communities
- **Reddit r/MachineLearning**: AI programming discussions
- **Discord Servers**: Official groups for Cursor IDE, GitHub Copilot
- **Stack Overflow**: AI programming related questions

#### Developer Communities
- **Hugging Face Community**: [https://huggingface.co/community](https://huggingface.co/community)
- **OpenAI Community**: [https://community.openai.com](https://community.openai.com)
- **GitHub Discussions**: Discussion areas for major AI programming tools

### Tools and Platforms

#### AI Programming Tools
- **Cursor**: [https://cursor.sh](https://cursor.sh)
- **GitHub Copilot**: [https://github.com/features/copilot](https://github.com/features/copilot)
- **Windsurf**: [https://codeium.com/windsurf](https://codeium.com/windsurf)
- **Replit**: [https://replit.com](https://replit.com)

#### Online IDEs
- **CodeSandbox**: [https://codesandbox.io](https://codesandbox.io)
- **StackBlitz**: [https://stackblitz.com](https://stackblitz.com)
- **Gitpod**: [https://gitpod.io](https://gitpod.io)

#### Deployment Platforms
- **Vercel**: [https://vercel.com](https://vercel.com)
- **Netlify**: [https://netlify.com](https://netlify.com)
- **Railway**: [https://railway.app](https://railway.app)

## References

### Core Literature

1. **Karpathy, A.** (2025). *Vibe Coding: A New Programming Paradigm*. OpenAI Blog.
2. **Chen, M., et al.** (2021). *Evaluating Large Language Models Trained on Code*. arXiv:2107.03374.
3. **Austin, J., et al.** (2021). *Program Synthesis with Large Language Models*. arXiv:2108.07732.
4. **Li, Y., et al.** (2022). *Competition-Level Code Generation with AlphaCode*. Science, 378(6624), 1092-1097.
5. **Nijkamp, E., et al.** (2022). *CodeGen: An Open Large Language Model for Code Generation*. arXiv:2203.13474.

### Technical Research

6. **Fried, D., et al.** (2023). *InCoder: A Generative Model for Code Infilling and Synthesis*. ICLR 2023.
7. **Wang, Y., et al.** (2023). *CodeT5+: Open Code Large Language Models for Code Understanding and Generation*. arXiv:2305.07922.
8. **Rozière, B., et al.** (2023). *Code Llama: Open Foundation Models for Code*. arXiv:2308.12950.
9. **Zheng, S., et al.** (2024). *SWE-RL: Training Code Generation Models with Reinforcement Learning from Software Engineering Feedback*. arXiv:2401.03994.

### Industry Reports

10. **Y Combinator** (2025). *AI-Generated Codebases in Startup Ecosystem*. YC Research.
11. **GitHub** (2024). *GitHub Copilot Impact Report: Developer Productivity Study*. GitHub Inc.
12. **McKinsey & Company** (2024). *The Economic Impact of AI-Assisted Programming*. McKinsey Global Institute.
13. **Stack Overflow** (2024). *Developer Survey: AI Tools in Programming*. Stack Overflow Insights.

### Web Resources

#### Official Documentation
- **OpenAI Codex**: [https://openai.com/blog/openai-codex](https://openai.com/blog/openai-codex)
- **GitHub Copilot Documentation**: [https://docs.github.com/en/copilot](https://docs.github.com/en/copilot)
- **Anthropic Claude for Coding**: [https://docs.anthropic.com/claude/docs/coding](https://docs.anthropic.com/claude/docs/coding)

#### Research Institutions
- **MIT CSAIL**: [https://www.csail.mit.edu](https://www.csail.mit.edu)
- **Stanford HAI**: [https://hai.stanford.edu](https://hai.stanford.edu)
- **Google Research**: [https://research.google](https://research.google)

#### Technical Blogs
- **The Pragmatic Engineer**: [https://blog.pragmaticengineer.com](https://blog.pragmaticengineer.com)
- **Towards Data Science**: [https://towardsdatascience.com](https://towardsdatascience.com)
- **AI Research**: [https://ai.googleblog.com](https://ai.googleblog.com)

#### Academic Databases
- **arXiv Computer Science**: [https://arxiv.org/list/cs/recent](https://arxiv.org/list/cs/recent)
- **ACM Digital Library**: [https://dl.acm.org](https://dl.acm.org)
- **IEEE Xplore**: [https://ieeexplore.ieee.org](https://ieeexplore.ieee.org)

#### Open Source Projects
- **Hugging Face Code Models**: [https://huggingface.co/models?pipeline_tag=text-generation&other=code](https://huggingface.co/models?pipeline_tag=text-generation&other=code)
- **Papers with Code**: [https://paperswithcode.com/task/code-generation](https://paperswithcode.com/task/code-generation)
- **Awesome AI for Code**: [https://github.com/sourcegraph/awesome-ai-coding](https://github.com/sourcegraph/awesome-ai-coding)

---

## Contributing

We welcome contributions to this guide! Please follow these steps:

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Create a Pull Request

## License

This project is licensed under the Apache License 2.0. See the [LICENSE](LICENSE) file for details.

## Contact Us

- **Issues**: [GitHub Issues](https://github.com/your-username/vibe-coding-guide/issues)
- **Discussions**: [GitHub Discussions](https://github.com/your-username/vibe-coding-guide/discussions)
- **Email**: vibe-coding@example.com

---

*Make programming a beautiful experience.* 