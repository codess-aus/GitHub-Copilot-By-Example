<div class="hero-section">
  <img src="images/advanced-hero.jpg" alt="Advanced Copilot" onerror="this.style.display='none'">
  <div class="hero-overlay">
    <h1>Advanced Copilot: Agent Mode, Integrations, Extensions</h1>
  </div>
</div>

Explore advanced features of GitHub Copilot including agent mode, integrations with development tools, and extensions.

## When to Use What: Choosing the Right Copilot Tool

Understanding when to use each Copilot feature is crucial for maximizing productivity.

### Decision Framework

```
Simple completion needed?
├─ Yes → Use Inline Suggestions
└─ No → Need explanation or multi-step?
    ├─ Quick question → Use Copilot Chat
    └─ Complex task → Use Agent Mode
```

### Inline Suggestions

**Best For:**
- Completing current line or function
- Implementing well-defined patterns
- Generating boilerplate code
- Quick autocomplete-style assistance

**When to Use:**
- You know exactly what you need
- Writing standard implementations
- Following established patterns
- Speed is priority

**Example Scenarios:**
```python
# Writing standard CRUD operations
def get_user_by_id(user_id):
    # Inline suggestion completes the query
```

```javascript
// Implementing common patterns
async function fetchData(url) {
    // Suggestion provides try-catch with fetch
}
```

### Copilot Chat

**Best For:**
- Understanding existing code
- Getting explanations
- Exploring different approaches
- Quick refactoring suggestions
- Debugging help
- Generating tests for specific code

**When to Use:**
- You need to understand something
- Exploring implementation options
- Need explanation of errors
- Want multiple approaches
- Reviewing code sections

**Example Scenarios:**
- "Explain how this authentication middleware works"
- "What's the time complexity of this algorithm?"
- "Suggest a more efficient way to implement this"
- "Generate unit tests for this function"
- "Why might this code cause a memory leak?"

### Agent Mode

**Best For:**
- Multi-file operations
- Scaffolding entire features
- Complex refactoring across files
- Architectural implementations
- End-to-end feature development

**When to Use:**
- Building complete features
- Need changes across multiple files
- Implementing complex workflows
- Setting up new components
- Large-scale refactoring

**Example Scenarios:**
- "Create a REST API with user authentication"
- "Add a payment processing system"
- "Refactor this to use dependency injection"
- "Implement caching across the application"
- "Set up a new microservice with logging"

### Comparison Table

| Feature | Speed | Scope | Context | Best Use Case |
|---------|-------|-------|---------|---------------|
| **Inline** | ⚡⚡⚡ Fast | Single line/block | Current file | Quick completions |
| **Chat** | ⚡⚡ Medium | File/concept | Current selection + workspace | Questions & exploration |
| **Agent** | ⚡ Slower | Multi-file/system | Entire workspace | Complex features |

### Workflow Integration

**Typical Development Flow:**

1. **Starting a new feature** → Use Agent Mode to scaffold structure
2. **Implementing details** → Use Inline Suggestions for code
3. **Stuck on logic** → Use Chat to explore approaches
4. **Writing tests** → Use Chat to generate test cases
5. **Refining code** → Use Inline for adjustments

### Best Practices

!!! tip "Combine Tools Effectively"
    - Start with Agent Mode for structure
    - Use Inline for implementation
    - Use Chat when you need to think through problems
    - Don't be afraid to switch between tools

!!! warning "Avoid Tool Misuse"
    - Don't use Agent Mode for simple completions (overkill)
    - Don't rely only on Inline for complex logic (insufficient)
    - Don't use Chat for everything (slower workflow)

## Copilot Agent Mode

### What is Agent Mode?

Agent mode allows Copilot to take a more proactive role in your development workflow by:
- Suggesting entire workflows
- Performing multi-step operations
- Understanding complex contexts
- Proposing architectural improvements

### Using Copilot Chat

Copilot Chat provides an interactive interface for:

**Code Explanation:**
```
User: Explain how this authentication middleware works
Copilot: This middleware checks for a valid JWT token in the request headers...
```

**Code Generation:**
```
User: Create a REST API endpoint for user registration with validation
Copilot: [Generates complete endpoint with validation, error handling, and tests]
```

