# Gemini CLI Complete Guide: Setup & Configuration

## What is Gemini CLI?

Gemini CLI is an open-source AI agent that runs directly in your terminal. It helps with coding tasks, file operations, and general queries. The tool comes with built-in features and supports MCP servers.

**Free Tier Benefits:**
- 60 requests per minute
- 1,000 requests per day (with personal Google account)

---

## Installation & Setup

### Requirements

- Node.js version 20 or higher

### Installation Steps

```bash
# Install Gemini CLI globally
npm install -g @google/gemini-cli

# Check version
gemini -v

# Upgrade to latest version
npm upgrade -g @google/gemini-cli
```

---

## First Launch

Start Gemini CLI:

```bash
gemini
```

### Initial Setup

1. **Choose Theme**: Select your preferred color theme
2. **Authentication**: Choose login method
   - **Google Login** (Recommended): Free tier access
   - **Gemini API Key**: For higher quota needs
   - **Vertex AI**: For Google Cloud projects

---

## Understanding the Interface


### Essential Commands

```bash
/help        # Show all commands and shortcuts
/docs        # Open documentation
/stats       # View session statistics
/tools       # List available tools
/quit        # Exit (or press Ctrl-C twice)
```

### Using Files in Context

Use `@` to reference files:
```
Explain @app.py
Update @README.md with installation steps
```

### Shell Mode

Toggle shell mode with `!` to run terminal commands:

```bash
!           # Enable shell mode
pwd         # Run commands
ESC         # Exit shell mode
```

---

## Command Line Options

### Version Check

```bash
gemini -v           # Check current version
gemini --version
```

### Model Selection

```bash
gemini -m "gemini-flash-2.5"    # Use Flash model
gemini -m "gemini-pro-2.5"      # Use Pro model
```

**Note**: Free tier may auto-switch to Flash due to quota limits.

### Single Prompt Mode

Run without interactive interface:

```bash
# Using prompt parameter
gemini -p "What is the gcloud command to deploy to Cloud Run"

# Using positional prompt (preferred)
gemini "What is the gcloud command to deploy to Cloud Run"
```

### Debug Mode

See detailed execution information:

```bash
gemini -d                       # Launch with debug
gemini -d -p "your prompt"      # Debug with single prompt
```

Debug mode shows:
- Authentication method
- GEMINI.md file search paths
- Context loading process
- Memory usage

### Session Summary

Save session metrics to file:

```bash
gemini --session-summary "session.txt"
```

Tracks:
- Model usage
- API calls
- Token consumption
- Tool usage statistics

### YOLO Mode (Use Carefully!)

Auto-accept all actions:

```bash
gemini -y
gemini --yolo
```

**Warning**: This automatically approves file writes and other operations.

---

## Working with GEMINI.md Files

### Purpose

`GEMINI.md` files provide instructions to the AI about:
- Coding style preferences
- Project-specific rules
- Framework versions
- Dependencies management

### File Hierarchy

Context loads in this order (specific overrides general):

1. **Global**: `~/.gemini/GEMINI.md` - Rules for all projects
2. **Project Root**: Project-wide instructions
3. **Local**: Subdirectory-specific rules

### View Current Context

```bash
/memory show        # Display loaded context
/memory refresh     # Reload GEMINI.md files
```

### Example GEMINI.md

```markdown
# Project Guidelines

## Code Style
- Use TypeScript strict mode
- Follow ESLint rules
- 2-space indentation

## Dependencies
- React 18.x
- Node.js 20+

## Testing
- Write tests for all functions
- Use Jest framework
```

---

## Built-in Tools

View available tools:

```bash
/tools
```

Common tools include:
- **GoogleSearch**: Search the web
- **ReadFile**: Read file contents
- **WriteFile**: Create/modify files
- **mkdir**: Create directories
- **Shell**: Execute terminal commands

**Tool Permissions**: Gemini CLI asks before using tools. Options:
- Allow once
- Always allow
- Reject
- Modify and allow

---

## Project Structure Best Practices

### Start from Project Folder

Always launch Gemini CLI from your project directory:

```bash
cd ~/my-projects/current-project
gemini
```

---

## Practical Example: Building a Web App

### Task: Cricket Score Viewer

**Prompt:**
```
Create a Python Flask application that displays live cricket scores from this RSS feed:
https://static.cricinfo.com/rss/livescores.xml
```

**What Happens:**
1. Gemini CLI asks permission to create folders
2. Generates Python code and HTML templates
3. Identifies dependencies (Flask, requests, feedparser)
4. Asks to install packages
5. Starts Flask server
6. Handles port conflicts automatically

**Result**: Working web application with minimal input.

---

## Tips & Best Practices

### DO:
- Launch from your project directory
- Review tool permissions before accepting
- Use GEMINI.md for consistent results
- Enable checkpointing for safety
- Keep Gemini CLI updated

### DON'T:
- Run from home directory
- Use YOLO mode by default
- Ignore tool permission prompts
- Skip updating regularly

---

## Common Workflows

### Quick Terminal Help
```bash
gemini "show me git commands for rebasing"
```

### Generate Code
```bash
cd my-project
gemini
> Create a REST API with user authentication
```

### Modify Existing Files
```bash
gemini
> In @app.py, add error handling to all functions
```

### Restore Previous State
```bash
gemini -c
> (make changes)
> /restore
> (select checkpoint to restore)
```

---

## Troubleshooting

### Model Switches to Flash
**Issue**: Pro model auto-switches to Flash  
**Solution**: Use Gemini API Key for higher quota

### No Context Loading
**Issue**: GEMINI.md not found  
**Solution**: Check file location with `gemini -d`

### Port Already in Use
**Issue**: Server won't start  
**Solution**: Ask Gemini to use different port

---

## Next Steps

This guide covers installation, configuration, and basic usage. Upcoming topics:
- Configuration files (settings.json, .env)
- MCP server integration
- Custom slash commands
- VS Code integration
- Advanced context management

---

## Quick Reference

```bash
# Installation
npm install -g @google/gemini-cli

# Launch
gemini                          # Interactive mode
gemini "prompt"                 # Single prompt
gemini -m "model"               # Choose model
gemini -c                       # With checkpointing
gemini -d                       # Debug mode

# Inside CLI
/help                           # Show commands
/tools                          # List tools
/memory show                    # View context
/restore                        # Restore checkpoint
/quit                           # Exit
!                               # Shell mode
@filename                       # Reference file
```

---

**Pro Tip**: Start small, experiment with simple tasks, and gradually add GEMINI.md instructions as you learn what works best for your workflow.