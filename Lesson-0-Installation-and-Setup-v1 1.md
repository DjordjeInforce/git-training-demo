# Lesson 0 — Course Welcome, Installation, and Initial Setup

**Audience:** Complete Beginners (No Git or GitHub Experience Required)

**Duration:** 40–60 Minutes

**Prerequisites:** None

---

# Learning Objectives

By the end of this lesson, you will be able to:

- Understand how this course is organized.
- Know where to get help throughout the training.
- Identify the software needed for the rest of the course.
- Install Git on your computer.
- Verify that Git works from the terminal.
- Configure your Git name and email.
- Choose and configure a default text editor.
- Understand the difference between global and local Git settings.
- Understand the difference between HTTPS and SSH repository URLs.

---

# 1. Welcome to the Course

Welcome to the Git & GitHub training course!

Whether you're completely new to Git or have used it a little before, this course is designed to build your knowledge step by step.

Throughout the training, we'll begin with the fundamentals and gradually progress to more advanced topics, including:

- Creating and managing repositories
- Tracking changes with commits
- Branching and merging
- Working with GitHub
- Collaborating with other developers
- Pull Requests and code reviews
- Best practices used in real software development

This is a **hands-on course**.

The best way to learn Git is by using it.

Throughout every lesson, I'll demonstrate the commands directly in the terminal so you can see exactly what I'm typing, the output Git produces, and what each command does.

I encourage you to pause the video frequently and perform the same steps on your own computer before continuing.

---

# 2. Daily Support Sessions

If you have any questions during the training or need additional help, you can join the daily support sessions with **Ksenija and Ognjen**.

The support sessions are held every day at:

- **7:00 AM – 8:00 AM EST**
- **1:00 PM – 2:00 PM CET**

Feel free to join these sessions whenever you need clarification about the course material or assistance with the hands-on exercises.

---

# 3. Software You'll Need

Before beginning the course, make sure you have the following software installed.

## Git

Git is the version control system we'll use throughout this course.

It tracks changes to your files, allows you to save snapshots of your work, and makes collaboration with other developers possible.

Official website:

https://git-scm.com/

---

## GitHub Account

GitHub hosts Git repositories online.

We'll use GitHub later in the course to:

- Store repositories
- Share code
- Collaborate with other developers

Create a free account if you don't already have one.

https://github.com/

---

## Visual Studio Code (Recommended)

Visual Studio Code is a free, lightweight code editor with excellent Git integration.

We'll use VS Code throughout this course for editing files and viewing Git changes.

https://code.visualstudio.com/

---

## GitHub Desktop (Optional)

GitHub Desktop provides a graphical interface for Git.

Although this course focuses primarily on the Git command line, GitHub Desktop can be useful if you prefer working with a graphical interface.

https://desktop.github.com/

---

# 4. Installing Git

Git is available for Windows, macOS, and Linux.

For this course, we'll be using **Git for Windows**.

Download Git from:

https://git-scm.com/

---

## Installing Git on Windows

During installation:

- Keep the default installation options unless you have a specific reason to change them.
- If prompted, choose **Visual Studio Code** as your default editor if you already use it.
---

# 5. Verify Your Installation

Once Git has been installed, let's verify that everything works correctly.

Open Git Bash and type:

```bash
git --version
```

Example output:

```text
git version 2.50.0
```

If you see a version number, Git has been installed successfully.

You can also run:

```bash
git help
```

This displays Git's built-in help system and confirms that Git commands are available.

---

# 6. First Git Configuration

Before creating commits, Git needs some basic information about you.

Every commit records:

- Who created it
- Their email address
- When it was created

This information helps teams understand who made each change.

---

## Configure Your Name

Replace the example with your own name.

```bash
git config --global user.name "Your Name"
```

Example:

```bash
git config --global user.name "Alex Smith"
```

---

## Configure Your Email

Use the same email address that is associated with your GitHub account.

```bash
git config --global user.email "you@example.com"
```

Example:

```bash
git config --global user.email "alex@example.com"
```

---

# 7. Understanding `--global`

Git stores configuration at different levels.

The two most common are **global** and **local**.

---

## Global Configuration

Global settings apply to **every Git repository** on your computer.

These settings are stored in:

```text
~/.gitconfig
```

Example:

```bash
git config --global user.name "Alex Smith"
```

---

## Local Configuration

Local settings apply only to a single repository.

They are stored inside:

```text
.git/config
```

Example:

```bash
git config user.name "Project Name"
```

If the same setting exists in both places, the **local configuration overrides the global configuration** for that repository.

---

# 8. View Your Configuration

To display your current Git configuration:

```bash
git config --list
```

To see where each setting comes from:

```bash
git config --list --show-origin
```

Example output:

```text
file:/home/user/.gitconfig user.name=Alex Smith
file:/home/user/.gitconfig user.email=alex@example.com
```

---
# 9. GitHub Authentication Basics

Later in the course, we'll connect our local repositories to GitHub.

GitHub no longer allows Git operations using your account password.

Instead, Git typically authenticates using one of two methods:

- HTTPS with a Personal Access Token (PAT)
- SSH with an SSH key

We'll cover both methods later in the course.

---

## HTTPS Repository URL

Example:

```text
https://github.com/username/project.git
```

---

## SSH Repository URL

Example:

```text
git@github.com:username/project.git
```

Both URLs connect to the same repository.

The difference is how Git authenticates with GitHub.

---

# Hands-On Exercises

## Exercise 1 — Install and Verify Git

**Time:** 10–20 minutes

Steps:

1. Install Git.
2. Open Git Bash.
3. Run:

```bash
git --version
```

4. Then run:

```bash
git help
```

**Expected Result**

Git is installed successfully and responds to commands.

---

## Exercise 2 — Configure Git

**Time:** 5–10 minutes

Configure your identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Configure Visual Studio Code as your editor:

```bash
git config --global core.editor "code --wait"
```

Verify your configuration:

```bash
git config --list --show-origin
```

**Expected Result**

Git is configured with your name, email address, and preferred editor.

---

# Common Beginner Problems

## "git" is not recognized as a command

Possible solutions:

- Restart Git Bash or your terminal.
- Verify that Git was installed successfully.
- Confirm that Git was added to your system's PATH.

---

## My commits show "Unknown Author"

Configure your identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

---

## GitHub rejected my password

GitHub no longer accepts account passwords for Git operations.

Instead, use:

- Personal Access Tokens (HTTPS)
- SSH Keys

We'll learn both methods later in this course.

---

# Before You Continue

Before moving on to Lesson 1:

### 1. Join the Daily Support Session (If Needed)

If you have any questions, you can join **Ksenija and Ognjen** during the daily support session.

**Time:**

- **7:00 AM – 8:00 AM EST**
- **1:00 PM – 2:00 PM CET**

Feel free to ask questions about today's lesson or any exercises you've completed.

---

### 2. Complete the Moodle Quiz

Log in to your Moodle account and complete the quiz:

**Course Orientation: Getting Started with Git & GitHub**

You may take the quiz **as many times as you'd like**.

The goal of the quiz is not to grade you, but to reinforce the material you've learned and help identify topics you may want to review before moving on.

---

# Lesson Summary

Today you prepared your development environment for the rest of the course.

You learned:

- How the course is organized
- Where to get help during the training
- Which software you'll use
- How to install Git
- How to verify your installation
- How to configure your Git identity
- The difference between global and local configuration
- The basics of GitHub authentication

Your environment is now ready, and you're prepared to begin learning how Git works.

In **Lesson 1**, we'll explore what Git is, why developers use version control, and the problems Git was designed to solve.