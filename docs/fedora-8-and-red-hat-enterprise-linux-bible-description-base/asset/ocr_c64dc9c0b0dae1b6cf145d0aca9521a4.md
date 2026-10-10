In the first example, the contents of the .bashrc file in the home directory are sent in a mail message to the computer’s root user. The second command line formats the chmod man page (using the man command), removes extra back spaces (col -b), and sends the output to the file /tmp/chmod (erasing the previous /tmp/chmod file, if it exists). The final command results in the following text being added to the user’s project file:

```
Finished project on Wed Jun 25 13:46:49 PST 2008
```

You could also pipe the output of the previous command to another command. For example, the following command line would send the line just shown in a mail message to the user boss@example.com:

```
$ echo "Finished project on $(date)" |mail -s 'Done' boss@example.com
```

# Understanding file permissions

After you’ve worked with Linux for a while, you are almost sure to get a Permission denied message. Permissions associated with files and directories in Linux were designed to keep users from accessing other users’ private files and to protect important system files.

The nine bits assigned to each file for permissions define the access that you and others have to your file. Permission bits appear as rwxrwxrwx. The first three bits apply to the owner’s permission, the next three apply to the group assigned to the file, and the last three apply to all others. The r stands for read, the w stands for write, and the x stands for execute permissions. If a dash appears instead of the letter, it means that permission is turned off for that associated read, write, or execute.

You can see the permission for any file or directory by typing the ls -lid command. The named file or directory appears as those shown in the following example:

```
$ ls -lid ch3 test
-rw-rw-r-- 1 chris sales 4983 Jan 18 22:13 ch3
drwxr-xr-x 2 chris sales 1024 Jan 24 13:47 test
```

The first line shows a file (ch3) that has read and write permission for the owner and the group. All other users have read permission, which means they can view the file but cannot change its contents (although a user may be allowed to remove the file, since the ability to remove a file is based on directory permissions). The second line shows a directory (indicated by the letter d before the permission bits). The owner has read, write, and execute permission, while the group and other users have only read and execute permissions. As a result, only the owner can add, change, or delete files in that directory. Any other user, however, can only read the contents, change to that directory, and list the contents of the directory. (Note that by using the -d option, the test directory entry is listed without listing its contents.)

If you own a file, you can change the permission on it as you please. You can do this with the chmod command. For each of the three sets of permission on a file (read, write, and execute), r is assigned to the number 4, w to 2, and x to 1. So to make permissions wide open for yourself as owner, you would set the first number to 7 (4 plus 2 plus 1). The same would be