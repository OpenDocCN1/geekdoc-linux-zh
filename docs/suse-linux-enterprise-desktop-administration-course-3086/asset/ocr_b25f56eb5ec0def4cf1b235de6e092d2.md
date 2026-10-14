# Part IV: Delete the Copied File and Empty the Trash

To delete the copied file and empty the trash, do the following:

+   1. Delete the example.txt file by dragging the file icon over the Trash icon on the desktop, and releasing the mouse button.
+   2. Close the Nautilus file manager window.
+   3. Right-click the Trash icon on the desktop and select Empty Trash from the pop-up menu.
+   4. In the confirmation dialog, select Empty Trash.

# Objective 3—Access the Command-Line Interface from the Desktop

A classic multiuser environment can be implemented by connecting several terminals (dialog stations)—monitor and keyboard units—to the serial interface of a single computer. Linux also supports multiterminal environments, allowing you to connect several terminals to the serial interfaces of a Linux system.

Serial terminals are rarely used; instead, virtual terminals were created in Linux. With virtual terminals, you can work in Linux as if you had several classic serial terminals available at the same time.

You can have up to six virtual terminals (F1-F6) running on your computer. By pressing Ctrl+Alt+Fx, you can switch between individual terminals. By pressing Ctrl+Alt+F7, you can switch back to your graphical user interface.

You can determine the terminal currently being used from the tty number (tty1–tty6). tty is an abbreviation for teletype, which is another word for terminal.

When you switch to a virtual terminal, a login prompt appears:

```
```text
Welcome to SUSE Linux Enterprise Desktop 10 (i586) -
Kernel 2.6.16.46-0.4-default (tty1).
dalo login:
```
```

From here you can enter your login name and password. To log out, type exit and press Enter.

In addition to using the virtual terminals, you can start a terminal emulation from your GNOME desktop by selecting GNOME Terminal (shown in Figure 2-18) or X Terminal from the main menu. Both belong to the System application group.