This page serves as a reference for the process of building an installable version of the application. 

## [Launch4j](http://launch4j.sourceforge.net/docs.html)

Launch4j is used in this project to wrap the `.jar` (JAR) file into an executable `.exe` file. Launch4j allows the developer to specify many attributes of the generated executable. The specifications of the generation of this "wrapper" executable must be within the `build.gradle` file in the `createExe()` task. This is achieved using the gradle plugin [launch4j-gradle](https://github.com/TheBoegl/gradle-launch4j).

In short, you can specify:
- The main class to be loaded using the full package name (e.g. `edu.rpi.legup.Legup`), 
- The output directory of the operation (e.g. `../native/windows` to set the directory `LegupSource/native/windows`)
- The output file location within the output directory (e.g. `bin/Legup.exe` to output to `LegupSource/native/windows/bin/Legup.exe`)
- The bundled JRE path (e.g. `jre` for the JRE path if you have the java runtime in the folder `jre` in the same directory as the executable)
- The JRE specifications (e.g. must be over Java 1.8, can be 64 or 32 bit, etc.)

*There are other settings which can be set within the `build.gradle` file for the `createExe()` task which I have not specified, see the launch4j and launch4j-gradle documentation.*

**This process generates what is essentially a JAR file packaged inside of an executable. This is not an installer; see below for information about the installer which installs this file and a given JRE.**

## [InnoSetup](https://jrsoftware.org/ishelp/)