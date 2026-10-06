output of one command to the filter's standard input. Another pipe connects the filter's standard output to standard input of another command. Not all utilities can be used as filters.

In the following example sort is a filter, taking standard input from standard output of who using a pipe to redirect standard output to standard input of lpr. The command line sends the sorted output of who to the printer:
The utilities were not specifically designed to work with each other, but they all use standard input and standard output in the conventional way. By using the shell to handle input and output, you can piece standard utilities together on the command line to achieve the results you want.

```
$ who | sort | lpr
```

# tee: Sends Output in Two Directions

In a pipe the tee utility sends the output of a command to a file and also to standard output. The utility is aptly named: It takes a single input and sends the output in two directions. In Figure 5-15 the output of who is sent via a pipe to standard input of tee. The tee utility saves a copy of standard input in a file named who and also sends a copy to standard output. Standard output of tee goes via a pipe to standard displays lines containing the string root.

$ who | tee who.out | grep root
root console Mar 27 05:00
$ cat who.out
root console Mar 27 05:00
alex pts/4 Mar 27 12:23
alex pts/5 Mar 27 12:33
jenny pts/7 Mar 26 08:45

**5-15** Using tee

# Running a Program in the Background

In all the examples so far in this book, commands were run in the *foreground*. When you run a command in the foreground, the shell waits for it to finish before