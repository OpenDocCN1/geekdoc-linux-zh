
You can view the assigned owner and group for a file or directory by adding the `-1` option to the `ls` command, as shown in Listing 15.1.

### **Listing 15.1:** Viewing file owner and group settings

```bash
$ ls -l
total 12
-rw-rw-r-- 1 Rich sales 1521 Jan 19 15:38 customers.txt
-rw-r-r-r-- 1 Christine sales 479 Jan 19 15:37 research.txt
-rw-r-r-r-- 1 Christine sales 696 Jan 19 15:37 salesdata.txt
$
```

In Listing 15.1, the first column, `-rw-rw-r--`, defines the access permissions assigned to the owner, group, and others. That will be discussed later in the chapter in the section “Controlling Access Permissions.” The third column in Listing 15.1, the *Rich* or *Christine* value, shows the user account assigned as the owner of the file. The fourth column, *sales*, shows the group assigned to the file.

![](img/c0a399aca0d18f8822d714ad0a173123_506_0.png)

> Many Linux distributions (such as both *Ubuntu* and *Rocky Linux*) assign each user account to a separate group with the same name as the user account. This helps prevent accidental sharing of files. However, it can also make things a little confusing when you’re working with owner and group permissions and you see the same name appear in both columns. Be careful when working in this type of environment.

When a user creates a file or directory, by default the Linux system automatically assigns that user as the owner and uses the primary group the user belongs to as the group for the file or directory. You can change the default owner and group assigned to files and directories by using Linux commands. The following sections show how to do that.

## Changing File or Directory Ownership

The root user account can change the owner assigned to a file or directory by using the `chown` command. The `chown` command format looks like this:

```bash
$ chown [options] newowner filenames
```

The `newowner` parameter is the username of the new owner to assign to the file or directory, and `filenames` is the name of the file or directory to change. You can specify more than one file or directory by placing a space between each file or directory name:

```bash
$ sudo chown Christine customers.txt
$ ls -l
total 12
-rw-rw-r-- 1 Christine sales 1521 Jan 19 15:38 customers.txt
-rw-r-r-r-- 1 Christine sales 479 Jan 19 15:37 research.txt
-rw-r-r-r-- 1 Christine sales 696 Jan 19 15:37 salesdata.txt
$
```

There are a few command-line options available for the chown command, but they are mostly obscure and not used much. One that may be helpful for you is the `-R` option, which recursively changes the owner of all files under the specified directory.

## Changing the File or Directory Group

The file or directory owner, or the root user account, can change the group assigned to the file or directory by using the chgrp command. The chgrp command uses this format:

```bash
$ chgrp [options] newgroup filenames
```

The `newgroup` parameter is the name of the new user group assigned to the file or directory, and the `filenames` parameter is the name of the file or directory to change. If you're the owner of the file, you can only change the group to a group that you belong to.

The root user account can change the group to any group on the system:

```bash
$ sudo chgrp marketing customers.txt
$ ls -l
total 12
-rw-r--r-- 1 Christine marketing 1521 Jan 19 15:38 customers.txt
-rw-r--r-- 1 Christine sales 479 Jan 19 15:37 research.txt
-rw-r--r-- 1 Christine sales 696 Jan 19 15:37 salesdata.txt
$
```

![](img/c0a399aca0d18f8822d714ad0a173123_507_0.png)

> The chown command allows you to change both the owner and the group assigned to a file or directory at the same time using this format:
> `chown newowner:newgroup filenames`
> 
> This is often preferred over using the separate chgrp command.

## Controlling Access Permissions

After you've established the file or directory owner and group, you can assign specific permissions to each. Linux uses three types of permission controls:

- **Read:** The ability to access the data stored in the file or directory
- **Write:** The ability to modify the data stored in the file or directory
- **Execute:** The ability to run the file on the system, or the ability to list the files contained in the directory

You can assign each tier of protection (owner, group, and others) different read, write, and execute permissions. This creates a set of nine different permissions that are assigned to each file and directory on the Linux system. The nine permissions appear in the `ls` output as the first column of information when you use the `-l` option, as shown in Listing 15.1. Figure 15.1 shows the order in which the permissions are displayed in the `ls` output.

![](img/c0a399aca0d18f8822d714ad0a173123_508_0.png)

In Figure 15.1, the first character denotes the object type. A dash indicates a file, and a d indicates a directory.

The next three characters denote the owner permissions in the order of read, write, and execute. A dash indicates the permission is not set, whereas the r, w, or x indicates the read, write, or execute permission is set. In the example in Listing 15.1, all three files use rw- for the owner permissions, which means the owner has permissions to read and write to the file but cannot execute, or run, the file. This is common with data files.

The second set of three characters denotes the group permissions for the file or directory. Again, this uses the read, write, and execute order; with a dash indicating the permission is not set. After making the change to the `customers.txt` file for the marketing group, the sales group can only read the `research.txt` and `salesdata.txt` files, but the marketing group can both read and write the `customers.txt` file.

Finally, the third set of three characters denotes the permissions assigned to user accounts that are not the owner or a member of the group assigned to the file or directory. The same order of read, write, and execute is used. In the Listing 15.1 examples, other user accounts on the system can read the files but not write or execute them.

Either the root user account or the owner of the file or directory can change the assigned permissions by using the chmod command.

The format of the `chmod` command can be somewhat confusing. It uses two different modes for denoting the read, write, and execute permission settings for the owner, group, and others. Both modes allow you to define the same sets of permissions, so there’s no reason to use one mode over the other.

In *symbolic mode*, you denote permissions by using a letter code for the owner (u), group (g), others (o), or all (a) and another letter code for the read (r), write (w), or execute (x) permission. The two codes are separated with a plus sign (+) if you want to add the permission, a minus sign (-) to remove the permission, or an equal sign (=) to set the permission as the only permission. Listing 15.2 shows an example of this.

### Listing 15.2: Changing file permissions

```bash
$ chmod g-w customers.txt
$ ls -al
total 12
-rw-r--r-- 1 Christine marketing 1521 Jan 19 15:38 customers.txt
-rw-r--r-- 1 Christine sales 479 Jan 19 15:37 research.txt
-rw-r--r-- 1 Christine sales 696 Jan 19 15:37 salesdata.txt
$
```

In Listing 15.2, the g-w code in the chmod command indicates that we are removing the write permission for the group from the customers.txt file.

You can combine letter codes for both to make multiple changes in a single chmod command, as shown in Listing 15.3.

### Listing 15.3: Combining permission changes

```bash
$ chmod ug=rwx salesdata.txt
$ ls -l
total 12
-rw-rw-r-- 1 Christine marketing 1521 Jan 19 15:38 customers.txt
-rw-rw-r-- 1 Christine sales 479 Jan 19 15:37 research.txt
-rwx-rwx-r-- 1 Christine sales 696 Jan 19 15:37 salesdata.txt
$
```

The ug code assigns the change to both the owner and the group, whereas the rwx code assigns the read, write, and execute permissions. We use the equal sign to set those permissions.

The second mode available in chmod is called *octal mode*. With octal sign, the nine permission bits are represented as three octal numbers, one each for the owner, group, and other permissions. Table 15.1 shows how the octal number matches the three symbolic mode permissions.

## TABLE 15.1 Octal mode permissions

| Octal value | Permission | Meaning |
|:------------|:-----------|:--------|
| 0 | --- | No permissions |
| 1 | --x | Execute only |
| 2 | -w- | Write only |
