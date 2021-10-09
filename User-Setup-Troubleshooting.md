This setup guide assumes that you have already downloaded the `Legup.jar` file.

### Legup jar file defaults to Internet Explorer (or another application)
1. Right click the `Legup.jar` file. A menu should pop up, and you should see an option that reads `Open with...`. (See image below for clarification.)
![](https://i.ibb.co/k9K1h0h/image.png)
2. On the subsequent window that pops up, select to open the file through Open JDK Platform. If you do not see the Open JDK Platform option, you most likely do not have Java installed. Please refer to the "Java not installed" section.
![](https://i.ibb.co/k4wvvyb/image.png).

### Java is not installed
1. Click on the Windows button `⊞ Win` to bring up the start menu. Search up for the application called Command Prompt and open it. The window that comes up should look something like this:
![](https://i.ibb.co/WgnvQyh/image.png)
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
![](https://i.ibb.co/hm5H6Yf/image.png)
3. If Java is not installed, go to https://www.oracle.com/java/technologies/downloads/#jdk17-windows and download JDK for either Linux, macOS, or Windows. Follow the installation guide, and once that is done, you should be able to open the `Legup.jar` file without problems.