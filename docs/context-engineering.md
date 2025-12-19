# Context Engineering & Prompting Techniques

Master the art of communicating effectively with GitHub Copilot through strategic context engineering and advanced prompting techniques.

## Understanding Context Engineering

Context engineering is the practice of structuring your code and comments to provide Copilot with the most relevant information for generating accurate suggestions.

### The Context Window

Copilot considers multiple sources of context:

1. **Current File**: The file you're working in
2. **Open Files**: Other files open in your editor
3. **Cursor Position**: Where you're typing
4. **Recent Edits**: Your recent changes
5. **Project Structure**: Your workspace organization

!!! tip "Context is King"
    The more relevant context you provide, the better Copilot's suggestions will be.

## Effective Prompting Strategies

### 1. Descriptive Comments

**Basic Prompt:**
```python
# sort function
def sort_data(data):
```

**Enhanced Prompt:**
```python
# Sort a list of user dictionaries by registration date (newest first)
# Handle None values and missing date fields by placing them at the end
# Expected input: [{"name": "John", "registered": "2024-01-15"}, ...]
# Returns: Sorted list of dictionaries
def sort_users_by_registration(users):
```

### 2. Type Hints and Signatures

**Without Types:**
```python
def process_data(data):
```

**With Types:**
```python
from typing import List, Dict, Optional
from datetime import datetime

def process_user_data(
    users: List[Dict[str, str]], 
    start_date: Optional[datetime] = None,
    include_inactive: bool = False
) -> List[Dict[str, any]]:
```

### 3. Example-Based Prompting

Provide examples of expected behavior:

```python
# Convert temperature between Celsius and Fahrenheit
# Examples:
# celsius_to_fahrenheit(0) -> 32
# celsius_to_fahrenheit(100) -> 212
# fahrenheit_to_celsius(32) -> 0
# fahrenheit_to_celsius(212) -> 100

def celsius_to_fahrenheit(celsius: float) -> float:
    # Copilot generates with example awareness
```

### 4. Constraint-Based Prompting

Specify constraints and requirements:

```javascript
// Function to validate email addresses
// Requirements:
// - Must contain exactly one @ symbol
// - Domain must have at least one dot
// - Local part must be 1-64 characters
// - Domain must be 1-255 characters
// - Cannot start or end with dots
// - No consecutive dots allowed

function isValidEmail(email) {
  // Copilot generates with all constraints
}
```

## Context Patterns

### Pattern 1: Top-of-File Documentation

```python
"""
User Management Module

This module handles user authentication and profile management.
Uses JWT for authentication, bcrypt for password hashing.
Follows REST API conventions with JSON responses.

Dependencies:
- Flask for web framework
- SQLAlchemy for database ORM
- PyJWT for token management

Author: Development Team
Last Updated: 2024-01-15
"""

# Subsequent code benefits from this context
```

### Pattern 2: Function Chains

```python
# Data processing pipeline
def load_data(filepath: str) -> pd.DataFrame:
    """Load CSV data with error handling"""
    # Implementation

def clean_data(df: pd.DataFrame) -> pd.DataFrame:
    """Remove duplicates, handle missing values, normalize formats"""
    # Implementation follows the pipeline context

def transform_data(df: pd.DataFrame) -> pd.DataFrame:
    """Apply business logic transformations"""
    # Copilot understands the flow

def save_results(df: pd.DataFrame, output_path: str) -> None:
    """Save processed data to specified location"""
    # Maintains context consistency
```

### Pattern 3: Class Hierarchies

```python
# Base class for all data processors
class BaseProcessor:
    """Abstract base class for data processors"""
    
    def validate(self, data):
        """Validate input data"""
        raise NotImplementedError
    
    def process(self, data):
        """Process the data"""
        raise NotImplementedError

# Concrete implementation for CSV processing
# Inherits validation and processing interface from BaseProcessor
# Adds CSV-specific parsing and transformation logic
class CSVProcessor(BaseProcessor):
    # Copilot understands inheritance and implements appropriately
```

## Advanced Prompting Techniques

### 1. Multi-Step Prompting

Break complex tasks into steps:

