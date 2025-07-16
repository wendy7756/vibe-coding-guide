# Cursor IDE 使用教程 (2025年最新版)

**语言**: [中文](#) | [English](cursor-tutorial-en.md)

## 目录
- [简介](#简介)
- [2025年最新功能](#2025年最新功能)
- [定价方案](#定价方案)
- [安装和设置](#安装和设置)
- [核心功能详解](#核心功能详解)
- [使用场景和案例](#使用场景和案例)
- [最佳实践](#最佳实践)
- [常见问题](#常见问题)
- [参考资料](#参考资料)

## 简介

Cursor是一款基于VS Code的AI原生IDE，由Anysphere公司开发。它被誉为"AI编程的未来"，在2025年估值达到90亿美元，年收入达到3亿美元，是目前增长最快的SaaS产品之一。

### 核心特性
- **AI原生设计**: 从底层架构就融入AI能力
- **深度代码库理解**: 完整项目上下文感知
- **多模型支持**: 支持GPT-4.1、Claude 3.7、Gemini等
- **Agent模式**: 自动化编程代理
- **实时协作**: 团队AI编程支持

## 2025年最新功能

### 🚀 Cursor 1.0 重大更新
- **发布时间**: 2025年6月
- **新Agent引擎**: 更智能的代码生成和重构
- **BugBot**: 自动化bug检测和修复
- **一键MCP安装**: 简化Model Context Protocol设置

### 🤖 背景代理 (Background Agents)
- **云端并行处理**: 多任务同时执行
- **自动分支管理**: 智能创建和切换分支
- **PR自动化**: 从代码到PR的完整流程
- **成本优化**: 使用Max Mode，按需付费

### 🎯 增强的Composer功能
- **多文件编辑**: 同时编辑多个文件
- **项目级重构**: 大规模代码重构支持
- **实时预览**: 即时查看修改效果
- **智能合并**: 自动解决代码冲突

### 🔧 深度IDE集成
- **VS Code兼容**: 完整的扩展生态支持
- **原生终端**: 增强的终端体验
- **Git集成**: 深度版本控制支持
- **调试工具**: AI辅助调试功能

## 定价方案

| 计划 | 价格 | 功能 | 适用场景 |
|-----|------|------|----------|
| **Hobby** | 免费 | 2000次补全，50次慢请求 | 个人学习和小项目 |
| **Pro** | $20/月 | 无限补全，500次请求，无限慢请求 | 专业开发者 |
| **Business** | $40/用户/月 | 团队管理，隐私模式，中央计费 | 团队和企业 |

### Max Mode 定价
- **按需付费**: 根据token使用量计费
- **高级模型**: 访问最新的AI模型
- **适合场景**: 复杂问题求解，大型项目

## 安装和设置

### 1. 下载和安装
```bash
# 官方网站下载
https://cursor.sh/

# 支持平台
- Windows 10/11
- macOS 10.15+
- Linux (Ubuntu, CentOS)
```

### 2. 初始设置
```bash
# 首次启动设置
1. 下载并运行Cursor安装程序
2. 选择主题和快捷键配置
3. 登录GitHub账户
4. 配置AI模型偏好
5. 导入VS Code设置（可选）
```

### 3. 基本配置
```json
// cursor.json 推荐配置
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

### 4. .cursorrules 文件
```bash
# 在项目根目录创建 .cursorrules 文件
# 示例配置
Use TypeScript for all new JavaScript files
Follow ESLint configuration
Write JSDoc comments for all functions
Prefer functional components over class components
Use React hooks instead of lifecycle methods
Write unit tests for all utility functions
```

## 核心功能详解

### 1. 智能代码补全
```python
# 示例：Python Flask API自动补全
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/api/users', methods=['POST'])
def create_user():
    # Cursor会自动建议完整的用户创建逻辑
    data = request.get_json()
    
    # 验证输入
    if not data or 'username' not in data:
        return jsonify({'error': 'Username is required'}), 400
    
    # 创建用户逻辑
    user = {
        'id': generate_id(),
        'username': data['username'],
        'email': data.get('email'),
        'created_at': datetime.now().isoformat()
    }
    
    # 保存到数据库
    db.users.insert_one(user)
    
    return jsonify(user), 201
```

### 2. Chat功能
```bash
# 快捷键
Ctrl+L (Windows/Linux) 或 Cmd+L (Mac)  # 打开Chat

# 常用命令
@文件名        # 引用特定文件
@代码选择      # 引用选中代码
@项目         # 引用整个项目
@文档         # 引用项目文档
```

### 3. Composer模式
```bash
# 激活Composer
Ctrl+Shift+I  # 打开Composer面板

# Composer能力
- 多文件同时编辑
- 项目级重构
- 自动测试生成
- 文档自动更新
- 依赖管理
```

### 4. Agent模式使用
```bash
# 启用Agent模式
1. 打开Chat面板
2. 输入复杂任务描述
3. Agent会自动：
   - 分析项目结构
   - 规划实现步骤
   - 生成完整代码
   - 运行测试验证
   - 创建PR
```

### 5. 背景代理功能
```bash
# 使用背景代理
1. 在设置中启用Background Agents
2. 使用截图或描述指派任务
3. 代理在云端并行处理
4. 查看处理进度和结果
5. 审查并合并更改
```

## 使用场景和案例

### 场景1: 全栈应用开发
```javascript
// 需求：创建一个完整的Todo应用
// 使用Composer模式，一次性生成前后端代码

// 前端 React 组件
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

### 场景2: 代码重构优化
```typescript
// 原始代码（需要重构）
class UserService {
  private users: any[] = [];
  
  public addUser(user: any) {
    this.users.push(user);
  }
  
  public getUser(id: number) {
    return this.users.find(u => u.id === id);
  }
}

// 使用Cursor重构后的代码
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

### 场景3: 自动化测试生成
```javascript
// 原始函数
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

// Cursor生成的测试用例
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

### 场景4: 文档自动生成
```python
# 原始代码
def process_order(order_data, customer_id):
    # 处理订单逻辑
    pass

# Cursor生成的文档化代码
def process_order(order_data: dict, customer_id: int) -> dict:
    """
    处理客户订单
    
    Args:
        order_data (dict): 订单数据，包含以下字段：
            - items (list): 订单项目列表
            - shipping_address (str): 配送地址
            - payment_method (str): 支付方式
        customer_id (int): 客户ID
    
    Returns:
        dict: 处理结果，包含以下字段：
            - order_id (str): 订单ID
            - status (str): 订单状态
            - total_amount (float): 订单总金额
            - estimated_delivery (str): 预计配送时间
    
    Raises:
        ValueError: 当订单数据无效时
        CustomerNotFoundError: 当客户不存在时
    
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
    # 验证客户存在
    if not customer_exists(customer_id):
        raise CustomerNotFoundError(f"Customer {customer_id} not found")
    
    # 验证订单数据
    if not order_data or 'items' not in order_data:
        raise ValueError("Invalid order data")
    
    # 处理订单逻辑
    order_id = generate_order_id()
    total_amount = calculate_total(order_data['items'])
    
    # 创建订单记录
    order = {
        'order_id': order_id,
        'customer_id': customer_id,
        'items': order_data['items'],
        'total_amount': total_amount,
        'status': 'pending',
        'created_at': datetime.now().isoformat()
    }
    
    # 保存到数据库
    save_order(order)
    
    return {
        'order_id': order_id,
        'status': 'pending',
        'total_amount': total_amount,
        'estimated_delivery': calculate_delivery_date()
    }
```

## 最佳实践

### 1. 项目设置优化
```bash
# 创建高质量的.cursorrules文件
echo "Use TypeScript for all new files
Follow project's ESLint configuration
Write comprehensive JSDoc comments
Prefer functional programming patterns
Use React hooks instead of class components
Write unit tests for all business logic
Follow REST API conventions
Use semantic commit messages" > .cursorrules
```

### 2. 有效的提示工程
```markdown
# 好的提示示例
创建一个用户认证系统，包含：
- JWT token认证
- 密码哈希存储
- 登录尝试限制
- 密码重置功能
- 角色权限管理
- 使用TypeScript和Express
- 包含完整的错误处理
- 编写单元测试
```

### 3. 团队协作配置
```json
// 团队共享配置
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

### 4. 成本优化策略
```bash
# 成本控制最佳实践
1. 使用免费层进行学习和实验
2. 为复杂任务保留Pro计划
3. 合理使用Max Mode
4. 定期监控使用情况
5. 培训团队高效使用AI
```

## 常见问题

### Q1: Cursor与VS Code的区别是什么？
**A**: Cursor是基于VS Code的AI原生IDE，具有深度集成的AI功能，包括完整的代码库理解、智能Agent模式和实时AI协作。而VS Code需要通过扩展添加AI功能。

### Q2: 背景代理功能是否安全？
**A**: 是的，背景代理在云端运行，但代码处理遵循严格的隐私政策。企业用户可以启用隐私模式，确保敏感代码不会被存储或共享。

### Q3: 如何处理AI生成代码的质量问题？
**A**: 
- 使用详细的.cursorrules文件
- 定期code review
- 建立测试驱动开发流程
- 使用静态分析工具
- 培训团队AI协作技能

### Q4: Cursor支持哪些编程语言？
**A**: Cursor支持所有主流编程语言，包括JavaScript/TypeScript、Python、Java、C++、Rust、Go等。AI对不同语言的理解程度可能有差异。

### Q5: 如何在团队中部署Cursor？
**A**: 
- 选择Business计划
- 配置团队共享规则
- 建立使用规范
- 监控使用情况和成本
- 提供团队培训

## 参考资料

### 官方资源
- [Cursor官方网站](https://cursor.sh/)
- [Cursor文档](https://docs.cursor.sh/)
- [Cursor社区论坛](https://forum.cursor.com/)

### 技术深度解析
- [Cursor工作原理详解](https://adityarohilla.com/2025/05/08/how-cursor-works-internally/)
- [AI编程工具对比](https://www.enginelabs.ai/blog/cursor-ai-an-in-depth-review-may-2025-update)
- [背景代理使用指南](https://decoupledlogic.com/2025/05/29/background-agents-in-cursor-cloud-powered-coding-at-scale/)

### 最新更新
- [Cursor 1.0更新日志](https://forum.cursor.com/t/cursor-1-0-update-changelog/51000)
- [背景代理功能发布](https://cursor.sh/blog/background-agents)
- [MCP集成指南](https://cursor.sh/blog/mcp-integration)

### 社区资源
- [Cursor使用技巧分享](https://forum.cursor.com/c/tips-and-tricks)
- [项目模板库](https://github.com/cursor-templates)
- [用户成功案例](https://cursor.sh/stories)

### 学习教程
- [Cursor初学者指南](https://www.youtube.com/watch?v=rKDJs2TdMRA)
- [高级功能教程](https://www.youtube.com/watch?v=5REHY4vxKSM)
- [团队协作实践](https://cursor.sh/blog/team-collaboration)

---

**更新日期**: 2025年7月
**版本**: v2.0
**作者**: Vibe Coding Guide团队

**其他语言版本**: [English](cursor-tutorial-en.md) 