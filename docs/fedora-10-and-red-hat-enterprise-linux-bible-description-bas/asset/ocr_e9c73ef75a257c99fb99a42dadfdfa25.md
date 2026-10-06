# Part III: Administering Fedora and RHEL

```
# useradd -s /sbin/nologin -d /var/html webuser
```

If you were adding a user for mail service only, you might choose to prevent any access to FTP as well. One way to do that is to point the user's home directory to /dev/null. For example:

```
# useradd -s /sbin/nologin -d /dev/null jerryb
```

Once you have set a limited user account, you can further define how your server's users can and cannot access, using features associated with the particular service.

# Creating Portable Desktops

Linux is an operating system that has born on the Internet, so it is not surprising that it has strong networking capabilities. This makes Linux an excellent server, but it also allows Linux to be an excellent desktop workstation, especially in a highly networked environment. Fedora and RHEL let you set up your users in a portable desktop that follows them from computer to computer. With other leading operating systems, it is not nearly as easy.

Typically, a Linux user's home directory is located within the /home directory. As an alternative, the home directory you can create a directory named after the system's name. With that directory, create the users' home directories. Thus, on a Linux system named dexter, mary would have a home directory of /home/dexter/mary instead of /home/mary. There is a very good reason for doing this.

If you are logged into the Linux system ratbert and would like to access your home directory on dexter as it were stored, the best approach is to use Network File System (NFS) to mount dexter/home directory on ratbert. This results in having the same contents of your home directory available to you no matter what machine you log in to.

> CROSS-REFERENCE: You can read more about NFS in Chapter 18.

To mount dexter/home directory as described, you would add a line similar to the following in ratbert's /etc/fstab file:

```
dexter:/home /nfs defaults 0 0
```

You would also add an entry such as the following in dexter's /etc/exports directory:

```
/home ratbert
```

Now, when ratbert boots up, it automatically mounts dexter's home partition over the network. This enables you to treat the remote files and directories on dexter's/home as they are locally stored on ratbert. Unfortunately, this has the side effect of "covering up" ratbert's actual /home/directory.