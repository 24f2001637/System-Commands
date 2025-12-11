# The Ultimate Git and GitHub Mastery Guide
## From Absolute Beginner to Expert

---

## Table of Contents

1. [Introduction](#introduction)
2. [Installation and Setup](#installation-and-setup)
3. [Git Basics and Core Concepts](#git-basics-and-core-concepts)
4. [Daily Workflow — The Essentials](#daily-workflow--the-essentials)
5. [Branching and Merging](#branching-and-merging)
6. [Rewriting History and Undoing Things](#rewriting-history-and-undoing-things)
7. [Remote Repositories and Collaboration](#remote-repositories-and-collaboration)
8. [Inspection and Debugging](#inspection-and-debugging)
9. [Stashing and Cleaning](#stashing-and-cleaning)
10. [Advanced Topics](#advanced-topics)
11. [Workflows and Best Practices](#workflows-and-best-practices)
12. [Cheat Sheets](#cheat-sheets)
13. [Troubleshooting Common Issues](#troubleshooting-common-issues)
14. [Exercises and Projects](#exercises-and-projects)
15. [Further Learning](#further-learning)

---

## 1. Introduction

### What is Version Control and Why It Matters

**Version control** is a system that tracks and manages changes to files over time. Imagine working on a document and being able to see every edit ever made — who made it, when, and why. Now imagine being able to revert to any previous version instantly, or see exactly what changed between two points in time. That's version control.

In software development, version control is indispensable because:

- **Collaboration**: Multiple developers can work on the same project without overwriting each other's code
- **History**: Every change is recorded with context (who made it, when, why)
- **Experimentation**: You can create branches to try new features without affecting the main project
- **Accountability**: Each change is attributed to a developer, creating responsibility
- **Safety**: You can recover from mistakes by reverting to previous states
- **Integration**: Version control enables continuous integration and deployment pipelines

### Centralized vs Distributed Version Control Systems

There are two main paradigms in version control:

#### Centralized VCS (e.g., SVN, Perforce)

```
        ┌─────────────────────┐
        │  Central Repository │
        │    (Single source   │
        │    of truth)        │
        └──────────┬──────────┘
                   │
        ┌──────────┼──────────┐
        │          │          │
    Developer 1 Dev 2    Developer 3
```

- Single central server holds the entire history
- Developers check out working copies, make changes, commit back
- Network connectivity required for most operations
- Single point of failure

#### Distributed VCS (e.g., Git, Mercurial)

```
    ┌──────────────┐  ┌──────────────┐  ┌──────────────┐
    │   Dev 1      │  │    Dev 2     │  │   Dev 3      │
    │  Local Repo  │  │  Local Repo  │  │  Local Repo  │
    └──────┬───────┘  └──────┬───────┘  └──────┬───────┘
           │                 │                 │
           └─────────────────┼─────────────────┘
                             │
                    ┌────────▼────────┐
                    │  Central Repo   │
                    │   (GitHub, etc) │
                    └─────────────────┘
```

- Every developer has a complete copy of the repository
- Works offline; syncs when connected
- No single point of failure
- More powerful and flexible

**Git is a distributed VCS**, which is why it's become the industry standard.

### Why Git is the Industry Standard

Git dominates the version control landscape because of several key advantages:

1. **Distributed Architecture**: Full repository on every developer's machine
2. **Performance**: Fast operations (branching, merging, viewing history)
3. **Powerful Branching**: Creating and merging branches is lightweight and fast
4. **Data Integrity**: SHA-1 hashing ensures no accidental corruption
5. **Staging Area**: Intermediate step between working directory and commit (unique advantage)
6. **Flexibility**: Supports multiple workflows and integration strategies
7. **Open Source**: Free, transparent, community-driven
8. **Industry Adoption**: Used by major tech companies, startups, and open-source projects worldwide

### Git vs GitHub vs GitLab/Bitbucket (Brief Overview)

| Term | What It Is | Purpose |
|------|-----------|---------|
| **Git** | Version control system (software) | Tracks file changes, manages repositories locally and remotely |
| **GitHub** | Hosting platform + social features | Hosts Git repositories in the cloud; adds pull requests, issues, actions, discussions, community features |
| **GitLab** | Self-hosted or cloud platform | Alternative to GitHub; emphasizes DevOps, CI/CD pipelines; can be self-hosted |
| **Bitbucket** | Cloud platform by Atlassian | GitHub alternative; integrates with Jira; Mercurial support |

**Key distinction**: Git is the tool; GitHub/GitLab/Bitbucket are platforms where you host Git repositories and collaborate.

This guide focuses primarily on Git (the tool) with GitHub examples for remote operations. The concepts transfer to other platforms.

---

## 2. Installation and Setup

### Installing Git on Windows

#### Method 1: Git for Windows (Recommended)

1. Visit https://git-scm.com/download/win
2. Download the installer (latest version)
3. Run the installer and follow the setup wizard
4. **Key options to select**:
   - **Use Git Bash** (recommended for command-line interface)
   - **Use Git from the Windows Command Prompt** (if you prefer CMD)
   - **Configuring line endings**: Select "Checkout as-is, commit as-is" (for cross-platform compatibility)
5. Complete installation

#### Method 2: Windows Package Manager

```bash
winget install --id Git.Git -e --latest
```

#### Method 3: Chocolatey

```bash
choco install git
```

#### Verification

```bash
git --version
```

Expected output:
```
git version 2.45.0.windows.1
```

### Installing Git on macOS

#### Method 1: Homebrew (Recommended)

```bash
brew install git
```

#### Method 2: Official Installer

1. Visit https://git-scm.com/download/mac
2. Download and run the installer

#### Method 3: Xcode Command Line Tools

```bash
xcode-select --install
```

#### Verification

```bash
git --version
```

### Installing Git on Linux

#### Debian/Ubuntu

```bash
sudo apt-get update
sudo apt-get install git
```

#### Fedora/RHEL/CentOS

```bash
sudo dnf install git
```

#### Arch Linux

```bash
sudo pacman -S git
```

#### Verification

```bash
git --version
```

### Configuring Git

After installation, configure Git with your identity. This information is attached to every commit you make.

#### Setting User Name and Email

```bash
git config --global user.name "Your Full Name"
git config --global user.email "your.email@example.com"
```

The `--global` flag sets configuration for your entire system. For project-specific configuration, omit `--global`:

```bash
git config user.name "Project-Specific Name"
```

#### Setting Your Default Editor

Git uses a text editor for commit messages and interactive commands. Configure your preferred editor:

```bash
# VS Code
git config --global core.editor "code --wait"

# Vim
git config --global core.editor "vim"

# Nano
git config --global core.editor "nano"

# Sublime Text
git config --global core.editor "subl -n -w"
```

#### Viewing Your Configuration

```bash
# View all settings
git config --global --list

# View a specific setting
git config user.name
```

#### Creating Useful Aliases

Aliases allow you to create shortcuts for frequently used commands:

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'restore --staged'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --graph --oneline --all'
```

### Setting Up SSH Keys for GitHub

SSH keys provide secure authentication without entering your password repeatedly.

#### Step 1: Generate an SSH Key Pair

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

When prompted:
- Press Enter to accept the default location (`~/.ssh/id_ed25519`)
- Enter a passphrase (optional but recommended for security)

For older systems that don't support Ed25519, use RSA:

```bash
ssh-keygen -t rsa -b 4096 -C "your.email@example.com"
```

#### Step 2: Start the SSH Agent

```bash
# On macOS and Linux
eval "$(ssh-agent -s)"

# On Windows (Git Bash)
eval $(ssh-agent -s)
```

Expected output:
```
Agent pid 12345
```

#### Step 3: Add Your SSH Key to the Agent

```bash
ssh-add ~/.ssh/id_ed25519
```

#### Step 4: Copy Your Public Key

```bash
# macOS
pbcopy < ~/.ssh/id_ed25519.pub

# Linux
cat ~/.ssh/id_ed25519.pub | xclip -selection clipboard

# Windows (Git Bash)
cat ~/.ssh/id_ed25519.pub | clip
```

#### Step 5: Add the Key to GitHub

1. Log in to GitHub
2. Go to **Settings** → **SSH and GPG keys**
3. Click **New SSH key**
4. Give it a descriptive title (e.g., "MacBook Pro")
5. Paste your public key
6. Click **Add SSH key**

#### Step 6: Test the Connection

```bash
ssh -T git@github.com
```

Expected output:
```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

### Verifying Installation

Create a test repository to verify everything works:

```bash
# Create a test directory
mkdir test-repo
cd test-repo

# Initialize repository
git init

# Check Git is working
git status

# Expected output:
# On branch master (or main)
# No commits yet
# nothing to commit (create/copy files and use "git add" to track)
```

Everything is now configured and ready to use!

---

## 3. Git Basics and Core Concepts

### Creating a Repository

#### Initializing a New Repository (git init)

```bash
git init
```

This command creates a new `.git` directory in your current folder. This hidden directory contains all the metadata Git needs to track your project.

**Example:**
```bash
$ mkdir my-project
$ cd my-project
$ git init
Initialized empty Git repository in /Users/john/my-project/.git/
```

#### Cloning an Existing Repository (git clone)

```bash
git clone <repository-url> [directory-name]
```

Cloning downloads an entire repository (all history, all branches) to your machine.

**Examples:**
```bash
# Clone with default directory name
git clone https://github.com/torvalds/linux.git

# Clone into a specific directory
git clone https://github.com/torvalds/linux.git my-linux-fork

# Clone using SSH (faster, more secure)
git clone git@github.com:torvalds/linux.git
```

### The Three States: Working Directory, Staging Area, Repository

This is Git's most important concept. Every file in your repository exists in one of three states:

```
┌─────────────────────────────────────────────────────────────┐
│                    Your Computer                            │
├──────────────────┬──────────────────┬──────────────────────┤
│ Working          │  Staging Area    │  Repository (.git)   │
│ Directory        │  (Index)         │  (Committed History) │
│                  │                  │                      │
│ Your actual      │ Changes ready    │ Permanent snapshots  │
│ files that you   │ to be committed  │ of your project      │
│ edit             │ (staging area)   │                      │
│                  │                  │                      │
│ git status       │ git add          │ git commit           │
│ git diff         │ git reset        │ git log              │
│ git restore      │                  │ git show             │
└──────────────────┴──────────────────┴──────────────────────┘
          ↓              ↓                      ↓
      Modified       Staged              Committed
```

**Workflow Example:**

```bash
# 1. Create/modify a file in Working Directory
echo "Hello World" > hello.txt

# 2. Check status (Working Directory has changes)
git status
# On branch main
# Untracked files:
#   hello.txt

# 3. Stage the file (move to Staging Area)
git add hello.txt

git status
# On branch main
# Changes to be committed:
#   new file:   hello.txt

# 4. Commit (move from Staging Area to Repository)
git commit -m "Add hello.txt"

git status
# On branch main
# nothing to commit, working tree clean
```

### Git Objects Internals: Blobs, Trees, Commits, and Tags

Git stores everything using four fundamental object types, identified by SHA-1 hashes:

#### 1. Blob (Binary Large Object)

A blob represents the **content of a single file** at a specific point in time. It doesn't store the filename — just the file's content.

```
SHA-1 Hash: e965047ad7612cba098dd41cb6982204ec77e3ce

Content:
Hello, World!
```

**Key point**: The same file content always produces the same hash. Different content = different hash.

#### 2. Tree

A tree is a snapshot of a **directory structure at a point in time**. It's a list of blobs and other trees with their filenames.

```
SHA-1 Hash: c1d7e8f4a9c3b2e1f5d8a7c4e9b2f5d8

Tree contents:
100644 blob e965047ad7 hello.txt
100644 blob f7c8b3a9d2 README.md
040000 tree a1b2c3d4e5 src/
```

**Key point**: A tree defines the folder structure and file organization at a moment in time.

#### 3. Commit

A commit is a snapshot of your **entire repository at a point in time**. It contains:
- Reference to a tree (the project state)
- Reference to parent commit(s) (the previous snapshot)
- Commit metadata (author, committer, timestamp, message)

```
SHA-1 Hash: abc123def456

Commit object:
tree c1d7e8f4a9c3b2e1f5d8a7c4e9b2f5d8
parent 0d1e2f3a4b5c6d7e8f9a0b1c2d3e4f5a
author John Doe <john@example.com> 1609459200 +0000
committer John Doe <john@example.com> 1609459200 +0000

Initial commit: Add project structure and README
```

**Key point**: Each commit is immutable and connected to its predecessors, forming a chain of history.

#### 4. Tag

A tag is a **named reference to a specific commit**. There are two types:

**Lightweight Tag**: Just a pointer to a commit
```
refs/tags/v1.0 → abc123def456
```

**Annotated Tag**: A full object with metadata (tagger, date, message)
```
SHA-1 Hash: tag123abc456

Annotated tag object:
object abc123def456
type commit
tag v1.0
tagger Jane Developer <jane@example.com> 1609545600 +0000

Version 1.0 release
```

### Git Objects Diagram

```
Commit History:
┌─────────────────────────────────────────────────────────┐
│ Commit abc123 (HEAD)                                    │
│ ├─ Tree: c1d7e8f (Project snapshot)                    │
│ │  ├─ Blob: e965047 (hello.txt content)               │
│ │  └─ Blob: f7c8b3a (README.md content)               │
│ ├─ Parent: 0d1e2f3                                      │
│ └─ Message: "Initial commit"                           │
└─────────────────────────────────────────────────────────┘
                       ↑ points to
┌─────────────────────────────────────────────────────────┐
│ Commit 0d1e2f3                                          │
│ ├─ Tree: a1b2c3d                                       │
│ ├─ Parent: (none - root commit)                        │
│ └─ Message: "Add basic setup"                          │
└─────────────────────────────────────────────────────────┘
```

### Refs: HEAD, Branches, and Tags

A **ref** is a human-readable pointer to a commit hash. Git uses refs to track where you are in the repository.

#### HEAD

`HEAD` is the **currently checked out commit**. It's your "you are here" marker.

```bash
# Most of the time, HEAD points to a branch
HEAD → main → abc123def456 (the actual commit)

# Sometimes, HEAD points directly to a commit (detached HEAD state)
HEAD → abc123def456
```

View where HEAD is pointing:

```bash
cat .git/HEAD
# ref: refs/heads/main

# When detached:
cat .git/HEAD
# abc123def456
```

#### Branches

A branch is a **movable pointer to a commit**. When you create a new commit, the branch pointer automatically moves forward.

```bash
# Create a branch (points to current commit)
git branch feature-login

# This creates:
# refs/heads/feature-login → abc123def456

# Switch to that branch
git checkout feature-login

# Make a new commit
git commit -m "Add login form"

# Branch pointer automatically moves:
# refs/heads/feature-login → xyz789uvw012
```

**Branch Structure:**
```
main           feature-login      bugfix-404
  │                 │                │
  ▼                 ▼                ▼
[abc123]      [def456]            [ghi789]
   ▲
   │
  HEAD
```

#### Tags

Tags are **immovable references to commits** (unlike branches). They're typically used for releases.

```bash
# Lightweight tag
git tag v1.0

# Creates:
# refs/tags/v1.0 → abc123def456 (immovable)

# Annotated tag
git tag -a v1.0 -m "Version 1.0 release"
```

### The .git Directory Structure

The `.git` directory is the heart of your repository. Understanding its structure demystifies Git:

```
.git/
├── HEAD                 # Points to current branch
├── config              # Project-specific configuration
├── description         # Repository description (GitHub only)
├── hooks/              # Git hooks scripts
│   ├── pre-commit
│   └── post-commit
├── info/               # Additional info (e.g., .gitignore local overrides)
│   └── exclude
├── objects/            # All Git objects (blobs, trees, commits, tags)
│   ├── ab/
│   ├── cd/
│   └── pack/           # Compressed objects (for efficiency)
├── refs/               # References (branches, tags, remotes)
│   ├── heads/          # Local branches
│   │   ├── main
│   │   └── feature-login
│   ├── tags/           # Tags
│   │   └── v1.0
│   └── remotes/        # Remote tracking branches
│       └── origin/
│           ├── main
│           └── feature-login
├── logs/               # Reflog (history of ref changes)
│   ├── HEAD
│   └── refs/
└── index               # Staging area (which files are staged)
```

**Key files:**

- **HEAD**: Contains `ref: refs/heads/main` (or a commit hash if detached)
- **config**: Your project's Git settings
- **objects/**: The database of all Git objects
- **refs/**: Pointers to commits
- **index**: The staging area

**View actual objects:**

```bash
# List all objects
ls .git/objects

# View object content (where abc is a commit hash)
git cat-file -p abc123def456
```

---

## 4. Daily Workflow — The Essentials

### Checking Repository Status (git status)

```bash
git status
```

This command shows:
- Current branch
- Tracked vs untracked files
- Staged vs unstaged changes
- Whether you're ahead of the remote

**Example output:**
```
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   hello.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        debug.log
        temp.txt

nothing added to commit but untracked files present (working tree dirty)
```

**Useful variants:**
```bash
git status --short      # Compact output
git status --porcelain  # Machine-readable format
```

### Staging Changes (git add)

```bash
git add <file>          # Stage specific file
git add .               # Stage all changes
git add *.txt           # Stage all .txt files
git add src/            # Stage entire directory
```

**Understanding staging:**

```bash
# Create a file
echo "version 1" > app.txt

# View status
git status
# Untracked files: app.txt

# Stage it
git add app.txt

git status
# Changes to be committed: app.txt

# Modify it again
echo "version 2" > app.txt

git status
# Changes to be committed: app.txt (version 1)
# Changes not staged for commit: app.txt (version 2)
```

This shows staging is a **separate step**. You can modify files after staging without affecting the staged version.

**Interactive staging:**

```bash
git add -p             # Choose changes interactively (patch mode)
```

This lets you select which parts of a file to stage:

```
Stage this hunk [y,n,q,a,d,s,e,?]?
```

Options:
- `y`: Stage this hunk
- `n`: Don't stage this hunk
- `s`: Split into smaller hunks
- `a`: Stage all remaining hunks

### Committing Changes (git commit)

```bash
git commit -m "Commit message"
```

A commit is a permanent snapshot of your project. Write meaningful messages!

#### Commit Message Guidelines

Follow these conventions for professional, readable commit histories:

**Format:**
```
<type>(<scope>): <subject>

<body>

<footer>
```

**Example 1 — Simple commit:**
```bash
git commit -m "Fix login button alignment"
```

**Example 2 — Detailed commit:**
```bash
git commit -m "Add user authentication

- Implement JWT token generation
- Add password hashing with bcrypt
- Create login and signup endpoints

Fixes #245"
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, semicolons)
- `refactor`: Code restructuring without changing behavior
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `chore`: Build, CI, dependency updates

**Guidelines:**
- Keep subject lines under 50 characters
- Use imperative mood ("Add feature" not "Added feature")
- Don't end the subject line with a period
- Separate subject from body with a blank line
- Wrap body at 72 characters
- Reference issues and pull requests when applicable

**Amending the last commit:**

```bash
# Change commit message
git commit --amend -m "New message"

# Add forgotten changes
git add forgotten-file.txt
git commit --amend --no-edit
```

⚠️ **Warning**: Only amend unpushed commits. Amending changes the commit hash, causing conflicts if others have based work on it.

### Understanding .gitignore

`.gitignore` tells Git which files to ignore (don't track).

#### Creating a .gitignore File

```bash
# Create in repository root
nano .gitignore
```

#### Common Patterns

```
# Ignore specific files
debug.log
*.log

# Ignore directories
node_modules/
dist/
build/

# Ignore all .env files
.env
.env.local
.env.*.local

# Ignore OS files
.DS_Store
Thumbs.db

# Ignore IDE files
.vscode/
.idea/
*.swp
*.swo

# Negation (don't ignore exception)
!important.log
```

#### Pattern Rules

| Pattern | Matches |
|---------|---------|
| `*.log` | All files ending in `.log` |
| `debug.log` | Specific file `debug.log` |
| `logs/` | Directory named `logs` |
| `logs/**` | Everything in `logs` directory |
| `*.log` | Files in any directory |
| `/file.txt` | File in root only |
| `file?.txt` | `file1.txt`, `file2.txt`, etc. |
| `!important.log` | Exception — don't ignore this |

#### Checking What's Ignored

```bash
git check-ignore -v <filename>
```

#### Applying .gitignore to Tracked Files

```bash
# Remove file from Git (keep local copy)
git rm --cached <file>

# Remove entire directory
git rm -r --cached <directory>

# Then commit
git commit -m "Remove tracked files from Git"
```

### Viewing Changes (git diff)

#### Unstaged Changes

```bash
git diff
```

Shows changes in the working directory that haven't been staged.

**Example output:**
```diff
diff --git a/hello.txt b/hello.txt
index e965047..abc1234 100644
--- a/hello.txt
+++ b/hello.txt
@@ -1 +1,2 @@
 Hello, World!
+This is a new line
```

#### Staged Changes

```bash
git diff --staged
```

Shows changes in the staging area (what will be committed).

#### Changes Between Commits

```bash
git diff <commit1> <commit2>
git diff main feature-branch
git diff HEAD~2 HEAD
```

#### Changes to Specific File

```bash
git diff <file>
git diff --staged <file>
```

#### Word-level Diff

```bash
git diff --word-diff
```

Shows differences at word level instead of line level.

**Example:**
```diff
This is a [-new-]{+modified+} line
```

#### Larger Diff Statistics

```bash
git diff --stat
```

Shows summary of files changed and line counts:

```
hello.txt | 3 ++-
README.md | 10 +++++-----
 2 files changed, 8 insertions(+), 5 deletions(-)
```

---

## 5. Branching and Merging

### Creating and Switching Branches

#### Creating a Branch

```bash
git branch <branch-name>
```

Creates a new branch pointing to the current commit.

**Example:**
```bash
git branch feature-login
```

This creates a new branch but doesn't switch to it. You're still on your current branch.

#### Switching Branches

```bash
git checkout <branch-name>
git switch <branch-name>  # Modern syntax (Git 2.23+)
```

**Example:**
```bash
git switch feature-login
# Switched to branch 'feature-login'
```

#### Creating and Switching in One Command

```bash
git checkout -b <branch-name>
git switch -c <branch-name>  # Modern syntax
```

**Example:**
```bash
git switch -c feature-dashboard
# Switched to a new branch 'feature-dashboard'
```

#### Viewing Branches

```bash
git branch              # Local branches only
git branch -a           # All branches (local + remote)
git branch -v           # With last commit info
git branch -vv          # With tracking info
```

**Example output:**
```
  feature-dashboard  abc123d Update dashboard UI
  feature-login      def456e Add authentication
* main               ghi789f Merge pull request #42
  remotes/origin/main
```

The asterisk (`*`) shows the current branch.

#### Deleting Branches

```bash
git branch -d <branch-name>              # Safe delete (only if merged)
git branch -D <branch-name>              # Force delete
git branch -m <old-name> <new-name>     # Rename branch
```

**Example:**
```bash
git branch -d feature-old-button
# Deleted branch feature-old-button
```

### Understanding Merging

Merging is combining two branches. Git uses different strategies depending on the situation.

#### Fast-Forward Merge

When the target branch hasn't changed since you created your feature branch, Git performs a fast-forward merge — it simply moves the branch pointer forward.

```
Before merge:
main          feature-login
  │              │
  ▼              ▼
[abc123] ← [def456] ← [ghi789]


After merge:
              main, feature-login
                    │
                    ▼
[abc123] ← [def456] ← [ghi789]
```

**In code:**
```bash
git switch main
git merge feature-login

# Output:
# Updating abc123..ghi789
# Fast-forward
#  login.txt | 1 +
#  1 file changed, 1 insertion(+)
```

#### Three-Way Merge

When both branches have diverged (both have new commits since they diverged), Git performs a three-way merge, creating a new commit that combines both branches.

```
Before merge:
main                    feature-login
  │                         │
  ▼                         ▼
[abc123] ← [def456]    [jkl012]
   ↑________________________↑
   (common ancestor)


After merge:
                main
                  │
                  ▼
[abc123] ← [def456] ← [new123] (merge commit)
  ↑                  ↙
  └─[jkl012]←─────┘
  
feature-login still points to jkl012
```

**In code:**
```bash
git switch main
git merge feature-login

# Output:
# Merge made by the 'ort' strategy.
#  login.txt     | 2 ++
#  register.txt  | 1 +
#  2 files changed, 3 insertions(+)
```

#### Merge Conflicts

Conflicts occur when the same part of a file was modified differently in both branches.

**Creating a conflict scenario:**
```bash
# On main
echo "Welcome to our app" > index.txt
git add index.txt
git commit -m "Add welcome message"

# Switch to feature branch
git switch -c feature-greeting

# Modify same line
echo "Welcome to our amazing app" > index.txt
git add index.txt
git commit -m "Improve greeting"

# Switch back to main and modify same line differently
git switch main
echo "Welcome, dear user" > index.txt
git add index.txt
git commit -m "Personalize greeting"

# Now try to merge
git merge feature-greeting
# Auto-merging index.txt
# CONFLICT (content): Merge conflict in index.txt
# Automatic merge failed; fix conflicts and then commit the result.
```

**Resolving conflicts manually:**

```bash
# View the conflicted file
cat index.txt

# Output:
# <<<<<<< HEAD
# Welcome, dear user
# =======
# Welcome to our amazing app
# >>>>>>> feature-greeting
```

Git marks conflicts with special markers:
- `<<<<<<< HEAD`: Your changes (current branch)
- `=======`: Separator
- `>>>>>>> feature-greeting`: Incoming changes (branch being merged)

**Edit the file to resolve:**

```bash
# Remove conflict markers and choose the right content
echo "Welcome to our amazing app, dear user" > index.txt

# Stage the resolution
git add index.txt

# Complete the merge
git commit -m "Resolve merge conflict: combine greetings"
```

**Using merge tools:**

```bash
# Open a visual merge tool
git mergetool

# Common tools: vimdiff, meld, kdiff3, VSCode
```

#### Aborting a Merge

If you realize you started a merge by mistake:

```bash
git merge --abort
```

This reverts to the state before the merge started.

### Merging Strategies

Git supports different merge strategies for specific situations:

#### Recursive (Default)

```bash
git merge <branch>
```

The default three-way merge strategy. Suitable for most cases.

#### Resolve

```bash
git merge -s resolve <branch>
```

Older three-way merge algorithm. Rarely needed with modern Git.

#### Ours

```bash
git merge -s ours <branch>
```

Automatically resolves conflicts by taking our version. The other branch's changes are not included.

```bash
git merge -X ours <branch>
```

More commonly, use `-X ours` to prefer our version in conflicts but still merge other files normally.

#### Theirs

```bash
git merge -X theirs <branch>
```

Opposite of `-X ours`: prefer their version in conflicts.

### Deleted Branches

After merging, you can safely delete the branch:

```bash
git branch -d feature-login
git branch -D feature-login  # Force if not merged
```

**Cleaning up remote branches:**

```bash
# Delete remote branch
git push origin --delete feature-login

# Remove stale remote tracking branches locally
git fetch --prune
```

---

## 6. Rewriting History and Undoing Things

This section covers Git's powerful (and potentially dangerous) tools for changing the past. **Use with caution on shared branches.**

### Understanding git reset

`git reset` moves the HEAD pointer and optionally stages/unstages changes. It has three modes:

#### Soft Reset (--soft)

```bash
git reset --soft HEAD~1
```

- Moves HEAD to previous commit
- **Keeps changes staged** in the staging area
- **Keeps changes in working directory**

**Useful for**: Redoing a commit — fix the message or add more changes before recommitting.

```bash
# Scenario: Made a commit but forgot to add a file
git add forgotten-file.txt
git commit -m "Forgot another file"

# Realize you forgot another change
git reset --soft HEAD~1
# Now the commit is undone, changes are staged
git add another-file.txt
git commit -m "Properly commit everything"
```

#### Mixed Reset (--mixed, DEFAULT)

```bash
git reset --mixed HEAD~1
# or simply: git reset HEAD~1
```

- Moves HEAD to previous commit
- **Unstages changes** (removes from staging area)
- **Keeps changes in working directory**

**Useful for**: Undoing a commit but keeping the changes to redo them differently.

```bash
# Scenario: Made a commit, want to split it into two smaller commits
git reset HEAD~1
# Commit is undone, changes are in working directory (unstaged)

git add file1.txt
git commit -m "First change"

git add file2.txt
git commit -m "Second change"
```

#### Hard Reset (--hard)

```bash
git reset --hard HEAD~1
```

- Moves HEAD to previous commit
- **Discards all changes** (both staged and working directory)
- **Changes are permanently lost**

**Useful for**: Completely abandon work and go back to a previous state.

```bash
# Scenario: Totally messed up, want to start over
git reset --hard HEAD~3
# Last 3 commits are gone, working directory matches 3 commits ago
```

⚠️ **Warning**: `--hard` is destructive. Use `git reflog` to recover if you made a mistake.

#### Reset Comparison Table

| Flag | HEAD | Staging Area | Working Directory |
|------|------|--------------|-------------------|
| `--soft` | ✓ Moves | ✓ Preserved | ✓ Preserved |
| `--mixed` | ✓ Moves | ✗ Discarded | ✓ Preserved |
| `--hard` | ✓ Moves | ✗ Discarded | ✗ Discarded |

#### Reset with Specific Paths

```bash
git reset <commit> <file>   # Mixed reset for specific file
git reset <commit> src/     # Mixed reset for directory
```

This unstages changes for that file/directory without changing HEAD.

### Reverting Changes (git revert)

`git revert` **creates a new commit** that undoes changes from a previous commit. Unlike `reset`, it doesn't rewrite history.

```bash
git revert <commit>
```

**When to use**: When you need to undo something on a shared branch. Revert is safe; reset is not on shared code.

**Example:**

```bash
# View history
git log --oneline
# abc123d Add newsletter feature
# def456e Fix login bug
# ghi789f Initial commit

# Decide newsletter feature was a mistake
git revert abc123d

# Git creates new commit:
# jkl012m Revert "Add newsletter feature"
# 
# The new commit has the opposite changes of abc123d
```

**If there are conflicts**, resolve them like you would with a merge:

```bash
# Resolve conflicts in files
# Then:
git revert --continue
```

**To abort a revert:**

```bash
git revert --abort
```

#### Reset vs Revert

| Aspect | Reset | Revert |
|--------|-------|--------|
| **What it does** | Moves HEAD pointer | Creates new commit |
| **Rewrites history** | Yes | No |
| **Safe on shared branches** | No | Yes |
| **Undoes how many commits** | 1 or more | 1 at a time |
| **Recover with reflog** | Yes | Not needed |

**Rule of thumb**: Use `revert` on public/shared branches. Use `reset` on local/private work.

### Amending Commits (git commit --amend)

```bash
git commit --amend
```

Modifies the most recent commit without creating a new one.

**Use cases:**

1. **Fix commit message:**
```bash
git commit --amend -m "Corrected commit message"
```

2. **Add forgotten changes:**
```bash
git add forgotten-file.txt
git commit --amend --no-edit
# --no-edit keeps the original message
```

3. **Change author:**
```bash
git commit --amend --author="New Name <new@email.com>" --no-edit
```

**Example workflow:**
```bash
# Make a commit
git commit -m "Add user login"

# Realize you misspelled the message
git commit --amend -m "Add user authentication"

# Or realize you forgot to add a file
git add auth-test.js
git commit --amend --no-edit
```

⚠️ **Warning**: Don't amend pushed commits. It rewrites history and causes problems for others.

### Restoring Files (git restore)

`git restore` was introduced in Git 2.23 as a safer alternative to `git reset` for file-specific operations.

#### Discard Working Directory Changes

```bash
git restore <file>
```

Reverts a file to its last committed version (dangerous — changes are lost).

**Example:**
```bash
# Made changes to bug.txt
echo "broken code" > bug.txt

# Oops, want the committed version back
git restore bug.txt
# bug.txt is now reverted to last commit
```

#### Unstage a File

```bash
git restore --staged <file>
```

Removes a file from the staging area without changing the working directory.

**Example:**
```bash
git add bug.txt
git restore --staged bug.txt
# bug.txt is unstaged but your changes remain
```

#### Restore to Specific Commit

```bash
git restore --source=<commit> <file>
```

Restore a file from a specific commit.

**Example:**
```bash
git restore --source=abc123d README.md
# README.md is restored to how it was in commit abc123d
```

### Interactive Rebase (git rebase -i)

Interactive rebase is Git's most powerful (and complex) tool. It lets you rewrite commit history: reorder, squash, reword, or delete commits.

```bash
git rebase -i <commit>
```

This opens your editor with a list of commits since `<commit>`.

**Example:**

```bash
# View last 3 commits
git log --oneline -3
# abc123d Add comments to auth module
# def456e Fix typo in config
# ghi789f Add user registration

# Rebase interactively
git rebase -i HEAD~3
```

Your editor opens with:

```
pick ghi789f Add user registration
pick def456e Fix typo in config
pick abc123d Add comments to auth module

# Rebase xyz789u..abc123d onto xyz789u (3 commands)
```

#### Rebase Commands

| Command | What it does |
|---------|------------|
| `pick` | Use commit as-is |
| `reword` | Use commit but edit message |
| `squash` | Meld into previous commit |
| `fixup` | Like squash but discard message |
| `exec` | Run a command |
| `break` | Stop at this point |
| `drop` | Delete commit |

#### Example: Squashing Commits

Squash multiple small commits into one:

```
pick ghi789f Add user registration
squash def456e Fix typo in config
squash abc123d Add comments to auth module
```

After saving, Git combines all three commits into one. You're prompted to edit the final commit message.

Result:
```bash
git log --oneline
# merged123 Add user registration with fixes and comments
```

#### Example: Reordering Commits

Rearrange the order:

```
pick def456e Fix typo in config
pick abc123d Add comments to auth module
pick ghi789f Add user registration
```

After rebase, commits are in this new order.

#### Example: Editing Commits

```
reword ghi789f Add user registration
pick def456e Fix typo in config
pick abc123d Add comments to auth module
```

When rebasing reaches the `reword` line, Git pauses for you to edit that commit's message.

#### Aborting a Rebase

If you mess up during a rebase:

```bash
git rebase --abort
```

This cancels the rebase and returns to the original state.

#### Continuing After Conflicts

If conflicts occur during rebase:

```bash
# Resolve conflicts in files
# Then:
git rebase --continue
```

#### Interactive Rebase Best Practices

- **Never rebase shared history**: Only rebase commits you haven't pushed
- **Use for local cleanup**: Squash WIP commits, fix messages, before pushing
- **Create a backup branch**: `git branch backup` before complex rebasing
- **Test after rebasing**: Run tests to ensure nothing broke

### Cherry-Picking Commits (git cherry-pick)

Cherry-pick is applying specific commits from one branch to another, without merging everything.

```bash
git cherry-pick <commit>
```

**Use case**: You need a specific bug fix from another branch, but aren't ready to merge the whole branch.

**Example:**

```bash
# Currently on main
# There's a critical bug fix on feature-bugfix branch

# View that branch's commits
git log feature-bugfix --oneline

# abc123d Critical security fix
# def456e Experimental feature
# ghi789f Refactoring

# Cherry-pick just the security fix
git cherry-pick abc123d

# abc123d is now applied to main as a new commit
git log --oneline -1
# xyz789u Critical security fix
```

**Cherry-picking multiple commits:**

```bash
git cherry-pick abc123d def456e ghi789f  # Specific commits
git cherry-pick abc123d..ghi789f          # Range of commits
```

⚠️ **Warning**: Cherry-picking can create duplicate commits if the original is later merged. Use when necessary, not as a substitute for proper merging.

### Recovering Lost Commits (git reflog)

`git reflog` (reference log) records every change to HEAD. It's your safety net for recovering "lost" commits.

```bash
git reflog
```

**Example output:**
```
abc123d (HEAD -> main) HEAD@{0}: rebase -i (finish): returning to refs/heads/main
def456e HEAD@{1}: rebase -i (squash): Add feature and fix typo
ghi789f HEAD@{2}: rebase -i (start): checkout HEAD~3
jkl012m HEAD@{3}: commit: Add comments
mno345p HEAD@{4}: commit: Fix typo
```

Each line shows a point you can return to.

**Recovering a deleted commit:**

```bash
# Accidentally hard reset
git reset --hard HEAD~5

# Oh no! Lost commits!
git reflog
# abc123d HEAD@{0}: reset: moving to HEAD~5
# def456e HEAD@{1}: commit: Important work
# ...

# Recover!
git reset --hard def456e
# You're back to before the reset
```

---

## 7. Remote Repositories and Collaboration

Git is distributed, but typically projects use a central remote repository (GitHub, GitLab, etc.) as the single source of truth.

### Adding Remotes (git remote)

A remote is a reference to a repository on another server.

#### Adding a Remote

```bash
git remote add <name> <url>
```

The default remote is usually named `origin`.

**Example:**

```bash
git remote add origin https://github.com/username/my-repo.git
# or SSH:
git remote add origin git@github.com:username/my-repo.git
```

#### Viewing Remotes

```bash
git remote              # Just names
git remote -v          # Names and URLs (verbose)
```

**Output:**
```
origin  git@github.com:username/my-repo.git (fetch)
origin  git@github.com:username/my-repo.git (push)
```

#### Changing a Remote URL

```bash
git remote set-url <name> <new-url>
```

**Example:**
```bash
git remote set-url origin git@github.com:username/my-repo.git
```

#### Removing a Remote

```bash
git remote remove <name>
```

### Fetching from Remote (git fetch)

```bash
git fetch <remote>
git fetch <remote> <branch>
```

Fetch downloads commits from the remote but **doesn't merge them**. It updates remote-tracking branches.

```bash
# Fetch all branches from origin
git fetch origin

# Output:
# remote: Counting objects: 5, done.
# Unpacking objects: 100% (5/5), done.
# From github.com:username/my-repo
#    abc123d..def456e  main       -> origin/main
```

**Remote-tracking branches:**

When you fetch, Git creates/updates branches like `origin/main`, `origin/feature-login`, etc. These are **read-only** representations of the remote branches.

```
Local branches:           Remote-tracking branches:
main                      origin/main
feature-login             origin/feature-login

You can:                  You can:
- Edit main              - Review changes before merging
- Commit to main         - Merge into local branches
- Delete main            - Can't commit directly
```

### Pulling from Remote (git pull)

```bash
git pull <remote> <branch>
# Equivalent to:
git fetch <remote>
git merge <remote>/<branch>
```

`pull` is a convenience command that fetches and merges in one step.

**Example:**

```bash
git pull origin main
# Fetches latest changes from origin/main
# Merges them into your current branch
```

#### Pulling with Rebase

Sometimes you want to rebase your commits onto the latest remote, rather than merge:

```bash
git pull --rebase <remote> <branch>
```

This prevents merge commits and keeps history linear.

**Example:**

Before pull:
```
Local:  [abc123] ← [def456] (your commits)
Remote: [abc123] ← [ghi789] ← [jkl012] (remote commits)
```

After `git pull origin main`:

With merge (default):
```
[abc123] ← [def456] ← [merged123] (merge commit)
   ↓                ↙
[ghi789] ← [jkl012]
```

With rebase (`git pull --rebase`):
```
[abc123] ← [ghi789] ← [jkl012] ← [def456'] (rebased)
```

### Pushing to Remote (git push)

```bash
git push <remote> <branch>
```

Uploads commits from your local branch to the remote.

**Example:**

```bash
git push origin main
# Uploads commits to github.com:username/my-repo
# Updates the remote's main branch
```

#### Pushing New Branches

When pushing a new branch for the first time:

```bash
git push -u origin feature-login
# -u sets upstream tracking
# Now: git pull / git push work without arguments
```

#### Pushing All Branches

```bash
git push origin --all
```

#### Force Pushing (Use with Caution!)

```bash
git push --force origin main
```

**Overwrites remote history with your local history.** Dangerous on shared branches because it can delete others' commits.

#### Safe Force Push

```bash
git push --force-with-lease origin main
```

This is safer: it only forces if the remote hasn't been updated since your last fetch. It prevents accidentally overwriting new remote commits.

**When to use force push**: After interactive rebasing or amending commits on a **personal/unshared branch**.

### Setting Upstream Branches

An upstream branch is the remote branch your local branch tracks.

```bash
# Set upstream when pushing
git push -u origin feature-login

# Set upstream for existing branch
git branch --set-upstream-to=origin/main main

# View upstream
git branch -vv
# main                 abc123d [origin/main] Latest commit
# feature-login        def456e [origin/feature-login: ahead 2] New work
```

Benefits of upstream:
- `git pull` / `git push` work without arguments
- `git status` shows how far ahead/behind you are

### GitHub-Specific Operations

#### Creating a Repository on GitHub

1. Log in to GitHub
2. Click **+** → **New repository**
3. Enter repository name
4. Add description (optional)
5. Choose public/private
6. Optionally add README, .gitignore, license
7. Click **Create repository**

#### README.md

GitHub automatically displays `README.md` on the repository page. Use Markdown:

```markdown
# My Project

Brief description of what this project does.

## Installation

Instructions to set up locally.

## Usage

Examples of how to use the project.

## Contributing

How others can contribute.

## License

License information.
```

#### LICENSE

Include a license file to specify how your code can be used. Common options:

- **MIT**: Permissive, minimal restrictions
- **Apache 2.0**: Permissive, includes patent protection
- **GPL**: Copyleft, derivative works must be open-source
- **BSD**: Similar to MIT

GitHub can generate license templates during repo creation.

#### .github Directory

Special workflows and configurations:

```
.github/
├── workflows/          # GitHub Actions CI/CD
│   └── ci.yml
├── ISSUE_TEMPLATE/     # Issue templates
│   └── bug_report.md
└── PULL_REQUEST_TEMPLATE.md
```

#### Creating a Pull Request

1. Push your branch to GitHub
2. Go to the repository
3. Click **Pull requests** → **New pull request**
4. Select your branch to merge into main
5. Add title and description
6. Click **Create pull request**

**Pull Request Description Template:**

```markdown
## Description
Brief description of what this PR does.

## Related Issue
Fixes #123

## How to Test
Steps to verify the changes work.

## Checklist
- [ ] Code follows style guidelines
- [ ] Tests added/updated
- [ ] Documentation updated
```

#### Reviewing Pull Requests

1. Go to the PR
2. Click **Files changed**
3. Click **+** on lines to comment
4. Click **Review changes** → **Approve** or **Request changes**
5. After approval, click **Merge pull request**

#### Forking and Contributing to Open Source

**Fork** creates your own copy of someone else's repository.

1. On GitHub, click **Fork**
2. GitHub creates `your-username/original-repo`
3. Clone your fork locally:
```bash
git clone git@github.com:your-username/original-repo.git
```

4. Add upstream remote:
```bash
git remote add upstream git@github.com:original-owner/original-repo.git
```

5. Create feature branch:
```bash
git switch -c fix-typo
```

6. Make changes, commit, push:
```bash
git push origin fix-typo
```

7. Go to GitHub, click **Pull request**
8. Submit PR to the original repository

**Staying in sync with upstream:**

```bash
git fetch upstream
git rebase upstream/main
git push --force-with-lease origin main
```

---

## 8. Inspection and Debugging

### Viewing Commit History (git log)

```bash
git log
```

Shows commit history in reverse chronological order.

**Default output:**
```
commit abc123def456...
Author: John Doe <john@example.com>
Date:   Mon Jan 15 10:30:00 2024 +0000

    Add user authentication feature

    - Implement JWT tokens
    - Add password hashing
    - Create login endpoint
```

#### Useful Log Options

```bash
git log --oneline                    # Compact: one line per commit
git log --oneline -5                 # Last 5 commits
git log --graph --oneline --all      # Show branching structure
git log -p                            # Show patch (changes) for each commit
git log -p -2                         # Patches for last 2 commits
git log --stat                        # Show files changed and line counts
git log --author="John"               # Filter by author
git log --grep="feature"              # Filter by commit message
git log --since="2024-01-01"          # Since specific date
git log --until="2024-12-31"          # Until specific date
git log main..feature-login           # Commits in feature-login not in main
git log --reverse                     # Reverse order (oldest first)
git log --oneline --decorate          # Show branch/tag names
```

**Beautiful graph visualization:**

```bash
git log --graph --oneline --all --decorate
```

**Output:**
```
* abc123d (HEAD -> main, origin/main) Merge pull request #42
|\
| * def456e (origin/feature-login) Add login form
|/
* ghi789f Update documentation
* jkl012m Initial commit
```

#### Custom Log Format

```bash
git log --format="%h %s (%an)" --date=short
# abc123d Add feature (John Doe)
# def456e Fix bug (Jane Smith)
```

Format codes:
- `%h`: Abbreviated hash
- `%s`: Commit message
- `%an`: Author name
- `%ae`: Author email
- `%ad`: Author date
- `%d`: Decorations (branches, tags)

### Showing Specific Commits (git show)

```bash
git show <commit>
```

Shows the full details of a specific commit, including changes.

**Example:**

```bash
git show abc123d
# commit abc123d...
# Author: John Doe <john@example.com>
# Date:   Mon Jan 15 10:30:00 2024 +0000
#
#     Add user authentication
#
# diff --git a/auth.py b/auth.py
# index 1234567..abcdefg 100644
# --- a/auth.py
# +++ b/auth.py
# ...
```

**Show specific file at commit:**

```bash
git show abc123d:path/to/file.txt
```

Displays how that file looked at that commit.

### Blaming Changes (git blame)

```bash
git blame <file>
```

Shows which commit last modified each line of a file.

**Example output:**
```
abc123d (John Doe 2024-01-15 10:30:00 +0000) function login(username) {
def456e (Jane Smith 2024-01-14 14:22:00 +0000)   const hash = bcrypt.hash(password);
ghi789f (John Doe 2024-01-15 11:45:00 +0000)   return authenticate(hash);
jkl012m (Jane Smith 2024-01-10 09:15:00 +0000) }
```

**Useful options:**

```bash
git blame -L 10,20 <file>     # Blame specific lines
git blame -e <file>            # Show email addresses
git blame -M <file>            # Track lines moved between files
git blame -C <file>            # Track lines copied between files
```

### Binary Search for Bugs (git bisect)

`git bisect` performs a binary search through commit history to find which commit introduced a bug.

**Scenario:** Your project works on commit `abc123d` but is broken on `xyz789u`. Which commit broke it?

```bash
# Start bisect
git bisect start

# Mark the broken commit
git bisect bad xyz789u

# Mark a known-good commit
git bisect good abc123d

# Git checks out a commit halfway between
# Test if it's broken or good...

git bisect bad       # If broken, mark bad
# or
git bisect good      # If working, mark good

# Repeat until Git narrows it down
# Eventually: "abc789m is the first bad commit"

# End bisect
git bisect reset
```

**Automated bisect with tests:**

```bash
git bisect start --auto
git bisect good abc123d
git bisect bad xyz789u
git bisect run npm test  # Automatically test each commit
```

### Searching Code (git grep)

```bash
git grep <pattern>
```

Searches for text in tracked files (faster than regular grep).

**Example:**

```bash
git grep "TODO"
# Finds all "TODO" comments in the codebase

git grep -i "database"     # Case-insensitive
git grep -n "function"     # Show line numbers
git grep -c "error"        # Count occurrences per file
```

### Commit Statistics (git shortlog)

```bash
git shortlog
```

Summary of commits grouped by author.

**Example output:**
```
Jane Smith (5):
      Add user authentication
      Fix password validation
      Update README
      Merge pull request #42
      Improve error handling

John Doe (3):
      Fix typo
      Add unit tests
      Update dependencies
```

**Useful options:**

```bash
git shortlog -s         # Just author count
git shortlog -n         # Sort by number of commits
git shortlog -e         # Show email addresses
```

---

## 9. Stashing and Cleaning

### Temporarily Saving Work (git stash)

`git stash` saves your uncommitted changes without committing them, allowing you to switch branches or pull changes.

```bash
git stash
```

Stashes both staged and unstaged changes.

**Example scenario:**

```bash
# You're on feature-login branch, working on login form
echo "password field code" > form.txt
git add form.txt

# Suddenly you need to switch to main to fix a critical bug
# But you have uncommitted work...

# Stash your changes
git stash
# Saved working directory and index state WIP on feature-login

# Switch to main (working directory is clean)
git switch main
# Fix bug...

# Switch back
git switch feature-login

# Restore your stashed changes
git stash pop
# Restores working directory to before stash
```

#### Stash Options

```bash
git stash save "descriptive message"    # Name your stash
git stash list                          # View all stashes
git stash show                          # Show what's in latest stash
git stash show -p                       # Show detailed changes
git stash apply stash@{0}               # Apply without removing
git stash pop stash@{0}                 # Apply and remove
git stash drop stash@{0}                # Delete a stash
git stash clear                         # Delete all stashes
git stash branch <branch-name>          # Create branch from stash
```

**Example:**

```bash
# Multiple stashes
git stash list
# stash@{0}: WIP on feature-login: abc123d Add form validation
# stash@{1}: WIP on feature-login: def456e Add password field

# Apply specific stash
git stash apply stash@{1}

# Or most recent
git stash apply
```

#### Only Stashing Unstaged Changes

```bash
git stash push -m "my changes"      # Only working directory
git stash -k                        # Keep staged changes
```

### Cleaning Untracked Files (git clean)

```bash
git clean
```

Deletes untracked files from your working directory.

⚠️ **Warning**: `git clean` is destructive. Use `-n` to preview first.

```bash
# Preview what will be deleted
git clean -n

# Delete untracked files
git clean -f

# Also delete untracked directories
git clean -fd

# Also delete ignored files (.gitignore)
git clean -fdx

# Interactively choose what to delete
git clean -i
```

**Common uses:**

```bash
# Clean after running build (removes node_modules, dist, etc.)
git clean -fd

# After changing .gitignore rules, remove tracked-but-ignored files
git clean -fdx
```

---

## 10. Advanced Topics

### Interactive Rebase Deep Dive

We covered basics earlier. Here are advanced techniques:

#### Squashing WIP Commits

Before pushing, squash multiple work-in-progress commits into one coherent commit:

```bash
git rebase -i HEAD~5
```

Mark most commits as `squash` or `fixup`:

```
pick abc123d Add feature
fixup def456e WIP: tests
fixup ghi789f Fix linting
fixup jkl012m Oops, forgot this part
pick mno345p Update docs
```

Result: One clean "Add feature" commit with all the fixes combined.

#### Reordering Commits

```bash
git rebase -i HEAD~4
```

```
pick jkl012m Update docs       # Move this to first
pick abc123d Add feature
pick def456e Add tests
pick ghi789f Fix bug
```

Becomes:

```
pick jkl012m Update docs
pick abc123d Add feature
pick def456e Add tests
pick ghi789f Fix bug
```

#### Splitting Commits

Use `reword` plus `reset`:

```bash
git rebase -i HEAD~2
```

Change first commit to `edit`:

```
edit abc123d Add feature and fix
pick def456e Update docs
```

When rebase pauses at `edit`:

```bash
git reset HEAD~1
# Now changes from abc123d are unstaged
git add feature-code.txt
git commit -m "Add feature"
git add fix-code.txt
git commit -m "Fix bug"
git rebase --continue
```

The one commit becomes two.

### Tagging

Tags mark important points in history (releases, milestones).

#### Lightweight Tags

```bash
git tag <tag-name>
git tag v1.0
```

A simple pointer to a commit.

#### Annotated Tags

```bash
git tag -a <tag-name> -m "message"
git tag -a v1.0 -m "Version 1.0 release"
```

Full objects with metadata.

#### Signing Tags

```bash
git tag -s v1.0 -m "Signed release"  # Sign with default key
git tag -u <key-id> -a v1.0 -m "Signed release"
```

Cryptographically sign your release.

#### Viewing Tags

```bash
git tag                     # List all
git tag -l "v1.*"          # Filter pattern
git show v1.0              # Show tag details
git tag -v v1.0            # Verify signed tag
```

#### Pushing Tags

```bash
git push origin v1.0        # Push specific tag
git push origin --tags      # Push all tags
git push origin --delete v1.0  # Delete remote tag
```

### Git Hooks

Git hooks are scripts that run automatically on Git events.

#### Common Hooks

Located in `.git/hooks/`:

- **pre-commit**: Before committing (check code style, run tests)
- **commit-msg**: Before commit finalizes (validate message)
- **post-commit**: After commit (notifications)
- **pre-push**: Before pushing (final checks)
- **post-checkout**: After branch switching

#### Example: Pre-commit Hook

```bash
# Create .git/hooks/pre-commit
#!/bin/bash

# Run linter before committing
npm run lint
if [ $? -ne 0 ]; then
  echo "Linting failed. Commit aborted."
  exit 1
fi
```

Make executable:

```bash
chmod +x .git/hooks/pre-commit
```

Now linting runs automatically before each commit.

#### Sharing Hooks

Hooks in `.git/hooks/` are local only. To share hooks, use a directory in your repo:

```bash
mkdir -p .githooks

# Configure Git to use this directory
git config core.hooksPath .githooks

# Commit hooks to repo
git add .githooks/
```

Others clone and get the hooks automatically.

### Submodules and Subtrees

Both let you include external Git repositories within your repo.

#### Submodules

```bash
git submodule add <repo-url> <path>
git submodule add https://github.com/lodash/lodash.git lib/lodash
```

Creates a reference to external repo. You manage it separately.

**Cloning with submodules:**

```bash
git clone --recurse-submodules <repo>
```

**Updating submodules:**

```bash
git submodule update --remote
```

**Downsides**: More complex, separate history, less transparent.

#### Subtrees

```bash
git subtree add --prefix=lib/lodash https://github.com/lodash/lodash.git main
```

Actually merges external repo's code into your repo. Simpler for small dependencies.

**Updating:**

```bash
git subtree pull --prefix=lib/lodash https://github.com/lodash/lodash.git main
```

**For most projects**: Subtrees are simpler. Use submodules for large dependencies with separate teams.

### Worktrees

Create multiple working directories for the same repository.

```bash
git worktree add <path> <branch>
git worktree add ../feature-login feature-login
```

Now you have two directories, both linked to the same repo:

```
project/
  .git (shared)
  [main branch files]

../feature-login/
  [feature-login branch files]
  (same .git reference)
```

**Use case**: Work on multiple features in parallel without switching branches constantly.

**Managing worktrees:**

```bash
git worktree list        # See all
git worktree remove <path>  # Delete worktree
```

### Large Files with Git LFS

Regular Git struggles with large binary files (videos, datasets, model files). Git LFS (Large File Storage) stores pointers instead.

```bash
git lfs install
git lfs track "*.mp4"
git add model.mp4
```

Git stores a pointer file instead of the actual video. The large file is managed separately.

### Sparse Checkout

Clone only parts of a large repository.

```bash
git sparse-checkout init
git sparse-checkout set src/ docs/
```

Only `src/` and `docs/` directories are downloaded.

Useful for monorepos or massive repositories.

### Signed Commits

Sign commits with GPG for verification.

```bash
# Generate GPG key (one-time)
gpg --gen-key

# Configure Git
git config --global user.signingkey <key-id>
git config --global commit.gpgsign true

# Sign commits (automatic if gpgsign is true)
git commit -S -m "Signed commit"

# Verify signatures
git log --show-signature
```

Provides authenticity: proves you made the commit, not someone else.

### Performance Tips for Large Repositories

```bash
# Shallow clone (limited history)
git clone --depth 1 <url>

# Partial clone (don't download all objects initially)
git clone --filter=blob:none <url>

# Garbage collection and optimization
git gc
git maintenance start  # (Git 2.37+) automatic optimization

# Reduce repository size
git prune
git repack -Ad
```

---

## 11. Workflows and Best Practices

### GitHub Flow

Simple, linear workflow suitable for continuous deployment.

**Steps:**

1. **Create branch**: `git switch -c feature-name`
2. **Make changes**: Commits are clearly named
3. **Push branch**: `git push -u origin feature-name`
4. **Open PR**: Request code review
5. **Review and discuss**: Address feedback
6. **Merge**: Deploy main automatically
7. **Delete branch**: Clean up

**Branch structure:**
```
main branch (always deployable)
  ├─ feature-login (PR #42)
  ├─ feature-dashboard (PR #43)
  └─ bugfix-404 (PR #44)
```

**Pro**: Simple, clear, good for fast-moving teams
**Con**: Doesn't handle versioning/releases well

### Git Flow

More structured workflow with dedicated branches for features, releases, and hotfixes.

**Branches:**
- `main`: Production-ready code (releases only)
- `develop`: Integration branch for features
- `feature/*`: Individual features
- `release/*`: Preparation for releases
- `hotfix/*`: Critical production fixes

**Workflow:**

```
main ─────────────────────────────────► (v1.0 release)
   ↑
   │ hotfix-security
   │ (merge after fix)
   │
develop ─┬─────────────────────────►
  ↑      │
  │      └─ feature-login ─┐
  │                         │ (merge after PR)
  │      ┌─ feature-dashboard ─┐
  │      │                      │ (merge after PR)
  └──────┴──────────────────────┴───► release-1.0 ──► main (merge)
```

**Feature development:**
```bash
git switch -c feature-login develop
# Work on feature...
git push -u origin feature-login
# Create PR, get reviewed, merge back into develop
```

**Creating a release:**
```bash
git switch -c release-1.0 develop
# Only version bumps and bug fixes
git push origin release-1.0
# Merge to main: git switch main && git merge release-1.0
# Merge back to develop: git switch develop && git merge release-1.0
```

**Critical hotfix:**
```bash
git switch -c hotfix-security main
# Fix the security issue
# Merge to main: git switch main && git merge hotfix-security
# Merge back to develop: git switch develop && git merge hotfix-security
```

**Pro**: Clear structure, good for versioned releases, big teams
**Con**: More complex, slower for rapid iteration

### Trunk-Based Development

Developers commit frequently to a single `main` branch with short-lived feature branches.

**Key rules:**
- Short-lived branches (< 1 day)
- Frequent commits to main (multiple times per day)
- Feature flags for incomplete features
- Continuous integration and testing

**Workflow:**

```bash
# Create tiny branch
git switch -c feature-button-color main
# Make one small change
echo "color: blue;" > button.css
git commit -m "Change button color to blue"
git push -u origin feature-button-color
# Create PR, get quick review, merge immediately
git switch main && git merge feature-button-color
```

**Pro**: Simple, reduces merge conflicts, continuous deployment-friendly
**Con**: Requires discipline, needs strong CI/CD, feature flags add complexity

### Conventional Commits

Standardized commit message format for automatic versioning and changelog generation.

**Format:**
```
<type>[optional scope]: <description>

[optional body]

[optional footer]
```

**Example:**
```
feat(auth): add JWT token generation

Add endpoint for generating JWT tokens with configurable expiration.
Implements refresh token rotation for security.

Closes #123
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting
- `refactor`: Code restructuring
- `perf`: Performance
- `test`: Tests
- `chore`: Maintenance
- `ci`: CI/CD changes
- `build`: Build system changes

**Benefits:**
- Automated changelog generation
- Automatic semantic versioning (with tools like commitlint)
- Clear history for bisecting
- Easy to scan

### Branch Naming Conventions

Consistent naming improves navigation and automation.

**Recommended format:**
```
<type>/<short-description>
```

**Examples:**
```
feature/user-authentication
feature/dark-mode-toggle
bugfix/404-error-page
hotfix/security-vulnerability
refactor/extract-auth-service
docs/update-readme
```

**Type prefixes:**
- `feature/`: New features
- `bugfix/`: Bug fixes
- `hotfix/`: Critical production fixes
- `refactor/`: Code improvements
- `docs/`: Documentation
- `test/`: Test additions
- `chore/`: Maintenance

**Automation:**
```bash
# Delete old feature branches automatically
git branch -a | grep feature/ | grep -v \* | xargs -n 1 git branch -d

# Find branches not merged
git branch -a --no-merged main
```

### Code Review Best Practices

#### Reviewer Responsibilities

- **Understand the change**: Ask questions if unclear
- **Check for bugs**: Look for logic errors, edge cases
- **Verify tests**: Are new tests added? Do they pass?
- **Review style**: Follows project conventions?
- **Performance**: Any obvious inefficiencies?
- **Documentation**: Updated docs, comments, README?

#### Review Comments

Good comment:
```
❌ This could cause a null pointer exception if user is not authenticated.
   Consider adding a null check here.
```

Not helpful:
```
❌ I don't like this code.
```

#### Approval Process

```bash
# Reviewer approves
# "Looks good to me!"

# Author merges and deletes branch
git switch main
git merge feature-login
git branch -d feature-login
git push origin main
git push origin --delete feature-login
```

### Avoiding Common Dangers

#### Force Push on Shared Branches

⚠️ **NEVER DO THIS:**
```bash
git push --force origin main
```

**Why**: Overwrites others' commits, causes lost work.

**Safe alternative**:
```bash
git push --force-with-lease origin main
```

Even safer: protect main branch in GitHub settings to prevent force pushes.

#### Rebasing Shared History

⚠️ **NEVER DO THIS:**
```bash
# On a shared branch
git rebase origin/main
git push --force
```

**Why**: Changes commit hashes, makes others' branches incompatible.

**Safe alternative**:
```bash
# Use merge instead
git merge origin/main
git push
```

#### Merging to Wrong Branch

⚠️ **Check before merging:**
```bash
git branch  # Verify you're on the right branch
git merge <branch>
```

**Undo accidental merge:**
```bash
git reset --hard HEAD~1  # Undo the merge commit
```

#### Committing Secrets

⚠️ **Never commit passwords, API keys, tokens!**

```bash
# Remove from git history
git rm --cached .env
echo ".env" >> .gitignore
git commit --amend -m "Remove .env from history"

# For already-pushed secrets: use BFG Repo-Cleaner
bfg --replace-text passwords.txt
```

---

## 12. Cheat Sheets

### Quick Command Reference

#### Repository Setup

```bash
git init                                  # Initialize new repo
git clone <url>                          # Clone existing repo
git clone --depth 1 <url>                # Shallow clone (fast)
git remote add origin <url>              # Add remote
git remote -v                            # View remotes
```

#### Daily Workflow

```bash
git status                               # Check status
git add <file>                           # Stage file
git add .                                # Stage all
git commit -m "<message>"                # Commit with message
git diff                                 # View changes
git diff --staged                        # View staged changes
git log --oneline                        # View history
```

#### Branches

```bash
git branch                               # List local branches
git branch -a                            # List all branches
git branch <name>                        # Create branch
git switch <name>                        # Switch branch
git switch -c <name>                     # Create and switch
git branch -d <name>                     # Delete branch (safe)
git branch -D <name>                     # Force delete
git merge <name>                         # Merge branch
```

#### Undoing Changes

```bash
git restore <file>                       # Discard working changes
git restore --staged <file>              # Unstage file
git reset HEAD~1                         # Undo last commit (keep changes)
git reset --hard HEAD~1                  # Undo last commit (discard)
git revert <commit>                      # Create undo commit
git commit --amend                       # Modify last commit
```

#### Remote Operations

```bash
git fetch origin                         # Download changes
git pull origin main                     # Fetch and merge
git pull --rebase origin main            # Fetch and rebase
git push origin main                     # Upload commits
git push -u origin <branch>              # Push new branch
git push --force-with-lease origin main  # Safe force push
```

#### Finding Things

```bash
git log <file>                           # History of file
git log --all --graph --oneline          # Visualize branches
git blame <file>                         # Who changed what
git show <commit>                        # Show commit details
git grep <pattern>                       # Search code
```

#### Cleanup

```bash
git stash                                # Stash changes
git stash pop                            # Restore stash
git stash list                           # List stashes
git clean -fd                            # Remove untracked files
git reflog                               # View all HEAD changes
```

### Reset vs Revert vs Restore

| Command | Effect | Safe on shared | Use case |
|---------|--------|----------------|----------|
| `reset --soft` | Undo commit, keep changes staged | No | Redo a commit |
| `reset --mixed` | Undo commit, keep changes unstaged | No | Modify changes before recommit |
| `reset --hard` | Undo everything | No | Completely abandon work |
| `revert` | Create opposite commit | Yes | Undo public change |
| `restore <file>` | Discard changes to file | N/A | Revert file to last commit |
| `restore --staged` | Unstage file | N/A | Remove from staging area |

### Merge vs Rebase

| Aspect | Merge | Rebase |
|--------|-------|--------|
| **Creates merge commit** | Yes | No |
| **History** | Non-linear, preserves truth | Linear, rewrites history |
| **When to use** | Shared branches, integrations | Local branches, cleanup |
| **Conflict resolution** | Once, during merge | Potentially multiple times |
| **Readability** | Shows integration points | Cleaner history |
| **Risk** | Low | High on shared code |

---

## 13. Troubleshooting Common Issues

### Detached HEAD

**Symptom**: You're not on any branch.

```
HEAD detached at abc123d
```

**Cause**: You checked out a commit instead of a branch.

**Solution:**

```bash
# Create a branch from current state
git switch -c recovery-branch

# Or go back to main
git switch main
```

**Preventing**: Always switch to branches, not commits.

```bash
git switch main      # Good
git checkout abc123d # Bad (detached HEAD)
```

### Authentication Errors

**Symptom**:
```
fatal: Authentication failed for 'https://github.com/...'
fatal: Permission denied (publickey)
```

**Cause**: Credentials not set up or SSH key missing.

**Solution for HTTPS**:
```bash
# Use Personal Access Token instead of password
git remote set-url origin https://token@github.com/user/repo.git
```

**Solution for SSH**:
```bash
# Verify SSH key exists
ls ~/.ssh/id_ed25519

# Test SSH connection
ssh -T git@github.com
# Should output: "Hi username! You've successfully authenticated..."

# If not, regenerate key
ssh-keygen -t ed25519 -C "your@email.com"

# Add to GitHub settings
cat ~/.ssh/id_ed25519.pub | pbcopy
# Paste in GitHub → Settings → SSH Keys
```

### Merge Conflicts

**Symptom**:
```
Auto-merging file.txt
CONFLICT (content): Merge conflict in file.txt
```

**Solution:**

```bash
# View conflicted file
cat file.txt

# Shows:
# <<<<<<< HEAD
# Our version
# =======
# Their version
# >>>>>>> branch-name

# Edit to fix, then:
git add file.txt
git commit -m "Resolve merge conflict"
```

**To abort merge:**
```bash
git merge --abort
```

### Large File Issues

**Symptom**:
```
fatal: The object is too large
```

**Prevention**:
```bash
# Configure to warn on large files
git config push.maxPackSize 1g
```

**Solution for already-committed large file**:
```bash
# Remove from repo history
git rm --cached large-file.zip
echo "large-file.zip" >> .gitignore
git commit --amend -m "Remove large file"

# For already-pushed large files, use BFG Repo-Cleaner
bfg --delete-files large-file.zip
```

### Permission Denied (publickey)

**Symptom**:
```
Permission denied (publickey).
fatal: Could not read from remote repository.
```

**Causes and solutions**:

1. **SSH key not added to agent:**
```bash
ssh-add ~/.ssh/id_ed25519
```

2. **Wrong SSH key permissions:**
```bash
chmod 600 ~/.ssh/id_ed25519
chmod 700 ~/.ssh
```

3. **SSH key not added to GitHub:**
   - Go to GitHub Settings → SSH Keys
   - Add your public key

4. **Using wrong remote URL:**
```bash
git remote set-url origin git@github.com:username/repo.git
```

### Lost Commits

**Symptom**: You reset hard and lost commits.

**Solution**: Use reflog to recover.

```bash
git reflog
# Shows:
# abc123d (HEAD -> main) HEAD@{0}: reset: moving to HEAD~3
# def456e HEAD@{1}: commit: Important work

# Recover
git reset --hard def456e
```

### Branch Has Diverged

**Symptom**:
```
Your branch has diverged from 'origin/main' by 3 and 2 commits
```

**Causes**: Someone force-pushed, or you rebased locally.

**Solution**:

Option 1: Merge remote:
```bash
git pull origin main
```

Option 2: Rebase onto remote:
```bash
git rebase origin/main
```

Option 3: Reset to remote:
```bash
git reset --hard origin/main
```

### Accidentally Deleted Branch

**Recover:**
```bash
git reflog
# Find where you deleted it
# deleted-branch: 67890ab HEAD

git checkout -b deleted-branch 67890ab
```

---

## 14. Exercises and Projects

### Exercise 1: Basic Workflow

**Objective**: Practice git add, commit, and viewing history.

**Steps:**

1. Create a new directory and initialize a repository:
```bash
mkdir my-project
cd my-project
git init
```

2. Create a file:
```bash
echo "Hello, World!" > hello.txt
```

3. Check status:
```bash
git status
```

4. Stage and commit:
```bash
git add hello.txt
git commit -m "Add hello.txt with greeting"
```

5. View history:
```bash
git log --oneline
```

6. Modify the file:
```bash
echo "Hello, World! Welcome!" > hello.txt
```

7. View what changed:
```bash
git diff
```

8. Stage and commit:
```bash
git add hello.txt
git commit -m "Update greeting message"
```

9. View full history:
```bash
git log --oneline --all
```

**Expected output** (step 5 & 9):
```
abc123d Update greeting message
def456e Add hello.txt with greeting
```

**Solution**: This exercise demonstrates the basic Git workflow. You've created commits with meaningful messages, staged changes, and reviewed history.

### Exercise 2: Branching and Merging

**Objective**: Practice creating branches, switching, and merging.

**Steps:**

1. Start from previous exercise repo (or create new):
```bash
git init my-project
cd my-project
echo "Version 1" > app.txt
git add app.txt
git commit -m "Initial version"
```

2. Create and switch to a feature branch:
```bash
git switch -c feature-v2
echo "Version 2 - New Feature" > app.txt
git add app.txt
git commit -m "Add version 2 feature"
```

3. Switch back to main:
```bash
git switch main
```

4. Verify you're on main:
```bash
cat app.txt
# Shows: "Version 1" (feature changes aren't here)
```

5. Merge feature branch:
```bash
git merge feature-v2
cat app.txt
# Now shows: "Version 2 - New Feature"
```

6. View the merged history:
```bash
git log --oneline --graph --all
```

7. Delete the feature branch:
```bash
git branch -d feature-v2
```

**Expected output** (step 6):
```
* abc123d Merge branch 'feature-v2'
|\
| * def456e Add version 2 feature
|/
* ghi789f Initial version
```

**Solution**: This demonstrates branch creation, switching, merging (fast-forward in this case), and cleanup. The graph shows how branches converge.

### Exercise 3: Handling Merge Conflicts

**Objective**: Create and resolve merge conflicts.

**Steps:**

1. Set up initial repo:
```bash
mkdir conflict-repo
cd conflict-repo
git init
echo "Line 1" > file.txt
git add file.txt
git commit -m "Add file"
```

2. Create feature branch and modify:
```bash
git switch -c feature
echo "Feature version" > file.txt
git add file.txt
git commit -m "Feature version"
```

3. Switch back and modify differently:
```bash
git switch main
echo "Main version" > file.txt
git add file.txt
git commit -m "Main version"
```

4. Try to merge (creates conflict):
```bash
git merge feature
# CONFLICT (content): Merge conflict in file.txt
```

5. View the conflicted file:
```bash
cat file.txt
# <<<<<<< HEAD
# Main version
# =======
# Feature version
# >>>>>>> feature
```

6. Manually resolve (keep both):
```bash
echo "Main and Feature version" > file.txt
```

7. Stage and complete merge:
```bash
git add file.txt
git commit -m "Resolve merge conflict: combine both versions"
```

8. View result:
```bash
git log --oneline --graph --all
```

**Expected output** (step 8):
```
*   abc123d Resolve merge conflict: combine both versions
|\
| * def456e Feature version
* | ghi789f Main version
|/
* jkl012m Add file
```

**Solution**: This shows how conflicts occur when the same lines are edited differently, and how to resolve them manually.

### Exercise 4: Undoing Commits

**Objective**: Practice reset, revert, and restore.

**Steps:**

1. Create repo with history:
```bash
mkdir undo-repo
cd undo-repo
git init
echo "v1" > version.txt && git add . && git commit -m "v1"
echo "v2" > version.txt && git add . && git commit -m "v2"
echo "v3" > version.txt && git add . && git commit -m "v3"
```

2. View history:
```bash
git log --oneline
# abc123d v3
# def456e v2
# ghi789f v1
```

3. Practice soft reset:
```bash
git reset --soft HEAD~1
git status
# Changes to be committed: version.txt
# (v3 is undone but changes are staged)
git commit -m "v3 (recommitted)"
```

4. Practice hard reset:
```bash
git reset --hard HEAD~1
cat version.txt
# Shows: "v2"
```

5. Practice revert:
```bash
# Suppose you want to undo the "v2" commit but keep "v3"
git log --oneline
# abc123d v3
# def456e v2
# ghi789f v1

git revert def456e
# Creates new commit: "Revert v2"
git log --oneline
# xyz789u Revert "v2"
# abc123d v3
# def456e v2
# ghi789f v1
```

6. Practice restore:
```bash
# Modify file
echo "modified" > version.txt

# Discard changes
git restore version.txt
cat version.txt
# Back to last commit
```

**Solution**: You've learned the difference between destructive (reset) and non-destructive (revert) ways to undo. Soft reset keeps changes for recommitting, hard reset discards everything, and revert creates a new commit that undoes changes.

### Exercise 5: Interactive Rebase

**Objective**: Master interactive rebase for history cleanup.

**Steps:**

1. Create repo with messy history:
```bash
mkdir rebase-repo
cd rebase-repo
git init
echo "feature" > file.txt && git add . && git commit -m "Add feature"
echo "fix typo" >> file.txt && git add . && git commit -m "Fix typo WIP"
echo "add test" >> file.txt && git add . && git commit -m "Add test WIP"
```

2. View history:
```bash
git log --oneline
# abc123d Add test WIP
# def456e Fix typo WIP
# ghi789f Add feature
```

3. Interactive rebase to squash:
```bash
git rebase -i HEAD~2
```

4. In the editor, change to:
```
pick ghi789f Add feature
squash def456e Fix typo WIP
squash abc123d Add test WIP
```

5. Save and editor shows final message. Clean it up:
```
Add feature with fixes and tests
```

6. View cleaned history:
```bash
git log --oneline
# xyz789u Add feature with fixes and tests
# (previous commits are gone)
```

**Solution**: Interactive rebase combined three commits into one clean commit. Useful before pushing to clean up work-in-progress commits.

### Exercise 6: Working with Remotes (Local Simulation)

**Objective**: Simulate remote operations locally.

**Steps:**

1. Create a "remote" repository (bare repo):
```bash
mkdir remote-repo.git
cd remote-repo.git
git init --bare
```

2. Create local repo and add remote:
```bash
cd ..
mkdir local-repo
cd local-repo
git init
git remote add origin ../remote-repo.git
```

3. Make commits and push:
```bash
echo "Hello" > file.txt
git add file.txt
git commit -m "Initial commit"
git push -u origin main
# Uploads to "remote"
```

4. Create another local clone:
```bash
cd ..
git clone remote-repo.git clone-repo
cd clone-repo
git log --oneline
# See the commit from original repo
```

5. Make changes in clone and push:
```bash
echo "Change in clone" > file.txt
git add file.txt
git commit -m "Clone change"
git push origin main
```

6. Fetch changes in original repo:
```bash
cd ../local-repo
git fetch origin
git log origin/main --oneline
# See the clone's commit
git merge origin/main
cat file.txt
# "Change in clone"
```

**Solution**: This simulates real remote workflows using local directories. You've practiced push, clone, fetch, and merge.

### Capstone Project: Simulated Team Workflow

**Objective**: Put it all together with a realistic team scenario.

**Scenario**: You and a colleague are building a web application. You need to:
- Create branches for features
- Make multiple commits
- Create pull requests (simulated with branches)
- Handle merge conflicts
- Review code
- Deploy releases with tags

**Steps:**

1. **Initialize the "project":**
```bash
mkdir team-project
cd team-project
git init
echo "# Web App" > README.md
git add README.md
git commit -m "Initial project setup"
```

2. **You work on authentication:**
```bash
git switch -c feature/auth
echo "login() {}" > auth.js
git add auth.js
git commit -m "feat(auth): add login function"

echo "logout() {}" >> auth.js
git add auth.js
git commit -m "feat(auth): add logout function"
```

3. **Colleague works on dashboard (simulated):**
```bash
git switch main
git switch -c feature/dashboard
echo "dashboard() {}" > dashboard.js
git add dashboard.js
git commit -m "feat(dashboard): add dashboard component"
```

4. **You make more changes (back to auth):**
```bash
git switch feature/auth
echo "// Secure auth" > comment.txt
git add comment.txt
git commit -m "docs(auth): add security notes"
```

5. **Both branches are ready. Merge dashboard first:**
```bash
git switch main
git merge feature/dashboard
```

6. **Now merge auth (might have conflict if editing same files):**
```bash
git merge feature/auth
# If conflict, resolve manually
```

7. **Create a release tag:**
```bash
git tag -a v1.0.0 -m "Version 1.0.0: Initial release"
```

8. **Create "hotfix" for a bug:**
```bash
git switch -c hotfix/security-patch main
echo "// Fixed security issue" > security.js
git add security.js
git commit -m "fix(security): patch vulnerability"
git switch main
git merge hotfix/security-patch
git tag -a v1.0.1 -m "Version 1.0.1: Security patch"
```

9. **View final history:**
```bash
git log --oneline --graph --all --decorate
```

10. **Cleanup:**
```bash
git branch -d feature/auth feature/dashboard hotfix/security-patch
```

**Expected output** (step 9):
```
* abc123d (HEAD -> main, tag: v1.0.1) fix(security): patch vulnerability
*   def456e (tag: v1.0.0) Merge branch 'feature/auth'
|\
| * ghi789f docs(auth): add security notes
| * jkl012m feat(auth): add logout function
| * mno345p feat(auth): add login function
|/
* pqr678s Merge branch 'feature/dashboard'
|\
| * stu901t feat(dashboard): add dashboard component
|/
* uvw234x (tag: v0.1.0) Initial project setup
```

**Solution**: This capstone demonstrates a complete workflow with multiple features, merging, conflict resolution, tagging for releases, and hotfixes. You've practiced most Git skills in a realistic scenario.

### Quiz: Check Your Knowledge

**Question 1**: What command creates a new commit that undoes a previous commit without rewriting history?
**Answer**: `git revert <commit>`

**Question 2**: When is it safe to use `git reset --hard`?
**Answer**: Only on local branches that haven't been pushed, or when you're absolutely sure you want to discard work.

**Question 3**: What's the difference between `git merge` and `git rebase`?
**Answer**: Merge creates a merge commit and preserves all history. Rebase replays commits on top of another branch, creating a linear history.

**Question 4**: How do you recover a commit that was accidentally deleted?
**Answer**: Use `git reflog` to find the commit hash, then `git checkout -b <branch> <hash>` to recover it.

**Question 5**: What file tells Git which files to ignore?
**Answer**: `.gitignore`

**Question 6**: What does `git stash` do?
**Answer**: Temporarily saves uncommitted changes without committing them, allowing you to switch branches.

**Question 7**: What's the safest way to undo a commit that's already been pushed?
**Answer**: `git revert <commit>` (creates a new commit that undoes it) rather than `git reset` (rewrites history).

**Question 8**: How do you set an upstream branch for tracking?
**Answer**: `git branch --set-upstream-to=origin/main main` or `git push -u origin <branch>`

---

## 15. Further Learning

### Official Resources

- **Pro Git Book**: https://git-scm.com/book/en/v2 (Free, comprehensive, written by Git authors)
- **Git Official Documentation**: https://git-scm.com/doc (Reference guide for all commands)
- **GitHub Learning Lab**: Interactive tutorials from GitHub
- **Git Koans**: Philosophical approach to learning Git fundamentals

### Tools and GUIs

While mastering command-line Git is important, these tools can assist:

- **GitKraken**: Cross-platform GUI with beautiful visualization
- **Sourcetree**: Free from Atlassian, good for visual branch management
- **GitHub Desktop**: Simplified interface for common operations
- **tig**: Terminal UI for Git
- **lazygit**: Terminal UI with keybindings for power users
- **VS Code Git Extensions**: Integrated Git features in your editor

### Advanced Learning

- **Git Internals**: Read `.git` directory structure in depth
- **Custom Git Hooks**: Automate workflows with pre-commit, husky
- **GitOps**: Version control for infrastructure and deployments
- **Monorepos**: Managing multiple projects in one repo (Monorepo tools)
- **Git Performance**: Tuning for large repositories (Scalar, GVFS)

### Practice Platforms

- **GitHub**: Create repositories, contribute to open-source
- **LeetCode**: Some problems require Git commands
- **Codewars**: Community challenges with Git workflows
- **First-Time Contributor Guides**: Open-source projects welcoming beginners

### Books and Courses

- **"Mastering Git" by Jon Loeliger**: Deep dive into Git internals
- **"Git In Practice" by Mike McQuaid**: Real-world scenarios
- **Pluralsight / Udemy**: Video courses (paid)
- **freeCodeCamp**: Free comprehensive courses on YouTube

---

## Conclusion

You've now mastered Git from absolute beginner to advanced practitioner. You understand:

- How Git works under the hood (objects, refs, staging)
- Day-to-day commands and workflows
- Advanced techniques (rebasing, cherry-picking, bisecting)
- Collaboration and remote operations
- Professional workflows and best practices
- How to recover from mistakes

**Key Principles to Remember:**

1. **Commit often** with clear messages
2. **Branch fearlessly** — branches are cheap
3. **Pull before you push** — stay in sync
4. **Never force push shared history** — use revert instead
5. **Review code carefully** — second eyes catch bugs
6. **Use meaningful commit messages** — future you will thank you
7. **Practice regularly** — Git mastery comes from repetition

**You are now equipped to:**

- Work confidently on any project
- Collaborate effectively with teams
- Handle complex Git situations
- Recover from mistakes gracefully
- Follow professional development practices
- Contribute to open-source projects

The only way to truly master Git is to use it daily. Start with the basics, gradually explore advanced features, and build confidence through practice. Every Git expert was once a beginner who faced confusing merge conflicts and lost commits.

**Your journey to Git mastery has just begun. Happy committing!**

---

## Quick Reference: Essential Commands by Category

### Initialization & Setup
```bash
git init                          # Create new repo
git clone <url>                   # Clone repo
git config user.name "Name"       # Set user name
git config user.email "email"     # Set user email
```

### Checking Status
```bash
git status                        # Current status
git log                           # Commit history
git diff                          # Unstaged changes
git diff --staged                 # Staged changes
```

### Making Changes
```bash
git add <file>                    # Stage file
git add .                         # Stage all
git commit -m "<message>"         # Create commit
git commit --amend                # Modify last commit
git restore <file>                # Discard changes
```

### Branching
```bash
git branch                        # List branches
git branch <name>                 # Create branch
git switch <name>                 # Switch branch
git switch -c <name>              # Create and switch
git merge <name>                  # Merge branch
git branch -d <name>              # Delete branch
```

### Undoing
```bash
git reset --soft HEAD~1           # Undo, keep staged
git reset HEAD~1                  # Undo, keep unstaged
git reset --hard HEAD~1           # Undo, discard all
git revert <commit>               # Create undo commit
git reflog                        # Find lost commits
```

### Remote Operations
```bash
git remote add origin <url>       # Add remote
git fetch origin                  # Download changes
git pull origin main              # Fetch and merge
git push origin main              # Upload changes
git push -u origin <branch>       # Push new branch
```

### Searching & Debugging
```bash
git log --all --graph --oneline   # Visualize history
git blame <file>                  # See who changed what
git bisect                        # Find bug-causing commit
git grep "<pattern>"              # Search code
```

### Cleanup & Organization
```bash
git stash                         # Save work temporarily
git stash pop                     # Restore saved work
git clean -fd                     # Remove untracked files
git tag -a v1.0 -m "Release"     # Create release tag
```

---

**End of Complete Git and GitHub Mastery Guide**

This comprehensive guide covers everything you need to become a Git expert. Return to this document whenever you need clarification, and remember that the best way to learn is by doing. Create repositories, make mistakes, explore recovery techniques, and gradually build your Git proficiency through regular practice.

Master Git, and you've mastered collaboration, version control, and professional software development.
