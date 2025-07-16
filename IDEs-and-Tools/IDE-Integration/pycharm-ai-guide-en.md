<div align="center">

# PyCharm + AI Integration Guide

<a href="./pycharm-ai-guide.md">中文</a> | English

</div>

## Overview

PyCharm is the premier Python IDE developed by JetBrains, offering powerful features for Python development. With AI integration, PyCharm becomes an exceptional tool for modern Python development, machine learning, data science, and web development projects.

## Installation and Setup

### System Requirements
- PyCharm 2023.1 or later (Professional or Community Edition)
- Python 3.8 or higher
- Minimum 8GB RAM (16GB recommended for data science)
- Internet connection for AI services

### AI Plugin Installation

#### 1. JetBrains AI Assistant
```bash
# Installation Steps
Settings → Plugins → Marketplace → Search "AI Assistant" → Install
Restart PyCharm → Sign in with JetBrains account
```

#### 2. GitHub Copilot
```bash
Settings → Plugins → Marketplace → Search "GitHub Copilot" → Install
Restart IDE → Sign in with GitHub account → Activate subscription
```

#### 3. Tabnine
```bash
Settings → Plugins → Marketplace → Search "Tabnine" → Install
Configure API key → Set preferences for Python-specific suggestions
```

## Python Development with AI

### 1. Smart Code Generation

#### Class and Function Creation
```python
# AI Prompt: Create a data processing class for customer analytics
class CustomerAnalytics:
    """
    AI Assistant will generate a comprehensive analytics class with:
    - Data loading and preprocessing
    - Statistical analysis methods
    - Visualization capabilities
    - Report generation
    """
    
    def __init__(self, data_source: str):
        self.data_source = data_source
        self.data = None
        self.processed_data = None
        
    def load_data(self) -> pd.DataFrame:
        """Load customer data from various sources"""
        try:
            if self.data_source.endswith('.csv'):
                self.data = pd.read_csv(self.data_source)
            elif self.data_source.endswith('.json'):
                self.data = pd.read_json(self.data_source)
            elif self.data_source.endswith('.xlsx'):
                self.data = pd.read_excel(self.data_source)
            else:
                raise ValueError(f"Unsupported file format: {self.data_source}")
            
            print(f"Data loaded successfully: {self.data.shape}")
            return self.data
            
        except FileNotFoundError:
            raise FileNotFoundError(f"Data file not found: {self.data_source}")
        except Exception as e:
            raise Exception(f"Error loading data: {str(e)}")
    
    def preprocess_data(self) -> pd.DataFrame:
        """Clean and preprocess customer data"""
        if self.data is None:
            raise ValueError("Data not loaded. Call load_data() first.")
        
        # Remove duplicates
        self.processed_data = self.data.drop_duplicates()
        
        # Handle missing values
        numeric_columns = self.processed_data.select_dtypes(include=[np.number]).columns
        self.processed_data[numeric_columns] = self.processed_data[numeric_columns].fillna(
            self.processed_data[numeric_columns].median()
        )
        
        # Fill categorical missing values with mode
        categorical_columns = self.processed_data.select_dtypes(include=['object']).columns
        for col in categorical_columns:
            self.processed_data[col] = self.processed_data[col].fillna(
                self.processed_data[col].mode().iloc[0] if not self.processed_data[col].mode().empty else 'Unknown'
            )
        
        # Convert date columns
        date_columns = [col for col in self.processed_data.columns if 'date' in col.lower()]
        for col in date_columns:
            self.processed_data[col] = pd.to_datetime(self.processed_data[col], errors='coerce')
        
        return self.processed_data
    
    def analyze_customer_segments(self) -> Dict[str, Any]:
        """Perform customer segmentation analysis"""
        if self.processed_data is None:
            raise ValueError("Data not preprocessed. Call preprocess_data() first.")
        
        analysis_results = {}
        
        # Age distribution analysis
        if 'age' in self.processed_data.columns:
            analysis_results['age_distribution'] = {
                'mean': self.processed_data['age'].mean(),
                'median': self.processed_data['age'].median(),
                'std': self.processed_data['age'].std(),
                'quantiles': self.processed_data['age'].quantile([0.25, 0.5, 0.75]).to_dict()
            }
        
        # Purchase behavior analysis
        if 'total_purchases' in self.processed_data.columns:
            analysis_results['purchase_behavior'] = {
                'total_revenue': self.processed_data['total_purchases'].sum(),
                'average_purchase': self.processed_data['total_purchases'].mean(),
                'top_customers': self.processed_data.nlargest(10, 'total_purchases')['customer_id'].tolist()
            }
        
        # Geographic distribution
        if 'country' in self.processed_data.columns:
            analysis_results['geographic_distribution'] = (
                self.processed_data['country'].value_counts().head(10).to_dict()
            )
        
        return analysis_results
    
    def generate_insights(self) -> List[str]:
        """Generate actionable business insights"""
        insights = []
        analysis = self.analyze_customer_segments()
        
        # Age-based insights
        if 'age_distribution' in analysis:
            avg_age = analysis['age_distribution']['mean']
            if avg_age < 30:
                insights.append("Target audience is primarily young adults - focus on digital marketing")
            elif avg_age > 50:
                insights.append("Mature customer base - emphasize quality and reliability")
        
        # Purchase behavior insights
        if 'purchase_behavior' in analysis:
            avg_purchase = analysis['purchase_behavior']['average_purchase']
            insights.append(f"Average customer value: ${avg_purchase:.2f}")
        
        return insights
```

