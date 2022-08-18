This page serves as a reference for the process of building an installable version of the application. 

**Note: This process can only be completed fully on windows.**

## [Launch4j](http://launch4j.sourceforge.net/docs.html)

Launch4j is used in this project to wrap the `.jar` (JAR) file into an executable `.exe` file. Launch4j allows the developer to specify many attributes of the generated executable. The specifications of the generation of this "wrapper" executable must be within the `build.gradle` file in the `createExe` task. This is achieved using the gradle plugin [launch4j-gradle](https://github.com/TheBoegl/gradle-launch4j).

In short, you can specify:
- The main class to be loaded using the full package name (e.g. `edu.rpi.legup.Legup`), 
- The output directory of the operation (e.g. `../native/windows` to set the directory `LegupSource/native/windows`)
- The output file location within the output directory (e.g. `bin/Legup.exe` to output to `LegupSource/native/windows/bin/Legup.exe`)
- The bundled JRE path (e.g. `jre` for the JRE path if you have the java runtime in the folder `jre` in the same directory as the executable)
- The JRE specifications (e.g. must be over Java 1.8, can be 64 or 32 bit, etc.)
- The icon (which is not yet implemented; details within `build.gradle`)

*There are other settings which can be set within the `build.gradle` file for the `createExe` task which I have not specified, see the launch4j and launch4j-gradle documentation.*

Running the `createExe` gradle task will generate the executable. For the current configuration, this generated file will be at `LegupSource/native/windows/bin/Legup.exe`. This process also generates a folder which stores the libraries managed by launch4j at `LegupSource/native/windows/lib`. These library files are unimportant after the task has finished and are not required distribute with the executable. If all has gone correctly and you already have Java properly installed on your system, you should now be able to run the generated `Legup.exe`. If Java 1.8 or above is not installed (correctly) on your system, you will be prompted to install it by an error message when trying to launch the program. If, however, there is a folder `jre` present in the same directory as the executable which contains a functional JRE at Java 1.8 or greater (as configurable through the `build.gradle` definition of the function), the program will also launch even if Java is not installed and pointed to correctly by the system path variable.

**This process generates what is essentially a JAR file packaged inside of an executable. This is not an installer; see below for information about the installer which installs this file and a given JRE.**

## [InnoSetup](https://jrsoftware.org/ishelp/)

InnoSetup is used to create an installer containing the file generated above. The generated installer must also include some JRE at Java version greater than or equal to 1.8 in the path `jre` (as described above). Hence, the script must be directed to the JRE on the system. This causes an issue since different systems store their Java installations in different directories and have different versions of the Java Runtime Environment. Because the script is thus hard-coded with a directory in which the JRE should be located, it fails to run on most systems. 

In short: **You must edit the script for it to run correctly.** 

The script you must edit is located at `LegupSource/native/windows/legup_inno_setup.iss`. Instructions for editing this file can be found within the file directly as comments including which line must be changed to match the JRE installation on your system you will package within the installer. The line will likely need to be changed to something akin to
```
#define MyJava "C:\Program Files\Java\jre*********\"
```
**Note: This path must end with a `\`.**

This edit will allow InnoSetup to know where the JRE to include within the installation. To edit other aspects of the script, please see the InooSetup 6.2 documentation. I am also aware that it is possible to create an InnoSetup script which automatically downloads and installs the correct version of Java to the machine. This would allow for a much smaller installer size and would no longer require the InnoSetup script to be edited by the person compiling it; editing the script for this is a likely vector for errors. See [Issue #281](https://github.com/Bram-Hub/Legup/issues/281) for information and discussion on this topic.

To run this build task, on a Windows machine you must run the `buildNativeWindows` gradle task as described within `build.gradle`. This task automatically runs the `createExe` task described above, so there is no need to run that separately first. Then, this task runs the small batch script located at `LegupSource/native/windows/make_windows_installer.bat`. All this script does is execute the InnoSetup compiler with the `legup_inno_setup.iss` file given as it's source.

InnoSetup is a small enough program that a copy of it can be reasonably included within the repository for use as described above. This version of InnoSetup can be found at the `LegupSource/native/windows/inno-setup/` directory. The InnoSetup license can be found at `LegupSource/native/windows/inno-setup/LICENSE` and allows for the redistribution of the binaries under certain conditions. Our use of InnoSetup meets all of the requirements as described within the license. If you intend to change how LEGUP uses the InnoSetup binaries or otherwise use the InnoSetup binaries yourself, I would encourage reading the license.