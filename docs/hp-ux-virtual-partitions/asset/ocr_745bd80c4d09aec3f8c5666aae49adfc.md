users may find it convenient to not have to enter a password when logging into a remote system, you have given every user in /etc/hosts.equiv access to the entire network. If you could ensure that all the permissions on all the files and directories on all systems were properly set up, then you wouldn't care who had access to what system. In the real UNIX world, however, permissions are sometimes not what they are supposed to be. Users have a strong tendency to "browse around," invariably stumbling upon a file they want to copy to which they really shouldn't have access.

# /.rhosts

This file is the /etc/hosts.equiv for superuser. If you log in as root, you want to have this file configured with exactly the same information as /etc/hosts.equiv. If you do, however, you have compounded your network security risk by allowing superuser on any system to log in to a remote system without a root password. If you are the undisputed ruler of your network and you're 100 percent certain that no security holes exist, then you may want to set up /.rhosts so that you don't have to issue a password when you log in remotely to a system as superuser. From a security standpoint, however, you should know that this setup is frowned upon.

If the appropriate changes have been made to the appropriate entries in /etc/hosts, /etc/hosts.equiv, and /.rhosts, you can use the ARPA Services commands ftp and telnet, as well as the Berkeley commands rcp, rologin, rmesh, and rwho.

I have described the process of setting up the appropriate files to get the most commonly used ARPA Services up and running. There is sometimes even more advanced functionality, such as DNS/BIND, required. Your system may have DNS/BIND or similar functionality set up that gives you access to some or all of the commands covered throughout this section.

# Network File System (NFS)

NFS allows you to mount disks on remote systems so that they appear as though they are local to your system. Similarly, NFS allows remote systems to mount your local disk so that it looks as though it is local to the remote system. Configuring NFS to achieve this functionality is simple. Here are the steps to go through in order to configure NFS: