# Github Basics

## 🧲 00 - How to Clone a GitHub Repository

### 🚀 **What Does “Cloning” Mean?**

Cloning means copying a remote Git repository to your local machine. This lets you work with the project files, branches, and history locally.

### 🔧 Requirements

✅ You need:

- Git installed (git --version to check)
- A GitHub account (for some repos)
- SSH or HTTPS access to the repo.

### 🌐 Choose a Clone URL

You can clone via:

- **HTTPS** (recommended for beginners)

- **SSH** (for advanced users with SSH keys)

Example GitHub repo URL:

```arduino
https://github.com/username/repo-name.git
```

### 🛠 Clone the Repo

```bash
git clone https://github.com/username/repo-name.git
```

This will:

- Create a folder named `repo-name`

- Copy all code, commit history, and branches into it

### 🧭 Navigate Into the Project

```bash
cd repo-name
```

### 📌 Check the Remote URL

```bash
git remote -v
```

Output:

```perl
origin  https://github.com/username/repo-name.git (fetch)
origin  https://github.com/username/repo-name.git (push)
```

## 🌿 01 - Branches in Git

### 🧠 What is a Branch?

A branch in Git lets you work on a separate line of development without affecting the main project. You can:

- Try new features

- Fix bugs

- Work independently

The default branch is usually called `main` (or `master` in older repos).

### 🔧 Basic Branch Commands

#### 🧾 View Branches

```bash
git branch
```

#### 🌱 Create a New Branch

```bash
git branch feature-xyz
```

#### 🔁 Switch to a Branch

```bash
git checkout feature-xyz
```

Or in one step (Git 2.23+):

```bash
git checkout -b feature-xyz

# or

git switch -b feature-xyz
```

#### 📂 List Remote Branches

```bash
git branch -r
```

#### 🔄 Merge a Branch into main

```bash
git checkout main
git merge feature-xyz
```

#### 🧼 Delete a Branch

```bash
git branch -d feature-xyz    # Only if merged
git branch -D feature-xyz    # Force delete
```

## 🚀 02 - Git Add, Stash, and Push

### 📦 What is `git add`?

`git add` tells Git you want to include changes in the next commit.

#### 🔧 Common Commands

- Add a single file:

```bash
git add filename.txt
```

- Add all changed files:

```bash
git add .
```

#### 🧩 Forcing a File to Be Tracked:

Sometimes, Git will ignore files listed in .gitignore. But what if you intentionally want to commit one of those ignored files?

For example:

```bash
git add --force .yarnclean 

# or

git add --force filename.txt
```
This command means:

- `git add` → Stage the file

- `-f` or `--force` → Force Git to add the file even if it’s ignored

- `.yarnclean` → The file used by Yarn to clean unnecessary packages

#### 💡 Why This is Useful

In some projects, .yarnclean or any other file is added to .gitignore, but you might still want to track it for consistent cleanup across machines.

### 🧙 What is `git stash`?

`git stash` temporarily saves uncommitted changes, letting you switch branches or pull updates without losing work.

#### 🔧 Common Commands

- Stash current changes:

```bash
git stash
```

- View stashed changes:

```bash
git stash list
```

- Re-apply last stashed changes:

```bash
git stash pop
```

- Drop a stash (delete it):

```bash
git stash drop
```

Tip: Use `git stash -u` or `git stash --include-untracked` to include untracked files too.

### 🚀 What is `git push`?

`git push` sends your local commits to the remote repository.

🔧 Common Commands

- Push current branch:

```bash
git push origin branch-name
```

- Push and set upstream (first time):

```bash
git push --set-upstream origin branch-name

# or

git push -u origin branch-name
```

