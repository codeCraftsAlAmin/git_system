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
**Industry Tips**: before you start coding always try to pull the latest code so that you stay syncked with the lastest code

```
git pull origin main
```

---
