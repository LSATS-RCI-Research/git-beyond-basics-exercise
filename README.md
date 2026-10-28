# Git Beyond the Basics: Conflict Exercises

Practice resolving conflicts with merge, rebase, and interactive rebase. After cloning, create local copies of the three published exercise branches; no remote changes are needed.

## Setup

In GitHub, click on "Fork" to create a copy of this repository that you own. On the fork creation screen, disable "Copy the `main` branch only". Then clone the repo to a local directory and open it.

When instructed to create a pull request during activities. Make sure to propose changes from the appropriate branch on your fork to the `main` branch on your fork, not the original repository.

## Activity 1 — Resolve a merge conflict

Merge `main` into a topic branch and resolve competing edits to the same line.

- Open a pull request for the changes in the `activity-1` branch. See that there are conflicts that need to be resolved.
- Locally, checkout the branch with `git switch activity-1`. Confirm with `git status`.
- Merge the incoming work with `git merge main`. You can inspect the in-progress merge with `git status`.
- Open `activities/activity-1/menu.txt`. Choose a final `daily_special` value and remove all conflict markers.
- Stage the conflict resolution with `git add activities/activity-1/menu.txt`. Then, create the merge commit with `git commit` (Git supplies a default merge-commit message).
- Review the result with `git log --graph --oneline --decorate --branches` and `git status`.
- Push the changes with `git push`.
- Merge the changes in GitHub with a merge commit.

Notice how this adds two seemingly extraneous commits to the Git history. One commit shows the merge from `main` to `activity-1` to bring our branch up to date. Another commit shows the merge of `activity-1` back into main.

## Activity 2 — Resolve a conflict during rebase

Rebase a commit on top of `main` and resolve a conflict.

- Open a pull request for the changes in the `activity-2` branch. See that there are conflicts that need to be resolved.
- Locally, checkout the branch with `git switch activity-2`. Confirm with `git status`.
- Begin the rebase with `git rebase main`.
- Open `activities/activity-2/deployment.txt`. Choose a final `deployment` value and remove all conflict markers.
- Stage the resolution: `git add activities/activity-2/deployment.txt`
- Continue rebasing the commit: `git rebase --continue`.
- Check the result with `git log --graph --oneline --decorate --branches` and `git status`.
- Push the changes with `git push --force-with-lease`.
- Merge the changes in GitHub with a merge commit.

Notice that this avoid adding the additional commit to the history that we saw in Activity 1. The rebase rewrites the `activity-2` branch to appear as if it was created from the latest commit on `main`, so the merge back into `main` is a simple fast-forward merge.

## Activity 3 — Interactive rebase to squash commits

Rebase multiple commits on top of `main` and resolve a conflict. Squash commits to clean up history.

- Locally, checkout the branch with `git switch activity-3`. Confirm with `git status`.
- Inspect the commit history so far with `git log --graph --oneline --decorate --branches`.
- Start the interactive rebase with `git rebase -i main`.
- In the list of commits, you have the option to apply commands like pick, reword, and squash. By default, a standard rebase applies pick commands for all commits. Use this an opportunity to update commit messages or squash multiple commits into the previous commit.
  - Change the side-dish and dessert commits to squash to combine them into the previous main course commit.
  - Reword the first commit to make it clear what's being updated.
- Save and close the list. Git will then rebase each commit and stop when something requires your attention.
  - Resolve conflicts as they occur. Run `git add activities/activity-3/plan.txt` and `git rebase --continue`.
  - Update the commit message for the first commit when it's presented.
- Check the result with `git log --graph --oneline --decorate --branches` and `git status`.
- Push the changes with `git push --force-with-lease`.
