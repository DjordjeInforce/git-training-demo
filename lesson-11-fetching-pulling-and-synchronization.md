# Lesson 11 — Fetching, Pulling, and Synchronization

**Audience / Level:** Beginners learning how local and remote repositories stay synchronized

**Duration:** 35–55 minutes

**Prerequisites:** Lesson 10 — GitHub Basics: Remotes, Push, and Clone

---

# Learning Objectives

By the end of this lesson, you will be able to:

- Explain the difference between a local and a remote repository.
- Use `git fetch` to safely download information from a remote repository.
- Use `git pull` to download and apply remote changes.
- Explain the difference between `git fetch` and `git pull`.
- Understand what `origin` and tracking branches are.
- View tracking branch information with `git branch -vv`.
- Understand why pull conflicts occur and how they are resolved.

---

# 1. Local vs. Remote Repositories

So far, almost everything we've done has happened inside our **local repository**—the Git repository stored on our own computer.

However, in real software development, your code usually lives in **two places**:

- **Your local repository** (on your computer)
- **A remote repository** (usually on GitHub)

```text
        Your Computer                     GitHub

    Local Repository   <------------->   Remote Repository
```

Think of your local repository as your personal workspace, where you write code, create commits, and experiment safely.

The remote repository acts as the team's shared copy. It allows multiple developers to collaborate, share changes, and keep everyone's work synchronized.

One of the most important concepts to understand is this:

> **Git does not automatically synchronize your local repository with GitHub.**

Nothing happens unless **you tell Git to do it**.

You decide when to:

- Send your commits to GitHub using `git push`
- Check whether GitHub has new commits using `git fetch`
- Download and apply those commits using `git pull`

---

## Example

Imagine the following situation.

Your computer contains:

```text
A --- B
```

GitHub also contains:

```text
A --- B
```

Everything is synchronized.

Later, another developer pushes a new commit.

GitHub now contains:

```text
A --- B --- C
```

But your computer still contains:

```text
A --- B
```

Your repository is now **behind** the remote repository.

Nothing has changed on your computer yet because Git **never updates your files automatically**.

You must decide whether to:

- inspect the changes (`git fetch`)
- or immediately update your branch (`git pull`)

---

# 2. Understanding `git fetch`

`git fetch` downloads new information from the remote repository **without changing your current branch or working directory**.

This is one of the safest Git commands because it never modifies your files.

Run:

```bash
git fetch
```

What happens?

Git contacts GitHub and downloads:

- new commits
- updated branch pointers
- tags
- other repository metadata

However, **your current branch stays exactly the same.**

---

## Visual Example

Before fetching:

Local:

```text
A --- B
```

Remote:

```text
A --- B --- C
```

After running:

```bash
git fetch
```

Your local branch is still:

```text
A --- B
```

But Git has now downloaded information about commit **C**.

Internally, Git updates a special branch called:

```text
origin/main
```

Notice:

- Your files did **not** change.
- Your branch did **not** move.
- Git simply learned that GitHub has a newer commit.

This lets you inspect everything before deciding whether to update your branch.

---

## Inspecting the Downloaded Changes

You can view your commit history.

```bash
git log --oneline
```

Or compare your current branch with the remote branch.

```bash
git diff HEAD..origin/main
```

This command asks Git:

> "Show me everything that exists on GitHub but not in my current branch."

This is why many experienced developers prefer using `git fetch` first.

They want to inspect changes before applying them.

---

# 3. Understanding `git pull`

While `git fetch` only downloads information, **`git pull` downloads the changes and immediately applies them to your current branch.**

Run:

```bash
git pull
```

Or specify the remote and branch explicitly:

```bash
git pull origin main
```

A beginner-friendly definition is:

```text
git pull = git fetch + integrate the downloaded changes
```

Most of the time, Git integrates those changes using a **merge**.

---

## Visual Example

Before pulling:

Local:

```text
A --- B
```

Remote:

```text
A --- B --- C
```

After:

```bash
git pull
```

Your local repository becomes:

```text
A --- B --- C
```

Your files are updated automatically to match GitHub.

---

## What Actually Happens?

When you run:

```bash
git pull
```

Git performs two operations:

