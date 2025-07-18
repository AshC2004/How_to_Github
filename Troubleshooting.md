# 🔧 Git Troubleshooting Guide

## 🚨 Common Error Messages & Solutions

### Authentication Errors

#### "Permission denied (publickey)"
**Problem:** SSH key authentication failed
```bash
git@github.com: Permission denied (publickey).
```

**Solutions:**
```bash
# Check if SSH key is loaded
ssh-add -l

# Add SSH key to agent
ssh-add ~/.ssh/id_ed25519

# Test SSH connection
ssh -T git@github.com

# Generate new SSH key if needed
ssh-keygen -t ed25519 -C "your_email@example.com"
```

#### "Authentication failed"
**Problem:** HTTPS authentication issues
```bash
remote: Support for password authentication was removed
```

**Solutions:**
```bash
# Switch to SSH
git remote set-url origin git@github.com:username/repo.git

# Or use personal access token
git remote set-url origin https://username:token@github.com/username/repo.git
```

### Merge Conflicts

#### "Automatic merge failed"
**Problem:** Git can't automatically merge changes
```bash
Auto-merging file.txt
CONFLICT (content): Merge conflict in file.txt
```

**Solutions:**
```bash
# View conflicted files
git status

# Open conflicted file and resolve manually
# Look for markers: <<<<<<<, =======, >>>>>>>

# After resolving conflicts:
git add resolved-file.txt
git commit
```

#### "You have unmerged paths"
**Problem:** Merge conflicts not fully resolved
```bash
You have unmerged paths.
  (fix conflicts and run "git commit")
```

**Solutions:**
```bash
# Check which files have conflicts
git status

# View conflict details
git diff

# Resolve conflicts and add files
git add .
git commit
```

### Branch Issues

#### "Your branch is ahead of 'origin/main'"
**Problem:** Local commits haven't been pushed
```bash
Your branch is ahead of 'origin/main' by 2 commits.
```

**Solutions:**
```bash
# Push local commits
git push origin main

# Or reset to remote state (loses local commits)
git reset --hard origin/main
```

#### "Your branch is behind 'origin/main'"
**Problem:** Remote has newer commits
```bash
Your branch is behind 'origin/main' by 3 commits.
```

**Solutions:**
```bash
# Pull latest changes
git pull origin main

# Or fetch and merge manually
git fetch origin
git merge origin/main
```

### Repository State Issues

#### "You are in 'detached HEAD' state"
**Problem:** Checked out specific commit instead of branch
```bash
You are in 'detached HEAD' state.
```

**Solutions:**
```bash
# Create new branch from current state
git checkout -b new-branch-name

# Or return to main branch
git checkout main
```

#### "nothing to commit, working tree clean"
**Problem:** No changes to commit
```bash
nothing to commit, working tree clean
```

**Solutions:**
```bash
# Check if files are staged
git status

# Stage files if needed
git add .

# Check if you're in right directory
pwd
ls -la
```

## 🔄 Undoing Changes

### Unstage Files
```bash
# Unstage specific file
git reset HEAD filename.txt

# Unstage all files
git reset HEAD

# Using newer syntax
git restore --staged filename.txt
```

### Undo Local Changes
```bash
# Discard changes in working directory
git checkout -- filename.txt

# Using newer syntax
git restore filename.txt

# Discard all local changes
git reset --hard HEAD
```

### Undo Commits

#### Undo Last Commit (Keep Changes)
```bash
# Soft reset - keeps changes staged
git reset --soft HEAD~1

# Mixed reset - keeps changes unstaged
git reset HEAD~1
```

#### Undo Last Commit (Discard Changes)
```bash
# Hard reset - discards all changes
git reset --hard HEAD~1
```

#### Undo Multiple Commits
```bash
# Undo last 3 commits
git reset --hard HEAD~3

# Reset to specific commit
git reset --hard abc123f
```

#### Undo Public Commits
```bash
# Create new commit that undoes changes
git revert HEAD

# Revert multiple commits
git revert HEAD~2..HEAD

# Revert specific commit
git revert abc123f
```

## 🔍 Recovering Lost Work

### Find Lost Commits
```bash
# Show reflog (recent HEAD changes)
git reflog

# Find commit in reflog
git reflog show HEAD

# Restore lost commit
git cherry-pick abc123f
```

### Recover Deleted Branch
```bash
# Find branch in reflog
git reflog | grep branch-name

# Recreate branch
git branch recovered-branch abc123f
```

### Recover Deleted Files
```bash
# Find commit that deleted file
git log --diff-filter=D -- path/to/file.txt

# Restore file from previous commit
git checkout abc123f~1 -- path/to/file.txt
```

## 🔧 Repository Corruption

### Fix Corrupted Repository
```bash
# Check repository integrity
git fsck

# Fix common issues
git gc --aggressive

# Rebuild index
rm .git/index
git reset
```

### Clone Issues
```bash
# Shallow clone for large repositories
git clone --depth 1 <url>

# Clone specific branch
git clone -b branch-name <url>

# Fix partial clone
git fetch --unshallow
```

## 🌐 Remote Repository Issues

### "fatal: remote origin already exists"
**Problem:** Trying to add remote that already exists
```bash
fatal: remote origin already exists.
```

**Solutions:**
```bash
# Remove existing remote
git remote rm origin

# Add new remote
git remote add origin <url>

# Or update existing remote
git remote set-url origin <new-url>
```

### "Updates were rejected"
**Problem:** Remote has changes that conflict with local
```bash
Updates were rejected because the remote contains work
```

**Solutions:**
```bash
# Pull changes first
git pull origin main

# Or force push (dangerous)
git push --force-with-lease origin main

# Or rebase local changes
git pull --rebase origin main
```

### "The requested URL returned error: 404"
**Problem:** Repository doesn't exist or no access
```bash
The requested URL returned error: 404 Not Found
```

**Solutions:**
```bash
# Check repository URL
git remote -v

# Update URL if incorrect
git remote set-url origin <correct-url>

# Check repository exists and you have access
```

## 🗂️ File and Directory Issues

### Large File Problems
```bash
# File too large for GitHub
remote: error: File is too large

# Solutions:
# 1. Remove from history
git filter-branch --tree-filter 'rm -f large-file.zip' HEAD

# 2. Use Git LFS
git lfs track "*.zip"
git add .gitattributes
git add large-file.zip
git commit -m "Add large file with LFS"

# 3. Remove from current commit
git rm --cached large-file.zip
echo "large-file.zip" >> .gitignore
git commit -m "Remove large file"
```

### Case Sensitivity Issues
```bash
# Mac/Windows case insensitive filesystems
git config core.ignorecase false

# Rename file with proper case
git mv filename.txt FileName.txt
```

### Line Ending Issues
```bash
# Configure line endings
git config --global core.autocrlf true   # Windows
git config --global core.autocrlf input  # Mac/Linux

# Fix existing files
git add --renormalize .
git commit -m "Fix line endings"
```

## 🔄 Synchronization Issues

### Diverged Branches
```bash
# Your branch and 'origin/main' have diverged
git status

# Solutions:
# 1. Merge (creates merge commit)
git merge origin/main

# 2. Rebase (cleaner history)
git rebase origin/main

# 3. Reset (loses local changes)
git reset --hard origin/main
```

### Stale Remote Branches
```bash
# List all remote branches
git branch -r

# Remove stale remote branches
git remote prune origin

# Or during fetch
git fetch --prune origin
```

## 🛠️ Performance Issues

### Slow Git Operations
```bash
# Repository maintenance
git gc --aggressive

# Repack objects
git repack -Ad

# Clean up unnecessary files
git prune

# Check repository size
du -sh .git/
```

### Large Repository Handling
```bash
# Partial clone
git clone --filter=blob:none <url>

# Shallow clone
git clone --depth 50 <url>

# Reduce history
git fetch --depth=1
```

## 📊 Diagnostic Commands

### Repository Health Check
```bash
# Check repository integrity
git fsck --full

# Show repository statistics
git count-objects -vH

# Check configuration
git config --list

# Show remote information
git remote show origin
```

### Debug Git Operations
```bash
# Verbose output
git -v command

# Debug SSH connections
ssh -vT git@github.com

# Trace Git operations
GIT_TRACE=1 git command
```

## 🚨 Emergency Recovery

### Nuclear Option - Start Fresh
```bash
# Backup important files
cp -r project-folder project-backup

# Remove Git history
rm -rf .git

# Initialize new repository
git init
git add .
git commit -m "Initial commit"
git remote add origin <url>
git push -u origin main
```

### Partial Recovery
```bash
# Create new branch from working directory
git checkout --orphan new-start
git add .
git commit -m "New start"

# Or stash everything and start over
git stash
git reset --hard HEAD
git stash pop
```

## 🔍 Getting Help

### Git Built-in Help
```bash
# Get help for specific command
git help <command>

# Quick help
git <command> --help

# Show Git version
git --version
```

### Useful Resources
- **Git Documentation:** https://git-scm.com/doc
- **Pro Git Book:** https://git-scm.com/book
- **Git Reference:** https://git-scm.com/docs
- **GitHub Help:** https://docs.github.com

### Community Support
- **Stack Overflow:** Tag questions with `git`
- **GitHub Community:** https://github.community
- **Git User Mailing List:** git@vger.kernel.org
- **Reddit:** r/git subreddit

## 📝 Prevention Tips

### Best Practices
- **Commit frequently** with clear messages
- **Pull before pushing** to avoid conflicts
- **Use branches** for experimental work
- **Keep backups** of important repositories
- **Review changes** before committing

### Setup Safeguards
```bash
# Set up useful aliases
git config --global alias.unstage 'reset HEAD --'
git config --global alias.visual '!gitk'

# Enable helpful features
git config --global help.autocorrect 1
git config --global color.ui auto

# Set up pre-commit hooks
# Create .git/hooks/pre-commit script
```

Remember: Most Git problems can be solved, and Git rarely loses data permanently. When in doubt, make a backup and seek help from the community!
