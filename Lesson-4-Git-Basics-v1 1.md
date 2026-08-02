# Lesson 4 - Git Basics: Working with Changes and Commits

**Audience / Level:** Beginner developers learning the everyday Git workflow
**Duration:** 45-60 minutes
**Prerequisites:**

* Lesson 0 - Installation and Initial Setup
* Lesson 2 - Creating Your First Git Repository
* Lesson 3 - Introducing Git

---

# Learning Objectives

By the end of this lesson, students will be able to:

* Check repository status using `git status`
* Add changes to the staging area using `git add`
* Save changes using `git commit`
* View project history using `git log`
* Understand the difference between:

  * Working directory
  * Staging area
  * Repository history
* Inspect simple changes using `git diff`
* Create clear commit messages

---

# 1 - Understanding the Basic Git Workflow

Git works by moving changes through three main areas:

```text
Working Directory
        |
        | git add
        v
Staging Area
        |
        | git commit
        v
Repository History
```

Think of it like preparing a package:

### Working Directory

This is where you create and edit files.

### Staging Area

The staging area is a place where you choose which changes should be included in your next commit.

Command:

```bash
git add filename
```

Meaning:

"Git, include this change in my next saved version."

### Repository

The repository stores your committed history.

Command:

```bash
git commit
```

Meaning:

"Save these staged changes permanently in Git history."

---

# 2 - Essential Git Commands

These are the commands developers use every day.

---

# `git status`

Shows what is happening in your repository.

Example:

```bash
git status
```

It tells you:

* Which files changed
* Which files are staged
* Which files are not staged
* What Git expects you to do next

Beginners should run:

```bash
git status
```

often.

It is one of the most useful Git commands.

---

# `git add`

Moves changes into the staging area.

Example:

```bash
git add hello.txt
```

Add all changed files:

```bash
git add .
```

Important:

`git add` does not save your changes permanently.

It only prepares them for a commit.

---

# `git commit`

Creates a permanent snapshot of staged changes.

Example:

```bash
git commit -m "Add hello file"
```

A commit records:

* What changed
* Who changed it
* When it changed
* A message describing the change

---

# `git log`

Shows previous commits.

Example:

```bash
git log
```

A shorter version:

```bash
git log --oneline
```

Example output:

```text
a82f91d Add login page
b17cd22 Create project structure
91ab234 Initial commit
```

Each commit has a unique identifier called a hash.

---

# `git diff`

Shows differences between versions.

Example:

```bash
git diff
```

This helps you review changes before committing.

You will learn `git diff` in detail in Lesson 8.

---

# 3 - Practicing the Everyday Workflow

Use the repository you created in Lesson 2.

Check your current state:

```bash
git status
```

Create a new file:

```bash
echo "Version 1" > version.txt
```

Stage the file:

```bash
git add version.txt
```

Create a commit:

```bash
git commit -m "Add version file"
```

View history:

```bash
git log --oneline
```

---

# 4 - Writing Good Commit Messages

A commit message should explain what changed.

Bad examples:

```text
update
changes
fixed stuff
test
```

These messages do not tell other developers anything useful.

Good examples:

```text
Add user profile page
Fix login validation error
Update installation instructions
```

Good commit messages are:

* Short
* Clear
* Written as an action

You will learn commits in more detail in Lesson 5.

---

# 5 - Quick Diff Practice

Create a change:

```bash
echo "Version 2" >> version.txt
```

Before staging it, run:

```bash
git diff
```

Stage it:

```bash
git add version.txt
```

Now run:

```bash
git diff --staged
```

For now, focus on:

```diff
- removed lines
+ added lines
```

Detailed diff reading is covered in Lesson 8.

---

# Hands-On Exercises

# Exercise 1 - Practice Add and Commit

**Time: 15 minutes**

Goal:

Practice the basic Git workflow in an existing repository.

Steps:

1. Create two files:

```bash
echo "My project" > project.txt
echo "Version 1" > version.txt
```

2. Check status:

```bash
git status
```

3. Add one file:

```bash
git add project.txt
```

4. Commit:

```bash
git commit -m "Add project description"
```

Expected result:

Students understand that Git only commits staged changes.

---

# Exercise 2 - Practice Commit Messages

**Time: 10 minutes**

Steps:

1. Edit a file.
2. Stage the change.
3. Create a commit with a short, clear message.

Example:

```bash
git commit -m "Update README instructions"
```

View the commit:

```bash
git show HEAD
```

Expected result:

Students understand how commits describe changes.

---

# Exercise 3 - Staged vs Unstaged Changes

**Time: 10 minutes**

Steps:

1. Edit a file.

Check:

```bash
git diff
```

2. Stage the file:

```bash
git add filename
```

3. Check:

```bash
git diff --staged
```

Expected result:

Students understand the difference between:

* Current changes
* Staged changes
* Committed changes

---

# Common Beginner Mistakes

## "I committed but my changes are missing"

Cause:

The file was not staged.

Solution:

Check:

```bash
git status
```

Then:

```bash
git add filename
git commit
```

---

## "Why do I need git add?"

Explanation:

Git separates choosing changes from saving changes.

This allows developers to create clean commits.

---

## "Can I commit everything?"

Yes:

```bash
git add .
git commit -m "message"
```

But developers should review changes before committing.

---

## "Why run git status so often?"

Because it tells you exactly what Git sees.

It prevents many mistakes.

---

# Lesson Summary

Today you practiced everyday local Git commands:

* `git status`
* `git add`
* `git commit`
* `git log`
* `git diff`

In the next lesson, you will learn how to make commits more useful.

---
