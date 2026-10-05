
# Graphics, Multimedia, and Productivity Tools

# LISTING 25.5 CONTINUED

```
skel_save,
skel_exit,
skel_editpopupulldown,      /* Edit menu *//
skel_cut,
skel_copy,
skel_paste,
skel_helpopupulldown,      /* Help menu *//
skel_version;                               /* temporary storage *//
XmString skel_string;
XmAppContext skel_app;

XtSetLanguageProc(NULL, NULL, NULL);

/* give the app name and initial size */
skeleton = XtVaAppInitialize(&skel_app, "Skeleton", NULL, &0, argc, argv,NULL, XmWidth, 320, XmHeight, 240, NULL);

/* create the main window */
skel_window = XtVaCreateManagedWidget("skel", xMainWindowClass,
skeleton,
XmScrollingPolicy, XmAUTOMATIC, NULL);

/* build a menu bar across main window */
skel_menubar = XmCreateMenuBar(skel_window, "skel_menubar", NULL, 0);

/* build the pull-down menu */
skel_filepopupulldown = XmCreatePullDownMenu(skel_menubar, "File", NULL, 0);
skel_string = XmStringLocalized("File");

/* create the menu, assign ALT+F as mnemonic key */
XtVaCreateManagedWidget("File", XmCascadeWidgetClass, skel_menubar,
XmLabelString, skel_string, XmMnemonic, 'F', XmSubMenuId,
skel_filepopupulldown, NULL);

/* release storage */
XmStringFree(skel_string);

/* now add File-down menu elements */
skel_new = XtVaCreateManagedWidget("New", XmButtonGadgetClass,
skel_filepopupulldown, NULL);
skel_open = XtVaCreateManagedWidget("Open", XmButtonGadgetClass,
skel_filepopupulldown, NULL);
```

# SuSE Linux Programming Tools CHAPTER 25

# LISTING 25.5 CONTINUED

```
XtVaCreateManagedWidget("separator", xmSeparatorGadgetClass, skel_filepopupldown,
NULL);
skel_close = XtVaCreateManagedWidget("Close", xmPushButtonGadgetClass,
skel_filepopupldown, NULL);
skel_save = XtVaCreateManagedWidget("Save", xmPushButtonGadgetClass,
skel_filepopupldown, NULL);
XtVaCreateManagedWidget("separator", xmSeparatorGadgetClass, skel_filepopupldown,
NULL);
skel_exit = XtVaCreateManagedWidget("Exit", xmPushButtonGadgetClass,
skel_filepopupldown, NULL);
```

```c
/ add what to do when user selects Exit /
XtCallBack(skel_exit, XmActivateCallback, skel_exit_action, NULL);
```

```c
/ build Edit menu /
skel_editpopupulldown = XmCreatePullDownMenu(skel_menubar, "Edit", NULL, 0);
skel_string = XmStringLocalized("Edit");
XtVaCreateManagedWidget("Edit", xmCascadeDropDownItemClass, skel_menubar,
XmLabelString, skel_string, XmMnemonic, 'E', XmSubMenuId,
skel_editpopupulldown, NULL);
```

```c
/ release storage /
XmStringFree(skel_string);
```

```c
/ add Edit pull-down menu elements /
skel_cut = XtVaCreateManagedWidget("Cut", xmPushButtonGadgetClass,
skel_editpopupulldown, NULL);
skel_copy = XtVaCreateManagedWidget("Copy", xmPushButtonGadgetClass,
skel_editpopupulldown, NULL);
skel_paste = XtVaCreateManagedWidget("Paste", xmPushButtonGadgetClass,
skel_editpopupulldown, NULL);
```

```c
/ build Help menu /
skel_helpopupulldown = XmCreatePullDownMenu(skel_menubar, "Help", NULL, 0);
skel_string = XmStringLocalized("Help");
XtVaCreateManagedWidget("Help", xmCascadeDropDownItemClass, skel_menubar,
XmLabelString, skel_string, XmMnemonic, 'H', XmSubMenuId,
skel_helpopupulldown, NULL);
```

```c
/ release storage /
XmStringFree(skel_string);
```

![](img/cbac72550c7126a22162e94d91a0c360_806_0.png)

# Graphics, Multimedia, and Productivity Tools

PART IV

# LISTING 25.5 CONTINUED

```c
/* now move the Help pull-down to right side - thanks, Motif FAQ! */
XtVaSetValues(skel_menubar, XmMenuHelpWidget, XNameToWidget(skel_menubar,
'Help'), NULL);

/* now create, label, and assign action to Help menu */
skel_version = XtVaCreateManagedWidget('Version', XmPushButtonGadgetClass,
skel_helpopupulldown, NULL);
XtAddCallback(skel_version, XmActivateCallback, skel_help_action, NULL);
```

