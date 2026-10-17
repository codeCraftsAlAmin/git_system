# Git & GitHub Workflow Guide

A beginner-friendly reference guide designed to simplify Git and GitHub, streamline everyday commands, and help developers follow professional development workflows.

## Table of Contents

1. [Push an Existing Project to GitHub](#1-push-an-existing-project-to-github)
2. [Update and Push Changes](#2-update-and-push-changes)
3. [Clone a Repository](#3-clone-a-repository)
4. [Check and Remove Remote Repositories](#4-check-and-remove-remote-repositories)
5. [Remove Git Tracking](#5-remove-git-tracking)
6. [Pull the Latest Changes](#6-pull-the-latest-changes)
7. [Git Branches](#7-git-branches)
8. [Commit Message Conventions](#8-commit-message-conventions)
9. [Switch Between Branches](#9-switch-between-branches)
10. [Handle Uncommitted Changes](#10-handle-uncommitted-changes)
11. [Check Merged and Unmerged Branches](#11-check-merged-and-unmerged-branches)
12. [Delete Branches](#12-delete-branches)
13. [Create a Pull Request](#13-create-a-pull-request)
14. [Check Repository Status](#14-check-repository-status)
15. [Quick Reference](#15-quick-reference)
16. [Best Practices](#16-best-practices)

---

## 1. Push an Existing Project to GitHub

After creating a new repository on GitHub, follow these steps to push your local project.

### Step 1: Initialize Git

```bash
git init
```

### Step 2: Connect to the Remote Repository

Replace `<repository-url>` with your GitHub repository URL.

```bash
git remote add origin <repository-url>
```

### Step 3: Set the Default Branch Name

Rename the current branch to `main`.

```bash
git branch -M main
```

### Step 4: Stage Your Files

```bash
git add .
```

### Step 5: Create Your First Commit

```bash
git commit -m "chore: initial project setup"
```

### Step 6: Push Your Code to GitHub

```bash
git push -u origin main
```

## **Note:** The `-u` flag sets the upstream branch. After the initial push, you can usually use `git push` and `git pull` without specifying the remote and branch.

## 2. Update and Push Changes

Whenever you make changes to your project, follow this workflow:

```bash
git status
git add .
git commit -m "fix: refactor user validation logic"
git push
```

### What Each Command Does

- `git status` — Shows the current state of your working tree.
- `git add .` — Stages changes in the current directory and its subdirectories.
- `git commit -m "..."` — Saves staged changes as a commit.
- `git push` — Uploads local commits to the configured remote branch.
  **Best Practice:** Make small, focused commits and use descriptive messages that explain the purpose of each change.

---

## 3. Clone a Repository

Use `git clone` to download an existing remote repository to your local computer, including its Git history and the default checkout of a branch.

### Clone a Repository

```bash
git clone <repository-url>
```

**Example:**

```bash
git clone https://github.com/username/repository-name.git
```

This creates a local directory named after the repository.

### Clone into a Specific Folder

```bash
git clone <repository-url> <folder-name>
```

**Example:**

```bash
git clone https://github.com/username/repository-name.git my-project
```

### Navigate into the Project

```bash
cd repository-name
```

If you specified a custom folder name, use that name instead.

### Clone a Specific Branch

```bash
git clone --branch <branch-name> <repository-url>
```

**Example:**

```bash
git clone --branch develop https://github.com/username/repository-name.git
```

**Best Practice:**

- Use `git clone` when you want to work on an existing remote repository.
- Use `git init` when starting a new local project that is not already a Git repository.
- After cloning, run `git status` to check your current branch and working tree.

---

## 4. Check and Remove Remote Repositories

### Check Configured Remotes

```bash
git remote -v
```

This displays the URLs associated with your configured remotes.

### Remove a Remote

```bash
git remote remove origin
```

This removes the remote configuration named `origin` from your local repository. It does not delete the repository from GitHub.

### Add a New Remote

```bash
git remote add origin <new-repository-url>
```

---

## 5. Remove Git Tracking

If you want to remove Git tracking from your local project, run the following command in PowerShell:

```powershell
Remove-Item -Recurse -Force .git
```

**Warning:** This deletes the local `.git` directory, including the repository's commit history, branches, and configuration. Your project files normally remain intact, but the local Git history and metadata are removed.
This command does not delete the remote GitHub repository.
Only run this command when you intentionally want to remove the local Git repository.

---

## 6. Pull the Latest Changes

Use `git pull` to fetch changes from a remote repository and integrate them into your current branch.

```bash
git pull origin main
```

This command does not automatically switch you to `main`. It integrates the remote `main` branch into whichever branch you are currently on.

### Recommended Team Workflow

Before starting new work, synchronize your local `main` branch with the remote repository.

```bash
git status
git switch main
git pull origin main
```

If you are working on a feature branch, update `main` first and then integrate the latest changes into your feature branch according to your team's workflow.
**Important:** Commit or stash local changes before pulling if they might conflict with incoming changes.

---

## 7. Git Branches

Branches allow developers to work on features, bug fixes, and experiments independently without directly changing the main development line.
Think of a branch as an independent workspace where you can develop and test changes before integrating them into the main codebase.

### Why Do We Use Branches?

- Keep the `main` branch stable.
- Develop features independently.
- Fix bugs without interrupting unrelated work.
- Make code reviews easier.
- Reduce the risk of introducing unfinished changes into production.

### Common Branch Naming Conventions

| Purpose               | Example                 |
| --------------------- | ----------------------- |
| New feature           | `feature/jwt-auth`      |
| Bug fix               | `fix/user-login-error`  |
| Refactoring           | `refactor/async-db`     |
| Documentation         | `docs/update-readme`    |
| Urgent production fix | `hotfix/payment-error`  |

Follow your team's branch naming conventions if they differ from these examples.

### Create and Push a New Branch

**Step 1: Create and switch to a new branch**

```bash
git switch -c feature/async-postgres
```

**Step 2: Stage your changes**

```bash
git add .
```

**Step 3: Commit your changes**

```bash
git commit -m "feat: add asynchronous PostgreSQL support"
```

**Step 4: Push the branch to GitHub**

```bash
git push -u origin feature/async-postgres
```

The `-u` flag establishes upstream tracking for the new branch.

### Professional Team Workflow

In many professional projects, developers do not push feature work directly to `main`. Instead, they:

1. Create a feature or bug-fix branch.
2. Implement and test the changes.
3. Commit and push the branch.
4. Open a Pull Request (PR).
5. Request a code review.
6. Resolve review comments and automated check failures.
7. Merge the PR after approval and required checks pass.
   **Note:** Follow your team's branch protection rules and contribution guidelines.

---

## 8. Commit Message Conventions

A good commit message describes the purpose of a change clearly and concisely.
A common convention is **Conventional Commits**.

### Common Commit Types

| Type        | Purpose                                              | Example                                  |
| ----------- | ---------------------------------------------------- | ---------------------------------------- |
| `feat`      | Introduce a new feature                              | `feat: add user login endpoint`          |
| `fix`       | Fix a bug                                            | `fix: resolve database deletion error`   |
| `refactor`  | Restructure code without changing intended behavior  | `refactor: simplify user service logic`  |
| `docs`      | Update documentation                                 | `docs: update README`                    |
| `test`      | Add or update tests                                  | `test: add user registration tests`      |
| `chore`     | Maintenance and tooling changes                      | `chore: update dependencies`             |
| `style`     | Formatting changes without affecting logic           | `style: format API route handlers`       |
| `perf`      | Improve performance                                  | `perf: optimize database queries`        |

### Examples

```bash
git commit -m "feat: add user registration endpoint"
git commit -m "fix: handle invalid login credentials"
git commit -m "refactor: simplify authentication service"
git commit -m "docs: update installation instructions"
```

### Best Practices

- Keep commit messages concise and descriptive.
- Use the imperative mood, such as `add`, `fix`, or `update`.
- Keep each commit focused on a logical change.
- Avoid vague messages such as `update`, `changes`, or `final code`.

---

## 9. Switch Between Branches

### List Local Branches

```bash
git branch
```

The current branch is marked with an asterisk (`*`).

### Switch to an Existing Branch

```bash
git switch <branch-name>
```

**Example:**

```bash
git switch main
```

### Create and Switch to a New Branch

```bash
git switch -c feature/user-profile
```

### The Classic Alternative

The older `checkout` command is also valid:

```bash
git checkout <branch-name>
```

Create and switch to a new branch using:

```bash
git checkout -b feature/user-profile
```

## For everyday branch operations, `git switch` is generally clearer because it separates branch switching from other checkout operations.

## 10. Handle Uncommitted Changes

Git may prevent you from switching branches when your local changes would be overwritten.
You can handle this in two common ways.

### Option A: Commit Your Work

If your changes are ready to save, create a commit.

```bash
git add .
git commit -m "WIP: save current progress"
```

`WIP` means _Work in Progress_. Use this type of commit when it fits your team's workflow.

### Option B: Stash Your Changes

If your work is unfinished and you do not want to commit it yet, stash your changes temporarily.

```bash
git stash push -u -m "temporary work"
```

The `-u` flag includes untracked files.
Now switch branches:

```bash
git switch <branch-name>
```

Return to the previous branch when needed:

```bash
git switch -
```

Restore your stashed changes:

```bash
git stash pop
```

### Useful Stash Commands

| Command            | Purpose                                                              |
| ------------------ | -------------------------------------------------------------------- |
| `git stash list`   | List saved stashes                                                   |
| `git stash apply`  | Restore a stash without removing it from the list                    |
| `git stash pop`    | Restore a stash and remove it from the list if successfully applied  |
| `git stash drop`   | Remove a stash entry                                                 |

## **Tip:** Resolve any conflicts carefully if they occur while restoring a stash.

## 11. Check Merged and Unmerged Branches

Before deleting a local branch, check whether its changes have been merged into your target branch.

### Step 1: Switch to the Target Branch

```bash
git switch main
```

### Step 2: List Fully Merged Branches

```bash
git branch --merged main
```

These branches have been merged into `main` according to Git's branch ancestry information.

### Step 3: List Unmerged Branches

```bash
git branch --no-merged main
```

These branches have commits that are not reachable from `main`.
**Important:** An unmerged branch may contain valuable work. Review it before deleting it. A branch not listed as merged is not necessarily safe to discard.

---

## 12. Delete Branches

Once a feature branch is no longer needed, you can clean it up locally and remotely.

### Delete a Local Branch

First, switch to another branch:

```bash
git switch main
```

Delete a branch that Git considers safely merged:

```bash
git branch -d <branch-name>
```

Force-delete a local branch:

```bash
git branch -D <branch-name>
```

**Warning:** The `-D` flag deletes the local branch even if Git detects unmerged commits. Make sure you no longer need that work.

### Delete a Remote Branch

```bash
git push origin --delete <branch-name>
```

This deletes the branch from the remote repository, assuming you have permission.

### Clean Up Stale Remote-Tracking References

```bash
git fetch --prune
```

## This removes local remote-tracking references for branches that no longer exist on the remote. It does not delete your local branches.

## 13. Create a Pull Request

A Pull Request (PR) allows developers to propose changes, review code, discuss implementation details, and merge approved changes into a target branch.

### Method 1: Create a PR on GitHub

**Step 1: Push your branch**

```bash
git push -u origin <branch-name>
```

**Step 2:** Open your repository on GitHub.
**Step 3:** Navigate to the **Pull requests** tab and select **New pull request**, or use GitHub's suggested **Compare & pull request** option if it appears.
**Step 4:** Select the correct base branch (usually `main` or `develop`) and your feature branch.
**Step 5:** Add a descriptive title and summary, review the changes, and click **Create pull request**.
**Step 6:** Respond to review comments, update your branch when needed, and wait for required approvals and checks.

### Method 2: Create a PR Using GitHub CLI

GitHub CLI (`gh`) is the official command-line tool for working with GitHub.

#### Install GitHub CLI

**Windows (PowerShell):**

```powershell
winget install --id GitHub.cli
```

**macOS (Homebrew):**

```bash
brew install gh
```

**Ubuntu/Debian:**

```bash
sudo apt install gh
```

Installation methods and package availability may vary by operating system.

#### Authenticate with GitHub

```bash
gh auth login
```

Follow the prompts to authenticate your account.

#### Open the PR Creation Page

```bash
gh pr create --web
```

This opens the Pull Request creation page in your browser.
Alternatively, create a PR from the terminal:

```bash
gh pr create --base main --head feature/user-profile --title "feat: add user profile" --body "Adds user profile functionality."
```

## Replace the branch names, title, and description with your actual changes.

## 14. Merge a Feature Branch into Main

After completing your feature branch, push the latest code to the remote repository before merging. In a team environment, follow your team's Pull Request and code-review process instead of merging directly when required.
Step 1: Commit and Push Your Latest Changes
Make sure your work is committed and pushed to your current feature branch.
git status
git add .
git commit -m "feat: complete async PostgreSQL authentication"
git push
If this is the first time you are pushing the branch, set its upstream:
git push -u origin feature/async-postgres-auth
If there are no new changes to commit, skip the commit command.
Step 2: Switch to the Main Branch
git switch main
Step 3: Update the Local Main Branch
git pull origin main
This ensures your local main branch includes the latest remote changes before you merge.
Step 4: Merge the Feature Branch into Main
git merge feature/async-postgres-auth
Replace feature/async-postgres-auth with the name of your feature branch.
If Git reports merge conflicts, resolve them in the affected files, then stage and commit the resolutions before continuing.
Step 5: Push Main to the Remote Repository
git push origin main
This pushes the merge commit and the merged feature changes to the remote main branch.
Verify the Merge
git status
git log --oneline --graph --decorate -10
Important: Directly pushing to main may be blocked by branch protection rules. In team projects, open a Pull Request and merge it after the required reviews and checks pass. Only merge and push directly when your project workflow permits it. 15. Check Repository Status
The `git status` command provides a snapshot of your current working tree and staging area.

```bash
git status
```

It helps you understand what has changed before committing, switching branches, or pushing code.

### What Does `git status` Show?

**1. Current Branch**
Shows the branch you are currently working on.
**2. Untracked Files**
New files Git has not started tracking.
**3. Changes Not Staged for Commit**
Tracked files that have been modified but whose latest changes have not been staged.
**4. Changes to Be Committed**
Changes staged with `git add` and ready for the next commit.
**5. Branch Synchronization**
When upstream tracking is configured and the relevant information is available, Git can indicate whether your local branch is ahead of or behind its upstream branch.

### The Three Main File States

| State      | Meaning                                   | Next Step                  |
| ---------- | ----------------------------------------- | -------------------------- |
| Untracked  | Git is not tracking the new file yet      | `git add <file>`           |
| Modified   | A tracked file has been changed           | `git add <file>`           |
| Staged     | Changes are prepared for the next commit  | `git commit -m "message"`  |

### Recommended Habit

Run `git status` frequently, especially:

- Before staging files.
- Before creating a commit.
- Before switching branches.
- Before pushing changes.
- After resolving merge conflicts.
  `git status` is a read-only command. It does not modify or delete your project files.

---

## 16. Quick Reference

| Command                    | Purpose                                                    |
| -------------------------- | ---------------------------------------------------------- |
| `git init`                 | Initialize a repository                                    |
| `git clone <url>`          | Clone an existing repository                               |
| `git status`               | Check the working tree                                     |
| `git add .`                | Stage changes in the current directory and subdirectories  |
| `git commit -m "message"`  | Create a commit                                            |
| `git push`                 | Push commits to the configured upstream                    |
| `git pull`                 | Fetch and integrate upstream changes                       |
| `git fetch`                | Download remote updates without integrating them           |
| `git branch`               | List local branches                                        |
| `git switch <branch>`      | Switch branches                                            |
| `git switch -c <branch>`   | Create and switch to a branch                              |
| `git log --oneline`        | View a compact commit history                              |
| `git diff`                 | Review unstaged changes                                    |
| `git diff --staged`        | Review staged changes                                      |
| `git stash`                | Temporarily save local changes                             |
| `git remote -v`            | List remote URLs                                           |
| `git fetch --prune`        | Remove stale remote-tracking references                    |

---

## 17. Best Practices

- **Keep `main` stable:** Follow your team's branch protection and review policies.
- **Pull or fetch regularly:** Stay informed about changes from other developers.
- **Use feature branches:** Isolate work before integrating it.
- **Write meaningful commits:** Make each commit focused and easy to review.
- **Review before committing:** Use `git status` and `git diff`.
- **Open Pull Requests:** Make code review part of your workflow.
- **Resolve conflicts carefully:** Review both sides before accepting changes.
- **Protect sensitive data:** Never commit passwords, API keys, access tokens, or `.env` files.
- **Use `.gitignore`:** Exclude generated files, dependencies, local configuration, and other files that should not be tracked.
- **Understand destructive commands:** Be cautious with `git reset --hard`, `git clean`, and `git branch -D`.

---

> **Remember:** Git is more than a tool for uploading code. It is a version control system that helps developers track changes, collaborate safely, and maintain a reliable development workflow.
