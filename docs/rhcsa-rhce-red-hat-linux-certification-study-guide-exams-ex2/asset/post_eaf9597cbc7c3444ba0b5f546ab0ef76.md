
In contrast, the following command changes the name of the group named project to secret:

```
# groupmod secret project
```

Exam Watch
The chage command is an excellent way to address the RHCE objective to “adjust password aging for local user accounts.”

## chage

The chage command is primarily used to manage aging information for a password, as stored in the /etc/shadow file. While some of the parameters can also be set with the useradd and usermod commands, most of the switches are different, as described in Table 8-8.

## TABLE 8-8
chage Command Options

| Option | Purpose |
|---|---|
| -d YYYY-MM-DD | Sets the last change date for a password; output shown in /etc/shadow as the number of days after January 1, 1970. |
| -E YYYY-MM-DD | Assigns the expiration date for an account; output shown in /etc/shadow as the number of days after January 1, 1970. |
| -I num | Locks an account num days after a password has expired; can be set to -1 to make the account permanent. |
| -l | Lists all aging information. |
| -m num | Sets a minimum number of days that a user must keep a password. |
| -M num | Sets a maximum number of days that a user is allowed to keep a password; can be set to -1 to remove that limit. |
| -W num | Specifies the number of days before a password must be changed; a user is warned at that time. |

## CERTIFICATION OBJECTIVE 8.02

### Administrative Control

As the root administrative user is all-powerful, it's important for administrators to execute most actions as the regular user. Limits on regular users can help protect Linux systems from accidents. Regular users who have the root administrative password can temporarily take root privileges with the su command. The su command can do more with other accounts. In contrast, the sg command is associated with privileges on special groups.

While the su command is adequate for small networks, no administrator should work alone. With the help of the sudo command configured in the /etc/sudoers file, it's possible to set up dedicated administrators with partial or complete root administrative privileges.

### The Ability to Log In as root

It's possible to keep users from logging in directly as the root administrative user. Local access is regulated in the /etc/securetty file. By default, it contains access directives for 12 virtual consoles. While only six virtual consoles are enabled in the /etc/init/start-ttys.conf file discussed in Chapter 5, it is possible to configure 12 (based on the number of function keys on a keyboard).

The virtual consoles listed in /etc/securetty determine the consoles where the root administrative user is allowed to log in. If the directives in this file were commented out, administrators would not be able to log in directly to the root account. They'd have to log in to a regular account and use either the su or sudo command for administration.

While it's still possible to log in remotely as the root administrative user with the ssh command, that ability can also be regulated. The configuration of the SSH server in this manner is an RHCE skill described in Chapter 12.

## EXERCISE 8-3

### Limit root Logins

In this exercise, you'll examine the effect of eliminating the consoles in the /etc/securetty file. But first, you'll confirm that the root administrative user can log in to the standard consoles on virtual terminals 1 through 6. This exercise assumes that a regular account is available on the local system.

- 1. Move to the second virtual console. Press CTRL-ALT-F2; alternatively, in a KVM VM, click Send Key | CTRL-ALT-F2. At the login: prompt that appears, log in as the root user.
- 2. Repeat the process with the first, third, fourth, fifth, and sixth virtual consoles. Unless /etc/securetty has already been changed, you should be able to log in as the root user in all of these consoles.
- 3. Back up the current /etc/securetty file.
- 4. Open the /etc/securetty file in a text editor. Comment out all of the directives. Save the file.
- 5. Log out of the console. Try logging back in as the root administrative user. What happens? Repeat the process in other virtual consoles. What happens?
- 6. Log in to a console as a regular user. Does it work? Run the su - command to assume root privileges. Restore the original /etc/securetty file.
- 7. If a regular user account doesn't exist on the system, you'll have to reboot the system in single-user mode, as discussed in Chapter 5. You'll then be able to restore the /etc/securetty file from the prompt that appears.

### The Ability to Log In

Beyond the /etc/securetty file is /etc/security/access.conf, which regulates access by all users. While the default version of this file is completely commented out, but the comments provide useful examples. The first example would disallow (with the -) access to the first virtual console (tty1) to ALL users but root:

```
-:ALL EXCEPT root:tty1
```

Jump ahead in the file. The following line is a slightly more complex example that would disallow access to all users, except users who are members of the wheel group, along with the shutdown and sync users, on the LOCAL system.

```
-:ALL EXCEPT (wheel) shutdown sync:LOCAL
```

Scroll down further in the file. The following lines allow (with the +) the root user to access the system from three specific remote IP addresses, along with the localhost address:

```
+ : root : 192.168.200.1 192.168.200.4 192.168.200.9
+ : root : 127.0.0.1
```

If you're protecting a system from outside networks, this type of limitation on direct root administrative access makes sense. As long as the su or sudo command allows, users who log in remotely as regular users can still elevate their privileges accordingly.

Be aware, the directives in this line are cumulative, and they are considered in order. So if directives that allow access (with the +) come first, then the following directive denies access to all other users from all other local or remote systems:

```
- : ALL : ALL
```

### The Proper Use of the su Command

In some cases, such as Red Hat exams, it's appropriate to log in as the root administrative user. But in practice, it's best to log in as a regular user. As a regular user, you can temporarily log in with root administrative privileges with the su command. Normally, that command prompts for the password of the root administrative user. After you've completed administrative tasks, it's best to log out of the root administrative account; the exit command would return to the regular account of that user.

The su - command is slightly different, as it accesses the full privileges of the root administrative account. If the password is accepted, it navigates to the root user's home directory, /root.

If you have the password of a second user, you can use the su - username command to log in directly to that account. For example, if I wanted to log in to user dickens' account, I'd run the su - dickens command. When I enter her password successfully, the command takes me to the /home/dickens directory.

Finally, the su -c command can be used to assume administrative privileges for one command. For example, the following command can be used to modify the first virtual drive on a system (assuming the root administrative password is successfully entered in response to the prompt):

```
$ su -c '/sbin/fdisk /dev/vda'
```

### Limit Access to su

As discussed earlier, the ability to log in directly as the root administrative user can be regulated. Further limitations on administrative access are possible. For example, you can limit the users who are allowed to run the su command. This requires two basic steps.

First, you'll need to list the users who should have access to the su command. Make them a part of the wheel group. By default, this line in /etc/group looks like:

```
wheel:x:10:root
```

You can add selected users to the end of this line directly, with the usermod -G wheel username command, or with the User Manager.

Second, this requires a change to the configuration of Pluggable Authentication Modules (PAM). While PAM, as described in Chapter 10, is an RHCE objective, there's a commented directive available in the /etc/pam.d/su file, ready for this purpose.

```
# auth required pam_wheel.so use_uid
```

If this line is activated, only users who are members of the wheel group are allowed to use the su command.

### The Proper Use of the sg Command

With the sg command, you can execute another command with the rights associated with a special group. This assumes you've set up a group password for the project group with the gpasswd project command. Then the sg project -c command allows you access to files and directories owned by the group named project. For example, if the /home/secret directory is owned by the project group, and you know the password set with the gpasswd command, the following command copies the important.doc file to the noted directory:

```
$ sg project -c 'cp important.doc /home/project'
```

### Custom Administrators with the sudo Command

Alternatively, you can limit access to the sudo command. Regular users who are authorized in /etc/sudoers can access administrative commands with their own password. You don't need to give out the administrative password to everyone who thinks they know as much as a Red Hat certified professional, as you will be.
