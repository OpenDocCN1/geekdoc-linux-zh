Now that we have learned to enter text in the terminal emulator, let’s try a few simple commands. Let’s begin with the date command, which displays the current time and date.

```
[me@linuxbox ~]$ date
Fri Feb  2 15:09:41 EST 2018
```

A related command is cal, which, by default, displays a calendar of the current month.

```
[me@linuxbox ~]$ cal
February 2018
Su Mo Tu We Th Fr Sa
      1  2  3
 4  5  6  7  8  9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28
```

# THE CONSOLE BEHIND THE CURTAIN

Even if we have no terminal emulator running, several terminal sessions continue to run behind the graphical desktop. We can access these sessions, called virtual consoles, by pressing CTRL-ALT-F1 through CTRL-ALT-F6 on most Linux distributions. When a session is accessed, it presents a login prompt into which we can enter our username and password. To switch from one virtual console to another, press ALT-F1 through ALT-F6. On most systems, we can return to the graphical desktop by pressing ALT-F7.

To see the current amount of free space on our disk drives, enter df.

```
[me@linuxbox ~]$ df
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/sda2      15115452  5012392   9949716  34% /
/dev/sda5      59631908 26545424  30008432  47% /home
/dev/sda1        147764    17370    122765  13% /boot
tmpfs            256856        0    256856   0% /dev/shm
```