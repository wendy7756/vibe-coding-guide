# Claude Code 使用教程 (2025年最新版)

<div align="center">中文 | [English](claude-code-tutorial-en.md)</div>

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

Claude Code是由Anthropic开发的AI编程助手，基于Claude系列大型语言模型。2025年版本带来了革命性的Computer Use API、混合推理能力和扩展思维功能，成为AI编程领域的新标杆。

### 核心特性
- **混合推理模型**: 支持快速推理和深度思考两种模式
- **Computer Use API**: 可以直接操作计算机界面
- **多模态支持**: 处理文本、图像、代码和文档
- **扩展思维**: 支持复杂问题的步骤化解决
- **API集成**: 灵活的API接口，支持多种编程语言

## 2025年最新功能

### 🚀 Claude 3.7 Sonnet 发布
- **发布时间**: 2025年2月24日
- **混合推理**: 双模式操作，标准和扩展思维模式
- **200K Token输出**: 大幅提升输出容量
- **编程性能**: 在编程任务上达到SOTA水平
- **动作扩展**: 支持迭代函数调用和环境交互

### 🤖 Claude 4 Sonnet 和 Opus 4
- **Claude 4 Sonnet**: 平衡性能和速度的最新版本
- **Claude Opus 4**: 最强大的模型，专为复杂问题求解设计
- **视觉能力**: 改进的图像理解和分析能力
- **工具使用**: 增强的函数调用和API集成

### 🖥️ Computer Use API
- **屏幕控制**: 直接操作GUI界面
- **自动化任务**: 执行复杂的计算机操作
- **跨平台支持**: 支持Windows、macOS和Linux
- **安全限制**: 严格的权限控制和安全措施

### 🧠 扩展思维能力
- **深度推理**: 支持复杂问题的多步骤分析
- **思维链**: 清晰展示推理过程
- **自我修正**: 能够检查和修正自己的推理
- **创新思维**: 支持创造性问题解决

## 定价方案

### API定价（按Token计费）

| 模型 | 输入价格 (每1M tokens) | 输出价格 (每1M tokens) | 适用场景 |
|------|----------------------|----------------------|----------|
| **Claude 3 Haiku** | $0.25 | $1.25 | 简单任务和快速响应 |
| **Claude 3 Sonnet** | $3.00 | $15.00 | 平衡性能和成本 |
| **Claude 3.5 Sonnet** | $3.00 | $15.00 | 增强版平衡模型 |
| **Claude 3.7 Sonnet** | $3.00 | $15.00 | 最新混合推理模型 |
| **Claude 4 Sonnet** | $3.00 | $15.00 | 最新平衡模型 |
| **Claude 3 Opus** | $15.00 | $75.00 | 复杂任务和高质量需求 |
| **Claude Opus 4** | $15.00 | $75.00 | 最强大的模型 |

### 订阅计划

| 计划 | 价格 | 特性 | 适用场景 |
|------|------|------|----------|
| **免费层** | $0 | 有限请求，基础功能 | 试用和学习 |
| **Pro计划** | $20/月 | 更多请求，优先队列 | 个人开发者 |
| **Team计划** | $25/用户/月 | 团队协作，更高限制 | 小团队 |
| **Enterprise** | 定制 | 无限制，专属支持 | 企业客户 |

## 安装和设置

### 1. 获取API密钥
```bash
# 访问Anthropic官网
https://console.anthropic.com/

# 步骤
1. 注册Anthropic账户
2. 验证邮箱和手机号
3. 进入API控制台
4. 创建新的API密钥
5. 保存密钥到安全位置
```

### 2. 环境设置
```bash
# 安装Python SDK
pip install anthropic

# 设置环境变量
export ANTHROPIC_API_KEY="your_api_key_here"

# 或者创建 .env 文件
echo "ANTHROPIC_API_KEY=your_api_key_here" > .env
```

### 3. 基本配置
```python
# Python 配置示例
import anthropic
import os

# 初始化客户端
client = anthropic.Anthropic(
    api_key=os.getenv("ANTHROPIC_API_KEY")
)

# 基本配置
default_config = {
    "model": "claude-3.7-sonnet",
    "max_tokens": 4096,
    "temperature": 0.3,
    "system": "You are a helpful AI programming assistant."
}
```

### 4. 多语言SDK
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

## 核心功能详解

### 1. 代码生成和补全
```python
# 示例：生成完整的API服务
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

### 2. 混合推理模式
```python
# 启用扩展思维模式
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
# 计算机使用示例
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

# 使用示例
result = use_computer_api("Open a text editor and create a simple HTML page")
```

### 4. 多模态处理
```python
# 图像和代码分析
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

# 使用示例
analysis = analyze_code_screenshot("code_screenshot.png")
```

### 5. 函数调用和工具使用
```python
# 定义工具函数
def get_weather(location):
    # 模拟天气API调用
    return f"Weather in {location}: 22°C, sunny"

