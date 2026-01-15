<div class="hero-section">
  <img src="images/project-hero.jpg" alt="Mini Project" onerror="this.style.display='none'">
  <div class="hero-overlay">
    <h1>Putting It All Together: Mini Project</h1>
  </div>
</div>

Apply everything you've learned by building a complete application with GitHub Copilot.

## Project Overview

Build a **Task Management API** with user authentication, CRUD operations, and deployment-ready configuration.

### Learning Objectives

- Apply context engineering techniques
- Use Copilot for full-stack development
- Implement security best practices
- Write comprehensive tests
- Create production-ready code

## Project Specifications

### Tech Stack

- **Backend**: Python/Flask or Node.js/Express
- **Database**: SQLite (development) / PostgreSQL (production)
- **Authentication**: JWT tokens
- **Testing**: pytest or Jest
- **Documentation**: OpenAPI/Swagger

### Features

1. User authentication (register, login, logout)
2. Task CRUD operations (create, read, update, delete)
3. Task filtering and search
4. User-specific task lists
5. Task categories and priorities
6. Due date management
7. API documentation
8. Comprehensive tests

## Project Structure

### Directory Layout

```
task-manager-api/
├── src/
│   ├── __init__.py
│   ├── app.py              # Application entry point
│   ├── config.py           # Configuration management
│   ├── models/
│   │   ├── __init__.py
│   │   ├── user.py         # User model
│   │   └── task.py         # Task model
│   ├── routes/
│   │   ├── __init__.py
│   │   ├── auth.py         # Authentication routes
│   │   └── tasks.py        # Task routes
│   ├── services/
│   │   ├── __init__.py
│   │   ├── auth_service.py # Authentication logic
│   │   └── task_service.py # Task business logic
│   └── utils/
│       ├── __init__.py
│       ├── validators.py   # Input validation
│       └── decorators.py   # Custom decorators
├── tests/
│   ├── __init__.py
│   ├── test_auth.py
│   └── test_tasks.py
├── requirements.txt
├── README.md
└── .env.example
```

## Implementation Guide

### Phase 1: Project Setup

#### Step 1: Initialize Project

Use Copilot to help set up the project structure:

```python
# Create the basic Flask application structure
# Requirements:
# - Flask with CORS support
# - SQLAlchemy for ORM
# - JWT for authentication
# - Environment variable configuration
# - Development and production configs

# src/app.py
"""
Task Manager API - Main Application

A RESTful API for managing tasks with user authentication.
Uses Flask, SQLAlchemy, and JWT for secure task management.
"""

from flask import Flask
from flask_sqlalchemy import SQLAlchemy
from flask_cors import CORS
from flask_jwt_extended import JWTManager

# Let Copilot help initialize the app
```

#### Step 2: Configuration

```python
# src/config.py
"""
Application Configuration

Manages different configurations for development, testing, and production.
Loads sensitive data from environment variables.
"""

import os
from datetime import timedelta

class Config:
    """Base configuration"""
    # Use Copilot to generate configuration class with:
    # - Database URL
    # - Secret key
    # - JWT settings
    # - CORS settings
```

### Phase 2: Database Models

#### Step 3: User Model

```python
# src/models/user.py
"""
User Model

Represents a user in the system with authentication capabilities.
Includes password hashing and verification methods.
"""

from werkzeug.security import generate_password_hash, check_password_hash
from datetime import datetime

class User:
    """
    User model with authentication
    
    Attributes:
        id: Unique user identifier
        username: Unique username (3-50 characters)
        email: Unique email address
        password_hash: Hashed password (never store plain text)
        created_at: Account creation timestamp
        updated_at: Last update timestamp
    
    Methods:
        set_password: Hash and set user password
        check_password: Verify password against hash
        to_dict: Convert user to dictionary (excluding password)
    """
    # Let Copilot generate the model with proper hashing
```

#### Step 4: Task Model

```python
# src/models/task.py
"""
Task Model

Represents a task with priority, category, and due date.
Each task belongs to a specific user.
"""

from datetime import datetime
from enum import Enum

class TaskPriority(Enum):
    """Task priority levels"""
    LOW = 1
    MEDIUM = 2
    HIGH = 3
    URGENT = 4

class TaskStatus(Enum):
    """Task status options"""
    TODO = "todo"
    IN_PROGRESS = "in_progress"
    COMPLETED = "completed"
    CANCELLED = "cancelled"

class Task:
    """
    Task model with full CRUD capabilities
    
    Attributes:
        id: Unique task identifier
        title: Task title (required, 1-200 characters)
        description: Detailed task description (optional)
        priority: Task priority level
        status: Current task status
        category: Task category (optional)
        due_date: Task due date (optional)
        user_id: Owner user ID (foreign key)
        created_at: Creation timestamp
        updated_at: Last update timestamp
        completed_at: Completion timestamp (null if not completed)
    
    Methods:
        to_dict: Convert task to dictionary
        is_overdue: Check if task is past due date
        mark_completed: Mark task as completed
    """
    # Copilot generates comprehensive model
```

