**Note: This page is a work in progress. Please refer to the old setup guide for now until this is complete.**
# Developer Setup Guide

For this setup guide, we will be using IntelliJ IDEA and GitHub Desktop. You can use other IDEs such as Eclipse and Visual Studio Code and stick to using the command line for Git, but we prefer using IntelliJ IDEA and GitHub Desktop.

> Note: The old developer setup guide set up everything entirely within IntelliJ. While this does work, we found that developers who were new to Git and Java often confused the workflow process because they thought anything they did within the IntelliJ IDE was Java-related. We found the best way to mitigate this confusion was to have these developers do all the Git operations within GitHub Desktop and all the Java coding within IntelliJ IDEA. If you don't want to use GitHub Desktop and prefer to do everything within IntelliJ, please refer to the [old developer setup guide](https://github.com/Bram-Hub/Legup/wiki/Programming-Setup-Guide). However, if you do choose to follow the old developer setup guide, please still follow the [Setting Up checkstyle within IntelliJ](#setting-up-checkstyle-within-intellij) section in the new developer setup guide as it is important and not present within the old setup guide.

## Installing IntelliJ IDEA
Visit the following page to download IntelliJ IDEA: https://www.jetbrains.com/idea/download/#section=windows

There are two versions of IntelliJ IDEA: IntelliJ IDEA Ultimate and IntelliJ IDEA Community. You can see the differences between the Ultimate and Community versions on the installation page. For Legup development, the Community edition is all we will need, since we will never make use of the features present in the Ultimate version. However, if you are a student and you still want to get the Ultimate version (as well as other IDEs, such as PyCharm, by JetBrains) for free, visit the following page to apply for a free educational license: https://www.jetbrains.com/community/education/#students

## Installing GitHub Desktop
Visit the following page to download GitHub Desktop: https://desktop.github.com/

To set up GitHub Desktop, follow Parts 1 and 2 of the [Getting started with GitHub Desktop](https://docs.github.com/en/desktop/installing-and-configuring-github-desktop/overview/getting-started-with-github-desktop) guide. Part 3 is about contributing to projects and adding and cloning repositories, but this setup guide will walk you through this process for Legup.

## Forking the Repository
Most of the work you will doing will be in your forked repository. Follow the following steps to fork the main repository:

1. Go to the the main Legup repository: https://github.com/Bram-Hub/Legup
2. Press the "Fork" button on the top right side of the page.
3. Once you have created your own fork, navigate to it, click the green "Code" button, then press the clipboard to copy your repository's link.

![](https://i.ibb.co/N6D2dTb/fork.png)

## Downloading the Project
Once the link to your forked version has been copied, you must [clone](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/cloning-a-repository) it onto your computer. 

Navigate to your fork, click the green "Code" button, and then click on "Open in GitHub Desktop". After a few moments, GitHub Desktop should open and prompt you to clone the repository. The repository URL should already be filled in and the local path should be `C:\Users\your_username\Documents\GitHub\Legup`. Click on the "Clone" button to clone the repository. Click on "Fetch Origin" to fetch from your fork.

The one operation that GitHub Desktop cannot do is syncing your forked repository with the upstream repository. For information on how to do that, please refer to [GitHub's tutorial on syncing a fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork).

## Setting Up checkstyle within IntelliJ

## Running Legup
To run Legup, you must build the project into a `.jar` file and then run the newly made file. 

Using IntelliJ, go to the Gradle window on the right side and run `Legup > Tasks > build > jar`. A terminal should appear at the bottom of the screen, and after a few minutes the terminal should print `Task execution finished 'jar'` (if the task never finishes successfully, you need to do some debugging). On the code navigation window, navigate to `Legup/build/libs`.

![](https://i.ibb.co/jMDCK06/jar-location.png)

Right click the `Legup.jar` file and then press "Run 'Legup.jar'" to launch your build of Legup.