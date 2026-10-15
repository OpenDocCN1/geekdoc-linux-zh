# EXPLANATION (CONTINUED)

3 The tmp file is removed.

4 With the pipe facility, you can perform all three of the preceding steps in one step. The output of the who command is sent to an anonymous kernel buffer; the wc -l command reads from the buffer and sends its output to the screen. See Figure 13.4.

5 The output of the du command, the number of disk blocks used per directory, starting in the parent directory (..), is piped to the sort command and sorted numerically. It is then piped to the sed command, which prints the last line of the output it receives. See Figure 13.5.

6 The du command (starting in the root directory) will send error messages to stderr (the screen) if it is unable to get into a directory because the permissions have been turned off. When you put the whole command line in a set of parentheses, all the output is sent to the screen, and all the errors are directed to the UNIX/Linux bit bucket, /dev/null.

![](bbox=[0.07, 0.52, 0.92, 0.73])

Figure 13.4 The pipe.

![](bbox=[0.07, 0.77, 0.92, 0.97])

Figure 13.5 Multiple pipes (filter).