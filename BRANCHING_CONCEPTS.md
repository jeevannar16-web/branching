# Git Branching Concepts - Complete Guide

## Table of Contents
1. [Creating Branches](#1-creating-branches)
2. [Switching Branches](#2-switching-branches)
3. [Viewing Branches](#3-viewing-branches)
4. [Merging Branches](#4-merging-branches)
5. [Fast-Forward Merge](#5-fast-forward-merge)
6. [3-Way Merge](#6-3-way-merge)
7. [Merge Conflicts](#7-merge-conflicts)
8. [Deleting Branches](#8-deleting-branches)
9. [Renaming Branches](#9-renaming-branches)
10. [Cherry-Pick](#10-cherry-pick)
11. [Rebase](#11-rebase)
12. [Stashing](#12-stashing)
13. [Detached HEAD](#13-detached-head)
14. [Remote Branches](#14-remote-branches)
15. [Tracking Branches](#15-tracking-branches)
16. [Branch Comparison](#16-branch-comparison)
17. [Branching Strategies](#17-branching-strategies)

---

## 1. Creating Branches

A branch is a lightweight movable pointer to a commit.

```bash
# Create a new branch
git branch feature-login

# Create and switch to new branch in one step
git checkout -b feature-signup
# OR (newer Git versions)
git switch -c feature-dashboard
```

## 2. Switching Branches

```bash
# Switch to existing branch
git checkout feature-login
# OR
git switch feature-login

# Switch back to main
git checkout main
# OR
git switch main
```

## 3. Viewing Branches

```bash
# List local branches
git branch

# List all branches (local + remote)
git branch -a

# List branches with last commit
git branch -v

# List merged branches
git branch --merged

# List unmerged branches
git branch --no-merged
```

## 4. Merging Branches

Merging brings changes from one branch into another.

```bash
# Switch to target branch first
git checkout main

# Merge feature branch into main
git merge feature-login
```

## 5. Fast-Forward Merge

Occurs when the target branch has no new commits since the feature branch was created.

```bash
# Before merge: A-B-C (main) and D-E (feature, branched from B)
# After merge:  A-B-C-D-E (main, fast-forwarded)
git merge feature-branch
# Result: Linear history, no merge commit created
```

## 6. 3-Way Merge

Occurs when both branches have diverged with new commits.

```bash
# Before merge: A-B-C-D (main) and A-B-E-F (feature)
# After merge:  A-B-C-D-G (main) --- E-F (feature)
# G = merge commit with two parents
git merge feature-branch
# Result: Merge commit created, non-linear history
```

## 7. Merge Conflicts

Conflicts happen when both branches modify the same lines.

```bash
# Git marks conflicts in files:
# <<<<<<< HEAD
# Changes from current branch
# =======
# Changes from incoming branch
# >>>>>>> feature-branch

# Steps to resolve:
# 1. Edit the file to keep desired changes
# 2. Remove conflict markers
# 3. Stage the resolved file
git add <file>
# 4. Complete the merge
git commit
```

## 8. Deleting Branches

```bash
# Delete local branch (safe - only if merged)
git branch -d feature-login

# Force delete local branch (even if unmerged)
git branch -D feature-experimental

# Delete remote branch
git push origin --delete feature-login
# OR
git push origin :feature-login
```

## 9. Renaming Branches

```bash
# Rename current branch
git branch -m new-name

# Rename specific branch
git branch -m old-name new-name

# Force rename (even if new name exists)
git branch -M old-name new-name

# Rename and push to remote
git branch -m feature-v2
git push origin feature-v2
git push origin --delete feature-v1
```

## 10. Cherry-Pick

Apply a specific commit from one branch to another without merging everything.

```bash
# Apply a single commit
git checkout main
git cherry-pick abc1234

# Apply multiple commits
git cherry-pick abc1234 def5678

# Apply without committing (stage changes only)
git cherry-pick --no-commit abc1234

# Cherry-pick a range of commits
git cherry-pick abc1234..ghi7890
```

## 11. Rebase

Reapply commits on top of another base tip. Creates linear history.

```bash
# Rebase current branch onto main
git checkout feature-branch
git rebase main

# Interactive rebase (edit, squash, reorder last 3 commits)
git rebase -i HEAD~3

# Abort rebase
git rebase --abort

# Continue rebase (after resolving conflicts)
git rebase --continue
```

### Merge vs Rebase
```bash
# Merge: preserves history, creates merge commit
# Before: A-B-C-D (main) and A-B-E-F (feature)
# After merge:  A-B-C-D-G (merge) --- E-F

# Rebase: rewrites history, linear
# Before: A-B-C-D (main) and A-B-E-F (feature)
# After rebase: A-B-C-D-E'-F' (feature rebased onto main)
```

## 12. Stashing

Temporarily save uncommitted changes to work on something else.

```bash
# Stash current changes
git stash

# Stash with a message
git stash push -m "WIP: login feature"

# List all stashes
git stash list

# Apply most recent stash (keep in stash list)
git stash apply

# Apply and remove most recent stash
git stash pop

# Apply specific stash
git stash apply stash@{2}

# Drop a specific stash
git stash drop stash@{0}

# Clear all stashes
git stash clear
```

## 13. Detached HEAD

HEAD points directly to a commit instead of a branch tip.

```bash
# Enter detached HEAD (checkout a specific commit)
git checkout abc1234

# Create a branch from detached HEAD
git checkout -b new-branch-from-detached

# Return to a branch
git checkout main
```

## 14. Remote Branches

```bash
# Fetch all remote branches (download but don't merge)
git fetch origin

# Show remote branches
git branch -r

# Show all branches (local + remote)
git branch -a

# Push branch to remote
git push origin feature-login

# Set upstream tracking
git push -u origin feature-login

# Pull (fetch + merge)
git pull origin main

# Pull with rebase
git pull --rebase origin main
```

## 15. Tracking Branches

Local branches that track remote branches.

```bash
# Set tracking for existing branch
git branch --set-upstream-to=origin/feature-login

# Push and set tracking in one step
git push -u origin feature-login

# Show tracking info
git branch -vv

# Remove tracking
git branch --unset-upstream feature-login
```

## 16. Branch Comparison

```bash
# Compare branches
git diff main..feature-login

# Compare branches (show only stats)
git diff --stat main..feature-login

# Compare with branch tip
git diff main...feature-login

# View commit history of a branch
git log feature-login

# View history of branch not in main
git log main..feature-login

# View commit graph
git log --oneline --graph --all
```

## 17. Branching Strategies

### Git Flow
```
main (production)
  |
develop (integration)
  |  \
feature/login  feature/signup
```

### GitHub Flow
```
main
  |  \
feature/login  feature/signup
```

### Trunk-Based Development
```
main (short-lived feature branches)
  |  \
feat/a  feat/b
```

---

## Quick Reference Commands

| Command | Description |
|---------|-------------|
| `git branch <name>` | Create branch |
| `git checkout -b <name>` | Create and switch |
| `git switch -c <name>` | Create and switch (new) |
| `git switch <name>` | Switch branch |
| `git merge <branch>` | Merge branch |
| `git branch -d <name>` | Delete merged branch |
| `git branch -D <name>` | Force delete branch |
| `git cherry-pick <commit>` | Apply specific commit |
| `git rebase <branch>` | Rebase onto branch |
| `git stash` | Stash changes |
| `git stash pop` | Apply and remove stash |
| `git push -u origin <branch>` | Push with tracking |
| `git log --graph --all` | Visual branch history |
