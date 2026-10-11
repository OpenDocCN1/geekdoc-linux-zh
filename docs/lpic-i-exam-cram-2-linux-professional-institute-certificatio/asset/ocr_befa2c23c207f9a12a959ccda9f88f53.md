# # Testing for Conditions

The test command is useful for comparing the dates of files, whether some-
thing is newer or older than another, or even that a file exists and is of a par-
ticular type. To test whether an object exists on the file system, the -f option
is used, followed by the full path and name of the object being tested.

The test command can handle a large set of test conditions. A useful smart-
tering is shown here:

+   > x = y—This compares x with y and, if true, returns an exit status of 0.
+   > x != y—This compares x with y and, if they're not equal, returns an exit
+   status of 0.
+   > x -eq y—If x is equal to y, such as two variable numeric values, it returns
+   an exit status of 0.
+   > x -ge y—If x is greater than or equal to y, it returns an exit status of 0.
+   > x -ne y—If x is not equal to y, it returns an exit status of 0.
+   > -r file1—It tests that file1 exists and is readable.
+   > -w file1—It tests that file1 exists and is writable.
+   > -u file1—It tests that file1 exists and has the SUID bit set.

Of course, more options are available, but you get the idea that test is useful
for determining the status of files and returning exit statuses based on what
it finds.

As an example, to test for the existence of the /etc/passwd file, you would use
the following command:

```
test -f /etc/passwd ; echo $?
```

The test command looks to see whether the /etc/passwd file exists; then echo
shows that the previous command exited with a status of 0 if it was true, and
the file was found.

# # Having Users Make Variables

Many times the best person to fill in the value of a variable is the user run-
ning the script. I like to have the user do as much work as possible, leaving
me to have more time to make up scripts she can run.

The read command is the primary tool I use to have a user type in the con-
tents of a variable that will exist only inside or during the execution of a
script.