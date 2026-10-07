
# Working with Permissions

Hat Linux system include symbolic links, designated by s. (You learn more about symbolic links in “What Are Symbolic Links,” in Chapter 10.)

You can use the chmod command to alter a file's permissions. This command uses various forms of command syntax, including octal or a mnemonic form (such as u, g, o or a rwx, and so on) to specify a desired change. The chmod command can be used to add, remove, or modify file and directory permissions in order to protect, hide, or open up access to a file by other users (except for root, who can access any file or directory on a Linux system).

The mnemonic forms of chmod's options (when used with a plus character, +, to add, or a minus sign, -, to take away) designate the following:

- Add or remove user (owner) read, write, or execute permission
- Add or remove group read, write, or execute permission
- Add or remove read, write, or execute permission for others not in a file's group
- Add or remove read, write, or execute permission for all users
- Add or remove read permission
- Add or remove write permission
- Add or remove execution permission

For example, if you create a file, such as a readme.txt, the file will have default permissions (set by the umask setting in /etc/bashrc) of

```
-rw-r--r-- 1 bball bball 12 Oct 2 16:48 readme.txt
```

As you can see, you and members of your group can read and write the file. Anyone else only read the file (and if it is outside of your home directory, which will have read, write, and execute permission set only for you, the owner). You can remove all permission for anyone by using chmod, the minus sign, and if so like:

```
$ chmod -aw readme.txt
$ ls -l readme.txt
-r--r--r-- 1 bball bball 12 Oct 2 16:48 readme.txt
```

Now, no one will be able to write to the file (except, if you is in your home /tmp directory because of directory permissions). To restore read and write permission for only you as the owner, use the plus sign and the u and rw options like so:

```
$ chmod u+rw readme.txt
$ ls -l readme.txt
-rw------- 1 bball bball 12 Oct 2 16:48 readme.txt
```

You can also use the octal form of the chmod command, for example, to modify a file's permissions so that only you, the owner, can read and write a file. Use the chmod command and a file permission of 600, like this:

```
$ chmod readme.txt
```

If you take execution permission for a directory, files might be hidden inside and may not be listed or accessed by anyone else (except the root operator, who has access to any file on your system). By using various combinations of permission settings, you can quickly and easily set up a more secure environment, even as a normal user in the directory.

# Understanding Set User ID (SUID) and Set Group ID (GUID) Permissions

Another type of permission available for use Linux is set user ID, known as suid, and set group ID (sgid) permissions. These settings, when used in a program, enable any user running that program to have program owner or group owner permissions for that program. These settings enable the program to run effectively by anyone, without requiring that each user's permissions be altered to include specific permissions for the program.

One commonly used with said permissions is the passwd command:

```
$ ls -l /usr/bin/passwd
-rwsr-xr-x 1 root  root 15536 Jul 12 2000 /usr/bin/passwd
```

This setting allows normal users to execute the command (as root) in order to make changes to a root-only accessible file, /etc/passwd.

You can also assign similar permission using the chfn command. This allows users to update or change finger information in /etc/passwd. You accomplish this permission modification by using a leading 4 (or the mnemonic) in front of the three oct values.

> NOTE
Other files that might have suid or guid permissions include at, rcp, login, rsh, chage, chsh, ssh, crontab, sudo, sendmail, ping, mount, and several UNIX-to-UNIX Copy (UUCP) utilities. Many programs (such as games) might also have this type of permission to access a sound device.

Files or programs that have suid or guid permissions can sometimes present security holes because they bypass normal permissions. This problem is especially compounded by the pension extends to an executable binary (a command) with an inherent security flaw because it could lead to any system user or intruder gaining root access. In past exploits, this typically happened when a user fed a vulnerable command with unexpected input (such as a long pathname or option); the command would bomb out, and the user would be presented with a root prompt. Although Linux developers are constantly on the lookout for poor programming practices, new exploits are found all the time, and can crop unexpectedly, especially in newer software packages that hadn't had the benefit of proper code review.

Savvy Red Linux system administrators will keep the number of suid or guid files present on a system to a minimum. The find command can be used to display all such files on your system:

```
# find -type f -perm -6000 -exec ls -l {}
```

> NOTE
The find command is quite helpful for purposes. See "Backing Up, Restoring" in Chapter 11.

Note that the system is not allowed to mount, for example. You will have to decide, as root operator, whether your users are allowed to. Red Hat Linux comes with a command sudo that allows you to run, for example.

# Working As root

# CHAPTER 5 First Steps with Linux

The only time you should run Linux as the superuser is when booting tolevel 1, or maintenance mode, to configure the filesystem. Knowing how to run commands without logging in as root can avoid serious mistakes. Red Hat Linux comes with a command sudo that allows you to run one or more commands as root and then return to a user status. For example, if you'd like to edit your system's filesystem table (a simple file that describes local or remote devices, their type, and location), you can use the sudo command like:

```
$ su -c "vi /etc/fstab"
```

Password:

After you press Enter, you'll be prompted for a password that gives you access to root. Enter.

> CAUTION
Before editing any important system or software configuration, make a backup copy. Then make sure to launch your text editor with line wrapping disabled. If you edit a configuration without line wrapping, you could insert spurious carriage returns and feeds into its contents, causing the configured service to fail when restarting. By convention, nearly all configuration files are formatted for 80-character width, but this isn't always the case. By default, the vi and emacs editors don't use line wrap.

Logging in and using Linux as the root de- the entire concept of file permissions.

You can use sudo to assign specific users permission to perform specific tasks (similar to BSD UNIX and its “wheel” group of users). The sudo command works by first examining the file named sudo /etc directory; you modify this file with the visudo command. See the section “Granting Root Privileges on Occasion—The sudo Command” in Chapter 9, “Managing Users,” for details on how to configure and use sudo.

# Creating Users

When a Red Hat Linux system administrator creates a user, an entry in /etc/passwd for the user is created. The system also creates a directory, labeled with the user’s username, in the /home directory. For example, if you create a user bsmith, the user’s home directory is /home/bsmith.

> NOTE
In this chapter you learn how to manage users from the command line. See Chapter 9, “Managing Users,” for more information on user administration with Red Hat Linux using graphical administration utilities, such as the redhat-config-users client.
