• INPUTRC — Sets keyboard mappings for particular situations, based on the contents of the /etc/inputrc file. In particular, the inputrc file makes sure that the Linux console and various terminal windows (xterm and rxvt) all behave sanely.

The last thing that the /etc/profile file does is look at the contents of the /etc/profile.d directory and source in the files that it finds. Each file contains settings that define environment variables or aliases that affect how users can use the shell. For example, the lang files identify the locations of foreign language files. The vim files create aliases that cause vim to be used when vi is typed. The which file defines a set of options used by the which command. You can modify the profile.d files or add your own to have environment variables and aliases set for all of your users.

# # Creating Portable Desktops

Linux is an operating system that was born on the Internet, so it is not surprising that it has such strong networking capabilities. This makes Linux an excellent server, but it also allows Linux to have an excellent desktop workstation, especially in a highly networked environment. Red Hat Linux lets you easily set up your users with a portable desktop that follows them from computer to computer. With other leading desktop operating systems, it is not nearly as easy.

Normally, a Red Hat Linux user’s home directory is located within the /home directory. As an alternative, within the home directory create a directory named after the system’s host name. Within that directory, create the users’ home directories. Thus, on a Linux system named dexter, the user mary would have a home directory of /home/dexter/mary instead of /home/mary. There is a very good reason for doing this.

If you are logged into the Linux system ratbert and wish to access your home directory on dexter as if it were stored locally, the best approach is to use Network File System (NFS) to mount dexter’s /home directory on the /home on ratbert. This results in having the same contents of your home directory available to you no matter which machine you log in to.

> **CROSS-REFERENCE:** You can read more about NFS in Chapter 18.

To mount dexter’s /home directory as described, you would add a line similar to the following in ratbert’s /etc/fstab file:

```
dexter:/home /home nfs defaults 0 0
```

You would also add an entry similar to the following in dexter’s /etc/exports directory:

```
/home ratbert
```

Now, when ratbert boots up, it automatically mounts dexter’s home partition over the network. This enables us to treat the remote files and directories on dexter’s /home as if they are locally stored on ratbert. Unfortunately, this has the side effect of “covering up” ratbert’s actual /home directory.