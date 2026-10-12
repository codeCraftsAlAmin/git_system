After creating a new repo go to your CMD and write these command

## Push Code to Git

1. Initialize git in your project folder
2. Connect to remote repo
3. Confirm default branch name(Main)
4. Tracking files and commit
5. Push to remote repo

```
git init
git remote add origin <your-repository-URL>
git branch -M main
git add .
git commit -m "feat: initial project setup"
git push -u origin main
```

---

## Update git push

```
git add .
git commit "fix: refector the code"
git push
```

---

## Check & remove Remote

```
git remote -v
git remote remove origin
```

3. Delete git folder in powershall:

```
Remove-Item -Rescurse -Force .git
```

---

## Git Pull

We pull code from Git to synchronize our local computer with the latest changes made by other developers on the remote repository (like GitHub or GitLab):
**\*Industry Tips**: before you start coding always try to pull the latest code so that you stay syncked with the lastest code

```
git pull origin main
```

---

## Git Branch

We use branches in Git to isolate our work so we can develop new features, fix bugs, or test ideas safely without affecting the main, stable code.
Think of a branch as your own independent workspace or a "parallel universe" for your project. While the main branch holds production-ready code, a branch lets you make changes freely

**\*Note:** in real an industry project we do not push code to main/master brnach directly. main branch is always for production ready and keep stable

When to create branch:

1. To add feature(e.g: feature/jwt-auth)
2. To fix bugs(e.g: bugfix/user-login-error)
3. To refector or experement the code(e.g: refactor/async-db)

Step-by-Step Workflow:

1. Create and switch to your new branch locally
2. Stage your changes to prepare them for tracking
3. Commit your changes with a descriptive message:
4. Push the branch to the remote repository and set up upstream tracking:

```
git checkout -b feature/async-postgres
git add .
git commit -m "Add your commit message here"
git push -u origin feature/async-postgres
```

When you should commit?
After completing a certian task you should commit. Here are some industy standard commit message:

```
feat: add user login endpoint (after adding something new)

fix: resolve database delete error (after fixing any bug)

refactor: clean up user service logic (after cleaning the code structure while keep the logic correct)

docs: update readme file (after changing document)
```

**\*Note**: You can not push the code to main branch directly. After completeing you feature branch code you have to open a **Pull Request**. And then your team leader or collegue will review the code and merge it to the main branch

To switch another branch:

1. See your available branches
2. Switch to the branch
3. The Classic Way:

```
git branch
git switch <branch-name>
git checkout <branch-name>
```

What if Git blocks your switch?

If you have uncommitted changes in your current branch, Git might block you from switching to prevent you from losing your work. You have two ways to handle this:

Option A: Commit your work. Save your progress before moving

```
git add .
git commit -m "WIP: save progress"
```

Option B: Stash your work. Stash temporarily hides your changes so you can switch branches without committing unfinished work.

```
git stash                 # Temporarily hide changes
git switch <branch-name>  # Switch to the other branch
# ... do your work ...
git switch -              # Switch back (the dash returns to your previous branch)
git stash pop             # Bring your hidden changes back
```

To check if your branch has been safely merged into your target branch (usually main or develop), you use specific flags with the git branch command.

1. Switch to your main branch
2. List all fully merged branches
3. List unmerged branches

```
git switch main
git branch --merged # if your feature branch is on this list, you can safely delete it using git branch -d
git branch --no-merged # If your branch is on this list, deleting it requires the force command: git branch -D
```

Clean or delete branch:
To cleanly delete a branch, you must first switch to a different branch (like main) because Git will not let you delete the branch you are currently standing on.

1. Switch to a different branch
2. Delete the branch locally
3. Delete the branch on the remote server (GitHub/GitLab)
4. Clean up your local branch list

```

git switch main
git branch -d <branch-name> # if the branch is fully merged (Safe delete)
git branch -D <branch-name> # if the branch is NOT merged (Force delete—use this only if you want to permanently discard the work)
git push origin --delete <branch-name>
git fetch --prune

```

## Open a Pull Request

You can open a Pull Request (PR) either directly on the GitHub website or directly inside your terminal using GitHub's official command-line tool.

**_Method_** 1: On the GitHub Website (The Traditional Way)

1. Push your branch to GitHub if you haven't already

```
git push -u origin <branch-name>
```

2. Go to your repository page on GitHub.
3. Look for a yellow banner at the top that says "Your branch was recently pushed" and click the green "Compare & pull request" button.
4. If you don't see the banner: Click the "Pull requests" tab -> click the green "New pull request" button -> select your feature branch from the dropdown menu.
5. Add a clear title and description of your changes, then click "Create pull request".

**_Method_** 2: Directly from your Terminal (The Fastest Way)
To do this from the terminal, you need **GitHub CLI (gh)**, which is a official tool provided by GitHub.

1. Install GitHub CLI (if you don't have it):

```
Mac: brew install gh
Windows: winget install GitHub.cli
Linux: sudo apt install gh
```

2. Log in to your GitHub account (only required the first time):

```
gh auth login
```

3. Create the PR instantly by typing:

```
gh pr create --web
```

- This will instantly open your browser directly to the PR creation page with everything filled out for you.
- Alternatively, run gh pr create --title "Your Title" --body "Your Description" to do it completely inside the terminal without ever opening a browser.

## Git status

We use the git status command to get our bearings and see exactly what is happening in our repository right now. It acts as a camera snapshot of your current workspace.
It is one of the most frequently used commands because it answers three critical questions before you make your next move

1. Where am I? (Branch Information)
   It immediately tells you which branch you are currently standing on.

2. How do I relate to the server? (Sync Status)
   It checks your local branch against the remote server (like GitHub) and tells you if you are ahead (you have changes to push) or behind (you need to pull your teammates' changes)

3. What have I changed? (The Three File States)
   The core job of git status is to break your files down into three distinct, color-coded categories so you know what will happen when you commit:
   • Untracked files (Usually Red): Brand new files you just created that Git isn't keeping track of yet.
   • Changes not staged for commit (Usually Red): Existing files that you have modified or edited, but haven't officially prepped for saving yet.
   • Changes to be committed (Usually Green): Files that you have run git add on. These are sitting in the staging area and are completely ready to be saved in your next snapshot

**\*Pro Tip**: git status is completely safe to run anytime. It only reads information and will never alter, delete, or break your code. Developers habitually run it right before running a git add, right before a git commit, and right before a git push
