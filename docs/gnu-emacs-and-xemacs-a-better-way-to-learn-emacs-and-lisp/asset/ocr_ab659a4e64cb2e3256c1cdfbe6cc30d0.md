# makefile-mode

When you load a makefile into an Emacs session, a special mode designed for this type of file becomes active, as shown in Figure 16.15. This mode provides font locking, several motion and completion key commands, and a menu. You can open a simple Makefile Browser window, but using Speedbar in conjunction with makefile-mode is much more intuitive and useful, as shown in Figure 16.16.

The motion commands are similar to those in the programming modes. Several useful key commands aren't included on the menu, such as Ctrl-c Ctrl-l, which appends backslashes to the lines in a selected region. This forces the make program to see several consecutive lines as one long line. The mode help key Ctrl-h m shows you a complete list of makefile-mode keybindings.

# EDE: The Emacs Development Environment

Eric Ludlam has been developing several interesting packages that significantly enhance Emacs. The Speedbar is one, and several others were mentioned earlier as required packages for a JDE installation.

One of his packages complements and extends compile-mode: The Emacs Development Environment (EDE) emulates commercial IDEs through its usage of the concept of a development project. A project can be more than just a directory

![](bbox=[0.04, 0.6, 0.8, 0.87])

Figure 16.15   makefile-mode