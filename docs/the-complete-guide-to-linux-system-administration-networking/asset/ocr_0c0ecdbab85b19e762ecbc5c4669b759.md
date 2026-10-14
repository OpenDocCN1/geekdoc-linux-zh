# Table 9-1 Run Levels in Linux

| Run level | Name | Description |
|---|---|---|
| 0 | Halt | Shuts down all services when the system will not be restarted |
| 1 | Single-user mode | Used for system maintenance. Does not require logging in with a user name and password—operates as root. Does not provide networking capabilities. |
| 2 | Multiuser mode with out networking enabled | Rarely used except for system maintenance or testing |
| 3 | Regular multiuser networking mode | Standard multiuser text-mode operation; non-graphical systems (such as network servers) use this mode for normal operation |
| 4 | - | Not used |
| 5 | Graphical login | Identical to run level 3 except a graphical login is used |
| 6 | Reboot | Shuts down all services so the system can be restarted |

The run level that the init program starts when Linux is booted is defined in the /etc/inittab file. For a typical Red Hat Linux or Fedora system, the default run level is 5, indicating that the system should start in multiuser mode, with networking enabled, using a graphical login screen.

The id: line in /etc/inittab defines the default run level used by init. You can change the 5 to a 3 and restart your computer to see how a nongraphical login appears. The last line in the /etc/inittab file, beginning with an x:, defines the program that init starts to provide the graphical login screen.

By using the init or telinit command (they are equivalent), you can tell the init program to change to a different run level. This is commonly done only to restart or halt the system. For example, entering this command restarts the system:

```
# telinit 6
```

You learned in Chapter 6, "Managing Processes," about virtual consoles. Each is defined in /etc/inittab. Six lines similar to this line appear in /etc/inittab:

```
1:2345:respawn:/sbin/mingetty tty1
```

This line tells init that it should start the mingetty program, which provides a login prompt. This program is handed the parameter tty1, the first virtual console. The init program respawns (restarts) the mingetty program if it exits, so the virtual console stays active. The first 1 is simply a label; the second set of numbers, 2345, indicates the run levels for which this line will be used—everything except the special purpose levels, 0, 1, and 6. Project 9-3 describes how you can edit the /etc/inittab file to add an additional virtual console.