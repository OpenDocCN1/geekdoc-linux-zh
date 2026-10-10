*pattern* is a *regular expression*, which can be a complex specification that can match many different strings. Alphabetic and numeric characters are interpreted in a literal way in a regular expression, but some others have special meaning. For instance, if you enclose a series of letters or numbers in square braces (\[\]), the system matches any one of those characters. Suppose you want to locate all the files in */etc* that contain the strings *tty1* or *tty2*. You could enter the following command:

```
`# grep tty\[12\] /etc/*`
```

You can use *grep* in conjunction with commands that produce a lot of output in order to sift through that output for the material that’s important to you. (Several examples throughout this book use this technique.) Suppose you want to find the process ID (PID) of a running *xterm*. You can use a pipe (described shortly in the section “Using Redirection and Pipes”) to send the result of a *ps* command (described in Chapter 3, “Managing Processes and Editing Files”) through *grep*; thus:

```
`# ps ax | grep xterm`
```

The result is a list of all running processes called *xterm*, along with their PIDs. You can even do this in series, using *grep* to further restrict the output on some other criterion, which can be useful if the initial pass still produces too much output.

# ### Viewing Short Text Files and Combining Text Files

The *cat* program has nothing to do with feline pets. Rather, it’s short for the word “concatenate,” and it’s a tool for combining files, one after the other, and sending them to *standard output* (that is, your screen, GUI terminal, or remote login session; sometimes called *stdout*). One common use for *cat* is to forgo the multifile aspect of the command and display a single file. For instance, the following command displays the contents of */etc/fstab*:

```
`$ cat /etc/fstab`
```

This can be a good way to quickly view a short file. It’s much less effective for large files, though, because the start of the file will scroll off the top of the display. For very long files, it may also take a long time to display the entire file.

Another use of *cat* is to quickly combine two files into one. This is best achieved in conjunction with the redirection operator (*>*), which is described in more detail shortly. For instance, suppose you want to combine */etc/fstab* with */etc/fstab-addition*. You might issue the following command:

```
`# cat /etc/fstab fstab-addition > fstab-plus`
```

You could then examine the resulting file, *fstab-plus*. If *fstab-addition* contains a new entry you wanted to add to */etc/fstab*, copying *fstab-plus* over the old */etc/fstab* will accomplish the job. In fact, *cat* can even serve as a quick-and-dirty way to create a text file:

```
`$ cat - > text.txt`
```