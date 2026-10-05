may look like it's hanged but waits for keyboard input. Try pressing <Ctrl>d (which means "end-of-file") to see that this will satisfy the "cat" command. Another example: I have seen many questions on the newsgroups about the "buggy" tar command that "hangs" when trying to uncompress a downloaded file, for example:

```
tar -xzv my_tar_file
```

This waits for user input, since no option "-f filename" was specified the second parameter "my_tar_file" was not recognized as file. The correct command is:

```
tar -xvmf my_tar_filename
```

Please note that the filename must follow immediately after the option "f" (which stands for "filename. This WILL NOT work (very common mistake):

```
tar -zxvf my_tar_file
```

**Any program (hanged or not) can be killed.** A text-mode program in the foreground can be killed by pressing <Ctrl>C. This will not work for larger applications which block the <Ctrl>C, so it is not used on them accidentally. Still you can get back in control by sending the program to the background by pressing <Ctrl>z (no guarantee this will work) or switching to a different terminal, for example using <Ctrl><+Alt><+F2> and login as the same user that hanged the program (this should always work). Once you are back in control, find the program you want to terminate, for example:

```
ps
```

This command stands for "print status" and shows the list of programs that are currently being run the current user. In the ps output, I find the process id (PID) of the program that hanged, and now I can kill it. For example:

```
kill 123
```

will kill the process with the process id (PID) of "123".

As user, I can only kill the processes I own (this is, the one I started). The root can kill any process. To see the complete list of all processes running on the system issue:

```
ps axu | more
```

This lists all the processes running (option "a"), even without the controlling terminal (option "x"), and together with the login name of the user that owns each process ("u"). The display is likely to be longer than one screen, use the "more" pipe so that the display stops after each screen.

The kill command has a shortcut killall to kill programs by name, for example: