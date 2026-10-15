Note that some of these commands require you to use additional fields, such as the names of files.

Tracking information is usually contained in separate control files; each document within a project might contain information that is automatically updated with each change to a project. A process called keyword substitution is used to perform these automatic updates. CVS uses keywords included inside C comment strings (/ * * /) near the top of a document. The following are some of the available keywords:

+   - $Authors$—The username of the person who performed the last check-in
+   - $Date$—The date and time of the last check-in
+   - $Id$—Same as $Header$, but without a full pathname
+   - $Name$—A symbolic name (see the co man page)
+   - $Revision$—The assigned revision number (such as 1.1)
+   - $State$—The state of the document, such as Exp for experimental, Rel for released, or Stab for stable

Getting started with CVS requires that you initialize a repository by first setting the $CVSROOT environment variable with the full pathname of the repository and then using the init command option with the cvs command, like this:

```
# cvs init
```

You can find documentation for CVS in various man pages, under the /usr/share/doc directory, and in GNU information documents.

With Subversion, you automatically get a new svnroot directory when you check out a Subversion tree. This creates a .svn directory in that folder, and from then on you can issue Subversion commands without having to authenticate with the server.

# Debugging Tools

Debugging is both a science and an art. Sometimes, the simplest tool—the code listing—is the best debugging tool. At other times, however, you need to use other debugging tools. Three of these tools are splint, gprof, and gdb.

# Using splint to Check Source Code

The splint command is similar to the traditional UNIX lint command: It statically examines source code for possible problems, and it also has many additional features. Even if your C code meets the standards for C and compiles cleanly, it might still contain errors. splint performs many types of checks and can provide extensive error information. For example, this simple program might compile cleanly and even run:

```
$ gcc -o tux tux.c
$ ./tux
```