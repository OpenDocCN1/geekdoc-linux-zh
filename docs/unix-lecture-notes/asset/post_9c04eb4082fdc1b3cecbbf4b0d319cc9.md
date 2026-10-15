
key and counting the number of characters output on the screen to make sure none were lost. We are not allowed to redirect input to copychars to facilitate this because redirecting input will imply that the terminal is not involved in supplying characters to the program, so we have to do this in a more tedious way. We do not have to type the characters one at a time, but can create files containing the required number of characters on a single line, and if our terminal emulator supports copy and paste, we can paste them into the terminal window and then press the Enter key. We are free to redirect output to the wc command to count the number of characters written to standard output.

We can create a file named a_N containing N consecutive 'a' characters with the command

```
$ ( for i in `seq 1 1 N` ; do echo -n 'a' ; done ) > a_N
```

where N is replaced by the desired number. Suppose we create such files of sizes 128, 256, 512, 1024, 2048, 4096, 8192 characters. We can open each file in a text editor, copy the sequence to the clipboard and paste it into the window after running the command

```
$ copychars | wc
```

We will see the following sequence of numbers output by wc

2   13   198
2   13   326
2   13   582
2   13   1094
2   13   2118
2   13   4165
2   13   4165

As you can see, the maximum number of characters reported by wc is 4165. Subtract the length of the prompt and the following newline, 70 characters, and you see that 4095 characters seems to be the maximum size of the buffer on the system used for this experiment. We will see shortly that this number is much larger than the documentation states. Where these characters are stored cannot be answered experimentally. That question requires some research.

Try one other thing. Run copychars, but this time, use your backspace key to change some of the characters. When you press the Enter key this time, there is no trace of that backspace character. It is not part of the stream of characters that the program received. The characters seem to be stored in the buffer in such a way that we can use editing keys to remove them from the set of characters delivered to the program.

Before we go further, and as a sort of advance peek at what we are about to do, try running the program as follows. Type the commands as they appear below:

```
$ stty -icanon ; copychars
```

When you are finished observing what happens, type the command

First, notice that no output took place until the Enter key was pressed. Once again, this means that the characters that were typed before the Enter key was pressed had to be stored in a buffer.

Second, unlike our copychars program, this lets us see the character codes of the characters that we enter. It seems that there was a character after the 'e' but before the 'D, and that this character caused a new line to appear on the screen and then caused "code = 10" to appear after it. But we pressed the Enter key after the 'e'. The fact that the second quote is in the first column on the next line implies that two characters were transmitted: a linefeed, ASCII 10, was transmitted to the screen to advance output to the next line, and a carriage return, ASCII 13, was transmitted, which forced the next character to appear in column 1 of that line. The ASCII code that was printed is decimal 10, which is the linefeed character, also known as newline. Therefore, only one ASCII code was generated, so even though both a newline and a carriage return were sent to the screen, only a newline character was seen by the program. Therefore, our pressing the Enter key caused only a newline code to be sent to the program. Usually, when you type the Enter key, it causes both the linefeed and the carriage return to be inserted in a document, but here you can see that only the linefeed is transmitted. ( If you do not remember your ASCII codes, type man ascii for the listing. )

Third, in the printf() statement, the program sent a "\n" (newline) character to the terminal, but this seems to cause both a linefeed and a carriage return to be placed on the terminal. The linefeed character, by definition, should cause the cursor to move down to the next line in the same "column" on the screen, whereas a carriage return should move the cursor to column one, the left margin, without moving it down one line. But somehow both things happen even though a single character is transmitted.

What we can conclude from this is that the terminal driver must be doing some character processing on the inputs it receives from the keyboard and on the outputs that the processor sends to the display device. (Remember that the terminal driver is controlling a logical input/output device.) We now explore what the terminal driver does and how we can control its behavior.

## 4.4.2 Terminal Devices: An Overview

The preceding experiment showed that the default input mode of a terminal includes assembling the input into lines, processing various special characters such as backspace, and delivering the input lines to the process after they have been processed. This mode of operation is called canonical input mode. Terminals can be operated in various non-canonical input modes as well. In a non-canonical mode, some part of this processing of input is turned off. Programs like emacs, vi, and less put the terminal into a non-canonical mode.

The behavior of a terminal device is controlled entirely by a piece of software called a terminal driver. A terminal driver is not the same thing as a terminal device driver. A terminal driver consists of two components:

- 1. a terminal device driver, and
- 2. a line discipline.

System 7 and BSD systems supported three different input modes: cooked, raw, and cbreak. POSIX.1 does not support these, although many systems still provide support for them.
