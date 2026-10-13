+   - Check to see whether you have the necessary libraries or other files that are required for a new software package to run.
+   - Check to make sure that a new package won’t conflict with one already installed on your system.
+   - Examine the procedure used to install a package, and verify that it doesn’t do anything to corrupt your system or defeat your system security.
+   - Verify that a package comes from a reliable, trusted source.
+   - Verify that a package’s files have not been corrupted or deleted.
+   - Find out other information about a package, such as where the software in it originally came from, or what restrictions exist on using or redistributing it.
+   - Upgrade to a newer version of software while preserving all your customizations to the software’s configuration files.
+   - Determine what package a particular file comes from.
+   - Surprisingly, there is much more that you can do with RPM.

> **Note**
> 
> RPM is the name of the package management system, but several different programs exist that can be used to manage your packages. A program called rpm is used to manage packages from the shell command line. This same program is used to create a package. Unfortunately, a package file itself is often referred to as an RPM because its filename ends in the extension `.rpm`. This overloaded use of the acronym can (and does) cause a lot of confusion. In this book, the package management system is referred to as RPM (all caps), the command-line utility as rpm, and an `.rpm` file as a package.

# ## WHAT IS A PACKAGE?

*A package* is a special file that contains the directories and files that are part of a particular piece of software or system component. It also contains additional information about the software that is used by the package manager. Two different kinds of packages exist: binary and source. A *binary* package contains software components that have already been built for a particular architecture and are ready to use. This is the kind you normally install on your system. A *source* package contains the source code and other items used to build the corresponding binary package. Source packages are provided in the event that you want to modify—and recompile—a program yourself.

Binary package filenames end in the suffix `.rpm`, whereas source package filenames end in the suffix `.src.rpm`. The use and manipulation of source packages is covered in Chapter 17, “Building/Rebuilding a Package,” so it is not covered here. From now on in this chapter, wherever there is an unqualified reference to a package, it is a reference to a binary package.

# ## WHAT’S IN A NAME?

A binary package has a filename that looks similar to the one shown in Figure 16.1.