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