### 2. Machine Learning Integration

#### AI-Generated ML Pipeline
```python
# AI Prompt: Create a machine learning pipeline for predictive analytics
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report, confusion_matrix, roc_auc_score
from sklearn.preprocessing import StandardScaler, LabelEncoder
import joblib

class MLPipeline:
    """Complete machine learning pipeline with automated model selection"""
    
    def __init__(self, target_column: str):
        self.target_column = target_column
        self.models = {
            'random_forest': RandomForestClassifier(n_estimators=100, random_state=42),
            'gradient_boosting': GradientBoostingClassifier(random_state=42),
            'logistic_regression': LogisticRegression(random_state=42, max_iter=1000)
        }
        self.best_model = None
        self.scaler = StandardScaler()
        self.label_encoders = {}
        self.feature_importance = None
        
    def prepare_features(self, df: pd.DataFrame) -> Tuple[pd.DataFrame, pd.Series]:
        """Prepare features for machine learning"""
        # Separate features and target
        X = df.drop(columns=[self.target_column])
        y = df[self.target_column]
        
        # Handle categorical variables
        categorical_columns = X.select_dtypes(include=['object']).columns
        for col in categorical_columns:
            le = LabelEncoder()
            X[col] = le.fit_transform(X[col].astype(str))
            self.label_encoders[col] = le
        
        # Scale numerical features
        numerical_columns = X.select_dtypes(include=[np.number]).columns
        X[numerical_columns] = self.scaler.fit_transform(X[numerical_columns])
        
        # Encode target variable if categorical
        if y.dtype == 'object':
            le_target = LabelEncoder()
            y = le_target.fit_transform(y)
            self.label_encoders['target'] = le_target
        
        return X, y
    
    def train_models(self, X: pd.DataFrame, y: pd.Series) -> Dict[str, float]:
        """Train multiple models and return performance scores"""
        X_train, X_test, y_train, y_test = train_test_split(
            X, y, test_size=0.2, random_state=42, stratify=y
        )
        
        model_scores = {}
        
        for name, model in self.models.items():
            # Train model
            model.fit(X_train, y_train)
            
            # Make predictions
            y_pred = model.predict(X_test)
            y_pred_proba = model.predict_proba(X_test)[:, 1] if hasattr(model, 'predict_proba') else None
            
            # Calculate scores
            accuracy = model.score(X_test, y_test)
            auc_score = roc_auc_score(y_test, y_pred_proba) if y_pred_proba is not None else 0
            
            model_scores[name] = {
                'accuracy': accuracy,
                'auc': auc_score,
                'classification_report': classification_report(y_test, y_pred, output_dict=True)
            }
            
            print(f"{name.title()} - Accuracy: {accuracy:.4f}, AUC: {auc_score:.4f}")
        
        # Select best model based on AUC score
        best_model_name = max(model_scores.keys(), key=lambda k: model_scores[k]['auc'])
        self.best_model = self.models[best_model_name]
        
        # Store feature importance
        if hasattr(self.best_model, 'feature_importances_'):
            self.feature_importance = pd.DataFrame({
                'feature': X.columns,
                'importance': self.best_model.feature_importances_
            }).sort_values('importance', ascending=False)
        
        print(f"Best model: {best_model_name}")
        return model_scores
    
    def predict(self, X: pd.DataFrame) -> np.ndarray:
        """Make predictions with the best model"""
        if self.best_model is None:
            raise ValueError("No model trained. Call train_models() first.")
        
        # Apply same preprocessing
        for col, le in self.label_encoders.items():
            if col != 'target' and col in X.columns:
                X[col] = le.transform(X[col].astype(str))
        
        numerical_columns = X.select_dtypes(include=[np.number]).columns
        X[numerical_columns] = self.scaler.transform(X[numerical_columns])
        
        return self.best_model.predict(X)
    
    def save_model(self, filepath: str):
        """Save the trained model and preprocessors"""
        model_package = {
            'model': self.best_model,
            'scaler': self.scaler,
            'label_encoders': self.label_encoders,
            'feature_importance': self.feature_importance
        }
        joblib.dump(model_package, filepath)
        print(f"Model saved to: {filepath}")
```

### 3. Web Development with AI

#### Django/FastAPI Integration
```python
# AI Prompt: Create a FastAPI application with user authentication
from fastapi import FastAPI, HTTPException, Depends, status
from fastapi.security import HTTPBearer, HTTPAuthorizationCredentials
from fastapi.middleware.cors import CORSMiddleware
from pydantic import BaseModel, EmailStr, validator
from sqlalchemy import create_engine, Column, Integer, String, DateTime, Boolean
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker, Session
from passlib.context import CryptContext
from datetime import datetime, timedelta
import jwt
from typing import Optional, List

# Database setup
SQLALCHEMY_DATABASE_URL = "sqlite:///./app.db"
engine = create_engine(SQLALCHEMY_DATABASE_URL, connect_args={"check_same_thread": False})
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()

# Security
pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")
security = HTTPBearer()
SECRET_KEY = "your-secret-key-change-in-production"
ALGORITHM = "HS256"

app = FastAPI(title="AI-Generated API", version="1.0.0")

# CORS middleware
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

# Models
class User(Base):
    __tablename__ = "users"
    
    id = Column(Integer, primary_key=True, index=True)
    email = Column(String, unique=True, index=True, nullable=False)
    username = Column(String, unique=True, index=True, nullable=False)
    hashed_password = Column(String, nullable=False)
    is_active = Column(Boolean, default=True)
    created_at = Column(DateTime, default=datetime.utcnow)

# Pydantic models
class UserCreate(BaseModel):
    email: EmailStr
    username: str
    password: str
    
    @validator('username')
    def validate_username(cls, v):
        if len(v) < 3:
            raise ValueError('Username must be at least 3 characters long')
        return v
    
    @validator('password')
    def validate_password(cls, v):
        if len(v) < 8:
            raise ValueError('Password must be at least 8 characters long')
        return v

class UserResponse(BaseModel):
    id: int
    email: str
    username: str
    is_active: bool
    created_at: datetime
    
    class Config:
        orm_mode = True

class Token(BaseModel):
    access_token: str
    token_type: str

# Database dependency
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

# Authentication functions
def verify_password(plain_password: str, hashed_password: str) -> bool:
    return pwd_context.verify(plain_password, hashed_password)

def get_password_hash(password: str) -> str:
    return pwd_context.hash(password)

def create_access_token(data: dict, expires_delta: Optional[timedelta] = None):
    to_encode = data.copy()
    expire = datetime.utcnow() + (expires_delta or timedelta(minutes=15))
    to_encode.update({"exp": expire})
    return jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)

def verify_token(credentials: HTTPAuthorizationCredentials = Depends(security)):
    try:
        payload = jwt.decode(credentials.credentials, SECRET_KEY, algorithms=[ALGORITHM])
        email: str = payload.get("sub")
        if email is None:
            raise HTTPException(status_code=401, detail="Invalid authentication credentials")
        return email
    except jwt.PyJWTError:
        raise HTTPException(status_code=401, detail="Invalid authentication credentials")

def get_current_user(db: Session = Depends(get_db), token: str = Depends(verify_token)):
    user = db.query(User).filter(User.email == token).first()
    if user is None:
        raise HTTPException(status_code=401, detail="User not found")
    return user

# API Routes
@app.post("/register", response_model=UserResponse)
def register_user(user: UserCreate, db: Session = Depends(get_db)):
    # Check if user exists
    if db.query(User).filter(User.email == user.email).first():
        raise HTTPException(status_code=400, detail="Email already registered")
    
    if db.query(User).filter(User.username == user.username).first():
        raise HTTPException(status_code=400, detail="Username already taken")
    
    # Create new user
    hashed_password = get_password_hash(user.password)
    db_user = User(
        email=user.email,
        username=user.username,
        hashed_password=hashed_password
    )
    
    db.add(db_user)
    db.commit()
    db.refresh(db_user)
    
    return db_user

@app.post("/login", response_model=Token)
def login_user(email: str, password: str, db: Session = Depends(get_db)):
    user = db.query(User).filter(User.email == email).first()
    
    if not user or not verify_password(password, user.hashed_password):
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Incorrect email or password"
        )
    
    access_token = create_access_token(
        data={"sub": user.email},
        expires_delta=timedelta(days=7)
    )
    
    return {"access_token": access_token, "token_type": "bearer"}

@app.get("/users/me", response_model=UserResponse)
def get_current_user_info(current_user: User = Depends(get_current_user)):
    return current_user

@app.get("/users", response_model=List[UserResponse])
def get_all_users(db: Session = Depends(get_db), current_user: User = Depends(get_current_user)):
    users = db.query(User).all()
    return users

# Create tables
Base.metadata.create_all(bind=engine)

if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

### 4. Data Science and Analysis

#### AI-Generated Data Analysis
```python
# AI Prompt: Create comprehensive data analysis functions
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
import plotly.express as px
import plotly.graph_objects as go

