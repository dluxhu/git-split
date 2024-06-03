# The `git-split` workflow

This document describes the workflow that you can use if you have lots of code that you hacked together and want to split into smaller parts and have them merge or review independently.

## How to work with `git-split`

Let's say you have your work branch that you are hacking on for a specific task. Let's call it `task1-work`. It's already a lot of code and if you sent it for review, your teammates would be really angry to you. The solution would be to split this PR into smaller, easily digestable pieces. I developed a small script for this.

You start out in your work branch with the code already in an advanced stage and all changes are committed. You want to create a branch that only contains some part of your changes and this is how you do it:

```
git-split task1-part1
```

This will create your `task1-part1` branch from `master` and all your changes will show up as modifications. Nothing is committed to this branch yet. Your original `task1-work` branch will be intact.

All you have to do is to revert the changes you don't want to be included in the first part that you send for review with your favorite git client (IDEA, VS Code, GitHub desktop, etc.) or command line. Then commit and push your code.

You can then return to your `task1-work` branch and merge `task1-part1` into your changes so that you can see the diffs between the two in review tools (e.g. in the GitHub review tool).

If your teammates wants you to make changes to `task1-part1` during the review process, then make those changes in that branch, then merge them into `task1-work` so that you can keep developing with your latest changes. It is not a problem if you accidentally committed the change to your `task1-work`, because you can cherry-pick the change to `task1-part1`, too.

Once your PR is approved and merged to `master`, you can merge `master` into your `task1-work` branch and start preparing the next PR with `git-split`.

I would not recommend creating more than one review branch and one work branch for one task, because I've found keeping them up to date too much work.

## Note

* If your branch name that you are developing against is not `master`, you can specify the base branch as a second parameter:

  ```
  git-split task1-part1 main
  ```
