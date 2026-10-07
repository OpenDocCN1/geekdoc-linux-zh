You can also use the octal form of the chmod command, for example, to modify a file's
permissions so that only you, the owner, can read and write a file. Use the chmod
command and a file permission of 600, like this:

```
$ chmod readme.txt
```

If you take execution permission for a directory, files might be hidden inside and
may not be listed or accessed by anyone else (except the root operator, who has
access to any file on your system). By using various combinations of permission settings,
y can quickly and easily set up a more secure environment, even as a normal user in
the directory.

# Understanding Set User ID (SUID) and Set Group ID (GUID)
Permissions

Another type of permission available for use Linux is set user ID, known as suid, and
set group ID (sgid) permissions. These settings, when used in a program, enable any user
running that program to have program owner or group owner permissions for that
program. These settings enable the program to run effectively by anyone, without
requiring that each user's permissions be altered to include specific permissions for the
program.

One commonly used with said permissions is the passwd command:

```
$ ls -l /usr/bin/passwd
-rwsr-xr-x 1 root  root 15536 Jul 12 2000 /usr/bin/passwd
```

This setting allows normal users to execute the command (as root) in order to make
changes to a root-only accessible file, /etc/passwd.

You can also assign similar permission using the chfn command. This allows
users to update or change finger information in /etc/passwd. You accomplish this
permission modification by using a leading 4 (or the mnemonic) in front of the three
ctal values.

> NOTE
Other files that might have suid or guid permissions include at, rcp, login, rsh, chage, chsh, ssh, crontab, sudo, sendmail, ping, mount, and several UNIX-to-UNIX Copy (UUCP) utilities. Many programs (such as games) might also have this type of permission to access a
sound device.

Files or programs that have suid or guid permissions can sometimes present security holes
because they bypass normal permissions. This problem is especially compounded by the
pension extends to an executable binary (a command) with an inherent security flaw