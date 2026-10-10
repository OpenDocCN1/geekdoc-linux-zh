# CHAPTER 3
Basic Bash Shell Commands

# IN THIS CHAPTER

+   - Interacting with the shell
+   - Using the Bash manual
+   - Traversing the filesystem
+   - Listing files and directories
+   - Managing files and directories
+   - Viewing file contents

The default shell used in many Linux distributions is the GNU Bash shell. This chapter describes the basic features available in the Bash shell, such as the Bash manual, command-line completion, and how to display a file’s contents. The chapter walks you through how to work with Linux files and directories using the basic commands provided by the Bash shell. If you’re already comfortable with the basics in the Linux environment, feel free to skip this chapter and go to Chapter 4 to see more advanced commands.

# Starting the Shell

The GNU Bash shell is a program that provides interactive access to the Linux system. It runs as a regular program and is normally started whenever a user logs into a terminal. The shell that the system starts depends on your user ID configuration.

The `/etc/passwd` file contains a list of all the system user accounts, along with basic configuration information about each user. Here’s a sample entry from an `/etc/passwd` file:

```
```
christine:x:1001:1001::/home/christine:/bin/bash
```
```

Every entry has seven data fields, each separated by a colon (:). The system uses the data in these fields to assign specific features for the user. Most of these entries are discussed in more detail in Chapter 7, “Understanding Linux File Permissions.” For now, just pay attention to the last field, which specifies the user’s shell program.