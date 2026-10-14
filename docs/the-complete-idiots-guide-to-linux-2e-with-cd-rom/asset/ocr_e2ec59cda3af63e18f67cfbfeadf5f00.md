```
[alberto@digital alberto]$ passwd
Changing password for alberto
(current) UNIX password: ********
Enter new UNIX password: ********
Retype new UNIX password: ********
passwd: all authentication tokens updated successfully
```

The superuser (root) can use the same passwd command to change any password in the system. When the superuser provides a username as an option to the command, he or she can change the password for any user in the system. The superuser does not need to authenticate the user's password. Changing a user's password as the superuser would look like this:

```
[root@digital /root]# passwd alberto
Enter new UNIX password: ********
Retype new UNIX password: ********
passwd: all authentication tokens updated successfully
```

# Changing Your Shell: chsh

If you don't like your shell, you can use the chsh command to change it. Only shells listed in /etc/shells are acceptable for use. It can be used interactively, like this:

```
alberto@digital alberto]$ more /etc/shells
/bin/bash
/bin/sh
/bin/ksh
/bin/csh
/bin/tcsh
[alberto@digital alberto]$ chsh
Changing shell for alberto.
Password: ********
New shell [/bin/tcsh]: /bin/bash
Shell changed.
```

If the shell you like is not listed, add an entry to the /etc/shells file, and then you'll be able to set it.

# Changing Personal Information: chfn

The chfn (change finger name) command changes additional information about yourself, such as your full name, office address, and office and home phone numbers. This information is accessible using the finger command (which is typically disabled in most systems because it poses certain security risks). It is used by some programs to determine your full name and other information. The chfn command, like the passwd command, is interactive:

```
[alberto@digital alberto]$ chfn
Changing finger information for alberto.
Password: *********
Name [Caldera OpenLinux User]: Alberto Ricart
Office []: Rm. 3210 Left Wing
Office Phone []: 800 555 1212 ext 800
Home Phone []: not listed

Finger information changed.
```

# Who's on the System: who and w

The who and w commands can be used to see who is logged into the system. The w tells you who is logged on and what they are doing: