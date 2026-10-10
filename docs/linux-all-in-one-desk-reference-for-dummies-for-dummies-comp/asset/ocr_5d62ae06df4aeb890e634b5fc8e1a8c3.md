chgrp accounting ledger.out

# Changing file permissions

Use the *chmod* command to set the file permissions. To use *chmod* effectively, you have to specify the permission settings. One way is to concatenate one or more letters from each column of Table 2-1, in the order shown (*Who/*Action/*Permission*).

| **Table 2-1** | **File Permission Codes** |
| :--- | :--- | :--- |
| **Who** | **Action** | **Permission** |
| u user | + add | r read |
| g group | - remove | w write |
| o others | = assign | x execute |
| a all | s set user ID | |

To give everyone read and write access to all files in a directory, type **chmod a+rw \***. On the other hand, to permit everyone to execute a specific file, type *chmod a+x filename*.

Another way to specify a permission setting is to use a three-digit sequence of numbers. In a detailed listing, the read, write, and execute permission settings for the user, group, and others appear as the sequence

*rw rwx rw x*

with dashes in place of letters for disallowed operations. Think of *rw xrwx rwx* as three occurrences of the string *rwx*. Now assign the values r=4, w=2, and x=1. To get the value of the sequence *rw x*, simply add the values of r, w, and x. Thus, *rw x* = 7. Using this formula, you can assign a three-digit value to any permission setting. For example, if the user can read and write the file but everyone else can only read the file, the permission setting is *rw -r --r --* (that’s how it appears in the listing), and the value is 644. Thus, if you want all files in a directory to be readable by everyone but writable only by the user, use the following command:

*chmod 644 \**

# Setting default permission

What permission setting does a file get when you (or a program) create a new file? The answer is in what is known as the *user file-creation mask* that you can see and set by using the *umask* command.