```
$ apropos who | sort
at.allow [at]      (5) - determine who can submit jobs via at or batch
at.deny [at]       (5) - determine who can submit jobs via at or batch
fwois [whois]     (1) - query a whos or nickname database
w                  (1) - Show who is logged on and what they are doing
who               (1) - show who is logged on
whoami            (1) - print effective userid
whois             (1) - query a whos or nickname database
```

**Figure 3-9** displays man page headers that match a string

# Obtaining User and System Information

This section covers utilities that display who is using the system, what most of the users are doing, and how the system is running. If you are running GNU/Linux on a workstation that is not connected to a network, you may want to skip the rest of this chapter. (If you are set up to send and receive e-mail, read “E-Mail” on page 87).

To find out who is using the computer system, you can use one of several utilities that vary in the details they provide and the options they support. The oldest utility, which produces a list of users who are logged in on your system, the terminal connection each person is using, and the time the person is logged in.

Two newer utilities, w and finger, show more detail, such as each user’s name and the command line each user is using. You can use the finger utility (page 370) to retrieve information about users on remote systems if your computer is attached to a network.

Following these utilities, Table 3-1 on page 84 summarizes their output.

# who: Lists Users on the System

The utility who displays a list of users who are logged in. In Figure 3-10 the first column of who shows that Alex and Jenny are logged in. (Alex is logged in two locations.) The second column shows the designation of the terminal, workstation, or terminal emulator that each person is using. The third column shows the date and time person logged in.

The information that who displays is useful when to communicate with a user at your installation. When the user is logged in, you can write (page 84) to establish communication immediately. If he does not list the user or you do not need to communicate immediately, you can send that person e-mail (page 87).