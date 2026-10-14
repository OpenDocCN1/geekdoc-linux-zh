In text mode, there are six virtual consoles available. Switch between them using `(Alt + F1)` to `(Alt + F6)`. The seventh console is reserved for X11. By modifying the `/etc/inittab` file, assign more or fewer consoles. To switch to a console from X11 without leaving X11, use `(Ctrl + Alt + F1)` to `(Ctrl + Alt + F6)`. `(Alt + F7)` then returns to X11.

# Keyboard Layout

To standardize the keyboard mapping of programs, changes were made to the following files:

```
```text
/etc/inputrc
/usr/X11R6/lib/X11/Xmodmap
/etc/skel/.Xmodmap
/etc/skel/.exrc
/etc/skel/.less
/etc/skel/.lesskey
/etc/csh.cshrc
/etc/termcap
/usr/lib/terminfo/x/xterm
/usr/X11R6/lib/X11/app-defaults/XTerm
/usr/share/emacs/(VERSION)/site-lisp/term/*.el
/usr/lib/joerc
```
```

These changes only affect applications that make use of terminfo entries or whose configuration files are changed directly (vi, less, etc.). Other non-SuSE applications should be adjusted to these defaults.

Under X, the compose key (“multikey”) can be accessed using the key combination `(Ctrl + Shift)` (right). Also see the corresponding entry in `/usr/X11R6/lib/X11/Xmodmap`.