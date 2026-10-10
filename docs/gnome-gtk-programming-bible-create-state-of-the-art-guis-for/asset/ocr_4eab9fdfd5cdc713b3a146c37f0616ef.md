One of the great advantages of open source is that you can go and look inside a function to see what it *really* does when you call it. Open-source documentation lags behind open-source programming (sometimes so far behind you can't even see it). And, even when you have the documentation, it may leave out that one little tidbit of information you need. For this reason, you need to have the source tucked away somewhere so you can take a peek at it whenever you get stuck.

One very important reason to have the source code is to prevent memory leaks. For example, if a function returns a pointer to a string, you need to know whether it is returning the address of a static string, or whether string is allocated. If you don't free an allocated string, that's a *memory leak*. If you attempt to free a static string, you produce a *runtime error*.

The organization described in this chapter follows the organization used by GNOME and GTK+. By exploring the source directories, you can find examples of the things described in this chapter. This should give you a good idea of the structure, as well as the sort of things you are able to do.

# Set Up the Development Directory

The first job is to create a directory where all development is to take place. This directory will hold some of the basic configuration files and scripts used to configure and control compilation. It also will have subdirectories that contain some system macros and your source code.

There are some things that you need to do only once. After this initial directory is set up, it is easy to add new projects. This structure gives you the flexibility to add source code for new systems and subsystems as needed. Of course, you don't have to do all of your development in the same directory tree; but because there is a bit of initial configuration and setup to do, it usually is a good idea to do it this way. Adding a new development project to an existing configuration is simply a matter of adding a subdirectory or two, putting the source into the new directory, and setting the configuration settings so the directory is found and the source compiled.

A sort of 'minimal' development root directory contains the following files and directories:

+   - AUTHORS
+   - ChangeLog
+   - IDGBIBLE
+   - Makefile.am
+   - NEWS
+   - README
+   - acconfig.h
+   - autoconf.sh
+   - configure.in
+   - helloauto/
+   - macros/