# FOUR MORE UTILITIES 171

You can use a pipe to send output of a program to the printer:

# FOUR MORE UTILITIES

The echo and date utilities are two of the most frequently used members of the large collection of Linux utilities. The script utility records part of a session in a file, and todos makes a copy of a text file that can be read on either a Windows or a Macintosh machine.

# echo: DISPLAYS TEXT

The echo utility copies the characters you type on the command line after echo to the screen. Figure 5-9 shows some examples. The last example shows what the echo does with an unquoted asterisk (*) on the command line: It expands the asterisk into a list of filenames in the directory.

The echo is a good tool for learning about the shell and other Linux utilities. Some examples on page 257 use echo to illustrate how special characters, such as the asterisk, work. Throughout Chapters 7, 9, and 27, echo explains how shell variables work and how you can send messages from shell scripts to the screen. Refer to the correutils page, for more information.

optional You can use echo to create a simple file by redirecting its output to a file:

```
$ echo 'My new file.' > myfile
$ cat myfile
My new file.
```

The greater than (>) sign tells the shell to send the output of echo to the file named myfile instead of the screen. For more information refer to “Redirecting Standard Output” on page 246.

```
$ ls
memo memo.0714 practice
$ echo Hi
Hi
$ echo This is a sentence.
This is a sentence.
$ echo star: *
star: memo memo.0714 practice
$
```

Figure 5-9 echo copies the command line (but not the word echo) to the screen