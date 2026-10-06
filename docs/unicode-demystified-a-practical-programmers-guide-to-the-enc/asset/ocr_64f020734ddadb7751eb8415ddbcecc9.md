144 Chapter 5 The Shell I

![](bbox=[0.44, 0.055, 0.735, 0.263])

**Figure 5-4** By default, standard input comes from the keyboard, and standard output goes to the screen/window.

# The Screen/Keyboard as Standard Input and Standard Output

When you first log in, the shell directs standard output (argument) of your commands to the device file that represents your window/screen (Figure 5-4). Directing output in this manner causes it to appear on your screen. The shell also directs standard input to come from the same file, so that your commands receive anything you type on your keyboard as input.

The cat utility provides a good example of the way screen/keyboard functions as standard input and standard output. When you use cat, it copies a file to standard output. Because the shell directs standard output to the screen, cat displays the file on the screen.

Up to this point cat has taken its input from the filename (argument) specified on the command line. When you do not give an argument (that is, when you give the command cat followed immediately by a RETURN), cat takes input from standard input. The cat utility can now be described as a utility that, when called without an argument, copies standard input to standard output, one line at a time.

To see how cat works, type cat and press RETURN in response to the prompt. Nothing happens. Enter a line of text and press RETURN. The same line appears under the one you entered. The cat utility is working. When you type a line of text using the keyboard, the shell associates that line with cat's standard input. Then cat copies your line of text to standard output, which the shell associates with the screen. This exchange is shown in Figure 5-5.

The cat utility keeps copying until you enter CONTROL-D on a line itself. Pressing CONTROL-D sends an EOF (end of file) signal to cat to indicate that it has reached the end of standard input and that there is no more text for it to copy. When you enter CONTROL-D, cat finishes execution and returns control to the shell, which gives you a