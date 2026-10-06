
If a permission is denied, a dash appears in the location. The three sets relate the three levels of security for the object:

- The owner of the object
- The group that owns the object
- Everyone else on the system

This is broken down in Figure 6-1.

## FIGURE 6-1

The Linux file permissions

![](img/adcbcf1053b52dbf22f3aa187738232f_192_0.png)

The easiest way to discuss this is to take an example and decode the file permissions by one:

```
-rwxwxrxr-x 1 rich rich 4882 2007-09-18 13:58 myprog
```

The file myprog has the following sets of permissions:

- rwx for the file owner (set to the login name rich)
- rwx for the file owner (set to the group name rich)
- r-x for everyone else on the system

These permissions indicate that user login name rich can read, write, and execute the file (considered full permissions). Likewise, members in the rich group can also read, write, and execute the file. However, anyone else not in the rich group can only read and execute the file; the w is replaced with a dash, indicating that write permissions are not assigned to this security level.

## Default file permissions

You may be wondering where these file permissions come from. The answer is, umask. The umask command sets the default permissions for any file or directory you create:

```
$ touch newfile
$ ls -al newfile
-rw-r---- 1 rich rich 0 Sep 20 19:16 newfile
$
```

# Part I The Linux Command Line

The touch command created the default permissions assigned to my user account. The umask command shows and sets the default permissions:

```
$ umask
0022
```

Unfortunately, the umask command setting isn't clear, and trying to understand exactly how it works makes things even muddier. The first digit represents a special feature called the sticky bit. We'll talk more about later on in this chapter in the "Sharing Files" section.

The next three digits represent the octal values of the umask for a file or directory. To understand how umask works, you first need to understand octal mode security settings.

Octal mode security settings take the three rwx permissions values and convert them into a 3-bit binary value, represented by a single octal value. In the binary representation, each position is a binary bit. Thus, if the read permission is the only permission set, the value becomes r--, relating to a binary value of 100. Table 6-5 shows the possible combinations you'll run into.

Octal mode takes the octal permissions and lists three of them in order for the security levels (user, group, and everyone). Thus, the octal mode 664 represents read and write permissions for the user and group, but read-only permission for everyone else.

Now that you know about octal mode permissions, the umask value becomes even more confusing. The octal mode shown for the default umask on my Linux system is 0022, but the file I created had an octal permission of 644. How did that happen?

## TABLE 6-5
Linux File Permission Codes

| Permissions | Binary | Octal | Description |
| --- | --- | --- | --- |
| --- | 000 | 0 | No permissions |
| -x | 001 | 1 | Execute-only permission |
| -w | 010 | 2 | Write-only permission |
| -wx | 011 | 3 | Write and execute permissions |
| r-- | 100 | 4 | Read-only permission |
| r-x | 101 | 5 | Read and execute permissions |
| rw- | 110 | 6 | Read and write permissions |
| rwx | 111 | 7 | Read, write, and execute permissions |

## Understanding Linux File Permissions

The umask value is just that, a mask. It masks out the permissions you don't want to give to the security level. Now we have to dive into some octal arithmetic to figure out the rest of the story.

The umask value is subtracted from the full permission set for an object. The full permission for a file is 666 (read/write permission for all), but for a directory it's 777 (read/write/execute permission for all).

Thus, in the example, the file starts out with permissions 666, and the umask of 022 is applied, leaving a file permission of 644.

The umask value is normally set in the /etc/profile startup file (see Chapter 5). You can specify a different default umask setting using the umask command:

```
$ umask 026
$ touch newfile2
$ ls -l newfile2
-rw-r--r-- 1 rich rich 0 Sep 20 19:46 newfile2
$
```

By setting the umask to 026, the default file permissions become 640, the new file is restricted to read-only for the group members, and everyone else on the system has no permissions to it.

The umask value also applies to making new directories:

```
$ mkdir newdir
$ ls -l
drwxr-x-x 2 rich rich 4096 Sep 20 20:11 newdir/
```

Since the default permissions for a directory are 777, the resulting permissions from the umask are different from those of a new file. The 026 umask value is subtracted from 777, leaving the 751 directory permission setting.

## Changing Security Settings

If you've already created a file or directory, and need to change the security settings on it, there are a few different utilities available in Linux. This section shows how to change the existing permissions, the default owner, and the default group settings for a file or directory.

## Changing permissions

The chmod command allows you to change the security settings for files and directories. The format of the chmod command is:

```
chmod options mode file
```

# The Linux Command Line

The mode parameter allows you to set the security settings using either octal or symbolic mode. The octal mode settings are pretty straightforward; use the standard three-digit octal code you write the file to have:

```
$ chmod 760 newfile
$ ls -l newfile
-rw-xr-- 1 rich 0 Sep 20 19:16 newfile*$
```

The octal file permissions are automatically applied to the file indicated. The symbolic mode permissions are not so easy to implement.

Instead of using the normal string of three sets of three characters, the chmod command takes a different approach. The format for specifying a permission in symbolic mode is:

```
[ugoa...][++-]=rwXstugo...]
```

Makes perfectly good sense, isn't it? The first group of characters defines to whom the new permissions apply:

- u for the user
- g for the group
- o for others (everyone)
- a for all of the above

Next, a symbol is used to indicate whether you want to add the permission to the existing permissions (+), subtract the permission from the existing permission (–), or set the permissions to the value (=).

Finally, the third symbol is used for the setting. You may notice that there are more than the normal rwx values here. The additional settings are:

- X to execute permissions only if the object is a directory or if it already had execute permissions
- s to set the GID
- t to save execution
- u to set the permissions to the owner's permissions
- g to set the permissions to the group's permissions
- o to set the permissions to the other's permissions

Using these permissions looks like this:

```
$ chmod o+r newfile
$ ls -l newfile
-rw-r-- 1 rich 0 Sep 20 19:16 newfile
```

The o+r entry adds the read permission to whatever permissions the everyone already had.

```
$ chmod u-x newfile
$ ls -l newfile
-rw-rw-- 1 rich 0 Sep 20 19:16 newfile
```

The u-x entry removes the execute permission that the user already had. Note that the settings for the ls command indicate if a file has execution permissions by adding an asterisk to the filename.

The options parameters provide a few additional features to augment the behavior of the chmod command. The -R parameter performs the file and directory changes recursively. You can use wildcards for the filename specified, changing the permissions on multiple files with just one.

## Changing ownership

Sometimes you need to change the owner of a file, such as when someone leaves an organization or a developer creates an application that needs to be owned by a system account when it's in production. Linux provides two commands for doing that. The chmod command makes it easy to change the owner of a file, and the chgrp command allows you to change the default group of a file.

The format of the chmod command is:

```
chown options owner[.group] file
```

You can specify either the login name or the numeric UID for the new owner of the file:

```
$ chown dan newfile
$ ls -l newfile
-rw-r-- 1 dan rich 0 Sep 20 19:16 newfile*
```

Simple. The chmod command allows you to change both the user and group of a file:

```
$ chown dan.dan newfile
$ ls -l newfile
-rw-rw-- 1 dan dan 0 Sep 20 19:16 newfile*
```

If you really want to get tricky, you can just change the default group for a file:

```
$ chown .rich newfile
$ ls -l newfile
-rw-r-- 1 dan rich 0 Sep 20 19:16 newfile*
```
