# 📋 Complete GitHub Workflow Guide

## 🚀 Daily Git Push Checklist

### 🔧 Prerequisites (One-time Setup)
Before using this checklist, ensure you have:
- [x] Generated an SSH key and added it to GitHub
- [x] Configured your repository's `origin` to use SSH URL (`git@github.com:username/repo.git`)
- [x] Set Git credential helper: `git config --global credential.helper osxkeychain`

---

### 📁 Step 1: Navigate to Your Project
```bash
cd ~/Code/your-project-name
```
*Replace `your-project-name` with your actual project directory*

### 🔍 Step 2: Check Repository Status
```bash
git status
```
**What this shows:**
- Modified files (red = unstaged, green = staged)
- Untracked files
- Current branch
- Commits ahead/behind remote

**Quick branch check:**
```bash
git branch
```

### 🔄 Step 3: Sync with Remote (Recommended)
```bash
git fetch origin
git rebase origin/main
```
**Alternative (if you prefer merging):**
```bash
git pull origin main
```

**Why this matters:** Prevents merge conflicts and keeps your history clean.

### ➕ Step 4: Stage Your Changes
**Option A - Stage all changes:**
```bash
git add .
```

**Option B - Stage specific files:**
```bash
git add path/to/file1.js path/to/directory/
```

**Option C - Interactive staging:**
```bash
git add -i
```

### 💬 Step 5: Commit with Clear Message
```bash
git commit -m "✨ Add user authentication feature"
```

**Commit Message Best Practices:**
- Use present tense ("Add feature" not "Added feature")
- Keep first line under 50 characters
- Use conventional commits:
  - `feat:` - New feature
  - `fix:` - Bug fix
  - `docs:` - Documentation
  - `style:` - Code style changes
  - `refactor:` - Code refactoring
  - `test:` - Adding tests
  - `chore:` - Maintenance tasks

### 🌿 Step 6: Branch Management (Optional)
**Create new feature branch:**
```bash
git checkout -b feature/user-profile
```

**Switch to existing branch:**
```bash
git checkout main
```

**List all branches:**
```bash
git branch -a
```

### 🚀 Step 7: Push to GitHub
**Push current branch:**
```bash
git push -u origin main
```

**Push feature branch:**
```bash
git push -u origin feature/user-profile
```

**Subsequent pushes (after using `-u` flag):**
```bash
git push
```

### ✅ Step 8: Verify on GitHub
1. Navigate to your repository: `https://github.com/username/repository-name`
2. Confirm latest commit appears
3. Check that all files are present and correctly updated

### 🧹 Step 9: Clean Up (Optional)
**Delete merged feature branch:**
```bash
git branch -d feature/user-profile
```

**Delete remote tracking branch:**
```bash
git push origin --delete feature/user-profile
```

---

## 🛠️ Pro Tips & Best Practices

### 📝 Commit Guidelines
- **Small, logical commits** - Each commit should represent one logical change
- **Descriptive messages** - Future you will thank present you
- **Commit early, commit often** - Don't wait until everything is perfect

### 🔒 Security & Setup
- Always use SSH keys for authentication
- Keep your `.gitignore` updated
- Never commit sensitive information (API keys, passwords)

### 🌊 Workflow Optimization
- **Pull before you push** - Always sync before starting work
- **Use branches** - Keep `main` stable, do work on feature branches
- **Review before pushing** - Use `git diff` to review changes

### 🚨 Common Issues & Solutions
**Merge conflicts:**
```bash
git status  # See conflicted files
# Edit files to resolve conflicts
git add .
git commit -m "Resolve merge conflicts"
```

**Undo last commit (keep changes):**
```bash
git reset --soft HEAD~1
```

**Force push (use with caution):**
```bash
git push --force-with-lease origin branch-name
```

---

## 📚 Quick Reference Commands

| Command | Description |
|---------|-------------|
| `git status` | Check repository status |
| `git log --oneline` | View commit history |
| `git diff` | See unstaged changes |
| `git diff --staged` | See staged changes |
| `git branch` | List branches |
| `git checkout -b <branch>` | Create and switch to new branch |
| `git merge <branch>` | Merge branch into current branch |
| `git remote -v` | View remote URLs |
| `git config --list` | View Git configuration |
