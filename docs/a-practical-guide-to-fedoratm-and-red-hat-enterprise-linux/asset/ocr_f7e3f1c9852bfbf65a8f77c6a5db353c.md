```
$ sudo mount /p03
Sorry, user sam is not allowed to execute '/bin/umount /p03' as root on localhost.
```

The following line limits Sam to mounting and unmounting filesystems mounted on /p01, /p02, /p03, and /p04:

```
sam ALL= /bin/mount /p0[1-4], /bin/umount /p0[1-4]
```

The following commands show the result:

```
$ sudo mount /music
Sorry, user sam is not allowed to execute '/bin/umount /music' as root on localhost.
$ sudo umount /p03
$
```

# Administrator: using the wheel group

As explained under “Administrator and the wheel group” on page 429, the following lines in sudoers allow users who are members of the wheel group (administrators) to use sudo to gain root privileges:

```
## Allows people in group wheel to run all commands
%wheel ALL=(ALL) ALL
```

This user privilege specification applies to all systems (as indicated by the ALL to the left of the equal sign). As the comment indicates, this line allows members of the wheel group (specified by preceding the name of the group with a percent sign: %wheel) to run any command (the rightmost ALL) as any user (the ALL within parentheses). When you call it without the -u option, the sudo utility runs the command you specify with root privileges, which is what sudo is used for most of the time.

If you modified the preceding line in sudoers as follows, it would allow members of the wheel group to run any command as any user with one exception: They would not be allowed to run passwd to change the root password (although they could gain root privileges and edit it manually).

```
%wheel ALL=(ALL) ALL, !/usr/bin/passwd root
```

# optional

In the %wheel ALL=(ALL) ALL line in /etc/sudoers, if you replaced (ALL) with (root) or if you omitted (ALL), you would still be able to run any command with root privileges. You would not, however, be able to use the -u option to run a command as another user. Typically, when you can have root privileges, this limitation is not an issue. Working as a user other than root allows you to use the least privilege possible to accomplish a task, which is a good idea.

For example, if you are in the wheel group, the default entry in the sudoers file allows you to give the following command to create and edit a file in Sam’s home directory. Because you are working as Sam, he will own the file and be able to read from and write to it.

```
$ sudo -u sam vi ~sam/reminder
$ ls -l ~sam/reminder
-rw-r--r-- 1 sam pubs 15 03-09 15:29 /home/sam/reminder
```