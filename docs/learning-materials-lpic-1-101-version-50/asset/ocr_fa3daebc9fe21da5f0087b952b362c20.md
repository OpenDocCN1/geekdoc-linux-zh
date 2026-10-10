# Answers to Guided Exercises

1. Consider the listing below:

```
$ ls -lh
    total 60K
    drwxr-xr-x 2 frank frank  4.0K Apr 1  2018 Desktop
    drwxr-xr-x 2 frank frank  4.0K Apr 1  2018 Documents
    drwxr-xr-x 2 frank frank  4.0K Apr 1  2018 Downloads
    -rw-r--r-- 1 frank frank  21 Sep 7 12:59 emp_name
    -rw-r--r-- 1 frank frank  20 Sep 7 13:03 emp_salary
    -rw-r--r-- 1 frank frank  8.8K Apr 1  2018 examples.desktop
    -rw-r--r-- 1 frank frank  10 Sep 1  2018 file1
    -rw-r--r-- 1 frank frank  10 Sep 1  2018 file2
    drwxr-xr-x 2 frank frank  4.0K Apr 1  2018 Music
    drwxr-xr-x 2 frank frank  4.0K Apr 1  2018 Pictures
    drwxr-xr-x 2 frank frank  4.0K Apr 1  2018 Public
    drwxr-xr-x 2 frank frank  4.0K Apr 1  2018 Templates
    drwxr-xr-x 2 frank frank  4.0K Apr 1  2018 Videos
```

+   What does the character **d** represent in the output?

**d** is the character that identifies a directory.

+   Why are the sizes given in human readable format?

Due the option **-h**.

+   What would be the difference in the output if **ls** was used with no argument?

Directory and file names would be provided only.

2. Consider the command below:

```
$ cp /home/frank/emp_name /home/frank/backup
```

+   What would happen to the file **emp_name** if this command is executed successfully?

**emp_name** would be copied into backup.

+   If **emp_name** was a directory what option should be added to **cp** to execute the command?