class DataAnalyzer:
    """Comprehensive data analysis toolkit with AI-generated insights"""
    
    def __init__(self, dataframe: pd.DataFrame):
        self.df = dataframe
        self.numeric_columns = self.df.select_dtypes(include=[np.number]).columns.tolist()
        self.categorical_columns = self.df.select_dtypes(include=['object']).columns.tolist()
    
    def generate_summary_report(self) -> Dict[str, Any]:
        """Generate comprehensive data summary report"""
        report = {
            'basic_info': {
                'shape': self.df.shape,
                'memory_usage': self.df.memory_usage(deep=True).sum(),
                'null_values': self.df.isnull().sum().to_dict(),
                'duplicate_rows': self.df.duplicated().sum()
            },
            'numeric_summary': self.df[self.numeric_columns].describe().to_dict() if self.numeric_columns else {},
            'categorical_summary': {
                col: {
                    'unique_values': self.df[col].nunique(),
                    'most_frequent': self.df[col].mode().iloc[0] if not self.df[col].mode().empty else None,
                    'value_counts': self.df[col].value_counts().head().to_dict()
                } for col in self.categorical_columns
            }
        }
        
        return report
    
    def detect_outliers(self, method: str = 'iqr') -> Dict[str, List]:
        """Detect outliers using IQR or Z-score method"""
        outliers = {}
        
        for col in self.numeric_columns:
            if method == 'iqr':
                Q1 = self.df[col].quantile(0.25)
                Q3 = self.df[col].quantile(0.75)
                IQR = Q3 - Q1
                lower_bound = Q1 - 1.5 * IQR
                upper_bound = Q3 + 1.5 * IQR
                outlier_mask = (self.df[col] < lower_bound) | (self.df[col] > upper_bound)
            
            elif method == 'zscore':
                z_scores = np.abs(stats.zscore(self.df[col].dropna()))
                outlier_mask = z_scores > 3
            
            outliers[col] = self.df[outlier_mask].index.tolist()
        
        return outliers
    
    def create_visualizations(self, output_dir: str = 'plots'):
        """Generate comprehensive visualizations"""
        import os
        os.makedirs(output_dir, exist_ok=True)
        
        # Correlation heatmap
        if len(self.numeric_columns) > 1:
            plt.figure(figsize=(12, 8))
            correlation_matrix = self.df[self.numeric_columns].corr()
            sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)
            plt.title('Correlation Matrix')
            plt.tight_layout()
            plt.savefig(f'{output_dir}/correlation_heatmap.png', dpi=300, bbox_inches='tight')
            plt.close()
        
        # Distribution plots for numeric columns
        for col in self.numeric_columns:
            fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(15, 5))
            
            # Histogram
            self.df[col].hist(bins=30, ax=ax1)
            ax1.set_title(f'Distribution of {col}')
            ax1.set_xlabel(col)
            ax1.set_ylabel('Frequency')
            
            # Box plot
            self.df.boxplot(column=col, ax=ax2)
            ax2.set_title(f'Box Plot of {col}')
            
            plt.tight_layout()
            plt.savefig(f'{output_dir}/distribution_{col}.png', dpi=300, bbox_inches='tight')
            plt.close()
        
        # Categorical value counts
        for col in self.categorical_columns:
            plt.figure(figsize=(12, 6))
            value_counts = self.df[col].value_counts().head(10)
            value_counts.plot(kind='bar')
            plt.title(f'Top 10 Values in {col}')
            plt.xlabel(col)
            plt.ylabel('Count')
            plt.xticks(rotation=45)
            plt.tight_layout()
            plt.savefig(f'{output_dir}/categorical_{col}.png', dpi=300, bbox_inches='tight')
            plt.close()
    
    def statistical_tests(self) -> Dict[str, Any]:
        """Perform statistical tests on the data"""
        results = {}
        
        # Normality tests for numeric columns
        for col in self.numeric_columns:
            if len(self.df[col].dropna()) > 5000:  # Use KS test for large samples
                statistic, p_value = stats.kstest(self.df[col].dropna(), 'norm')
                test_name = 'Kolmogorov-Smirnov'
            else:  # Use Shapiro-Wilk for smaller samples
                statistic, p_value = stats.shapiro(self.df[col].dropna())
                test_name = 'Shapiro-Wilk'
            
            results[f'{col}_normality'] = {
                'test': test_name,
                'statistic': statistic,
                'p_value': p_value,
                'is_normal': p_value > 0.05
            }
        
        return results
