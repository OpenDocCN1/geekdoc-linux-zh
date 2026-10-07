
# Graphical Development Tools

Red Hat Linux includes a number of graphical prototyping and development environments using X sessions. If you want to build client software for KDE or GNOME, you might find K, QT Designer, and Glade extremely helpful. You can use each of these programs to build graphical frameworks for interactive windowing clients, and you can use each of them to automatically generate the necessary skeleton of code needed to support a custom interface for your program.

# Using the KDevelop Client

You can launch the KDevelop client (shown in Figure 21.1) from the desktop panel's start menu of Extras, Programming menu item or from the command line of a terminal window, like this:

```bash
$ kdevelop
```

![](img/446debe023486a07fde575245cf7a3ff_744_0.png)

FIGURE 21.1 KDE's KDevelop is a rapid prototyping and client-building tool for use Linux.

After you press Enter, the KDevelop Setup Wizard runs, and you are taken through several short dialogs that set up and ensure a stable environment. You will see the main KDevelop window and can start your project by selecting KDE's Project menu and clicking the New menu item.

# CHAPTER 21 Introduction to C/C++ Programming Tools

You can begin building your project by stepping through the wizard dialogs. When you click the button, KDevelop automatically generates all the files that are normally found in a KDE client source directory (including the configure script, which checks dependencies and builds the client's myfile). To test your client, you can either first click the Build menu's Make menu item (or F8) or just click the Execute menu item (or F9), and the client is built automatically. You can use KDevelop to create KDE clients, plug-ins for the konqueror browser, KDE kicker panel applets, KDE desktop themes, QT library-based clients, and use programs for GNOME.

# Trolltech's QT Designer

A development environment that is related to KDevelop and is included with Red Hat Linux is Trolltech's QT Designer. You can use this program to build cross-platform applications. QT Designer has a complex interface that supports drawing of windows, buttons, and other client controls. You can start QT Designer from the command line of a terminal window like:

```bash
$ designer &
```

The QT Designer main window (as shown in Figure 21.2) provides tools to quickly build a graphical client. You can get started with it first creating a directory to store your project's files. Next, you can choose File, New Menu to create a new project. Then, you can select a C++ project and then save it with a name that ends with .pro.

Next, you can again use the File menu to add a file, but this time, you select a window, widget, or dialog, design the graphical interface you'd like to add to your project. After you design the project's GUI, you can test the new client. You begin by changing the directory to your project's folder (using the cd command), and then you use the qmake and make commands, like this:

```bash
$ qmake -o Makefile myproject.pro
$ make
$ ./myproject
```

# The Glade Client for Developing in GNOME

If you prefer to use GNOME and GNOME development tools, the glade client can help you save time and effort when building a basic skeleton for a program. You launch glade from the GNOME panel's Programming menu or from the command line of a terminal window, like this:

```bash
$ glade &
```

![](img/446debe023486a07fde575245cf7a3ff_746_0.png)

**Figure 21.2** Trolltech's Qt Designer is like KDevelop, a capable prototyping and client-tool for use with Linux and X.

When you launch Glade, a directory Projects is created in your home directory, and you see a main window, along with two floating palette and properties windows (see Figure 21.3). You can use Glade's File menu to save the blank project and then building your client by clicking and adding user interface elements from the Palette window. For example, you can first click the Palette window's Gnome button and then create your new client's main window. A window with a menu and a toolbar appears—the basic framework for a new GNOME client!

When you have finished building the client, you can select Build Source Code from the Project window's File menu, and Glade builds the necessary source code and scripts for the project. You can then build the project's configure script by executing the autogen.sh script in the project directory, like so:

```bash
$ autogen.sh
```

After you set up the project, as with KDevelop projects, you are ready to configure, build, and install your project. To begin that process, execute the following:

```bash
# ./configure; make install
```

![](img/446debe023486a07fde575245cf7a3ff_747_0.png)

**Figure 21.3** The GNOME client can be used to build a graphical interface for a custom GNOME program.

You need to fill in the actions for your new KDE or GNOME client, but using these rapid prototyping tools can help save development time and effort and allow you to finely tune the user interface for a program.

# Related Red Hat Linux Commands

You'll use these commands when programming in C and C++ in Red Hat Linux:

- make—A GNU archive development tool
- asm—The GNU assembler
- autoconf—The GNU configuration script generator
- cervisia—A KDE client that provides a graphical interface to a CVS
- cvs—A project revision control system
- designer—Trolltech's graphical prototyping tool for use with Qt libraries and X
- gcc—The GNU C/C++ compiler system
- gdb—The GNU interactive debugger
- glade—The GNOME graphical development environment for building GTK+ classes
- gprof—The GNU program profiler
- develop—The KDE C/C++ graphical environment for building KDE, GNOME, or terminal clients
- make—A GNU project management command
- pmake—A BSD project management command
- rc—A suite of programs used to manage project documents
- savigator—Red Hat's graphical source code analysis tool for X11
- splint—The C source file checker
- xmkmf—A shell script for X that is used to create a localized