```python
# Step 1: Define data model
class UserProfile:
    """User profile with validation"""
    # Copilot generates model

# Step 2: Create CRUD operations
class UserProfileManager:
    """Manages user profile operations"""
    
    # Step 2a: Create operation
    def create_profile(self, user_data):
        """Create new user profile with validation"""
        # Implementation
    
    # Step 2b: Read operation
    def get_profile(self, user_id):
        """Retrieve user profile by ID"""
        # Implementation
    
    # Step 2c: Update operation
    def update_profile(self, user_id, updates):
        """Update existing profile with validation"""
        # Implementation
    
    # Step 2d: Delete operation
    def delete_profile(self, user_id):
        """Soft delete user profile"""
        # Implementation

# Step 3: Add search and filtering
def search_profiles(self, criteria):
    """Search profiles with multiple criteria"""
    # Copilot understands the context from previous steps
```

### 2. Context Inheritance

```typescript
// Context: E-commerce application using TypeScript and React
// Architecture: Redux for state management, React Router for navigation
// API: RESTful backend at /api/v1/

// Product interface used throughout the application
interface Product {
  id: string;
  name: string;
  price: number;
  category: string;
  inStock: boolean;
}

// Shopping cart component - uses Product interface
// Implements add, remove, update quantity functionality
// Calculates totals and applies discount codes
// Syncs with backend API on changes
interface ShoppingCartProps {
  // Copilot knows about Product from above
}

const ShoppingCart: React.FC<ShoppingCartProps> = () => {
  // Implementation inherits all the context
};
```

### 3. Pattern Recognition

Establish patterns for Copilot to follow:

```python
# API Endpoint Pattern:
# All endpoints follow this structure:
# 1. Validate request data
# 2. Check authentication/authorization
# 3. Perform business logic
# 4. Handle errors with proper status codes
# 5. Return standardized JSON response

@app.route('/api/users', methods=['POST'])
def create_user():
    """Create new user - follows API endpoint pattern"""
    # Copilot applies the pattern

@app.route('/api/users/<user_id>', methods=['GET'])
def get_user(user_id):
    """Get user details - follows API endpoint pattern"""
    # Pattern is maintained

@app.route('/api/users/<user_id>', methods=['PUT'])
def update_user(user_id):
    """Update user - follows API endpoint pattern"""
    # Consistency across endpoints
```

### 4. Negative Examples

Tell Copilot what NOT to do:

```javascript
// Function to sanitize user input for SQL queries
// DO NOT use string concatenation
// DO NOT trust user input directly
// DO use parameterized queries
// DO validate and sanitize all inputs

function sanitizeForSQL(input) {
  // Copilot avoids the anti-patterns mentioned
}
```

## Language-Specific Techniques

### Python

```python
# Use type hints and docstrings
from typing import List, Dict, Optional, Union
from dataclasses import dataclass

@dataclass
class Configuration:
    """Application configuration with validation"""
    host: str
    port: int
    debug: bool = False
    max_connections: int = 100
    
    def __post_init__(self):
        """Validate configuration after initialization"""
        # Copilot generates appropriate validation
```

### JavaScript/TypeScript

```typescript
// Use JSDoc or TypeScript types
/**
 * Fetches user data from the API
 * @param {string} userId - The unique user identifier
 * @param {Object} options - Fetch options
 * @param {boolean} options.includeProfile - Include profile data
 * @param {boolean} options.includePosts - Include user posts
 * @returns {Promise<User>} User object with requested data
 * @throws {APIError} When the request fails
 */
async function fetchUserData(
  userId: string,
  options: { includeProfile?: boolean; includePosts?: boolean }
): Promise<User> {
  // Well-documented function gets better suggestions
}
```

### Java

```java
/**
 * Service for managing user authentication and session management.
 * 
 * Uses JWT tokens for authentication with RS256 signing.
 * Tokens expire after 24 hours and refresh tokens after 7 days.
 * 
 * Thread-safe implementation using synchronized methods.
 * 
 * @author Development Team
 * @version 1.0
 * @since 2024-01-01
 */
public class AuthenticationService {
    // Copilot understands Java conventions and documentation
    
    /**
     * Authenticates a user with username and password.
     * 
     * @param username the username to authenticate
     * @param password the password to verify
     * @return JWT token if authentication successful
     * @throws AuthenticationException if credentials are invalid
     */
    public String authenticate(String username, String password) 
        throws AuthenticationException {
        // Implementation follows Javadoc conventions
    }
}
```

