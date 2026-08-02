# Lesson 3 - Introducing Git: Understanding How Git Works

**Audience / Level:** Beginner developers learning Git fundamentals and what happens behind the scenes
**Duration:** 45-60 minutes
**Prerequisites:**

* Lesson 1 - Course Orientation
* Lesson 2 - Creating Your First Git Repository

---

# Learning Objectives

By the end of this lesson, students will be able to:

* Explain why Git was created and what problems it solves
* Describe why Git is called a distributed version control system
* Understand the three main areas of a Git repository:

  * Working directory
  * Staging area
  * `.git` directory
* Explain the basic building blocks Git uses to store information:

  * Blob
  * Tree
  * Commit
  * Tag
* Use simple Git commands to look inside a repository and understand what Git stores

---

# 1 - The Story Behind Git

Before Git existed, developers needed tools to track changes in large software projects.

One of the biggest software projects in the world is the Linux kernel. In 2005, the Linux development team needed a version control system that could handle:

* Thousands of developers
* Millions of lines of code
* Fast development and frequent changes
* Reliable collaboration across the world

Linus Torvalds, the creator of Linux, designed Git to solve these problems.

Git was built with four important goals:

### 1. Speed

Developers should be able to create commits, view history, and compare changes quickly.

### 2. Simple Design

Git should have a small number of simple concepts that work together.

### 3. Strong Branching and Merging

Developers should be able to create branches easily and combine work safely.

### 4. Distributed Collaboration

Every developer should have their own complete copy of the project.

---

# 2 - Why Git History Matters

Understanding why Git was created helps explain why Git works differently from older tools.

Many Git features exist because of its original goals:

* Branches are lightweight because Git needed fast experimentation.
* Most operations happen locally because developers needed speed.
* Git stores snapshots because it needed reliable history tracking.

Most Git operations happen on your own computer.

Examples:

```bash
git status
git log
git commit
```

These commands do not need the internet.

This makes Git fast.

---

# 3 - Understanding Distributed Version Control

Git is called a **distributed version control system**.

This means every developer has their own complete repository.

Example:

```text
          Push / Pull

Developer A  <------------>  Remote Repository
(Local Git)                   (GitHub)

Developer B  <------------>
(Local Git)
```

Each copy contains:

* Project files
* Commit history
* Branch information

Although every developer has a complete copy of the repository, developers do **not automatically see each other's changes**.

To collaborate, developers use a **remote repository** such as GitHub, GitLab, or Bitbucket.

Developers make commits locally, push them to the remote repository, and teammates fetch or pull those commits.

---

# 4 - Inside a Git Repository

When you run:

```bash
git init
```

Git creates a hidden directory called:

```text
.git
```

This directory contains everything Git needs to track your project.

A Git repository has three important areas:

---

# Working Directory

The working directory is the files you see and edit.

Example:

```text
project/
  app.js
  README.md
  index.html
```

When you change a file, you are changing the working directory.

---

# Staging Area

The staging area is where you prepare changes before creating a commit.

Example:

```bash
git add app.js
```

This tells Git:

"Include this file in my next commit."

The staging area allows you to choose exactly what changes go into a commit.

---

# `.git` Directory

The `.git` directory is Git's internal database.

It stores:

* History
* Commits
* Branches
* Configuration
* File information

You normally do not edit this directory manually.

---

# 5 - Exploring a Repository

Try these commands inside the repository you created in Lesson 2:

```bash
git rev-parse --show-toplevel
```

Shows the location of the repository.

```bash
ls -la .git
```

Shows the contents of Git's internal directory.

```bash
git ls-files
```

Shows files tracked by Git.

---

# Important `.git` Files and Folders

Inside `.git` you will find:

## objects/

Stores Git's saved information.

Examples:

* Files
* Folders
* Commits

---

## HEAD

Tells Git which branch you are currently using.

Example:

```text
HEAD -> main
```

---

## index

Stores the staging area information.

---

# 6 - How Git Stores Information

Git does not simply save copies of your project folders.

Instead, Git stores information using objects.

There are four main object types:

---

# Blob

A blob stores the contents of a file.

Example:

```text
hello.txt

contains:

Hello Git!
```

Git stores the text inside the file as a blob.

---

# Tree

A tree represents a folder.

It connects:

* File names
* File permissions
* Blobs
* Other trees

Example:

```text
Project Tree

app.js    ---> Blob
style.css ---> Blob
images    ---> Tree
```

---

# Commit

A commit records a snapshot of your project.

A commit contains:

* The project tree
* Author information
* Commit message
* Parent commit

Example:

```text
Commit
 |
 +-- Tree
      |
      +-- Files
```

---

# Tag

A tag is a name attached to a specific Git object.

Developers often use tags for releases.

Example:

```text
v1.0
v2.0
v3.0
```

You will create tags later in the course.

---

# 7 - Git History as a Graph

Git history is not always a straight line.

It is a graph called a **Directed Acyclic Graph (DAG).**

Example:

```text
        C3
       /
C1 --- C2
       \
        C4
```

Each commit points to previous commits.

This allows Git to understand:

* Where changes came from
* How branches were created
* How work was combined

---

# 8 - Looking Inside Git Objects

After creating a commit, try:

## Show the current commit:

```bash
git rev-parse HEAD
```

---

## View commit details:

```bash
git cat-file -p <commit-hash>
```

You will see:

* Author
* Message
* Parent commit
* Tree reference

---

## View the files inside a commit:

```bash
git ls-tree HEAD
```

---

# 9 - Plumbing vs Porcelain Commands

Git has two types of commands.

## Porcelain Commands

These are everyday commands:

```bash
git add
git commit
git push
```

Most developers use these daily.

---

## Plumbing Commands

These are lower-level commands used to inspect Git:

```bash
git cat-file
git hash-object
```

They help us understand how Git works internally.

---

# Hands-On Exercises

# Exercise 1 - Explore the `.git` Folder

**Time: 10 minutes**

Use the repository from Lesson 2.

Run:

```bash
ls -la .git
```

Find:

* objects
* refs
* HEAD

Expected Result:

Students understand that Git stores information inside `.git`.

---

# Exercise 2 - Explore Commits

**Time: 15 minutes**

Create a second commit:

```bash
echo "second change" >> README.md
git add README.md
git commit -m "Update README"
```

View history:

```bash
git log --oneline
```

Find the latest commit:

```bash
git rev-parse HEAD
```

Inspect it:

```bash
git cat-file -p <commit-hash>
```

View files:

```bash
git ls-tree HEAD
```

Expected Result:

Students see that commits point to trees, and trees point to files.

---

# Common Beginner Confusions

## "The staging area is another folder"

Correction:

The staging area is information stored by Git that prepares the next commit.

---

## "Git needs internet"

Correction:

Most Git operations work locally.

Internet is only needed when communicating with remote repositories.

---

## "A commit stores my entire project again"

Correction:

A commit does not save your entire project again. Git saves the changes and keeps track of everything needed to rebuild your project exactly as it looked when you made the commit.

---

# Lesson Summary

Today you learned what Git stores inside a repository.

You also learned:

* Why Git was created
* Why Git is distributed
* What the working directory, staging area, and `.git` directory are
* What blobs, trees, commits, and tags are
* The difference between porcelain and plumbing commands

In the next lesson, you will practice the everyday Git commands in more detail.

---
