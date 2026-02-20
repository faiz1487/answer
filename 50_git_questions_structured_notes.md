# 📚 50 Git Questions – Structured Answers (Interview + DevOps Ready)

---

## 1. What is Git and why is it used?
Git is a distributed version control system used to track code changes, manage versions, and enable collaboration among developers without overwriting each other’s work.

---

## 2. Explain the difference between Git and GitHub.
- Git: A distributed version control tool (local + CLI based)
- GitHub: A cloud platform that hosts Git repositories and provides collaboration features like pull requests and CI/CD integrations.

---

## 3. How do you install Git on your machine?
Linux:
```
sudo apt update
sudo apt install git
```
Windows/Mac: Download and install from https://git-scm.com

---

## 4. How do you configure your username and email in Git?
```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

---

## 5. What is a repository in Git?
A repository (repo) is a project directory that Git tracks, containing source code, commit history, branches, and configuration.

---

## 6. How do you create a new Git repository?
```
git init
```

---

## 7. How do you clone a repository from GitHub?
```
git clone https://github.com/username/repo.git
```

---

## 8. What is the purpose of the .gitignore file?
The .gitignore file tells Git which files and folders (like logs, secrets, node_modules) should not be tracked or committed.

---

## 9. How do you check the status of your working directory in Git?
```
git status
```

---

## 10. How do you add files to the staging area in Git?
```
git add file.txt
git add .
```

---

## 11. Explain the concept of commits in Git.
A commit is a snapshot of staged changes saved in the repository with a unique hash ID and message for version tracking.

---

## 12. How do you create a new commit in Git?
```
git commit -m "Your commit message"
```

---

## 13. What is the purpose of the git log command?
The git log command displays the complete history of commits including author, date, and messages.

---

## 14. How do you view the history of commits in a repository?
```
git log --oneline --graph --all
```

---

## 15. How do you view the changes made in a commit?
```
git show <commit_id>
```

---

## 16. What is branching in Git and why is it useful?
Branching allows parallel development so new features or fixes can be developed without affecting the main branch.

---

## 17. How do you create a new branch in Git?
```
git branch feature-branch
# or
git checkout -b feature-branch
```

---

## 18. How do you switch between branches in Git?
```
git checkout branch-name
# or
git switch branch-name
```

---

## 19. What is the difference between git merge and git rebase?
- git merge: Combines histories and creates a merge commit
- git rebase: Rewrites commit history to keep it linear and clean

---

## 20. How do you resolve merge conflicts in Git?
Edit the conflicted file, remove conflict markers, fix the code, then:
```
git add .
git commit
```

---

## 21. What is the purpose of the git stash command?
It temporarily saves uncommitted changes so you can switch branches without committing unfinished work.

---

## 22. How do you apply stashed changes in Git?
```
git stash apply
# or
git stash pop
```

---

## 23. What is the purpose of the git tag command?
Git tag is used to mark specific commits as releases or version points (e.g., v1.0, v2.0).

---

## 24. How do you create and push tags to a remote repository?
```
git tag v1.0
git push origin v1.0
```

---

## 25. Explain the concept of remote repositories in Git.
A remote repository is a version of your project hosted on a server (GitHub, GitLab, Bitbucket) used for collaboration and backup.

---

## 26. How do you add a remote repository in Git?
```
git remote add origin https://github.com/user/repo.git
```

---

## 27. How do you push changes to a remote repository?
```
git push origin main
```

---

## 28. How do you pull changes from a remote repository?
```
git pull origin main
```

---

## 29. What is the purpose of the git fetch command?
It downloads changes from the remote repository without merging them into the current branch.

---

## 30. How do you delete a branch in Git?
```
git branch -d branch-name
git push origin --delete branch-name
```

---

## 31. Create a new Git repository and configure your username and email.
```
git init
git config user.name "Your Name"
git config user.email "your@email.com"
```

---

## 32. Create a file, add some content to it, and commit the changes.
```
echo "Hello Git" > file.txt
git add file.txt
git commit -m "Added file"
```

---

## 33. Create a .gitignore file and add rules to ignore specific files and directories.
```
touch .gitignore
echo "node_modules/" >> .gitignore
echo ".env" >> .gitignore
```

---

## 34. Clone an existing repository from GitHub and make some changes.
```
git clone repo_url
cd repo
echo "New change" >> file.txt
git add .
git commit -m "Updated file"
```

---

## 35. Create a new branch, make some changes, and switch back to the main branch.
```
git checkout -b feature
# make changes
git checkout main
```

---

## 36. Merge changes from a feature branch into the main branch.
```
git checkout main
git merge feature
```

---

## 37. Resolve a merge conflict between two branches.
Open the conflicted file, resolve conflicts manually, then:
```
git add .
git commit
```

---

## 38. What is the difference between a working directory, staging area, and repository?
- Working Directory: Current files being edited
- Staging Area: Changes prepared for commit
- Repository: Permanent commit history stored in .git

---

## 39. What is the difference between tracked and untracked files?
- Tracked files: Files already added/committed and monitored by Git
- Untracked files: New files not yet added to Git tracking

---

## 40. What does git init do internally?
It creates the hidden .git directory, initializes metadata, sets up HEAD, and prepares the repo for version control.

---

## 41. What is the purpose of the .git directory?
The .git directory stores all repository data including commits, objects, branches, logs, and configuration.

---

## 42. What is the difference between git pull and git clone?
- git clone: Downloads the full repository for the first time
- git pull: Fetches and merges updates into an existing local repository

---

## 43. What is git cherry-pick and when would you use it?
Git cherry-pick applies a specific commit from one branch to another, commonly used for hotfixes or selective changes.

---

## 44. What is git revert and how is it different from git reset?
- git revert: Creates a new commit that undoes previous changes (safe for shared repos)
- git reset: Moves HEAD and can rewrite history (risky in shared environments)

---

## 45. How do you squash commits?
```
git rebase -i HEAD~3
# then mark commits as squash
```

---

## 46. How do you undo the last commit without losing changes?
```
git reset --soft HEAD~1
```

---

## 47. How can you recover a deleted branch?
```
git reflog
git checkout -b recovered-branch <commit_id>
```

---

## 48. How do you resolve conflicts during rebase?
```
git rebase main
# fix conflicts
git add .
git rebase --continue
```

---

## 49. What is git blame used for?
Git blame shows line-by-line authorship of a file to identify who made specific changes.
```
git blame file.txt
```

---

## 50. Explain different types of git reset: --soft, --mixed, --hard

### --soft
Moves HEAD to previous commit but keeps changes staged.
```
git reset --soft HEAD~1
```

### --mixed (default)
Moves HEAD and unstages changes but keeps them in the working directory.
```
git reset --mixed HEAD~1
```

### --hard
Moves HEAD and deletes commits and working directory changes permanently (use with caution).
```
git reset --hard HEAD~1
```

