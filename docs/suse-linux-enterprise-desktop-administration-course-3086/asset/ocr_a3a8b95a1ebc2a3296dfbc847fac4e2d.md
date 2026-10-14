# Objective 1—YaST Basics

YaST stands for *Yet another Setup Tool*. You can use YaST to complete many configuration tasks as a SUSE Linux Enterprise Desktop administrator.

The YaST user interface can appear in two kinds:

+   - *ncurses*—Text mode
+   - *Qt*—Fully graphical mode

The appearance of the user interface depends on which command you use to start YaST and on whether you use the graphical system or the command line, as indicated in Table 4.1.

| Command | Terminal in X Window | Command Line |
|---|---|---|
| yast2 | Qt | ncurses |
| yast | Ncurses | ncurses |

Table 4-1

In the graphical interface, you can control YaST with the mouse. To start it, select YaST from the main menu (Computer > More Applications > System > YaST). You are asked to enter the root password. See Figure 4-1.

![](bbox=[0.105, 0.498, 0.461, 0.698])

Figure 4-1

The YaST dialog appears in Figure 4-2.

To start the ncurses interface of YaST, you can start a terminal emulation from your GNOME desktop by right-clicking on the desktop background and selecting Open Terminal. See Figure 4-3.

Enter su – to get root permissions. After entering the root password, start YaST by entering yast.