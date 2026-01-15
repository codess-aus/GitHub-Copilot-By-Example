# Setup

Get started with GitHub Copilot by installing and configuring it in your development environment.

## Prerequisites

Before you begin, ensure you have:

- **GitHub Account**: A GitHub account with Copilot access
- **Subscription**: GitHub Copilot Individual, Business, or Enterprise subscription
- **Supported IDE**: Visual Studio Code, Visual Studio, JetBrains IDEs, or Neovim

## Installation Steps

### Visual Studio Code

1. **Install the Extension**
   - Open Visual Studio Code
   - Go to Extensions (Ctrl+Shift+X / Cmd+Shift+X)
   - Search for "GitHub Copilot"
   - Click "Install"

2. **Sign In to GitHub**
   - Click the GitHub icon in the status bar
   - Follow the authentication prompts
   - Authorize GitHub Copilot

3. **Verify Installation**
   - Open a new file
   - Start typing code
   - Look for gray suggestion text from Copilot

### Visual Studio

1. **Install the Extension**
   - Open Visual Studio
   - Go to Extensions → Manage Extensions
   - Search for "GitHub Copilot"
   - Download and install

2. **Restart Visual Studio**
   - Close and reopen Visual Studio
   - Sign in with your GitHub account

### JetBrains IDEs

1. **Install the Plugin**
   - Go to File → Settings → Plugins (Windows/Linux)
   - Or IntelliJ IDEA → Preferences → Plugins (macOS)
   - Search for "GitHub Copilot"
   - Install and restart the IDE

2. **Authenticate**
   - Follow the in-IDE prompts to sign in
   - Authorize the plugin

## Configuration

### Basic Settings

Configure GitHub Copilot to match your preferences:

```json
{
  "github.copilot.enable": {
    "*": true,
    "yaml": false,
    "plaintext": false
  },
  "github.copilot.editor.enableAutoCompletions": true
}
```

### Advanced Settings

!!! tip "Customization"
    Adjust Copilot's behavior for different file types and languages through your IDE settings.

## Verify Your Setup

Test your installation:

1. Create a new file (e.g., `test.py`, `test.js`)
2. Write a comment describing a function
3. Press Enter and wait for suggestions
4. Accept a suggestion with Tab

!!! success "Setup Complete!"
    If you see code suggestions, you're ready to start coding with GitHub Copilot!

## Troubleshooting

### Common Issues

**Not Seeing Suggestions?**
- Verify your subscription is active
- Check that Copilot is enabled in settings
- Restart your IDE

**Authentication Failed?**
- Clear browser cookies and try again
- Check your GitHub account permissions
- Ensure you're using the correct GitHub account

**Slow Suggestions?**
- Check your internet connection
- Verify firewall/proxy settings
- Try restarting your IDE

## Next Steps

Now that you have GitHub Copilot set up, proceed to [Copilot Deep Dive: Concepts & Capabilities](copilot-deep-dive.md) to learn about its features and how it works.