# 配置工具
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

# 使用工具
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

## 使用场景和案例

### 场景1: 复杂算法实现
```python
# 需求：实现一个高效的图算法
prompt = """
实现一个用于社交网络分析的图算法，包含：
1. 图的表示和存储
2. 最短路径算法
3. 社区检测算法
4. 影响力分析
5. 并行处理支持
6. 完整的测试用例
"""

response = client.messages.create(
    model="claude-3.7-sonnet",
    max_tokens=4000,
    system="You are an expert in graph algorithms and parallel computing.",
    messages=[{"role": "user", "content": prompt}]
)

# Claude生成的完整图算法实现
import networkx as nx
from collections import defaultdict, deque
import numpy as np
from concurrent.futures import ThreadPoolExecutor
import heapq

class SocialNetworkAnalyzer:
    def __init__(self):
        self.graph = nx.Graph()
        self.adjacency_list = defaultdict(list)
        self.node_attributes = {}
    
    def add_node(self, node_id, attributes=None):
        """添加节点到图中"""
        self.graph.add_node(node_id)
        self.node_attributes[node_id] = attributes or {}
    
    def add_edge(self, node1, node2, weight=1):
        """添加边到图中"""
        self.graph.add_edge(node1, node2, weight=weight)
        self.adjacency_list[node1].append((node2, weight))
        self.adjacency_list[node2].append((node1, weight))
    
    def dijkstra_shortest_path(self, start, end):
        """使用Dijkstra算法计算最短路径"""
        distances = {node: float('inf') for node in self.graph.nodes()}
        distances[start] = 0
        priority_queue = [(0, start)]
        previous = {}
        
        while priority_queue:
            current_distance, current_node = heapq.heappop(priority_queue)
            
            if current_node == end:
                break
                
            if current_distance > distances[current_node]:
                continue
                
            for neighbor, weight in self.adjacency_list[current_node]:
                distance = current_distance + weight
                
                if distance < distances[neighbor]:
                    distances[neighbor] = distance
                    previous[neighbor] = current_node
                    heapq.heappush(priority_queue, (distance, neighbor))
        
        # 重构路径
        path = []
        current = end
        while current in previous:
            path.append(current)
            current = previous[current]
        path.append(start)
        path.reverse()
        
        return path, distances[end]
    
    def detect_communities(self, resolution=1.0):
        """使用Louvain算法检测社区"""
        import community as community_louvain
        
        partition = community_louvain.best_partition(self.graph, resolution=resolution)
        communities = defaultdict(list)
        
        for node, community_id in partition.items():
            communities[community_id].append(node)
        
        return dict(communities)
    
    def calculate_influence(self, node_id):
        """计算节点影响力（结合度中心性、介数中心性和PageRank）"""
        degree_centrality = nx.degree_centrality(self.graph)[node_id]
        betweenness_centrality = nx.betweenness_centrality(self.graph)[node_id]
        pagerank = nx.pagerank(self.graph)[node_id]
        
        # 综合影响力得分
        influence_score = (
            0.4 * degree_centrality +
            0.3 * betweenness_centrality +
            0.3 * pagerank
        )
        
        return influence_score
    
    def parallel_influence_analysis(self, top_k=10):
        """并行计算所有节点的影响力"""
        nodes = list(self.graph.nodes())
        
        with ThreadPoolExecutor(max_workers=4) as executor:
            influence_scores = list(executor.map(self.calculate_influence, nodes))
        
        # 排序并返回top_k
        node_influence = list(zip(nodes, influence_scores))
        node_influence.sort(key=lambda x: x[1], reverse=True)
        
        return node_influence[:top_k]

# 测试用例
def test_social_network_analyzer():
    analyzer = SocialNetworkAnalyzer()
    
    # 添加节点和边
    for i in range(10):
        analyzer.add_node(i, {"name": f"User{i}"})
    
    edges = [(0, 1), (0, 2), (1, 3), (2, 3), (3, 4), (4, 5), (5, 6), (6, 7), (7, 8), (8, 9)]
    for edge in edges:
        analyzer.add_edge(edge[0], edge[1])
    
    # 测试最短路径
    path, distance = analyzer.dijkstra_shortest_path(0, 9)
    print(f"最短路径从0到9: {path}, 距离: {distance}")
    
    # 测试社区检测
    communities = analyzer.detect_communities()
    print(f"检测到的社区: {communities}")
    
    # 测试影响力分析
    top_influencers = analyzer.parallel_influence_analysis(5)
    print(f"Top 5 影响力用户: {top_influencers}")

if __name__ == "__main__":
    test_social_network_analyzer()
```

