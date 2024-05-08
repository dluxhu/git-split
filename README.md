# The `git-split` workflow

This document describes the workflow that you can use if you have lots of code that you hacked together and want to split into smaller parts and have them merge or review independently.

## How to work with `git-split`

Let's say you have your `project1-work` branch that you are hacking on. It's a lot of code and if you sent it for review, your teammates would be really angry to you. The solution would be to split this PR into smaller, easily digestable pieces. I developed a small script for this.

You start out in your work branch, then you run:

```
git-split project1-part1
```

This will create your `project1-part1` from `master` and all your changes will show up as modifications. Your original `project1-work` branch will be intact.

All you have to do is to revert the changes you don't want to be included in the first commit with your favorite git client (IDEA, VS Code, GitHub desktop, etc.) or command line. Then commit and push your code.

You can then return to your `project1-work` branch and merge `project1-part1` into your changes so that you can see the diffs between the two in review tools (e.g. in the GitHub review tool).

I would not recommend creating more than one review branch (the one you send for review and expect comments and modification requests) and one work branch (that you hack ahead of the reviewed code), because I've found keeping them up to date too much work.

## Note

* If your branch name that you are developing against is not `master`, you have to update the script. It would be easy to add a command-line parameter or environment variable to specify this, but I leave it to you as an exercise.
