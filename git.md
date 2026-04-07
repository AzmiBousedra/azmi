# Git Command Cheat Sheet: Developer Edition
**Author:** Azmi-Salah Bousedra

This cheat sheet is organized by workflow stages, from initial setup to emergency rollbacks. The goal is to keep your repository clean, collaborate safely, and ensure you never lose or overwrite critical assignment code.

---

## 1. Setup & Initialization
*Commands to start a new project or configure your environment.*

| Command | Description |
| :--- | :--- |
| `git config --global user.name "Name"` | Set the name attached to your commits. |
| `git config --global user.email "email"` | Set the email attached to your commits. |
| `git init` | Initialize a local Git repository in the current directory. |
| `git clone <url>` | Clone an existing remote repository to your local machine. |

---

## 2. The Daily Bread & Butter
*The standard loop for saving and tracking your work.*

| Command | Description |
| :--- | :--- |
| `git status` | Show modified files, staged files, and untracked files. **(Run this constantly)** |
| `git add <file>` | Stage a specific file for the next commit. |
| `git add .` | Stage all modified and new files in the current directory. |
| `git commit -m "Message"` | Commit your staged changes with a descriptive message. |
| `git commit --amend -m "Msg"` | Replace the last commit with a new one (fixes a bad commit message or forgotten files). |

---

## 3. Branching & Context Switching
*Never work directly on `main`. Always branch out for features or assignments to avoid breaking a working state.*

| Command | Description |
| :--- | :--- |
| `git branch` | List all local branches. The active branch has a `*`. |
| `git branch <branch-name>` | Create a new branch. |
| `git switch <branch-name>` | Switch to an existing branch. (Modern alternative to `git checkout`). |
| `git switch -c <branch-name>` | Create a new branch and switch to it immediately. |
| `git branch -d <branch-name>` | Delete a local branch safely (prevents deletion if unmerged). |

---

## 4. Syncing & Team Collaboration
*Commands for pushing your work and pulling your teammates' work.*

| Command | Description |
| :--- | :--- |
| `git fetch` | Download history and changes from the remote repo, but **do not** merge them yet. |
| `git pull` | Fetch changes from the remote and instantly merge them into your active branch. |
| `git push origin <branch>` | Push your local branch commits to the remote repository. |
| `git push -u origin <branch>` | Push a new branch and set the remote tracking link for future `git pull`/`push` commands. |

---

## 5. Merging & Integration
*Combining work. This is where merge conflicts happen, so proceed with caution.*

| Command | Description |
| :--- | :--- |
| `git merge <branch-name>` | Merge the specified branch into your **currently active** branch. |
| `git rebase <base-branch>` | Reapply your current branch's commits on top of another branch (keeps a linear history). |
| `git merge --abort` | **Emergency Button:** If you get overwhelmed by merge conflicts, abort the merge and return to the pre-merge state. |

---

## 6. Stashing (Quick Saves)
*Use these when you need to switch branches but aren't ready to commit your half-finished work.*

| Command | Description |
| :--- | :--- |
| `git stash` | Temporarily shelve (stash) all modified tracked files. |
| `git stash pop` | Restore the most recently stashed files and remove them from the stash list. |
| `git stash list` | View all stashed changes. |
| `git stash drop` | Discard the most recent stash permanently. |

---

## 7. History & Inspection
*Figuring out who did what, and when.*

| Command | Description |
| :--- | :--- |
| `git log` | Show the commit history for the active branch. |
| `git log --oneline --graph` | Show a condensed, visual graph of the commit history and branches. |
| `git diff` | Show the exact line-by-line code changes in unstaged files. |
| `git diff --staged` | Show the code changes in files you have already `git add`ed. |

---

## 8. Undoing Mistakes (Saving the Assignment)
*How to fix things when you've messed up your code or your repository state.*

| Command | Description |
| :--- | :--- |
| `git restore <file>` | Discard uncommitted local changes to a file, returning it to the last committed state. |
| `git restore --staged <file>`| Unstage a file (undo a `git add`), but keep your code modifications. |
| `git revert <commit-hash>` | Create a *new* commit that undoes the changes of a specific past commit (safest way to undo pushed history). |
| `git reset --soft HEAD~1` | Undo the last commit, but keep all your code changes staged and ready. |
| `git reset --hard HEAD~1` | **Warning:** Undo the last commit AND delete all code changes you made in it. Use with extreme caution. |