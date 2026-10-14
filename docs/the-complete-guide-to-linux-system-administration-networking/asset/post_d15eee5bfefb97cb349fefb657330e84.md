
use an IP address, either for a single host or for a network or part of a network. The exports man page lists all of the possible permutations.

An /etc/exports file can be as simple as this:

```
/projects
```

This /etc/exports file allows anyone who can reach your host via NFS to mount the /projects directory, as no host name or access options are specified. Well, that's almost true. When you use an NFS client to access a remote file system, the NFS server must decide what user to treat you as, because you never "log in" or provide a password when you use the NFS client (as you saw in Chapter 10's discussion of the mount command). The default action is that the mount command sends your user ID and group ID on the client, then the NFS server uses the same user ID and group ID on the server system. Your file permissions match those of the corresponding user and group. This is designed for a situation where a single user has accounts on multiple systems, with the same user ID and group ID on each one. (This is a lot like the rlogin, rsh, and rcp commands you learned about in Chapter 7, "Using Network Clients.")

This arrangement is not always easy to achieve, nor is it always appropriate. For this reason, you normally include options in /etc/exports to map incoming client user and group IDs to user and group IDs on the NFS server.

NFS uses a security concept called squashing to prevent a user from gaining access to a user account on the NFS server simply because the user has the same ID on the NFS client. The most important use of this is squashing the root account: you shouldn't have root access on the NFS server just because you have root access on an NFS client! Squashing of the root account is done automatically unless you use the no_root_squash option. One method of squashing incoming client user IDs is to define an anonymous user account and tell NFS to map all incoming users to that account. Thus, all NFS clients have access only to areas that you have specifically granted to this "anonymous" user. Reviewing a few examples should make the uses of this system apparent:

```
/
    scout (rw,no_root_squash)
```

This line shows a very trusted host, scout, for which squashing is not used (remember, root_squash is the default action). The root user can thus have root access to the / directory on the NFS server. This type of entry would be used for a trusted network in which a single system administrator wanted to have complete access to multiple hosts' file systems via NFS.

The next example assumes that everyone on the myplace.net domain has a user account with a matching user ID on the NFS server. They all are permitted to access the /projects directory, reading and writing according to the file permissions within /projects on the NFS server.

```
/projects    *.myplace.net(rw)
```

## Accessing Remote NFS File Systems

When you need to access a remote NFS file system, as shown previously, you can either include all needed options on the command line, or create an entry for the NFS server in the /etc/fstab. About 20 special options are available when you mount a file system on an NFS server. Some of the most useful are listed here:

- - rsize=8192,wsize=8192—Used together, these options alter the default buffer size for NFS transfers. Using these options avoids the speed problems sometimes associated with NFS on Linux.
- - ro and rw—You can mount a file system as read-only (ro) or read-write (rw).
- - hard or soft—You can hard mount an NFS file system, which means your programs wait—without limit—for the NFS server to respond. If the remote server goes down and then comes up again a while later, your program continues without a hitch. Alternatively, you can soft mount an NFS file system, which means that NFS waits for a while and then gives up. The documentation recommends not using the soft option unless the NFS server you are working with is quite unreliable.
- - noauto—This option causes the NFS file system not to be mounted automatically at system start-up.

This example line from /etc/fstab shows how NFS options appear in that file:

```
rome:/home/public  /mnt/rome
nfs  rsize=8192,wsize=8192,rw,noauto 0 0
```

## Setting up a Samba Server

The Samba suite is a collection of programs that implement file and print sharing using the SMB and CIFS protocols, which are the standards used by Microsoft Windows operating systems. Samba includes two server daemons: nmbd, which implements the NetBIOS name service, and smbd, which handles file and print services. Both of these daemons must be running. On Red Hat Linux and Fedora, you can manage these daemons together as the smb service; on some Linux distributions, the service is called Samba. After you have set up the configuration file and created appropriate user accounts as outlined in this section, you can start the Samba service on Red Hat Linux or Fedora using this command:

