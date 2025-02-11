# Git Branching, Merging & Conflict Resolution – Step-by-Step Guide

Each scenario is performed in a **separate Git repository** to keep things isolated.

---

## 1. Fast-Forward Merge (No Conflict)
A **fast-forward merge** happens when there are no diverging changes between branches.

```sh
# Create a new directory for the project
mkdir fast-forward-merge

# Navigate inside the fast-forward-merge directory
cd fast-forward-merge/

# Initialize a Git repository
git init

# Create and switch to the main branch
git checkout -b main

# Create an initial file and add some content
echo "Initial content" > file.txt

# Stage the file for commit
git add file.txt

# Commit the file with a message
git commit -m "Initial commit on main branch"

# Create and switch to a new branch called feature-branch
git switch -c feature-branch

# Make changes in the feature branch (update the content of file.txt)
echo "Feature branch update" > file.txt

# Stage the file for commit
git add file.txt

# Commit the changes in the feature branch
git commit -m "Updated file.txt in feature-branch"

# Switch back to the main branch
git switch main

# View commits that are unique to either `main` or `feature-branch`, but not both
git log main...feature-branch

# Merge feature-branch (Fast-Forward)
git merge feature-branch --ff-only

# Verify the merge
git log
```

---

## 2. Three-Way Merge (No Conflict)
A **three-way merge** occurs when both branches have new commits that need merging.

```sh
# Create a new directory and initialize a Git repository
mkdir three-way-merge
cd three-way-merge
git init

# Create an initial file and commit
echo "Initial content" > file.txt
git add file.txt
git commit -m "Initial commit on main"

# Create a new feature branch
git switch -c new-feature

# Modify file.txt in new-feature branch
echo "New feature branch changes" >> file.txt
git add file.txt
git commit -m "Updated file.txt in new-feature branch"

# Switch back to the main branch and make different changes
git switch main
echo "Main branch additional content" >> file.txt
git add file.txt
git commit -m "Updated file.txt in main branch"

# View commits that are unique to either `main` or `feature-branch`, but not both
git log main...feature-branch

# Merge new-feature branch (Three-Way Merge)
git merge new-feature

# Verify the merge
git log
```

---

## 3. Merge Conflict Scenario
A **merge conflict** happens when two branches change the same part of a file differently.  

```sh
# Create a new directory and initialize a Git repository
mkdir merge-conflict
cd merge-conflict
git init

# Create an initial file and commit
echo "Initial content" > file.txt
git add file.txt
git commit -m "Initial commit on main"

# Create a conflicting branch
git switch -c conflict-branch

# Modify file.txt in conflict-branch
echo "Conflict branch changes" > file.txt
git add file.txt
git commit -m "Updated file.txt in conflict-branch"

# Switch back to main and make conflicting changes
git switch main
echo "Main branch conflicting changes" > file.txt
git add file.txt
git commit -m "Updated file.txt in main branch with conflicting changes"

# View commits that are unique to either `main` or `feature-branch`, but not both
git log main...feature-branch

# Merge conflict-branch (This will cause a merge conflict)
git merge conflict-branch

# Verify the merge
git log
```

---

## 4. Resolving Merge Conflicts
Manually resolve conflicts by editing the file.

### Steps:
1. Open `file.txt` in a text editor.  
2. Decide which version to keep or manually merge both.  
3. Remove conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).  
4. Save the file.  
5. Stage and commit the resolved file:
   ```sh
   git add file.txt
   git commit -m "Resolved merge conflict"
   git log
   ```

---

## 5. Deleting Branches
After merging, you can delete the feature branches.

```sh
# Create a new directory and initialize a Git repository
mkdir delete-branch
cd delete-branch
git init

# Create an initial file and commit
echo "Initial content" > file.txt
git add file.txt
git commit -m "Initial commit on main"

# Create a feature branch and make changes
git switch -c feature-branch
echo "Feature branch changes" >> file.txt
git add file.txt
git commit -m "Updated file.txt in feature-branch"

# Switch back to main and merge
git switch main
git merge feature-branch

# Delete a merged branch
git branch -d feature-branch

# Create a new branch and delete it forcefully before merging
git switch -c unmerged-branch
echo "Unmerged branch changes" >> file.txt
git add file.txt
git commit -m "Updated file.txt in unmerged-branch"

# Force delete an unmerged branch
git branch -D unmerged-branch
```

---

## 6. Checking History & Logs
Use these commands to visualize Git history.

```sh
# Show branch history
git log --oneline --graph --all
```

---

## Summary of Scenarios Covered

| Scenario | Command Summary |
|----------|----------------|
| **Fast-Forward Merge** (No conflict) | `git merge feature-branch --ff-only` |
| **Three-Way Merge** (No conflict) | `git merge new-feature` |
| **Merge Conflict** | `git merge conflict-branch` → Resolve manually |
| **Delete Branch** | `git branch -d feature-branch` |

---

Now you’re ready to manage branches, merge code, and resolve conflicts in Git!
