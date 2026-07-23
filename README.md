# Git Branching Concepts

A comprehensive guide and demo repository for learning Git branching concepts.

## What's Included

### Documentation
- **[BRANCHING_CONCEPTS.md](BRANCHING_CONCEPTS.md)** - Complete guide covering 17 branching concepts
- **[BRANCHING_STRATEGIES.md](BRANCHING_STRATEGIES.md)** - Popular branching strategies

### Key Concepts Covered
| Concept | Description |
|---------|-------------|
| Creating Branches | `git branch`, `git checkout -b` |
| Switching Branches | `git checkout`, `git switch` |
| Merging | Fast-forward & 3-way merge |
| Merge Conflicts | How to resolve conflicts |
| Cherry-Pick | Apply specific commits |
| Rebase | Reapply commits on new base |
| Stashing | Temporarily save changes |
| Deleting Branches | Safe and force delete |
| Renaming Branches | `git branch -m` |
| Remote Branches | Push, pull, fetch |
| Tracking Branches | Link local to remote |
| Branch Comparison | `git diff`, `git log` |

## Quick Start

```bash
# Clone the repository
git clone https://github.com/jeevannar16-web/branching.git

# Check out the guide
cat BRANCHING_CONCEPTS.md

# Try the commands yourself
git branch feature-test
git checkout feature-test
echo "Hello" > test.txt
git add . && git commit -m "Test"
git checkout main
git merge feature-test
git branch -d feature-test
```

## Files Overview
- `first.txt` - Original file with branch demo content
- `two.txt` - Demonstrates merge conflict resolution
- `third.cpp` - Original C++ file
- `feature-login.txt` - Feature branch demo
- `feature-signup.txt` - 3-way merge demo
- `cherry-pick-file1.txt` - Cherry-pick demo
- `rebase-demo.txt` - Rebase demo
- `stash-demo.txt` - Stash demo

## License
Free to use for learning purposes.
