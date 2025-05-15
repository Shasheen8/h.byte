---
title: Basics of working with Git
date: Wed, 05 Jan 2022 16:31:00 +0000
---

**Git** is an *open-source version control system* that efficiently manages projects by tracking changes over time, maintaining a complete *history* similar to a file manager. It enables *developers* to collaborate seamlessly on the same project. **GitHub**, a platform that hosts *Git repositories*, enhances this collaboration.

## What is Version Control?

Version control:

- Tracks *project changes* over time.
- Stores a *complete history* of modifications.
- Facilitates *collaboration* among developers working on the same codebase.

> **Key Insight**: Git empowers teams to work concurrently while preserving the integrity of project files.

## GitHub Terminologies

GitHub introduces key concepts for managing repositories:

- **Fork**: A replication of another user’s *repository* that resides on your personal *GitHub account*.
- **Main**: The default *development branch* created when a new repository is initialized.
- **Readme**: A *plain text file* containing *documentation* about the repository’s files.
- **Repository**: A storage space (or *directory*) where project work is stored, often shortened to *repo*.
- **License**: Makes a repository *open-source*, allowing others to *use*, *modify*, and *distribute* it.
- **Pull Request**: Announces *changes* made in a branch, enabling team review and integration of completed features.

### Summary of GitHub Terminologies

| Term | Description | Purpose |
|------|-------------|---------|
| Fork | Copy of another user’s repo | Personal experimentation |
| Main | Default branch | Primary development line |
| Readme | Documentation file | Guides users on repo contents |
| Repository | Storage for project files | Centralizes project data |
| License | Open-source permissions | Enables sharing and modification |
| Pull Request | Proposed branch changes | Facilitates team review |

## Git Commands

Git provides a set of commands to manage repositories effectively:

- **`git init`**: Initializes a new *Git repository*, creating a `.git` subdirectory with all metadata.
- **`git clone`**: Creates a *copy* of a specific repository or branch.
- **`git branch <branch-name>`**: Creates a new *branch* for a repository.
- **`git checkout <branch-name>`**: Navigates between *branches* created by `git branch`.
- **`git add`**: Saves a *snapshot* of the current project state to the *commit history*, tracking files and changes.
- **`git commit`**: Captures a *snapshot* of the project’s current state.
- **`git push`**: Uploads *Git commits* to a remote repository, such as *GitHub*.

### Summary of Git Commands

| Command | Function | Example Use Case |
|---------|----------|------------------|
| `git init` | Initializes a new repository | Start a new project |
| `git clone` | Copies a repository | Download a project to work on |
| `git branch` | Creates a branch | Develop a new feature |
| `git checkout` | Switches branches | Work on a specific feature |
| `git add` | Stages changes | Prepare files for commit |
| `git commit` | Saves changes | Record a project snapshot |
| `git push` | Uploads changes | Share updates with the team |

## Git States

Git operates in three primary states:

- **Modified**: A file in the repository has been *changed*.
- **Staged**: Modifications are *prepared* for committing using `git add`.
- **Committed**: Staged files are *finalized* and saved to the repository’s history using `git commit`.

> **Pro Tip**: Understanding Git’s states helps manage the lifecycle of project changes effectively.

## Basic Git Setup

Follow these steps to set up a Git repository and push it to GitHub:

1. **Create a new folder**:
   ```
   mkdir testing
   ```
2. **Navigate to the folder**:
   ```
   cd testing
   ```
3. **Create a new file**:
   ```
   touch test.py
   ```
4. **Check untracked changes**:
   ```
   git status
   ```
5. **Add the file**:
   ```
   git add test.py
   ```
6. **Commit changes**:
   ```
   git commit -m "<add a comment for your commit >"
   ```
7. **Add a remote origin**:
   ```
   git remote add origin main https://github.com/shasheen/<directory>
   ```
8. **Push to GitHub**:
   ```
   git push -u origin
   ```

> **Key Consideration**: Replace `<directory>` with your actual GitHub repository path and ensure you’ve created or linked a repo on GitHub.

## Why Use Git?

Git is a cornerstone of modern development due to its ability to:

- Prevent *overwriting* of content in files.
- Store *snapshots* of project changes.
- Maintain *data integrity*.
- Support *collaboration* in the *development lifecycle*.

> **Pro Tip**: Experiment with Git to master version control and streamline team workflows.

## Conclusion

**Git** and **GitHub** are essential tools for managing *projects* and enabling *collaboration*. By leveraging *version control*, developers can track changes, avoid conflicts, and maintain a robust project history. Commands like `git init`, `git commit`, and `git push`, combined with GitHub features like *pull requests* and *forks*, make Git a critical part of the *development lifecycle*. Start exploring Git to enhance your project management and teamwork capabilities.