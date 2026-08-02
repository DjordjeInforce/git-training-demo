# Lesson 5 — Understanding Commits in Detail

**Audience / Level:** Beginner → Intermediate developers learning how to create, improve, and manage commits
**Duration:** 45–75 minutes
**Prerequisites:** Lesson 4 — Git Basics

---

# Learning Objectives

By the end of this lesson, students will be able to:

* Write clear and meaningful commit messages
* Understand what makes a good commit
* Fix the most recent commit using `git commit --amend`
* Understand the purpose of combining commits
* Use `.gitignore` to prevent unwanted files from being tracked
* Inspect commit history and understand `HEAD`

---

# 1 — What Makes a Good Commit?

A commit is more than just saving files.

A commit tells a story:

* What changed?
* Why was it changed?
* How does this change help the project?

Good commits make it easier to:

* Understand project history
* Find problems later
* Review code changes
* Work with other developers

---

# Bad Commit Examples

These messages do not provide enough information:

```
update
fix
changes
work done
final version
```

A future developer will not know what happened.

---

# Better Commit Examples

```
Add login form validation

Fix incorrect password error message

Update installation instructions
```

These messages explain the purpose of the change.

---

# 2 — Writing Good Commit Messages

A common commit format:

```
Short summary

Optional detailed explanation
```

Example:

```
Add email validation to signup form

Validate email addresses before creating new accounts.
This prevents invalid user registrations.
```

---

# Commit Message Rules

## 1. Keep the first line short

A good subject line is usually:

* Around 50 characters
* Easy to read in logs

Example:

Good:

```
Add user profile page
```

Too long:

```
Add a completely new user profile page with settings and account management options
```

---

## 2. Use an action style

Write the message as if giving a command.

Good:

```
Add login button
Fix broken link
Update documentation
```

Avoid:

```
Added login button
Fixed broken link
Updated documentation
```

---

## 3. Explain why when needed

Simple changes only need one line.

Complex changes benefit from a body.

Example:

```
Fix payment validation issue

The payment form accepted empty card numbers.
This change adds validation before submission.
```

---

# 3 — Creating Better Commits

A good commit should usually contain:

✓ One logical change
✓ Related files only
✓ A clear message

Avoid creating commits like:

```
Update everything
```

with many unrelated changes.

Instead:

```
Add database configuration

Update README instructions

Fix login error
```

Small commits are easier to understand and review.

---

# 4 — Fixing the Last Commit with Amend

Sometimes you create a commit and immediately notice a mistake.

Examples:

* Forgot to include a file
* Made a typo in the commit message
* Forgot a small change

Git provides:

```bash
git commit --amend
```

This updates the most recent commit.

---

# Example 1 — Fix the Commit Message

Current commit:

```
Add user logn
```

Correct it:

```bash
git commit --amend -m "Add user login"
```

The previous commit message is replaced.

---

# Example 2 — Add a Forgotten File

Imagine:

You committed:

```bash
git commit -m "Add profile page"
```

Then you realize:

```
profile.css
```

was missing.

Add the file:

```bash
git add profile.css
```

Update the commit:

```bash
git commit --amend --no-edit
```

The existing message stays the same.

---

# Important Safety Rule

Amending changes the commit history.

It is safe when:

✓ The commit is only on your computer
✓ Nobody else has downloaded it

Avoid amending commits that are already shared with teammates.

---

# 5 — Combining Commits (Squashing)

Sometimes developers create several small commits while working.

Example:

```
Add button
Fix button style
Fix button spacing
Fix button color
```

Before sharing, they may combine them into one cleaner commit:

```
Add styled button component
```

This process is called:

**Squashing commits**

---

# Why Squash Commits?

Benefits:

* Cleaner project history
* Easier code review
* Easier understanding of changes

Example:

Before:

```
C4 Fix typo
C3 Add tests
C2 Add feature
C1 Initial commit
```

After:

```
C2 Add feature with tests
C1 Initial commit
```

---

# Introduction to Interactive Rebase

The command commonly used is:

```bash
git rebase -i HEAD~3
```

This means:

"Show my last three commits so I can organize them."

We will learn this process in detail in a later lesson.

For now, remember:

**Squashing combines multiple commits into a cleaner history.**

---

# 6 — Using `.gitignore`

Not every file belongs in Git.

Some files should stay only on your computer.

Examples:

* Temporary files
* Build output
* Password files
* Editor settings
* Dependencies