```

## Testing and Debugging with AI

### 1. Automated Test Generation
```python
# AI generates comprehensive test suite
import pytest
import unittest.mock as mock
from unittest.mock import patch, MagicMock

class TestCustomerAnalytics:
    
    @pytest.fixture
    def sample_data(self):
        return pd.DataFrame({
            'customer_id': range(1, 101),
            'age': np.random.randint(18, 80, 100),
            'total_purchases': np.random.uniform(100, 5000, 100),
            'country': np.random.choice(['USA', 'Canada', 'UK', 'Germany'], 100)
        })
    
    @pytest.fixture
    def analytics(self, tmp_path):
        csv_file = tmp_path / "test_data.csv"
        return CustomerAnalytics(str(csv_file))
    
    def test_load_data_success(self, analytics, sample_data, tmp_path):
        csv_file = tmp_path / "test_data.csv"
        sample_data.to_csv(csv_file, index=False)
        
        result = analytics.load_data()
        assert len(result) == 100
        assert list(result.columns) == ['customer_id', 'age', 'total_purchases', 'country']
    
    def test_load_data_file_not_found(self, analytics):
        with pytest.raises(FileNotFoundError):
            analytics.load_data()
    
    @patch('pandas.read_csv')
    def test_preprocess_data(self, mock_read_csv, analytics, sample_data):
        mock_read_csv.return_value = sample_data
        analytics.data = sample_data.copy()
        
        result = analytics.preprocess_data()
        assert len(result) <= len(sample_data)  # Should be same or fewer due to duplicate removal
        assert result.isnull().sum().sum() == 0  # No null values after preprocessing
    
    def test_analyze_customer_segments(self, analytics, sample_data):
        analytics.processed_data = sample_data
        
        results = analytics.analyze_customer_segments()
        assert 'age_distribution' in results
        assert 'purchase_behavior' in results
        assert 'geographic_distribution' in results
        
        # Verify age distribution calculations
        age_stats = results['age_distribution']
        assert 'mean' in age_stats
        assert 'median' in age_stats
        assert age_stats['mean'] == sample_data['age'].mean()
