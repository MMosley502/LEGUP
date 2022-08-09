# This version of the Programming Principles is outdated. Please refer to the [most recent Programming Principles documentation](https://github.com/Bram-Hub/Legup/wiki/Programming-Principles). This old version is being kept for archival purposes.

## Commenting
Since this project will be passed on to different students every year, it is important to include comments so that anyone, including someone who is brand new to the project team, can understand quickly what the code is for. It is not necessary to comment every single line, but please try to “chunk” the code and include comments for every chunk.

## Issues
### Creating and Reporting Issues
If you see an issue, double check if it has already been documented. If the issue has not already been document, please open a new issue and give it the appropriate labels. 

If the issue is a bug that needs to be fixed, **please include the current behavior, expected behavior, and any steps needed to reproduce the bug in your issue.** If possible, including a video of how to reproduce the issue would be preferred. Please refer to [this issue](https://github.com/Bram-Hub/Legup/issues/97) as an example for reporting bugs.

### Solving an Issue
If you are working on an issue, please assign it to yourself and create a branch for that issue (remember to create the branch off of `dev`). Anyone is free to solve any issue, and we encourage people to collaborate on issues together.

## Creating Branches
**This project follows the [git-flow branching model](https://nvie.com/posts/a-successful-git-branching-model/). This means that, for the most part, if you need to create a new branch, you should branch off of `dev`, NOT `master`.**

All branches involving bug fixes should follow the following format: `puzzle-issue00-descriptive_name` (note that if the branch is solving a general problem and not a problem related to a specific puzzle, the first part can be omitted). If an issue number is included, it should always refer to the respective issue on [Legup's GitHub Issues page](https://github.com/Bram-Hub/Legup/issues). Always create a new branch if you are tackling a new problem so that only one task is being done on a single branch at all times. This will make it easier to debug code and figure out where issues stem from. Please stray away from including your name in your branches.

Examples of good branch names:
	`sudoku-issue12-fix_terrible_bug`
	`nurikabe-new_feature`

Examples of bad branch names:
	`johnny-appleseed`
	`mike-sudoku-algorithm-fix`

## Pull Requests and Merging
For the most part, developers should always merge into the branch `dev`. Any merges into `master` will only be from `dev`, and will be done after given approval from Dr. van Heuveln. As a developer, it is important that you resolve any conflicts in `dev` before requesting to merge into `master`.

Please document what changes are being made in a particular pull request. If applicable, please remember to link the pull request to a GitHub issue.
