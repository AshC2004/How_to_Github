# 🤖 Automation & Tools Guide

## 🔧 GitHub CLI Usage

### 🚀 Installation and Setup

**📦 Installation**

```bash
# macOS
brew install gh

# Windows
winget install GitHub.cli

# Linux (Ubuntu/Debian)
sudo apt install gh

# Verify installation
gh --version
```

**🔐 Authentication**

```bash
# Login to GitHub
gh auth login

# Check authentication status
gh auth status

# Login with token
gh auth login --with-token %Creset' --abbrev-commit"
```

### 📝 Complete .gitconfig Alias Section

**📋 Professional Git Aliases**

```ini
[alias]
    # Basic shortcuts
    co = checkout
    br = branch
    ci = commit
    st = status
    
    # Create and switch to new branch
    nb = checkout -b
    
    # Delete branch
    del = branch -D
    
    # Quick commit
    cm = commit -m
    
    # Stage all and commit
    ac = !git add -A && git commit -m
    
    # Amend last commit
    amend = commit --amend --no-edit
    
    # Undo last commit but keep changes
    uncommit = reset --soft HEAD~1
    
    # Discard all changes
    discard = checkout -- .
    
    # Show repository status
    state = !git fetch --prune && git status
    
    # Pretty log
    lg = log --oneline --graph --decorate --all
    
    # Detailed log
    ll = log --pretty=format:'%C(yellow)%h%Cred%d %Creset%s%Cblue [%cn]' --decorate --numstat
    
    # Push to origin with same branch name
    push-branch = !git push -u origin $(git branch --show-current)
    
    # Interactive rebase
    rb = rebase -i HEAD~
    
    # Show conflicts
    conflicts = diff --name-only --diff-filter=U
    
    # List aliases
    aliases = config --get-regexp alias
    
    # Clean up merged branches
    cleanup = !git branch --merged | grep -v '\\*\\|master\\|main\\|develop' | xargs -n 1 git branch -d
    
    # Find commits by message
    find = !git log --grep
    
    # Show file history
    filelog = log -u
    
    # Show modified files in last commit
    dl = !git ll -1
    
    # Show diff of last commit
    dlc = diff --cached HEAD^
    
    # Show content of a commit
    dr = !f() { git diff "$1"^.."$1"; }; f
    
    # Find a file path in codebase
    f = !git ls-files | grep -i
    
    # Search/grep your entire codebase for a string
    grep = grep -Ii
    
    # Grep from root folder
    gra = !f() { A=$(pwd) && TOPLEVEL=$(git rev-parse --show-toplevel) && cd $TOPLEVEL && git grep --full-name -In $1 | xargs -I{} echo $TOPLEVEL/{} && cd $A; }; f
    
    # List remotes
    rem = remote -v
    
    # Reset previous commit, but keep all the associated changes
    r = !git l -1 --pretty=format:'%C(yellow)%h%Creset %C(white)%s%Creset %C(cyan)(%ar)%Creset' && git reset --soft HEAD~1
    
    # Delete local branch
    db = branch -D
    
    # Delete remote branch
    dr = push origin --delete
    
    # Switch to previous branch
    prev = checkout -
    
    # Show all branches
    branches = branch -a
    
    # Show all tags
    tags = tag -l
    
    # Show all stashes
    stashes = stash list
    
    # Create new stash
    save = stash save
    
    # Apply stash
    apply = stash apply
    
    # Drop stash
    drop = stash drop
    
    # Show stash content
    show = stash show -p
```

### 🔧 Shell Aliases (Bash/Zsh)

**📋 Shell Aliases for Git**

```bash
# Add to ~/.bashrc or ~/.zshrc
alias g='git'
alias gs='git status'
alias ga='git add'
alias gaa='git add --all'
alias gc='git commit'
alias gcm='git commit -m'
alias gp='git push'
alias gpl='git pull'
alias gd='git diff'
alias gco='git checkout'
alias gcb='git checkout -b'
alias gbr='git branch'
alias gm='git merge'
alias gr='git rebase'
alias gss='git stash save'
alias gsp='git stash pop'
alias gsl='git stash list'
alias glog='git log --oneline --graph --decorate'
alias gundo='git reset --soft HEAD~1'
alias gclean='git clean -fd'
alias gpull='git pull --rebase'
alias gpush='git push origin HEAD'
```

## 🖥️ GitHub Desktop Alternative

### 📊 GitHub Desktop vs Command Line

**🎯 When to Use GitHub Desktop**

| Scenario | GitHub Desktop | Command Line |
|----------|----------------|--------------|
| **Beginner-friendly** | ✅ Visual interface | ❌ Steep learning curve |
| **Complex operations** | ❌ Limited features | ✅ Full Git power |
| **Merge conflicts** | ✅ Visual diff tools | ❌ Manual resolution |
| **Automation/Scripting** | ❌ No scripting | ✅ Scriptable |
| **Performance** | ❌ Slower for large repos | ✅ Fast operations |
| **Visual history** | ✅ Rich visualization | ❌ Text-based |

### 🚀 GitHub Desktop Features

**📋 Key Capabilities**

```bash
# Download GitHub Desktop
https://desktop.github.com/

# Key features:
- Visual diff viewer
- Commit history visualization
- Branch management
- Pull request creation
- Merge conflict resolution
- Stash management
- Cherry-picking commits
```