```

## Best Practices and Configuration

### 1. PyCharm AI Settings
```json
{
  "ai.assistant.python.enableSmartCompletion": true,
  "ai.assistant.python.generateDocstrings": true,
  "ai.assistant.python.suggestRefactoring": true,
  "ai.assistant.dataScience.enableMLSuggestions": true,
  "ai.assistant.testing.generatePytestCases": true,
  "ai.assistant.django.enableFrameworkSupport": true,
  "ai.assistant.flask.enableFrameworkSupport": true
}
```

### 2. Code Quality and Standards
- Follow PEP 8 style guidelines with AI assistance
- Use type hints for better AI suggestions
- Maintain comprehensive docstrings
- Implement proper error handling
- Regular code reviews with AI assistance

### 3. Performance Optimization
- Profile code with AI-suggested improvements
- Optimize data processing pipelines
- Use vectorized operations in NumPy/Pandas
- Implement caching for expensive computations

## Integration with Data Science Tools

### 1. Jupyter Notebook Integration
- AI-powered cell completion
- Automatic visualization suggestions
- Smart data exploration
- Markdown documentation generation

### 2. Popular Libraries Support
- **Pandas**: Data manipulation with AI suggestions
- **NumPy**: Numerical computing optimization
- **Scikit-learn**: ML model recommendations
- **TensorFlow/PyTorch**: Deep learning assistance
- **Matplotlib/Seaborn**: Visualization improvements

## Troubleshooting

### Common Issues
1. **Slow AI response**: Increase IDE memory allocation
2. **Irrelevant suggestions**: Provide better code context
3. **Plugin conflicts**: Update all plugins to latest versions
4. **Import errors**: Configure Python interpreter correctly

### Performance Tips
- Use virtual environments for project isolation
- Configure appropriate Python interpreter
- Optimize AI suggestion frequency
- Clear IDE caches when necessary

## Conclusion

PyCharm with AI integration significantly enhances Python development productivity across various domains including web development, data science, machine learning, and automation. The combination of PyCharm's powerful features with AI assistance creates an exceptional development environment for modern Python projects. 