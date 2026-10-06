# Table 2-10
Setting Read, Write, Execute Permissions

| Permission | File | Directory |
| --- | --- | --- |
| Read | View what's in the file. | See what files and subdirectories it contains. |
| Write | Change the file's content, rename it, or delete it. | Add files or subdirectories to the directory. |
| Execute | Run the file as a program. | Change to that directory as the current directory, search through the directory, or execute a program from the directory. |

You can see the permission for any file or directory by typing the `ls -ld` command. The named file or directory appears as shown in this example:

```
$ ls -ld ch3 test
rw-rw-r-- 1 chris 4983 Jan 18 22:13 ch3
ddrwxr-xr-x 2 charlie 1024 Jan 24 13:47 test
```

The first line shows that the ch3 file has read and write permission for the owner and the group. All other users have read permission, which means they can view the file but cannot change its contents or remove it. The second line shows the test (indicated by the letter d) before the permission bits. The owner has read, write, and execute permission, while the group and others have only read and execute permissions. As a result, the owner can add, change, or delete files in that directory, and everyone else can only read the contents, change that directory and list the contents of the directory.

If you own a file, you can use the `chmod` command to change the permission on it as you please. In one method of doing this, each permission (read, write, and execute) is assigned a number—r=4, w=2, and x=1—and you use each set's total number to establish the permission. As owner, set the first number to 7 (4+2+1), and to give the group and others only read permission, you both the second and third numbers to 4 (4+0+0), so that the final number is 744. Any combination of permissions can result in 0 (no permission) through 7 (full permission).

Here are some examples of how to change permission on a file (named file) and what the resulting permission would be:

```
# chmod 777 file  rwxrwxrwx
# chmod 755 file  rwxr-xr-x
# chmod 644 file  rw-r--r--
# chmod 000 file  ----------
```