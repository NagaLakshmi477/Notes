# What is Git?

- It is a **Distributed Version Control System (VCS)** used to track changes in files, especially source code.
- It allows multiple developers to work on the same project, view previous versions, and restore changes when needed.

---

# `git init`

- Initializes the current folder as a Git repository.
- It creates a hidden `.git` folder.

---

# `.git`

- The `.git` folder is the heart of a Git repository.
- If your folder contains a `.git` folder, it is called a **Git Repository (Repo)**.

---

# `git branch -M main`

- Renames the current branch to `main`.
- The `-M` option forces the rename, even if a branch named `main` already exists.

---

# `git remote add origin <remote-url>`

- Connects your local Git repository to a remote repository (e.g., GitHub).
- `origin` is the default name given to the remote repository.

---

# Protect Main Branch

```
Settings
    ↓
Rules
    ↓
Rulesets
    ↓
Create New Branch Ruleset
    ↓
Select main branch
```

- Used to restrict direct code changes to the `main` branch.
- Developers must create a separate branch and raise a Pull Request (PR) to merge changes.

---

# Create a New Branch

```bash
git checkout -b <new-branch-name>
```

- Creates a new branch.
- Switches to the newly created branch.

---

# Add, Commit and Push

```bash
git add .
git commit -m "light oil added"
git push origin <new-branch-name>
```

---

# View Commit History

```bash
git log --oneline
```

- Displays the commit history in a single-line format.

---

# Pull Request (PR)

- If you want to move the code to the `main` branch, you need to raise a **Pull Request (PR)**.
- After the PR is reviewed and approved, it can be merged into the `main` branch.

---

# `git cat-file <commit-id>`

```bash
git cat-file <commit-id>
```

- Used to inspect Git objects such as commits, trees, blobs, and tags.


What is a Feature Branch?Why is it used?

- A feature branch is a separate branch in Git created to work on a new feature
- It is created from the main branch and used to make changes independently.
- Keeps the main branch stable
- Allows safe development and testing of new features.
- Enables multiple developers to work in parallel.
- Makes code review easier before merging changes.
- Reduces the risk of breaking the main codebase.
What is a Release Branch?

- A release branch is a separate branch created to prepare a new version of the application for production.
- It is usually created from the main or develop branch when the features for a release are complete.
What is Merge in Git?

- Merge is the process of combining changes from one branch into another branch.
- It is commonly used to bring feature branch changes into the main branch.
What is a Hotfix Branch?

- A hotfix branch is a separate branch created to quickly fix critical bugs in the production code.
- It is usually created from the main (production) branch.
- After fixing, it is merged back into the main branch and also into develop to keep everything updated.
- To fix urgent issues without waiting for the next release cycle.