
The other types are as follows:

- Regular file with different extensions such as .txt, .php, .sh, .py, and so on
- 1: Symbolic link (or symlink or soft link)
- c: char file type
- b: Block device file

![](img/8c6a223c57e25ea0cc1593903a1b920f_233_0.png)

Figure 7.8 - Permissions for Unix

We then have the permissions. Here, we have three letters (plus a special char) to represent the permissions **(read, write, execute, or disable)** for the three different types of user **(User, Group, or Other)**:

- User: Is the owner or creator of the file or folder. By default, this indicates who created the file, however, this can be modified.
- Group: This shows the permissions of the users on the specified group (as seen in Figure 7.7).
- Other: This specifies the permissions of the other users who are not the owner (user) and are not part of the specified group.

## Examples of permissions

As seen in the preceding section, Unix-like systems have four types of permissions:

- Read: User can open the file.
- Write: User can modify the content of the file.
- Execute: User can execute or run the file from the shell.
- Disable: No permissions.

To better understand this, let's see how the permissions are applied:

- ---: No permissions
- -x-: Execute-only permissions
- -w-: Write-only permissions
- -wx: Write and execute permissions

## Hardening a Unix Server

- r--: Read permissions
- r-x: Read and execute permissions
- rw-: Read and write permissions
- rwx: Read, write, and execute permissions

Now, let's see how this will look for the different users:

- rwx-xr-x: User can read, write, and execute, the group and others can only read and execute.
- rwx-xr--: User can read, write and execute, the group can read and execute, and others can only read.

Remember when assigning permissions, you must do it based on the **Principle of Least Privilege (PoLP)**.

## Permissions in numeric mode (octal representation)

Unix systems have a very interesting feature in which permissions can also be represented using numbers, which enables the system to use math to calculate the permissions. To do that, the system has a value for each permission:

- Read: 4
- Write: 2
- Execute: 1

The following figure represents how values are added to calculate permissions in numeric mode:

| Permission | Read | write | execute |
|---|---|---|---|---|
| -------- | 0 | 0 | 0 | 0 |
| --x | 1 | 0 | 0 | 1 |
| -w- | 2 | 0 | 2 | 0 |
| -wx | 3 | 0 | 2 | 1 |
| r-- | 4 | 4 | 0 | 0 |
| r-x | 5 | 4 | 0 | 1 |
| rw- | 6 | 4 | 2 | 0 |
| rwx | 7 | 4 | 2 | 1 |

Figure 7.9 – Permissions in numeric mode

Based on the --- preceding table, the permissions will now look like this:

- 0 (--): No permissions
- 1 (-x): Execute-only permissions
- 2 (-w-): Write-only permissions
- 3 (-wx): Write and execute permissions
- 4 (r--): Read permissions
- 5 (r-x): Read and execute permissions
- 6 (rw-): Read and write permissions
- 7 (rwx): Read, write, and execute permissions

Over time, using numbers may be easier. However, you must be familiar with both representations of permissions, as some commands may input one or the other.

## Default permissions

When creating files, Unix systems will assign the default permissions to the newly created file, and as a data security professional, you must understand how permissions are assigned. Also, you must understand how you can customize those settings in case you need to apply more restricted permissions for the newly created files.

We can see the permissions of a file using the `ls -1 {file_name}` command, to see the default permissions let's create a new file using the `touch {file_name}` command, and then use the previous (ls -1) command to see the permissions the system assigned by default.

We created an example in the following figure that shows the default permissions of a file in our system. In this case, the default permissions are as follows:

- User (kali): Read and write
- Group (kali): Read
- Others: Read

```
kali@kali:~$ touch bravo
kali@kali:~$ ls -l bravo
-rw-r-r-- 1 kali kali 0 Nov 29 12:16 bravo
```

Figure 7.10 - File with no execute permissions

## Hardening a Unix Server

You can play with the commands to get up to speed with Unix systems (create files, delete the files that you created, list permissions, and so on), but you can also play with conversions to get more familiar with the numeric mode. For example, you can use the permissions shown in Figure 7.10 and [rest of text continues based on logic]...
