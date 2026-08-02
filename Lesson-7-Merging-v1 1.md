# Lesson 7 — Git Merging: Combining Work Safely

**Audience / Level:** Beginner → Intermediate developers learning how to combine changes from different branches
**Duration:** 45–75 minutes
**Prerequisites:**

* Lesson 4 — Git Basics
* Lesson 6 — Branches

---

# Learning Objectives

By the end of this lesson, students will be able to:

* Explain why Git merging is needed
* Understand fast-forward
* Merge one branch into another
* Read Git merge results
* Understand why merge conflicts happen
* Resolve simple merge conflicts
* Use safe recovery commands when a merge goes wrong

---

# 1 — Why Do We Need Merging?

Branches allow developers to work separately.

Example:

A developer creates a feature branch:

```text
main

A --- B --- C

        \
         D --- E
         feature/login
```

The feature is complete.

Now the changes need to return to `main`.

This is called:

**merging**

After merging:

```text
main

A --- B --- C ----- M
        \          /
         D --- E --
```

Git combines the work from both branches.

---

# 2 — Understanding Merge Concepts

Before merging, Git compares:

* The current branch
* The branch being merged
* The point where they separated

Git tries to combine the changes automatically.

Most merges happen without problems.

Sometimes Git needs help.

Those situations are called:

**merge conflicts**

---

# 3 — Fast-Forward Merge

A fast-forward merge happens when the main branch has not changed since the feature branch was created.

Example:

Starting point:

```text
main
 |
A --- B
```

Create feature branch:

```text
main
 |
A --- B
      \
       C
       feature
```

No new commits on `main`.

When merging:

```bash id="7z0h8r"
git switch main
git merge feature
```

Git simply moves the `main` pointer:

```text
main
 |
A --- B --- C
```

No extra merge commit is created.

---

# 5 — Performing a Merge

The normal merge workflow:

## Step 1 — Switch to the Receiving Branch

Usually:

```bash id="5k8m11"
git switch main
```

You are telling Git:

"I want to bring changes into main."

---

## Step 2 — Merge the Feature Branch

Example:

```bash id="j5d3gy"
git merge feature/login
```

Git attempts to combine the changes.

---

## Step 3 — Check the Result

Run:

```bash id="b6r8kf"
git status
```

If successful:

```text
working tree clean
```

---

# 6 — Creating a Merge Commit on Purpose

Sometimes teams want every feature integration recorded.

Use:

```bash id="x6u4j2"
git merge --no-ff feature/login
```

`--no-ff` means:

"Always create a merge commit."

This can make project history easier to understand.

Example:

```text
          Merge login feature
               |
A --- B ------- M
       \       /
        C --- D
```

---

# 7 — Understanding Merge Conflicts

A conflict happens when Git cannot automatically decide which change should win.

Example:

Original file:

```text
Welcome to my website
```

Developer A changes it:

```text
Welcome to my application
```

Developer B changes it:

```text
Welcome to our platform
```

Git sees two different changes to the same line.

It asks:

"Which version should I keep?"

---

# What a Conflict Looks Like

Git adds markers:

```text id="n0f4y6"
<<<<<<< HEAD
Welcome to my application
=======
Welcome to our platform
>>>>>>> feature/update
```

Meaning:

```text
<<<<<<< HEAD
Your current branch
=======

Other branch
>>>>>>> branch-name
```

---

# 8 — Resolving a Merge Conflict

When a conflict happens:

---

## Step 1 — Check the Problem

Run:

```bash id="gjy7sc"
git status
```

Example:

```text
both modified: README.md
```

---

## Step 2 — Open the File

Find conflict markers:

```text
<<<<<<<
=======
>>>>>>>
```

Decide what the final version should look like.

Example:

Before:

```text
<<<<<<< HEAD
Welcome to my application
=======
Welcome to our platform
>>>>>>> feature/update
```

After editing:

```text
Welcome to our application
```

