program. The `ls` utility uses the `isatty()` system call to determine whether output is going to the screen (a tty). In addition, `ls` can use another system call to determine the width of the screen it is sending output to; with this information it can modify its output to fit the screen. Compare the output of `ls` by itself and when you send it through a pipeline to `less`. See page 1020 for information on how you can determine whether standard input and standard output of shell scripts is going to/coming from the terminal.

# ## THE SCREEN AS A FILE

Chapter 6 discusses ordinary files, directory files, and hard and soft links. Linux has an additional type of file: a *device file*. A device file resides in the file structure, usually in the /dev directory, and represents a peripheral device, such as a terminal, printer, or disk drive.

The device name the *who* utility displays following a username is the filename of the terminal that user is working on. For example, when *who* displays the device name pts/4, the pathname of the terminal is /dev/pts/4. When you work with multiple windows, each window has its own device name. You can also use the *tty* utility to display the name of the device that you give the command from. Although you would not normally have occasion to do so, you can read from and write to this file as though it were a text file. Reading from the device file that represents the terminal you are using reads what you enter on the keyboard; writing to it displays what you write on the screen.

# ## THE KEYBOARD AND SCREEN AS STANDARD INPUT AND STANDARD OUTPUT

After you log in, the shell directs standard output of commands you enter to the device file that represents the terminal (figure 5-3). Directing output in this manner causes it to appear on the screen. The shell also directs standard input to come from the same file, so commands receive as input anything you type on the keyboard.

The *cat* utility provides a good example of the way the keyboard and screen function as standard input and standard output, respectively. When you run *cat*, it copies a file to standard output. Because the shell directs standard output to the screen, *cat* displays the file on the screen.

Up to this point *cat* has taken its input from the filename (argument) you specify on the command line. When you do not give *cat* an argument (i.e., when you give the command *cat* followed immediately by RETURN), *cat* takes its input from standard input. Thus, when called without an argument, *cat* copies standard input to standard output, one line at a time.

To see how *cat* works, type *cat* and press RETURN in response to the shell prompt. Nothing happens. Enter a line of text and press RETURN. The same line appears just under the one