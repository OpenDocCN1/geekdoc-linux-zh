
## Part I: The Linux Command Line

- The GID
- The list of user accounts that belong to the group

The group password allows a non-group member to temporarily become a member of the group by using the *password*. This feature is not used all that commonly, but it does exist.

Since the /etc/group file is a standard text file, you can manually edit it to add and modify group memberships. However, be careful that you don't make any typos or you could corrupt the file and cause problems for your system. Instead, it's safer to use the **usermod** command (discussed earlier in the “Exploring Linux Security” section) to add a user account to a group. Before you can add users to different groups, you must create the groups.

> **Note**
>
> The list of user accounts is somewhat misleading. You'll notice that there are several groups in the list that don't have any users listed. This isn't because they don't have any members. When a user account uses a group as the primary group in the /etc/passwd file, the user account doesn't appear in the /etc/group file as a member. This has caused confusion for more than one system administrator over the years!

### Creating new groups

The groupadd command allows you to create new groups on your system:

```
# /usr/sbin/groupadd shared
# tail /etc/group
haldaemon:x:68:
xfce:x:43:
gdm:x:42:
rich:x:500:
mama:x:501:
katie:x:502:
Jessica:x:503:
mysql:x:27:
test:x:504:
shared:x:505:
#
```

When you create a new group, no users are assigned to it by default. The groupadd command doesn't provide an option for adding user accounts to the group. Instead, to add new users, use the usermod command:

```
# /usr/sbin/usermod -G shared rich
# /usr/sbin/usermod -G shared test
# tail /etc/group
haldaemon:x:68:
xfce:x:43:
gdm:x:42:
rich:x:500:
mama:x:501:
katie:x:502:
Jessica:x:503:
mysql:x:27:
test:x:504:
shared:x:505:rich, test
#
```

The shared group now has two members, test and rich. The -G parameter in usermod appends the new group to the list of groups for the user account.

> **NOTE**
>
> If you change the user groups for an account that is currently logged into the system, the user will have to log out and then back in for the group changes to take effect.

> **CAUTION**
>
> Be careful when assigning groups for user accounts. If you use the -g parameter, the group name you specify replaces the primary group assigned to the user account in the /etc/passwd file. The -G parameter adds the group to the list of groups the user belongs to, keeping the primary group intact.

### Modifying groups

As you can see from the /etc/group file, there isn’t too much information about a group for you to modify. The groupmod command allows you to change the GID (using the -g parameter) or the group name (using the -n parameter) of an existing group:

```
# groupmod -n sharing shared
# tail /etc/group
haldaemon:x:68:
xfce:x:43:
gdm:x:42:
rich:x:500:
mama:x:501:
katie:x:502:
Jessica:x:503:
mysql:x:27:
test:x:504:
sharing:x:505:test,rich
#
```

When changing the name of a group, the GID and group members remain the same, and only the group name changes. Because all security permissions are based on the GID, you can change the name of a group as often as you want without adversely affecting file security.

## Decoding File Permissions

Now that you know about users and groups, it’s time to decode the cryptic file permissions you’ve seen when using the `ls` command. This section describes how to decipher the permissions and where they come from.

### Using file permission symbols

As you’ll recall from Chapter 3, “Basic Bash Shell Commands,” the `ls` command allows you to see the file permissions for files, directories, and devices on the Linux system:

```
$ ls -l
total 68
-rw-rw-r-- 1 rich rich   50 2025-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich   23 2025-09-13 07:50 file2
-rw-rw-r-- 1 rich rich   48 2025-09-13 07:56 file3
-rw-rw-r-- 1 rich rich   34 2025-09-13 08:59 file4
-rwxrwxr-x 1 rich rich 4882 2025-09-18 13:58 myprog
-rw-rw-r-- 1 rich rich  237 2025-09-18 13:58 myprog.c
drwxrwxr-x 2 rich rich 4096 2025-09-03 15:12 test1
drwxrwxr-x 2 rich rich 4096 2025-09-03 15:12 test2
```

