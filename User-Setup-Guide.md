# Setting up the Software
Setting up the software is quite easy.

1. Download the `Legup.jar` file from LMS.
2. Double click on the file to run it.

And that's it! But if you're still reading this, that means you probably ran into some problems...

If you're using a Windows computer, refer to the troubleshooting guide here.
If you're using Mac, refer to the troubleshooting guide here.
Note: both setup guides assume that you have already downloaded the `Legup.jar` file.

# Troubleshooting on Windows
While the screenshots provided were taken on a laptop running Windows 10, these instructions should still work on Windows 7 and Windows 8 machines.

### Legup jar file defaults to Internet Explorer (or another application)
1. Right click the `Legup.jar` file. A menu should pop up, and you should see an option that reads `Open with...`. (See image below for clarification.)

<img src="https://i.ibb.co/k9K1h0h/image.png" width="400">

2. On the subsequent window that pops up, select to open the file through Open JDK Platform. If you do not see the Open JDK Platform option, you most likely do not have Java installed. Please refer to the "Java not installed" section.

<img src="https://i.ibb.co/k4wvvyb/image.png" width="400">

### Java is not installed
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

# Troubleshooting on macOS
Under construction