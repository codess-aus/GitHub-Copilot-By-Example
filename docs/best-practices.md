<div class="hero-section">
  <img src="images/best-practices-hero.jpg" alt="Best Practices" onerror="this.style.display='none'">
  <div class="hero-overlay">
    <h1>Best Practices for Secure & Effective Coding</h1>
  </div>
</div>

Learn how to use GitHub Copilot responsibly while maintaining code quality, security, and best practices.

## Code Quality Principles

### 1. Always Review Generated Code

!!! warning "Never Trust Blindly"
    Copilot is a tool, not a replacement for your judgment. Always review, understand, and test generated code.

**Review Checklist:**
- [ ] Logic correctness
- [ ] Edge case handling
- [ ] Error handling
- [ ] Performance implications
- [ ] Security concerns
- [ ] Code style consistency

### 2. Test Everything

```python
# Always write tests for Copilot-generated code
def test_user_authentication():
    # Test valid credentials
    assert authenticate_user("valid_user", "correct_password") == True
    
    # Test invalid credentials
    assert authenticate_user("valid_user", "wrong_password") == False
    
    # Test edge cases
    assert authenticate_user("", "") == False
    assert authenticate_user(None, None) == False
```

### 3. Maintain Code Standards

Ensure generated code follows your project's:
- Naming conventions
- Code style guidelines
- Architecture patterns
- Documentation standards

## Security Best Practices

### 1. Validate Input

Always validate and sanitize user input:

```python
# Good: Input validation
def process_user_input(user_data):
    # Validate data before processing
    if not isinstance(user_data, dict):
        raise ValueError("Invalid input format")
    
    # Sanitize strings
    username = user_data.get('username', '').strip()
    if not username or len(username) > 50:
        raise ValueError("Invalid username")
    
    # Continue with validated data
    return process_validated_data(username)
```

```python
# Bad: No validation
def process_user_input(user_data):
    # Directly using user input is dangerous
    username = user_data['username']
    return process_data(username)
```

### 2. Avoid Hardcoded Secrets

```python
# Bad: Hardcoded credentials
API_KEY = "sk-1234567890abcdef"

# Good: Environment variables
import os
API_KEY = os.getenv('API_KEY')
if not API_KEY:
    raise ValueError("API_KEY environment variable not set")
```

### 3. SQL Injection Prevention

```python
# Bad: String concatenation
def get_user(username):
    query = f"SELECT * FROM users WHERE username = '{username}'"
    return db.execute(query)

# Good: Parameterized queries
def get_user(username):
    query = "SELECT * FROM users WHERE username = ?"
    return db.execute(query, (username,))
```

### 4. XSS Prevention

```javascript
// Bad: Unsafe HTML insertion
function displayMessage(message) {
  document.getElementById('output').innerHTML = message;
}

// Good: Text content or sanitization
function displayMessage(message) {
  document.getElementById('output').textContent = message;
  // Or use a sanitization library
}
```

### 5. Authentication & Authorization

```python
# Implement proper authentication checks
from functools import wraps

def require_authentication(f):
    @wraps(f)
    def decorated_function(*args, **kwargs):
        if not is_authenticated():
            return redirect('/login')
        return f(*args, **kwargs)
    return decorated_function

@app.route('/admin')
@require_authentication
def admin_panel():
    # Protected route
    pass
```

## Performance Best Practices

### 1. Optimize Algorithms

```python
# Less efficient: O(n²)
def find_duplicates(arr):
    duplicates = []
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):
            if arr[i] == arr[j] and arr[i] not in duplicates:
                duplicates.append(arr[i])
    return duplicates

# More efficient: O(n)
def find_duplicates(arr):
    seen = set()
    duplicates = set()
    for item in arr:
        if item in seen:
            duplicates.add(item)
        seen.add(item)
    return list(duplicates)
```

### 2. Resource Management

