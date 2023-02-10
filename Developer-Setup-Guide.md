For this setup guide, we will be using IntelliJ IDEA and GitHub Desktop. You can use other IDEs such as Eclipse and Visual Studio Code and stick to using the command line for Git, but we prefer using IntelliJ IDEA and GitHub Desktop.

> Note: The old developer setup guide set up everything entirely within IntelliJ. While this does work, we found that developers who were new to Git and Java often confused the workflow process because they thought anything they did within the IntelliJ IDE was Java-related. We found the best way to mitigate this confusion was to have these developers do all the Git operations within GitHub Desktop and all the Java coding within IntelliJ IDEA. 
>
> If you don't want to use GitHub Desktop and prefer to do everything within IntelliJ, please refer to the [old developer setup guide](https://github.com/Bram-Hub/Legup/wiki/The-Developer-Setup-Guide-for-an-IntelliJ-Workflow). However, if you do choose to follow the old developer setup guide, please still follow the [Setting Up checkstyle within IntelliJ](#setting-up-checkstyle-within-intellij) section in the new developer setup guide as it is important and not present within the old setup guide.

## Installing IntelliJ IDEA
Visit the following page to download IntelliJ IDEA: https://www.jetbrains.com/idea/download/#section=windows

There are two versions of IntelliJ IDEA: IntelliJ IDEA Ultimate and IntelliJ IDEA Community. You can see the differences between the Ultimate and Community versions on the installation page. For LEGUP development, the Community edition is all we will need, since we will never make use of the features present in the Ultimate version. However, if you are a student and you still want to get the Ultimate version (as well as other IDEs, such as PyCharm, by JetBrains) for free, visit the following page to apply for a free educational license: https://www.jetbrains.com/community/education/#students

## Installing GitHub Desktop
Visit the following page to download GitHub Desktop: https://desktop.github.com/

To set up GitHub Desktop, follow Parts 1 and 2 of the [Getting started with GitHub Desktop](https://docs.github.com/en/desktop/installing-and-configuring-github-desktop/overview/getting-started-with-github-desktop) guide. Part 3 is about contributing to projects and adding and cloning repositories, but this setup guide will walk you through this process for LEGUP.

## Forking the Repository
Most of the work you will doing will be in your forked repository. Follow the following steps to fork the main repository:

1. Go to the the main LEGUP repository: https://github.com/Bram-Hub/Legup
2. Press the "Fork" button on the top right side of the page.
3. Once you have created your own fork, navigate to it, click the green "Code" button, then press the clipboard to copy your repository's link.

![](https://i.ibb.co/N6D2dTb/fork.png)

## Downloading the Project
Once the link to your forked version has been copied, you must [clone](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/cloning-a-repository) it onto your computer. 

Navigate to your fork, click the green "Code" button, and then click on "Open in GitHub Desktop". After a few moments, GitHub Desktop should open and prompt you to clone the repository. The repository URL should already be filled in and the local path should, by default, be `C:\Users\your_username\Documents\GitHub\Legup`. You can change this local path if you want, but we don't recommend it. Click on the "Clone" button to clone the repository. Click on "Fetch Origin" to fetch from your fork.

The one operation that GitHub Desktop cannot do is syncing your forked repository with the upstream repository. For information on how to do that, please refer to [GitHub's tutorial on syncing a fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork).

## Opening the Project within IntelliJ
After opening IntelliJ, click on the "Open" button. Navigate to `C:\Users\your_username\Documents\GitHub\Legup` (or if you changed the path in the previous step, whatever path you changed it to) and open the folder. After a few moments, IntelliJ should open the project up. 

In the bottom right hand corner, a popup will appear saying that it found a Gradle script. Gradle is a tool used by LEGUP to build the code. Press the "Import Gradle Project" button. After about a minute, IntelliJ will import the Gradle commands needed for LEGUP. 

To verify that everything worked, press the "Project" button on the left sidebar followed by the "LEGUP" button (this shows you all the files and folders in the LEGUP project). Your window should look similar to this:

![](https://i.ibb.co/S3dtrhP/legup-clone.png)

## Running LEGUP
To run LEGUP, you must build the project into a `.jar` file and then run the newly made file. 

Using IntelliJ, go to the Gradle window on the right side and run `Legup > Tasks > build > jar`. A terminal should appear at the bottom of the screen, and after a few minutes the terminal should print `Task execution finished 'jar'` (if the task never finishes successfully, you need to do some debugging). On the code navigation window, navigate to `Legup/build/libs`.

NOTE: If the Legup.jar file or the build folder does not appear after running the jar file, try running the `buildNeeded` and `buildDependants` files (in that order)

![](https://i.ibb.co/jMDCK06/jar-location.png)

Right click the `Legup.jar` file and then press "Run 'Legup.jar'" to launch your build of LEGUP.

## Setting Up checkstyle within IntelliJ
### Installing the CheckStyle Plugin
Within IntelliJ, click on `File > Settings`. After the settings dialog pops up, click on "Plugins" on the menu on the left side. Go to the marketplace and search for "CheckStyle-IDEA" and install the plugin. The item within the marketplace should look like the attachment below:

![image](https://user-images.githubusercontent.com/46334090/183318550-93652e0e-364a-478a-8300-0b1948f783ea.png)

After installing the plugin, click on `File > Settings`. After the settings dialog pops up, click on "Tools" on the menu on the left side and then click on "Checkstyle". By default, there should be two default configuration files: "Sun Checks" and "Google Checks". 

Click on the "+" button to add a configuration. Set the description field to "Legup". Select "Use a local Checkstyle file". Browse for the LEGUP checkstyle file. From the repository root, the path for the LEGUP checkstyle file should be `.idea/checkstyle-idea.xml`.

### Testing Your CheckStyle Setup
At the bottom of IntelliJ, you should have seen a bar that includes options such as "Git", "Run", "TODO", "Problems", and more. "CheckStyle" should now also be added to those options. Click on "CheckStyle", and then set the active configuration to "Legup". On the left, click on "Check Project" to check the entire project. You'll be able to see all the problems with your code formatting after the check is complete.

### Reformatting
In order to fix any issues with your formatting, the easiest way to do this is to right click the LEGUP source folder and click "Reformat Code". This will reformat the all the code within the repository to meet the CheckStyle standards.

Additionally, in the future, as you code, you can use the shortcut `Ctrl+Alt+L` to reformat the file you are working on.

### Troubleshooting
There is a chance that after reformatting, you may still see a bunch of problems if you run CheckStyle. For whatever reason, IntelliJ does not seem to import the entire CheckStyle file correctly.

To fix this, download this `LegupDefault.zip` attachment:
[LegupDefault.zip](https://github.com/Bram-Hub/Legup/files/9293908/LegupDefault.zip). This contains `LegupDefault.xml`, which we will be using in the upcoming steps.

Within IntelliJ, go to `File > Settings`. Then, in the pop up menu, go to `Editor > Code Style > Java`. Click on the little gear icon, then click on "Import Scheme > IntelliJ IDEA code style XML". Navigate to where you downloaded and unzipped `LegupDefault.xml` and click on it. Then, select "Apply". Now, when you reformat the code and then run Checkstyle, you should not have any problems.

