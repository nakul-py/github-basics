# Github Basics

- [🧲 00 - How to Clone a GitHub Repository](https://github.com/nakul-py/github-basics#-00---how-to-clone-a-github-repository)

- [🌿 01 - Branches in Git](https://github.com/nakul-py/github-basics#-01---branches-in-git)

- [🚀 02 - Git Add, Stash, and Push](https://github.com/nakul-py/github-basics#-02---git-add-stash-and-push)

- [📜 03 - Viewing Commit History with git log](https://github.com/nakul-py/github-basics#-03---viewing-commit-history-with-git-log)

- [🗑️ 04 - Remove a Commit, Push, and Retrieve It (Force Push & Recovery)](https://github.com/nakul-py/github-basics#%EF%B8%8F-04---remove-a-commit-push-and-retrieve-it-force-push--recovery)

- [🚀 05 - Pulling Updates from a Remote Repository
](https://github.com/nakul-py/github-basics#-05---pulling-updates-from-a-remote-repository)

- [📌 06 - Working with Remotes](https://github.com/nakul-py/github-basics#-06---working-with-remotes)

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

#### 🧩 Forcing a File to Be Tracked

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

------------------------------------------------------------------------------------------------

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

------------------------------------------------------------------------------------------------

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

## 📜 03 - Viewing Commit History with `git log`

### 🧠 What is `git log`?

`git log` shows the history of commits in your current branch — what was committed, by whom, and when.

### 🔧 Basic Usage

```bash
git log
```

Output:

```sql
commit 6e4f3f8f (HEAD -> feature-xyz, origin/feature-xyz)
Author: Firstname Lastname <user@example.com>
Date:   Sun Jan 1 00:00:00 2022 +0000

    feat: Add new file
```

### 🧩 Useful Options

| Command                        | What it does                                        |
| ------------------------------ | --------------------------------------------------- |
| `git log --oneline`            | Show each commit in one line (short hash + message) |
| `git log --graph`              | Show a visual commit tree                           |
| `git log -p`                   | Show the diff introduced by each commit             |
| `git log --stat`               | Show files changed + insertions/deletions           |
| `git log --author="nakul"`     | Show commits by a specific author                   |
| `git log --since="2 days ago"` | Show recent commits                                 |
| `git log -- <filename>`        | Show commits that touched a specific file           |

## 🗑️ 04 - Remove a Commit, Push, and Retrieve It (Force Push & Recovery)

### 🧾 Use git log to Find a Commit

```bash
git log
```

--------------------------------------------------------------------------------------------------------

### ❌ How to Remove the Last Commit

#### 🔹 1. Remove last commit but keep changes (editable)

```bash
git reset --soft HEAD~1
```

This keeps your changes in staging (`git status` will show them as "to be committed").

#### 🔹 2. Remove last commit and unstage changes

```bash
git reset --mixed HEAD~1
```

Changes go back to the working directory, not staged.

#### 🔹 3. Remove last commit and discard changes (permanent)

```bash
git reset --hard HEAD~1
```

⚠️ This deletes the commit and all local changes.

____________________________________________________________________________

### 🚀 Push the Updated History

After removing a commit, your local branch history is now different **HEAD** from the remote. So you'll need to force push:

```bash
git push origin --force
```

### 🔄 Retrieve a Removed Commit (If You Didn't Hard Reset)

You can retrieve commits even after removal, if they haven’t been garbage collected.

#### 🕵️ Find the commit hash

```bash
git reflog
```

This shows a log of all HEAD movements — even ones you've undone.

Example:

```kotlin
abc1234 HEAD@{1}: commit: added something
```

#### 🧙‍♂️ Recover it

```bash
git checkout abc1234
# or
git reset --hard abc1234
```

### 🧠 Tip: Safer Way to Undo Commits

Instead of `git reset`, you can also use `git revert`:

```bash
git revert HEAD
```

This creates a **new commit** that undoes the last one — safer for public branches.

## 🚀 05 - Pulling Updates from a Remote Repository

### 🧠 What is `git pull`?

`git pull` updates your local branch with the latest changes from the remote repository.

### 🔧 Common Command

```bash
git pull
```

---------------------------------------------------------------------------------------------------

### 🧙 What is `git fetch`?

`git fetch` downloads updates from the remote repository without merging them into your local branch.

### 🔧 Common Command

```bash
git fetch
```

-------------------------------------------------------------------------------------------------------

### 🚀 What is `git merge`?

`git merge` merges changes from one branch into another.

### 🔧 Common Command

```bash
git merge feature-xyz
```

-------------------------------------------------------------------------------------------------------

### 🚀 What is `git rebase`?

`git rebase` updates the history of a branch by applying the commits from another branch on top of it.

### 🔧 Common Command

```bash
git rebase feature-xyz
```

-------------------------------------------------------------------------------------------------------

### 🚀 What is `git reset`?

`git reset` undoes local changes to tracked files.

### 🔧 Common Command

```bash
git reset --hard HEAD
```

-------------------------------------------------------------------------------------------------------

## 📌 06 - Working with Remotes

### 🧠 What is `git remote`?

`git remote` lets you list and add remotes.

### 🔧 Common Commands

- List remotes:

```bash
git remote
```

- Add a remote:

```bash
git remote add origin https://github.com/username/repo-name.git
```

- Remove a remote:

```bash
git remote remove origin
```

-------------------------------------------------------------------------------------------------------
