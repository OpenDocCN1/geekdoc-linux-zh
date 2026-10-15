
## Directory Permissions

Directories are also files under Linux. For example, again use the ls command to show permissions like this:

```
$ mkdir foo
$ ls -ld foo
drwxr-xr-x 2 andrew andrew 4096 2007-02-24 12:14 foo
```

In this example, the mkdir command is used to create a directory. The ls command and its -ld option is used to show the permissions and other information about the directory (not its contents). Here you can see that the directory has permission values of 775 (read+write+execute or 4+2+1, read+write+execute or 4+2+1, and read+execute or 4+1).

This shows that the owner and group members can read and write to the directory and, because of execute permission, also list the directory's contents. All other users can only list the directory contents. Note that directories require execute permission in order for anyone to be able to view their contents.

You should also notice that the ls command's output shows a leading d in the permissions field. This letter specifies that this file is a directory; normal files will have a blank field in place. Other files, such as those specifying a block or character device, will have a different letter.

For example, if you examine the device file for a Linux serial port, you will see

```
$ ls -l /dev/ttyS0
crw-rw---- 1 root root 4, 0 2007-02-24 11:53 /dev/ttyS0
```

Here, /dev/ttyS0 is a character device (such as a serial communications port and designated by a c) owned by root and available to anyone in the uucp group. The device has permissions of 660 (read+write, read+write, no permission).

The mnemonic forms of chmod's options (when used with a plus character, +, to add, or a minus sign, -, to take away) designate the following:

- `u`—Adds or removes user (owner) read, write, or execute permission
- `g`—Adds or removes group read, write, or execute permission
- `o`—Adds or removes read, write, or execute permission for others not in a file's group
- `a`—Adds or removes read, write, or execute permission for all users
- `r`—Adds or removes read permission
- `w`—Adds or removes write permission
- `x`—Adds or removes execution permission

For example, if you create a file, such as a `readme.txt`, the file will have default permissions (set by the umask setting in `/etc/bashrc`) of

```
 -rw-rw-r--    1 andrew    andrew           12 Jan  2 16:48 readme.txt
```

As you can see, you and members of your group can read and write the file. Anyone else can only read the file (and only if it is outside of your home directory, which will have read, write, and execute permission set only for you, the owner). You can remove all write permission for anyone by using chmod, the minus sign, and `aw` like so:

```
$ chmod -aw readme.txt
$ ls -l readme.txt
-r--r--r--    1 andrew    andrew           12 Jan  2 16:48 readme.txt
```

Now, no one will be able to write to the file (except you, if the file is in your home or `/tmp` directory because of directory permissions). To restore read and write permission for only you as the owner, use the plus sign and the `u` and `w` options like so:

```
$ chmod u+rw readme.txt
$ ls -l readme.txt
-rw-------    1 andrew    andrew           12 Jan  2 16:48 readme.txt
```

You can also use the octal form of the chmod command, for example, to modify a file's permissions so that only you, the owner, can read and write a file. Use the chmod command and a file permission of 600, like this:

```
$ chmod 600 readme.txt
```

If you take away execution permission for a directory, files might be hidden inside and may not be listed or accessed by anyone else (except the root operator, of course, who has access to any file on your system). By using various combinations of permission settings, you can quickly and easily set up a more secure environment, even as a normal user in your home directory.

## Understanding Set User ID and Set Group ID Permissions

Another type of permission is “set user ID”, known as suid, and “set group ID” (sgid) permissions. These settings, when used in a program, enable any user running that program to have program owner or group owner permissions for that program. These settings enable the program to be run effectively by anyone, without requiring that each user’s permissions be altered to include specific permissions for that program.

One commonly used program with suid permissions is the passwd command:

```
$ ls -l /usr/bin/passwd
-r-s--x--x 1 root root 13536 Jan 12 2000 /usr/bin/passwd
```

This setting allows normal users to execute the command (as root) to make changes to a root-only accessible file, /etc/passwd.

You also can assign similar permission using the chfn command. This command allows users to update or change finger information in /etc/passwd. You accomplish this permission modification by using a leading 4 (or the mnemonic s) in front of the three octal values.

### NOTE

Other files that might have suid or guid permissions include at, rcp, rlogin, rsh, chage, csh, ssh, crontab, sudo, sendmail, ping, mount, and several UNIX-to-UNIX Copy (UUCP) utilities. Many programs (such as games) might also have this type of permission in order to access a sound device.

Files or programs that have suid or guid permissions can sometimes present security holes because they bypass normal permissions. This problem is especially compounded if the permission extends to an executable binary (a command) with an inherent security flaw because it could lead to any system user or intruder gaining root access. In past exploits, this typically happened when a user fed a vulnerable command with unexpected input (such as a long pathname or option); the command would bomb out, and the user would be presented a root prompt. Although Linux developers are constantly on the lookout for poor programming practices, new exploits are found all the time, and can crop up unexpectedly, especially in newer software packages that haven’t had the benefit of peer developer review.

Savvy Linux system administrators keep the number of suid or guid files present on a system to a minimum. The find command can be used to display all such files on your system:

```
$ sudo find / -type f -perm +6000 -exec ls -l {} \;
```
