# Lesson 12 - Pull Requests, Issues, and Code Review

**Audience / Level:** Beginners learning GitHub collaboration tools

**Duration:** 60-75 minutes

**Prerequisites:** Lesson 11 - Fetching, Pulling, and Synchronization

---

## Learning Objectives

By the end of this lesson, you will be able to:

- Explain what GitHub Issues are used for.
- Create a feature branch for a GitHub task.
- Open a Pull Request.
- Write a useful PR title and description.
- Understand basic code review.
- Respond to review feedback.
- Update a PR after review.
- Explain basic branch protection.
- Explain basic GitHub Actions.
- Recognize forks as optional for open-source contribution.

---

## 1. Issues

Issues are GitHub items used to track work.

Examples:

- Bug: Login button does not work.
- Feature: Add dark mode.
- Task: Update README instructions.

A good beginner issue includes:

- A clear title
- What needs to change
- Why it matters
- Any useful notes or examples

---

## 2. Feature Branches on GitHub

Team work usually does not happen directly on `main`.

Instead:

1. Create an issue.
2. Create a branch for the issue.
3. Commit the change.
4. Push the branch.
5. Open a Pull Request.

Example branch:

```bash
git switch main
git pull
git switch -c docs/update-readme
```

---

## 3. Pull Requests

A Pull Request, often called a PR, asks:

> Please review these changes before they are merged.

A PR lets the team:

- Discuss the change
- Review the files
- Request improvements
- Run automated checks
- Merge when ready

---

## 4. Good PR Titles and Descriptions

Good title:

```text
Update README setup instructions
```

Weak title:

```text
changes
```

Good description:

```text
Updates the README with clearer setup steps for beginners.

Closes #1
```

Include:

- What changed
- Why it changed
- How you checked it
- Related issue number, if any

---

## 5. Code Review Basics

Reviewers look for:

- Clear code or documentation
- Correct behavior
- Missing steps
- Possible mistakes
- Consistency with the project

Review is not about blame. It is a normal quality step.

---

## 6. Reviewer Etiquette

Good review comments are:

- Specific
- Respectful
- Focused on the work
- Clear about what should change

Useful comment:

```text
Could we add one example command here so beginners can follow the step?
```

Less useful comment:

```text
This is bad.
```

---

## 7. Updating a PR After Review

After review feedback:

1. Edit files locally.
2. Commit the update on the same branch.
3. Push again.

Example:

```bash
git switch docs/update-readme
echo "Extra setup note" >> README.md
git add README.md
git commit -m "Clarify README setup step"
git push
```

The existing PR updates automatically.

---

## 8. Branch Protection Concept

Branch protection helps teams protect important branches like `main`.

Rules may require:

- Pull Requests before merging
- One or more reviews
- Passing checks
- No force pushes

You do not need to configure every rule now. Understand the purpose:

> Important branches should not be changed carelessly.

---

## 9. GitHub Actions Concept

GitHub Actions is automation on GitHub.

Common uses:

- Run tests
- Check formatting
- Build the project
- Deploy software

In a PR, Actions may show checks as passed or failed.

Beginner idea:

> A passing check is a signal that the change meets an automated quality rule.

---

## Optional: Forks

A fork is your own GitHub copy of someone else's repository.

Forks are common in open-source contribution.

For most team projects in this beginner course, you can work with branches in the main shared repository instead.

---

## Hands-On Exercises

### Exercise 1 - Complete a PR Workflow

Use your `git-training-demo` GitHub repository.

### Step 1 - Create an Issue

On GitHub, create an issue:

```text
Title: Improve README course description
```

Add a short description of the requested documentation change.

### Step 2 - Create a Branch

Locally:

```bash
git switch main
git pull
git switch -c docs/improve-readme-description
```

### Step 3 - Commit a Documentation Change

```bash
echo "This repository is used for hands-on Git and GitHub practice." >> README.md
git diff
git add README.md
git commit -m "Improve README course description"
```

### Step 4 - Push the Branch

```bash
git push -u origin docs/improve-readme-description
```

### Step 5 - Open a Pull Request

On GitHub:

1. Open a Pull Request from your branch into `main`.
2. Use a clear title.
3. Describe the change.
4. Link the issue using `Closes #issue-number`.

### Step 6 - Add a Review Comment

If working with a partner, ask them to add one review comment.

If you are completing this course alone, you can simulate the reviewer role yourself by adding a comment to your own Pull Request or by writing down what a reviewer would ask you to change.

### Step 7 - Update the PR

Make one more local change:

```bash
echo "Students will practice local commits, branches, remotes, and Pull Requests." >> README.md
git add README.md
git commit -m "Clarify README practice topics"
git push
```

The PR updates automatically.

### Step 8 - Merge the PR

After review and checks, merge the PR on GitHub.

Then update local `main`:

```bash
git switch main
git pull
```

---

## Commands Learned in This Lesson

```bash
git switch main
git pull
git switch -c branch-name
git diff
git add filename
git commit -m "Message"
git push -u origin branch-name
git push
```

---

## Common Beginner Mistakes

### Opening a PR from the wrong branch

Check the source branch and target branch on GitHub before creating the PR.

### Creating a new branch after making the commit on `main`

Check your branch before editing:

```bash
git branch --show-current
```

### Thinking a PR is only for code

PRs are also useful for documentation, configuration, and small text changes.

---

## Before Continuing Checklist

- [ ] You can create an Issue.
- [ ] You can create a feature branch.
- [ ] You can push a branch to GitHub.
- [ ] You can open a Pull Request.
- [ ] You can update a PR with another commit.
- [ ] You understand basic review etiquette.
- [ ] You understand branch protection and GitHub Actions at a basic level.

---

## Lesson Summary

You learned how Issues, feature branches, Pull Requests, reviews, branch protection, and GitHub Actions fit together in a beginner collaboration workflow.

In the next lesson, you will put the whole course together in a final collaboration practice.
