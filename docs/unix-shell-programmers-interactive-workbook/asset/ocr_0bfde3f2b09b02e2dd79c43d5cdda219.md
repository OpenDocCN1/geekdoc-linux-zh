# Chapter 2: Command Syntax 103

Use the set -o noclobber form in scripts and functions because it makes your programs easier to read. The set -C form can save you a few keystrokes when entering commands interactively, but you have to learn what option letter goes with what option name.

Turn on the noclobber option, and use cat with >> to make two copies of out in out1.

+   f) What commands did you type?

Answer: You could have used the following sequence of commands:
$ rm -f out1
$ touch out1
$ set -C
$ cat out out >> out1

The first two commands make sure out1 exists but is empty.

Even with noclobber set, >> redirection lets you add material to the end of an existing file.

Note that the cat command has file out appearing as a parameter twice. If you specify multiple parameters, cat reads from each of them, one after the other, so this cat command makes two copies of out in out1.

+   g) How can you verify that out1 contains two copies of out?

Answer: Because the file is so small, you could just print it out, like the following:
$ more out1
hello again
good-bye again
hello again
good-bye again
$

You could also use ls -1 to see what the file sizes are, but that wouldn't tell you whether they actually contain the same information or not.