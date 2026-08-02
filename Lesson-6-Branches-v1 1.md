# Lesson 6 - Git Branches: Working on Multiple Versions of Your Project

**Audience / Level:** Beginner developers learning how to work on features safely
**Duration:** 45-60 minutes
**Prerequisites:**

* Lesson 4 - Git Basics
* Lesson 5 - Commits In Detail

---

# Learning Objectives

By the end of this lesson, students will be able to:

* Explain what a Git branch is
* Create and switch between branches
* Understand how branches connect to commits
* Rename and delete branches safely
* Use `git switch` and understand `git checkout`
* Understand the basic idea of merging branches

---

# 1 - Why Do We Need Branches?

Imagine you are working on a website.

The current version works:

```text
main
 |
A --- B --- C
```

Now you want to add a new login feature.

Should you directly change the working version?

Maybe not.

What if:

* The feature is not finished?
* The code breaks?
* You want to try a different approach?

Branches solve this problem.

A branch lets you create a separate line of development.

Example:

```text
              feature/login
                   |
A --- B --- C ----- D --- E

main
 |
A --- B --- C
```

The main project stays safe while you work on the new feature.

---

# 2 - What Is a Git Branch?

A common beginner misunderstanding:

> "A branch is a copy of my project."

This is not true.

A branch is simply a **name that points to a commit**.

Example:

```text
main
 |
 v
C1 --- C2 --- C3
```

The branch `main` points to commit `C3`.

Create a new branch:

```text
main
 |
 v
C1 --- C2 --- C3
             ^
             |
        feature/login
```

Both branches point to the same commit at first.

---

# What Happens After a New Commit?

If we make a commit on `feature/login`:

```text
main
 |
 v
C1 --- C2 --- C3
              \
               C4
               ^
               |
          feature/login
```

The branch moves forward.

The files were not copied.

Only the branch pointer moved.

---

# 3 - Viewing Branches

List branches:

```bash
git branch
```

Example:

```text
* main
  feature/login
```

The `*` shows your current branch.

Show your current branch:

```bash
git branch --show-current
```

Check repository status:

```bash
git status
```

---

# 4 - Creating a Branch

There are two steps:

1. Create a branch
2. Switch to it

---

## Create Only

```bash
git branch feature/login
```

This creates the branch.

You are still on your current branch.

---

## Create and Switch

The recommended beginner command:

```bash
git switch -c feature/login
```

This does both:

* Creates the branch
* Moves you onto it

Example:

```bash
git switch -c feature/profile
```

---

# Older Command: `git checkout`

You may see:

```bash
git checkout -b feature/login
```

This does the same thing.

However, `checkout` has many different uses, so Git introduced:

```bash
git switch
```

to make branch operations clearer.

---

# 5 - Working on a Branch

Example:

Start on:

```text
main
```

Create a feature branch:

```bash
git switch -c feature/about-page
```

Create a file:

```bash
echo "About page" > about.html
```

Commit:

```bash
git add about.html
git commit -m "Add about page"
```

Now history looks like:

```text
main
 |
A --- B

       \
        C
        ^
        |
 feature/about-page
```

The new commit exists only on the feature branch.

---

# 6 - Switching Between Branches

Move back to main:

```bash
git switch main
```

Move to your feature:

```bash
git switch feature/about-page
```

Always check your location:

```bash
git branch
```

---

# Important Beginner Tip

Before switching branches, check your changes:

```bash
git status
```

If you have unfinished work, Git may prevent switching.

---

# 7 - Renaming Branches

Sometimes a branch name needs improvement.

Example:

Current:

```text
feature/login-test
```

Better:

```text
feature/login
```

Rename:

```bash
git branch -m feature/login-test feature/login
```

If you are already on the branch:

```bash
git branch -m new-name
```

---

# 8 - Deleting Branches

After a feature is complete, the branch may no longer be needed.

---

## Safe Delete

```bash
git branch -d feature/login
```

Git checks:

"Has this work been merged?"

If yes, it deletes the branch.

---

## Force Delete

```bash
git branch -D feature/login
```

This deletes the branch even if work is not merged.

Use carefully.

---

# Deleting Remote Branches

A remote branch exists on GitHub or another server.

Delete it with:

```bash
git push origin --delete feature/login
```

Remote branches are covered later in the GitHub lessons.

---

# 9 - Introduction to Merging

Eventually, completed work needs to return to the main branch.

This process is called:

**merging**

Example:

Before:

```text
main

A --- B --- C

        \
         D --- E
         feature/login
```

After merge:

```text
A --- B --- C ------ M
        \           /
         D --- E ---
```

Git combines the changes.

Detailed merging is covered in Lesson 7.

---

# Viewing Branch History

Branches become easier to understand visually.

Run:

```bash
git log --oneline --graph --decorate --all
```

Example:

```text
* e41abc Add login page
|\
| * c32aaa Update documentation
|/
* a91bbb Initial commit
```

---

# Hands-On Exercises

# Exercise 1 - Create and Switch Branches

**Time: 10 minutes**

Goal:

Learn how branches separate work.

Steps:

1. Create a repository with a commit.
2. Create a branch:

```bash
git switch -c feature/profile
```

3. Add a file:

```bash
echo "Profile page" > profile.txt
```

4. Commit:

```bash
git add profile.txt
git commit -m "Add profile page"
```

5. Return to main:

```bash
git switch main
```

6. View history:

```bash
git log --oneline --graph --all
```

Expected result:

Students see separate branch histories.

---

# Exercise 2 - Rename and Delete Branches

**Time: 10 minutes**

Steps:

Rename:

```bash
git branch -m feature/profile feature/user-profile
```

Delete:

```bash
git branch -d feature/user-profile
```

Expected result:

Students understand branch management.

---

# Exercise 3 - Preview a Merge

**Time: 10 minutes**

Steps:

1. Create a branch.
2. Make one commit on the branch.
3. Return to `main`.
4. Merge the branch:

```bash
git merge feature/test
```

5. View history:

```bash
git log --oneline --graph
```

Expected result:

Students see that a branch can be combined back into `main`.

---

# Common Beginner Mistakes

## "Branches copy my files"

Correction:

Branches are pointers to commits.

---

## "I lost my work when switching branches"

Usually caused by:

* Uncommitted changes
* Wrong branch

Solution:

Use:

```bash
git status
```

before switching.

---

## "I deleted my branch, is my code gone?"

Usually no.

If commits exist elsewhere, Git can often recover them.

---

## "Should I always work on main?"

For learning projects maybe.

For team projects:

Usually create feature branches.

Team workflows are covered in Lesson 13.

---

# Lesson Summary

Today you learned how branches let you work on separate versions of a project.

You practiced:

* Viewing branches
* Creating branches
* Switching branches
* Renaming branches
* Deleting branches
* Previewing a merge

In the next lesson, you will learn merging in detail.

---