### Phase 3: Authentication

#### Step 5: Authentication Service

```python
# src/services/auth_service.py
"""
Authentication Service

Handles user registration, login, and token management.
Implements security best practices for authentication.
"""

from flask_jwt_extended import create_access_token, create_refresh_token

class AuthService:
    """
    Authentication service with JWT token management
    
    Methods:
        register_user: Create new user account with validation
        authenticate_user: Verify credentials and generate tokens
        validate_username: Check username requirements
        validate_email: Verify email format
        validate_password: Ensure password strength
    
    Password Requirements:
        - Minimum 8 characters
        - At least one uppercase letter
        - At least one lowercase letter
        - At least one number
        - At least one special character
    """
    # Generate authentication logic with Copilot
```

#### Step 6: Authentication Routes

```python
# src/routes/auth.py
"""
Authentication Routes

API endpoints for user registration, login, and token refresh.
All endpoints return JSON responses with appropriate status codes.
"""

from flask import Blueprint, request, jsonify
from flask_jwt_extended import jwt_required, get_jwt_identity

auth_bp = Blueprint('auth', __name__, url_prefix='/api/auth')

@auth_bp.route('/register', methods=['POST'])
def register():
    """
    Register a new user
    
    Request Body:
        {
            "username": "string (3-50 chars)",
            "email": "string (valid email)",
            "password": "string (min 8 chars)"
        }
    
    Returns:
        201: User created successfully
        400: Validation error
        409: Username or email already exists
    """
    # Copilot implements with proper validation and error handling

@auth_bp.route('/login', methods=['POST'])
def login():
    """
    Authenticate user and return JWT tokens
    
    Request Body:
        {
            "username": "string",
            "password": "string"
        }
    
    Returns:
        200: Authentication successful with tokens
        401: Invalid credentials
        400: Validation error
    """
    # Implementation with security best practices
```

### Phase 4: Task Management

#### Step 7: Task Service

```python
# src/services/task_service.py
"""
Task Service

Business logic for task management operations.
Handles task creation, updates, filtering, and search.
"""

class TaskService:
    """
    Task management service
    
    Methods:
        create_task: Create new task for user
        get_task: Retrieve specific task
        get_user_tasks: Get all tasks for user with filtering
        update_task: Update existing task
        delete_task: Delete task
        search_tasks: Search tasks by title/description
        filter_by_priority: Filter tasks by priority
        filter_by_status: Filter tasks by status
        get_overdue_tasks: Get tasks past due date
        get_upcoming_tasks: Get tasks due soon
    
    All methods verify user ownership before operations.
    """
    # Copilot generates comprehensive task management
```

#### Step 8: Task Routes

```python
# src/routes/tasks.py
"""
Task Routes

RESTful API endpoints for task management.
All endpoints require JWT authentication.
"""

from flask import Blueprint, request, jsonify
from flask_jwt_extended import jwt_required, get_jwt_identity

tasks_bp = Blueprint('tasks', __name__, url_prefix='/api/tasks')

@tasks_bp.route('', methods=['GET'])
@jwt_required()
def get_tasks():
    """
    Get all tasks for authenticated user
    
    Query Parameters:
        status: Filter by status (todo, in_progress, completed)
        priority: Filter by priority (low, medium, high, urgent)
        category: Filter by category
        search: Search in title and description
        sort: Sort field (created_at, due_date, priority)
        order: Sort order (asc, desc)
    
    Returns:
        200: List of tasks
        401: Unauthorized
    """
    # Generate with filtering and pagination support

@tasks_bp.route('', methods=['POST'])
@jwt_required()
def create_task():
    """
    Create a new task
    
    Request Body:
        {
            "title": "string (required)",
            "description": "string (optional)",
            "priority": "low|medium|high|urgent",
            "status": "todo|in_progress|completed",
            "category": "string (optional)",
            "due_date": "ISO 8601 date (optional)"
        }
    
    Returns:
        201: Task created
        400: Validation error
        401: Unauthorized
    """
    # Copilot implements with validation

# Continue with PUT, DELETE endpoints
```

### Phase 5: Validation and Security

#### Step 9: Input Validators

```python
# src/utils/validators.py
"""
Input Validation Utilities

Validates and sanitizes user input to prevent security issues.
"""

import re
from datetime import datetime

class Validator:
    """
    Input validation with security in mind
    
    Prevents:
        - SQL injection
        - XSS attacks
        - Invalid data types
        - Out-of-range values
    """
    
    @staticmethod
    def validate_task_input(data):
        """
        Validate task creation/update data
        
        Checks:
            - Required fields present
            - Field types correct
            - String lengths within limits
            - Dates valid and not in past
            - Priority and status valid
        """
        # Generate comprehensive validation

    @staticmethod
    def sanitize_string(value, max_length=None):
        """
        Sanitize string input
        
        Removes:
            - Leading/trailing whitespace
            - Control characters
            - Potentially dangerous characters
        """
        # Security-focused sanitization
```

