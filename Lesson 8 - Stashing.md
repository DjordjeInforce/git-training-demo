# Lesson 8 - Git Stashing

**Audience / Level:** Beginner developers learning how to temporarily save unfinished work

**Duration:** 45-60 minutes

**Prerequisites:**

* Lesson 0 - Installation and Initial Setup
* Lesson 2 - Creating Your First Git Repository
* Lesson 3 - Introducing Git
* Lesson 4 - Git Basics: Working with Changes and Commits
* Lesson 5 - Understanding Commits
* Lesson 6 - Branching
* Lesson 7 - Merging
* Lesson 8 - Inspecting Changes with Git Diff

---

# Learning Objectives

By the end of this lesson, students will be able to:

* Explain what Git Stash is and why it is useful
* Save unfinished work using `git stash`
* View saved stashes using `git stash list`
* Restore stashed work using `git stash apply`
* Restore and remove a stash using `git stash pop`
* Create named stashes
* Stash only selected changes
* Explain when Git Stash should be used instead of committing

---

# 1 - What Is Git Stash?

As you work on a project, there will be times when you need to stop what you're doing and work on something else.

For example:

* A production bug needs immediate attention.
* Your team asks you to fix another issue.
* You need to switch to another branch.
* You need to pull the latest changes before continuing your work.

The problem is that your current work isn't finished yet.

You don't want to create a commit because the feature is incomplete, but you also don't want to lose your work.

Git provides a solution called **Git Stash**.

A stash temporarily saves your uncommitted changes and restores your working directory to its last committed state.

Think of Git Stash as placing your unfinished work into a temporary storage box. When you're ready, you can take it back out and continue working exactly where you left off.

---

# 2 - Saving Your Work

To save your current changes, use:

```bash
git stash
```

Git will:

* Save your tracked changes.
* Return your working directory to the most recent commit.
* Store your work safely in the stash.

Check the status afterward:

```bash
git status
```

Example output:

```text
On branch main
nothing to commit, working tree clean
```

Your files have **not** been deleted.

Git has simply stored the changes for later.

---

# 3 - Viewing Your Stashes

Git can store multiple stashes.

To see them, run:

```bash
git stash list
```

Example output:

```text
stash@{0}: WIP on main: Add login validation
stash@{1}: WIP on main: Update README
```

Each stash receives an identifier.

The newest stash is always:

```text
stash@{0}
```

Older stashes move down the list.

---

# 4 - Restoring a Stash

There are two common ways to restore your work.

## Using `git stash apply`

```bash
git stash apply
```

This restores the latest stash but leaves it in the stash list.

Use this if you think you might need the same stash again.

---

## Using `git stash pop`

```bash
git stash pop
```

This restores the latest stash and removes it from the stash list.

Use this when you're finished with the stash.

Remember:

| Command | Restores Changes | Removes Stash |
|----------|------------------|---------------|
| `git stash apply` | ✅ Yes | ❌ No |
| `git stash pop` | ✅ Yes | ✅ Yes |

---

# 5 - Creating Named Stashes

Git automatically creates a default description for every stash.

However, you can create your own descriptive message.

Example:

```bash
git stash push -m "WIP: Update login page"
```

View it:

```bash
git stash list
```

Example output:

```text
stash@{0}: On main: WIP: Update login page
```

Using meaningful names makes it much easier to find the correct stash later.

You decide which changes to stash and which changes remain in your working directory.

This is called an **interactive** or **partial** stash.


# 7 - Common Uses for Git Stash

Developers frequently use Git Stash when:

* Switching branches before finishing work.
* Fixing an urgent production bug.
* Pulling the latest changes from the remote repository.
* Experimenting with code they may not keep.
* Pausing one feature to work on another.

If your work is temporary or incomplete, Git Stash is often a better choice than creating an unnecessary commit.

---

# 8 - Practicing Git Stash

Use the repository you've been working with throughout this course.

Check your repository status:

```bash
git status
```

Modify an existing file.

For example:

```bash
echo "Temporary change" >> notes.txt
```

Check your changes:

```bash
git status
```

Save your work:

```bash
git stash
```

Verify that your working directory is clean:

```bash
git status
```

View the stash:

```bash
git stash list
```

Restore your work:

```bash
git stash pop
```

Verify your changes have returned:

```bash
git status
```

---

# Hands-On Exercises

# Exercise 1 - Create Your First Stash

**Time:** 15 minutes

### Goal

Learn how to temporarily save unfinished work.

### Steps

1. Modify an existing file.

2. Check your repository status.

```bash
git status
```

3. Save your changes.

```bash
git stash
```

4. Verify your working directory is clean.

```bash
git status
```

5. Restore your changes.

```bash
git stash pop
```

### Expected Result

Students understand that Git can temporarily save unfinished work without creating a commit.

---

# Exercise 2 - Working with Multiple Stashes

**Time:** 15 minutes

### Goal

Learn how Git manages multiple stashes.

### Steps

Create your first stash.

```bash
git stash push -m "Update documentation"
```

Make another change.

Create a second stash.

```bash
git stash push -m "Fix login form"
```

View the stash list.

```bash
git stash list
```

### Expected Result

Students understand that Git stores multiple stashes in a stack.

---

# Exercise 3 - Partial Stashes

**Time:** 15 minutes

### Goal

Practice saving only selected changes.

### Steps

Modify multiple sections of a file.

Run:

```bash
git stash push -p
```

Choose which changes should be stashed.

Verify that only the selected changes were removed.

### Expected Result

Students understand how partial stashes work.

---

# Common Beginner Mistakes

## "Did Git delete my work?"

No.

Your changes are safely stored.

View your saved stashes:

```bash
git stash list
```

---

## "What's the difference between apply and pop?"

`git stash apply`

* Restores the stash.
* Keeps it for future use.

`git stash pop`

* Restores the stash.
* Removes it after restoring.

---

## "Why shouldn't I just commit?"

Sometimes your work is:

* Incomplete
* Experimental
* Not ready to become part of project history

Git Stash lets you save your progress without creating unnecessary commits.

---

## "Can I have more than one stash?"

Yes.

Git allows you to save multiple stashes.

Use:

```bash
git stash list
```

to view them.

---

# Before Continuing

Before moving to the next lesson, make sure you can:

- [ ] Explain what Git Stash is used for.
- [ ] Save your work using `git stash`.
- [ ] View saved stashes using `git stash list`.
- [ ] Restore a stash using `git stash apply`.
- [ ] Restore and remove a stash using `git stash pop`.
- [ ] Create a named stash.
- [ ] Create a partial stash using `git stash push -p`.
- [ ] Explain when Git Stash is a better choice than committing.

---

# Lesson Summary

Today you learned how to temporarily save unfinished work using Git Stash.

You practiced:

* `git stash`
* `git stash list`
* `git stash apply`
* `git stash pop`
* `git stash push -m`
* `git stash push -p`

Git Stash is a powerful tool that lets you pause your work without creating unnecessary commits, making it easy to switch tasks and return to your work later.

---

