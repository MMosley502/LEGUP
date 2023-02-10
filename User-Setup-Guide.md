# Setting up the Software
Setting up the software is quite easy.

### Setup Guide for Windows and macOS
1. Download the `Legup.jar` file.
2. Double click on the file to run it.

### Setup Guide for Linux
Reference this website: https://askubuntu.com/questions/101746/how-can-i-execute-a-jar-file-from-the-terminal

And that's it! But if you're still reading this, that means you probably ran into some problems. There are two troubleshooting guides: one for Windows and one for macOS.

If you're using a Windows computer, refer to [this troubleshooting guide](https://github.com/Bram-Hub/Legup/wiki/User-Setup-Guide#troubleshooting-on-windows).

If you're using Mac, refer to [this troubleshooting guide](https://github.com/Bram-Hub/Legup/wiki/User-Setup-Guide#troubleshooting-on-macos).

Note: both setup guides assume that you have already downloaded the `Legup.jar` file.

# Troubleshooting on Windows
While the screenshots provided were taken on a laptop running Windows 10, these instructions should still work on Windows 7 and Windows 8 machines.

## Common Issues
[Java is not installed](https://github.com/Bram-Hub/Legup/wiki/User-Setup-Guide/_edit#java-is-not-installed)

[LEGUP jar file defaults to Internet Explorer (or another application)](https://github.com/Bram-Hub/Legup/wiki/User-Setup-Guide#legup-jar-file-defaults-to-internet-explorer-or-another-application)

### Java is not installed
If you are absolutely sure that Java is not installed, you can skip straight to the last step, which contains [the link to install Java](https://java.com/en/download/). If you're not 100% sure, you can start from the first step to verify whether or not Java is installed.

1. Click on the Windows button `⊞ Win` to bring up the start menu. Search up for the application called Command Prompt and open it. The window that comes up should look something like this:

<img src="https://i.ibb.co/WgnvQyh/image.png" width="600">

2. Type in the command `java --version`. If Java is not installed, you should see a message that reads: 
```
'java' is not recognized as an internal or external command, operable program or batch file.
```
If Java is installed, you should see a message similar to the following:
```
java 15 2020-09-15
Java(TM) SE Runtime Environment (build 15+36-1562)
Java HotSpot(TM) 64-Bit Server VM (build 15+36-1562, mixed mode, sharing)
```
Below is a sample screenshot of the error message that would appear if Java is not installed.

<img src="https://i.ibb.co/hm5H6Yf/image.png" width="600">

3. If Java is not installed, go to https://java.com/en/download/ and follow the instructions on the website. Once that is done, you should be able to open the `Legup.jar` file without problems.

### LEGUP jar file defaults to Internet Explorer (or another application)
1. Right click the `Legup.jar` file. A menu should pop up, and you should see an option that reads `Open with...`. (See image below for clarification.)

<img src="https://i.ibb.co/k9K1h0h/image.png" width="400">

2. On the subsequent window that pops up, select to open the file through Open JDK Platform. If you do not see the Open JDK Platform option, you most likely do not have Java installed. Please refer to the "Java not installed" section.

<img src="https://i.ibb.co/k4wvvyb/image.png" width="400">

# Troubleshooting on macOS

## Common Issues
[Unable to locate Java Runtime](https://github.com/Bram-Hub/Legup/wiki/User-Setup-Guide#unable-to-locate-java-runtime)

[Unidentified developer](https://github.com/Bram-Hub/Legup/wiki/User-Setup-Guide#unidentified-developer)

### Unable to locate Java Runtime
When running the LEGUP jar you may be presented with this message:

<img width="269" alt="image" src="https://user-images.githubusercontent.com/55092742/173092677-a2bc03a5-28b9-478c-b128-a3393fbf8ba9.png">

If you see this message, please go to the [Java download page](https://java.com/en/download/). Download and install Java then you should be able to run the application.

### Unidentified developer
When running the LEGUP jar you may be presented with this message:

<img width="266" alt="image" src="https://user-images.githubusercontent.com/55092742/173093717-0aa7535e-8565-4e76-95e2-43ff6eed3b06.png">

If you see this message do the following:
1. Open Finder and navigate where you Legup.jar is located
2. Right click the Legup.jar
3. Hold down the option key and click "Open"
4. Now you can click Open on the new message and LEGUP should be running