After creating a new repo go to your CMD and write these command

## Push Code to Git

1. Initialize git in your project folder:

```
git init
```

2. Connect to remote repo:

```
git remote add origin <your-repository-URL>
```

3. Confirm default branch name(Main):

```
git branch -M main
```

4. Tracking files and commit:

```
git add .
git commit -m "feat: initial project setup"
```

5. Push to remote repo:

```
git push -u origin main
```

---

## Check Remote

```
git remote -v
```

## Remove Remote

1. Check your current repo:

```
git remote -v
```

2. Remove remote:

```
git remote remove origin
```

3. Delete git folder in powershall:

```
Remove-Item -Rescurse -Force .git
```

---