```python
# Good: Context managers for resource handling
def process_file(filename):
    with open(filename, 'r') as file:
        data = file.read()
        # File automatically closed
        return process_data(data)
```

### 3. Caching

```python
from functools import lru_cache

@lru_cache(maxsize=128)
def expensive_calculation(n):
    # Cache results for better performance
    if n <= 1:
        return n
    return expensive_calculation(n-1) + expensive_calculation(n-2)
```

## Error Handling

### 1. Specific Exception Handling

```python
# Good: Specific exceptions
def read_config_file(path):
    try:
        with open(path, 'r') as f:
            return json.load(f)
    except FileNotFoundError:
        logger.error(f"Config file not found: {path}")
        return default_config()
    except json.JSONDecodeError as e:
        logger.error(f"Invalid JSON in config: {e}")
        return default_config()
    except Exception as e:
        logger.error(f"Unexpected error reading config: {e}")
        raise
```

### 2. Graceful Degradation

```python
def get_user_recommendations(user_id):
    try:
        # Try ML-based recommendations
        return ml_recommender.get_recommendations(user_id)
    except Exception as e:
        logger.warning(f"ML recommender failed: {e}")
        # Fall back to simple recommendations
        return simple_recommender.get_recommendations(user_id)
```

## Documentation Practices

### 1. Clear Function Documentation

```python
def calculate_shipping_cost(weight, distance, express=False):
    """
    Calculate shipping cost based on package weight and distance.
    
    Args:
        weight (float): Package weight in kilograms
        distance (float): Shipping distance in kilometers
        express (bool, optional): Whether to use express shipping. Defaults to False.
    
    Returns:
        float: Calculated shipping cost in dollars
    
    Raises:
        ValueError: If weight or distance is negative
    
    Examples:
        >>> calculate_shipping_cost(2.5, 100)
        15.50
        >>> calculate_shipping_cost(2.5, 100, express=True)
        25.50
    """
    if weight < 0 or distance < 0:
        raise ValueError("Weight and distance must be non-negative")
    
    base_cost = weight * 2 + distance * 0.1
    return base_cost * 1.5 if express else base_cost
```

### 2. Inline Comments for Complex Logic

```python
def process_complex_algorithm(data):
    # Phase 1: Normalize data to 0-1 range
    normalized = [(x - min(data)) / (max(data) - min(data)) for x in data]
    
    # Phase 2: Apply weighted transformation
    weights = [0.3, 0.5, 0.2]  # Importance factors
    weighted = [n * w for n, w in zip(normalized, weights)]
    
    # Phase 3: Aggregate results
    return sum(weighted)
```

## License Compliance

### Be Aware of Licensing

!!! info "License Considerations"
    - Copilot may suggest code from various sources
    - Review suggestions for recognizable copyrighted patterns
    - Ensure compliance with your project's license
    - Check your organization's policies

### Attribution

When using significant code patterns:
- Add comments noting the origin if known
- Follow your organization's attribution guidelines

## Code Review Integration

### 1. Treat Copilot Code Like Any Other Code

- Request peer reviews
- Run automated checks
- Perform security scans
- Test thoroughly

### 2. Document Copilot Usage

```python
# Generated with GitHub Copilot assistance and reviewed
def complex_data_transformation(input_data):
    # Implementation details...
    pass
```

## Anti-Patterns to Avoid

!!! danger "Common Mistakes"
    1. **Accepting without understanding** - Always understand what the code does
    2. **Skipping tests** - Copilot code needs testing too
    3. **Ignoring security** - Don't assume generated code is secure
    4. **Copy-paste mentality** - Adapt suggestions to your needs
    5. **Not refactoring** - Generated code may need improvement

## Continuous Improvement

### 1. Learn from Suggestions

Study Copilot's suggestions to learn new patterns and techniques.

### 2. Provide Feedback

Use the feedback mechanism to report:
- Incorrect suggestions
- Security issues
- Helpful suggestions

