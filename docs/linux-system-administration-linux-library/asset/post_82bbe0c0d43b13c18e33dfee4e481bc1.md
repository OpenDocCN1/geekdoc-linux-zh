
# Chapter 1 The Basics of System Administration

essential whenever you need to communicate something to more than one user, but unless you return receipts on your e-mail, you won't know if users have even checked their e-mail at all.

Whichever method of communication is appropriate to your purpose, communication is a critical factor in maintaining a good working relationship with the users who rely on you.

# Working on the System as Root

Root access is the power of the system administrator. There's a t-shirt that bears the message, "Bow down before me I am root," and that isn't far from the way system administrators view things. For a new system administrator, having access to the root password is a very cool thing. Root access means you are unstoppable. The root user, also known as the superuser, has the authority to do anything, anywhere on the entire system. This may include any computers that are networked to that machine as well. You can do very significant things, inherent to your new power is the potential to make very significant mistakes! Root be careful. The general rule is "don't log in root unless you need to." If you need to log in root, perform the task that requires root access and immediately assume the identity of your normal user. You can use the sudo utility, which is described shortly, to minimize the number of commands that you or your staff have to log in as root to perform.

You can use the /etc/security file to restrict the set of terminals from which root can log in. This file is a list of TTY numbers, from vc/1 through vc/11 and tty1 through default, which the login program reads when it is run. The default settings mean root is allowed to log in from any of the virtual terminals but not remotely. Adding pseudoterminals (ttypn) would allow root to log in remotely. This is not secure and in most cases should not be done. To completely disable root login, forcing the use of su instead, /etc/security should be an empty file. Do not delete the /etc/security file, since doing so that root can log in from anywhere. The default setup is very good and should rarely be changed.

NOTE In Linux, terminal and TTY most commonly refer to a virtual terminal, which is simply an alternative login session. There are also physical devices called terminals, which should not be confused with workstations. These telewriter (TTY) devices, consisting of little more than a keyboard and monitor, were the only means of connecting to Unix mainframe and minicomputers through the 1980s and still have uses today. Chapter 12, "Serial Communications," shows how to configure these terminals.

Train yourself and the others who are allowed access to the root password as root and not to abuse the power it gives. A mistake while logged in root could delete files that are required for the system to run properly. We once heard of a system administrator who deleted the /tmp directory, causing the whole system to become unstable. Another system administrator deleted the password file. Still another deleted the entire /home directory, taking all the users' files and functionality away until it could be dumped from a backup tape making his boss very unhappy. In, most of these mistakes are recoverable if you perform regular backups, but they are embarrassing and time-consuming.

# Becoming the Root User

How does one become the root user? This section outlines the most commonly used techniques.

### su

If you logged in the system under your own user account, you need to use the su command to amass the privileges of root. The command allows you to initiate a new shell in which your user ID and group ID are temporarily replaced with the username you seem to "become" root, and you are actually only using an effective user ID and group ID. It is important to note that although you. Your identity is still known to the system; your actions are still very traceable. Command to change to the superuser is:

```
$ su root
```

You will be prompted for the root password and properly authenticate to be granted root access. Failure to do so will send a message to the root user about a failed su attempt.

If you successfully authenticate, you will retain the environment of your original user account but will be allowed to change into directories owned by root, create binaries that would not be executable by your normal account, create files in directories that are restricted to root, and much more. Your PATH will remain as with your normal user, so many of the more dangerous commands will not be accessible unless you specify their full path.

### su -

Adding the - parameter starts a root login shell wherein the environment of the root user is assumed as well. The command for this would be:

```
$ su - root
```

You will be prompted for the root password, and failure to authenticate will leave you as your own owner and send a message of the failed su to the root user. If you authenticate successfully, however, your working directory will be changed to root's home directory. From this point on, you are effectively root, although your identity is still known.

# Starting an X Session as Root

If your network uses the X Window System GUI interface (discussed in Chapter 16, "The X Window System"), you can run an entire X session as root by changing to the root user and then starting X. Everything in that session will be performed as if you had logged in as root from the original login prompt, again your true identity will be recorded. It is easy to forget that you have assumed superuser privileges, so this session should be handled with special care. One method of ensuring that you don't forget you started an X session as root is to use a totally different X environment for the root user than the other users. You might make the background of the root user's X session red or yellow to flag the session as initiated by the superuser.

# sudo

sudo (which stands for "superuser do") is a Linux command that system administrators commonly use to grant "superuser" privileges to a user or group temporarily so that they can perform specific operations which would not be allowed to do. sudo logs its use, keeping track of who used it and what was done. It also sends e-mail to the superuser if someone tries to invoke sudo which does not have the necessary access to. Once authenticated, sudo grants the requested privilege for five minutes (this default is configurable), and each command gets its five minutes. The command looks like this:

```
$ sudo -r now
```

sudo first validates the user's identity by querying for a password. It then consults a file, /etc/sudoers in Red Hat Linux, to determine whether user has permission to execute a command as the specified user or as root if no other user is specified. The /etc/sudoers file looks like this:

```
# sudoers file.
```

```
#
```

```
# This file MUST be edited with the 'visudo' command as root.
```

```
#
```

```
# See the sudoers man page for the details on how to write a sudoers file.
```

```
#
```

```
# Host alias specification
```

```
#
```

```
# User alias specification
```

```
#
```

```
# Cmnd alias specification
```

```
#
```

```
# User privilege specification
```

```
root      ALL=(ALL) ALL
someuser  ALL=(ALL) ALL
```

If the user is listed in /etc/sudoers, a password prompt is issued. If the user can authenticate with the appropriate password, the referenced operation is performed and a five-minute timer will be set. During that five minutes, the authenticated user can perform commands without reauthenticating.

Sudo is a critical tool. Thanks to it, you can grant certain users and administrative staff access to perform some high-level tasks without giving them the root password. (Of course, you'll do this only when the benefit of letting the user handle the task outweighs the potential risks. The user needs to be not only trustworthy but technically competent.) This tool is available on most standard distributions of Linux and is available for most flavors of Unix. For a more extensive description of sudo, visit its home page at http://www.courtesan.com/sudo/man/sudo.html.
