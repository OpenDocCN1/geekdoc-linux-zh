aio_sigevent member of a control block. But here, the notification means that all the requests in the list have completed. You can still be notified of completions via the aio_sigevent members of the individual control blocks.

For LIO_WAIT, the sig argument isn’t used.

As for some of the other AIO calls, a successful return from lio_listsio only means that that call went well. It says nothing about the I/O operations, which you test for with aio_error.

# Exercises

+   3.1. Modify the program in Section 3.2.2 as suggested by the last paragraph of that section.
+   
+   3.2. Write the standard clc command.
+   
+   3.3. Modify the aupls command as suggested by the last paragraph of Section 3.6.2.
+   
+   3.4. Modify the getcwdx function in Section 3.6.4 so it never changes the current directory.
+   
+   3.5. Fix Problem 2 that’s described at the start of Section 3.6.5.
+   
+   3.6. Modify the aupls command from Section 3. 3.6.5 so it sorts the list by name.
+   
+   3.7. Modify the aupls command from Section 3. 3.6.5 so it takes a –t option to sort by modified time and name.
+   
+   3.8. Modify the aupls command from Section 3. 3.6.5 so it takes additional standard options (your choice).
+   
+   3.9. Write a program to copy an entire tree of directories and files. It should have two arguments: the root of the tree (e.g., /usr/marc/book), and the root of the copy (e.g., /usr/marc/backup/book). Don’t bother dealing with symbolic or hard links (i.e., it’s OK to make multiple copies), and don’t bother with preserving ownership, permissions, or times.
+   
+   3.10. Same as Exercise 3.9, but, to the extent possible, preserve ownership, permissions, and times. Make "the extent possible” dependent on whether the command is running as superuser.
+   
+   3.11. Same as Exercise 3.10, but preserve the symbolic and hard link structure.