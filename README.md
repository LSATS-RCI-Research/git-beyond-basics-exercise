# Git Beyond the Basics: Conflict Exercises

Practice resolving conflicts with merge, rebase, and interactive rebase. After cloning, create local copies of the three published exercise branches; no remote changes are needed.

## Setup

In GitHub, click on "Use this template" to create a copy of this repository that you own. On the repository creation screen. Make sure to enable "Include all branches".

Then clone the repo to a local directory and open it.

## Activity 1 — Resolve a merge conflict

Goal: merge `main` into a topic branch and resolve competing edits to the same line.

- Start: `git switch activity-1`
- Confirm the branch and clean starting tree: `git status`
- Merge the incoming work: `git merge main`
- Open `activities/activity-1/menu.txt`. Choose a final `daily_special` value and remove all conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
- Stage and complete the merge: `git add activities/activity-1/menu.txt`, then `git commit` (Git supplies a merge-commit message).
- Integrate the topic branch: `git switch main`, then `git merge --ff-only activity-1`.
- Review the result with `git log --graph --oneline --decorate --branches` and `git status`.

## Activity 2 — Resolve a conflict during rebase

Goal: replay a topic commit on top of `main`, resolving the conflict as the commit is replayed.

- Start: `git switch activity-2`
- Begin the rebase: `git rebase main`
- Open `activities/activity-2/deployment.txt`. Choose a final `deployment` value and remove all conflict markers.
- Stage the resolution: `git add activities/activity-2/deployment.txt`
- Continue replaying the commit: `git rebase --continue` (save/close the commit-message editor if Git opens one).
- Integrate the rebased topic branch: `git switch main`, then `git merge --ff-only activity-2`.
- Check the result with `git log --graph --oneline --decorate --branches` and `git status`.
- If you need to abandon an in-progress rebase, use `git rebase --abort`.

## Activity 3 — Interactive rebase: squash a linear topic branch

Goal: resolve a conflict, squash a linear three-commit topic history, and place the resulting commit on top of `main`.

- Start: `git switch activity-3`
- Inspect the local starting graph: `git log --graph --oneline --decorate --branches`.
- Start the interactive rebase: `git rebase -i main`
- In the todo list, keep the main-course commit as `pick`; change the side-dish and dessert commits to `squash`.
- Save and close the todo list. Whenever a conflict appears in `activities/activity-3/plan.txt`, resolve it (the instructor key recommends `main=ramen_and_risotto` to retain both ideas), remove conflict markers, then run `git add activities/activity-3/plan.txt` and `git rebase --continue`. Repeat this resolve/add/continue cycle if squashing a later commit reports another conflict.
- If Git asks for a combined commit message, keep or edit it and save/close. Integrate the rewritten topic branch: `git switch main`, then `git merge --ff-only activity-3`.
- Inspect the final graph and status; all three topic branches should now be integrated into `main`, and Activity 3 should have no merge commit.
- If you need to abandon this activity, use `git rebase --abort`.
