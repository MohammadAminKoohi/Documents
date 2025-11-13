
2024-10-08 12:05

Tags: 

---

# Git Documentation for Software Engineers

## Introduction
Git is a distributed version control system that helps track changes in code, collaborate with others, and maintain a history of your project. It is essential for managing software development.

## Basic Git Setup

### Configuring Git
Before using Git, configure your user details:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

To verify the configuration:
```bash
git config --list
```

## Common Git Commands

### Initialize a Git Repository
```bash
git init
```
Initializes a new Git repository in the current directory.

### Clone a Repository
```bash
git clone <repository-url>
```
Clones a remote repository to your local machine.

### Check Repository Status
```bash
git status
```
Shows the status of changes in your working directory.

### Add Changes to Staging Area
```bash
git add <file>          # Adds a specific file
git add .               # Adds all modified and untracked files
```

### Commit Changes
```bash
git commit -m "Commit message"
```
Commits changes in the staging area with a message. Use meaningful commit messages.

### View Commit History
```bash
git log
```
Displays commit history.

- **Important Flags:**
  - `--oneline`: Shows one line per commit.
  - `--graph`: Shows the commit graph visually.

### Push Changes to Remote Repository
```bash
git push <remote> <branch>
```
Pushes your commits to a remote repository, such as `origin main`.

### Pull Changes from Remote Repository
```bash
git pull <remote> <branch>
```
Pulls and merges changes from a remote repository into your current branch.

### Create a New Branch
```bash
git branch <branch-name>
```
Creates a new branch.

### Switch to a Branch
```bash
git checkout <branch-name>
```
Switches to an existing branch.

Alternatively, for newer versions:
```bash
git switch <branch-name>
```

### Create and Switch to a New Branch
```bash
git checkout -b <branch-name>
```
Or, using `switch`:
```bash
git switch -c <branch-name>
```

### Merge a Branch
```bash
git merge <branch-name>
```
Merges the specified branch into your current branch.

### Delete a Branch
```bash
git branch -d <branch-name>   # Deletes a merged branch
git branch -D <branch-name>   # Forcefully deletes an unmerged branch
```

## Stashing Changes

### Save Uncommitted Changes for Later
```bash
git stash
```
Stores your uncommitted changes for later use.

### Apply Stashed Changes
```bash
git stash apply
```
Applies the most recent stash.

### List Stashed Changes
```bash
git stash list
```

### Drop a Stash
```bash
git stash drop
```

## Undoing Changes

### Undo Last Commit (Keep Changes)
```bash
git reset --soft HEAD^
```

### Undo Last Commit (Discard Changes)
```bash
git reset --hard HEAD^
```

### Discard Unstaged Changes
```bash
git checkout -- <file>
```
Reverts changes in a file to the last committed state.

### Revert a Commit (Without Losing History)
```bash
git revert <commit-hash>
```
Creates a new commit that undoes the specified commit.

## Working with Remotes

### Add a Remote Repository
```bash
git remote add <name> <repository-url>
```

### List Remote Repositories
```bash
git remote -v
```

### Remove a Remote Repository
```bash
git remote remove <name>
```

### Rename a Remote
```bash
git remote rename <old-name> <new-name>
```

## Tagging

### Create a Tag
```bash
git tag <tag-name>
```

### View All Tags
```bash
git tag
```

### Push Tags to Remote
```bash
git push <remote> <tag-name>   # Pushes a specific tag
git push --tags                # Pushes all tags
```

## Rebase

### Rebase Current Branch on Another Branch
```bash
git rebase <branch>
```
Moves your current branch's commits to the tip of the specified branch.

### Continue a Rebase After Conflict Resolution
```bash
git rebase --continue
```

## Working with Conflicts

When merging or rebasing, conflicts might occur. Resolve conflicts by manually editing the conflicting files, then add them and complete the process.

### Abort a Merge
```bash
git merge --abort
```

### Abort a Rebase
```bash
git rebase --abort
```

## Git Ignore

### Ignore Files with `.gitignore`
To ignore files from being tracked, create a `.gitignore` file in the root directory and list the files or directories you want to ignore. Example:
```
# Ignore log files
*.log

# Ignore node_modules
node_modules/
```

## Git Bisect (Debugging Tool)

### Start Bisecting
```bash
git bisect start
```

### Mark Commit as Bad
```bash
git bisect bad
```

### Mark Commit as Good
```bash
git bisect good <commit-hash>
```

### Reset Bisecting Process
```bash
git bisect reset
```

## Useful Flags and Options

| Flag                | Usage                                                           |
| ------------------- | ----------------------------------------------------------------|
| `-a`                | Add all files when committing (`git commit -a`).                |
| `--amend`           | Modify the most recent commit (`git commit --amend`).           |
| `-m`                | Provide a commit message (`git commit -m "message"`).           |
| `-u`                | Only add updated files (`git add -u`).                          |
| `-p`                | Interactively choose hunks of changes (`git add -p`).           |
| `--no-ff`           | Force a merge commit (`git merge --no-ff`).                     |

