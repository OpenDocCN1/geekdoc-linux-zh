
## FIGURE 7-33

sftp connection.

![](img/37f079cee226b270f2e09b37a2e4a05d_204_0.png)

After the connection is made, sftp allows control using a set of interactive commands. The full list can be viewed using the **man sftp** command. Some of the more commonly used commands are:

- **bye**: Allows you to quit sftp.
- **cd <path>**: Allows you to change the path on the remote FTP server.
- **get <remote_filename> <local_filename>**: Retrieves the remote file and stores it on the local drive. If the local_filename is not given, a filename the same as the remote is used and the file is stored in the current local directory.
- **lcd <path>**: Changes directories on the local drive to the path indicated.
- **lpwd**: Prints the local computer’s current directory.
- **put <local_filename> <remote_filename>**: Copies a file from the local drive to the remote drive.
- **pwd**: Displays the remote current directory.
- **!<command>**: Allows execution of a command on the local machine from the sftp command prompt.

The following is a sample session using sftp to copy the file **for_case** from the **/root** directory on a remote server to the local client’s **/home/jsmith** directory.

```
sftp> cd /root
sftp> pwd
Remote working directory: /root
sftp> ls
if_test
for_case
for_ls
mytar.tar.z
sftp> lcd /home/jsmith
sftp> lpwd
Local working directory: /home/jsmith
sftp> !ls
sftp> get for_case
Fetching /root/for_case to for_case
sftp> !ls
for_case
sftp>
```

Line 1 changes the directory on the remote server to /root.

Line 2 prints the working directory on the remote server.

Line 4 lists the files in /root on the remote server.

Line 9 changes the directory on the local client to /home/jsmith.

Line 10 prints the working directory on the local client.

Line 12 executes a command on the local client to list the current directory.

Line 13 retrieves the file for_case from the remote server to the local client.

Line 15 executes a command on the local client to list the current directory.

The following is a sample session using sftp to copy the file displaysettings.png from the /screenshots directory on the local client to the /root directory on the remote server.

```
sftp> cd /root
sftp> pwd
Remote working directory: /root
sftp> ls
if_test
mytar.tar.z
for_case
for_ls
sftp> lcd /screenshots
sftp> lpwd
Local working directory: /screenshots
sftp> lls
displaysettings.png
displaysettings2.png
InformationSettings.png
sftp> put displaysettings.png
Uploading displaysettings.png to /root/displaysettings.png
sftp> ls
displaysettings.png
if_test
for_case
for_ls
mytar.tar.z
sftp>
```

Line 1 changes directory on the remote server to /root.

Line 2 prints the working directory on the remote server.

Line 4 lists the files in /root on the remote server.

Line 9 changes the local client directory to /screenshots.

Line 10 prints the working directory on the local client.

Line 12 executes a command on the local client to list the current directory.

Line 16 copies the file displaysettings.png from the local client to the remote server.

Line 18 lists the directory on the remote server.

## Accessing Shares

The Linux operating system allows access to network shares. Two types of shares are Server Message Block (SMB) and Network File System (NFS). A share is a directory on a remote server that a client can connect to and use as remote disk space. Files can be copied to and from the share. The remote share can be mounted on the local file system for easy access.

### SMB/CIFS Shares

Microsoft Windows uses the SMB protocol, renamed Common Internet File System (CIFS). This protocol is used to share a directory on a server to allow clients to access the remote resource. SMB allows for file exchange.

Linux distributions include tools for accessing SMB shares. The main package for SMB is called Samba. The two major client programs for accessing remote shares are smbclient and smbmount.

The smbclient program allows you to connect to a remote share and manage files. To connect to a remote share, you should have an account on the remote server. To use smbclient use the syntax **smbclient //server/share**, where *server* is the remote server name and *share* is the share name of the remote shared directory. For example, to connect to a remote server named **Hephaestus** with a shared directory called **dfs-software**, use the following code:

```
$ smbclient //hephaestus/dfs-software
added interface ip=130.160.46.23 bcast=130.160.46.255 nmask=255.255.255.0
added interface ip=130.160.46.84 bcast=130.160.46.255 nmask=255.255.255.0
Password:
Domain=[CS-DEPARTMENT] OS=[Windows 5.0] Server=[Windows 2000 LAN Manager]
smb: \>
```

The prompt is displayed as **smb:\>**, indicating that you are using an SMB (*smb*) share and your current directory is the root (*\*) of the shared directory. When you connect, the remote machine is given your username. If the username is valid, the remote machine will then ask for a password to authenticate you.

