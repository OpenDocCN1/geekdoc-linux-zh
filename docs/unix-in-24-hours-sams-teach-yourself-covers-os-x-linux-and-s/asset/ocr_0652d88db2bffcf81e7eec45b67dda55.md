lines). I’ll look at just the first four lines of the .login file:

```
$ head -4 .login
#
# @(#) $Revision: 62.2 $

setenv TERM vt100
```

# 3. You also can easily check multiple files by listing them one by one on the command line:

Click here to view code image

```
$ head -3 .newsrc /etc/passwd
==> .newsrc ===
misc.forsale.computers.mac: 1-14536
utech.student-orgs! 1
general! 1-546

==> /etc/passwd <=
root:?:0:0:root,,,::/bin/csh
news:?:6:11:USENET News,,,:/usr/spool/news:/bin/ksh
ingres:?:7:519:INGRES Manager,,,:/usr/ingres:/bin/csh
```

# 4. More importantly, head and other Unix commands can work also as part of a pipeline, where the output of one program is the input of the next. The special symbol for creating Unix pipelines is the pipe character (|). Pipelines are read left to right, so you can easily have the output of who, for example, feed into head; this offers powerful new possibilities. If you want to see just the first five people logged in to the computer right now, try this:

Click here to view code image

```
$ who | head -5
root     console  Nov  9 07:31
mccool   ttya0    Nov 10 14:25
millek12 ttyaP    Nov 10 14:58
paulwhit ttyaR    Nov 10 14:50
bobweir  ttyaS    Nov 10 14:49
Broken pipe
```

Pipelines are one of the most powerful features of Unix, and I have many examples of how to use them to great effect throughout the remainder of this book. Stay tuned!

# 5. Here is one last thing. Find an executable—/bin/ls will do fine—and enter head -1 /bin/ls. Watch what happens. Or, if you’d like to preserve your sanity, take it from me that the random junk thrown on your screen is enough to cause your shell or terminal program to get quite confused and possibly even crash.

The point isn’t to have that happen to your system but rather to remind you that using file to confirm the file type for unfamiliar files can save you lots of grief and frustration!

head is the simplest of programs for viewing the contents of a file; it’s easy to use, it’s efficient, and it works as part of a pipeline, too. The remainder of this hour focuses on other tools in Unix that offer other ways to view the contents of text and ASCII files.