### 3. Stay Updated

- Follow GitHub Copilot updates
- Review new features and capabilities
- Adjust your workflow accordingly

## Team Guidelines

### Establish Team Standards

1. **When to use Copilot**: Define appropriate use cases
2. **Review requirements**: Set code review standards
3. **Testing expectations**: Require tests for generated code
4. **Security policies**: Define security review processes

### Share Knowledge

- Document effective prompting techniques
- Share useful patterns and examples
- Conduct training sessions

## Daily Workflows with Copilot

Integrate Copilot into your real-world development workflows for maximum productivity.

### Starting Your Day

**Morning Workflow:**

1. **Review PRs with Copilot**
   ```
   # In PR review, use Copilot Chat:
   "Summarize the changes in this PR"
   "What are potential issues with this implementation?"
   "Suggest improvements for this code"
   ```

2. **Check Issues and Plan**
   ```
   # Use Agent Mode to break down issues:
   "Analyze issue #123 and suggest implementation approach"
   "What files need to be modified for this feature?"
   ```

3. **Update Your Branch**
   ```bash
   git pull origin main
   # Use Copilot Chat for merge conflicts:
   "Explain this merge conflict and suggest resolution"
   ```

### Working on Features

**Development Workflow:**

1. **Scaffold the Feature** (Agent Mode)
   ```
   "Create a user profile editing feature with:
   - API endpoints
   - Validation
   - Tests
   - Documentation"
   ```

2. **Implement Details** (Inline Suggestions)
   - Let suggestions guide implementation
   - Accept and modify as needed
   - Keep context clear with comments

3. **Write Tests** (Copilot Chat)
   ```
   Select function → "/tests"
   "Generate edge case tests for this function"
   ```

4. **Document** (Inline Suggestions)
   ```python
   def complex_function(data, options):
       """
       # Copilot generates comprehensive docstring
   ```

### Debugging Sessions

**When Things Break:**

1. **Understand the Error**
   ```
   # Copy error to Copilot Chat:
   "Explain this error: TypeError: cannot read property 'id' of undefined"
   ```

2. **Find the Root Cause**
   ```
   "Analyze this function and identify potential null pointer issues"
   ```

3. **Generate Fix**
   ```
   "Suggest a fix for this race condition"
   ```

4. **Add Safeguards**
   ```
   "Add error handling to prevent this issue"
   ```

### Code Review Workflow

**Reviewing Others' Code:**

1. **Understand Changes**
   ```
   "Summarize what this PR does"
   "Explain this algorithm"
   ```

2. **Check for Issues**
   ```
   "What security concerns exist in this code?"
   "Are there any performance issues?"
   "Check for edge cases not handled"
   ```

3. **Suggest Improvements**
   ```
   "How could this be more efficient?"
   "Suggest better variable names"
   ```

**Being Reviewed:**

- Use Copilot to pre-review your own code
- Generate comprehensive PR descriptions
- Add inline comments explaining complex logic

### Refactoring Sessions

**Improving Existing Code:**

1. **Analyze Current State**
   ```
   "What are the problems with this implementation?"
   "How can this be more maintainable?"
   ```

2. **Plan Refactoring**
   ```
   "Suggest a refactoring approach for this module"
   "What design pattern would work better here?"
   ```

3. **Execute Safely**
   - Use Agent Mode for multi-file refactoring
   - Write tests first
   - Refactor incrementally

4. **Verify**
   ```
   "Generate comprehensive tests for the refactored code"
   ```

### Working with Legacy Code

**Understanding Old Code:**

1. **Get Context**
   ```
   "Explain what this legacy function does"
   "What are the dependencies of this module?"
   ```

2. **Plan Updates**
   ```
   "How can I modernize this code safely?"
   "Suggest a migration path to the new API"
   ```

3. **Add Tests**
   ```
   "Generate characterization tests for this legacy code"
   ```

### Integrating into Existing Projects

