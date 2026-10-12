drive space. If you plan to build programs for the Linux kernel, you need the Kernel development packages and an additional 180Mb of storage space (not counting temporary disk space required when building a new kernel).

You should also become familiar with a good text editor. Although GNU purists use the emacs editing environment to write, edit, and compile programs, many other developers do just fine with an editor such as vi or nano for editing source and then use the command line to run development tools.

When programming for GNOME or KDE, you might find it most convenient to use a graphical development project manager, such as GNOME’s Glade (the GTK+ User Interface Builder, glade-2), Trolltech’s Qt Designer (designer), or KDE’s KDevelop (the KDE development environment, kdevelop). These clients allow you to prototype an application with graphical drawing tools, which frees you to concentrate on your client’s interface. You can use either to automatically generate all necessary project and source code files for skeletal applications. See the “Graphical Development Tools” section, later in this chapter, for more information.

# ## The Process of Programming

Many Linux C programmers start by writing a program that solves an immediate need, such as a simple command-line program to download or upload phone numbers or other data to a cellular phone or handheld computer. Many beginners get started by becoming proficient in using a Linux text editor, researching any required software routines and reading documentation, browsing available Linux source code, learning how to run a compiler (such as gcc, discussed later in this chapter), and then launching into the iterative process of editing, compiling, executing, and testing.

The following sections in this chapter discuss some of the required or helpful software tools included with Fedora Core. You also see how to create, compile, and run a simple C program and how to use several graphical prototyping tools (such as Glade, Designer, or KDevelop) to shorten the process of developing a user interface for graphical programs. These tools can free up time and effort on those tasks, allowing you to concentrate on the core functions of your new program.

# ## Elements of the C/C++ Language

The C programming language has its own syntax—a specific form in which all commands and code must be written in order to be understood and processed by the computer system. The syntax you should understand when beginning to program in C includes the following:

+   - **Comments**—Comments are statements that document code and describe the program. A comment begins and ends with special characters, such as /∗ and ∗/, that tell the compiler to ignore all content between those characters.

+   - **Identifiers**—You need to know how to properly name values, variables, and subroutines, such as &a, *p, and my_func().