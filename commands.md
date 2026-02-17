| Command | Explanation (What it does) | Example Usage |
| :--- | :--- | :--- |
| **git init** | Initializes a new Git repository in the current directory. Creates a .git/ folder to start version control. | `git init` |
| **git status** | Shows the current state of the working directory (modified, staged, untracked files). | `git status` |
| **git add** | Stages files for the next commit (moves them to the staging area). | `git add main.py` <br> `git add .` |
| **git commit** | Records staged changes into the repository history. | `git commit -m "Initial project structure"` |
| **git log** | Displays commit history. | `git log --oneline` |
| **git diff** | Shows differences between working directory and staged/committed files. | `git diff` |
| **git restore** | Restores a file to its last committed state (discard changes). | `git restore main.py` |
| **git branch** | Lists, creates, or deletes branches. | `git branch` <br> `git branch feature/explainability-risk` |
| **git branch -m** | Renames a branch. | `git branch -m master main` |
| **git checkout** | Switches between branches or restores working tree files. | `git checkout feature/explainability-risk` |
| **git remote add** | Adds a remote repository connection. | `git remote add origin https://github.com/user/repo.git` |
| **git remote** | Manages remote repository connections. | `git remote -v` |
| **git push** | Uploads local commits to a remote repository. | `git push -u origin main` |
| **git push --force** | Forces remote branch to match local branch (overwrites remote history). | `git push -u origin main --force` |
| **git pull** | Fetches and merges changes from a remote repository. | `git pull` |
| **git fetch** | Downloads changes from remote without merging. | `git fetch origin` |
| **git stash** | Temporarily saves uncommitted changes without committing them. Useful when switching branches. | `git stash` <br> `git stash pop` |
| **git merge** | Combines changes from one branch into another. | `git merge feature/explainability-risk` |
| **git rebase** | Reapplies commits on top of another base branch (cleaner history than merge). | `git rebase main` |
| **git reset** | Moves HEAD to a previous commit. Can unstage or delete commits depending on mode. | `git reset --soft HEAD~1` |
| **git revert** | Creates a new commit that undoes a previous commit (safe undo). | `git revert <commit_hash>` |
| **git tag** | Marks a specific commit (often for version releases). | `git tag v1.0` |
| **git cherry-pick** | Applies a specific commit from one branch to another. | `git cherry-pick <commit_hash>` |
| **git config** | Sets Git configuration (user name, email, settings). | `git config --global user.name "Your Name"` |
| **git clean** | Removes untracked files from working directory. | `git clean -fd` |
| **git show** | Displays detailed information about a commit. | `git show <commit_hash>` |
| **git blame** | Shows who last modified each line of a file. | `git blame main.py` |
| **git rm** | Removes a file from working directory and staging area. | `git rm old_file.py` |
| **git mv** | Moves or renames a file while tracking the change. | `git mv old.py new.py` |
| **git branch -d** | Deletes a branch safely. | `git branch -d feature/explainability-risk` |
| **git push origin --delete** | Deletes a branch from remote repository. | `git push origin --delete master` |