1. Fetches the newest commits from GitHub.
2. Integrates those commits into your current branch.

In most beginner scenarios, this happens automatically because there are no conflicting changes.

---

# 4. Fetch vs. Pull

Many beginners confuse these commands because both contact GitHub.

The important difference is **whether your files change**.

| Command | Downloads remote changes | Updates your files? | Typical use |
|----------|--------------------------|---------------------|-------------|
| `git fetch` | Yes | No | Inspect first |
| `git pull` | Yes | Usually Yes | Update immediately |

Think of them like this:

### `git fetch`

> "Show me what's new."

### `git pull`

> "Bring me up to date."

---

# 5. Origin and Tracking Branches

When you cloned your repository earlier, Git automatically created a remote named:

```text
origin
```

`origin` is simply a nickname for your GitHub repository.

It is **not** a Git command.

View your remotes:

```bash
git remote -v
```

Example:

```text
origin  https://github.com/username/git-training-demo.git (fetch)
origin  https://github.com/username/git-training-demo.git (push)
```

# 6. Common Synchronization Situations

Let's look at the three situations you'll encounter most often.

---

## Situation 1 — The Remote Repository Has New Commits

Your local repository:

```text
A --- B
```

GitHub:

```text
A --- B --- C
```

The remote repository is **ahead**.

Your branch is **behind**.

To update your branch:

```bash
git pull
```

---

## Situation 2 — Your Local Repository Has New Commits

Local:

```text
A --- B --- C
```

Remote:

```text
A --- B
```

Your branch is **ahead**.

GitHub doesn't have your latest commit yet.

Upload it with:

```bash
git push
```

---

## Situation 3 — Both Local and Remote Changed

This is where many beginners first encounter merge conflicts.

Initially, both repositories are synchronized:

```text
A --- B
```

You create a new commit locally:

```text
Local

A --- B --- C
```

Before you push, another developer creates a different commit on GitHub:

```text
Remote

A --- B --- D
```

If we combine those histories, we get:

```text
        C (your commit)
       /
A --- B
       \
        D (remote commit)
```

Git now sees **two different histories**.

Neither commit contains the other.

Git cannot simply move one branch forward because doing so would lose someone else's work.

Instead, Git must combine both histories.

### Why Can't Git Just Push Your Commit?

Suppose GitHub currently looks like this:

```text
A --- B --- D
```

Your local repository looks like this:

```text
A --- B --- C
```

If Git simply replaced the remote history with yours, the repository would become:

```text
A --- B --- C
```

Commit `D` would disappear.

That means another developer's work would be lost.

To prevent this, Git rejects your push and asks you to first synchronize with the remote repository.

---

## Merge Example

When both you and another developer create new commits, Git has two separate lines of history.

Before the merge, the history looks like this:

```text
        C (your commit)
       /
A --- B
       \
        D (remote commit)
```

Both commits started from the same commit (`B`), but they contain different work.

- Commit **C** contains **your changes**.
- Commit **D** contains **the other developer's changes**.

Neither commit contains the other, so Git cannot simply move one branch forward.

Instead, Git creates a **new commit** called a **merge commit**.

After the merge:

```text
        C
       / \
A --- B   M
       \ /
        D
```

The merge commit `M` has **two parent commits**:

- One parent points to your commit (`C`).
- The other parent points to the remote commit (`D`).

Think of the merge commit as saying:

> "I combine everything from both branches."

Unlike a normal commit, which has **one parent**, a merge commit has **two parents** because it represents the point where two separate histories come back together.

The resulting history now contains **both developers' work**:

```text
A --- B --- C  (your work)
       \     \
        D ----M (combined history)
```

Nothing is overwritten or deleted.

- Your commit (`C`) is still part of the project's history.
- The remote commit (`D`) is still part of the project's history.
- The merge commit (`M`) simply joins them together into a single timeline so everyone can continue working from the same point.

After the merge, any new commits are created from `M`:

```text
        C
       / \
A --- B   M --- E
       \ /
        D
```

Now both developers are working from the same shared history again.

---

## Rebase Example

A merge isn't the only way Git can combine two lines of history.

Another option is **rebase**.

Instead of creating a merge commit, Git **moves your commits so they appear as if they were created after the latest remote commits**.

