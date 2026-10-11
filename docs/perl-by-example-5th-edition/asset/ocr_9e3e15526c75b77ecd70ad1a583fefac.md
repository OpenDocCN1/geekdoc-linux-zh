# EXPLANATION

+   1. This script calls for only one argument. If ARGV is empty (meaning, no arguments are passed at the command line), the die function is executed and the script exits with an error message. (Remember: $#ARGV is the number of the last subscript in the ARGV array, and ARGV[0] is the first argument, not counting the name of the script, which is $0.) If more than one argument is passed, the script will also exit with the error message.

+   2. The /etc/passwd file is opened for reading via the Spw filehandle.
+   3. The first argument is shifted from @ARGV and assigned to $username.
+   4. Each time the while loop is entered, a line of the /etc/passwd file is read via the Spw filehandle.

+   5. The == is used to test if the first argument passed matches the $username. If a match is not found, the loop is exited.

+   6. The filehandle is closed.

+   7. LOGGEDON is opened as a pipe to accept input. Output from the UNIX who command will be piped to the LOGGEDON pipe.
+   8. Each line of the input from the pipe is tested. If the user is logged on, the scalar $logged_on is set to 1, and the loop is exited.
+   9. The pipe is closed.

+   10. PROC is opened a pipe to accept input. Output from the UNIX ps command will be piped to PROC. Each line from the pipe is read in turn and placed in the scalar $line. If $line contains a match for the user, that line will be printed to STDOUT, the screen.
+   11. The pipe is closed.

# 10.3.3 The eof Function

The eof function can be used to test if end of file has been reached. It returns 1 if either the next read operation on a FILEHANDLE is at the end of the file, or the file was not opened. Without an argument, the eof function returns the eof status of the last file read. The eof function with parentheses can be used in a loop block to test the end of file when the last filehandle has been read. Without parentheses, each file opened can be tested for end of file.

# FORMAT

```
eof (FILEHANDLE)
eof ( )
eof
```