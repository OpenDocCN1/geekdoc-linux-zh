# EDITING THE GENERATED MAKEFILE

I’ve usually found it necessary to make small changes to the Makefile created by the V application generator vgenx. By default, this file is named something like makefile.my, so the first step is to rename it to Makefile using these commands:

```
$ cd /home/username/vmyapp
$ mv makefile.my Makefile
```

You can now try to compile the application by typing make, but if that doesn’t work, you probably have to make some changes inside Makefile. If you are following along, load that file into your text editor and add "x" to the two include pathnames defined as follows:

```
VPATH = $(HOME)/includex
CDFLAGS = -O -I$(X11INC) -I$(HOME)/includex
```

Actually, the VPATH symbol appears to be defined but never used. These changes should allow you to type make to compile and link the generated application and then run it as follows:

```
$ make
...
$ ./my
```

Figure 29.3 shows the resulting window after I opened the sample program’s modal and modeless dialog boxes (more on these topics in the following section, "Anatomy of a V Application"). The program is a complete X client application ready for modifying with your own menu commands and other features. Feel free to play with the menus—their commands simply display a verification window and don’t do anything. The following section explains some of the generated files and classes to give an overview of how the generated V application is organized.

# Figure 29.3

The sample application’s modal and modeless dialog boxes.

![](bbox=[0.28, 0.68, 0.78, 0.9])

Note Chapter 30, "Developing X Software with V," shows my own Makefile commands and sample programs for creating V applications without using vgenx.