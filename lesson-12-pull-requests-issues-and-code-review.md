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

Branch protection is a GitHub feature that helps teams protect important branches, especially branches like:

```text
main
master
release
```

These branches usually contain stable code that should always be in a working state.

Without protection, any developer with access could accidentally:

- Push broken code directly to `main`
- Delete important commits
- Skip code review
- Merge changes without testing

Branch protection adds rules that control how changes enter important branches.

---

# Why Do Teams Protect Branches?

In a professional development environment, the `main` branch represents the official version of the application.

The goal is:

> Keep the main branch stable, tested, and safe for everyone.

Instead of allowing developers to directly change `main`, teams usually follow this workflow:

```text
Developer

    |
    v

Create feature branch

    |
    v

Make changes

    |
    v

Create Pull Request

    |
    v

Review + Automated Checks

    |
    v

Merge into main
```

Branch protection helps enforce this process.

---

# Common Branch Protection Rules

## 1. Require Pull Requests Before Merging

This prevents developers from pushing directly to the protected branch.

Without protection:

```text
Developer
    |
    v
git push main
    |
    v
main changes immediately
```

With protection:

```text
Developer
    |
    v
Feature branch
    |
    v
Pull Request
    |
    v
Review
    |
    v
Merge into main
```

The team gets a chance to review the change before it becomes part of the main codebase.

---

# 2. Require Code Reviews

A team may require another developer to approve changes before merging.

Example:

```text
Developer creates Pull Request

        |
        v

Reviewer checks the code

        |
        v

Approved

        |
        v

Merge allowed
```

Code review helps teams:

- Find bugs
- Share knowledge
- Maintain coding standards
- Discuss better solutions

---

# 3. Require Passing Checks

Branch protection can require automated checks to pass before merging.

Examples:

- Unit tests
- Integration tests
- Build verification
- Code quality checks
- Security scans

Example:

```text
Pull Request Checks

✓ Build completed
✓ Unit tests passed
✓ Code formatting passed

Merge allowed
```

If a test fails:

```text
Pull Request Checks

✓ Build completed
✗ Unit tests failed

Merge blocked
```

The developer must fix the problem before merging.

---

# 4. Prevent Force Pushes

A force push can rewrite Git history.

Example:

Normal history:

```text
A --- B --- C
```

A force push could replace it with:

```text
A --- D
```

Commits `B` and `C` may disappear from the branch.

This can be dangerous on shared branches.

Branch protection can prevent force pushes to important branches like `main`.

---

# 5. Prevent Branch Deletion

Teams may also prevent accidental deletion of important branches.

For example:

```text
main
release
production
```

should usually always exist.

Deleting these branches could interrupt development or deployment processes.

---

# Example Protected Main Branch

A typical company might configure `main` like this:

```text
main branch protection rules:

✓ Require Pull Request before merging
✓ Require 2 approvals
✓ Require tests to pass
✓ Prevent force pushes
✓ Prevent branch deletion
```

Now every change follows the same safe process.

---

# Branch Protection and Collaboration

Branch protection creates a safety system around shared code.

Without protection:

```text
Anyone
   |
   v
Direct changes to main
   |
   v
Possible broken application
```

With protection:

```text
Developer
   |
   v
Feature branch
   |
   v
Pull Request
   |
   v
Review + Automated Checks
   |
   v
Protected main branch
```

The team can move quickly while reducing the risk of breaking the application.

---

# Beginner Understanding

For now, remember:

> Branch protection prevents important branches from being changed carelessly.

It does not stop developers from working.

Instead, it creates a controlled process where changes are:

- Reviewed
- Tested
- Approved
- Safely merged

---

# Branch Protection in Real Teams

In many companies:

- Developers never commit directly to `main`.
- Every change goes through a Pull Request.
- Automated tests run automatically.
- Reviewers approve changes.
- Only then can the code be merged.

This process is one of the foundations of professional software development workflows.

---

## 9. GitHub Actions Concept

GitHub Actions is a built-in automation platform inside GitHub.

