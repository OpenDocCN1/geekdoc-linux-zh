# Using Streams, Redirection, and Pipes

> > NOTE
>> Part of the Unix philosophy to which Linux adheres, whenever possible, to do complex things by combining multiple tools. Redirection and pipes help in this task by enabling simple programs to be combined in chains, each link feeding the output of the preceding link.

# Exploring Types of Streams

To begin understanding redirection and pipes, you must first understand the different types of input and output streams. Three are most important for this topic:

**Standard Input** Programs accept keyboard input via *standard input*, or stdin. In most cases, this is the data that comes into the computer from a keyboard.

**Standard Output** Text-mode programs send most data to your users via *standard output* (aka stdout), which is normally displayed on the screen, either in a full-screen text-mode session or in a GUI window as an *xterm*. (Fully GUI programs as GUI word processors do not use standard output for their regular interactions, they might use standard output to display messages in the terminal when they were launched. GUI output is not handled via an output stream in the sense I'm describing here.)

**Standard Error** Linux provides a second type of output stream, known as *standard error*, or stderr. This output stream is intended to carry high-priority information such as error messages. Ordinarily, standard error is sent to the same output device as standard output, though this can be handy. For instance, you can redirect standard error to a file leaving standard output going to the screen so that you can interact with the program and then study the error messages.

Internally, programs treat these streams just like data files—they open or to write to the files, and close them when they're done. Another way, ordinary files are streams from a program's point of view. The standard input, output, and error streams just happen to be the ones used to interact with users.

# Redirecting Input and Output

To redirect input or output, you use symbols following the command, including any options it takes. For instance, to redirect the output of the echo command, you would type something like this:

```
$ echo $NNTPSERVER > nntserver.txt
```

The result is that the file nntserver.txt contains the output of the command (in this case, the value of $NNTPSERVER environment variable). Redirection operators exist to achieve several effects, as summarized in Table 1.2.