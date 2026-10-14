+   5. Change to your home directory.
+   6. Without changing directory, perform a long listing of the `/dev/log` file using a relative path. What type of file is it?

# Managing Files and Directories

+   - Log in to tty1 as the root user and perform the following actions in order. For each action, write down the command(s) that you used. When finished, log out of tty1.
+   
+   1. Copy the file `/etc/issue` to your current directory and verify that the copy was successful.
+   2. Copy the file `/etc/issue` to your current directory and rename it `newissue` with one command. Verify that the copy was successful.
+   3. Rename the file `newissue` in your current directory to `newissue2` and verify that the file was renamed successfully.
+   4. Make a copy of the `Desktop` directory (in your home directory) called `Desktop2` and verify that the contents of each directory are identical.
+   5. Rename the `Desktop2` directory `Desktop3` and verify that the rename operation was successful.
+   6. Remove the `newissue2` file in your home directory and verify that you were successful.
+   7. Remove the `Desktop3` directory in your home directory with a single command and verify that you were successful.

# Exploring the /dev Directory

+   - Log in to tty1 as the geeko user. Type the command `ls -l /dev/fd0 /dev/fd1` to perform a long listing of the device files for your first and second floppy devices. What type are they (block or character)? Do they share the same device driver? How can you tell?
+   - Do a long listing of the device files associated with the local command-line terminals on your system by typing `ls -l /dev/tty[1-6]` at the command prompt. What type are these files? Do they all share the same major number? Do they share the same minor number? Why?
+   - Log out of tty1.

# Viewing and Testing Hidden Environment Files

+   - Your home directory contains several hidden files that contribute to your user environment. Log in to tty1 as the geeko user and run the `ls -a` command. How can you identify the hidden files?
+   - Type the command `less .bash_history` and press Enter. What is stored in this file? Press q when finished.
+   - The `.profile` file is used to create variables and load programs when you log in to your system and obtain a login shell. If you create additional shells following login,