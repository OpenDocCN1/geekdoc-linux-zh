
libtk.a and libtcl.a will fail to build, for instance, unless you cross-compiled and installed Tcl/Tk for your target. This doesn't mean the Python build has failed. Rather, it is an indication that one of the Python components has not built successfully. You will still be able to install and use the Python interpreter and the modules that built properly on your target.

## Other Programming Languages

Linux, of course, supports many more programming languages. Whether you are looking for programming in Ada, Forth, Lisp, or FORTRAN, a short search on the Net with your favorite search engine should yield rapid results. A good starting point is the “Other Languages” section in Chapter 13 of *Running Linux* by Matthias Dalheimer and Matt Welsh (O'Reilly).

The cross-compiling and cross-development capabilities of the various language tools will need to be evaluated on a tool-tool basis, since few compilers and interpreters lend themselves well to cross-platform development.

## Eclipse: An Integrated Development Environment

As we have seen in previous sections, the development tools for embedded Linux are a collection of standalone command-line programs. It has long been the preference of die-hard Unix and Linux developers to create software using a simple file editor and a command-line shell to invoke the development tool. However, most embedded software developers prefer to work in an IDE that provides a common graphical interface to all the functions of the development tools.

The Eclipse project, which IBM originally created in November 2001, and which has been an independent nonprofit corporation since 2004, provides an open development platform comprised of extensible frameworks, tools, and runtimes for building, deploying, and managing software. Its popularity, openness, and rich features make it an excellent choice as an IDE for embedded Linux development. A typical display by Eclipse appears in Figure 4-5.

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_157_0.png)

*Figure 4-5. Typical Eclipse project workspace*

Instead of a monolithic IDE, Eclipse provides a modular framework on which many IDEs can be built by combining a common base and a plethora of plug-ins for various functionalities, such as the CDT plug-in for C/C++ developers and the Remote System Explorer for target management. You can read more about Eclipse on the project website at http://www.eclipse.org.

Although several other IDEs exist for Linux, no other such tool enjoys the widespread adoption of Eclipse, which is used by both commercial vendors (who base development environments on Eclipse and provide many plug-ins and extensions) and the open source community, which has extended Eclipse to support practically every need.

We will cover the installation, adaptation, and use of Eclipse in the following sections.

### Installing Eclipse

Eclipse is a Java application, which makes it cross-platform. However, that means you need a Java runtime virtual machine (JVM) to run it. Most current Linux distributions come with a preinstalled JVM called GCJ. Unfortunately, although Eclipse does run on the GCJ, it is not one of the referenced JVMs on which it is regularly tested. We therefore recommend that you first install a free JVM for Linux from the Sun Java download website at http://www.java.com/en/download/manual.jsp.

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_157_1.png)

The Sun Java JVM can peacefully coexist with GCJ, so you should not worry about trashing your current JVM installation.

After successfully installing the Sun JVM, proceed to download Eclipse from the project download page at http://www.eclipse.org/downloads. You will want to download the Eclipse IDE for C/C++ Developers edition, which integrates the basic common Eclipse core with the CDT plug-in for C/C++ developers.

After downloading the compressed tar archive, change into the directory to which you wish to install Eclipse and decompress the tar archive.

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_158_0.png)

You can install Eclipse in any location you wish, including your home directory, but if you wish to share the Eclipse installation with others using the same computer (such as a shared networked server), we recommend you open the archive in a location that is accessible to all users. This may require you to uncompress the archive as the superuser.

```bash
$ cd $SPRROOT/tools
$ tar zxvf $SPRROOT/build-tools/eclipse-cpp-europa-fall12-linux-gtk-x86_64.tar.gz
```

Before you can run Eclipse, you need to configure the location of your alternative JVM. To do so, find the text file named `eclipse.ini` in the `SPRROOT/tools/eclipse` folder, and make sure the following lines are present and point to the correct location where the Sun JVM has been installed:

```ini
...
-vm
/ust/lib/jvm/java-6-sun/jre/bin/java
...
```

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_158_1.png)

Do not try to put the path to the JVM in the same line as the `-vm` argument. The text must appear on two separate lines, as shown in the preceding excerpt.

### Running Eclipse

Now you are ready to run Eclipse:

```bash
$ SPRROOT/tools/eclipse/eclipse &
```

The first time you invoke it, you will be presented with a dialog box asking you to select a workspace (Figure 4-6). An Eclipse workspace is the location where development projects and Eclipse configuration information are saved. Either accept the default workspace location of a directory named `workspace` in your home directory, or provide an alternate location and click OK.

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_159_0.png)

*Figure 4-6. Eclipse Workspace Launcher*

After Eclipse finishes loading, it presents you with a welcome screen.

### Extending Eclipse

As we explained, Eclipse is a modular framework for building IDEs. Thus, apart from the common core framework, most Eclipse-based IDE functionalities are provided by plug-ins. Plug-ins allow Eclipse to support a wide range of languages, source control systems, targets, debugging facilities, and more.

As we chose to install the Eclipse IDE for C/C++ Developers edition, one plug-in is already installed in our new Eclipse installation: CDT, the C/C++ developer support plug-in. In order to make Eclipse a more useful developer environment for embedded Linux, we will add the Target Management toolkit plug-in and the Subclipse Subversion source control integration plug-in.

> You can find many more plug-ins (more than a thousand are listed at the time of this writing) in the Eclipse Plugin Central website at http://www.eclipseplugincentral.com.

### Installing a plug-in

Eclipse contains a generic infrastructure for installing and updating plug-ins. Installation of practically all Eclipse plug-ins, therefore, follows the same procedure.

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_160_0.png)

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_160_1.png)

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_161_0.png)

*Figure 4-9. Eclipse Install dialog with update sites*

First, locate the requested plug-in’s update site URL. This is a web URL (e.g., http://download.eclipse.org/dsdp/linupdates/2.0) that hosts a specific plug-in download and future updates. The update site URL tells the Eclipse plug-in framework where to download both the plug-in and future updates to it. The update site URL for a specific plug-in version is usually published on the plug-in website.

Now configure the Eclipse plug-in framework to pull the plug-in from the update site as follows:

- 1. From the Help menu, choose the Software Updates entry (Figure 4-7).
- 2. In the Install/Update dialog that appears, choose “Search for new features to install” and click Next (Figure 4-8).
- 3. In the Install dialog, click on the “New Remote Site...” button, which displays a list of update sites (Figure 4-9).
- 4. Enter a descriptive name for the new update site (such as the plug-in name) and the update site URL from the plug-in website. Click OK.
- 5. The new site will be added to the list of available update sites. Make sure the checkbox next to the new site entry is marked and click Finish.
- 6. In the new Updates dialog that appears, check all the requested plug-ins from the available list.
- 7. Click on the Select Required button to automatically add any additional plug-ins that your chosen plug-ins depend upon.