```c
XtManageChild(skel_menubar);
XtRealizeWidget(skeleton);
XtAppMainLoop(skel_app);

return (0);
```

If you have an older version of Motif, such as 2.0, use the following command line to build the client:
```bash
# gcc -o skel skeleton.c -L/usr/X11R/lib -lXm -lXpm -lXt
```

To compile this program for Motif 2.1, you need to add a new library and linker directive, like this:
```
# gcc -o skel skeleton.c -L/usr/X11R/lib -lXm -lXpm -lXt
```
These lines direct the GNU linker to look in /usr/X11R/lib directories for needed libraries. The program is then linked, using the shared Xm, Xpm, Xt, libraries. The final size of the program is fewer than 16,000 characters. You must run this Motif client during an X session (as all Motif clients are built with software libraries that still depend upon X11 graphics support). From the command line of terminal, type

```bash
# skel
```
and press Enter. If you select the Help item after the program starts, a small dialog appears, as shown in Figure 25.1.

# Using make and xmkmf

If you've created or built programs for the X Window System, you'll be familiar with Toddhoff's make utility and Jim Fulton's xmkmf command. Like the make command, SuSE Linux Programming Tools CHAPTER 25

FIGURE 25.1 The sample Motif client also provides a small Help dialog.

![](img/cbac72550c7126a22162e94d91a0c360_808_0.png)

commands help you save time, limit errors, and organize your programming tasks by automating the building process. A C preprocessor interface to make uses configuration files found under /usr/X11R/lib/X11/config directory. These files include Makefile.cf, lib.rules, lib.tmpl, rules and doc.tmpl.

The xmkmf command, which creates a Makefile from a template, is a simple shell script that runs make, telling it to define the specifics about your system and which command-line parameters need to be passed to your compiler, assembler, linker, and even formatter. Note that you should never run make by itself; always use xmkmf script instead.

Typically, after unpacking the source for an X client, you use xmkmf command and the make command to build your program. Another of the reasons many programmers use is to ensure portability. Assuming the Makefile is written properly, xmkmf command will work on nearly any UNIX system, and includes Linux.

# Note

Many programmers now include a configure script to be used when building a program for the Linux console, a client for X11, and other collections of software, especially the K Desktop Environment (or the LessTif libraries—see the following section, “LessTif—An Motif Clone”). The configure script is built with the GNU Autoconf package and creates scripts to automatically configure source packages prior to using the make command. This approach has several advantages, one of which is that the configure script is dependent of autoconf (meaning that autoconf does not need to be installed). On the other hand, Makefiles are more compact and work well with a properly configured distribution. All Linux distributions now include autoconf. For more information see autoconf GNU info.

SuSE Linux Programming Tools

# Graphics, Multimedia, and Productivity Tools

PART IV

imake works by reading an Imakefile. In turn, the Imakefile contains directions for the cpp compiler preprocessor, whose output is then fed back into imake, which generates the Makefile for your program. The magic of imake is that it simplifies the job of creating Makefiles for every possible computer or operating system your program could be built on or run under.

For example, here's a simple Imakefile for our sample program, skeleton.c:

```
INCLUDES = -I.
DEPLIBS = XClientLibs
LOCAL_LIBRARIES = XClientLibs
SRCS = skeleton.c
OBJS = skeleton.o
PROGRAMS = skel
NormalLibraryObject()
MProgramTarget(skeleton,$(LOCAL_LIBRARIES),$(SYSLibs))
```

To use this listing, type it in your favorite text editor (such as pico or nedit) and save the text as Imakefile. Then, use the two commands:

- # xmkmf
- # make

to build the program. This will also save you lot of time if you use the edit-compile-run-cycle of programming, because you won't have to retype the compiler command line shown earlier in this chapter (# gcc -o sk skeleton.c -L/usr/X11R/lib -lXm -lXpm -lXt -lxext -lX11)

# LessTif—An Alternative Motif Clone

Much of the success of Linux is a direct result of the generosity of the thousands of programmers who chose to distribute their software either for free or under the GNU General Public License. Motif, as you already know, is freeware, nor it is distributed under the GPL.

For those of us who use source code, but are on limited budgets and still want to build Motif-compliant clients without paying for a distribution, the LessTif, a Motif clone designed to be compatible with Motif 1.2. Distributed under the terms of the GPL, LessTif currently builds more than 70 Motif clients (probably many more by the time you read this).