Git uses:

```
.gitignore
```

to decide what should not be tracked.

---

# Example `.gitignore`

Create a file named:

```
.gitignore
```

Example:

```
# Operating system files
.DS_Store
Thumbs.db

# Node dependencies
node_modules/

# Build files
dist/

# Editor settings
.vscode/

# Secret files
.env
*.key
*.pem
```

---

# Important: `.gitignore` Does Not Remove Existing Files

If a file is already committed, adding it to `.gitignore` will not remove it.

Example:

You already committed:

```
.env
```

Then add:

```
.env
```

to `.gitignore`.

Git will still track it.

---

# Remove a File from Tracking

Keep the file on your computer:

```bash
git rm --cached filename
```

Example:

```bash
git rm --cached .env
```

Then commit:

```bash
git commit -m "Stop tracking environment file"
```

---

# 7 — Understanding Git History

Git provides several commands for exploring commits.

---

# View Commit History

Simple:

```bash
git log
```

Short version:

```bash
git log --oneline
```

Example:

```
a81bc21 Add login page
b91d220 Create project
c41aa10 Initial commit
```

---

# Visual History

Use:

```bash
git log --oneline --graph --decorate
```

Example:

```
* a81bc21 Add login page
* b91d220 Create project
* c41aa10 Initial commit
```

Later, this will help visualize branches.

---

# View a Specific Commit

Command:

```bash
git show <commit>
```

Example:

```bash
git show HEAD
```

Shows:

* Commit message
* Changed files
* Actual changes

---

# 8 — Understanding HEAD

`HEAD` is Git's name for your current position.

Most of the time, `HEAD` points to your current branch.

The branch points to the latest commit on that branch.

Example:

```
HEAD
 |
 v
main
 |
 v
C3
```

This means:

* You are on the `main` branch
* `main` currently points to commit `C3`
* New commits will be added after `C3`

In short:

```
HEAD -> main -> latest commit
```

---

# What Happens When You Commit?

Before a new commit:

```text
HEAD
 |
 v
main
 |
 v
C1 --- C2
```

After you create a new commit:

```text
HEAD
 |
 v
main
 |
 v
C1 --- C2 --- C3
```

The important idea:

`HEAD` did not move by itself.

Your branch moved forward to the new commit, and `HEAD` still points to that branch.

---

# Finding the Current Commit

Command:

```bash
git rev-parse HEAD
```

Example output:

```
a81bc21f92d8...
```

This is the unique commit identifier.

---


# Recovering with reflog

Sometimes developers think:

"I lost my commit!"

Git keeps a local record of where HEAD has been.

Command:

```bash
git reflog
```

Example:

```
a81bc21 HEAD@{0}: commit
b91d220 HEAD@{1}: checkout main
```

`reflog` can help recover from mistakes.

---

# Hands-On Exercises

# Exercise 1 — Create Better Commits

**Time: 15 minutes**

Steps:

1. Make a small project change.
2. Create a commit with only a short message.

Example:

```
Add contact page
```

3. Make another change.
4. Create a commit with:

* Subject
* Explanation body

5. Compare:

```bash
git show HEAD
```

Expected Result:

Students understand the difference between basic and detailed commit messages.

---

# Exercise 2 — Amend a Commit

**Time: 10 minutes**

Steps:

1. Create a commit:

```bash
git commit -m "Add profile page"
```

2. Create a missing file:

```bash
touch profile.css
```

3. Add it:

```bash
git add profile.css
```

4. Amend:

```bash
git commit --amend --no-edit
```

5. Check history:

```bash
git log --oneline
```

Expected Result:

Students fix a recent commit without creating an unnecessary extra commit.

---

# Exercise 3 — Create a `.gitignore`

**Time: 15 minutes**

Steps:

1. Create:

```
.gitignore
```

2. Add:

```
*.log
.env
```

3. Create:

```
test.log
```

4. Check:

```bash
git status
```

Expected Result:

Ignored files no longer appear as untracked.
---

# Common Beginner Mistakes

## "I changed my commit but the old one disappeared"

Explanation:

Amend replaces the previous commit with a new version.

---

## "Why is `.gitignore` not working?"

Common reason:

The file was already tracked.

Solution:

```bash
git rm --cached filename
```

---

## "Can I rewrite history?"

Yes, but only carefully.

Safe:

* Local commits
* Personal branches

Be careful:

* Shared team branches

---

