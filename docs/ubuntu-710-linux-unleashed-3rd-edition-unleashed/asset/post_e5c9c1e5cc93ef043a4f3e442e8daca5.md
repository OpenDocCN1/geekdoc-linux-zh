
![](img/7aaa8e4f2209bf9f2fb443905096e94c_635_0.png)

FIGURE 26.1 KDE's KDevelop is a rapid prototyping and client-building tool for use with Linux.

You can begin building your project by stepping through the wizard dialogs. When you click the Create button, KDevelop automatically generates all the files that are normally found in a KDE client source directory (including the configure script, which checks dependencies and builds the client's makefile). To test your client, you can either first click the Build menu's Make menu item (or press F8) or just click the Execute menu item (or press F9), and the client is built automatically. You can use KDevelop to create KDE clients, plug-ins for the Konqueror browser, KDE kicker panel applets, KDE desktop themes, Qt library-based clients, and even programs for GNOME.

## The Glade Client for Developing in GNOME

If you prefer to use GNOME and its development tools, the Glade GTK+ GUI builder can help you save time and effort when building a basic skeleton for a program. You launch Glade from the desktop panel's Programming menu.

When you launch Glade, a directory named Projects is created in your home directory, and you see a main window, along with two floating Palette and Properties windows (see Figure 26.2, which shows a basic GNOME client with a calendar widget added to its main window). You can use Glade's File menu to save the blank project and then start building your client by clicking and adding user interface elements from the Palette window. For example, you can first click the Palette window's Gnome button and then click to create your new client's main window. A window with a menu and a toolbar appears—the basic framework for a new GNOME client!

![](img/7aaa8e4f2209bf9f2fb443905096e94c_636_0.png)

FIGURE 26.2 You can use the GNOME Glade client to build and preview a graphical interface for a custom GNOME program.

## Related Ubuntu and Linux Commands

You will use many of these commands when programming in C and C++ for Linux:

- ar—The GNU archive development tool
- as—The GNU assembler
- autoconf—The GNU configuration script generator
- cervisia—A KDE client that provides a graphical interface to a CVS project
- cvs—A project revision control system
- designer—Trolltech's graphical prototyping tool for use with Qt libraries and X
- gcc—The GNU C/C++ compiler system
- gdb—The GNU interactive debugger
- glade-2—The GNOME graphical development environment for building GTK+ clients
- gprof—The GNU program profiler
- kdevelop—The KDE C/C++ graphical development environment for building KDE, GNOME, or terminal clients
- make—A GNU project management command
- patch—Larry Wall's source patching utility
- splint—The C source file checker
- svn—The Subversion revision control system

This page intentionally left blank

## CHAPTER 27

## Mono

### IN THIS CHAPTER

- ► Why Use Mono?
- ► Mono on the command line
- ► Building on Mono's libraries
- ► Reference

Although Microsoft intended it for Windows, Microsoft's .NET platform has grown to encompass many other operating systems. No, this isn't a rare sign of Microsoft letting customers choose which OS is best for them—instead, the spread of .NET is because of the Mono project, which is a free re-implementation of .NET available under the a GPL license.

Because of the potential for patent complications, it took most distros a long time to incorporate Mono, but it's here now and works just fine. What's more, Mono supports both C# and Visual Basic .NET, as well as the complete .NET 1.0 and 1.1 frameworks (and much of the 2.0 framework too), making it quick to learn and productive to use.

## Why Use Mono?

Linux already has numerous programming languages available to it, so why bother with Mono and .NET? Here are my top five reasons:

- ► .NET is "compile once, run anywhere"; that means you can compile your code on Linux and run it on Windows, or the reverse.
- ► Mono supports C#, which is a C-like language with many improvements to help make it object-oriented and easier to use.
- ► .NET includes automatic garbage collection to remove the possibility of memory leaks.
- ► .NET uses comes with built-in security checks to ensure that buffer overflows and many types of exploits are a thing of the past.
