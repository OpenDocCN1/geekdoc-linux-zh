# Summary

In this chapter, you learned about the concept of input and output and examined the echo and printf commands that are used to produce messages from within shell scripts. You also learned about output redirection, and covered the methods of redirecting and appending the output of a command to a file. You also learned about the concept of file descriptor and saw several aspects of its use, including opening files for reading and writing, closing files, and redirecting the output of two file descriptors to one source.

In subsequent chapters, you will expand on the material covered here, and you will see many more applications of both input and output redirection along with the use of file descriptors.

# Questions

+   1. Which file descriptors are associated with STDOUT, STDERR and STDIN?
+   2. Use printf to convert the numbers 16, 255, and 65535 into hexadecimal and octal.
+   3. Given the following script:
+   ```
+   exec 6>out.txt
+   exec 5>&4
+   exec 1>&5
+   date
+   ```
+   Where does the output from date end up?

# Terms

**Escape sequence** A special sequence of characters that represents another character.
**File descriptor** An integer that is associated with a file. Enables you to read and write from a file using the integer instead of the file's name.
**Input redirection** In UNIX, the process of sending input to a command from a file.
**Output redirection** In UNIX, the process of capturing the output of a command and storing it in a file. It redirects the output of a command into a file instead of the screen.
**STDERR** Standard Error. A special type of output used for error messages. The file descriptor for STDERR is 2.
**STDIN** Standard Input. User input is read from STDIN. The file descriptor for STDIN is 0.
**STDOUT** Standard Output. The output of scripts is usually to STDOUT. The file descriptor for STDOUT is 1.