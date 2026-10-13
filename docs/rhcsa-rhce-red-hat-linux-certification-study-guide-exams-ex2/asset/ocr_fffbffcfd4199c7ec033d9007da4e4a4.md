Any user who is a member of the accgrp group can now create files in and copy files to the /home/accshared directory. Any files generated within or copied to that directory will be owned by accgrp group.

This is made possible by the 2770 permissions that assigned to the /home/accshared directory. Break that down into its component parts. The first digit (2) is the set group ID bit, also known as the SGID bit. When a SGID bit is set on a directory, any files created in that directory automatically have their group ownership set to be the same as the group owner of the directory. In addition, group ownership of files copied from other directories is reassigned, in this case, to the group named accgrp. There is a second way to set the SGID bit for the /home/accshared directory:

```
chmod g+s /home/accshared
```

The remaining digits are basic knowledge for any experienced Linux or Unix user. The 770 sets read, write, and execute permissions for the user and group that own the directory. Other users get no permissions to that directory. But since the user owner of the directory is the nonprivileged user named nobody, the group owner of the directory is most important. In this case, members of the accgrp group have read, write, and execute permissions to files created in this directory.

# EXERCISE 8-5

# Control Group Ownership with the SGID Bit

In this exercise, you will create new files in a directory designed to be shared by a group of users. You'll also see the difference in what happens before and after the SGID bit is set.

+   1. Add users called test1, test2, and test3. Specify passwords when prompted. Check the /etc/passwd and /etc/group files to verify that each user's private group was created:
+   ```
+   # useradd test1; passwd test1
+   # useradd test2; passwd test2
+   # useradd test3; passwd test3
+   ```
+   2. Edit the /etc/group file and add a group called tg1. Make the test1 and test2 accounts members of this group. You could add the following line to /etc/group directly or use the Red Hat User Manager:
+   ```
+   tg1:x:99999:test1,test2
+   ```