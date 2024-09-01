Here are the basic Git commands along with examples to help you understand how to use them:

### 1. **Setup Commands**
   - **Set your name and email for Git:**
     ```bash
     git config --global user.name "Shyam"
     git config --global user.email "shyam@example.com"
     ```
   - **Check your configuration settings:**
     ```bash
     git config --list
     ```
     Example output:
     ```
     user.name=Shyam
     user.email=shyam@example.com
     ```

### 2. **Repository Commands**
   - **Initialize a new Git repository:**
     ```bash
     git init
     ```
     Example:
     ```bash
     Initialized empty Git repository in /path/to/repo/.git/
     ```
   - **Clone an existing repository:**
     ```bash
     git clone https://github.com/user/repo.git
     ```
     Example:
     ```bash
     Cloning into 'repo'...
     ```

### 3. **Basic Commands**
   - **Check the status of your repository:**
     ```bash
     git status
     ```
     Example:
     ```
     On branch main
     Your branch is up to date with 'origin/main'.
     nothing to commit, working tree clean
     ```
   - **Stage a specific file for commit:**
     ```bash
     git add file.txt
     ```
   - **Stage all changes for commit:**
     ```bash
     git add .
     ```
   - **Commit staged changes with a message:**
     ```bash
     git commit -m "Added new features"
     ```
   - **Commit all tracked changes (skipping the `git add` step):**
     ```bash
     git commit -a -m "Fixed bugs"
     ```
   - **View commit history:**
     ```bash
     git log
     ```
     Example:
     ```
     commit abc1234
     Author: Shyam <shyam@example.com>
     Date:   Fri Sep 1 2024

         Initial commit
     ```

### 4. **Branching Commands**
   - **List all branches in your repository:**
     ```bash
     git branch
     ```
     Example:
     ```
     * main
       feature-branch
     ```
   - **Create a new branch:**
     ```bash
     git branch feature-branch
     ```
   - **Switch to a different branch:**
     ```bash
     git checkout feature-branch
     ```
   - **Create and switch to a new branch:**
     ```bash
     git checkout -b new-feature
     ```
   - **Merge a branch into the current branch:**
     ```bash
     git merge feature-branch
     ```
   - **Delete a branch locally:**
     ```bash
     git branch -d feature-branch
     ```

### 5. **Remote Commands**
   - **Add a remote repository:**
     ```bash
     git remote add origin https://github.com/user/repo.git
     ```
   - **Fetch updates from the remote repository:**
     ```bash
     git fetch
     ```
   - **Pull updates from the remote repository and merge with your local branch:**
     ```bash
     git pull origin main
     ```
   - **Push your commits to the remote repository:**
     ```bash
     git push origin main
     ```
   - **Push a specific branch to the remote repository:**
     ```bash
     git push origin feature-branch
     ```

### 6. **Stashing Changes**
   - **Save your changes temporarily without committing:**
     ```bash
     git stash
     ```
   - **Reapply stashed changes:**
     ```bash
     git stash apply
     ```
   - **Apply and remove the latest stash:**
     ```bash
     git stash pop
     ```

### 7. **Undo Changes**
   - **Discard changes in a file:**
     ```bash
     git checkout -- file.txt
     ```
   - **Unstage a file:**
     ```bash
     git reset file.txt
     ```
   - **Reset the working directory to the last commit, discarding all changes:**
     ```bash
     git reset --hard
     ```
   - **Revert a specific commit by creating a new commit that undoes the changes:**
     ```bash
     git revert abc1234
     ```

### 8. **Tagging**
   - **Create a tag at the current commit:**
     ```bash
     git tag v1.0
     ```
   - **Create an annotated tag:**
     ```bash
     git tag -a v1.0 -m "Version 1.0 release"
     ```
   - **Push a tag to the remote repository:**
     ```bash
     git push origin v1.0
     ```

### 9. **Viewing Changes**
   - **Show changes between the working directory and staging area:**
     ```bash
     git diff
     ```
   - **Show changes between the staging area and the last commit:**
     ```bash
     git diff --staged
     ```
   - **Show details about a specific commit:**
     ```bash
     git show abc1234
     ```

### 10. **Collaboration Commands**
   - **Fork a repository (done via platforms like GitHub, not directly in Git):**
     - Visit the repository on GitHub and click the "Fork" button.
   - **Create a pull request (usually done through GitHub or similar platforms):**
     - After pushing your branch, go to the repository on GitHub and click "New pull request".

These examples should help you practice Git commands effectively.