Before rebasing, the history looks like this:

```text
        C (your commit)
       /
A --- B
       \
        D (remote commit)
```

Both you and another developer started from commit `B`, but each created a different commit.

With a merge, Git would keep both branches and create a new merge commit.

With a rebase, Git takes a different approach.

### Step 1 — Temporarily Remove Your Commits

Git temporarily removes your local commit (`C`).

Your branch now looks like this:

```text
A --- B
       \
        D
```

Your work isn't deleted—Git simply stores it temporarily while it updates your branch.

---

### Step 2 — Move to the Latest Remote Commit

Git updates your branch so it points to the latest remote commit (`D`).

Your branch is now up to date with the remote repository.

---

### Step 3 — Replay Your Work

Finally, Git reapplies your changes on top of commit `D`.

The history becomes:

```text
A --- B --- D --- C'
```

Notice that the commit is now called **`C'` (C prime)** instead of `C`.

This is because Git actually creates a **new commit**.

Even though the code changes are the same, the commit has:

- a different parent commit
- a different commit ID (SHA)
- a different position in the history

The original commit `C` is replaced by the new commit `C'`.

---

### Why Do Developers Use Rebase?

One advantage of rebasing is that the project history becomes a straight line.

Instead of:

```text
        C
       /
A --- B
       \
        D
```

or

```text
        C
       / \
A --- B   M
       \ /
        D
```

you get:

```text
A --- B --- D --- C'
```

This linear history is often easier to read because it looks like everyone committed one after another, even though the work happened at the same time.

---

### Merge vs. Rebase

Both approaches preserve everyone's work.

The difference is **how the history looks**.

**Merge:**

```text
        C
       / \
A --- B   M
       \ /
        D
```

- Keeps the true history of what happened.
- Creates a merge commit.
- History shows where branches split and rejoined.

**Rebase:**

```text
A --- B --- D --- C'
```

- Rewrites your local commits.
- Does not create a merge commit.
- Produces a cleaner, linear history.

Both approaches include the same code changes. The difference is only in how Git records the project's history.

---

# Hands-On Exercises

## Exercise 1 — Fetch and Inspect

1. Edit `README.md` directly on GitHub and commit the change.
2. In your local repository, run:

```bash
git fetch
git log --oneline --graph --decorate --all
git diff HEAD..origin/main
```

**Expected Result:** You can see the remote changes without modifying your local files.

---

## Exercise 2 — Pull the Remote Change

```bash
git pull
git log --oneline
```

**Expected Result:** Your local repository is updated with the changes from GitHub.

---

## Exercise 3 — View Tracking Branches

```bash
git remote -v
git branch -vv
```

**Expected Result:** You can identify the `origin` remote and the remote branch your local branch tracks.

---

# Commands Learned in This Lesson

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

# Common Beginner Mistakes

## Expecting GitHub changes to appear automatically

Git never synchronizes automatically.

Run:

```bash
git fetch
```

or

```bash
git pull
```

---

## Confusing Fetch and Pull

Remember:

- **Fetch** downloads information.
- **Pull** downloads and applies changes.

---

## Thinking `origin` is a Git command

It isn't.

`origin` is simply the default nickname for your remote repository.

---

# Before Continuing Checklist

- [ ] I understand the difference between a local and remote repository.
- [ ] I can explain what `git fetch` does.
- [ ] I can use `git pull` to update my branch.
- [ ] I understand why `git fetch` is safer when inspecting changes.
- [ ] I know what a tracking branch is.
- [ ] I understand why merge conflicts happen after a pull.

---

# Lesson Summary

In this lesson, you learned how Git keeps local and remote repositories synchronized.

You learned that:

- Git never synchronizes repositories automatically.
- `git fetch` safely downloads information without changing your files.
- `git pull` downloads and applies remote changes.
- Tracking branches allow Git to know where to push and pull.
- Diverging histories occur when both local and remote repositories receive new commits.
- Git combines those histories through either a merge or a rebase.
- Merge conflicts occur only when Git cannot safely combine changes automatically.

These concepts form the foundation of collaborating with other developers and prepare you for the next lesson on **Pull Requests, Issues, and Code Reviews**.