### 场景2: 自动化运维脚本
```python
# 需求：创建一个自动化部署和监控系统
prompt = """
创建一个Python脚本，实现：
1. 自动化应用部署
2. 系统监控和告警
3. 日志分析
4. 自动故障恢复
5. 性能指标收集
6. 邮件通知系统
"""

response = client.messages.create(
    model="claude-3.7-sonnet",
    max_tokens=3000,
    system="You are a DevOps expert specializing in automation and monitoring.",
    messages=[{"role": "user", "content": prompt}]
)

# Claude生成的自动化运维脚本
import subprocess
import psutil
import smtplib
import time
import logging
import json
from datetime import datetime
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
import requests
import os

class AutomationSystem:
    def __init__(self, config_file="automation_config.json"):
        self.config = self.load_config(config_file)
        self.setup_logging()
        self.alert_cooldown = {}
    
    def load_config(self, config_file):
        """加载配置文件"""
        default_config = {
            "email": {
                "smtp_server": "smtp.gmail.com",
                "smtp_port": 587,
                "username": "your_email@gmail.com",
                "password": "your_password",
                "recipients": ["admin@company.com"]
            },
            "monitoring": {
                "cpu_threshold": 80,
                "memory_threshold": 85,
                "disk_threshold": 90,
                "check_interval": 60
            },
            "services": [
                {"name": "nginx", "port": 80},
                {"name": "application", "port": 8000}
            ]
        }
        
        if os.path.exists(config_file):
            with open(config_file, 'r') as f:
                return json.load(f)
        return default_config
    
    def setup_logging(self):
        """设置日志"""
        logging.basicConfig(
            level=logging.INFO,
            format='%(asctime)s - %(levelname)s - %(message)s',
            handlers=[
                logging.FileHandler('automation.log'),
                logging.StreamHandler()
            ]
        )
        self.logger = logging.getLogger(__name__)
    
    def send_email_alert(self, subject, message):
        """发送邮件告警"""
        try:
            msg = MIMEMultipart()
            msg['From'] = self.config['email']['username']
            msg['To'] = ', '.join(self.config['email']['recipients'])
            msg['Subject'] = subject
            
            msg.attach(MIMEText(message, 'plain'))
            
            server = smtplib.SMTP(self.config['email']['smtp_server'], self.config['email']['smtp_port'])
            server.starttls()
            server.login(self.config['email']['username'], self.config['email']['password'])
            server.send_message(msg)
            server.quit()
            
            self.logger.info(f"邮件告警已发送: {subject}")
        except Exception as e:
            self.logger.error(f"发送邮件失败: {e}")
    
    def check_system_resources(self):
        """检查系统资源"""
        cpu_usage = psutil.cpu_percent(interval=1)
        memory = psutil.virtual_memory()
        disk = psutil.disk_usage('/')
        
        alerts = []
        
        if cpu_usage > self.config['monitoring']['cpu_threshold']:
            alerts.append(f"CPU使用率过高: {cpu_usage}%")
        
        if memory.percent > self.config['monitoring']['memory_threshold']:
            alerts.append(f"内存使用率过高: {memory.percent}%")
        
        if disk.percent > self.config['monitoring']['disk_threshold']:
            alerts.append(f"磁盘使用率过高: {disk.percent}%")
        
        if alerts:
            alert_message = "\n".join(alerts)
            self.send_alert_with_cooldown("系统资源告警", alert_message)
            
            # 尝试自动恢复
            self.auto_recovery()
        
        return {
            "cpu": cpu_usage,
            "memory": memory.percent,
            "disk": disk.percent,
            "timestamp": datetime.now().isoformat()
        }
    
    def check_service_health(self):
        """检查服务健康状态"""
        service_status = {}
        
        for service in self.config['services']:
            try:
                response = requests.get(f"http://localhost:{service['port']}", timeout=10)
                service_status[service['name']] = response.status_code == 200
            except Exception as e:
                service_status[service['name']] = False
                self.logger.warning(f"服务 {service['name']} 检查失败: {e}")
                
                # 尝试重启服务
                self.restart_service(service['name'])
        
        return service_status
    
    def restart_service(self, service_name):
        """重启服务"""
        try:
            subprocess.run(['systemctl', 'restart', service_name], check=True)
            self.logger.info(f"服务 {service_name} 已重启")
            
            # 等待服务启动
            time.sleep(5)
            
            # 验证服务是否正常
            if self.verify_service_restart(service_name):
                self.send_email_alert(
                    f"服务恢复成功",
                    f"服务 {service_name} 已成功重启并恢复正常"
                )
            else:
                self.send_email_alert(
                    f"服务恢复失败",
                    f"服务 {service_name} 重启后仍然无法正常工作"
                )
        except subprocess.CalledProcessError as e:
            self.logger.error(f"重启服务 {service_name} 失败: {e}")
            self.send_email_alert(
                f"服务重启失败",
                f"无法重启服务 {service_name}: {e}"
            )
    
    def verify_service_restart(self, service_name):
        """验证服务重启是否成功"""
        # 查找对应的端口配置
        for service in self.config['services']:
            if service['name'] == service_name:
                try:
                    response = requests.get(f"http://localhost:{service['port']}", timeout=10)
                    return response.status_code == 200
                except:
                    return False
        return False
    
    def auto_recovery(self):
        """自动恢复操作"""
        self.logger.info("执行自动恢复操作...")
        
        # 清理临时文件
        subprocess.run(['find', '/tmp', '-type', 'f', '-atime', '+7', '-delete'], 
                      capture_output=True)
        
        # 重启高内存使用的进程（示例）
        try:
            result = subprocess.run(['ps', 'aux', '--sort', '-rss'], 
                                  capture_output=True, text=True)
            # 这里可以添加更复杂的进程管理逻辑
        except Exception as e:
            self.logger.error(f"自动恢复失败: {e}")
    
    def send_alert_with_cooldown(self, subject, message, cooldown_minutes=30):
        """带冷却时间的告警发送"""
        now = datetime.now()
        alert_key = f"{subject}_{message}"
        
        if alert_key in self.alert_cooldown:
            time_diff = (now - self.alert_cooldown[alert_key]).total_seconds() / 60
            if time_diff < cooldown_minutes:
                return
        
        self.alert_cooldown[alert_key] = now
        self.send_email_alert(subject, message)
    
    def collect_metrics(self):
        """收集性能指标"""
        metrics = {
            "timestamp": datetime.now().isoformat(),
            "system": self.check_system_resources(),
            "services": self.check_service_health(),
            "processes": len(psutil.pids()),
            "network": {
                "connections": len(psutil.net_connections()),
                "io_counters": psutil.net_io_counters()._asdict()
            }
        }
        
        # 保存到文件
        with open(f"metrics_{datetime.now().strftime('%Y%m%d')}.json", 'a') as f:
            f.write(json.dumps(metrics) + '\n')
        
        return metrics
    
    def deploy_application(self, app_path, service_name):
        """部署应用"""
        try:
            self.logger.info(f"开始部署应用: {service_name}")
            
            # 停止服务
            subprocess.run(['systemctl', 'stop', service_name], check=True)
            
            # 备份当前版本
            backup_path = f"/backup/{service_name}_{datetime.now().strftime('%Y%m%d_%H%M%S')}"
            subprocess.run(['cp', '-r', app_path, backup_path], check=True)
            
            # 部署新版本（这里假设新版本在/tmp/new_version目录）
            subprocess.run(['cp', '-r', '/tmp/new_version/*', app_path], check=True)
            
            # 启动服务
            subprocess.run(['systemctl', 'start', service_name], check=True)
            
            # 验证部署
            time.sleep(10)
            if self.verify_service_restart(service_name):
                self.send_email_alert(
                    "部署成功",
                    f"应用 {service_name} 已成功部署并运行正常"
                )
                self.logger.info(f"应用 {service_name} 部署成功")
            else:
                # 回滚
                self.rollback_deployment(backup_path, app_path, service_name)
                
        except Exception as e:
            self.logger.error(f"部署失败: {e}")
            self.send_email_alert("部署失败", f"应用 {service_name} 部署失败: {e}")
    
    def rollback_deployment(self, backup_path, app_path, service_name):
        """回滚部署"""
        try:
            self.logger.info(f"开始回滚应用: {service_name}")
            
            subprocess.run(['systemctl', 'stop', service_name], check=True)
            subprocess.run(['rm', '-rf', app_path], check=True)
            subprocess.run(['cp', '-r', backup_path, app_path], check=True)
            subprocess.run(['systemctl', 'start', service_name], check=True)
            
            self.send_email_alert(
                "应用回滚完成",
                f"应用 {service_name} 已回滚到之前版本"
            )
            
        except Exception as e:
            self.logger.error(f"回滚失败: {e}")
            self.send_email_alert("回滚失败", f"应用 {service_name} 回滚失败: {e}")
    
    def run_monitoring_loop(self):
        """运行监控循环"""
        self.logger.info("开始监控系统...")
        
        while True:
            try:
                metrics = self.collect_metrics()
                self.logger.info(f"指标收集完成: CPU={metrics['system']['cpu']}%, "
                               f"内存={metrics['system']['memory']}%")
                
                time.sleep(self.config['monitoring']['check_interval'])
                
            except KeyboardInterrupt:
                self.logger.info("监控系统已停止")
                break
            except Exception as e:
                self.logger.error(f"监控循环错误: {e}")
                time.sleep(10)

# 使用示例
if __name__ == "__main__":
    automation = AutomationSystem()
    
    # 可以单独运行各个功能
    # automation.deploy_application("/var/www/myapp", "myapp")
    # automation.collect_metrics()
    
    # 或者运行持续监控
    automation.run_monitoring_loop()
```

