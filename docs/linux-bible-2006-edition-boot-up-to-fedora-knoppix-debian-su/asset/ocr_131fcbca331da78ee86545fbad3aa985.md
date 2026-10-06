# Chapter 2 ✦ Running Commands from the Shell 47

# Command-Recall Recall

After you type a command line, entire command line is saved in your shell's history list. The list is stored in a history file, from which any command can be recalled to run again. After it is recalled, you can modify the command line, as described earlier.

To view your history list, use the history command. Type the command without options or followed by a number to list many of the most recent commands. For example:

```
$ history 8
382 date
383 ls /usr/bin | sort -a | more
384 sort
385 cd /usr/local/bin
386 man
387 userid -m /home/chris -u 10 chris
388 password chris
389 history 8
```

A number precedes each command line in the list. There are several ways to run a command immediately from this list, including:

+   !—Run command line. Replace the n with the number of the command line, and that line is run. For example, here's to repeat the date command shown as command number 382 in the preceding history listing:

```
$ !382
date
Thu Apr 13 21:30:06 PDT 2006
```

+   --! Run previous command. Runs the previous command line. Here's how you'd immediately run that same date command:

```
$ !!
date
Thu Apr 13 21:30:39 PDT 2006
```

+   ?—Run command containing string. This runs the most recent command that contains a particular string of characters. For example, you can run the date command again by just searching for part of that command line as follows:

```
$ !?date?
date
Thu Apr 13 21:32:41 PDT 2006
```