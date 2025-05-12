---
layout: post
title: "How to Use Git & GitHub Like a Pro"
description: "Master Git and GitHub with these advanced tips and workflows for developers."
date: 2025-04-24
tags: [Git, GitHub, version control, tutorial, productivity]
categories: [tools, tutorials, git, productivity]
author: Tech Empire
image: /assets/images/git-github-pro.jpg
---

# How to Use Git & GitHub Like a Pro

Take your version control skills to the next level with these expert tips.

## Introduction

Git and GitHub have revolutionized the way developers collaborate on code. While most developers know the basics—commit, push, pull, and merge—there's a world of advanced techniques that can dramatically improve your workflow. This guide will take you beyond the fundamentals and show you how to use Git and GitHub like a seasoned professional.

## Table of Contents

1. [Advanced Git Commands](#advanced-git-commands)
2. [Efficient Branching Strategies](#efficient-branching-strategies)
3. [Pull Request Best Practices](#pull-request-best-practices)
4. [GitHub Actions Automation](#github-actions-automation)
5. [Git Hooks for Quality Control](#git-hooks-for-quality-control)
6. [Rebasing vs. Merging](#rebasing-vs-merging)
7. [Managing Large Repositories](#managing-large-repositories)
8. [Security Best Practices](#security-best-practices)
9. [Advanced GitHub Features](#advanced-github-features)
10. [Troubleshooting Common Issues](#troubleshooting-common-issues)

## Advanced Git Commands

### Interactive Rebase

One of the most powerful features of Git is the ability to rewrite history using interactive rebase:

```bash
git rebase -i HEAD~5  # Rebase the last 5 commits
```

This opens an editor where you can:
- Reorder commits
- Edit commit messages
- Squash multiple commits into one
- Drop commits entirely

### Cherry-Pick

Need to apply a specific commit from one branch to another? Cherry-pick is your friend:

```bash
git cherry-pick 789abcd  # Apply the specific commit to your current branch
```

### Git Reflog

Ever lost a commit or accidentally reset? Git reflog is your safety net:

```bash
git reflog  # Shows a log of all Git operations
git checkout HEAD@{2}  # Go back to where you were 2 operations ago
```

### Git Bisect

Find which commit introduced a bug with binary search:

```bash
git bisect start
git bisect bad  # Current commit is broken
git bisect good 789abcd  # Last known good commit
# Git will check out commits for you to test
# After testing, mark each as good or bad until it finds the culprit
git bisect good  # or git bisect bad
```

## Efficient Branching Strategies

### GitFlow

GitFlow is a robust branching model for managing larger projects:

- **Main branch**: Production code
- **Develop branch**: Integration branch for features
- **Feature branches**: For new features
- **Release branches**: Preparing for a release
- **Hotfix branches**: Emergency fixes for production

### GitHub Flow

For teams deploying continuously, GitHub Flow offers a simpler approach:

1. Create a branch from main
2. Add commits
3. Open a pull request
4. Review and discuss
5. Merge to main and deploy

### Trunk-Based Development

For mature teams with strong testing practices:

- Most work happens in the main branch
- Short-lived feature branches
- Feature flags for incomplete work
- Requires robust CI/CD and testing

## Pull Request Best Practices

### Title and Description

- Write clear, descriptive PR titles
- Include a detailed description explaining:
  - Why the change is needed
  - How it addresses the issue
  - Any potential risks or side effects

### PR Size

- Keep PRs focused and small (ideally <300 lines of code)
- One logical change per PR
- Break large features into smaller, sequential PRs

### Code Review Guidelines

- Be specific and constructive in comments
- Use GitHub's suggestion feature for minor changes
- Look for:
  - Logic errors
  - Security issues
  - Performance concerns
  - Test coverage
  - Documentation

### PR Templates

Create a `.github/PULL_REQUEST_TEMPLATE.md` file:

```markdown
## Description
[Describe your changes here]

## Related Issue
Fixes #[issue number]

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## How Has This Been Tested?
[Describe your test approach]

## Checklist
- [ ] My code follows the project's style guidelines
- [ ] I have performed a self-review
- [ ] I have added tests that prove my fix is effective or my feature works
- [ ] Documentation has been updated
```

## GitHub Actions Automation

### CI/CD Pipeline

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main, develop ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: 18
    - name: Install dependencies
      run: npm ci
    - name: Run tests
      run: npm test
    - name: Run linting
      run: npm run lint
```

### Automated Dependency Updates

Implement Dependabot by creating `.github/dependabot.yml`:

```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 10
```

### Custom GitHub Actions

Create a reusable action for your common workflows:

```yaml
# .github/actions/custom-lint/action.yml
name: 'Custom Linting'
description: 'Run project-specific linting rules'
runs:
  using: 'composite'
  steps:
    - run: npm run custom-lint
      shell: bash
```

## Git Hooks for Quality Control

### Pre-commit Hooks

Set up pre-commit hooks to run automatically before each commit:

```bash
# .git/hooks/pre-commit
#!/bin/sh

npm run lint
npm run format
npm run test:quick
```

For team-wide hooks, use Husky:

```json
// package.json
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "pre-push": "npm test"
    }
  },
  "lint-staged": {
    "*.js": ["eslint --fix", "prettier --write"],
    "*.css": ["stylelint --fix"]
  }
}
```

### Commit Message Validation

Enforce conventional commit messages:

```bash
# .git/hooks/commit-msg
#!/bin/sh

commit_msg=$(cat "$1")
pattern='^(feat|fix|docs|style|refactor|test|chore)(\(.+\))?: .+'

if ! echo "$commit_msg" | grep -qE "$pattern"; then
  echo "Error: Commit message doesn't follow conventional commits format"
  exit 1
fi
```

## Rebasing vs. Merging

### When to Merge

- When maintaining the exact history is important
- For merging feature branches into main/develop
- When the branch is already shared publicly

```bash
git checkout main
git merge feature/new-component
```

### When to Rebase

- To keep a clean, linear history
- Before submitting a PR to update with latest changes
- For local branches that aren't shared

```bash
git checkout feature/new-component
git rebase main  # Reapply your branch's commits on top of main
```

### Interactive Rebasing for Clean History

```bash
git checkout feature/new-component
git rebase -i main
```

This allows you to:
- Squash related commits
- Reword commit messages
- Drop unnecessary commits

## Managing Large Repositories

### Git LFS (Large File Storage)

For repositories with large binary files:

```bash
# Initialize Git LFS
git lfs install

# Track large file types
git lfs track "*.psd"
git lfs track "*.zip"

# Add .gitattributes
git add .gitattributes

# Commit and push as normal
git add image.psd
git commit -m "Add design file"
git push
```

### Partial Clones

For huge repos, clone only what you need:

```bash
# Exclude specific directories
git clone --filter=blob:none --sparse https://github.com/user/repo.git
cd repo
git sparse-checkout set dir1 dir2

# Or exclude only large files
git clone --filter=blob:limit=1m https://github.com/user/repo.git
```

### Shallow Clones

When you only need recent history:

```bash
git clone --depth=1 https://github.com/user/repo.git
```

## Security Best Practices

### Secret Detection

Use pre-commit hooks to prevent secrets from being committed:

```bash
# .git/hooks/pre-commit
#!/bin/sh

# Check for AWS keys
if git diff --cached | grep -E 'AKIA[0-9A-Z]{16}'; then
  echo "Error: AWS key detected in commit"
  exit 1
fi

# Check for private keys
if git diff --cached | grep -E '\-\-\-\-\-BEGIN PRIVATE KEY'; then
  echo "Error: Private key detected in commit"
  exit 1
fi
```

### Signed Commits

Set up GPG signing to verify commit authenticity:

```bash
# Generate a GPG key
gpg --full-generate-key

# Configure Git to use your key
git config --global user.signingkey YOUR_KEY_ID
git config --global commit.gpgsign true

# Sign commits
git commit -S -m "Signed commit message"
```

### Branch Protection Rules

In GitHub repository settings:

1. Require pull request reviews
2. Require status checks to pass
3. Require signed commits
4. Enforce linear history
5. Include administrators in restrictions

## Advanced GitHub Features

### GitHub Codespaces

Launch a complete development environment directly from your repository:

1. Click the "Code" button on your repository
2. Select "Open with Codespaces"
3. Create a new codespace

Customize with a `.devcontainer/devcontainer.json` file:

```json
{
  "image": "mcr.microsoft.com/vscode/devcontainers/typescript-node:16",
  "extensions": [
    "dbaeumer.vscode-eslint",
    "esbenp.prettier-vscode"
  ],
  "forwardPorts": [3000],
  "postCreateCommand": "npm install"
}
```

### GitHub Advanced Security

Enable security features:

1. **Dependabot alerts**: Automatic vulnerability scanning
2. **Code scanning**: Static analysis with CodeQL
3. **Secret scanning**: Identify tokens and keys in your code

### GitHub Issues Automation

Create issue templates in `.github/ISSUE_TEMPLATE/`:

```yaml
# .github/ISSUE_TEMPLATE/bug_report.yml
name: Bug Report
description: File a bug report
body:
  - type: markdown
    attributes:
      value: Thanks for taking the time to fill out this bug report!
  - type: textarea
    id: what-happened
    attributes:
      label: What happened?
      description: Also tell us, what did you expect to happen?
    validations:
      required: true
  - type: dropdown
    id: browsers
    attributes:
      label: What browsers are you seeing the problem on?
      multiple: true
      options:
        - Chrome
        - Firefox
        - Safari
        - Edge
```

## Troubleshooting Common Issues

### Fixing Merge Conflicts

```bash
# During merge conflict
git status  # See which files are conflicted
# Edit files to resolve conflicts
git add <resolved-files>
git merge --continue  # Or git rebase --continue
```

### Recovering Lost Work

```bash
# Find lost commits
git reflog

# Restore a deleted branch
git checkout -b recovered-branch <commit-hash>

# Recover uncommitted changes
git fsck --lost-found
```

### Fixing Broken Commits

```bash
# Fix the last commit
git commit --amend

# Fix an older commit
git rebase -i <commit>^
# Mark the commit as "edit", make changes
git commit --amend
git rebase --continue
```

### Cleaning Up

```bash
# Clean untracked files
git clean -fd

# Remove stale remote-tracking branches
git remote prune origin

# Garbage collection
git gc --aggressive
```

## Conclusion

Mastering Git and GitHub is a journey, not a destination. By incorporating these advanced techniques into your workflow, you'll not only improve your own productivity but also become a more valuable contributor to any development team.

Remember that the best Git workflow is the one that works for your team and project. Don't be afraid to adapt these techniques to fit your specific needs.

## Further Resources

- [Pro Git Book](https://git-scm.com/book/en/v2) - Free comprehensive guide
- [GitHub Skills](https://skills.github.com/) - Interactive courses
- [Git Flight Rules](https://github.com/k88hudson/git-flight-rules) - Guide for what to do when things go wrong
- [Oh Shit, Git!?](https://ohshitgit.com/) - Quick fixes for common mistakes

Happy coding, and may your repositories always be conflict-free!