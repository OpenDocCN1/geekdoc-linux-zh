# Chapter 23: Software Development on Ubuntu

As you might suspect from the previous paragraph, the rest of this part of the chapter focuses on installing and using the Eclipse IDE.

# Installing Eclipse

To install Eclipse and related packages, use your favorite software installation tool to install the eclipse package, which installs a huge number of associated/required packages and provides everything you need to use the standard Eclipse IDE to develop Java applications, including plugins for Java and Python development, the ant utility for building Java applications, all required libraries, and so.

See Chapter 19 for detailed information on installing applications on Ubuntu systems.

# Note

If you have problems using or installing plugins and features in the version of Eclipse that is available through the Ubuntu repositories, you can always use your favorite package management tool to remove the eclipse package, and then download and install an "official" version of Eclipse from the eclipse.org web site (www.eclipse.org/downloads). The Eclipse downloads preconfigured versions of Eclipse for Java EE developers, C/C++ developers, and so on. After downloading an archived file from the Eclipse site and extracting its contents, you can run the downloaded version of Eclipse by executing the file "eclipse" in the extracted directory. If you use this approach (which I often do to get the latest versions of Eclipse), you will not get updates for Eclipse through the standard Ubuntu Update Manager, but you can keep your versions up-to-date by using the Check for Updates menu item. On the version that you download and install, you may still want to enable and install additional Eclipse features.

# Using Eclipse for C Application Development

This section provides two examples of using Eclipse: one that shows how to create a simple application from scratch, and one that shows how to import the source code for an existing software package into Eclipse to take advantage of its compilation, debugging, and usability features. Entire books about using Eclipse, and these introductory sections are hardly equivalent to those, but they should help you get a feeling for the power, capabilities, and ease-of-use of the Eclipse IDE.

# Note

The examples in the next two sections are both programs and therefore assume that you followed the instructions in the "Installing GCC Compilers, make, and Friends" section, and installed the build-essential package, which provides user-space include files that are typically required to build C applications.

# Starting Eclipse

Installing Eclipse on your Ubuntu system creates the Applications Programming Eclipse menu entry, which you can select to start the Eclipse IDE.

The first time you start Eclipse, Eclipse displays a dialog that prompts you for a location in which to create a workspace, and then creates the workspace and eclipse directories in the specified location (usually your home directory). Unless you have a good reason to use another