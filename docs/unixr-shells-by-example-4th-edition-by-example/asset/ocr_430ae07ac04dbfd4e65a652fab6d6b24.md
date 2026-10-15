# EXAMPLE 10.25 (CONTINUED)

```
3  if ( ! -z file ) then
    echo file is not of zero length
endif
4  if ( -r file && -w file ) then
    echo file is readable and writable
endif
```

# EXPLANATION

+   1. The statement reads: if the file exists, then . . .
+   2. The statement reads: if the file is a directory, then . . .
+   3. The statement reads: if the file is not of zero length, then . . .
+   4. The statement reads: if the file is readable and writable, then . . . . The file-testing flags cannot be stacked, as in -rw file. A single option precedes the filename (e.g., -r file && -w file && -x file).

# 10.6.16 The test Command and File Testing

The UNIX/Linux test command includes options that were built into the C shell, as well as a number of options that were not. See Table 10.8 for a list of test options. You may need these additional options when testing less common attributes of files such as block and special character files, or setuid files. The test command evaluates an expression and returns an exit status of either 0 for success or 1 for failure. When using the test command in an if conditional statement, curly braces must surround the command so that the shell can evaluate the exit status properly.⁴

# Table 10.8 File Testing with the test Command

| Option | Meaning—Tests True If |
|--------|------------------------|
| -b | File is a block special device file |
| -c | File is a character special device file |
| -d | File exists and is a directory file |
| -f | File exists and is a plain file |
| -g | File has the set-group-ID bit set |
| -k | File has the sticky bit set |

> 4. A common error is to name your script test. If your search path contains the UNIX test command first, it will execute it instead of your script. The test command either displays an error or nothing at all if the syntax is correct.