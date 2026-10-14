
![](img/304f637afcecc491b152ee8ac5afadee_229_0.png)

## Figure 5-5 phpPgAdmin default page

![](img/304f637afcecc491b152ee8ac5afadee_229_1.png)

## Figure 5-6 phpPgAdmin database administration

server. There are two main file servers for Ubuntu that most people favor: Samba and NFS. While both can work across multiple platforms, most administrators tend to favor Samba when their clients are mostly Windows, and NFS when their clients are mostly Linux. Both are relatively simple to set up on Ubuntu.

## Samba

Samba is a program that implements Windows file-sharing protocols, SMB and CIFS. As such it's ideal as a platform for file sharing under Windows, since all of the clients can access the server without additional software. Over time Samba has grown to support advanced sections of Windows file sharing to the point that it can operate much like any other Windows file server or Primary Domain Controller.

## Install Samba

To install Samba, you can either select the Samba Server option during the Ubuntu install or after the install with the tasksel program, or you can install the samba, samba-doc, smbfs, and winbind packages separately with the package manager:

```
$ sudo apt-get install samba samba-doc smbfs winbind
```

The Samba service will start automatically; of course, by default nothing too interesting will be shared, so you will need to tweak Samba's configuration files before any directories are shared.

## Ubuntu Samba Conventions

- /etc/samba/
  This directory contains all of the main configuration files used by Samba, including local password files.

- /etc/samba/smb.conf
  The smb.conf file is the core configuration file for Samba and is used to define file shares and global settings for Samba itself. The default smb.conf file is heavily commented and sets up sane defaults for the file server such as a default workgroup of Workgroup. The file also contains a number of different examples of how to set up shares,

including a useful example configuration that shares out all of the users’ home directories, but by default all of these sample shares are commented out.

- **/etc/init.d/smbd, /etc/init/smbd.conf**
  Samba’s init script has been converted to an Upstart script, although there is still an old init script available as a placeholder. This means that you will use the standard Upstart programs like `start`, `stop`, and `status` to manage the service. Samba automatically starts at system boot by default.

- **/etc/init.d/nmbd, /etc/init/nmbd.conf**
  Like the smbd init script, the nmbd init script is also managed by Upstart now.

- **/usr/bin/smbpasswd**
  This tool is used to create user accounts for Samba. If you want to set up Samba shares that require authentication, you use this tool to create a Samba user database. Samba usernames that you add need to already exist on the system as well. For example, to add an ubuntu user to Samba, I would type

```
$ sudo smbpasswd -a ubuntu
```

I can also use this command when I want to change the password for a particular user. To delete a user from Samba, replace the -a option with -x. You can also temporarily disable Samba users without deleting their accounts. To do this, use the -d and -e options to disable and enable the user, respectively.

- **/usr/share/doc/samba-doc/**
  If you installed the `samba-doc` program, you will find Samba documentation and example configuration files under this directory.

- **/var/lib/samba**
  This directory contains all of the different databases used by Samba, including the user and password database used by smbpasswd.

## /var/log/samba/

Samba logs in to its own directory and creates separate log files for the smbd and nmbd processes (log.nmbd and log.smbd respectively) as well as a separate log for each host that accesses Samba. This organization can make it easier to narrow down to the logging information you need.

## Sample Samba Configuration

A good way to set up a new Samba share is to read the comments in the /etc/samba/smb.conf file. There are many different examples that show you how to share the user home directories or the CD-ROM drive, for instance. In this example I will show how to share a directory located at /mnt/share so that everyone on the network can access and write to it as a general storage location. Open /etc/samba/smb.conf in your preferred text editor and move to the bottom of the file. Then add the following:

```
[general]
    path = /mnt/share
    comment = General Storage
    writeable = Yes
    browseable = Yes
    guest ok = Yes
    force user = ubuntu
```

In this example I have set up the /mnt/share directory so that anyone on the network can write to it (writeable = Yes, guest ok = Yes) and use the force user = ubuntu option so that when a user creates a file on the share, it will be owned by the local user named ubuntu. Of course you would want to change this user from ubuntu to a user that exists on your system. Now I can create the shared directory and make sure that its permissions are set so that the local ubuntu user can write to it:

```
$ sudo mkdir /mnt/share
$ sudo chown ubuntu:ubuntu /mnt/share
```

One nice feature of Samba is that I can add or tweak a share like the one above without having to restart Samba. This is handy because when you restart Samba, any user accessing a file on the share will temporarily be disconnected from the file. Certain programs react very poorly to having
