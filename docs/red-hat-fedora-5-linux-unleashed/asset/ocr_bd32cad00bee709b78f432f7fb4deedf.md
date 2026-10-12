![](bbox=[0.14, 0.1, 0.84, 0.39])

FIGURE 33.2 Trolltech’s Qt Designer is, like KDEvelop, a capable prototyping and client-building tool for use with Linux and X.

Next you can again use the File menu to add a file, but this time, you select a window, widget, or dialog, depending on the graphical interface you’d like to add to your project. After you design the program’s GUI, you can preview your design by using the Preview menu. You can also test a build of the new client if you have added enough requisite code. You begin by navigating to your project’s folder (using the cd command), and then you use the qmake and make commands, like this:

```
$ qmake -o Makefile myproject.pro
$ make
$ ./myproject
```

# The Glade Client for Developing in GNOME

If you prefer to use GNOME and its development tools, the Glade GTK+ GUI builder (the glade-2 client) can save you time and effort when building a basic skeleton for a program. You launch glade 2 from the desktop panel’s Programming menu or from the command line of a terminal window, like this:

```
$ glade-2 &
```

When you launch Glade, a directory named Projects is created in your home directory, and you see a main window, along with two floating palette and properties windows (see Figure 33.3, which shows a basic GNOME client with a calendar widget added to its main window). You can use Glade’s File menu to save the blank project and then start building your client by clicking and adding user interface elements from the Palette window. For