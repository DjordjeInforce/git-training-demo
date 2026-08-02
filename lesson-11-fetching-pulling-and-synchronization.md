# Lesson 11 - Fetching, Pulling, and Synchronization

**Audience / Level:** Beginners learning how local and remote repositories stay synchronized

**Duration:** 35-55 minutes

**Prerequisites:** Lesson 10 - GitHub Basics: Remotes, Push, and Clone

---

## Learning Objectives

By the end of this lesson, you will be able to:

- Explain local and remote repositories.
- Use `git fetch` to download remote information safely.
- Use `git pull` to download and apply remote changes.
- Explain the difference between fetch and pull.
- Explain `origin` and tracking branches.
- Use `git branch -vv`.
- Handle a simple pull conflict.
- Recognize upstream and fork workflows as optional.

---

## 1. Local vs Remote Repositories

Your local repository is on your computer.

The remote repository is usually on GitHub.

```text
Your computer                    GitHub
Local repository  <----------->  Remote repository
```

Git does not automatically synchronize them.

You choose when to:

- Send commits with `git push`
- Check remote updates with `git fetch`
- Download and apply updates with `git pull`

---

## 2. `git fetch`

`git fetch` downloads new information from the remote repository but does not change your current files.

Run:

```bash
git fetch
```

Then inspect:

```bash
git log --oneline --graph --decorate --all
```

Compare your current branch with the remote version:

```bash
git diff HEAD..origin/main
```

Fetch is safer when you want to inspect remote changes before applying them.

---

## 3. `git pull`

`git pull` downloads remote changes and applies them to your current branch.

Run:

```bash
git pull
```

Or specify the remote and branch:

```bash
git pull origin main
```

Beginner meaning:

```text
git pull = git fetch + apply the remote changes
```

Often Git applies the changes through a merge.

---

## 4. Fetch vs Pull

| Command | What it does | Changes your current files? | Beginner use |
| --- | --- | --- | --- |
| `git fetch` | Downloads remote information | No | Inspect first |
| `git pull` | Downloads and applies changes | Usually yes | Update when ready |

Use `git fetch` when you want to look before changing your branch.

Use `git pull` when you are ready to update your branch.

---

## 5. Origin and Tracking Branches

`origin` is usually the nickname for the GitHub repository.

View remotes:

```bash
git remote -v
```

A tracking branch connects a local branch to a remote branch.

View tracking information:

```bash
git branch -vv
```

Example:

```text
* main a123abc [origin/main] Update README
```

This means local `main` tracks `origin/main`.

Tracking lets plain `git push` and `git pull` know which remote branch to use.

---

## 6. Common Synchronization Situations

### Remote has new commits

```text
Local:  A---B
Remote: A---B---C
```

Your branch is behind. Use:

```bash
git pull
```

### Local has new commits

```text
Local:  A---B---C
Remote: A---B
```

Your branch is ahead. Use:

```bash
git push
```

### Both local and remote changed

```text
        C local
       /
A---B
       \
        D remote
```

Git must combine changes. Sometimes this creates a conflict.

---

## 7. Simple Pull Conflicts

A pull conflict looks like a merge conflict because pull often includes a merge.

This lesson explains what pull conflicts look like. The hands-on exercise uses a safer conflict-free workflow first. You will practice conflict resolution in controlled exercises elsewhere in the course.

Conflict markers:

```text
<<<<<<< HEAD
Your local version
=======
Remote version
>>>>>>> origin/main
```

Resolve it:

```bash
git status
```

Open the file, edit the final content, remove markers, then run:

```bash
git add filename
git commit
```

Cancel the merge part of a pull:

```bash
git merge --abort
```

---

## Optional: Upstream and Forks

In fork workflows, `origin` often points to your fork and `upstream` points to the original project.

Example:

```bash
git remote add upstream https://github.com/original-owner/project.git
git fetch upstream
```

This is useful for open-source contribution, but it is optional for the main beginner path.

---

## Hands-On Exercises

### Exercise 1 - Fetch and Inspect

Use your GitHub repository.

1. Edit `README.md` directly on GitHub and commit the change there.
2. In your local `git-training-demo`, run:

```bash
git fetch
git log --oneline --graph --decorate --all
git diff HEAD..origin/main
```

Expected result: You can see the remote change before applying it.

### Exercise 2 - Pull the Remote Change

```bash
git pull
git log --oneline --graph --decorate --all
```

Expected result: Your local files include the GitHub change.

### Exercise 3 - View Tracking

```bash
git remote -v
git branch -vv
```

Expected result: You can identify `origin` and the remote branch your local branch tracks.

---

## Commands Learned in This Lesson

```bash
git fetch
git pull
git pull origin main
git diff HEAD..origin/main
git branch -vv
git remote -v
git merge --abort
```

---

## Common Beginner Mistakes

### Expecting GitHub edits to appear locally automatically

Run `git fetch` or `git pull`.

### Confusing fetch and pull

Fetch downloads information. Pull downloads and applies changes.

### Thinking `origin` is a command

`origin` is a remote nickname.

---

## Before Continuing Checklist

- [ ] You can explain local vs remote repositories.
- [ ] You can use `git fetch`.
- [ ] You can use `git pull`.
- [ ] You understand why fetch is safer for inspection.
- [ ] You can view tracking branches with `git branch -vv`.
- [ ] You know that pull conflicts are resolved like merge conflicts.

---

## Lesson Summary

You learned how local and remote repositories synchronize, why fetch is safer for inspection, how pull applies changes, and how tracking branches help Git know where to push and pull.

In the next lesson, you will learn Pull Requests, Issues, and code review.
