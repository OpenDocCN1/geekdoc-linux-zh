Each line represents a single login session. The -H option will print column headings, in case the data is not obvious. The first column is the username, the second is the terminal line on which the user is logged in, the third is the time of the login on that terminal, and the last is the source of the login, either the host name or an X display. For example, sweiss was logged in on terminal line pts/6, the session started at 13:08 on July 26th of the then current year, and the login was initiated from a computer identified as 70.ny325.east.verizon.net. Notice that there may be multiple logins with the same username.

The output of who may vary from one system to another. Some of the reasons have to do with how systems treat users who have multiple terminal windows open in a single login or are running terminal multiplexers such as Gnu’s screen program. The w command, by the way, is approximately equivalent to the command sequence “uptime ; who”; it shows more information than who does.

# 2.4 Researching Commands In UNIX

UNIX is a self-documented operating system. You can use UNIX itself to learn how it works if you do a thorough exploration of the documentation. In particular, the man pages can be a source of information about how a command might be implemented. This information is not explicit, but can be obtained by using clues within the page. The man page for a command may not have enough content, and will instead have a message such as the following in the SEE ALSO section at the bottom:

```
The full documentation for who is maintained as a Texinfo manual.
If the info and who programs are properly installed at your site,
the command
    info coreutils ’who invocation’
should give you access to the complete manual.
```

In this case, one should use the info command instead. The info command brings up the Texinfo pages. The Texinfo system is an alternative system for providing on-line documentation. To learn how to use the Texinfo viewer, type

```
info info
```

which will bring up a tutorial on using the Texinfo documentation system. The general idea is that the information is stored in a tree-like structure, in which an internal node represents a topic area, and its child nodes are specific to that topic. The space bar will advance within the entire tree using breadth-first search. To descend into a node’s children, d (for down) works. To go back up, u (for up) works. To traverse the siblings from left to right, n (for next) does the trick, and to go back, p (for previous) works. Just picture the tree.

Note. On some systems, when you type "info coreutils who", you will see the page for the whoami command. If you move ahead a few pages, you will find the page for who. On other systems you may have to type “info who” or "info coreutils ’who invocation’” to bring up the proper pages.

The man page for who tells us that the command may be called with zero or more of the command-line options abcdImpqrsTtTu. It can also be called as follows: