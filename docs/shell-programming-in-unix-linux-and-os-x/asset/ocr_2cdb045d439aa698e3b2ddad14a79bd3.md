As an example, recall that executing the who command results in the display of all users that are currently logged-in. More formally, the who command writes a list of the logged-in users to standard output. This is depicted in Figure 1.10.

![](bbox=[0.142, 0.233, 0.657, 0.453])

Figure 1.10 who command

It turns out that just about every single Unix command can take the output of a previous command or file as its input too, and can even send its output to another command or program. This concept is hugely important to understanding the power of the command line and why it's so helpful to know all of these commands even when a graphical interface might be also available for your use.

Before we get there, however, consider this: if the sort command is invoked without argument, the command takes its input from standard input. With standard output, this is your terminal (or keyboard) by default.

When input is entered this, an end-of-file sequence must be specified after the last line is typed, and by Unix convention, that Ctrl+d; is the sequence produced by simultaneously pressing the Control (or Ctrl, depending on your keyboard) key and the d key.

As an example, let's use the sort command to sort the following names: Tony, Barbara, Harry, Dirk. Instead of first entering the names into a file, we'll enter them directly from the terminal:

```
$ sort
Tony
Barbara
Harry
Dirk
Ctrl+d
```