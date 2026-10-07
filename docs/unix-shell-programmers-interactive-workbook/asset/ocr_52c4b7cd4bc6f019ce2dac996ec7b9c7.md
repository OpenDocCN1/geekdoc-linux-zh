# 520 Lab 11.2: The exec Command

Inside a script the standard I/O fds (0, 1, and 2) will be copies of those in effect in your interactive shell, but all fds greater than number 2 will be closed. However, all the interactive shell's fds will still be open when control returns to it.

![](bbox=[0.143, 0.101, 0.222, 0.163])

+   b) What do the last two lines do?
Answer:They close the two fds that were opened by the first command lines.

LAB 11.2

Closing files when you are finished with them is a good thing to do, although failing to do so will generally not have much effect on your life. Doing so prevents your program from doing more reads or prints using the fd until it is opened again. You saw that m&n is the syntax for connecting fd m to the same file or device as fd in Lab 2.3, "Redirect Input and Output." Now you can see that using a dash ( ) for n means that fd m gets closed and cannot be used for I/O.

+   c) What does the -ru3 on the read command accomplish?
Answer:It makes the command read from the first input file.

The -r part says to treat backslashes ( \ ) at the ends of lines as normal characters rather than line-continuation characters. The u3 part says to read from fd number 3. You could have typed this as -r -u3, if you prefer.

> It's always a good idea to use -r when you read from a file; line continuation is really designed for interactive use.

![](bbox=[0.143, 0.6, 0.222, 0.66])

+   d) What do the quotes around the reference to REPLY accomplish?
Answer:They preserve the spacing in the lines being printed.

The IFS variable was set to the empty string before entering the loop that does the shuffle so that no token splitting would be done by the two read commands inside the loop, and the print commands used to prevent the spacing from being lost in the output. The value of IFS is restored to its default value after doing the copying, so that the read command asking for the next two file names will do token splitting as required.