# Git Commands Reference

| Category | Command | Explanation | Example Usage |
| :--- | :--- | :--- | :--- |
| **🚀 Setup & Config** | `git init` | Initializes a new Git repository. Creates a .git/ folder. | `git init` |
| | `git config` | Sets Git configuration (user name, email, settings). | `git config --global user.name "Your Name"` |
| | `git help` | Shows help documentation. | `git help commit` |
| **📝 Core Snapshotting** | `git status` | Shows the state of the working directory (modified, staged files). | `git status` |
| | `git add` | Stages files for the next commit. | `git add main.py` <br> `git add .` |
| | `git commit` | Records staged changes into the repository history. | `git commit -m "Message"` |
| | `git rm` | Removes a file from working directory and staging area. | `git rm old_file.py` |
| | `git mv` | Moves or renames a file while tracking the change. | `git mv old.py new.py` |
| **🌿 Branching** | `git branch` | Lists, creates, or deletes branches. | `git branch` <br> `git branch feature/login` |
| | `git branch -m` | Renames a branch. | `git branch -m master main` |
| | `git branch -d` | Deletes a branch safely (checks for merge status). | `git branch -d feature/login` |
| | `git checkout` | Switches branches or restores files (classic command). | `git checkout feature/login` |
| | `git switch` | Switches branches (modern, clearer alternative to checkout). | `git switch main` |
| | `git merge` | Combines changes from one branch into another. | `git merge feature/login` |
| **⏳ History Manipulation** | `git rebase` | Reapplies commits on top of another base branch (linear history). | `git rebase main` |
| | `git cherry-pick` | Applies a specific commit from another branch to current one. | `git cherry-pick <commit_hash>` |
| | `git reset` | Moves HEAD to previous commit (can unstage/delete changes). | `git reset --soft HEAD~1` |
| | `git revert` | Safely undoes a commit by creating a new "reverse" commit. | `git revert <commit_hash>` |
| **↩️ Undoing Changes** | `git restore` | Restores a file to its last committed state (discards local changes). | `git restore main.py` |
| | `git restore --staged` | Unstages a file (keeps changes in working directory). | `git restore --staged main.py` |
| | `git clean` | Removes untracked files from the working directory. | `git clean -fd` |
| **🌍 Remote Sync** | `git remote -v` | Lists remote repositories and URLs. | `git remote -v` |
| | `git remote add` | Adds a remote repository connection. | `git remote add origin <url>` |
| | `git remote remove` | Removes a remote connection. | `git remote remove origin` |
| | `git fetch` | Downloads changes from remote without merging. | `git fetch origin` |
| | `git fetch --all` | Fetches updates from all registered remotes. | `git fetch --all` |
| | `git pull` | Fetches and merges changes from a remote repository. | `git pull` |
| | `git push` | Uploads local commits to a remote repository. | `git push -u origin main` |
| | `git push --force` | Forces remote branch to match local (overwrites history). | `git push -u origin main --force` |
| | `git push origin --delete` | Deletes a branch from the remote repository. | `git push origin --delete feature/login` |
| | `git push --tags` | Pushes all local tags to the remote. | `git push --tags` |
| **📦 Stashing** | `git stash` | Temporarily saves uncommitted changes. | `git stash` |
| | `git stash pop` | Restores the last stashed changes and removes them from stash list. | `git stash pop` |
| | `git stash list` | Shows all currently saved stashes. | `git stash list` |
| | `git stash apply` | Applies a stash without deleting it from the list. | `git stash apply` |
| **🔍 Inspecting & Debugging** | `git log` | Displays commit history. | `git log --oneline` |
| | `git diff` | Shows differences between working directory and staged/committed files. | `git diff` |
| | `git show` | Shows details of a specific commit or tag. | `git show HEAD` |
| | `git blame` | Shows who modified each line of a file. | `git blame main.py` |
| | `git reflog` | Shows history of HEAD movements (useful for recovering lost commits). | `git reflog` |
| | `git shortlog` | Grouped summary of commits by author. | `git shortlog -sn` |
| **🏷 Releases & Tags** | `git tag` | Creates a lightweight tag. | `git tag v1.0` |
| | `git tag -a` | Creates an annotated tag (recommended for releases). | `git tag -a v1.0 -m "Release"` |
| | `git describe` | Finds the most recent tag reachable from a commit. | `git describe --tags` |
| **🔧 Advanced / Maintenance** | `git submodule add` | Adds an external repository inside the project. | `git submodule add <url>` |
| | `git submodule update` | Updates submodules. | `git submodule update --init` |
| | `git worktree` | Manages multiple working directories from one repo. | `git worktree add ../new-branch` |
| | `git gc` | Runs garbage collection to optimize the repository. | `git gc` |
| | `git fsck` | Checks repository integrity. | `git fsck` |