The first field in the output listing is a code that describes the permissions for the files and directories. The first character in the field defines the type of the object:

- `-` for files
- `d` for directories
- `l` for links
- `c` for character devices
- `b` for block devices
- `p` for named pipes
- `s` for network sockets

After that, there are three sets of three characters. Each set of three characters defines an access permission triplet for the object:

- `r` for read permission
- `w` for write permission
- `x` for execute permission

If a permission is denied, a dash appears in the location. The three sets relate to the three levels of security for the object:

- The owner of the object
- The group that owns the object
- Everyone else on the system

This is broken down in Figure 7.1.

### FIGURE 7.1

The Linux file permissions.

![](img/0798d50a0e5dbf1265fbda3832b3e015_186_0.png)

The easiest way to discuss this is to take an example and decode the file permissions one by one:

```
-rwxrwxr-x 1 rich engr 4882 2025-09-18 13:58 myprog
```

The `myprog` file has the following sets of permissions:

- `rwx` for the file owner (set to the login name `rich`)
- `rwx` for the file group owner (set to the group name `engr`)
- `r-x` for everyone else on the system

These permissions indicate that the user login name `rich` can read, write, and execute the file (considered full permissions). Likewise, members in the group `engr` can also read, write, and execute the file. However, anyone else not in the `engr` group can only read and execute the file; the `w` is replaced with a dash, indicating that write permissions are not assigned to this security level.

### Default file permissions

You may be wondering about where these file permissions come from. The answer is `umask`. The `umask` command sets the default permissions for any file or directory you create:

```
$ touch newfile
$ ls -al newfile
-rw-rw-r-- 1 rich    rich      0 Sep 20 19:16 newfile
$
```

The `touch` command created the file using the default permissions assigned to my user account. The `umask` command shows and sets the default permissions:

```
$ umask
0022
$
```

Unfortunately, the `umask` command setting isn't overtly clear, and trying to understand exactly how it works makes things even muddier. The first digit represents a special security feature assigned to the file. You learn more about that later in this chapter in the “Sharing Files” section.

### Part 1: The Linux Command Line

The next three digits represent the octal values of the umask for a file or directory. To understand how umask works, you first need to understand octal mode security settings.

Octal mode security settings take the three rwx permission values and convert them into a 3-bit binary value, represented by a single octal value. In the binary representation, each position is a binary bit. Thus, if the read permission is the only permission set, the value becomes r--, relating to a binary value of 100, indicating the octal value of 4. Table 7.5 shows the possible combinations you'll run into.

**TABLE 7.5 Linux File Permission Codes**

| Permissions | Binary | Octal | Description |
| :--- | :--- | :--- | :--- |
| --- | 000 | 0 | No permissions |
| --x | 001 | 1 | Execute-only permission |
| -w- | 010 | 2 | Write-only permission |
| -wx | 011 | 3 | Write and execute permissions |
| r-- | 100 | 4 | Read-only permission |
| r-x | 101 | 5 | Read and execute permissions |
| rw- | 110 | 6 | Read and write permissions |
| rwx | 111 | 7 | Read, write, and execute permissions |

Octal mode takes the octal permissions and lists three of them in order for the three security levels (user, group, and everyone). Thus, the octal mode value 664 represents read and write permissions for the user and group but read-only permission for everyone else.

Now that you know about octal mode permissions, the umask value becomes even more confusing. The octal mode shown for the default umask on my Linux system is 0022, but the file I created had an octal mode permission of 644. How did that happen?

The umask value is just that, a mask. It masks out the permissions you don't want to give to the security level. You have to dive into some octal arithmetic to figure out the rest of the story.

The umask value is subtracted from the full permission set for an object. The full permission for a file is mode 666 (read/write permission for all), but for a directory it's 777 (read/write/execute permission for all).

Thus, in the example, the file starts out with permissions 666, and the umask of 022 is applied, leaving a file permission of 644.

The umask value is normally set in the /etc/profile startup file (see Chapter 6). You can specify a different default umask setting using the umask command:

```
$ umask 026
$ touch newfile2
```
