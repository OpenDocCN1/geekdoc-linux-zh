# Chapter 4: Using Linux Commands 157

```
383 ls /usr/bin  sort -a  more
384 man sort
385 cd /usr/local/bin
386 man more
387 useradd -m /home/chris -u 101 chris
388 passwd chris
389 history 8
```

A number precedes each command line in the list, using an exclamation point (!). Keep in mind that with an exclamation point, the command is run blind, without giving a chance to confirm. There are several ways to run a command immediately from this list, including the following:

+   Run Command Number (!n) — Replace the n with the number of the command line, and the command line indicated is run. For example, to repeat the date command shown as command 382 from the previous history list, you could type the following:

```
$ !382
date
Thu Oct 16 21:30:06 PDT 2016
```

+   Run Previous Command (!!) — Runs the previous command line. To run the same date command again immediately, use the following:

```
$ !!
date
Thu Oct 16 21:30:39 PDT 2016
```

+   Run Command Containing String (!*string?) — Runs the most recent command that contains a particular string of characters. For example, you could run the date command again by searching for part of that command line as follows:

```
$ !*date?
date
Thu Oct 16 21:32:41 PDT 2016
```

Instead of using a history command line immediately, you can recall a particular line and edit it. You use these keys to do:

+   Step (Arrow Keys) — Press the (↑) and down (↓) arrow keys to step through each command line in your history list to arrive the one you want. (Ctrl+p and Ctrl+n do the same functions, respectively.)

+   Reverse Incremental Search (Ctrl+r) — After you press these keys, you are asked to enter a search string to do a reverse search. As you type the string, a matching line appears that you can run or edit.

+   Reverse Search (Alt+p) — After you press these keys, you are asked to enter a string to do a reverse search. Type a string and press Enter to see the most recent command line that includes that string.