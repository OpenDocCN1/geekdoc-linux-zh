
automount where to look for a file system to mount on the mount point. The indirect map, the name of which does not start with a hyphen, names a file in /etc that contains names of file systems to mount under the mount point along with the remote machine and path name of the file system.

A special or built-in map deals with remote file systems in a specific manner. There are three special maps: -hosts, -xfs, and -null. The -hosts special map works by default with the /net autofs mount point. If you access /net/<hostname>, <hostname> is automatically expanded to a list of all file systems exported from server <hostname>. These file systems are then mounted under /net/<hostname>. The -xfs special map works with Sun’s Federated Naming Service (FNS). These directories are mounted under /sfn. The -null map disables the entries that are inherited from NIS or NIS+. In order to be effective, any of the -null entries must precede the +auto-master entry.

> **TIP** The /home directory is under the control of automountd. If you put a new user named Kay with a home directory in /home/kay, automounting will fail. However, putting Kay’s home directory in /export/home/kay will work once you change the passwd file entry to /export/home/kay and put an entry into /etc/auto-home.

## Unmounting Remote File Systems

Files that have been mounted on remote file systems will need to be unmounted at some point. The following example demonstrates how to use the umount command to unmount files from remote file systems:

```bash
% umount /var/mail
```

This command tells umount to check /etc/mnttab to get the information necessary to unmount the appropriate file system from the correct server.

It is also possible to unmount all remote file systems with the single command umountall. Used with the -F option, this command will unmount all NFS file systems from all remote hosts. The syntax for this command is as follows:

```bash
% umountall -F nfs
```

If a file system is in use when umount is trying to unmount it, a message will be displayed such as the one shown here:

```bash
nfs umount: /opt/reliant: is busy
```

You can use the -k option with umountall to find processes that are using the file system that it is trying to unmount, to terminate them, and then to attempt to unmount the file system again. If that fails, ask all the users to log off the system, kill any processes that may still be using the file system you wish to unmount, and try it again. You may have to reboot the system if all else fails.

Because the `-F option designates the types of file systems to unmount, you can also use umountall to unmount all file systems that were mounted by automount, UFS, or any type of file system. The following example demonstrates this:

```bash
# umountall -F -K nfs
# umountall -F ufs
# umountall -F lofs
# umountall -F autoifs
```

The second command will unmount local UFS file systems not in use but will fail on the root file system simply because most of the system daemons are started from the root hierarchy. The third command will unmount all loopback file systems usually referred to as LOFS. A loopback file system is created by automount when the automount map indicates that the mount point is on a local machine. If you use automount to mount a LOFS, you will not be able to unmount the UFS file system that houses the mounted LOFS until the LOFS is unmounted.

### Other File System Commands

You can use the dfmounts command with a host name as the argument. It will display the resources that are mounted from the server you specify. The syntax for dfmounts is displayed here:

```bash
dfmounts [<options>] [<hostname>]
```

If used without the host name, dfmounts will report on local file systems that are exported and can be mounted by remote hosts. If you use the host name as an argument, dfmounts will report on file systems that are local to the host name and are exported.

The automount daemon controls a directory that has been assigned as an autoifs mount point. You cannot have the same directory as an autoifs mount point and as an entry that is mounted using /etc/vfstab. You should never put a /home entry in /etc/vfstab because the /etc/auto-master file also has an entry for /home. The vfstab version of /home will disappear each time you reboot the system.

You can disable automounting of /home; delete or comment out the /home entry from the /etc/auto-master file simply by starting the line with a #. If you want to disable automounting completely, use mv to rename /etc/rc2.d/S74autofs to /etc/rc2.d/.S74autoofs and reboot. Giving this file an invisible filename keeps it from being seen and executed. It will still be there, however, if you want to recall it.

### Network Utilities

Solaris 8 provides utilities that you should become familiar with and use when communicating with networks. If you will be using the Internet (see Chapter 14), you will use these tools often. By using a common convention for the format of network addresses, Sun has modified existing tools to use on the Internet much as you would use them on a local network. Whenever an @ sign is used, a utility such as finger or talk interprets that to mean that you are looking for a remote host computer. If the @ sign is not used, the utility assumes that you are corresponding with someone on your local host computer.

> **TIP** The prevalence of networks has created the need for newer utilities to control and monitor their activities. The commands that are discussed in this section were created specifically for systems on a network. They will not be of use with stand-alone computers.

To display information about users on remote systems, use the finger utility. Although it was originally designed to use on local networks, it has been enhanced to perform with remote networks.

You can use the user's name or login name in front of the @ sign. This causes finger to retrieve the information from the remote system for that user only. If there is more than one incidence of the user's name on the remote system, finger will display the results for all. Figure 9.10 displays how finger works.

This utility works by querying a standard network service, the fingd daemon that runs on the remote system. Solaris supplies this service but some sites do not run it simply to minimize the load on their system, to reduce security risks, or to maintain privacy.

> **TIP** It is the remote fingd daemon that shares information with your system and decides how much information will be shared and in what format. The fingd daemon gives account information on the system that can be viewed by anyone. Many sites disable finger and randomize user account IDs to maintain privacy.

Reports may have a different appearance than those shown in Figure 9.10. The appearance of the information for remote finger is similar to the appearance of the information for local finger with just one difference: finger will report the name of the remote system before displaying the results. The name of the host that answers may not be the system name you specified on the command line, depending on how the daemon service is configured at the remote end. Several host names may be listed if the finger daemon needs to contact another to retrieve information.

![](img/256e02a6afce528d264a8d911fa0ff20_391_0.png)

### Remote Login Utilities

You can use the rlogin utility to connect and log in to an account on a remote system via the network if you want to access a special application or device available on a remote system where you have an account set up. It can be faster to take advantage of a remote system and then log out when your task has been completed. If you use a window system on your local computer, you have the ability to use many systems simultaneously by logging in to each one through a different window. To log out from a remote login, you would use the exit command at the command prompt.

When you log in remotely, the network can perform authentication to determine the user. Network authentication usually takes precedence over system authentication. When the remote system authenticates the user, the user is asked for a password unless the user is listed in the /etc/hosts.equiv or .rhosts file. In that case, the network can authenticate the user and no additional passwords are required.

The Telnet utility also lets you interact with a remote computer. It is similar to rlogin but will work in places where rlogin is not available. Unix supports Telnet access more heavily than it supports rlogin. Figure 9.11 shows how the remote utility logs in to a remote system using Telnet.