**Debugging Assistance:**
```
User: Why is this function returning undefined?
Copilot: The function returns undefined because...
```

### Slash Commands

Use specialized commands in Copilot Chat:

- `/explain` - Explain selected code
- `/fix` - Suggest fixes for problems
- `/tests` - Generate test cases
- `/help` - Get help with Copilot
- `/clear` - Clear chat history

### Workspace Context

Copilot Chat can understand your entire workspace:

```
User: How does the authentication system work across the application?
Copilot: [Analyzes multiple files and provides architectural overview]
```

## IDE Integrations

### Visual Studio Code

#### Advanced Features

**1. Inline Chat**
- Press `Ctrl+I` / `Cmd+I` to open inline chat
- Ask questions without leaving your code
- Get suggestions directly in the editor

**2. Quick Actions**
- Right-click on code → Copilot options
- Generate docs, tests, or explanations
- Refactor or optimize selected code

**3. Terminal Integration**
```bash
# Explain shell commands
git rebase -i HEAD~3  # Copilot explains: Interactive rebase last 3 commits
```

#### Extension Settings

```json
{
  "github.copilot.enable": {
    "*": true,
    "markdown": true,
    "yaml": true
  },
  "github.copilot.advanced": {
    "debug.overrideEngine": "default",
    "debug.testOverrideProxyUrl": "",
    "debug.overrideProxyUrl": ""
  }
}
```

### Visual Studio

**Features:**
- IntelliCode integration
- Whole line completions
- Multi-line suggestions
- Copilot Chat in sidebar

**Keyboard Shortcuts:**
- `Alt+/` - Trigger Copilot suggestion
- `Alt+.` - Next suggestion
- `Alt+,` - Previous suggestion

### JetBrains IDEs

**Supported IDEs:**
- IntelliJ IDEA
- PyCharm
- WebStorm
- Rider
- And more

**Features:**
- Smart completion integration
- Language-specific optimizations
- Debugging assistance
- Refactoring support

## GitHub Integration

### Copilot in Pull Requests

Generate PR descriptions:
```markdown
# PR: Add user authentication

Copilot can help generate:
- Summary of changes
- Testing instructions
- Related issues
- Breaking changes
```

### Copilot in Issues

Use Copilot to:
- Suggest implementation approaches
- Generate code examples
- Propose architectures
- Estimate complexity

### Code Review Assistance

```
User: Review this security implementation
Copilot: Here are potential security concerns:
1. SQL injection risk in query construction
2. Missing input validation on user_id parameter
3. Consider adding rate limiting
```

## CLI Integration

### GitHub CLI with Copilot

```bash
# Install GitHub CLI with Copilot extension
gh extension install github/gh-copilot

# Use Copilot in terminal
gh copilot suggest "how to find large files in git history"
gh copilot explain "git rebase -i HEAD~5"
```

### Common CLI Use Cases

**1. Git Commands:**
```bash
# Ask for git help
gh copilot suggest "undo last commit but keep changes"
# Suggests: git reset --soft HEAD~1
```

**2. System Administration:**
```bash
# Get shell command suggestions
gh copilot suggest "find all python files modified in last week"
# Suggests: find . -name "*.py" -mtime -7
```

**3. DevOps Tasks:**
```bash
# Docker command assistance
gh copilot explain "docker-compose up -d"
```

## Neovim Integration

### Setup Copilot in Neovim

```lua
-- Install with vim-plug
Plug 'github/copilot.vim'

-- Configuration
vim.g.copilot_no_tab_map = true
vim.api.nvim_set_keymap("i", "<C-J>", 'copilot#Accept("<CR>")', { silent = true, expr = true })
```

### Neovim Features

- Asynchronous suggestions
- Custom keybindings
- Integration with LSP
- Terminal support

## API and Custom Integrations

### Copilot for Business

Enterprise features:
- Organization-wide settings
- Usage analytics
- Policy controls
- SSO integration

### Custom Extensions

Build custom tools with Copilot:

```javascript
// Example: Custom linting with Copilot suggestions
async function lintWithCopilot(code) {
  const suggestions = await copilot.suggest(code, {
    context: 'linting',
    rules: projectRules
  });
  return suggestions;
}
```

## Advanced Prompting Techniques

### Context Priming

Provide rich context in comments:

```python
# Context: This is a Django REST API endpoint
# Requirements: 
# - Support pagination (page size: 20)
# - Filter by status and date
# - Include related objects
# - Handle authentication
# - Rate limit: 100 requests/hour

@api_view(['GET'])
def get_user_orders(request, user_id):
    # Copilot generates comprehensive implementation
```

### Multi-File Context

```python
# File: models.py
class User:
    """User model with authentication"""

# File: serializers.py  
# Create a serializer for the User model with all fields except password
class UserSerializer:
    # Copilot understands the User model from models.py
```

### Pattern Libraries

Create reusable patterns:

```typescript
// Pattern: Error boundary component
// This pattern should be used for all route components
export class ErrorBoundary extends React.Component {
  // Copilot learns your patterns
}
```

## Copilot Labs

### Experimental Features

!!! info "Copilot Labs"
    GitHub Copilot Labs offers experimental features:
    - Explain code
    - Translate code
    - Brushes (code modifications)
    - Test generation

### Code Brushes

Transform code with specific intents:
- Make code more readable
- Add types
- Fix bugs
- Improve performance
- Add error handling

## Integration with CI/CD

### Pre-commit Hooks

```bash
# Use Copilot to generate tests before commit
#!/bin/bash
if [ "$COPILOT_GENERATE_TESTS" = "true" ]; then
  # Trigger test generation
  gh copilot suggest "generate tests for modified files"
fi
```

### Automated Code Review

```yaml
# GitHub Actions workflow
name: Copilot Code Review
on: [pull_request]
jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Copilot Review
        run: |
          # Use Copilot API for automated review
```

## Team Collaboration

### Shared Patterns

Document team patterns for Copilot:

```python
# Team Pattern: API Response Format
# Always return responses in this format:
# {
#   "status": "success" | "error",
#   "data": {...},
#   "message": "...",
#   "timestamp": "ISO-8601"
# }

def api_response(status, data=None, message=""):
    # Copilot will follow this pattern
```

### Code Style Enforcement

```javascript
// Team convention: Use arrow functions for React components
// Copilot adapts to your style

const UserProfile = ({ user }) => {
  // Component implementation
};
```

## Performance Optimization

### Copilot Performance Settings

Optimize Copilot's responsiveness:

```json
{
  "github.copilot.editor.enableAutoCompletions": true,
  "editor.inlineSuggest.enabled": true,
  "editor.quickSuggestions": {
    "other": true,
    "comments": true,
    "strings": true
  }
}
```

### Network Optimization

- Use proxy settings for restricted networks
- Configure timeouts appropriately
- Cache suggestions when possible

## Advanced Use Cases

### 1. Microservices Architecture

Generate service boilerplate:
```
User: Create a microservice for order processing with message queue
Copilot: [Generates service structure, queue handling, API endpoints]
```

### 2. Database Migrations

```python
# Generate Alembic migration for adding user profile fields
def upgrade():
    # Copilot generates migration code
```

### 3. Infrastructure as Code

```hcl
# Create Terraform configuration for AWS ECS cluster with auto-scaling
resource "aws_ecs_cluster" "main" {
  # Copilot generates complete Terraform config
}
```

### 4. Test Automation

```python
# Generate comprehensive E2E test suite for checkout flow
class TestCheckoutFlow(unittest.TestCase):
    # Copilot creates complete test scenarios
```

## Troubleshooting Advanced Features

### Common Issues

**Chat Not Responding:**
- Check internet connection
- Verify subscription status
- Clear chat history
- Restart IDE

**Slow Suggestions:**
- Reduce workspace size
- Close unnecessary files
- Check network latency
- Update Copilot extension

**Context Issues:**
- Ensure files are saved
- Check workspace structure
- Verify file associations
- Review .gitignore

## Future Capabilities

Stay informed about upcoming features:
- Enhanced multi-file awareness
- Better architectural suggestions
- Improved refactoring capabilities
- Advanced debugging assistance

## Next Steps

Master the art of effective communication with Copilot in [Context Engineering & Prompting Techniques](context-engineering.md).
