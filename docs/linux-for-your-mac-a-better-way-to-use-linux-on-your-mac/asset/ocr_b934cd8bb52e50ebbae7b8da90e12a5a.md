5 + 6 6 KDE 2.1.1 help Dimitris Andavoglou
6 + 2 15 KDE 2.1.1 anti-aliasing Bob Raymond
7 + 4 28 Caldera Workstation or: Open Beta Fox7777
8 + 7 24 CDR on eDesktop 2.4 1198
9 + 2 11 Upgrade Caldera OpenLinux 2.3 to 2.4 Eduard de Vries
10 + 4 35 XFce 4.0.3 problems Robert Gelb
11 + 11 Anti-aliasing in KDE 2.1.1 Robert Gelb
12 + 2 11 KDat + KDE Ulrich Mensefeld
13 + 14 16 Linux commands John Aifab Alam
14 + 5 6 Kernel Update Ed
15 + 3 15 Kernel2.4.3 problem Dimitris Andavoglou
16 + 2 11 MySQL Startup Script under eServer 2.3 Mathis Moder

```
<*>=set current to n; TAB-next unread; /-search pattern; ^X kill/select;
a}uthor search; clatchup; j=line down; k=line up; K=mark read; l=list thread;
|=pipe; m|all; o=print; q/uit; r=toggle all/unread; s|ave; t|ag; w=post
```

As you can see, tin uses single-letter commands. This is how nearly all console-based newsreaders work. Once you pick a newsreader, you will become very proficient at reading and navigation within a few sessions.

# ## Using slrn

The slrn newsreading client is a console-based reader that features colors and an easy-to-use split interface. The split window, shown in Figure 9.24, allows you to browse subjects while reading a message. This client may be launched from the desktop's panel or the command line of an X Window terminal, like this:

```
$ slrn -n -c
```

This command line tells slrn to not check for any new newsgroups that have appeared on your ISP's news server. The -c option specifies the use of color for reading messages. After you press Enter, you will see slrn's main window.

As with many e-mail clients and newsreading programs, slrn responds to single-letter commands. You can type a question mark at any time to get help. Note that slrn will use the default system editor to edit follow-up replies or compose posts. So if you do not want to end up using the vi editor, you can define a different system editor, such as pico, like this:

```
$ export EDITOR=/usr/bin/pico
```