### 场景3: 数据分析和可视化
```python
# 需求：创建一个全面的数据分析工具
prompt = """
创建一个Python数据分析工具，包含：
1. 数据清洗和预处理
2. 统计分析和假设检验
3. 机器学习模型训练
4. 交互式数据可视化
5. 报告生成
6. 实时数据处理
"""

response = client.messages.create(
    model="claude-3.7-sonnet",
    max_tokens=4000,
    system="You are a data science expert with extensive experience in Python analytics.",
    messages=[{"role": "user", "content": prompt}]
)

# Claude生成的数据分析工具
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.graph_objects as go
import plotly.express as px
from plotly.subplots import make_subplots
import streamlit as st
from scipy import stats
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor
from sklearn.metrics import accuracy_score, classification_report, mean_squared_error
import joblib
from datetime import datetime, timedelta
import warnings
warnings.filterwarnings('ignore')

class DataAnalyzer:
    def __init__(self):
        self.data = None
        self.processed_data = None
        self.models = {}
        self.scalers = {}
        self.encoders = {}
        
    def load_data(self, file_path, file_type='csv'):
        """加载数据"""
        try:
            if file_type == 'csv':
                self.data = pd.read_csv(file_path)
            elif file_type == 'excel':
                self.data = pd.read_excel(file_path)
            elif file_type == 'json':
                self.data = pd.read_json(file_path)
            
            print(f"数据加载成功: {self.data.shape}")
            return self.data
        except Exception as e:
            print(f"数据加载失败: {e}")
            return None
    
    def data_profiling(self):
        """数据概览和分析"""
        if self.data is None:
            return "请先加载数据"
        
        profile = {
            'shape': self.data.shape,
            'columns': list(self.data.columns),
            'dtypes': self.data.dtypes.to_dict(),
            'missing_values': self.data.isnull().sum().to_dict(),
            'duplicate_rows': self.data.duplicated().sum(),
            'memory_usage': self.data.memory_usage(deep=True).sum() / 1024**2,  # MB
            'numeric_summary': self.data.describe(),
            'categorical_summary': self.data.select_dtypes(include=['object']).describe()
        }
        
        return profile
    
    def clean_data(self, drop_duplicates=True, handle_missing='drop', outlier_method='iqr'):
        """数据清洗"""
        if self.data is None:
            return "请先加载数据"
        
        self.processed_data = self.data.copy()
        
        # 删除重复行
        if drop_duplicates:
            self.processed_data.drop_duplicates(inplace=True)
        
        # 处理缺失值
        if handle_missing == 'drop':
            self.processed_data.dropna(inplace=True)
        elif handle_missing == 'fill_mean':
            numeric_cols = self.processed_data.select_dtypes(include=[np.number]).columns
            self.processed_data[numeric_cols] = self.processed_data[numeric_cols].fillna(
                self.processed_data[numeric_cols].mean()
            )
        elif handle_missing == 'fill_median':
            numeric_cols = self.processed_data.select_dtypes(include=[np.number]).columns
            self.processed_data[numeric_cols] = self.processed_data[numeric_cols].fillna(
                self.processed_data[numeric_cols].median()
            )
        
        # 处理异常值
        if outlier_method == 'iqr':
            numeric_cols = self.processed_data.select_dtypes(include=[np.number]).columns
            for col in numeric_cols:
                Q1 = self.processed_data[col].quantile(0.25)
                Q3 = self.processed_data[col].quantile(0.75)
                IQR = Q3 - Q1
                lower_bound = Q1 - 1.5 * IQR
                upper_bound = Q3 + 1.5 * IQR
                self.processed_data = self.processed_data[
                    (self.processed_data[col] >= lower_bound) & 
                    (self.processed_data[col] <= upper_bound)
                ]
        
        print(f"数据清洗完成: {self.processed_data.shape}")
        return self.processed_data
    
    def statistical_analysis(self, column1, column2=None, test_type='correlation'):
        """统计分析"""
        if self.processed_data is None:
            return "请先进行数据清洗"
        
        results = {}
        
        if test_type == 'correlation' and column2:
            # 相关性分析
            correlation = self.processed_data[column1].corr(self.processed_data[column2])
            results['correlation'] = correlation
            results['p_value'] = stats.pearsonr(
                self.processed_data[column1], 
                self.processed_data[column2]
            )[1]
        
        elif test_type == 'normality':
            # 正态性检验
            statistic, p_value = stats.shapiro(self.processed_data[column1])
            results['shapiro_statistic'] = statistic
            results['shapiro_p_value'] = p_value
            results['is_normal'] = p_value > 0.05
        
        elif test_type == 't_test' and column2:
            # t检验
            group1 = self.processed_data[self.processed_data[column2] == 
                                       self.processed_data[column2].unique()[0]][column1]
            group2 = self.processed_data[self.processed_data[column2] == 
                                       self.processed_data[column2].unique()[1]][column1]
            statistic, p_value = stats.ttest_ind(group1, group2)
            results['t_statistic'] = statistic
            results['p_value'] = p_value
            results['significant'] = p_value < 0.05
        
        return results
    
    def create_visualizations(self, chart_type='distribution', columns=None):
        """创建可视化图表"""
        if self.processed_data is None:
            return "请先进行数据清洗"
        
        fig = make_subplots(rows=2, cols=2, 
                           subplot_titles=('分布图', '相关性热力图', '箱线图', '散点图'))
        
        if chart_type == 'distribution' and columns:
            # 分布图
            fig.add_trace(
                go.Histogram(x=self.processed_data[columns[0]], name=columns[0]),
                row=1, col=1
            )
        
        if len(columns) >= 2:
            # 散点图
            fig.add_trace(
                go.Scatter(x=self.processed_data[columns[0]], 
                          y=self.processed_data[columns[1]], 
                          mode='markers',
                          name=f'{columns[0]} vs {columns[1]}'),
                row=2, col=2
            )
        
        # 相关性热力图
        numeric_cols = self.processed_data.select_dtypes(include=[np.number]).columns
        if len(numeric_cols) > 1:
            corr_matrix = self.processed_data[numeric_cols].corr()
            fig.add_trace(
                go.Heatmap(z=corr_matrix.values,
                          x=corr_matrix.columns,
                          y=corr_matrix.columns,
                          colorscale='RdBu',
                          name='相关性'),
                row=1, col=2
            )
        
        fig.update_layout(height=800, title_text="数据分析可视化")
        return fig
    
    def train_model(self, target_column, model_type='classification', test_size=0.2):
        """训练机器学习模型"""
        if self.processed_data is None:
            return "请先进行数据清洗"
        
        # 准备数据
        X = self.processed_data.drop(columns=[target_column])
        y = self.processed_data[target_column]
        
        # 处理分类变量
        categorical_cols = X.select_dtypes(include=['object']).columns
        for col in categorical_cols:
            if col not in self.encoders:
                self.encoders[col] = LabelEncoder()
                X[col] = self.encoders[col].fit_transform(X[col])
            else:
                X[col] = self.encoders[col].transform(X[col])
        
        # 标准化数值特征
        numeric_cols = X.select_dtypes(include=[np.number]).columns
        if len(numeric_cols) > 0:
            if 'scaler' not in self.scalers:
                self.scalers['scaler'] = StandardScaler()
                X[numeric_cols] = self.scalers['scaler'].fit_transform(X[numeric_cols])
            else:
                X[numeric_cols] = self.scalers['scaler'].transform(X[numeric_cols])
        
        # 分割数据
        X_train, X_test, y_train, y_test = train_test_split(
            X, y, test_size=test_size, random_state=42
        )
        
        # 训练模型
        if model_type == 'classification':
            model = RandomForestClassifier(n_estimators=100, random_state=42)
            model.fit(X_train, y_train)
            
            # 预测和评估
            y_pred = model.predict(X_test)
            accuracy = accuracy_score(y_test, y_pred)
            report = classification_report(y_test, y_pred, output_dict=True)
            
            results = {
                'model': model,
                'accuracy': accuracy,
                'classification_report': report,
                'feature_importance': dict(zip(X.columns, model.feature_importances_))
            }
            
        else:  # regression
            model = RandomForestRegressor(n_estimators=100, random_state=42)
            model.fit(X_train, y_train)
            
            # 预测和评估
            y_pred = model.predict(X_test)
            mse = mean_squared_error(y_test, y_pred)
            rmse = np.sqrt(mse)
            
            results = {
                'model': model,
                'mse': mse,
                'rmse': rmse,
                'r2_score': model.score(X_test, y_test),
                'feature_importance': dict(zip(X.columns, model.feature_importances_))
            }
        
        self.models[target_column] = model
        return results
    
    def generate_report(self, output_path='analysis_report.html'):
        """生成分析报告"""
        if self.processed_data is None:
            return "请先进行数据清洗"
        
        report_html = f"""
        <!DOCTYPE html>
        <html>
        <head>
            <title>数据分析报告</title>
            <style>
                body {{ font-family: Arial, sans-serif; margin: 40px; }}
                .section {{ margin: 20px 0; }}
                .metric {{ display: inline-block; margin: 10px; padding: 10px; 
                          border: 1px solid #ddd; border-radius: 5px; }}
                table {{ border-collapse: collapse; width: 100%; }}
                th, td {{ border: 1px solid #ddd; padding: 8px; text-align: left; }}
                th {{ background-color: #f2f2f2; }}
            </style>
        </head>
        <body>
            <h1>数据分析报告</h1>
            <p>生成时间: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}</p>
            
            <div class="section">
                <h2>数据概览</h2>
                <div class="metric">
                    <strong>数据形状:</strong> {self.processed_data.shape}
                </div>
                <div class="metric">
                    <strong>列数:</strong> {len(self.processed_data.columns)}
                </div>
                <div class="metric">
                    <strong>行数:</strong> {len(self.processed_data)}
                </div>
            </div>
            
            <div class="section">
                <h2>数据质量</h2>
                <div class="metric">
                    <strong>缺失值:</strong> {self.processed_data.isnull().sum().sum()}
                </div>
                <div class="metric">
                    <strong>重复行:</strong> {self.processed_data.duplicated().sum()}
                </div>
            </div>
            
            <div class="section">
                <h2>数值特征统计</h2>
                {self.processed_data.describe().to_html()}
            </div>
            
            <div class="section">
                <h2>分类特征统计</h2>
                {self.processed_data.select_dtypes(include=['object']).describe().to_html()}
            </div>
        </body>
        </html>
        """
        
        with open(output_path, 'w', encoding='utf-8') as f:
            f.write(report_html)
        
        print(f"分析报告已生成: {output_path}")
        return output_path
    
    def real_time_processing(self, data_stream):
        """实时数据处理"""
        processed_stream = []
        
        for data_point in data_stream:
            # 应用相同的清洗和预处理步骤
            processed_point = self.apply_preprocessing(data_point)
            
            # 如果有训练好的模型，进行预测
            if self.models:
                for target, model in self.models.items():
                    prediction = model.predict([processed_point])[0]
                    processed_point[f'{target}_prediction'] = prediction
            
            processed_stream.append(processed_point)
        
        return processed_stream
    
    def apply_preprocessing(self, data_point):
        """应用预处理步骤到单个数据点"""
        # 这里应该应用与训练时相同的预处理步骤
        # 包括编码、标准化等
        return data_point
    
    def save_model(self, target_column, file_path):
        """保存训练好的模型"""
        if target_column in self.models:
            model_data = {
                'model': self.models[target_column],
                'scaler': self.scalers.get('scaler'),
                'encoders': self.encoders
            }
            joblib.dump(model_data, file_path)
            print(f"模型已保存: {file_path}")
        else:
            print(f"未找到模型: {target_column}")
    
    def load_model(self, file_path, target_column):
        """加载训练好的模型"""
        try:
            model_data = joblib.load(file_path)
            self.models[target_column] = model_data['model']
            if model_data['scaler']:
                self.scalers['scaler'] = model_data['scaler']
            if model_data['encoders']:
                self.encoders = model_data['encoders']
            print(f"模型加载成功: {file_path}")
        except Exception as e:
            print(f"模型加载失败: {e}")

# Streamlit 应用界面
def create_streamlit_app():
    st.title("数据分析工具")
    
    analyzer = DataAnalyzer()
    
    # 文件上传
    uploaded_file = st.file_uploader("上传数据文件", type=['csv', 'excel', 'json'])
    
    if uploaded_file is not None:
        # 加载数据
        file_type = uploaded_file.name.split('.')[-1]
        analyzer.load_data(uploaded_file, file_type)
        
        # 显示数据概览
        st.subheader("数据概览")
        st.write(analyzer.data_profiling())
        
        # 数据清洗
        st.subheader("数据清洗")
        handle_missing = st.selectbox("缺失值处理", ['drop', 'fill_mean', 'fill_median'])
        outlier_method = st.selectbox("异常值处理", ['iqr', 'none'])
        
        if st.button("执行清洗"):
            analyzer.clean_data(handle_missing=handle_missing, outlier_method=outlier_method)
            st.success("数据清洗完成")
        
        # 可视化
        if analyzer.processed_data is not None:
            st.subheader("数据可视化")
            columns = st.multiselect("选择列", analyzer.processed_data.columns)
            
            if len(columns) > 0:
                fig = analyzer.create_visualizations(columns=columns)
                st.plotly_chart(fig, use_container_width=True)
            
            # 模型训练
            st.subheader("模型训练")
            target_column = st.selectbox("目标列", analyzer.processed_data.columns)
            model_type = st.selectbox("模型类型", ['classification', 'regression'])
            
            if st.button("训练模型"):
                results = analyzer.train_model(target_column, model_type)
                st.write("模型训练结果:", results)
            
            # 生成报告
            if st.button("生成报告"):
                report_path = analyzer.generate_report()
                st.success(f"报告已生成: {report_path}")

# 使用示例
if __name__ == "__main__":
    # 创建分析器实例
    analyzer = DataAnalyzer()
    
    # 示例：加载和分析数据
    # analyzer.load_data('sample_data.csv')
    # profile = analyzer.data_profiling()
    # print(profile)
    
    # 运行Streamlit应用
    # streamlit run data_analyzer.py
    create_streamlit_app()
```

