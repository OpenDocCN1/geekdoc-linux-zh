# Chapter 3: Compound Command Syntax 139

If a command line gets too long to fit on one line of the screen, keep typing, and the shell will recognize the full command line, even if you can't see it all on the screen. Also, you can press Enter in the middle of a command line, and the shell will automatically prompt you to continue typing, provided that it can tell that there’must be more to the-command. For example, if you press Enter after a pipe character, the shell knows that another command must follow. Finally, you can type a back-slash character (\), immediately followed by Enter and the shell will prompt for additional input, even if what you have typed so far appears to be a complete command line.

![](bbox=[0.025, 0.085, 0.105, 0.135])

LAB 3.1

Pipe the output of uniq to tee instead of to the cut command. After running the command, look at the file out.

+   f) What does tee do?
Answer: Your command lines and output should look like the following:
$ cat days days | tr a-z-Z | tr -d DAY | sort | uniq | tee out
FR
MO
ST
SU
TH
TU
WE
$ cat out
FR
MO
ST
SU
TH
TU
WE
$

The documentation for tee calls it a pipe fitting, which is pretty accurate! It splits its stdin so it goes to both its stdout and to any file(s) named as parameter(s), like directing water coming into a pipe so that it goes to two (or more) spigot.