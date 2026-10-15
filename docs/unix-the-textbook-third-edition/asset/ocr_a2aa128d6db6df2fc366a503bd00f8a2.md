to index the inode table in the main memory in order to access the file's inode. The inode contains the attributes of Chapter3, including its location on disk.

Here is a brief description of the ln command:

# SYNTAX

```
ln [options] existing-file new-file
ln [options] existing-file-list directory
```

+   **Purpose:** First syntax: Create a link to existing-file and name it new-file
+   Second syntax: Create links to the ordinary files in existing-file-list in directory, links have the same names as the original file
+   
+   **Commonly used options/features:**
+   - **-f** Force creation of link; don't prompt if new-file already exists
+   - **-n** Don't create the link if new-file already exists
+   - **-s** Create a symbolic link to existing-file and name it new-file

The ln command without any option creates a hard link to a file, provided the user has execute permission for all the directories in the path leading to the file. The following session illustrates how the ln command can be used to create a hard link in the same directory that contains existing-file. The only purpose of this example is to illustrate how the ln command is used; it isn't representative of how you would establish and use hard links in practice.

```
$ ls -l
13059 -rwx------ 1 sarwar faculty 398 Mar 11 14:20 Chapter1
17488 -rwx------ 1 sarwar faculty 5983 Apr 17 11:57 Chapter2
52473 -rwx------ 1 sarwar faculty 9352 Aug 20 23:09 Chapter3
$ ln Chapter3 Chapter3.hard
$ ls -l
13059 -rwx------ 1 sarwar faculty 398 Mar 11 14:20 Chapter1
17488 -rwx------ 1 sarwar faculty 5983 Apr 17 11:57 Chapter2
52473 -rwx------ 2 sarwar faculty 9352 Aug 20 23:09 Chapter3
52473 -rwx------ 2 sarwar faculty 9352 Aug 20 23:09 Chapter3.hard
$
```

The ls -l command shows some of the attributes of all the files in the present working directory, including their inode numbers. The command ln Chapter3 Chapter3.hard creates a hard link to the file Chapter3; the name of the hard link is Chapter3.hard. The system creates a new directory entry (52473, Chapter3.hard) for Chapter3 in the present working directory. Thus, you can refer to Chapter3 by accessing Chapter3.hard as well, because both names point to the same file on disk. The second ls -l command is used to confirm that Chapter3.hard and Chapter3 are two names for the same file, as both have the same inode number, 52473, and hence the same attributes. Therefore, when a hard link is created to Chapter3, a new pointer