### 场景4: 自然语言处理API
```python
# 需求：创建一个文本分析API服务
prompt = """
创建一个FastAPI服务，提供以下NLP功能：
1. 文本情感分析
2. 实体识别
3. 文本摘要
4. 关键词提取
5. 文本分类
6. 语言检测
7. 文本相似度计算
"""

response = client.messages.create(
    model="claude-3.7-sonnet",
    max_tokens=3000,
    system="You are an NLP expert specializing in text analysis and API development.",
    messages=[{"role": "user", "content": prompt}]
)

# Claude生成的NLP API服务
# 这里展示生成的代码框架，完整实现会更长
```

## 最佳实践

### 1. 成本优化策略
```python
# 智能选择模型
def choose_model_by_task(task_complexity):
    if task_complexity == 'simple':
        return 'claude-3-haiku'
    elif task_complexity == 'medium':
        return 'claude-3.7-sonnet'
    else:
        return 'claude-opus-4'

# 缓存结果
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

### 2. 安全和隐私保护
```python
# 数据脱敏
import re

def sanitize_prompt(prompt):
    """移除敏感信息"""
    # 移除邮箱
    prompt = re.sub(r'\S+@\S+\.\S+', '[EMAIL]', prompt)
    # 移除电话号码
    prompt = re.sub(r'\b\d{3}-\d{3}-\d{4}\b', '[PHONE]', prompt)
    # 移除身份证号等
    prompt = re.sub(r'\b\d{15}|\d{18}\b', '[ID]', prompt)
    
    return prompt

