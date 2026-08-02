# Lesson 13 — Final Git and GitHub Collaboration Project

**Audience / Level:** Beginners completing a practical Git and GitHub workflow

**Duration:** 60–90 Minutes

**Prerequisites:** Lessons 0–12

---

# Learning Objectives

By the end of this lesson, you will be able to:

- Complete a full Git and GitHub collaboration workflow.
- Create a task using GitHub Issues.
- Create a feature branch from `main`.
- Make and commit changes locally.
- Push a branch to GitHub.
- Create and update a Pull Request.
- Understand the review and feedback process.
- Merge changes into `main`.
- Synchronize your local repository after merging.
- Apply basic Git collaboration best practices.

---

# 1. Final Project Overview

Throughout this course, you learned how developers use Git and GitHub to manage changes and collaborate.

In this final lesson, you will combine everything into one realistic workflow.

You will simulate working as a developer on a team.

The workflow:

```text
GitHub Issue
      |
      v
Create Feature Branch
      |
      v
Make Changes Locally
      |
      v
Commit Changes
      |
      v
Push Branch to GitHub
      |
      v
Create Pull Request
      |
      v
Review Changes
      |
      v
Update Pull Request
      |
      v
Merge Into main
      |
      v
Synchronize Local Repository
```

This is the same general workflow used by many software development teams.

---

# 2. Project Scenario

Imagine you joined a development team.

Your team lead creates a task:

```text
Improve the project documentation for new developers.
```

Your responsibility is to:

- Update the README file.
- Add useful setup information.
- Submit your changes for review.

The team does not want changes directly on `main`.

Instead, you will:

1. Create a branch.
2. Make your changes.
3. Open a Pull Request.
4. Review and merge your work.

---

# 3. Step 1 — Create a GitHub Issue

Open your GitHub repository.

Create a new Issue.

Example:

## Title

```text
Improve README setup instructions
```

## Description

```text
Add clearer setup instructions for developers who are new to the project.

Include:
- Required tools
- Installation steps
- Basic Git commands
```

The Issue represents the work that needs to be completed.

---

# 4. Step 2 — Update Your Local Repository

Before starting new work, make sure your local repository is up to date.

Check your current branch:

```bash
git branch
```

Switch to `main`:

```bash
git switch main
```

Download the latest changes:

```bash
git pull
```

Your local `main` should now match GitHub.

---

# 5. Step 3 — Create a Feature Branch

Create a branch for the Issue.

Example:

```bash
git switch -c docs/improve-readme
```

Verify your branch:

```bash
git branch
```

Expected:

```text
* docs/improve-readme
  main
```

Your work will now happen safely away from `main`.

---

# 6. Step 4 — Make Changes

Open your README file.

Add a new section:

```text
## Developer Setup

Install Git.

Clone the repository.

Create a feature branch before making changes.
```

Save the file.

Check your changes:

```bash
git status
```

View the difference:

```bash
git diff
```

---

# 7. Step 5 — Commit Your Work

Stage the file:

```bash
git add README.md
```

Create a commit:

```bash
git commit -m "Improve README setup instructions"
```

Check your history:

```bash
git log --oneline
```

A good commit message explains what changed.

Example:

Good:

```text
Improve README setup instructions
```

Bad:

```text
changes
```

---

# 8. Step 6 — Push Your Branch to GitHub

Push the new branch:

```bash
git push -u origin docs/improve-readme
```

The `-u` option connects your local branch with the remote branch.

After this, Git remembers the relationship.

Future pushes can simply use:

```bash
git push
```

---

# 9. Step 7 — Create a Pull Request

Go to GitHub.

Create a Pull Request.

Select:

```text
base:
main

compare:
docs/improve-readme
```

---

## Pull Request Title

Example:

```text
Improve README setup instructions
```

---

## Pull Request Description

Example:

```text
This PR improves the README documentation for new developers.

Changes:
- Added setup instructions
- Added basic Git workflow information

Closes #1
```

The description should explain:

- What changed
- Why it changed
- Any related Issue

---

# 10. Step 8 — Review the Pull Request

A reviewer checks:

- Is the change correct?
- Is the documentation clear?
- Does anything need improvement?

Example review comment:

```text
Could we add one example Git command for creating a branch?
```

Review comments are not criticism.

They are part of improving the quality of the project.

---

# 11. Step 9 — Update the Pull Request

Make the requested change locally.

Example:

```bash
echo "git switch -c feature-name" >> README.md
```

Check the change:

```bash
git diff
```

Commit:

```bash
git add README.md

git commit -m "Add branch creation example"
```

Push:

```bash
git push
```

The Pull Request updates automatically.

You do not create a new PR.

---

# 12. Step 10 — Merge the Pull Request

After the review is complete:

The team verifies:

- The changes are correct.
- The Pull Request description is clear.
- All checks pass.
- No conflicts exist.

Merge the Pull Request on GitHub.

After merging:

```text
main
 |
 v
A---B---C
        ^
        |
    your changes
```

Your work is now part of the main project.

---

# 13. Step 11 — Synchronize Your Local Repository

Your local repository does not automatically know about the merge.

Update it:

```bash
git switch main
```

Pull the latest changes:

```bash
git pull
```

Now your local `main` contains the merged changes.

---

# 14. Step 12 — Clean Up the Branch

After the merge, the feature branch is no longer needed.

Delete it locally:

```bash
git branch -d docs/improve-readme
```

Confirm:

```bash
git branch
```

Your repository should now be clean.

---

# 15. Final Workflow Review

You completed:

```text
Issue
 |
 v
Feature Branch
 |
 v
Local Changes
 |
 v
Commit
 |
 v
Push
 |
 v
Pull Request
 |
 v
Review
 |
 v
Update
 |
 v
Merge
 |
 v
Pull Latest main
 |
 v
Delete Branch
```

This is the foundation of professional GitHub collaboration.

---

# Final Assessment Checklist

Before completing the course, confirm that you can:

- [ ] Create a GitHub Issue.
- [ ] Create a feature branch.
- [ ] Make changes locally.
- [ ] Use `git status`.
- [ ] Use `git diff`.
- [ ] Create meaningful commits.
- [ ] Push a branch to GitHub.
- [ ] Create a Pull Request.
- [ ] Understand review feedback.
- [ ] Update an existing Pull Request.
- [ ] Merge changes.
- [ ] Update local `main`.
- [ ] Delete completed branches.

---

# Commands Practiced in This Lesson

```bash
git branch

git switch main

git pull

git switch -c branch-name

git status

git diff

git add filename

git commit -m "Message"

git push -u origin branch-name

git push

git branch -d branch-name
```

---

# Common Beginner Mistakes

## Starting work without updating main

Before creating a branch:

```bash
git switch main
git pull
```

---

## Working directly on main

Avoid:

```bash
git switch main
# edit files
# commit changes
```

Instead:

```bash
git switch -c feature-name
```

---

## Creating unclear commits

Avoid:

```text
Update
Fix
Changes
```

Prefer:

```text
Add login validation
Update README setup steps
Fix incorrect API endpoint
```

---

## Forgetting to push changes

A local commit is not visible on GitHub.

Remember:

```bash
git push
```

---

# Lesson Summary

Congratulations!

You completed the full beginner Git and GitHub workflow.

You learned how to:

- Work with local repositories.
- Track changes.
- Create commits.
- Create branches.
- Merge changes.
- Work with GitHub.
- Synchronize repositories.
- Collaborate through Issues and Pull Requests.

You are now familiar with the basic Git workflow used by software development teams.