Remove all conflict markers.

---

## Step 3 — Stage the Resolution

Tell Git the conflict is fixed:

```bash id="3y9wup"
git add README.md
```

---

## Step 4 — Complete the Merge

Create the merge commit:

```bash id="yz4w5k"
git commit
```

Git usually provides a default merge message.

---

# 9 — Aborting a Merge

Sometimes you start a merge and realize:

* Wrong branch
* Too many conflicts
* Need to rethink the approach

You can cancel:

```bash id="d8v6j1"
git merge --abort
```

This returns your repository to the state before the merge started.

---

# 10 — Using Merge Tools

Instead of manually comparing files, developers can use visual tools.

Examples:

* VS Code merge editor
* Vimdiff
* Other Git-compatible merge tools

Start a merge tool:

```bash id="c9a5wb"
git mergetool
```

Configure a tool:

```bash id="g3w2js"
git config --global merge.tool vscode
```

---

# 11 — Safe Merge Practices

Good merge habits:

---

## Keep Branches Small

Smaller branches create fewer conflicts.

Better:

```text
Feature A
  ↓
Merge
  ↓
Feature B
  ↓
Merge
```

Avoid:

```text
Huge branch for six months
```

---

## Merge Frequently

Regular merging keeps branches closer together.

---

## Review Before Merging

Before merging:

Check:

```bash id="4jv6ae"
git status
```

View changes:

```bash id="f4q2e7"
git diff main feature/login
```

---

# Hands-On Exercises

# Exercise 1 — Fast-Forward Merge

**Time: 15 minutes**

Goal:

See how Git moves branch pointers.

Steps:

Create a branch:

```bash id="4f7x2p"
git switch -c feature/fast-forward
```

Create a commit:

```bash id="j7k2o0"
echo "Feature change" > feature.txt
git add feature.txt
git commit -m "Add feature file"
```

Return:

```bash id="9a4n1h"
git switch main
```

Merge:

```bash id="0h6n7z"
git merge feature/fast-forward
```

View:

```bash id="7w2wq1"
git log --oneline --graph
```

Expected result:

Students see a fast-forward merge.

---

# Exercise 2 — Create and Resolve a Conflict

**Time: 20–30 minutes**

Goal:

Practice real conflict resolution.

---

## Step 1

Create:

```text
README.md

Welcome
```

Commit:

```bash id="h3w4r6"
git add README.md
git commit -m "Add welcome message"
```

---

## Step 2

Create branch:

```bash id="0v3m7d"
git switch -c feature/change-message
```

Edit README:

```text
Welcome to Git training
```

Commit:

```bash id="3a9p4k"
git add README.md
git commit -m "Update welcome message"
```

---

## Step 3

Return to main:

```bash id="4d8y0n"
git switch main
```

Change the same line differently.

Commit:

```bash id="6h7z3p"
git add README.md
git commit -m "Change welcome text"
```

---

## Step 4

Merge:

```bash id="7p1f3a"
git merge feature/change-message
```

A conflict should appear.

Resolve it.

Then:

```bash id="n8s4q2"
git add README.md
git commit
```

Expected result:

Students complete a real merge conflict.

---

# Exercise 3 — Explore Merge Tools (Optional)

**Time: 10–15 minutes**

Steps:

1. Configure a merge tool.
2. Create a conflict.
3. Run:

```bash id="w9c6s5"
git mergetool
```

Expected result:

Students understand visual conflict resolution.

---
# Common Beginner Mistakes

## "A conflict means Git is broken"

Correction:

Conflicts are normal when multiple people edit the same area.

---

## "I should always choose my version"

Correction:

The correct solution depends on the project.

Sometimes both changes need to be combined.

---

## "I am stuck in a merge"

Use:

```bash id="s9k7f4"
git status
```

It tells you the next step.

---

## "Can I undo a merge?"

Yes, before completing:

```bash id="r8w1x4"
git merge --abort
```

---

