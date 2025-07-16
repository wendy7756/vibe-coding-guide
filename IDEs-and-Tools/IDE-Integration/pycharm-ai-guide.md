# PyCharm + AI 完整指南

[English](./pycharm-ai-guide-en.md) | 中文

## 目录
1. [概述](#概述)
2. [AI插件配置](#ai插件配置)
3. [Python开发与AI](#python开发与ai)
4. [数据科学与机器学习](#数据科学与机器学习)
5. [Web开发](#web开发)
6. [测试与调试](#测试与调试)
7. [最佳实践](#最佳实践)

## 概述

PyCharm作为专业的Python IDE，结合AI技术为Python开发者提供强大的智能编程体验。本指南涵盖Python开发、数据科学、机器学习、Web开发等领域的AI应用。

### 主要AI功能
- **智能Python代码补全**: 精准的Python语法和库建议
- **数据科学支持**: Jupyter、NumPy、Pandas等智能辅助
- **ML模型开发**: TensorFlow、PyTorch等框架支持
- **Web框架助手**: Django、Flask等框架的AI支持
- **自动化测试**: pytest、unittest测试用例生成

## AI插件配置

### 1. JetBrains AI Assistant

```python
# PyCharm AI Assistant配置
# Settings -> Plugins -> Marketplace -> "JetBrains AI Assistant"

# Python特定设置
{
    "ai_assistant": {
        "python_version": "3.11",
        "enable_type_hints": True,
        "enable_docstrings": True,
        "enable_data_science": True,
        "frameworks": ["django", "flask", "fastapi"]
    }
}
```

### 2. GitHub Copilot

```json
{
    "github.copilot.enable": {
        "python": true,
        "jupyter": true,
        "yaml": true,
        "requirements.txt": true
    }
}
```

## Python开发与AI

### 1. 智能代码生成

#### 类和函数自动生成
```python
# 输入注释，AI生成完整实现
class DataProcessor:
    """
    数据处理器，支持多种数据格式的读取和处理
    """
    
    def __init__(self, config: Dict[str, Any]):
        self.config = config
        self.data_cache = {}
        
    def load_csv(self, file_path: str, **kwargs) -> pd.DataFrame:
        """加载CSV文件并缓存"""
        try:
            df = pd.read_csv(file_path, **kwargs)
            self.data_cache[file_path] = df
            return df
        except Exception as e:
            logger.error(f"Failed to load CSV: {e}")
            raise
    
    def clean_data(self, df: pd.DataFrame) -> pd.DataFrame:
        """清理数据，处理缺失值和异常值"""
        # 删除重复行
        df = df.drop_duplicates()
        
        # 处理数值列的缺失值
        numeric_cols = df.select_dtypes(include=[np.number]).columns
        df[numeric_cols] = df[numeric_cols].fillna(df[numeric_cols].mean())
        
        # 处理分类列的缺失值
        categorical_cols = df.select_dtypes(include=['object']).columns
        df[categorical_cols] = df[categorical_cols].fillna('Unknown')
        
        return df
```

### 2. 异步编程

```python
import asyncio
import aiohttp
from typing import List, Dict

class AsyncAPIClient:
    """异步API客户端"""
    
    def __init__(self, base_url: str, max_concurrent: int = 10):
        self.base_url = base_url
        self.max_concurrent = max_concurrent
        
    async def fetch_data(self, endpoints: List[str]) -> List[Dict]:
        """并发获取多个端点的数据"""
        async with aiohttp.ClientSession() as session:
            semaphore = asyncio.Semaphore(self.max_concurrent)
            
            async def fetch_single(endpoint):
                async with semaphore:
                    async with session.get(f"{self.base_url}/{endpoint}") as response:
                        return await response.json()
            
            tasks = [fetch_single(endpoint) for endpoint in endpoints]
            return await asyncio.gather(*tasks)

# 使用示例
async def main():
    client = AsyncAPIClient("https://api.example.com")
    endpoints = ["users", "posts", "comments"]
    results = await client.fetch_data(endpoints)
    print(f"Fetched {len(results)} datasets")
```

## 数据科学与机器学习

### 1. 机器学习管道

```python
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report
import joblib

class MLPipeline:
    """机器学习管道"""
    
    def __init__(self, model_name: str = "random_forest"):
        self.model_name = model_name
        self.model = None
        self.feature_names = None
        
    def prepare_data(self, df: pd.DataFrame, target_col: str):
        """数据预处理"""
        X = df.drop(columns=[target_col])
        y = df[target_col]
        
        # 处理分类特征
        from sklearn.preprocessing import LabelEncoder
        le = LabelEncoder()
        
        for col in X.select_dtypes(include=['object']).columns:
            X[col] = le.fit_transform(X[col].astype(str))
        
        self.feature_names = X.columns.tolist()
        return train_test_split(X, y, test_size=0.2, random_state=42)
    
    def train(self, X_train, y_train):
        """训练模型"""
        self.model = RandomForestClassifier(n_estimators=100, random_state=42)
        self.model.fit(X_train, y_train)
        
    def evaluate(self, X_test, y_test):
        """评估模型"""
        y_pred = self.model.predict(X_test)
        report = classification_report(y_test, y_pred)
        print("Classification Report:")
        print(report)
        return report
    
    def save_model(self, path: str):
        """保存模型"""
        joblib.dump({
            'model': self.model,
            'feature_names': self.feature_names
        }, path)
```

### 2. 深度学习

```python
import tensorflow as tf
from tensorflow import keras
import matplotlib.pyplot as plt

class NeuralNetworkBuilder:
    """神经网络构建器"""
    
    def __init__(self):
        self.model = None
        self.history = None
    
    def build_classifier(self, input_dim: int, num_classes: int):
        """构建分类器"""
        model = keras.Sequential([
            keras.layers.Dense(128, activation='relu', input_shape=(input_dim,)),
            keras.layers.Dropout(0.3),
            keras.layers.Dense(64, activation='relu'),
            keras.layers.Dropout(0.2),
            keras.layers.Dense(num_classes, activation='softmax')
        ])
        
        model.compile(
            optimizer='adam',
            loss='sparse_categorical_crossentropy',
            metrics=['accuracy']
        )
        
        self.model = model
        return model
    
    def train(self, X_train, y_train, X_val, y_val, epochs=50):
        """训练模型"""
        callbacks = [
            keras.callbacks.EarlyStopping(patience=10, restore_best_weights=True),
            keras.callbacks.ReduceLROnPlateau(factor=0.5, patience=5)
        ]
        
        self.history = self.model.fit(
            X_train, y_train,
            validation_data=(X_val, y_val),
            epochs=epochs,
            batch_size=32,
            callbacks=callbacks,
            verbose=1
        )
        
    def plot_history(self):
        """绘制训练历史"""
        fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 4))
        
        ax1.plot(self.history.history['loss'], label='Training Loss')
        ax1.plot(self.history.history['val_loss'], label='Validation Loss')
        ax1.set_title('Model Loss')
        ax1.legend()
        
        ax2.plot(self.history.history['accuracy'], label='Training Accuracy')
        ax2.plot(self.history.history['val_accuracy'], label='Validation Accuracy')
        ax2.set_title('Model Accuracy')
        ax2.legend()
        
        plt.tight_layout()
        plt.show()
```

## Web开发

### 1. Django项目

```python
# Django模型
from django.db import models
from django.contrib.auth.models import AbstractUser

class CustomUser(AbstractUser):
    email = models.EmailField(unique=True)
    phone = models.CharField(max_length=15, blank=True)
    created_at = models.DateTimeField(auto_now_add=True)
    
    USERNAME_FIELD = 'email'

class Product(models.Model):
    name = models.CharField(max_length=200)
    description = models.TextField()
    price = models.DecimalField(max_digits=10, decimal_places=2)
    created_at = models.DateTimeField(auto_now_add=True)
    
    def __str__(self):
        return self.name

# Django视图
from django.shortcuts import render, get_object_or_404
from django.http import JsonResponse
from rest_framework.decorators import api_view
from rest_framework.response import Response

@api_view(['GET', 'POST'])
def product_list(request):
    if request.method == 'GET':
        products = Product.objects.all()
        data = [{
            'id': p.id,
            'name': p.name,
            'price': str(p.price)
        } for p in products]
        return Response(data)
    
    elif request.method == 'POST':
        serializer = ProductSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=201)
        return Response(serializer.errors, status=400)
```

### 2. FastAPI项目

```python
from fastapi import FastAPI, HTTPException, Depends
from pydantic import BaseModel
from typing import List, Optional
import uvicorn

app = FastAPI(title="AI-Generated API", version="1.0.0")

class UserCreate(BaseModel):
    name: str
    email: str
    age: Optional[int] = None

class User(BaseModel):
    id: int
    name: str
    email: str
    age: Optional[int]

# 模拟数据库
users_db = []
user_id_counter = 1

@app.post("/users/", response_model=User)
async def create_user(user: UserCreate):
    global user_id_counter
    new_user = User(id=user_id_counter, **user.dict())
    users_db.append(new_user)
    user_id_counter += 1
    return new_user

@app.get("/users/", response_model=List[User])
async def list_users():
    return users_db

@app.get("/users/{user_id}", response_model=User)
async def get_user(user_id: int):
    user = next((u for u in users_db if u.id == user_id), None)
    if not user:
        raise HTTPException(status_code=404, detail="User not found")
    return user

if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

## 测试与调试

### 1. 自动化测试

```python
import pytest
import pandas as pd
from unittest.mock import Mock, patch

class TestDataProcessor:
    
    @pytest.fixture
    def sample_data(self):
        return pd.DataFrame({
            'name': ['Alice', 'Bob', 'Charlie'],
            'age': [25, 30, 35],
            'city': ['NYC', 'LA', 'Chicago']
        })
    
    @pytest.fixture
    def processor(self):
        config = {'format': 'csv', 'encoding': 'utf-8'}
        return DataProcessor(config)
    
    def test_clean_data_removes_duplicates(self, processor, sample_data):
        # 添加重复行
        duplicate_data = pd.concat([sample_data, sample_data.iloc[:1]])
        
        cleaned = processor.clean_data(duplicate_data)
        
        assert len(cleaned) == len(sample_data)
        assert not cleaned.duplicated().any()
    
    @patch('pandas.read_csv')
    def test_load_csv_success(self, mock_read_csv, processor, sample_data):
        mock_read_csv.return_value = sample_data
        
        result = processor.load_csv('test.csv')
        
        mock_read_csv.assert_called_once_with('test.csv')
        pd.testing.assert_frame_equal(result, sample_data)
    
    def test_load_csv_file_not_found(self, processor):
        with pytest.raises(FileNotFoundError):
            processor.load_csv('nonexistent.csv')

# 性能测试
@pytest.mark.performance
def test_large_dataset_performance():
    large_data = pd.DataFrame({
        'col1': np.random.randn(100000),
        'col2': np.random.randn(100000)
    })
    
    processor = DataProcessor({})
    
    import time
    start = time.time()
    result = processor.clean_data(large_data)
    duration = time.time() - start
    
    assert duration < 5.0  # 应在5秒内完成
    assert len(result) > 0
```

### 2. 调试助手

```python
import logging
from functools import wraps

# 配置日志
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

def debug_function(func):
    """调试装饰器"""
    @wraps(func)
    def wrapper(*args, **kwargs):
        logger.info(f"Calling {func.__name__} with args={args}, kwargs={kwargs}")
        try:
            result = func(*args, **kwargs)
            logger.info(f"{func.__name__} returned: {result}")
            return result
        except Exception as e:
            logger.error(f"Error in {func.__name__}: {e}")
            raise
    return wrapper

class PerformanceMonitor:
    """性能监控器"""
    
    @staticmethod
    def measure_time(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            import time
            start = time.time()
            result = func(*args, **kwargs)
            duration = time.time() - start
            print(f"{func.__name__} took {duration:.4f} seconds")
            return result
        return wrapper
```

## 最佳实践

### 1. 代码质量保证

```python
# 类型注解示例
from typing import List, Dict, Optional, Union
from dataclasses import dataclass

@dataclass
class DataPoint:
    """数据点类"""
    x: float
    y: float
    label: Optional[str] = None
    metadata: Dict[str, Union[str, int, float]] = None

def process_data_points(
    data: List[DataPoint],
    threshold: float = 0.5
) -> List[DataPoint]:
    """
    处理数据点列表
    
    Args:
        data: 数据点列表
        threshold: 过滤阈值
        
    Returns:
        过滤后的数据点列表
    """
    return [point for point in data if point.x > threshold]

# 错误处理
class DataProcessingError(Exception):
    """数据处理异常"""
    pass

def safe_divide(a: float, b: float) -> float:
    """安全除法操作"""
    if b == 0:
        raise DataProcessingError("Division by zero")
    return a / b
```

### 2. 项目结构

```
project/
├── src/
│   ├── __init__.py
│   ├── models/
│   ├── services/
│   ├── utils/
│   └── config.py
├── tests/
│   ├── test_models.py
│   ├── test_services.py
│   └── conftest.py
├── requirements.txt
├── setup.py
└── README.md
```

### 3. 环境管理

```bash
# 虚拟环境管理
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# 依赖管理
pip install -r requirements.txt
pip freeze > requirements.txt

# 使用poetry
poetry init
poetry add numpy pandas scikit-learn
poetry install
```

---

*最后更新: 2025年*

[返回顶部](#pycharm--ai-完整指南) | [English](./pycharm-ai-guide-en.md) 