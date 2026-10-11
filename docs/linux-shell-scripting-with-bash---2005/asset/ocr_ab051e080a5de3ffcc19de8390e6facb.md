The keyword then is treated as a separate command, requiring a semicolon to separate it from the if command. The keyword fi appears after the final command to be executed inside the if.

For example, the test -f command checks for the existence of a file.

```
if test -f ./report.out ; then

    printf "The report file ./report.out exists!\n"
fi
```

The message "The report file ./report.out exists!" is printed only if the file exists. If the file does not exist, the printf command is skipped and execution proceeds after the fi.

# # File Expressions

The built-in test command contains a wide variety of tests for files. It can test the type of file, the accessibility of the file, compare the ages of files or other file attributes. The following is a complete list of Bash file tests:

+   - -b file—True if the file is a block device file
+   - -c file—True if the file is a character device file
+   - -d file—True if the file is a directory
+   - -e file—True if the file exists
+   - -f file—True if the file exists and is a regular file
+   - -g file—True if the file has the set-group-id permission set
+   - -h file (or -1 file)—True if the file is a symbolic link
+   - -k file—True if the file has the sticky permission bit set
+   - -p file—True if the file is a pipe
+   - -r file—True if the file is readable (by your script)
+   - -s file—True if the file exists and is not empty
+   - -S file—True if the file is a socket
+   - -t fd—True if the file descriptor is opened on a terminal
+   - -u file—True if the file has the set-user-id permission set
+   - -w file—True if the file is writable (by your script)
+   - -x file—True if the file is executable (by your script)
+   - -O file—True if the file is (effectively) owned by you
+   - -G file—True if the file is (effectively) owned by your group
+   - -N file—True if the file has new content (since the last time it was read)
+   - f1 -nt f2—(never than) True if file f1 is newer than f2