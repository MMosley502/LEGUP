**This is very much in progress. Please refer to the old programming principles page until this is done.**

## Workflow
Legup uses the Feature Forking Workflow. Please refer to [this blog post](https://medium.com/@jerrylin720/git-workflow-comparison-f84d270708ab) for more information on the Feature Forking Workflow as well as other workflows.

![image](https://user-images.githubusercontent.com/46334090/182742871-c3e08638-1d51-40b4-9146-410865b4d737.png)

Source: https://medium.com/@jerrylin720/git-workflow-comparison-f84d270708ab

This means that the Bram-Hub/Legup repository should have very few branches. `master` and `dev` will always exist, and beyond those two branches, there may be a few more for major features being implemented (e.g. `puzzle-editor`).

For creating branches on the Bram-Hub/Legup repository, please be sure to follow the [git-flow branching model](https://nvie.com/posts/a-successful-git-branching-model/). This means that all new feature branches should be created off of `dev`, not `master`.

## Commenting
Since Legup is primarily developed by students, meaning that people constantly leave and join the project. It is important to prioritize commenting your code to ensure that anyone, including someone who is brand new to the project team, can understand quickly what the code is for. It is not necessary to comment every single line, but please comment particularly confusing and important segments of your code.

## Issues
### Creating Issues
In order to [report a new issue](https://github.com/Bram-Hub/Legup/issues/new/choose), you just have to fill out one of the issue forms. In addition to filling out the form, please be sure to specify any other labels that may be applicable to your issue. In order to do this, reference the "Labels" section to the right of the issues form, click on the gear icon, and click on any other applicable labels. Reference the sample image below for further clarification.

For example, if you were reporting a Nurikabe bug, you would add the Nurikabe label to your issue.

![image](https://user-images.githubusercontent.com/46334090/182708802-918283a9-7fef-4c63-b275-7a5f44f7a8a1.png)

### Solving an Issue
If you are working on an issue, please assign it to yourself and work on the issue in your fork. Anyone is free to solve any issue, and we encourage people to collaborate on issues together. 

## Pull Requests
For the most part, due to the workflow Legup is using, you should not be creating a pull request to merge into `master`. The most common exceptions to this is if you're only updating documentation or doing a hotfix. Most of your pull requests should be merging into `dev` or a feature branch.

At the end of each semester (or every couple months), a pull request should be done on Bram-Hub/Legup from `dev` into `master` at the approval of Dr. van Heuveln. This version of Legup that is being merged into `master` should be stable and good for general use. 