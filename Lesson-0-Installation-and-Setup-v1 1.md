# Lesson 0 - Installation and Initial Setup

**Audience:** Complete Beginners (No Git or GitHub Experience Required)

**Duration:** 30-60 Minutes

**Prerequisites:** None

---

# Learning Objectives

By the end of this lesson, you will be able to:

* Identify the software needed for the rest of the course.
* Install Git on your computer.
* Verify that Git works from the terminal.
* Configure your Git name and email.
* Choose and configure a default text editor.
* Understand the difference between global and local Git settings.
* Understand the difference between HTTPS and SSH repository URLs.

---

# 1 - Software You'll Need

Before the course starts, prepare the tools below.

### Git

Git is the software that tracks your project history.

Official website:

https://git-scm.com/

---

### GitHub Account

GitHub is used for storing repositories online and collaborating with others.

https://github.com/

---

### Visual Studio Code (Recommended)

Visual Studio Code is a free code editor with good Git support.

https://code.visualstudio.com/

---

### GitHub Desktop (Optional)

GitHub Desktop is a graphical interface for Git.

It can be helpful for beginners, but this course also teaches the command line.

https://desktop.github.com/

---

# 2 - Installing Git

Git is available for:

* Windows

The official Git website is:

https://git-scm.com/

---

# Installing Git on Windows

Most Windows developers should install:

**Git for Windows**

During installation:

* Keep the default options unless you know you need something different
* Choose VS Code as the editor if you already use it
* Choose Git Bash as the terminal option

After installation, open:

**Git Bash**

Git Bash provides a command-line environment where Git commands work consistently.

---

# Verify Git Installation

After installing Git, check that it works:

```bash
git --version
```

Example output:

```text
git version 2.50.0
```

If you see a version number, Git is installed correctly.

You can also run:

```bash
git help
```

This confirms that Git commands are available.

---

# 3 - First Git Configuration

Git needs some basic information about you before creating commits.

Every commit records:

* Who created it
* Their email address
* When it was created

This helps teams understand who changed what.

---

# Setting Your Name

Replace the example with your real name:

```bash
git config --global user.name "Your Name"
```

Example:

```bash
git config --global user.name "Alex Smith"
```

---

# Setting Your Email

Use the email connected to your GitHub account:

```bash
git config --global user.email "you@example.com"
```

Example:

```bash
git config --global user.email "alex@example.com"
```

---

# What Does `--global` Mean?

Git settings can exist at different levels.

## Global Settings

Apply to all repositories on your computer.

Stored in:

```text
~/.gitconfig
```

Example:

```bash
git config --global user.name "Alex"
```

---

## Local Settings

Apply only to one repository.

Stored inside:

```text
.git/config
```

Example:

```bash
git config user.name "Project Name"
```

Local settings override global settings.

---

# Check Your Configuration

View your Git settings:

```bash
git config --list
```

To see where settings come from:

```bash
git config --list --show-origin
```

Example:

```text
file:/home/user/.gitconfig user.name=Alex
file:/project/.git/config user.email=team@example.com
```

---

# Set VS Code as Your Editor

If you use VS Code:

```bash
git config --global core.editor "code --wait"
```

The `--wait` option tells Git:

"Wait until I finish editing before continuing."

---

# 4 - GitHub Authentication Basics

GitHub does not use normal passwords for Git operations.

When Git needs to connect to GitHub, you will usually use:

* HTTPS with a Personal Access Token
* SSH with an SSH key

Repository URLs look different depending on the method.

## Using HTTPS

```bash
https://github.com/username/project.git
```

## Using SSH

```bash
git@github.com:username/project.git
```

You will use these URLs later when connecting a local repository to GitHub.

---

# Hands-On Exercises

# Exercise 1 - Install and Verify Git

**Time: 10-20 minutes**

Steps:

1. Install Git
2. Open Git Bash or terminal
3. Run:

```bash
git --version
```

4. Run:

```bash
git help
```

Expected result:

Students have a working Git installation.

---

# Exercise 2 - Configure Git

**Time: 5-10 minutes**

Steps:

Set your identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Set your editor:

```bash
git config --global core.editor "code --wait"
```

Check settings:

```bash
git config --list --show-origin
```

Expected result:

Git knows the student's identity and preferences.

---

# Common Beginner Problems

## "Git command not found"

Possible solutions:

* Restart terminal after installation
* Confirm Git was installed
* Check system PATH settings

---

## "My commit says unknown author"

Solution:

Configure:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

---

## "GitHub rejected my password"

Explanation:

GitHub does not use normal passwords for Git operations.

Use:

* SSH keys
* Personal Access Tokens

---

# Lesson Summary

Today you prepared the tools needed for the course:

* Git
* A GitHub account
* VS Code
* Optional GitHub Desktop

You also verified Git, configured your identity, and learned where Git stores configuration.

In the next lesson, you'll learn what Git does and why developers use it.

---