```
# service smb start
```

Once you have configured Samba, you can use the chkconfig command to make it start automatically whenever you start Linux.

Samba configuration files are typically stored in /etc/samba, though the location may vary in different Linux distributions. The main configuration file is smb.conf. A sample or default smb.conf file is provided. It contains many comments, but not enough to understand all the

configuration options. Still, you should review that file and add your own settings before running a Samba server. A very basic smb.conf file is shown here:

```
[global]
workgroup = MYPLACE
netbios name = sundance
server string = Samba on Linux posing as Windows 2000
hosts allow = 192.168.100.
printcap name = /etc/printcap
load printers = yes
printing = lprng
log file = /var/log/samba.log
max log size = 0
security = user
encrypt passwords = yes
smb passwd file = /etc/samba/smbpasswd
socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
dns proxy = no

[homes]
comment = User home directories
browseable = no
writable = yes

[printers]
comment = Linux printers
path = /var/spool/samba
browseable = no
guest ok = no
printable = yes
```

The smb.conf file is divided into sections. The [global] section defines the overall operation of the server. Other sections define how the server handles shared resources: either the printers or specific file system shares (directories that you want to share). The [homes] and [printers] sections are standard names that refer to the home directories of each user who logs in and the Linux printers, respectively. You can create other sections to define other shares.

## Creating Samba Users

Although the sample configuration file settings above are sufficient to start a basic Samba server, the recommended user-based security model requires that each user must log in with a valid user name and password before using a share on the Samba server. It's common to allow everyone with a Linux user account to also log in via Samba. Several utilities included with the Samba suite make this easy to implement. Assuming that you have created all your Linux user accounts, the following command creates a Samba password file for all your Linux users:

```
# cat /etc/passwd | mksmbpasswd.sh > /etc/samba/smbpasswd
```

No passwords are transferred in this process; you must enter a password for each user (twice) using the smbpasswd command. For example, this command lets you set the Samba password for user nwells in the smbpasswd file:

```
# smbpasswd nwells
```

User nwells can then use the password entered to access a share on the Samba server from a Windows system. (The Samba server simply appears as part of the Windows network—it can take some time after activating the Samba server before the Windows systems displays it.)

If you add Linux users to your system after setting up Samba, you can add them to your smbpasswd file using the smbpasswd command with the -a option. This command has no effect on the Linux users on your system. For example, you could add a new Samba user and define a password for that user (when prompted) using this command:

```
# smbpasswd -a abutler
```

A more comprehensive user management utility for Samba is the pdbedit utility. To add a Samba user with this utility, you can use this format:

```
# pdbedit -a -u abutler
```

## Using SWAT to Configure SMB

The example smb.conf configuration file described previously contains only a fraction of the hundreds of options supported by Samba. Exploring them all can be a challenge, especially if you are new to Windows networking. A graphical tool that can help you both configure Samba and learn about its options is SWAT, a browser-based graphical interface that sets up the smb.conf file, restarts the Samba servers, and provides some status information on how the server is being utilized.

SWAT runs as a network service managed by the superserver, which is discussed at the end of this section. After enabling SWAT in your superserver configuration (either in /etc/inetd.conf or /etc/xinetd.d/swat), you can use your browser from any system to reach SWAT and manage your Samba server. However, SWAT transfers are not encrypted, so unless you are using SWAT to manage Samba on the same machine, you risk exposing your root password to someone snooping around on your network. (You can configure ssh to protect you from this danger and permit safe remote management.)

To access SWAT once you have the network capabilities configured, start your Web browser and enter the URL http://localhost:901/ (assuming you are configuring SWAT on your own machine.) You are prompted for a user name and password. You must enter the user name root and the root password for your host.

## Creating a Proxy Server with Squid

A proxy server is similar in function to the network address translation and IP masquerading features discussed previously in this section. A proxy lets one server make a request for another server. This is typically done either to improve the efficiency or the security of the