# 请求限制
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
        
        # 清理过期请求
        self.requests[user_id] = [
            req_time for req_time in self.requests[user_id]
            if now - req_time < self.time_window
        ]
        
        if len(self.requests[user_id]) >= self.max_requests:
            return False
        
        self.requests[user_id].append(now)
        return True
```

### 3. 错误处理和重试机制
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

### 4. 性能监控和日志
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
        
        self.logger.info(f"请求完成 - 模型: {model}, 响应时间: {response_time:.2f}s, "
                        f"Token使用: {tokens_used}")
    
    def get_metrics(self):
        return self.metrics
```

## 常见问题

### Q1: 如何选择合适的Claude模型？
**A**: 根据任务复杂度选择：
- **简单任务**: Claude 3 Haiku（快速、低成本）
- **平衡需求**: Claude 3.7 Sonnet（性能与成本平衡）
- **复杂任务**: Claude Opus 4（最高性能）

### Q2: 如何控制API使用成本？
**A**: 
- 实现请求缓存机制
- 根据任务选择合适的模型
- 设置Token限制
- 使用批处理减少请求次数
- 监控和分析使用情况

### Q3: Computer Use API有哪些限制？
**A**: 
- 需要明确的权限授权
- 不能执行危险操作
- 有严格的安全检查
- 仅支持特定的应用场景

