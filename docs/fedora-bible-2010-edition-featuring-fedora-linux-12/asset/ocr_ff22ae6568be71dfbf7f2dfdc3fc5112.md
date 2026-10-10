# **Command-line recall**

After you type a command line, that entire command line is saved in your shell's history list.
The list is stored in a history file, from which any command can be recalled to run again. After
it is recalled, you can modify the command line, as described earlier.

To view your history list, use the `history` command. Type the **command** without options or
followed by a number to list that many of the most recent commands. For example:

```
```
$ history 8
382 date
383 ls /usr/bin | sort -a | more
384 man sort
385 cd /usr/local/bin
386 man more
387 useradd -m /home/chris -u 101 chris
388 passwd chris
389 history 8
```
```

A number precedes each command line in the list, using an exclamation point (!). Keep in
mind that with an exclamation point, the command is run blind, without giving you a chance
to confirm. There are several ways to run a command immediately from this list, including the
following:

+   *   **Run Command Number (!n)** — Replace the *n* with the number of the command line,
+       and the command line indicated is run. For example, to repeat the `date` command
+       shown as command number 382 from the previous history listing, you could type the
+       following:
+   
+       ```
+       $ !382
+       date
+       Fri Oct 16 21:30:06 PDT 2009
+       ```

+   *   **Run Previous Command (!!)** — Runs the previous command line. To run that same
+       `date` command again immediately, type the following:
+   
+       ```
+       $ !!
+       date
+       Fri Oct 16 21:30:39 PDT 2009
+       ```

+   *   **Run Command Containing String (!?string?)** — Runs the most recent command
+       that contains a particular *string* of characters. For example, you could run the `date`
+       command again by just searching for part of that command line as follows:
+   
+       ```
+       $ !?dat?
+       date
+       Fri Oct 16 21:32:41 PDT 2009
+       ```

Instead of just running a `history` command line immediately, you can recall a particular line
and edit it. You can use these keys to do that: