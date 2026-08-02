# Lesson 09 - Undoing Changes Safely

**Audience / Level:** Beginners learning how to recover from common Git mistakes

**Duration:** 45-70 minutes

**Prerequisites:** Lesson 08 - Git Stashing

---

## Learning Objectives

By the end of this lesson, you will be able to:

- Use `git restore` to discard unstaged file changes.
- Use `git restore --staged` to unstage files.
- Use `git reset --soft`, `git reset --mixed`, and `git reset --hard`.
- Use `git revert` for shared commits.
- Use `git reflog` to find lost local commits.
- Choose a safer undo command using a decision tree.

---

## 1. The Main Question

Before undoing anything, ask:

> Did I commit the change?

Then ask:

> Has anyone else received this commit?

Git has different undo tools for different situations.

---

## 2. Undo Decision Tree

```text
Did you commit?
|
+-- No
|   |
|   +-- Is the change staged?
|   |   |
|   |   +-- Yes: git restore --staged filename
|   |
|   +-- Is the change unstaged?
|       |
|       +-- Yes: git restore filename
|
+-- Yes
    |
    +-- Is it local only?
    |   |
    |   +-- Yes: git reset
    |
    +-- Was it pushed or shared?
    |   |
    |   +-- Yes: git revert <commit>
    |
    +-- Did a commit seem lost?
        |
        +-- Use: git reflog
```

When unsure, run:

```bash
git status
git log --oneline
```

---

## 3. Unstage a File

If you staged a file by mistake:

```bash
git restore --staged filename
```

Example:

```bash
echo "Undo practice" >> notes.md
git add notes.md
git restore --staged notes.md
```

The change stays in your file, but it is no longer staged.

---

## 4. Discard Unstaged File Changes

If you changed a file and want to throw away the uncommitted edit:

```bash
git restore filename
```

Example:

```bash
git restore notes.md
```

Warning:

This removes your local file changes. If you need them later, commit or stash first.

---

## 5. Reset Local Commits

`git reset` moves your current branch to another commit.

Use reset mainly for local commits that you have not shared.

### Soft Reset

```bash
git reset --soft HEAD~1
```

Removes the last commit, but keeps the changes staged.

Use when you want to redo the commit message or add more files.

### Mixed Reset

```bash
git reset --mixed HEAD~1
```

Removes the last commit and unstages the changes.

This is the default mode:

```bash
git reset HEAD~1
```

### Hard Reset

```bash
git reset --hard HEAD~1
```

Strong warning:

Warning: `git reset --hard` can delete uncommitted work. Run `git status` before using it.

`git reset --hard` discards that commit and any uncommitted changes in your working directory.

Do not use `--hard` on important work unless you have a backup, a commit you can recover, or instructor guidance.

---

## 6. Revert Shared Commits

If a bad commit was pushed or shared, prefer:

```bash
git revert <commit>
```

Example:

```bash
git revert HEAD
```

`git revert` creates a new commit that undoes the old commit.

If you want Git to use the default revert message without opening an editor, use:

```bash
git revert --no-edit HEAD
```

This keeps history intact and is safer for collaboration.

---

## 7. Recover with Reflog

If you think a local commit disappeared:

```bash
git reflog
```

Example output:

```text
abc1234 HEAD@{0}: reset: moving to HEAD~1
def4567 HEAD@{1}: commit: Add practice file
```

To recover a commit into a new branch:

```bash
git switch -c recovery def4567
```

Reflog is local. It records where your `HEAD` has been on your computer.

---

## Hands-On Exercises

### Exercise 1 - Unstage and Restore

```bash
echo "Undo practice line" >> notes.md
git add notes.md
git status
git restore --staged notes.md
git status
git restore notes.md
git status
```

Expected result: The staged change becomes unstaged, then the file returns to the last committed version.

### Exercise 2 - Compare Reset Modes

Use a disposable practice file:

```bash
echo "Reset mode practice" > reset-demo.md
git add reset-demo.md
git commit -m "Add reset demo"
echo "Soft reset line" >> reset-demo.md
git add reset-demo.md
git commit -m "Add soft reset practice"
git reset --soft HEAD~1
git status
git commit -m "Add soft reset practice"
```

Repeat with mixed reset:

```bash
echo "Mixed reset line" >> reset-demo.md
git add reset-demo.md
git commit -m "Add mixed reset practice"
git reset --mixed HEAD~1
git status
git add reset-demo.md
git commit -m "Add mixed reset practice"
```

Only try hard reset on disposable work:

```bash
echo "Disposable hard reset line" >> reset-demo.md
git add reset-demo.md
git commit -m "Add disposable hard reset practice"
git reset --hard HEAD~1
git status
```

### Exercise 3 - Revert a Commit

```bash
echo "Revert practice" > revert-demo.md
git add revert-demo.md
git commit -m "Add revert demo"
git revert --no-edit HEAD
git log --oneline
```

Expected result: Git creates a new commit that reverses the previous commit.

### Exercise 4 - Find a Commit with Reflog

```bash
git reflog
```

Find recent commit movement. Do not recover anything unless you are using a disposable practice commit.

---

## Commands Learned in This Lesson

```bash
git restore filename
git restore --staged filename
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset HEAD~1
git reset --hard HEAD~1
git revert <commit>
git revert --no-edit HEAD
git reflog
git switch -c recovery <commit-hash>
```

---

## Common Beginner Mistakes

### Using `git reset --hard` too early

This can delete local work. Use `git status`, `git diff`, and `git stash` first if you are unsure.

### Using reset on shared commits

Use `git revert` for commits that were pushed or shared.

### Thinking `restore --staged` deletes work

It only unstages the change. The file content remains.

---

## Before Continuing Checklist

- [ ] You can use the undo decision tree.
- [ ] You can unstage a file.
- [ ] You can discard an unstaged change.
- [ ] You understand the three reset modes.
- [ ] You know why `git revert` is safer for shared commits.
- [ ] You know that reflog can help find lost local commits.

---

## Lesson Summary

You learned how to choose the right undo command for unstaged changes, staged changes, local commits, shared commits, and lost local commits.

In the next lesson, you will connect your local repository to GitHub.
