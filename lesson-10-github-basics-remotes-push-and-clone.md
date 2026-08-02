# Lesson 10 - GitHub Basics: Remotes, Push, and Clone

**Audience / Level:** Beginners connecting local Git repositories to GitHub

**Duration:** 45-60 minutes

**Prerequisites:** Lesson 09 - Undoing Changes Safely

---

## Learning Objectives

By the end of this lesson, you will be able to:

- Explain the Git vs GitHub difference again.
- Create a repository on GitHub.
- Explain what a remote is.
- Explain why the default remote is usually named `origin`.
- View remotes with `git remote -v`.
- Add a remote with `git remote add origin`.
- Rename the main branch with `git branch -M main`.
- Push with `git push -u origin main`.
- Push later commits with `git push`.
- Clone a repository with `git clone`.

---

## 1. Git and GitHub Reminder

Git tracks history on your computer.

GitHub stores Git repositories online and adds collaboration tools.

In this lesson, you will connect:

```text
Local repository on your computer
        |
        | git push
        v
Repository on GitHub
```

---

## 2. Create a GitHub Repository

On GitHub:

1. Sign in.
2. Create a new repository.
3. Name it:

```text
git-training-demo
```

4. Choose public or private.
5. Do not add a README, `.gitignore`, or license on GitHub if your local repository already has files.
6. Create the repository.

GitHub will show a repository URL. Keep it available.

---

## 3. What Is a Remote?

A remote is a saved connection to another Git repository.

Most often, the remote points to GitHub.

The default remote name is commonly:

```text
origin
```

`origin` is not a special command. It is just a nickname.

---

## 4. Connect Your Local Repository

Open your local course repository:

```bash
cd git-training-demo
```

Check history:

```bash
git log --oneline
```

Make sure the branch is named `main`:

```bash
git branch -M main
```

Add the GitHub remote.

HTTPS example:

```bash
git remote add origin https://github.com/<username>/git-training-demo.git
```

SSH example:

```bash
git remote add origin git@github.com:<username>/git-training-demo.git
```

Check it:

```bash
git remote -v
```

---

## 5. GitHub Authentication on First Push

When you push to GitHub for the first time, GitHub needs to confirm who you are.

GitHub account passwords do not work as Git passwords.

On Windows with Git Bash, Git Credential Manager usually opens a browser window or sign-in prompt. Sign in with your GitHub account and allow Git to continue.

After this, Git usually remembers the login.

If browser authentication does not work, common alternatives are HTTPS with a Personal Access Token or SSH with an SSH key.

For this beginner course, you only need to understand that a credential prompt or browser sign-in is expected.

---

## 6. Push the First Time

Run:

```bash
git push -u origin main
```

On your first push, a browser window or credential prompt may appear. This is normal. Sign in to GitHub to continue.

Meaning:

- `push` sends commits to GitHub.
- `origin` is the remote nickname.
- `main` is the branch.
- `-u` sets up tracking so future pushes and pulls are simpler.

After this, refresh the GitHub page. Your files should appear online.

---

## 7. Push Later Commits

After the first push, make another small change:

```bash
echo "GitHub remote practice" >> README.md
git add README.md
git commit -m "Update README after GitHub setup"
git push
```

Because tracking is set, plain `git push` knows where to send the current branch.

---

## 8. Clone a Repository

Clone means download a repository and its history to your computer.

Move outside your existing project folder:

```bash
cd ..
```

Clone into a separate folder:

```bash
git clone https://github.com/<username>/git-training-demo.git git-training-demo-clone
```

or with SSH:

```bash
git clone git@github.com:<username>/git-training-demo.git git-training-demo-clone
```

Go into the clone:

```bash
cd git-training-demo-clone
git log --oneline
git remote -v
```

Cloning automatically creates the `origin` remote.

Return to the main course project when finished:

```bash
cd ../git-training-demo
```

---

## Hands-On Exercises

### Exercise 1 - Push the Course Repository

If you already added `origin` and pushed during the main walkthrough, do not add `origin` again.

Verify your setup:

```bash
cd git-training-demo
git remote -v
git branch --show-current
git status
git push
```

If this is your first time connecting the repository, use the commands from sections 4 and 5.

Expected result: Your local commits appear on GitHub, and `git push` works after upstream tracking is set.

### Exercise 2 - Make and Push Another Commit

```bash
echo "Another GitHub practice line" >> README.md
git add README.md
git commit -m "Add GitHub practice note"
git push
```

Expected result: GitHub shows the new commit after refreshing the page.

### Exercise 3 - Clone Your Repository

```bash
cd ..
git clone https://github.com/<username>/git-training-demo.git git-training-demo-clone
cd git-training-demo-clone
git remote -v
git log --oneline
```

---

## Commands Learned in This Lesson

```bash
git remote -v
git remote add origin <repository-url>
git branch -M main
git push -u origin main
git push
git clone <repository-url>
```

---

## Common Beginner Mistakes

### I committed but do not see the change on GitHub

Commit saves locally. Push uploads to GitHub.

### I added a README on GitHub and also have a local README

This can create different histories. For this lesson, create an empty GitHub repository when pushing an existing local project.

### `remote origin already exists`

Check:

```bash
git remote -v
```

If the URL is wrong, an instructor may help you run:

```bash
git remote set-url origin <correct-url>
```

---

## Before Continuing Checklist

- [ ] You have a GitHub repository named `git-training-demo`.
- [ ] Your local repository has an `origin` remote.
- [ ] `git remote -v` shows the correct GitHub URL.
- [ ] `git push -u origin main` worked.
- [ ] You can push later commits with `git push`.
- [ ] You have cloned a repository into a separate folder.

---

## Lesson Summary

You connected local Git to GitHub, added a remote, pushed commits, and cloned a repository.

In the next lesson, you will learn how to fetch, pull, and keep local and remote repositories synchronized.
