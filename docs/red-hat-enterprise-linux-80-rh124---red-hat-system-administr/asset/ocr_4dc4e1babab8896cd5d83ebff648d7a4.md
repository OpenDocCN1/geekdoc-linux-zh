The preceding command uses the redirection symbol (>) to save the command output to /home/student/grading/manage-files.txt so that any existing content in the file gets overwritten.

3.2. Verify that the file /home/student/grading/manage-files.txt contains the following text.

```
Test AA
Test BB
Test CC
Test DD
Test EE
```

4. Append the last three lines of /home/student/grading/bin/manage-files to the file /home/student/grading/manage-files.txt. You must not overwrite any text already in the file /home/student/grading/manage-files.txt.

4.1. Use the tail command to view the last three lines of the file /home/student/bin/manage-files and append the output to /home/student/grading/manage-files.txt.

```
[student@serverb ~]$ tail -3 bin/manage-files >> grading/manage-files.txt
```

The preceding command uses the double redirection symbol (>>) to append the output to /home/student/grading/manage-files.txt so that the existing contents in the file are preserved.

4.2. Verify that the file /home/student/grading/manage-files.txt contains the following text.

```
Test AA
Test BB
Test CC
Test DD
Test HH
Test II
Test JJ
```

5. Copy the /home/student/grading/manage-files.txt file to /home/student/grading/manage-files-copy.txt.

5.1. Use the cd command to navigate to the directory /home/student/grading.

```
[student@serverb ~]$ cd grading/
```