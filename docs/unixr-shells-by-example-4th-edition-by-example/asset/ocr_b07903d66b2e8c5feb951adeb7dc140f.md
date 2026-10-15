# EXPLANATION

+   1 The outer for loop is started. The first time in the loop, Jan is assigned to month.
+   2 The inner for loop starts. The first time in this loop, 1 is assigned to week. The inner loop iterates completely before going back to the outer loop.
+   3 If the user enters either an n or presses Enter, line 4 is executed.
+   4 The continue command with an argument of 2 starts control at the top of the second outermost loop. The continue without an argument returns control to the top of the innermost loop.
+   5 Control is returned to the innermost for loop.
+   6 This done terminates the innermost loop.
+   7 This done terminates the outermost loop.

# 14.6.7 I/O Redirection and Subshells

Input can be piped or redirected to a loop from a file. Output can also be piped or redirected to a file from a loop. The shell starts a subshell to handle I/O redirection and pipes. Any variables defined within the loop will not be known to the rest of the script when the loop terminates.

# Redirecting the Output of a Loop to a File.

Output from a bash loop can be sent to a file rather than to the screen. See Example 14.51.

# EXAMPLE 14.51

```
(The Command Line)
1 $ cat memo
abc
def
ghi

(The Script)
#!/bin/bash
# Program name: numberit
# Put line numbers on all lines of memo
2 if (( $# < 1 ))
then
3   echo "Usage: $0 filename " >&2
    exit 1
fi
4 count=1          # Initialize count
```