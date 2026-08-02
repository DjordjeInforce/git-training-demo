# Lesson 8 — Understanding Changes with Git Diff

**Audience / Level:** Beginner developers learning how to see and understand changes
**Duration:** 30–45 minutes
**Prerequisites:**

* Lesson 4 — Git Basics
* Lesson 5 — Commits In Detail

---

# Learning Objectives

By the end of this lesson, students will be able to:

* Explain what `git diff` does
* View changes before committing
* Understand the difference between staged and unstaged changes
* Compare commits and branches
* Read Git diff output
* Use helpful diff options for reviewing changes

---

# 1 — Why Do We Need `git diff`?

When working on a project, developers constantly change files.

For example:

You open:

```text
README.md
```

You edit:

```text
Hello Git
```

into:

```text
Hello Git Training
```

Before committing, you may want to ask:

* What exactly did I change?
* Did I accidentally remove something?
* Are my changes ready to commit?

`git diff` answers these questions.

Think of it as:

> "Show me the difference between two versions of my project."

---

# 2 — The Three Places Git Compares

To understand `git diff`, remember the three areas from earlier lessons:

```text
Working Directory
        |
        |
     git add
        |
        v
Staging Area
        |
        |
   git commit
        |
        v
Repository
```

Git can compare these areas.

---

# 3 — Viewing Unstaged Changes

When you edit a file but do not run `git add` yet:

```bash
git diff
```

shows the changes that are still only in your working directory.

Example:

You had:

```text
Hello Git
```

You changed it to:

```text
Hello Git World
```

`git diff` shows:

```diff
- Hello Git
+ Hello Git World
```

Meaning:

* `-` removed line
* `+` added line

---

# 4 — Viewing Staged Changes

After adding a file:

```bash
git add README.md
```

the change moves to the staging area.

Now:

```bash
git diff
```

shows nothing.

Why?

Because there are no unstaged changes.

To see staged changes:

```bash
git diff --staged
```

or:

```bash
git diff --cached
```

This shows:

```
Staging Area → Last Commit
```

---

# 5 — Comparing Everything with HEAD

Sometimes you want to see:

"What has changed since my last commit?"

Use:

```bash
git diff HEAD
```

This compares:

```
Working Directory + Staging Area
        |
        v
      HEAD
```

Example:

```bash
git diff HEAD
```

shows all current changes that are not yet committed.

---

# 6 — Comparing Commits

Git can compare older versions of your project.

Example:

View the difference between the previous commit and the latest commit:

```bash
git diff HEAD~1 HEAD
```

Meaning:

```text
HEAD~1 = previous commit

HEAD = current commit
```

---

# Comparing Two Specific Commits

Example:

```bash
git diff abc123 def456
```

Git shows what changed between those two commits.

---

# 7 — Reading Diff Output

A Git diff looks like:

```diff
@@ -10,5 +10,6 @@
 Hello Git
-Old line
+New line
 Another line
```

Let's break it down.

---

## Removed Lines

Start with:

```diff
-
```

Example:

```diff
-Old text
```

This line existed before but was removed.

---

## Added Lines

Start with:

```diff
+
```

Example:

```diff
+New text
```

This line was added.

---

## Unchanged Lines

Lines without a symbol are context.

Example:

```text
Hello Git
```

They help you understand where the change happened.

---

# 8 — Understanding Diff Headers

Example:

```text
@@ -12,5 +12,6 @@
```

You do not need to memorize this immediately.

The important idea:

* The `-` section describes the old file
* The `+` section describes the new file

Example:

```text
@@ -12,5 +12,6 @@
```

Means:

Old version:

* starts at line 12
* includes 5 lines

New version:

* starts at line 12
* includes 6 lines

---

# 9 — Useful Diff Commands

## Show Changed File Names Only

Sometimes you do not need details.

Use:

```bash
git diff --name-only
```

Example output:

```text
README.md
app.js
config.json
```

---

## Show Summary of Changes

Use:

```bash
git diff --stat
```

Example:

```text
README.md | 5 +++--
app.js    | 10 +++++-----
```

Useful for quickly understanding the size of a change.

---

## Compare Word Changes

For small text changes:

```bash
git diff --color-words
```

Example:

Before:

```text
Create user account
```

After:

```text
Create customer account
```

Git highlights the changed words.

---

Show only changed files:

```bash
git show --name-only HEAD
```

Example:

```text
README.md
server.js
```

---

# Hands-On Exercises

# Exercise 1 — Explore Unstaged and Staged Changes

**Time: 10 minutes**

Goal:

Understand the difference between working files and staged files.

Steps:

Create a file:

```bash
echo "Hello Git" > example.txt
```

Check:

```bash
git diff
```

Add:

```bash
git add example.txt
```

Check:

```bash
git diff
```

Then:

```bash
git diff --staged
```

Expected result:

Students see the difference between unstaged and staged changes.

---

# Exercise 2 — Compare Commits

**Time: 15 minutes**

Steps:

1. Create several commits.

Example:

```bash
git log --oneline
```

2. Compare commits:

```bash
git diff HEAD~2 HEAD
```

3. Inspect one commit:

```bash
git show HEAD
```

Expected result:

Students can review project history.

---

# Exercise 3 — Use Diff Options

**Time: 10 minutes**

Try:

```bash
git diff --stat
```

Then:

```bash
git diff --name-only
```

Then:

```bash
git diff --color-words
```

Expected result:

Students learn different ways to summarize changes.
---
# Common Beginner Mistakes

## "git diff shows nothing"

Possible reasons:

* Changes are already staged
* No changes exist

Try:

```bash
git diff --staged
```

---

## "I cannot understand the output"

Start by looking only for:

```diff
+
-
```

Added and removed lines tell the main story.

---

## "Diff is too large"

Use:

```bash
git diff --stat
```

for a summary first.

---

## "I need to know what changed in a commit"

Use:

```bash
git show HEAD
```

---