**🔄 GitHub Desktop Workflow**

1. **Clone Repository**
   - File → Clone Repository
   - Choose from GitHub.com or URL

2. **Make Changes**
   - Edit files in your preferred editor
   - Desktop shows changes automatically

3. **Stage and Commit**
   - Review changes in left panel
   - Write commit message
   - Click "Commit to main"

4. **Push Changes**
   - Click "Push origin" button
   - Changes sync to GitHub

5. **Create Pull Request**
   - Click "Create Pull Request"
   - Opens browser to complete PR

### 🔀 Advanced GitHub Desktop Usage

**🌿 Branch Management**

```bash
# Create new branch
Branch → New Branch → "feature/new-feature"

# Switch branches
Current Branch dropdown → Select branch

# Merge branches
Branch → Merge into Current Branch

# Delete branch
Branch → Delete (after merging)
```

**⚙️ GitHub Desktop Settings**

```bash
# Preferences (macOS) / Options (Windows)
File → Preferences/Options

# Key settings:
- Default clone directory
- External editor preference
- Git configuration
- Advanced settings
```

### 🔧 GitHub Desktop Keyboard Shortcuts

**📋 Essential Shortcuts**

| Action | macOS | Windows/Linux |
|--------|-------|---------------|
| **New Repository** | `Cmd+N` | `Ctrl+N` |
| **Clone Repository** | `Cmd+Shift+O` | `Ctrl+Shift+O` |
| **Show Changes** | `Cmd+1` | `Ctrl+1` |
| **Show History** | `Cmd+2` | `Ctrl+2` |
| **Show Repositories** | `Cmd+T` | `Ctrl+T` |
| **Open in Terminal** | `Cmd+\`` | `Ctrl+\`` |
| **Push** | `Cmd+P` | `Ctrl+P` |
| **Pull** | `Cmd+Shift+P` | `Ctrl+Shift+P` |
| **Create Branch** | `Cmd+Shift+N` | `Ctrl+Shift+N` |
| **Switch Branch** | `Cmd+B` | `Ctrl+B` |

## 🔧 Advanced Git Workflow Automation

### 🤖 Git Hooks

**📋 Pre-commit Hooks**

```bash
# Install pre-commit
pip install pre-commit

# Create .pre-commit-config.yaml
cat > .pre-commit-config.yaml "
    exit 1
fi

# Update main branch
git checkout main
git pull origin main

# Create and push feature branch
git checkout -b "feature/$feature_name"
git push -u origin "feature/$feature_name"

echo "✅ Feature branch 'feature/$feature_name' created and pushed"
```

**🚀 Release Preparation Script**

```bash
#!/bin/bash
# prepare-release.sh

version=$1
if [ -z "$version" ]; then
    echo "Usage: $0 "
    exit 1
fi

# Update version in files
sed -i "s/\"version\": \".*\"/\"version\": \"$version\"/" package.json

# Update changelog
echo "## [$version] - $(date +%Y-%m-%d)" >> CHANGELOG.md

# Commit changes
git add .
git commit -m "chore: prepare release $version"

# Create tag
git tag -a "v$version" -m "Version $version"

echo "✅ Release $version prepared. Push with: git push origin main --tags"
```

### 🔄 GitHub Actions Integration

**📋 Automated Workflow with GitHub CLI**

```yaml
# .github/workflows/auto-pr.yml
name: Auto PR Creation

on:
  push:
    branches:
      - 'feature/*'

jobs:
  create-pr:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Create Pull Request
        run: |
          gh pr create \
            --title "Auto PR: ${GITHUB_REF#refs/heads/}" \
            --body "Automated PR creation for branch ${GITHUB_REF#refs/heads/}" \
            --base main \
            --head ${GITHUB_REF#refs/heads/}
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## 🎯 Tool Selection Guide

### 📊 Choose the Right Tool

**🔧 Task-Based Tool Selection**

| Task | Best Tool | Alternative |
|------|-----------|-------------|
| **Quick commits** | Command Line + Aliases | VS Code |
| **Visual diff review** | GitHub Desktop | GitLens |
| **Automation** | GitHub CLI | Scripts |
| **Complex merges** | VS Code + Extensions | GitHub Desktop |
| **Repository management** | GitHub CLI | GitHub Web |
| **Code review** | GitHub Web | VS Code |

### 🚀 Workflow Optimization Tips

**⚡ Speed Up Your Workflow**

1. **Use aliases for common commands**
   ```bash
   alias gac='git add -A && git commit -m'
   alias gps='git push'
   alias gpl='git pull'
   ```

2. **Set up tab completion**
   ```bash
   # Add to ~/.bashrc or ~/.zshrc
   source /usr/share/bash-completion/completions/git
   ```

3. **Use GitHub CLI for repository operations**
   ```bash
   gh repo create --clone
   gh pr create --fill
   gh issue create --title "Bug report"
   ```

4. **Configure VS Code for Git**
   ```json
   {
     "git.enableSmartCommit": true,
     "git.autofetch": true,
     "git.confirmSync": false
   }
   ```

This comprehensive automation guide provides tools and techniques to streamline your GitHub workflow, from command-line efficiency to visual interfaces and automated processes. Choose the tools that best fit your workflow and gradually incorporate automation to improve your productivity.
