# Principles

Note: this page is still under construction; everything in the Wiki is subject to change.

## Commenting
Since this project will be passed on to different students every year, it is important to include comments so that anyone, including someone who is brand new to the project team, can understand quickly what the code is for. It is not necessary to comment every single line, but please try to “chunk” the code and include comments for every chunk.

## Documenting Issues
Please use GitHub issues to note any bugs or problems that may occur. If you want to document issues in a separate Google Doc or Word document for yourself, that is fine. However, in order to help foster a collaborative and efficient workspace, it is best if we report issues on GitHub issues so that team members can have a quick overview of what is fixed, what is being fixed, and what needs to be fixed at all times.

## Creating Branches
Please do not include your name in branch names. Including your name in the branch might make it seem like that everything that is being done in that branch is off limits to everyone else, which goes against the collaborative environment we are trying to create.

Please name branches something concise but descriptive of what is being accomplished in that branch. Always create a new branch if you are tackling a new problem so that only one task is being done on a single branch at all times. This will make it easier to debug code and figure out where issues stem from.

Examples of bad branch names:
	`johnny-appleseed`
	`mike-sudoku-algorithm-fix`

Examples of good branch names:
	`sudoku-fix-ui`
	`nurikabe-puzzle-check`

## Merging
For the most part, student developers should always merge into the branch `dev`. Any merges into `main` will only be from `dev`, and will be done after a confirmation from Professor Bram. As a student developer, it is important that you resolve any conflicts in `dev` before requesting to merge into main.

# Student Developer Setup Guide

## Forking the Repository
The first thing that you will want to do is fork the main Legup repository. Press the "Fork" button on the top right side of the page. Once you have created your own fork, navigate to it, click the green "Code" button, then press the clipboard to copy your repository's link.

![](https://i.ibb.co/N6D2dTb/fork.png)

## Downloading the Project
Once the link to your forked version has been copied, you must [clone](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/cloning-a-repository) it onto your computer. 

Doing so using IntelliJ is relatively simple, as all you need to do is press "Get from Version Control" once IntelliJ opens, paste in the URL you copied, and then press "Clone". After a few moments, IntelliJ should have downloaded all the Legup code (if on Windows, it should be stored in `C:\Users\YOUR_USERNAME\IdeaProjects\Legup`) and opened the coding window. In the bottom right hand corner, a popup will appear saying that it found a Gradle script. Gradle is a tool used by Legup to build the code. Press the "Import Gradle Project" button. After about a minute, IntelliJ will import the Gradle commands needed for Legup. 

To verify that everything worked, press the "Project" button on the left sidebar followed by the "Legup" button (this shows you all the files and folders in the Legup project). Your window should look similar to this:

![](https://i.ibb.co/S3dtrhP/legup-clone.png)

## Running Legup
To run Legup, you must build the project into a `.jar` file and then run the newly made file. 

Using IntelliJ, go to the Gradle window on the right side and run `Legup > Tasks > build > jar`. A terminal should appear at the bottom of the screen, and after a few minutes the terminal should print `Task execution finished 'jar'` (if the task never finishes successfully, you need to do some debugging). On the code navigation window, navigate to `Legup/build/libs`.

![](https://i.ibb.co/jMDCK06/jar-location.png)

Right click the `Legup.jar` file and then press "Run 'Legup.jar'" to launch your build of Legup.

If you are not using IntelliJ, all you need to do is run the command `gradlew.bat jar` if you use Windows or the command `gradlew jar` if you use Linux. This will create the file `Legup/build/libs/Legup.jar` (same place as IntelliJ).

## Pushing Changes
Once you are ready to add your changes to the main Legup repository, you need to commit your changes, push your changes to your forked repository, and then open a pull request on the main repository. 

Committing and pushing your changes can be done within IntelliJ using the Git buttons on the right side of the top bar.

![](https://i.ibb.co/RvrZS3y/git.png)

The leftmost blue arrow button can be used to update the project on your computer whenever somebody else makes changes to the project on GitHub. The middle green button is used to commit your changes. The rightmost green button is used to push your committed changes to your forked GitHub repository.

### Committing
Since the first step is to commit your changes, press the commit button. A window will appear on the left that lists all the changes files as well as a text box to describe the changes you've made. Put a brief description of what you've done, and then press the "Commit" button at the bottom.

### Pushing
The next step is to push your changes. Press the push button. Like before, you will be presented with all the files that you've changed. Press the "Push" button at the bottom (you may be prompted to login to GitHub). After a few seconds, all your changes will be uploaded to your forked GitHub repository. 

### Pull Requests
The final step is to open a pull request to merge the code from your repository into the main repository (NOTE: you can make multiple commits to your forked repo before opening a pull request, this step does not have to immediately follow the previous one). Open your forked version on GitHub and then press "Pull requests", followed by"New pull request", and then "Create pull request". Create a title for your request as well as a description of the changes. Finally, press "Create pull request". Pull requests must be approved by another maintainer in order to be merged, so all you need to do now is wait for somebody else to approve and then merge your request.