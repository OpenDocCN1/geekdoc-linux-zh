# Chapter 16. I/O Redirection

There are always three default "files" open, stdin (the keyboard), stdout (the screen), and stderr (error messages output to the screen), and any other open files can be redirected. Redirection simply means capturing output from a file, command, program, script, or even code block within a script (Example 4-1 and Example 4-2) and sending it to another file, command, program, or script.

Each file gets assigned a file descriptor. [445] The file descriptors for stdin, stdout, and stderr are 0, 1, and 2, respectively. For opening additional files, remain descriptors 3 to 9. It is sometimes useful to assign one of these additional file descriptors to stdin, stdout, and stderr as a temporary duplicate. [146] This simplification restores to normal after complex redirection and reshuffling (see Example 16-1).

```
> Redirect stdout to a file.
# Creates the file if not present, otherwise overwrites it.

ls -LR > dir-tree.list
# Creates a file listing of the directory tree.

> filename
# The truncates "filename" to zero length.
# If not present, creates zero-length file (same effect as 'touch').
# The serves as a dummy placeholder, producing no output.

>> Redirect stdout to a file.
# Creates the file if not present, otherwise appends to it.

# Single-line redirection commands (affect only the line they are on):
#----------------------------------------------------------------------
1>filename
# Redirect stdout to file "filename"
1>>filename
# Redirect and append stdout to file "filename"
2>filename
# Redirect stderr to file "filename"
2>>filename
# Redirect and append stderr to file "filename"
#----------------------------------------------------------------------
# Redirecting stdout, one line at a time.
LOGFILE=script.log
echo "This statement is sent to the log file, \"$LOGFILE\"" 1>$LOGFILE
echo "This statement is appended to \"$LOGFILE\"" 1>>LOGFILE
echo "This statement is also appended to \"$LOGFILE\"" 1>>$LOGFILE
echo "This statement is echoed to stdout, and will not appear in \"$LOGFILE\""\n# These redirection commands automatically "reset" after each line.
```

# Redirecting stdout, one line at a time.