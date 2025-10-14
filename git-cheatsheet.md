# 🧠 Git Cheatsheet

A quick reference guide for the most commonly used Git commands.

---

## 🔹 Basic Commands

| Action | Command |
|--------|----------|
| Initialize a new local repository | `git init` |
| Clone a remote repository | `git clone <url>` |
| Check file status | `git status` |
| Add a specific file | `git add <file>` |
| Add all modified files | `git add .` |
| Commit with a message | `git commit -m "message"` |
| Show commit history | `git log` |
| Show compact commit history | `git log --oneline --graph --decorate` |

---

## 🌿 Branch Management

| Action | Command |
|--------|----------|
| List all branches | `git branch` |
| Create a new branch | `git branch <name>` |
| Switch to a branch | `git checkout <name>` |
| Create and switch to a new branch | `git checkout -b <name>` |
| Delete a local branch | `git branch -d <name>` |
| Rename the current branch | `git branch -m <new_name>` |

---

## 🚀 Remote Repositories

| Action | Command |
|--------|----------|
| Add a remote repository | `git remote add origin <url>` |
| View remote repositories | `git remote -v` |
| Push commits to a remote branch | `git push origin <branch>` |
| Push and set upstream branch | `git push -u origin <branch>` |
| Pull updates from the remote | `git pull` |
| Fetch updates without merging | `git fetch` |

---

## ⚔️ Merge & Rebase

| Action | Command |
|--------|----------|
| Merge another branch into the current one | `git merge <branch>` |
| Rebase the current branch onto another | `git rebase <branch>` |
| Abort a merge in progress | `git merge --abort` |
| Resolve conflicts and continue | `git add . && git commit` |

---

## 🧹 Undo & Clean Up

| Action | Command |
|--------|----------|
| Undo last commit (keep changes) | `git reset --soft HEAD~1` |
| Undo last commit (discard changes) | `git reset --hard HEAD~1` |
| Revert a specific commit | `git revert <commit_hash>` |
| Discard local changes to a file | `git checkout -- <file>` |
| Show changes between commits or branches | `git diff <commit1> <commit2>` |

---

## 💡 Useful Tips

| Tip | Command |
|-----|----------|
| Create a `.gitignore` file | `touch .gitignore` |
| Stash current changes temporarily | `git stash` |
| Apply stashed changes | `git stash apply` |
| Remove all stashes | `git stash clear` |
| View remote branches | `git branch -r` |
| Delete remote branch | `git push origin --delete <branch>` |

---

**Author:** Kaio Garcia  
**Last updated:** October 2025  
