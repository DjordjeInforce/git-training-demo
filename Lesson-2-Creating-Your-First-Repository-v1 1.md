# Lesson 2 - Creating Your First Git Repository

**Audience / Level:** Beginner developers creating their first local Git project
**Duration:** 30-45 minutes
**Prerequisites:**

* Lesson 0 - Installation and Initial Setup
* Lesson 1 - Course Orientation

---

# Learning Objectives

By the end of this lesson, students will be able to:

* Create a project folder
* Initialize a Git repository
* Create a file
* Check the repository status
* Add a file to the staging area
* Create a first commit
* View basic commit history

---

# 1 - Before You Start

Make sure Lesson 0 is complete.

Check that Git works:

```bash
git --version
```

Check your identity:

```bash
git config --global user.name
git config --global user.email
```

If Git does not show your name and email, return to Lesson 0 before continuing.

---

# 2 - Create a Project Folder

Open your terminal.

Create a folder:

```bash
mkdir git-demo
cd git-demo
```

This folder is currently just a normal folder.

Git is not tracking it yet.

---

# 3 - Initialize Git

Run:

```bash
git init
```

Git creates a hidden folder:

```text
.git
```

This folder stores repository information.

Your project is now a Git repository.

---

# 4 - Create a File

Create a README file:

```bash
echo "# Git Demo" > README.md
```

A README usually explains what a project is.

For now, it gives us a simple file to track.

---

# 5 - Check Git Status

Run:

```bash
git status
```

Git should show:

```text
Untracked files:
  README.md
```

This means:

"Git sees the file, but it is not tracking it yet."

---

# 6 - Add the File

Move the file into the staging area:

```bash
git add README.md
```

Check again:

```bash
git status
```

Git should show:

```text
Changes to be committed:
  new file: README.md
```

This means the file is ready to be saved in the next commit.

---

# 7 - Create Your First Commit

Run:

```bash
git commit -m "Initial commit"
```

Your first snapshot is now saved locally.

---

# 8 - View Your Project History

Run:

```bash
git log --oneline
```

Example:

```text
d91ab22 Initial commit
```

Each commit has:

* A short identifier
* A commit message

---

# 9 - Rename the Main Branch

Modern Git projects commonly use:

```text
main
```

Set the branch name:

```bash
git branch -M main
```

You will learn more about branches in Lesson 6.

---

# Hands-On Exercises

# Exercise 1 - Create a Local Repository

**Time: 15 minutes**

Goal:

Create your first Git repository.

Steps:

1. Create a folder:

```bash
mkdir my-first-repo
cd my-first-repo
```

2. Initialize Git:

```bash
git init
```

3. Create a README:

```bash
echo "# My First Repository" > README.md
```

4. Check status:

```bash
git status
```

5. Stage the file:

```bash
git add README.md
```

6. Commit:

```bash
git commit -m "Initial commit"
```

7. View history:

```bash
git log --oneline
```

Expected result:

Students create a local Git repository and save the first commit.

---

# Exercise 2 - Practice the Same Workflow Again

**Time: 10 minutes**

Goal:

Repeat the basic Git workflow until the steps feel familiar.

Steps:

1. Create a second folder.
2. Initialize Git.
3. Create a file.
4. Check status.
5. Add the file.
6. Commit the file.
7. View the commit history.

Expected result:

Students understand the sequence:

```text
Create file
git status
git add
git commit
git log
```

---

# Common Beginner Problems

## "Git says this is not a repository"

Cause:

You are probably outside the folder where you ran:

```bash
git init
```

Solution:

Move into the project folder:

```bash
cd folder-name
```

Then run:

```bash
git status
```

---

## "I committed but my file is missing"

Cause:

The file was not staged before committing.

Solution:

Run:

```bash
git status
git add filename
git commit -m "Add missing file"
```

---

## "I do not see the `.git` folder"

The `.git` folder is hidden.

That is normal.

You normally do not edit it directly.

---

# Lesson Summary

Today you created your first local Git repository.

You practiced:

* Creating a project folder
* Running `git init`
* Creating a file
* Checking `git status`
* Staging with `git add`
* Saving with `git commit`
* Viewing history with `git log --oneline`

In the next lesson, you'll look inside a Git repository and learn how Git tracks changes behind the scenes.

---
