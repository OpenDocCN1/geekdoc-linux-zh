its turn. Similarly, imagine multiple processes that are cooperating to compute the structure of a complex protein. Certain parts of the structure cannot be constructed until other parts have been calculated, so the processes must coordinate their activities with respect to the work accomplished by the others. Both of these situations require the use of process synchronization. The challenge is to master these concepts.

# 1.11 A First System Program

We will begin by writing a stripped down version of the more program, which displays a file one "screen" at a time. When more runs, it displays one screen’s many lines of a file and then displays information and a prompt on the very bottom line of the screen:

–More–(0%)

It then waits for the user to press a key such as the space-bar to advance to the next screen, or the Enter key to advance one line, or the "q" key to exit. The prompt is in reverse video, meaning the foreground and background terminal colors are reversed. While there are other more advanced options, we will limit our version to these alone. Run more and observe that when you press the space-bar, it responds immediately; you do not have to press the Enter key after space-bar.

# 1.11.1 A First Attempt at the more Program

The more command can be run in several ways:

```
$ more file1 file2 ... fileN
$ ls -l | more
$ more < myfile
```

The first line causes more to display the files named file1, file2, and so on until fileN, one after the other. This proves that the more program has to look at the command line arguments and use them as its input if they exist. In the second example, the output of the command "ls -l" becomes the input of the more program, and the result is that more displays the directory listing a screen at a time. This implies that more also has to work when its input comes from standard input through a pipe. In the last line, the file myfile is used as input to the more command, but the more command is simply getting input from the standard input stream.

These three examples show that more has to be able to read from a file specified on the command line as well as read from standard input, and in either case it has to output a screen at a time. Suppose that we let P represent the number of lines in a terminal window (P stands for "page", which is what a screenful of data is called.) A crude outline of the more program, ignoring the issue of where it gets its input, is:

28 The standard screen has 24 lines, but this is user-adjustable and also dependent on both hardware and system settings. Until we know how to find the actual number, we will assume a screen has 24 lines, and we write 23 new lines at a time.