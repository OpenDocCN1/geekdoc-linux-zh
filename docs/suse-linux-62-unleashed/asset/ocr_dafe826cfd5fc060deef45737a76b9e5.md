# Graphics, Multimedia, and Productivity Tools

PART IV

# LISTING 25.5  CONTINUED

```
* now move the Help pull-down to right side - thanks, Motif FAQ! */
XtVaSetValues(skel_menubar, XmmenuHelpWidget, XNameToWidget(skel_menubar,
'Help'), NULL);

* now create, label, and assign action to Help menu *
skel_version = XtVaCreateManagedWidget('Version', XmpushButtonGadgetClass,
skel_helppulldown, NULL);
XtAddCallback(skel_version, XmactivateCallback, skel_help_action, NULL);
```

```
XtManageChild(skel_menubar);
XtRealizeWidget(skleton);
XtAppMainLoop(skel_app);

return (0);
```

If you have an older version of Motif, such as 2.01, use the following command line to build the client:

```
# gcc -o skel skeleton.c -L/usr/X11R6/lib -lXm -lXpm -lXt -X11
```

To compile this program for Motif 25.1, you need to add a new library and linker directive,
 like this:

```
# gcc -o skel skeleton.c -L/usr/X11R6/lib -lXp -lXm -lXpm -lXt -Xext -X11
```

These lines direct the GNU linker to look in the /usr/X11R6/lib directories for needed
libraries. The program is then linked, using the shared Xp, Xm, Xpm, Xt, Xt, and X11
libraries. The final size of the program is fewer than 16,000 characters.

You must run this Motif client during an X Window session (as all Motif clients are built
with software libraries that still depend upon X11 graphics support). From the command
line of terminal, type

# skel

and press Enter. If you select the Help menu item after the program starts, a small dialog
appears, as shown in Figure 25.1.

# Using make and xmkmf

If you've created or built programs for the X Window System, you'll be familiar with Todd
Brunhoff's make utility and Jim Fulton's xmkmf command. Like the make command, we