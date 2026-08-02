# Lesson 1 - Course Orientation: Getting Started with Git & GitHub

**Audience:** Complete Beginners (No Git or GitHub Experience Required)

**Duration:** 30-45 Minutes

**Prerequisites:** Lesson 0 - Installation and Initial Setup

---

# Learning Objectives

By the end of this lesson, you will be able to:

* Explain why developers use version control.
* Describe what Git is and why it is useful.
* Explain the difference between Git and GitHub.
* Understand the basic Git workflow.
* Recognize important Git vocabulary used throughout the course.

---

Intro - dedicated teams channel, daily meeeting to answer questions Ksenija and Ognjen

# Welcome

This course assumes **zero previous knowledge**.

By the end of this lesson, you'll understand **what Git does, why developers use it, and how it makes coding easier.**

---

# 1. Why Do Developers Need Git?

Before learning Git, let's look at a common problem.

Imagine you're writing a assignment or a work report.

Your folder slowly starts looking like this:

```text
Report.docx
Report_Final.docx
Report_Final_v2.docx
Report_Final_v2_FIXED.docx
Report_Final_v2_FINAL.docx
Report_Final_v2_FINAL_REAL.docx
```

Which one is actually the newest?

What if someone asks:

> "Can you restore yesterday's version?"

What if your teammate edited another copy?

What if you accidentally deleted an important section?

This happens to developers all the time.

As software grows, it becomes impossible to manage dozens-or even hundreds-of versions manually.

That's why developers use **Git**.

Git automatically keeps track of every important change you make.

Instead of creating dozens of folders and files, Git stores a complete history of your project.

Think of Git as an **unlimited Undo button** that never forgets.

---

# 2. What is Version Control?

Version control is a system that records changes made to files over time.

Instead of creating lots of different copies of your project, version control remembers every saved version for you.

Each saved version is called a **commit**.

A commit stores:

* What changed
* When it changed
* Who made the change
* Why it changed (using a message)

Imagine writing a book.

Instead of saving:

```text
Book_v1
Book_v2
Book_v3
Book_Final
Book_Final2
```

You simply keep working.

Git remembers every version automatically.

---

# Benefits of Version Control

Version control helps you:

### Keep a complete history

You can see every change ever made.

---

### Recover deleted work

Accidentally removed something?

Git can usually restore it.

---

### Work safely

Want to try a new idea?

You can experiment without breaking your main project.

---

### Collaborate with others

Multiple developers can work on the same project at the same time.

Git helps combine everyone's work.

---

### Understand changes

Every commit includes a message explaining what changed.

Months later, you'll still know why you made a change.

---

# 3. Meet Git

Git is a **Version Control System**.

It is software installed on your computer.

Git watches your project and remembers important changes.

Git works **locally**, meaning you don't need an internet connection to use it.

You can:

* Create projects
* Save versions
* Restore previous versions
* Organize your work
* Experiment safely

All without being connected to the internet.

---

# 4. Important Git Vocabulary

Don't worry about memorizing everything today.

You'll use these words throughout the course.

| Word              | Simple Meaning                          |
| ----------------- | --------------------------------------- |
| Git               | Software that tracks changes            |
| Repository (Repo) | A project managed by Git                |
| Commit            | A saved checkpoint                      |
| Branch            | A safe place to work on new ideas       |
| Merge             | Combine work together                   |
| Remote            | A copy of your repository stored online |
| GitHub            | A website that stores Git repositories  |

---

# 5. What is a Repository?

A **repository**, often called a **repo**, is simply a project folder that Git manages.

For example:

```text
MyWebsite/

    index.html

    styles.css

    script.js
```

Normally, this is just a folder.

After running:

```bash
git init
```

Git begins tracking changes inside that folder.

It has now become a **Git repository**.

---

# 6. What is a Commit?

A **commit** is a saved version of your project.

Think about playing a video game.

When you reach a checkpoint, your progress is saved.

If something goes wrong later, you can return to that checkpoint.

Git commits work the same way.

Every commit is a checkpoint you can return to.

Example:

```text
Commit 1
Created project

|

Commit 2
Added homepage

|

Commit 3
Fixed navigation

|

Commit 4
Updated colors
```

At any time, Git can return to one of these saved versions.

---

# 7. Understanding the Git Workflow

Every Git project follows the same basic workflow.

```text
Edit Files

      |

Working Folder

      |
git add

Staging Area

      |
git commit

Git History
```

Let's look at each step.

---

## Step 1 - Edit Your Files

You create or modify files in your project.

Example:

```text
README.md
```

---

## Step 2 - Stage Your Changes

When you're happy with your changes, you tell Git what should be saved.

You do this using:

```bash
git add README.md
```

Think of the staging area as a **"Ready to Save" box**.

You choose exactly what goes into the next save.

---

## Step 3 - Commit Your Changes

Now you permanently save those staged changes.

```bash
git commit -m "Created README"
```

This creates a checkpoint in your project's history.

---

## Step 4 - Repeat

Continue editing, staging, and committing as your project grows.

Over time your project history looks like this:

```text
Initial Project

|

Added Login

|

Fixed Bug

|

Updated Design

|

Released Version 1.0
```

---

# 8. Git vs GitHub

This is one of the biggest sources of confusion.

They are **not** the same thing.

## Git

Git is software installed on your computer.

It tracks changes in your project.

It works even without the internet.

---

## GitHub

GitHub is a website.

It stores Git repositories online.

GitHub allows you to:

* Share projects
* Collaborate with others
* Review code
* Backup repositories
* Contribute to open-source projects

---

Think of it like this:

| Git                   | GitHub              |
| --------------------- | ------------------- |
| Software              | Website             |
| Runs on your computer | Runs online         |
| Tracks changes        | Stores repositories |
| Works offline         | Requires internet   |

A simple analogy:

**Git is like Microsoft Word.**

**GitHub is like OneDrive.**

You use Word to create documents.

You use OneDrive to share and store them online.

---

# 9. A Typical Git Workflow

A developer's day usually looks like this:

```text
Create Project

|

Edit Files

|

Stage Changes

|

Commit Changes

|

Repeat

|

Push to GitHub

|

Collaborate with Others
```

You'll learn each of these steps throughout this course.

---

# Hands-On Exercise

## Why Git?

Create a folder called:

```text
MyProject
```

Inside it create several files:

```text
notes.txt

notes_v2.txt

notes_final.txt

notes_final_REAL.txt

notes_final_REAL2.txt
```

Now ask yourself:

* Which file is newest?
* Which one should someone else open?
* How would another developer know?

This is exactly the problem Git solves.

---

# Common Beginner Questions

## Do I need internet to use Git?

No.

Git works completely offline.

---

## Is Git the same as GitHub?

No.

Git is software.

GitHub is a website that works with Git.

---

## Can Git recover deleted work?

Usually yes-if the work was committed.

---

## Can I break Git?

Not easily.

Git was designed to help developers recover from mistakes.

---

## Why do developers love Git?

Because it makes experimenting safe.

If something goes wrong, you can usually return to an earlier version.

---

# Lesson Summary

Today you learned:

* Why developers use version control
* What Git is
* What GitHub is
* The difference between Git and GitHub
* What a repository is
* What a commit is
* The basic Git workflow

In the next lesson, you'll create your first Git repository.

---
