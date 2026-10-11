+   2. A list of permissions on the file (also called the mode of the file)
+   3. A hard link count (discussed in Chapter 5)
+   4. The owner of the file (discussed in Chapter 5)
+   5. The group owner of the file (discussed in Chapter 5)
+   6. The file size
+   7. The most recent modification time of the file
+   8. The filename (some files are shortcuts or pointers to other files and indicated with an arrow `->` as with the file called "current" in the preceding output; these are known as symbolic links and are discussed in Chapter 5)

For the file named *project* in the previous example, you can see that this file is a regular file because the long listing of it begins with a \- character, the permissions on the file are `rw-r--r--`, the hard link count is 1, the owner of the file is the root user, the group owner of the file is the root group, the size of the file is 71 bytes, and the file was modified last on April 7th at 9:58 AM.

# NOTE

> On most Linux systems, a shortcut to the `ls` command can be used to display the same columns of information as the `ls -l` command. Some users prefer to use this shortcut, commonly known as an alias, which is invoked when a user types `ll` at a command prompt. This is known as the **ll** command.

The `ls -F` and `ls -1` commands are valuable to a user who wants to display file types; however, neither of these commands can display all file types using special characters. To display the file type of any file, you can use the **file** command; simply give the `file` command an argument specifying what file to analyze. You can also pass multiple files as arguments or use the `*` metacharacter to refer to all files in the current directory. An example of using the `file` command in the root user's home directory is:

```
[root@server1 root]$ pwd
/root
[root@server1 root]$ ls
current myprogram project project2 project3 project4
Desktop myscript project1 project3 project4 project5
[root@server1 root]$ file Desktop
Desktop: directory
[root@server1 root]$ file project Desktop
project:    ASCII text
Desktop:    directory
[root@server1 root]$ file *
Desktop:    directory
```