After you connect to a remote share you can use commands similar to those of sftp to manage files. Common commands are:

- **! [command]**: Runs a command on the local client. If no command is given, a local shell is run.
- **cd <path>**: Used to change directory on the remote server.
- **del <filename>**: Used to delete files on the remote server.
- **dir**: Used to list files on the remote server.
- **get <remote_filename> [local_filename]**: Used to copy a file from the remote server to the local client. If no local filename is used, the remote filename is used.
- **lcd**: Lists the current directory of the local client.
- **mkdir <directory>**: Creates a directory on the remote server.
- **put <local_filename> [remote_filename]**: Copies a file from the local client to the remote client. If no remote filename is given, the local filename is used.
- **quit**: Exits the smbclient program.
- **rmdir <directory>**: Removes a directory from the remote server.

The easiest way to manage a remote directory is to mount the directory locally. The smbmount command is used to do this. The syntax is similar to the mount command, **smbmount //server/share <local_directory>**, where *server* is the name of the remote server, *share* is the name of the shared directory, and *local_directory* is a directory on the client machine. After a file is mounted, it can be managed in the local directory using standard shell commands.

To mount a directory called **dfs-software** on server **hephaestus** to the local directory **/mnt/hssoftware**, use the following command sequence:

```
# smbmount //hephaestus/dfs-software /mnt/hssoftware
Password:
# cd /mnt/hssoftware/axis
# ls
2120ig.pdf 2120um.pdf axis2120.bin Axis FAQ.doc
#cp 2120ig.pdf /root
# cd /
# smbunmount /mnt/hssoftware
#
```

After the directory is mounted, commands to change the directory, list files, and copy files can be used. To unmount the directory, use the **smbunmount** command.

## NFS Shares

NFS shares are a Unix design from Sun Microsystems. Network File System (NFS) is the preferred method for file sharing between Linux systems.

To use NFS you use the *mount* command. The basic syntax of mount is *mount <server>:<share> <local_directory>*, where *server* is the name of the remote server, *share* is the name of the shared directory, and *local_directory* is the name of the local directory used for the mount point. You can use *showmount -e server* to see the mounts on a specified server.

To mount the NFS share */gzipfiles* from server *Styx* to local mount point */StyxFiles*, do the following commands:

```
# showmount -e Styx
Export list for Styx:
/home (everyone)
# showmount -e Styx
Export list for Styx:
/home EngleLinux
/gzipfiles EngleLinux
# mount Styx:/gzipfiles /StyxFiles
# cd /StyxFiles
# ls
Disk1 glibc-devel-2.3.2-5.i386.rpm
Disk2 lnx_920_disk1.cpio.gz
Disk3 lnx_920_disk2.cpio.gz
ftape lnx_920_disk3.cpio.gz
glibc-2.3.3-2-5.i386.rpm openldap-2.1.21
glibc-2.3.3-2-5.i686.rpm openldap-stable-20030531.tar
glibc-common-2.3.2-5.i386.rpm
# cp glibc-2.3.2-5.i386.rpm /root
# umount /StyxFiles
#
```

After the share is mounted, commands to change the directory, list files, and copy files can be used. The umount command unmounts the share.

## SNMP

Simple Network Management Protocol (SNMP) was designed to integrate management of different types of networks. There are two main elements in the SNMP architecture, the agent and the manager. Similar to most network programs, SNMP is a client/server application with the agent working as the server and the manager as the client.

The agent is a program running on each monitored host of the network. The agent stores monitored information into a management information base (MIB) until it is requested by a client.

The manager is the front-end client software. Typically, SNMP client software is GUI enabled. The manager’s role is to contact the different agents running on remote hosts and request information about current configurations and performance.

SNMP can also be used to configure a system from a remote client. The SNMP agent will accept input values and pass them on to other programs.

The SNMP server program is *snmpd*. The client programs from the command line are *snmpget*, *snmpup*, *snmpstatus*, and *snmpwalk*. You can also use an SNMP GUI client.

## NIS

Network Information Service (NIS) is a protocol that is designed to simplify user authentication. If you have multiple Linux systems, NIS can be used to authenticate to one NIS server instead of creating duplicate accounts on all the servers. There are several variations of NIS, such as NIS+ and NYS. The original NIS was once called Yellow Pages (YP) and so the service files names start with yp.
