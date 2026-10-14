# LISTING 4.3 WELCOME.CPP (COMMENTS ONLY)

```
// ===================================================================
// welcome.cpp - A simple C++ program
// Time-stamp: <1999-02-10 10:24:17 tswan>
// To compile:
// g++ -o welcome welcome.cpp
// To run:
// ./welcome
// Copyright (c) 1999 by Tom Swan. All rights reserved.
// ===================================================================
```

Each comment line in welcome.cpp is a C++-style comment that begins with a double slash. Various comments identify and describe the program. On the third line is a time stamp in a form that the Emacs editor recognizes (more on this in the next section). Other comments show compilation and running instructions, and the ubiquitous copyright notice. In some files, you might find additional comments at the end where I like to keep a revision history of modifications and bug fixes.

# CREATING AN AUTOMATIC TIME STAMP

If you use the Emacs text editor, you can track modifications to files with an automatic time stamp comment such as in welcome.cpp. To create a time stamp, insert the following comment in any of the first eight lines of a source code file:

```
// Time-stamp: <>
```

A similar entry works the same in any text file, but in a non-source-code file, the C++ comment delimiter, //, isn't needed. You may also write the line as a C-style comment. To enable automatic time stamping for Emacs, insert the following command into a text file named .emacs (preceded by a period) saved in your home directory:

```
(add-hook 'write-file-hooks 'time-stamp)
```

Now every time Emacs saves a file to disk, it inserts the date, time, and your login username between the time stamp's angle brackets. Saving welcome.cpp, for example, changes the time stamp to something like this:

```
// Time-stamp: <1999-02-10 10:24:17 tswan>
```

An automatic time stamp is a great way to note when you last modified a file. Later in this book (see Chapter 20, "Customizing I/O Streams"), you examine a program that prints the names of files and their automatic time stamps.

# PROGRAM ENTRY AND EXIT

Two important aspects of all programs, large and small, are how they start and how they end. As a programmer, you have certain responsibilities to ensure that your programs start correctly, but more important, to make certain they end in high style. Following are proper methods for correctly starting and ending C++ programs.