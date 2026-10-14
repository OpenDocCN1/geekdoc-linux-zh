# The Runlevels

In Linux, runlevels define the state of the system. Table 11-1 shows what runlevels are available.

| Command | Description |
|---|---|
| 0 | Halt |
| S | Used to boot into single-user mode (U.S. keyboard layout) |
| 1 | Single-user mode |
| 2 | Multiuser mode without network server services |
| 3 | Multiuser mode with network |
| 4 | Not used |
| 5 | Multiuser mode with network and display manager |
| 6 | Reboot |

Table 11-1

The runlevel command displays the runlevel you are currently in (second number) and the previous runlevel (first number), as in the following:

```
da10:~ # runlevel
3 5
da10:~ #
```

You can also use the who -r command, as shown in the following:

```
da10:~ # who -r
         run-level 5        Feb 14 08:43        last=3
da10:~ #
```

# init Configuration File (/etc/inittab)

To understand the contents of the /etc/inittab file, you need to know the following:

+   - inittab Syntax
+   - inittab Standard Entries

# inittab Syntax

Each line in the /etc/inittab file uses the following syntax:

```
id:rl:action:process
```

The parameters are explained here:

+   - **id**—A unique name for the entry in /etc/inittab. It can be up to four characters long.
+   - **rl**—Refers to one or more runlevels in which this entry should be evaluated.