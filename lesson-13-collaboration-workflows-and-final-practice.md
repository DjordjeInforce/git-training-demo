# Lesson 13 - Collaboration Workflows and Final Practice

**Audience / Level:** Beginners completing a practical Git and GitHub workflow

**Duration:** 60-90 minutes

**Prerequisites:** Lessons 00-12

---

## Learning Objectives

By the end of this lesson, you will be able to:

- Explain GitHub Flow.
- Explain the feature branch workflow.
- Describe the Pull Request lifecycle.
- Use a merge readiness checklist.
- Explain branch protection as a team safety rule.
- Explain CI as a basic quality gate.
- Complete a final end-to-end Git and GitHub practice workflow.
- Recognize advanced workflow names without needing to use them yet.

---

## 1. Why Workflows Matter

A workflow is an agreed way for a team to use Git and GitHub.

It answers:

- Where should new work happen?
- When should branches be pushed?
- How should review happen?
- When is a PR ready to merge?
- How does the team protect `main`?

For beginners, the most important workflow is GitHub Flow.

---

## 2. GitHub Flow

GitHub Flow is simple:

1. Start from `main`.
2. Create a short-lived branch.
3. Make a small change.
4. Commit with a clear message.
5. Push the branch.
6. Open a Pull Request.
7. Review and update.
8. Merge into `main`.
9. Delete the branch.

Example:

```bash
git switch main
git pull
git switch -c docs/final-practice
```

After changes:

```bash
git add README.md
git commit -m "Update final practice notes"
git push -u origin docs/final-practice
```

---

## 3. Feature Branch Workflow

A feature branch is a branch created for one task.

Good feature branches are:

- Short-lived
- Focused on one change
- Named clearly
- Reviewed before merge

Examples:

```text
docs/update-readme
fix/login-error
feature/profile-page
```

For this course, documentation branches are enough. You do not need to build a full application.

---

## 4. Pull Request Lifecycle

Typical PR lifecycle:

```text
Create issue
   |
Create branch
   |
Commit and push
   |
Open PR
   |
Review and checks
   |
Update if needed
   |
Merge
   |
Delete branch
```

At each step, use `git status` and clear commit messages.

---

## 5. Merge Readiness Checklist

Before merging a PR, check:

- [ ] The PR solves the issue or task.
- [ ] The title is clear.
- [ ] The description explains what changed.
- [ ] The branch is up to date with `main`.
- [ ] Review comments are resolved.
- [ ] Automated checks pass, if the repository has checks.
- [ ] The diff contains only expected changes.
- [ ] No secrets or local files are included.

---

## 6. Branch Protection Recap

Branch protection helps prevent risky changes to important branches.

Common rules:

- Require a Pull Request before merging.
- Require review approval.
- Require passing status checks.
- Block force pushes.

For beginners, remember:

> Protected branches help teams keep `main` stable.

---

## 7. Basic CI Quality Gate Recap

CI means Continuous Integration.

On GitHub, CI often runs through GitHub Actions.

A quality gate may:

- Run tests
- Check formatting
- Build the project
- Block merging if checks fail

You do not need to write Actions workflows in this course. You only need to understand what the checks mean in a PR.

---

## Optional: Git Flow

Git Flow is a more structured workflow for scheduled releases.

It often uses:

- `main` for production-ready code
- `develop` for upcoming work
- `feature/*` branches
- `release/*` branches
- `hotfix/*` branches

This is useful in some release-heavy teams, but it is more complex than needed for most beginner practice.

---

## Optional: Trunk-Based Development

Trunk-based development focuses on very small changes integrated into `main` frequently.

It works best with:

- Strong automated tests
- Reliable CI
- Small commits
- Short-lived branches

It is common in mature teams, but it requires discipline and automation.

---

## Optional: Release Branches, Hotfixes, and Backports

Release branches prepare a version for release.

Hotfix branches fix urgent production problems.

Backports apply a fix from a newer branch to an older supported version.

These are useful concepts to recognize, but they are not required for the main beginner workflow.

---

## Hands-On Exercises

### Exercise 1 - Final Practical Assessment

Complete this workflow from start to finish.

### Step 1 - Clone a Repository

Use a GitHub repository provided by your instructor or your own `git-training-demo` repository:

```bash
git clone <repository-url> git-training-demo-final
cd git-training-demo-final
```

### Step 2 - Create a Feature Branch

```bash
git switch main
git pull
git switch -c docs/final-practice-update
```

### Step 3 - Make a Change

```bash
echo "Final practice completed by <your-name>." >> README.md
```

### Step 4 - Inspect Changes

```bash
git status
git diff
```

### Step 5 - Commit with a Clear Message

```bash
git add README.md
git commit -m "Add final practice note"
```

### Step 6 - Push the Branch

```bash
git push -u origin docs/final-practice-update
```

### Step 7 - Open a Pull Request

On GitHub:

1. Open a PR from `docs/final-practice-update` into `main`.
2. Write a clear title.
3. Explain what changed.

### Step 8 - Respond to a Review Comment

If you are working alone, simulate the reviewer role by leaving your own review comment or writing down one requested change before updating the Pull Request.

If a reviewer requests a change:

```bash
echo "Review feedback addressed." >> README.md
git add README.md
git commit -m "Address review feedback"
git push
```

### Step 9 - Pull Latest Main

Before final merge, update local `main`:

```bash
git switch main
git pull
```

Then bring the latest `main` into your feature branch:

```bash
git switch docs/final-practice-update
git merge main
```

### Step 10 - Resolve a Simple Conflict if Needed

If GitHub or Git reports a conflict:

1. Open the file.
2. Remove conflict markers.
3. Keep the correct final content.
4. Stage and commit the fix.

```bash
git add README.md
git commit
git push
```

### Step 11 - Merge the PR

Merge the Pull Request on GitHub when:

- Review is complete.
- Checks pass, if checks exist.
- The diff is correct.

### Step 12 - Delete the Branch

On GitHub, delete the branch after merge.

Locally:

```bash
git switch main
git pull
git branch -d docs/final-practice-update
```

If `git branch -d` refuses to delete the branch, stop and check whether the PR was merged. If the PR was merged with squash merge, the exact local branch commit may not appear on `main`; in that case, use `git branch -D docs/final-practice-update` only after confirming the PR is merged and the branch is no longer needed.

---

## Commands Learned in This Lesson

```bash
git clone <repository-url>
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
git branch -D branch-name
```

---

## Common Beginner Mistakes

### Starting work from an outdated `main`

Run:

```bash
git switch main
git pull
```

before creating a new feature branch.

### Making a huge PR

Keep beginner PRs small and focused.

### Ignoring failed checks

Read the failed check. A failing check usually means something must be fixed before merging.

---

## Before Continuing Checklist

- [ ] You can describe GitHub Flow.
- [ ] You can create a feature branch from `main`.
- [ ] You can inspect, commit, push, and open a PR.
- [ ] You can respond to review feedback.
- [ ] You can pull latest `main`.
- [ ] You know how to handle a simple conflict.
- [ ] You can merge a PR and delete the branch.

---

## Lesson Summary

You completed the beginner Git and GitHub path: local workflow, diffs, commits, branches, merges, stash, undo, remotes, synchronization, Pull Requests, review, and final collaboration practice.
