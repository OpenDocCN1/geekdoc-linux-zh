# 6.15.1 Closing Files and Pipes

If you plan to use a file or pipe in an awk program again for reading or writing, you may want to close it first, because it remains open until the script ends. Once opened, the pipe remains open until awk exits. Therefore, statements in the END block will also be affected by the pipe. The first line in the END block closes the pipe.

```
**EXAMPLE 6.103**

(In Script)
```awk
{
  1  print $1, $2, $3 | "sort -r +1 -2 +0 -1"
}
END{
  2  close("sort -r +1 -2 +0 -1")
  <rest of statements>
}
```
```

+   **EXPLANATION**
+   
+   1. Awk pipes each line from the input file to the UNIX/Linux sort utility.
+   2. When the END block is reached, the pipe is closed. The string enclosed in double quotes must be identical to the pipe string where the pipe was initially opened.

**The system Function.** The built-in system function takes a UNIX/Linux system command as its argument, executes the command, and returns the exit status to the awk program. It is similar to the C standard library function, also called system(). The UNIX/Linux command must be enclosed in double quotes.

```
**FORMAT**

```awk
system("UNIX/Linux command")
```
```

```
**EXAMPLE 6.104**

(In Script)
```awk
{
  1  system ( "cat" $1 )
  2  system ( "clear" )
}
```
```

+   **EXPLANATION**
+   
+   1. The system function takes the UNIX/Linux cat command and the value of the first field in the input file as its arguments. The cat command takes the value of the first field, a filename, as its argument. The UNIX/Linux shell causes the cat command to be executed.
+   2. The system function takes the UNIX/Linux clear command as its argument. The shell executes the command, causing the screen to be cleared.