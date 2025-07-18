# 🚀 Initial Setup Guide

## 📋 Complete GitHub Setup from Scratch

### 🔐 Step 1: Generate SSH Key

**Check if you already have SSH keys:**
```bash
ls -al ~/.ssh
```
*Look for files like `id_rsa.pub`, `id_ed25519.pub`, or `id_ecdsa.pub`*

**Generate new SSH key (if needed):**
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

**For older systems (if ed25519 isn't supported):**
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

**When prompted:**
- Press Enter for default file location
- Enter a secure passphrase (recommended)

### 🔑 Step 2: Add SSH Key to SSH Agent

**Start SSH agent:**
```bash
eval "$(ssh-agent -s)"
```

**Add SSH key to keychain (macOS):**
```bash
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

**For other systems:**
```bash
ssh-add ~/.ssh/id_ed25519
```

### 📋 Step 3: Add SSH Key to GitHub

**Copy SSH key to clipboard:**
```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

**Add to GitHub:**
1. Go to GitHub.com → Settings → SSH and GPG keys
2. Click "New SSH key"
3. Give it a title (e.g., "MacBook Pro")
4. Paste your key and click "Add SSH key"

**Test SSH connection:**
```bash
ssh -T git@github.com
```
*You should see: "Hi username! You've successfully authenticated..."*

### ⚙️ Step 4: Configure Git

**Set your identity:**
```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

**Set default branch name:**
```bash
git config --global init.defaultBranch main
```

**Configure credential helper (macOS):**
```bash
git config --global credential.helper osxkeychain
```

**Set default editor:**
```bash
git config --global core.editor "code --wait"  # VS Code
# or
git config --global core.editor "nano"          # Nano
```

### 🏠 Step 5: Create Your First Repository

**Option A: Create on GitHub first (Recommended)**
1. Go to github.com/new
2. Enter repository name
3. Choose public/private
4. Initialize with README
5. Click "Create repository"

**Option B: Create locally first**
```bash
mkdir my-project
cd my-project
git init
echo "# My Project" >> README.md
git add README.md
git commit -m "Initial commit"
```

### 🔗 Step 6: Connect Local to Remote

**Add remote origin:**
```bash
git remote add origin git@github.com:username/repository-name.git
```

**Push to GitHub:**
```bash
git push -u origin main
```

### ✅ Step 7: Verify Everything Works

**Check remote connection:**
```bash
git remote -v
```

**Check configuration:**
```bash
git config --list
```

**Make a test change:**
```bash
echo "Test update" >> README.md
git add README.md
git commit -m "Test commit"
git push
```

## 🛠️ Essential Configuration

### Global .gitignore
Create a global gitignore file:
```bash
git config --global core.excludesfile ~/.gitignore_global
```

**Common entries for ~/.gitignore_global:**
```
# macOS
.DS_Store
.AppleDouble
.LSOverride

# Windows
Thumbs.db
ehthumbs.db
Desktop.ini

# IDE
.vscode/
.idea/
*.swp
*.swo

# Logs
*.log
npm-debug.log*
```

### Useful Git Aliases
```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
```

## 🔧 Troubleshooting Setup

### SSH Issues
**Permission denied (publickey):**
```bash
ssh-add -l  # Check if key is loaded
ssh-add ~/.ssh/id_ed25519  # Add key if missing
```

**Wrong permissions:**
```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```

### Git Configuration Issues
**Check current config:**
```bash
git config --list --show-origin
```

**Reset specific config:**
```bash
git config --global --unset user.name
git config --global --unset user.email
```

## 📱 Additional Tools

### GitHub CLI (Optional)
```bash
brew install gh  # macOS
gh auth login    # Follow prompts
```

### Git GUI Tools
- **GitHub Desktop** - Official GitHub client
- **GitKraken** - Advanced Git GUI
- **SourceTree** - Free Git client by Atlassian
- **Tower** - Premium Git client for Mac

## 🎯 Next Steps
After completing this setup:
1. ✅ Review the [Daily Workflow Guide](daily-workflow.md)
2. ✅ Learn about [GitHub Features](github-features.md)
3. ✅ Set up [Project Templates](templates/)
4. ✅ Explore [Best Practices](best-practices.md)
