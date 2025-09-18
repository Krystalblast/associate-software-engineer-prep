# 🐙 Git & GitHub Basics

Git is a **version control system** that helps track changes in your code.  
GitHub is a **platform** to host and share Git repositories online.

---

## 🔑 Git Basics

### 1. Setup Git
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 2. Initialize Repository
```bash
git init
```

### 3. Check Status
```bash
git status
```

### 4. Stage Changes
```bash
git add file.txt      # add specific file
git add .             # add all files
```

### 5. Commit Changes
```bash
git commit -m "Your commit message"
```

### 6. View History
```bash
git log
```

---

## 🔗 GitHub Basics

### 1. Create a Repository on GitHub
- Go to [GitHub](https://github.com) → New Repository
- Copy the repo URL (HTTPS or SSH)

### 2. Connect Local Repo to GitHub
```bash
git remote add origin https://github.com/username/repo.git
```

### 3. Push to GitHub
```bash
git branch -M main
git push -u origin main
```

### 4. Clone a Repo
```bash
git clone https://github.com/username/repo.git
```

### 5. Pull Updates
```bash
git pull origin main
```

---

## 🔀 Branching & Merging

### Create a Branch
```bash
git branch feature-branch
git checkout feature-branch
```

Or in one step:
```bash
git checkout -b feature-branch
```

### Merge into Main
```bash
git checkout main
git merge feature-branch
```

---

## 🛠 Useful Commands
```bash
git diff            # see changes
git reset file.txt  # unstage file
git rm file.txt     # remove file from repo
git stash           # save work temporarily
```

---

## 📚 References
- [Git Documentation](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)
- [Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials)