### Q4: 如何处理API限制和速率限制？
**A**: 
- 实现重试机制
- 使用指数退避算法
- 监控API使用情况
- 预留缓冲时间
- 考虑使用多个API密钥

### Q5: 如何确保数据安全和隐私？
**A**: 
- 数据脱敏处理
- 使用HTTPS传输
- 不在提示中包含敏感信息
- 定期轮换API密钥
- 遵循数据保护法规

## 参考资料

### 官方文档
- [Anthropic官方文档](https://docs.anthropic.com/)
- [Claude API参考](https://docs.anthropic.com/claude/reference/)
- [Computer Use API指南](https://docs.anthropic.com/claude/docs/computer-use)

### 定价和计费
- [API定价页面](https://www.anthropic.com/pricing)
- [Token计算器](https://platform.anthropic.com/token-calculator)
- [成本优化指南](https://apidog.com/blog/claude-api-cost/)

### 技术资源
- [Claude 3.7 Sonnet发布说明](https://aimlapi.com/models/claude-3-7-sonnet-api)
- [Claude Code使用教程](https://www.youtube.com/watch?v=P_pTypZZL4c)
- [Python SDK文档](https://github.com/anthropics/anthropic-sdk-python)

### 社区和支持
- [Anthropic社区论坛](https://community.anthropic.com/)
- [Discord服务器](https://discord.gg/anthropic)
- [GitHub Issues](https://github.com/anthropics/anthropic-sdk-python/issues)

### 最佳实践
- [提示工程指南](https://docs.anthropic.com/claude/docs/prompt-engineering)
- [安全最佳实践](https://docs.anthropic.com/claude/docs/safety-best-practices)
- [性能优化技巧](https://docs.anthropic.com/claude/docs/performance-optimization)

---

**更新日期**: 2025年7月
**版本**: v2.0
**作者**: Vibe Coding Guide团队

**其他语言版本**: [English](claude-code-tutorial-en.md) 