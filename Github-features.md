# 🌟 GitHub Features Guide

## 🔄 Pull Requests (PRs)

### Creating a Pull Request
1. **Push your feature branch:**
   ```bash
   git checkout -b feature/new-feature
   # Make your changes
   git add .
   git commit -m "Add new feature"
   git push -u origin feature/new-feature
   ```

2. **Create PR on GitHub:**
   - Go to your repository on GitHub
   - Click "Compare & pull request" button
   - Fill out PR template:
     - **Title:** Clear, descriptive summary
     - **Description:** What changes were made and why
     - **Link related issues:** Use `Closes #123` or `Fixes #456`

### PR Best Practices
- **Keep PRs focused** - One feature/fix per PR
- **Write clear descriptions** - Explain the "why" not just the "what"
- **Include screenshots** for UI changes
- **Add reviewers** before submitting
- **Respond to feedback** promptly and professionally

### PR Commands
```bash
# Update PR branch with latest main
git checkout main
git pull origin main
git checkout feature/new-feature
git merge main
git push origin feature/new-feature

# Or using rebase (cleaner history)
git rebase main
git push --force-with-lease origin feature/new-feature
```

## 🎯 Issues & Project Management

### Creating Issues
**Good issue structure:**
- **Title:** Clear, specific problem statement
- **Labels:** bug, enhancement, question, help wanted
- **Assignees:** Who should work on this
- **Milestone:** Which release/sprint
- **Description template:**
  ```markdown
  ## Problem
  Brief description of the issue
  
  ## Steps to Reproduce
  1. Step one
  2. Step two
  3. Step three
  
  ## Expected Behavior
  What should happen
  
  ## Actual Behavior
  What actually happens
  
  ## Environment
  - OS: macOS 12.0
  - Browser: Chrome 96
  - Version: 1.2.3
  ```

### Issue Management
- **Use labels** for categorization
- **Link to PRs** that fix the issue
- **Close issues** when resolved
- **Reference in commits:** `git commit -m "Fix login bug (closes #123)"`

### GitHub Projects
1. **Create project board:** Repository → Projects → New project
2. **Add columns:** To Do, In Progress, Done
3. **Add cards:** Issues, PRs, or custom notes
4. **Automate:** Set up column automation rules

## 🤖 GitHub Actions Basics

### Simple CI/CD Workflow
Create `.github/workflows/ci.yml`:
```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
        
    - name: Install dependencies
      run: npm ci
      
    - name: Run tests
      run: npm test
      
    - name: Run linter
      run: npm run lint
```

### Common Actions
- **Checkout code:** `actions/checkout@v3`
- **Setup Node.js:** `actions/setup-node@v3`
- **Setup Python:** `actions/setup-python@v4`
- **Deploy to S3:** `aws-actions/configure-aws-credentials@v2`

### Action Triggers
```yaml
on:
  push:                    # On every push
  pull_request:           # On every PR
  schedule:               # Cron schedule
    - cron: '0 2 * * *'   # Daily at 2 AM
  workflow_dispatch:      # Manual trigger
```

## 🔒 Repository Settings & Permissions

### Branch Protection Rules
**Settings → Branches → Add rule:**
- **Require pull request reviews** before merging
- **Require status checks** to pass before merging
- **Require branches to be up to date** before merging
- **Require conversation resolution** before merging
- **Restrict pushes** to matching branches

### Access Control
**Settings → Manage access:**
- **Public repos:** Anyone can read
- **Private repos:** Only collaborators can access
- **Team permissions:** Read, Write, Admin
- **Branch permissions:** Per-branch access control

### Repository Settings
**Essential settings to configure:**
- **Default branch:** Usually `main`
- **Delete head branches:** Auto-delete merged branches
- **Merge button:** Allow/disallow merge types
- **Issue templates:** Standardize issue creation
- **Security alerts:** Enable vulnerability alerts

## 📊 Insights & Analytics

### Repository Insights
**Insights tab provides:**
- **Pulse:** Recent activity summary
- **Contributors:** Who's contributing what
- **Traffic:** Views and clones
- **Commits:** Commit activity over time
- **Code frequency:** Additions/deletions over time

### Understanding Graphs
- **Network graph:** Branch and merge visualization
- **Dependency graph:** Package dependencies
- **Security advisories:** Known vulnerabilities

## 🏷️ Releases & Tags

### Creating Releases
1. **Create tag:**
   ```bash
   git tag -a v1.0.0 -m "Release version 1.0.0"
   git push origin v1.0.0
   ```

2. **Create release on GitHub:**
   - Go to Releases → Create new release
   - Choose tag or create new one
   - Write release notes
   - Upload assets (binaries, docs)

### Semantic Versioning
- **Major:** `v1.0.0` - Breaking changes
- **Minor:** `v1.1.0` - New features, backwards compatible
- **Patch:** `v1.1.1` - Bug fixes

## 🔍 Search & Navigation

### Search Syntax
```
# Search in specific repository
repo:username/repository searchterm

# Search by language
language:javascript

# Search by filename
filename:package.json

# Search by file extension
extension:md

# Search in commits
author:username

# Search in issues/PRs
is:issue is:open label:bug
```

### Advanced Search
- **Code search:** Find specific code patterns
- **Issue search:** Filter by labels, assignees, state
- **User search:** Find users and organizations
- **Repository search:** Find repos by topic, language

## 🎨 Customization

### README Enhancements
- **Badges:** Build status, version, license
- **Shields.io:** Custom badge creation
- **Markdown features:** Tables, code blocks, images
- **GitHub-flavored markdown:** Task lists, @mentions

### GitHub Pages
1. **Settings → Pages**
2. **Choose source:** Branch (main/gh-pages) or GitHub Actions
3. **Custom domain:** Optional custom domain setup
4. **Themes:** Jekyll themes for documentation

### Repository Topics
- **Add topics:** Help others discover your repo
- **Use relevant keywords:** programming language, framework, purpose
- **Maximum 20 topics:** Choose wisely

## 🔗 Integrations

### Popular GitHub Apps
- **Slack:** Notifications and updates
- **Jira:** Issue tracking integration
- **CodeClimate:** Code quality analysis
- **Dependabot:** Dependency updates
- **Vercel/Netlify:** Deployment platforms

### Webhooks
**Settings → Webhooks:** Send HTTP POST requests on events
- **Push events:** Code changes
- **Pull request events:** PR activities
- **Issue events:** Issue changes
- **Custom payloads:** JSON data about events

## 📈 Best Practices

### Repository Organization
- **Clear README:** Project description, setup instructions
- **Consistent naming:** Use clear, descriptive names
- **Proper branching:** main/develop/feature structure
- **Regular maintenance:** Update dependencies, fix issues

### Community Guidelines
- **Code of Conduct:** Set behavioral expectations
- **Contributing guidelines:** How others can contribute
- **Issue templates:** Standardize bug reports
- **PR templates:** Consistent pull request format

### Security
- **Enable security alerts:** Vulnerability notifications
- **Use secrets:** Never commit sensitive data
- **Regular audits:** Review access permissions
- **Two-factor authentication:** Enable 2FA on your account
