![](bbox=[0.22, 0.15, 0.28, 0.2])

The colors you can use for the color settings are listed in the file rgb.txt under the /usr/X11R6/lib/X11 directory.

Use these options, and others (such as X11 resource settings, discussed in Hour 7, “Using the X Window System”) to customize how xemacs looks when started in X11:

```
# emacs -geometry 80x24 -fg black -bg white blue -cr red
```

This starts xemacs in a window 80 characters wide and 24 lines high. The text is black with a white background. The cursor is red, and the mouse cursor is blue. Emacs also has 43 different X resource settings you can configure and enter into your .Xresources file in your home directory. You can also save editor defaults (such as word wrapping, or fill-mode on) in a file called .emacs in your home directory.

For example, you can automatically put xemacs into a text- and word-wrap mode, enable daily diary service, and put the current time in the modeline, a status bar in the main window. Create the .emacs file with xemacs, like this:

```
# xemacs .emacs
```

```
(setq default-major-mode 'text-mode)
(setq text-mode-hook 'turn-on-auto-fill)
(require 'appt)
(display-time)
(appt-initialize)
```

Press Ctrl+X and Ctrl+S to save the file, and then press Ctrl+X and Ctrl+C to exit xemacs. The next time you start the editor, you see the time displayed in the modeline.

The xemacs program for OpenLinux comes in 14 different packages containing various files and utilities. If you install everything, emacs requires more than 60 megabytes of disk space. You can, however, save 45 megabytes if you install the xemacs package, which contains the editor, documentation, and support routines.

You can find documentation for xemacs under the /usr/info/xemacs directory. You also can read the xemacs manual page for an overview.

# Variants of the Visual iMproved Editor —vim

The vim editor, by Bram Moolenaar, is a text editor that is compatible with the original Berkeley Software Distribution vi editor by Bill Joy. An X11 version is called gvim and sports multiple scrolling windows and menus.