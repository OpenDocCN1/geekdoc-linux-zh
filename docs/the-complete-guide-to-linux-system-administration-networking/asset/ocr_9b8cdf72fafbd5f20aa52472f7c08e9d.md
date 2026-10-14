# 23. The output of the id command includes:

+   a. the effective UID, the effective GID, and a list of groups of which the effective UID user is a member
+   b. a list of all terminals on which the current user is working
+   c. the user name used to log in
+   d. the effective UID and the effective GID

# 24. If the far left column in the output of the ls -l command shows the character "s" you would know that the object on that line was a:

+   a. regular file with su-based superuser access
+   b. special block device file
+   c. special character device file
+   d. socket

# 25. Which utility typically provides the highest compression ratio (makes the smallest compressed file from a given data file)?

+   a. zip
+   b. bzip2
+   c. compress
+   d. gzip

# HANDS-ON PROJECTS

# Project 4-1

In this project, you use the su command and various user information commands to see how the effective UID can change. To complete this project, you need to have both a regular user account and root access to your Linux system.

+   1. Log in to Linux using your regular user account.
+   2. If you logged in using a graphical login window, open a command-line window.
+   3. At the $ prompt, enter the id command to see your currently effective UID.
+   4. Create a file named newfile in your home directory by typing touch newfile.
+   5. Use the ls command to view the owner and group assigned to this file by entering ls -l newfile. What do you see?
+   6. Enter su (without a hyphen) to change to the root account, and supply the root password when prompted.
+   7. Use the id command again to see how your effective UID has changed.
+   8. Enter logname. What do you see?