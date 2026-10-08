# Table 16.2. continued

| Option | Meaning |
| --- | --- |
| -o | True if the file exists and is owned by the same user as the process. |
| -S | True if the file exists and is a file used for communications programs (socket). |
| -b | True if the file exists and is a symbol identifying a physical device used for input and output in large chunks of data, such as a hard disk, (block special device). |
| -c | True if the file exists and is a symbol identifying a physical device used for input and output in single characters, such as a terminal (character special device). |
| -d | True if the file is a directory. |
| -e | True if the file exists. |
| -f | True if the file exists and is a regular file. |
| -g | True if the file exists and runs in a specific group. |
| -k | True if the file exists and is set to remain in memory after execution. This makes a program a faster starter, at the cost of overall system performance. |
| -p | True if the file exists and is a named pipe. |
| -r | True if the file exists and is readable. |
| -s | True if the file exists and has data. |
| -u | True if the file exists and runs as a specific user. |
| -w | True if the file exists and is writable. |
| -x | True if the file exists and is executable. |

A sample test would be:

```
test -d $HOME/bin
```

This checks to see if you directory named bin in your home directory. The -f flag and the -d flag. The most common flags are used only in unusual situations.

The file system has three binary comparisons. The -of test determines whether the two files are the same. (When you create a link between files, this is true.) The -nt flag is true if the first file is newer than the second, and the -ot flag is true if the first file is older than the second. You might see a test in a looping statement like:

```
test file1 -ot file2
```

![](bbox=[0.065, 0.893, 0.138, 0.973])