It allows developers to create automated workflows that run whenever something happens in a repository.

For example:

- Someone pushes new code.
- Someone creates a Pull Request.
- A new release is created.
- A scheduled task needs to run.

GitHub Actions automatically starts the defined workflow.

---

## Why Do Teams Use GitHub Actions?

In a professional software team, developers do not manually check every change.

Instead, teams automate repetitive tasks.

GitHub Actions can automatically:

- Run automated tests
- Check code formatting
- Analyze code quality
- Build applications
- Package software
- Deploy applications
- Publish releases

Automation helps teams find problems earlier and reduces manual work.

---

## Example Workflow

Imagine a developer creates a Pull Request:

```text
Developer
    |
    v
Creates Pull Request
    |
    v
GitHub Actions starts automatically
    |
    +----------------+
    |                |
    v                v
Run Tests       Check Formatting
    |                |
    v                v
Passed          Passed
    |
    v
Pull Request can be reviewed
```

Before merging the Pull Request, the team can see whether the automated checks passed.

---

# GitHub Actions in a Pull Request

When a Pull Request is opened, GitHub can display automated checks.

Example:

```text
Pull Request

✓ Build application
✓ Run unit tests
✓ Check code style

All checks passed
```

or:

```text
Pull Request

✓ Build application
✗ Run unit tests

Some checks failed
```

A failed check does not necessarily mean Git is broken.

It means that one of the automated rules defined by the team found a problem.

---

# What Is a Workflow?

A GitHub Actions workflow is a file that describes:

- When automation should run
- What tasks should be performed
- Which environment should execute the tasks

Workflows are stored inside the repository:

```text
.github/
   workflows/
       build.yml
       tests.yml
```

The workflow files use YAML format.

Example:

```yaml
name: Run Tests

on:
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run tests
        run: npm test
```

You do not need to create workflows yet, but it is important to understand the concept.

---

# Important GitHub Actions Terms

## Workflow

A complete automation process.

Example:

"Run all tests when someone creates a Pull Request."

---

## Event

Something that triggers a workflow.

Examples:

```text
push
pull_request
schedule
release
```

Example:

```yaml
on:
  pull_request:
```

Means:

"Run this workflow whenever a Pull Request is created or updated."

---

## Job

A group of related tasks.

Example:

```text
Test Application

- Install dependencies
- Run tests
- Generate report
```

A workflow can contain multiple jobs.

---

## Step

A single task inside a job.

Example:

```text
Step 1:
Checkout the code

Step 2:
Install dependencies

Step 3:
Run tests
```

---

# GitHub Actions and Quality Gates

Many teams use GitHub Actions as a **quality gate**.

A quality gate means:

> Code must pass certain automated checks before it can be merged.

Example rules:

A Pull Request cannot merge unless:

✓ All automated tests pass  
✓ Code builds successfully  
✓ No critical issues are found  

This helps protect the main branch from broken code.

---

# Example From a Real Development Team

A developer changes a login feature.

They create a Pull Request.

GitHub Actions automatically:

1. Downloads the code.
2. Installs dependencies.
3. Runs automated tests.
4. Checks code quality.
5. Reports the result.

If everything passes:

```text
✓ All checks passed
```

The team can review and merge.

If something fails:

```text
✗ Tests failed
```

The developer investigates and fixes the problem before merging.

---

# Beginner Understanding

For now, remember:

> GitHub Actions is a way to make GitHub automatically perform tasks for you.

A passing GitHub Actions check means:

> "The automated rules configured by the team have passed."

It does **not** guarantee the software is perfect, but it gives the team confidence that important checks were completed.

---

# GitHub Actions in the Development Workflow

A typical workflow looks like this:

```text
Developer writes code
          |
          v
Creates commit
          |
          v
Pushes to GitHub
          |
          v
Creates Pull Request
          |
          v
GitHub Actions runs automatically
          |
          v
Tests and checks complete
          |
          v
Code review
          |
          v
Merge into main branch
```

GitHub Actions is one of the foundations of modern Continuous Integration (CI) practices.

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