### Phase 6: Testing

#### Step 10: Authentication Tests

```python
# tests/test_auth.py
"""
Authentication Tests

Comprehensive test suite for authentication endpoints.
"""

import pytest
from src.app import create_app

class TestAuthentication:
    """Test authentication functionality"""
    
    def test_user_registration_success(self):
        """Test successful user registration"""
        # Copilot generates test with proper assertions
    
    def test_user_registration_duplicate_username(self):
        """Test registration with existing username"""
        # Test error handling
    
    def test_user_login_success(self):
        """Test successful login"""
        # Verify token generation
    
    def test_user_login_invalid_credentials(self):
        """Test login with wrong password"""
        # Verify error response
    
    def test_password_strength_validation(self):
        """Test password requirements"""
        # Test various password scenarios
```

#### Step 11: Task Tests

```python
# tests/test_tasks.py
"""
Task Management Tests

Test suite for task CRUD operations and filtering.
"""

import pytest
from datetime import datetime, timedelta

class TestTaskManagement:
    """Test task management functionality"""
    
    def test_create_task_success(self):
        """Test creating a new task"""
        # Copilot generates comprehensive test
    
    def test_get_user_tasks(self):
        """Test retrieving user's tasks"""
        # Verify task retrieval
    
    def test_update_task(self):
        """Test updating task details"""
        # Test update operations
    
    def test_delete_task(self):
        """Test task deletion"""
        # Verify deletion
    
    def test_task_filtering_by_status(self):
        """Test filtering tasks by status"""
        # Test filter functionality
    
    def test_task_search(self):
        """Test task search functionality"""
        # Test search operations
    
    def test_unauthorized_task_access(self):
        """Test that users can't access other users' tasks"""
        # Security test
```

### Phase 7: Documentation

#### Step 12: API Documentation

```python
# Add OpenAPI/Swagger documentation
"""
Generate Swagger/OpenAPI specification for the API

Document:
    - All endpoints
    - Request/response schemas
    - Authentication requirements
    - Error responses
    - Example requests
"""

# Use Copilot to generate comprehensive API docs
```

#### Step 13: README

```markdown
# Task Manager API

A RESTful API for managing tasks with user authentication.

## Features
[Let Copilot help write comprehensive documentation]

## Installation
[Setup instructions]

## API Endpoints
[Endpoint documentation]

## Testing
[Test instructions]

## Deployment
[Deployment guide]
```

## Advanced Challenges

### Challenge 1: Add Real-Time Features

- Implement WebSocket support
- Real-time task updates
- Collaborative task lists

### Challenge 2: Advanced Filtering

- Complex query builder
- Date range filtering
- Tag-based organization

### Challenge 3: Email Notifications

- Task due date reminders
- Task assignment notifications
- Digest emails

### Challenge 4: File Attachments

- Upload files to tasks
- Cloud storage integration
- Image preview support

## Deployment

### Prepare for Production

```python
# Add production configurations:
# - Environment-based settings
# - Database migrations
# - Logging configuration
# - Error monitoring
# - Rate limiting
# - API versioning
```

### Docker Configuration

```dockerfile
# Dockerfile for containerization
# Use Copilot to generate multi-stage build
```

### CI/CD Pipeline

```yaml
# .github/workflows/ci.yml
# Automated testing and deployment
```

## Evaluation Checklist

### Code Quality
- [ ] Clear, descriptive variable names
- [ ] Proper error handling
- [ ] Input validation
- [ ] Security best practices
- [ ] DRY principle followed
- [ ] Comments where necessary

### Functionality
- [ ] All CRUD operations work
- [ ] Authentication secure
- [ ] Filtering and search work
- [ ] Edge cases handled

### Testing
- [ ] Unit tests passing
- [ ] Integration tests passing
- [ ] >80% code coverage
- [ ] Security tests included

### Documentation
- [ ] API documented
- [ ] README complete
- [ ] Code comments present
- [ ] Setup instructions clear

## Reflection Questions

1. How did Copilot help speed up development?
2. What suggestions required the most refinement?
3. How did context engineering affect suggestion quality?
4. What security issues did you catch in suggestions?
5. How would you improve your prompting technique?

## Next Steps

### Expand Your Skills

- Build a frontend for the API
- Add more complex features
- Deploy to cloud platform
- Integrate with external APIs
- Add analytics and reporting

### Continue Learning

- Explore other frameworks
- Try different languages
- Build different project types
- Contribute to open source
- Share your learnings

## Conclusion

Congratulations! You've built a complete application using GitHub Copilot. You've learned to:

✅ Use context engineering effectively  
✅ Apply security best practices  
✅ Write comprehensive tests  
✅ Create production-ready code  
✅ Leverage AI assistance efficiently  

Keep practicing and refining your skills with GitHub Copilot!

---

**Need help?** Review previous chapters or ask questions in Copilot Chat!