**Adding Copilot to Current Work:**

1. **Start Small**
   - Use Inline suggestions for new code
   - Try Chat for understanding existing code
   - Avoid Agent Mode on unfamiliar codebase initially

2. **Learn Project Patterns**
   ```python
   # Add context comments to teach Copilot your patterns:
   """
   Project Convention: All API responses use this format:
   {
       "success": bool,
       "data": any,
       "error": Optional[str]
   }
   """
   ```

3. **Gradually Increase Usage**
   - Week 1: Inline suggestions only
   - Week 2: Add Chat for questions
   - Week 3: Use Agent Mode for new features

### Team Collaboration

**Working with Team Members:**

1. **Share Effective Prompts**
   ```markdown
   # Team Wiki: Effective Copilot Prompts
   - For API endpoints: "Create a {METHOD} endpoint for {resource} with validation and error handling"
   - For tests: "Generate tests for {function} covering happy path and edge cases"
   ```

2. **Establish Standards**
   - Always review Copilot suggestions
   - Require tests for generated code
   - Document Copilot-generated scaffolding

3. **Pair Programming with Copilot**
   - Use Copilot Chat during pair sessions
   - Discuss suggestions together
   - Learn from each other's prompting

### Production Deployment Workflow

**Shipping Copilot-Assisted Code:**

1. **Pre-Deployment Checklist**
   ```
   # Use Copilot Chat to review:
   "Check this code for security issues"
   "Verify error handling is comprehensive"
   "Confirm all edge cases are covered"
   ```

2. **Generate Deployment Docs**
   ```
   "Create deployment documentation for this feature"
   "List configuration requirements"
   ```

3. **Monitor and Iterate**
   - Use Copilot to quickly fix issues
   - Generate hotfix tests
   - Document lessons learned

### Time Management

**Typical Day Breakdown:**

- **Planning (15 min)**: Use Agent Mode to break down tasks
- **Implementation (3-4 hours)**: Inline suggestions + Chat
- **Testing (1 hour)**: Chat for test generation
- **Code Review (1 hour)**: Chat for reviewing others' code
- **Documentation (30 min)**: Inline suggestions for docs
- **Bug Fixes (variable)**: Chat for debugging

### Efficiency Tips

!!! success "Maximize Productivity"
    - **Keep context files open**: Copilot learns from open files
    - **Write clear comments first**: Better suggestions follow
    - **Use keyboard shortcuts**: Accept/reject suggestions quickly
    - **Batch similar tasks**: Context stays consistent
    - **Take breaks**: Copilot works better with fresh context

!!! tip "Daily Habits"
    - Start with most complex task (Agent Mode)
    - Use Chat when stuck (don't waste time)
    - Review suggestions critically (maintain quality)
    - Share learnings with team (improve together)

### Common Workflow Patterns

**Pattern 1: Feature Development**
```
1. Agent Mode: Scaffold structure
2. Inline: Implement business logic
3. Chat: Generate tests
4. Chat: Document
5. Inline: Refine and polish
```

**Pattern 2: Bug Fix**
```
1. Chat: Understand the bug
2. Inline: Implement fix
3. Chat: Generate regression test
4. Inline: Add error handling
```

**Pattern 3: Code Review**
```
1. Chat: Summarize changes
2. Chat: Check for issues
3. Inline: Suggest improvements
4. Chat: Verify fix approaches
```

## Compliance Checklist

Before committing Copilot-generated code:

- [ ] Code reviewed and understood
- [ ] Tests written and passing
- [ ] Security review completed
- [ ] No hardcoded secrets
- [ ] Input validation present
- [ ] Error handling implemented
- [ ] Documentation added
- [ ] License compliance verified
- [ ] Performance acceptable
- [ ] Code style consistent

## Next Steps

Explore advanced features in [Advanced Copilot: Agent Mode, Integrations, Extensions](advanced-copilot.md).
