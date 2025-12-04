# GitHub Repository Creation Guide for AI Agents

This document provides step-by-step instructions for AI agents to create GitHub repositories using the GitHub CLI (gh).

## Prerequisites

Before creating a repository, verify the following:

### 1. Check GitHub CLI Authentication

```bash
gh auth status
```

**Expected output:**
- Should show logged in status
- Should display the authenticated account name
- Should show active account: true

**If not authenticated:**
```bash
gh auth login
```

## Repository Creation Process

### Step 1: Decide on Repository Details

Gather the following information:
- **Repository name**: Choose a clear, descriptive name (lowercase, hyphens for spaces)
- **Description**: Brief description of the repository's purpose
- **Visibility**: Public or Private
- **Initialize with README**: Yes/No
- **Add .gitignore**: Yes/No (and which template)
- **Add license**: Yes/No (and which license type)

### Step 2: Create the Repository

#### Basic Repository Creation

```bash
gh repo create <repository-name> --public --description "Description here"
```

#### Repository Creation with Options

```bash
gh repo create <repository-name> \
  --public \
  --description "Repository description" \
  --clone \
  --gitignore <template> \
  --license <license-type>
```

**Common Options:**
- `--public`: Create a public repository
- `--private`: Create a private repository
- `--description "text"`: Add repository description
- `--clone`: Clone the repository after creation
- `--gitignore <template>`: Add .gitignore (e.g., Python, Node, Java)
- `--license <type>`: Add license (e.g., mit, apache-2.0, gpl-3.0)
- `--enable-issues`: Enable issues (default: true)
- `--enable-wiki`: Enable wiki (default: true)

### Step 3: Verify Repository Creation

```bash
gh repo view <username>/<repository-name>
```

Or visit the repository in the browser:
```bash
gh repo view <username>/<repository-name> --web
```

## Complete Example Workflow

```bash
# 1. Check authentication
gh auth status

# 2. Create repository
gh repo create my-new-project \
  --public \
  --description "A sample project for demonstration" \
  --clone \
  --gitignore Python \
  --license mit

# 3. Navigate to repository (if cloned)
cd my-new-project

# 4. Verify creation
gh repo view --web
```

## Alternative: Interactive Creation

For a guided experience, run without arguments:

```bash
gh repo create
```

This will prompt for:
- Repository name
- Description
- Visibility (public/private)
- Whether to clone locally
- Whether to add README, .gitignore, or license

## Post-Creation Steps

### Initialize Local Repository (if not cloned)

```bash
mkdir <repository-name>
cd <repository-name>
git init
git remote add origin git@github.com:<username>/<repository-name>.git
```

### Add Initial Files

```bash
# Create README
echo "# Repository Name" > README.md

# Create .gitignore
echo "node_modules/" > .gitignore

# Add and commit
git add .
git commit -m "Initial commit"

# Push to GitHub
git push -u origin main
```

## Common Repository Templates

### Node.js Project
```bash
gh repo create my-node-app \
  --public \
  --description "Node.js application" \
  --clone \
  --gitignore Node \
  --license mit
```

### Python Project
```bash
gh repo create my-python-app \
  --public \
  --description "Python application" \
  --clone \
  --gitignore Python \
  --license mit
```

### Documentation Repository
```bash
gh repo create my-docs \
  --public \
  --description "Documentation repository" \
  --clone
```

## Troubleshooting

### Authentication Issues
```bash
# Re-authenticate
gh auth login

# Check current authentication
gh auth status
```

### Repository Already Exists
- Error: "Name already exists on this account"
- Solution: Choose a different name or delete the existing repository first

### Permission Denied
- Verify authentication token has repository creation permissions
- Check organization permissions if creating under an organization

## Additional Commands

### List Your Repositories
```bash
gh repo list
```

### Clone Existing Repository
```bash
gh repo clone <username>/<repository-name>
```

### Delete Repository
```bash
gh repo delete <username>/<repository-name>
```

### Fork Repository
```bash
gh repo fork <username>/<repository-name>
```

## Best Practices for Agents

1. **Always verify authentication first** - Run `gh auth status` before attempting to create a repository
2. **Use descriptive names** - Repository names should be clear and follow conventions (lowercase, hyphens)
3. **Add descriptions** - Always include a meaningful description
4. **Initialize with README** - Helps provide context for the repository
5. **Choose appropriate visibility** - Default to private for sensitive projects
6. **Add .gitignore early** - Prevents committing unnecessary files
7. **Include license** - Clarifies usage rights for open-source projects
8. **Verify creation** - Always confirm the repository was created successfully
9. **Document the process** - Log the repository URL and creation details

## Quick Reference

| Task | Command |
|------|---------|
| Create public repo | `gh repo create NAME --public` |
| Create private repo | `gh repo create NAME --private` |
| Create and clone | `gh repo create NAME --public --clone` |
| Interactive creation | `gh repo create` |
| View repository | `gh repo view USER/REPO` |
| Open in browser | `gh repo view USER/REPO --web` |
| List repositories | `gh repo list` |
| Delete repository | `gh repo delete USER/REPO` |

## Example: Full Project Setup

```bash
# Create repository with all options
gh repo create awesome-project \
  --public \
  --description "An awesome new project" \
  --clone \
  --gitignore Python \
  --license mit

# Navigate to repository
cd awesome-project

# Create initial project structure
mkdir src tests docs
touch src/__init__.py tests/__init__.py

# Create additional documentation
cat > README.md << 'EOF'
# Awesome Project

Description of the project.

## Installation

Instructions here.

## Usage

Usage examples here.
EOF

# Commit and push
git add .
git commit -m "Initial project structure"
git push -u origin main

# Verify
gh repo view --web
```

---

**Document Version:** 1.0
**Last Updated:** 2025-12-04
**For:** AI Agents automating GitHub repository creation
