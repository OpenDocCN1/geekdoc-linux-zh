
10 lines of a file, but it can also take a numeric option specifying the number of lines to display on the terminal screen, as shown in the following example with the project4 file:

```
[root@server1 ~]# tail project4
I have been reading on the history of Algonquin Park but
no where could I find a description of where the Highland
Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth
[root@server1 ~]# tail -2 project4
Regards,
Mackenzie Elizabeth
[root@server1 ~]#_
```

Although some text files are small enough to be displayed completely on the terminal screen, you might encounter text files that are too large to fit in a single screen. In this case, the cat command sends the entire file contents to the terminal screen; however, the screen only displays as much of the text as it has room for. To display a large text file in a page-by-page fashion, you need to use the more and less commands.

The more command gets its name from the pg command once used on UNIX systems. The pg command displayed a text file page by page on the terminal screen, starting at the beginning of the file; pressing the spacebar or Enter key displays the next page, and so on. The more command does more than pg did, because it displays the next complete page of a text file if you press the spacebar but displays only the next line of a text file if you press Enter. In that way, you can browse the contents of a text file page by page or line by line. The fictitious file project5 is an excerpt from Shakespeare's tragedy Macbeth and is too large to be displayed fully on the terminal screen using the cat command. Using the more command to view its contents results in the following output:

```
[root@server1 ~]# more project5
Go bid thy mistress, when my drink is ready,
She strike upon the bell. Get thee to bed.
Is this a dagger which I see before me,
The handle toward my hand? Come, let me clutch thee.
I have thee not, and yet I see thee still.
Art thou not, fatal vision, sensible
To feeling as to sight? or art thou but
A dagger of the mind, a false creation,
Proceeding from the heat-opressed brain?
I see thee yet, in form as palpable
As this which now I draw.
Thou marshal'st me the way that I was going;
And such an instrument I was to use.

Mine eyes are made the fools o' the other senses,

Or else worth all the rest; I see thee still,

And on thy blade and dudgeon gouts of blood,

Which was not so before. There's no such thing;

It is the bloody business which informs

Thus to mine eyes. Now o'er the halfworld

Nature seems dead, and wicked dreams abuse

The curtain'd sleep; witchcraft celebrates

Pale Hecate's offerings, and wither'd murder,

Alarum'd by his sentinel, the wolf,

--More-- (71%)
```

As you can see in the preceding output, the more command displays the first page without returning you to the shell prompt. Instead, the more command displays a prompt at the bottom of the terminal screen that indicates how much of the file is displayed on the screen as a percentage of the total file size. In the preceding example, 71 percent of the project5 file is displayed. At this prompt, you can press the spacebar to advance one whole page, or you can press the Enter key to advance to the next line. In addition, the more command allows other user interactions at this prompt. Pressing the h character at the prompt displays a help screen, which is shown in the following output, and pressing the q character quits the more command completely without viewing the remainder of the file.

Most commands optionally preceded by integer argument k. Defaults in brackets. Star (*) indicates argument becomes new default.

- <space> Display next k lines of text [current screen size]
- z Display next k lines of text [current screen size]
- <return> Display next k lines of text [1]
- d or Ctrl-D Scroll k lines [current scroll size, initially 11]
- q or Q or <interrupt> Exit from more
- s Skip forward k lines of text [1]
- f Skip forward k screenfuls of text [1]
- b or Ctrl-B Skip backward k screenfuls of text [1]
- / Go to place where previous search started
- = Display current line number
- /regular expression> Search for kth occurrence of regular expression [1]
- n Search for kth occurrence of last r.e [1]
- !<cmd> or :!<cmd> Execute <cmd> in a subshell
- v Start up /usr/bin/vi at current line
- Ctrl-L Redraw screen
- :n Go to kth next file [1]
- :p Go to kth previous file [1]
- :f Display current filename and line number
- . Repeat previous command

--More-- (71%)

Just as the `more` command was named as a result of allowing more user functionality, the `less` command is named for doing more than the `more` command (remember that “less is more,” more or less). Like the `more` command, the `less` command can browse the contents of a text file page by page by pressing the spacebar and line by line by pressing the Enter key; however, you can also use the cursor keys on the keyboard to scroll up and down the contents of the file. The output of the `less` command, when used to view the `project5` file, is as follows:

```
[root@server1 ~]# less project5
Go bid thy mistress, when my drink is ready,
She strike upon the bell. Get thee to bed.
Is this a dagger which I see before me,
The handle toward my hand? Come, let me clutch thee.
I have thee not, and yet I see thee still.
Art thou not, fatal vision, sensible
To feeling as to sight? or art thou but
A dagger of the mind, a false creation,
Proceeding from the heat-opressed brain?
I see thee yet, in form as palpable
As this which now I draw.
Thou marshall'st me the way that I was going;
And such an instrument I was to use.
Mine eyes are made the fools o’ the other senses,
Or else worth all the rest; I see thee still,
And on thy blade and dudgeon gouts of blood,
Which was not so before. There’s no such thing:
It is the bloody business which informs
Thus to mine eyes. Now o’er the one half world
Nature seems dead, and wicked dreams abuse
The curtain’d sleep; witchcraft celebrates
Pale Hecate’s off’rings, and wither’d murder,
Alarum’d by his sentinel, the wolf,
Whose howl’s his watch, thus with his stealthy pace.
project5
```

Like the `more` command, the `less` command displays a prompt at the bottom of the file using the : character or the filename of the file being viewed (`project5` in our example), yet the `less` command contains more keyboard shortcuts for searching out text within files. At the prompt, you can press the h key to obtain a help screen or the q key to quit. The first help screen for the `less` command is shown next:

```
SUMMARY OF LESS COMMANDS
Commands marked with * may be preceded by a number, N.
Notes in parentheses indicate the behavior if N is given.
A key preceded by a caret indicates the Ctrl key; thus ^k is ctrl-K.
 h H Display this help.
 q :q Q :Q ZZ Exit.
```

### MOVING

- e `^E` j `^N` CR * Forward one line (or N lines)
- y `^Y` k `^K` `^P` * Backward one line (or N lines)
- f `^F` ^V SPACE * Forward one window (or N lines)
- b `^B` ESC-[ * Backward one window (or N lines)
- z * Forward one window (and set window to N)
- w * Backward one window (and set window to N)
- ESC-SPACE * Forward one window, but don't stop at end-of-file
- d `^D` * Forward one half-window (and set half-window to N)
- u `^U` * Backward one half-window (and set half-window to N)
- ESC-( RightArrow * Left 8 character positions (or N positions)
- ESC-) LeftArrow * Right 8 character positions (or N positions)
- F * Forward forever; like "tail -f"

HELP -- Press RETURN for more, or q when done

The more and less commands can also be used in conjunction with the output of commands if that output is too large to fit on the terminal screen. To do this, simply use the `|` metacharacter after the command, followed by either the more or less command, as follows:

```
[root@server1 ~]# cd /etc
[root@server1 etc]# ls -1 | more
total 3680
-rw-r-r-- 1 root  root  15276 Mar 22 12:20 a2ps.cfg
-rw-r-r-- 1 root  root  2562 Mar 22 12:20 a2ps-site.cfg
drwxr-xr-x 4 root  root  4096 Jun 11 08:45 acpi
-rw-r-r-- 1 root  root  46 Jun 16 16:42 adjtime
drwxr-xr-x 2 root  root  4096 Jun 11 08:47 aep
-rw-r-r-- 1 root  root  688 Feb 17 00:35 aep.conf
-rw-r-r-- 1 root  root  703 Feb 17 00:35 aeplog.conf
drwxr-xr-x 4 root  root  4096 Jun 11 08:47 alchemist
-rw-r-r-- 1 root  root  1419 Jan 26 10:14 aliases
-rw-r-r-- 1 root  smmsp 12288 Jun 17 13:17 aliases.db
drwxr-xr-x 2 root  root  4096 Jun 11 11:11 alternatives
drwxr-xr-x 3 amanda disk 4096 Jun 11 10:16 amanda
-rw-r-r-- 1 amanda disk  0 Mar 22 12:28 amandates
-rw------- 1 root  root  688 Mar 4 22:28 amd.conf
-rw-r-r--- 1 root  root  105 Mar 4 22:34 amd.net
-rw-r-r-- 1 root  root  317 Feb 15 14:33 anacrontab
-rw-r-r-- 1 root  root  331 May 5 08:07 ant.conf
-rw-r-r-- 1 root  root  6200 Jun 16 16:42 aouned.state
drwxr-xr-x 3 root  root  4096 Jun 11 10:37 atalk
-rw----- 1 root  root  1 May 5 13:39 at.deny
-rw-r-r-- 1 root  root  325 Apr 14 13:39 auto.master
-rw-r-r-- 1 root  root  581 Apr 14 13:39 auto.misc
--More--
```

In the preceding example, the output of the `ls -l` command was redirected to the more command, which displays the first page of the output on the terminal. You can then advance
