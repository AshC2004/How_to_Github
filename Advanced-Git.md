# ⚡ Advanced Git Commands

## 🔄 Interactive Rebase

### Basic Interactive Rebase
```bash
# Rebase last 3 commits
git rebase -i HEAD~3

# Rebase from specific commit
git rebase -i abc123f
```

**Interactive Commands:**
- **pick (p):** Use commit as-is
- **reword (r):** Change commit message
- **edit (e):** Stop to amend commit
- **squash (s):** Combine with previous commit
- **fixup (f):** Like squash but discard message
- **drop (d):** Remove commit

### Squashing Commits
```bash
# Original commits:
pick abc123f Add user model
pick def456g Fix typo in user model
pick ghi789h Add user validation

# Squash into single commit:
pick abc123f Add user model
squash def456g Fix typo in user model
squash ghi789h Add user validation
```

### Splitting Commits
```bash
# Mark commit for editing
git rebase -i HEAD~3
# Change 'pick' to 'edit' for target commit

# When rebase stops at the commit:
git reset HEAD~1
git add file1.js
git commit -m "First logical change"
git add file2.js
git commit -m "Second logical change"
git rebase --continue
```

## 🍒 Cherry-Picking

### Basic Cherry-Pick
```bash
# Apply specific commit to current branch
git cherry-pick abc123f

# Cherry-pick multiple commits
git cherry-pick abc123f def456g ghi789h

# Cherry-pick range of commits
git cherry-pick abc123f..ghi789h
```

### Cherry-Pick Options
```bash
# Cherry-pick without committing
git cherry-pick --no-commit abc123f

# Cherry-pick and edit message
git cherry-pick --edit abc123f

# Cherry-pick with signature
git cherry-pick --signoff abc123f
```

### Handling Cherry-Pick Conflicts
```bash
# If conflicts occur:
# 1. Resolve conflicts in files
# 2. Add resolved files
git add resolved-file.js

# 3. Continue cherry-pick
git cherry-pick --continue

# Or abort cherry-pick
git cherry-pick --abort
```

## 📦 Stashing Changes

### Basic Stashing
```bash
# Stash current changes
git stash

# Stash with message
git stash push -m "Work in progress on feature X"

# Stash including untracked files
git stash -u

# Stash including ignored files
git stash -a
```

### Managing Stashes
```bash
# List all stashes
git stash list

# Show stash contents
git stash show stash@{0}

# Apply latest stash
git stash pop

# Apply specific stash
git stash apply stash@{2}

# Drop specific stash
git stash drop stash@{1}

# Clear all stashes
git stash clear
```

### Partial Stashing
```bash
# Stash specific files
git stash push -m "Partial stash" file1.js file2.js

# Interactive stashing
git stash -p
```

## 🔗 Git Hooks

### Types of Hooks
**Client-side hooks:**
- `pre-commit` - Before commit is created
- `prepare-commit-msg` - Before commit message editor
- `commit-msg` - After commit message is entered
- `post-commit` - After commit is completed
- `pre-push` - Before push to remote

**Server-side hooks:**
- `pre-receive` - Before any refs are updated
- `update` - Before each ref is updated
- `post-receive` - After all refs are updated

### Creating Hooks
```bash
# Navigate to hooks directory
cd .git/hooks

# Create pre-commit hook
touch pre-commit
chmod +x pre-commit
```

**Sample pre-commit hook:**
```bash
#!/bin/sh
# Run tests before commit
npm test
if [ $? -ne 0 ]; then
    echo "Tests failed. Commit aborted."
    exit 1
fi

# Run linter
npm run lint
if [ $? -ne 0 ]; then
    echo "Linting failed. Commit aborted."
    exit 1
fi

echo "Pre-commit checks passed!"
```

### Bypassing Hooks
```bash
# Skip pre-commit hooks
git commit --no-verify -m "Skip hooks"

# Skip pre-push hooks
git push --no-verify
```

## 🌲 Git Submodules

### Adding Submodules
```bash
# Add submodule
git submodule add https://github.com/user/repo.git path/to/submodule

# Add to specific branch
git submodule add -b develop https://github.com/user/repo.git libs/mylib
```

### Working with Submodules
```bash
# Initialize submodules after clone
git submodule init
git submodule update

# Or combine both
git submodule update --init

# Update submodule to latest
cd path/to/submodule
git pull origin main
cd ../..
git add path/to/submodule
git commit -m "Update submodule"
```

### Submodule Commands
```bash
# Update all submodules
git submodule update --remote

# Update specific submodule
git submodule update --remote path/to/submodule

# Remove submodule
git submodule deinit path/to/submodule
git rm path/to/submodule
```

## 🔍 Advanced Searching

### Git Grep
```bash
# Search in tracked files
git grep "function"

# Search in specific branch
git grep "function" main

# Search with line numbers
git grep -n "function"

# Search with context
git grep -C 3 "function"
```

### Git Log Searching
```bash
# Search commit messages
git log --grep="bug fix"

# Search by author
git log --author="John Doe"

# Search by date
git log --since="2023-01-01" --until="2023-12-31"

# Search for changes in specific file
git log -p filename.js

# Search for code changes
git log -S "function_name"
```

### Git Blame
```bash
# Show who changed each line
git blame filename.js

# Show blame for specific lines
git blame -L 10,20 filename.js

# Show blame with email
git blame -e filename.js
```

## 🔄 Advanced Merging

### Merge Strategies
```bash
# Fast-forward merge (default)
git merge feature-branch

# No fast-forward merge
git merge --no-ff feature-branch

# Squash merge
git merge --squash feature-branch

# Octopus merge (multiple branches)
git merge branch1 branch2 branch3
```

### Merge Conflict Resolution
```bash
# Use merge tool
git mergetool

# Accept their changes
git checkout --theirs filename.js

# Accept our changes
git checkout --ours filename.js

# Manual resolution then:
git add filename.js
git commit
```

### Three-Way Merge
```bash
# Show three-way diff during conflict
git diff

# Show conflict in different format
git diff --name-only --diff-filter=U
```

## 🏷️ Advanced Tagging

### Tag Types
```bash
# Lightweight tag
git tag v1.0.0

# Annotated tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# Signed tag
git tag -s v1.0.0 -m "Signed release"
```

### Tag Management
```bash
# List tags
git tag

# List tags with pattern
git tag -l "v1.*"

# Show tag information
git show v1.0.0

# Delete tag
git tag -d v1.0.0

# Delete remote tag
git push origin :refs/tags/v1.0.0
```

### Tagging Previous Commits
```bash
# Tag specific commit
git tag -a v1.0.0 abc123f -m "Release version 1.0.0"

# Push tags to remote
git push origin v1.0.0
git push