## Project-Wide Context

### 1. README Documentation

Create comprehensive README files:

```markdown
# Project Architecture

## Tech Stack
- Backend: Python/Flask
- Database: PostgreSQL
- Cache: Redis
- Queue: Celery
- Frontend: React/TypeScript

## Code Conventions
- Use snake_case for Python variables
- Use camelCase for JavaScript variables
- Maximum line length: 100 characters
- Use type hints in all Python functions
- Write docstrings for all public methods

## Error Handling
- Use custom exception classes
- Log all errors with context
- Return appropriate HTTP status codes
```

### 2. Configuration Files

```python
# config.py - centralized configuration
"""
Application configuration module.

All configuration values should be defined here.
Use environment variables for sensitive data.
Validate all configuration on startup.
"""

class Config:
    """Base configuration"""
    # Copilot understands project structure from this
```

### 3. Architectural Comments

```python
# architecture_notes.py
"""
System Architecture Notes

Data Flow:
1. Request → API Gateway → Route Handler
2. Route Handler → Business Logic Service
3. Business Logic → Data Access Layer
4. Data Access Layer → Database
5. Response ← formatted by Serializer

All layers follow dependency injection pattern.
"""
```

## Debugging with Context

### Providing Debug Context

```python
# Bug: Users are seeing duplicate entries in their order history
# Expected: Each order appears once
# Actual: Orders appear 2-3 times
# Reproduction: Place order, wait 5 minutes, check order history
# Hypothesis: Issue in order_history query or deduplication logic

def get_user_order_history(user_id):
    """
    Retrieve user's order history without duplicates
    Fix for issue #123: duplicate orders
    """
    # Copilot generates fix with bug context
```

## Iterative Refinement

### Start Broad, Then Narrow

```python
# Iteration 1: Basic structure
def process_payment(amount, method):
    """Process a payment"""
    pass

# Iteration 2: Add detail
def process_payment(amount: float, method: str) -> Dict:
    """
    Process payment through specified method
    Supports: credit_card, debit_card, paypal
    """
    pass

# Iteration 3: Full specification
def process_payment(
    amount: float,
    method: str,
    user_id: str,
    metadata: Optional[Dict] = None
) -> Dict[str, any]:
    """
    Process payment with full validation and error handling.
    
    Validates payment method, checks user limits, processes transaction,
    records in database, sends confirmation email.
    
    Returns transaction ID and status.
    Raises PaymentError for processing failures.
    """
    # Final, detailed implementation
```

## Context Anti-Patterns

### What to Avoid

!!! danger "Avoid These Patterns"
    1. **Vague comments**: "do something with data"
    2. **Inconsistent naming**: Using different conventions in same file
    3. **Missing types**: No type information in typed languages
    4. **Cluttered files**: Too many unrelated functions
    5. **No examples**: Abstract descriptions without concrete examples
    6. **Outdated comments**: Comments that don't match code

## Measuring Context Effectiveness

### Quality Indicators

Good context leads to:
- First suggestion is usually correct
- Suggestions match your style
- Less manual editing needed
- Appropriate error handling included
- Consistent with project patterns

Poor context results in:
- Multiple attempts needed
- Style mismatches
- Missing edge cases
- Inconsistent patterns

## Practical Exercises

### Exercise 1: Context Comparison

Compare these two approaches:

**Approach A:**
```python
def calc(x, y):
    pass
```

**Approach B:**
```python
def calculate_compound_interest(
    principal: float,
    rate: float,
    time: float,
    compounds_per_year: int = 12
) -> float:
    """
    Calculate compound interest using A = P(1 + r/n)^(nt)
    
    Args:
        principal: Initial investment amount
        rate: Annual interest rate (as decimal, e.g., 0.05 for 5%)
        time: Time period in years
        compounds_per_year: Number of times interest compounds per year
    
    Returns:
        Final amount after interest
        
    Example:
        >>> calculate_compound_interest(1000, 0.05, 2, 12)
        1104.94
    """
    pass
```

Which produces better suggestions?

### Exercise 2: Pattern Establishment

Create a consistent pattern for error handling across your project and observe how Copilot adapts.

## Next Steps

Put everything you've learned into practice with the [Putting it all together: Mini Project](mini-project.md).
