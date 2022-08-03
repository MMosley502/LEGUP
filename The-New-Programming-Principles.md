**This is very much in progress. Please refer to the old programming principles page until this is done.**

## Workflow
Legup uses the Feature Forking Workflow. Please refer to [this blog post](https://medium.com/@jerrylin720/git-workflow-comparison-f84d270708ab) for more information on the Feature Forking Workflow as well as other workflows.

This means that the Bram-Hub/Legup repository should have very few branches. `master` and `dev` will always exist, and beyond those two branches, there may be a few more for major features being implemented (e.g. `puzzle-editor`).

For creating branches on the Bram-Hub/Legup repository, please be sure to follow the [git-flow branching model](https://nvie.com/posts/a-successful-git-branching-model/). This means that all new feature branches should be created off of `dev`, not `master`.

## Commenting
Since Legup is primarily developed by students, meaning that people constantly leave and join the project. It is important to prioritize commenting your code to ensure that anyone, including someone who is brand new to the project team, can understand quickly what the code is for. It is not necessary to comment every single line, but please comment particularly confusing and important segments of your code.

