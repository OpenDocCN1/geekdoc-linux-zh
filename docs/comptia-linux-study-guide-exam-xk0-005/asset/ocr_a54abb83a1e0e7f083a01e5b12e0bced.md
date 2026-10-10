each file and directory on the Linux system. The nine permissions appear in the `ls` output as the first column of information when you use the `-l` option, as shown in Listing 15.1. Figure 15.1 shows the order in which the permissions are displayed in the `ls` output.

![](bbox=[0.15, 0.19, 0.85, 0.46])

In Figure 15.1, the first character denotes the object type. A dash indicates a file, and a d indicates a directory.

The next three characters denote the owner permissions in the order of read, write, and execute. A dash indicates the permission is not set, whereas the r, w, or x indicates the read, write, or execute permission is set. In the example in Listing 15.1, all three files use rw- for the owner permissions, which means the owner has permissions to read and write to the file but cannot execute, or run, the file. This is common with data files.

The second set of three characters denotes the group permissions for the file or directory. Again, this uses the read, write, and execute order; with a dash indicating the permission is not set. After making the change to the `customers.txt` file for the marketing group, the sales group can only read the `research.txt` and `salesdata.txt` files, but the marketing group can both read and write the `customers.txt` file.

Finally, the third set of three characters denotes the permissions assigned to user accounts that are not the owner or a member of the group assigned to the file or directory. The same order of read, write, and execute is used. In the Listing 15.1 examples, other user accounts on the system can read the files but not write or execute them.

Either the root user account or the owner of the file or directory can change the assigned permissions by using the chmod command.

The format of the `chmod` command can be somewhat confusing. It uses two different modes for denoting the read, write, and execute permission settings for the owner, group, and others. Both modes allow you to define the same sets of permissions, so there’s no reason to use one mode over the other.

In *symbolic mode*, you denote permissions by using a letter code for the owner (u), group (g), others (o), or all (a) and another letter code for the read (r), write (w), or execute (x)