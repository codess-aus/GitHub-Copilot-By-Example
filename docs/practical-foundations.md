# Practical Foundations: Coding with Copilot

Learn hands-on techniques for effective coding with GitHub Copilot through practical examples.

## Getting Started with Copilot

### Your First Code with Copilot

Let's start with a simple example:

```python
# Function to check if a number is prime
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True
```

!!! tip "Comment-First Development"
    Write a clear comment describing what you want, then let Copilot generate the implementation.

## Core Techniques

### 1. Descriptive Comments

The quality of comments directly impacts suggestion quality:

**Good Comment:**
```python
# Calculate the average of a list of numbers, handling empty lists and None values
def calculate_average(numbers):
    # Copilot generates robust implementation
```

**Poor Comment:**
```python
# avg function
def avg(n):
    # Less context = less helpful suggestions
```

### 2. Function Signatures

Provide clear function signatures:

```typescript
// Good: Clear types and parameters
function fetchUserData(userId: string, includeOrders: boolean): Promise<UserData> {
  // Copilot understands the expected behavior
}

// Poor: Vague signature
function getData(id) {
  // Copilot has less context
}
```

### 3. Test-Driven Development

Generate tests with Copilot:

```python
# Test suite for email validation
import unittest

class TestEmailValidation(unittest.TestCase):
    def test_valid_email(self):
        self.assertTrue(is_valid_email("user@example.com"))
    
    def test_invalid_email_no_at(self):
        self.assertFalse(is_valid_email("userexample.com"))
    
    def test_invalid_email_no_domain(self):
        self.assertFalse(is_valid_email("user@"))
```

## Common Patterns

### Pattern 1: Data Processing

```python
# Process a list of transactions and calculate totals by category
def calculate_category_totals(transactions):
    category_totals = {}
    for transaction in transactions:
        category = transaction.get('category', 'uncategorized')
        amount = transaction.get('amount', 0)
        category_totals[category] = category_totals.get(category, 0) + amount
    return category_totals
```

### Pattern 2: API Integration

```javascript
// Fetch weather data from an API with error handling
async function getWeatherData(city) {
  try {
    const response = await fetch(`https://api.weather.com/v1/weather?city=${city}`);
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error fetching weather data:', error);
    return null;
  }
}
```

### Pattern 3: Class Implementation

```python
# User management class with authentication
class UserManager:
    def __init__(self):
        self.users = {}
    
    def register_user(self, username, password):
        """Register a new user with hashed password"""
        if username in self.users:
            return False
        hashed_password = self.hash_password(password)
        self.users[username] = hashed_password
        return True
    
    def authenticate(self, username, password):
        """Verify user credentials"""
        if username not in self.users:
            return False
        return self.verify_password(password, self.users[username])
```

## Workflow Examples

### Example 1: Building a REST API Endpoint

**Step 1: Write the route definition**
```python
# Flask route to create a new blog post
@app.route('/api/posts', methods=['POST'])
def create_post():
    # Copilot suggests the implementation
```

**Step 2: Add validation**
```python
def validate_post_data(data):
    # Validate required fields for a blog post
    required_fields = ['title', 'content', 'author']
    # Copilot generates validation logic
```

**Step 3: Generate tests**
```python
# Test creating a new post
def test_create_post():
    # Copilot creates comprehensive tests
```

### Example 2: Data Analysis Script

```python
# Analyze sales data and generate insights
import pandas as pd
import matplotlib.pyplot as plt

def analyze_sales_data(csv_file):
    # Load data
    df = pd.read_csv(csv_file)
    
    # Calculate key metrics
    total_sales = df['amount'].sum()
    average_sale = df['amount'].mean()
    top_products = df.groupby('product')['amount'].sum().sort_values(ascending=False).head(5)
    
    # Generate visualizations
    plt.figure(figsize=(10, 6))
    top_products.plot(kind='bar')
    plt.title('Top 5 Products by Sales')
    plt.xlabel('Product')
    plt.ylabel('Total Sales')
    plt.tight_layout()
    plt.savefig('sales_analysis.png')
    
    return {
        'total_sales': total_sales,
        'average_sale': average_sale,
        'top_products': top_products.to_dict()
    }
```

## Interactive Features

### Using Copilot Chat

Ask questions directly:

- "How do I handle file uploads in Express.js?"
- "What's the best way to implement pagination?"
- "Explain this regex pattern"
- "Help me optimize this SQL query"

### Multiple Suggestions

Press `Ctrl+Enter` (Windows/Linux) or `Cmd+Enter` (Mac) to see alternative implementations.

## Practical Exercises

### Exercise 1: Todo List Manager

Create a command-line todo list application:

```python
# Todo list manager with add, remove, and list functions
class TodoList:
    # Implement initialization, add_task, remove_task, list_tasks
```

### Exercise 2: Data Validator

Build a flexible data validation system:

```javascript
// Create a validator that checks various data types and constraints
class DataValidator {
  // Implement validation rules and checking logic
}
```

### Exercise 3: Log Parser

Parse and analyze log files:

```python
# Parse server logs and extract error statistics
def parse_log_file(log_path):
    # Extract errors, warnings, and generate summary
```

## Best Practices

!!! success "Do This"
    - Write clear, descriptive comments
    - Use meaningful variable and function names
    - Provide type hints where possible
    - Review and test all generated code
    - Iterate on suggestions

!!! danger "Avoid This"
    - Blindly accepting all suggestions
    - Using vague or ambiguous comments
    - Skipping code review
    - Ignoring edge cases
    - Not testing generated code

## Keyboard Shortcuts

| Action | Windows/Linux | Mac |
|--------|---------------|-----|
| Accept suggestion | `Tab` | `Tab` |
| Reject suggestion | `Esc` | `Esc` |
| Next suggestion | `Alt+]` | `Option+]` |
| Previous suggestion | `Alt+[` | `Option+[` |
| Show all suggestions | `Ctrl+Enter` | `Cmd+Enter` |

## Next Steps

Now that you understand the practical foundations, learn about [Best Practices for Secure & Effective Copilot Coding](best-practices.md).
