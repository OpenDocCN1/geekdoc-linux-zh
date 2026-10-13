
## CERTIFICATION OBJECTIVE 15.02

### Samba as a Client

You can configure two types of clients through Samba. One connects to directories shared from Microsoft Windows servers or Samba servers on Linux/Unix. The second connects to shared printers from one of the same two types of servers. The Samba client commands are available from the samba-client RPM. With those commands, you should be able to find browse lists and mount shared directories locally.

### Command Line Tools

To browse shared directories from a Linux computer, you should know how to use the smbclient command. This can test connectivity to any SMB host on a Windows- or Samba-based Linux/Unix computer. Assuming it's allowed by a firewall, you can use smbclient to check the shared directories and printers from other systems on at least the local network. For example, the following smbclient command checks shared directories and printers:

```
# smbclient -L server1.example.com -U donna
```

I've specified two arguments with the smbclient command: the -L specifies the name of the Samba server, and the -U specifies a username on the remote computer. When the command reaches the Samba server, you're prompted for the appropriate password.

Shares will appear; for example, the following output reveals shares named public and donna, as well as a printer named OfficePrinter on a remote system named Maui.

Domain=[MYGROUP] OS=[Unix] Server=[Samba 3.5.4-68.el6_0.2]

| Sharename | Type | Comment |
|---|---|---|
| public | Disk | Public Stuff |
| IPC$ | IPC | IPC Service (Samba Server Version 3.5.4-68.el6_0.2) |
| OfficePrinter@Maui | Printer | in the office |
| donna | Disk | Home Directories |

Domain=[MYGROUP] OS=[Unix] Server=[Samba 3.5.4-68.el6_0.2]

From the displayed output, there's a share available named public. You can also use the smbclient command to make a client connection similar to an FTP connection with the following command:

```
$ smbclient //server1.example.com/public -U michael
```

Of course, most administrators would prefer to mount that share on a local directory. That's where options to the mount command are helpful.

### Mount Options

Shares can be mounted by the root administrative user. The standard is with the mount.cifs command, functionally equivalent to the mount -t cifs command. For example, the following command mounts the share named public on the local /home/shared directory:

```
# mount.cifs //server1.example.com/public /home/shared -o username=donna
```

This command prompts for user donna's password on the remote server. That password should be part of the Samba user authentication database on the server1.example.com system, normally different from the standard Linux authentication database. Of course, that user donna could also mount her remote home directory in a similar fashion, with a command like the following:

```
# mount.cifs //server1.example.com/donna /home/donna/remote -o username=donna
```

While there is no longer a umount.cifs command for shared Samba directories, you can still use the umount command to unmount such directories.

### Automated Samba Mounts

As it certainly takes a few extra steps to set up a shared directory, it would be useful to automate the process. The standard method is through the /etc/fstab configuration file discussed in Chapter 6. To review the essential elements of that chapter, you could set up the public share in /etc/fstab by adding the following line (which is wrapped):

```
//server1.example.com/public /home/shared cifs rw,username=donna,password=pass, 0 0
```

But that can be a risk, as the /etc/fstab file is world-readable. To that end, you can configure a dedicated credentials file with the username and password, as follows:

```
//server/pub /share cifs rw,credentials=/etc/smbdonna 0 0
```

As suggested in Chapter 6, you can then set up the username and password in the /etc/smbdonna file:

```
username=donna
password=donnapassword
```

While the contents of that file must still exist in clear text, you can configure the /etc/smbdonna file as readable only by the root administrative user. It's also possible to configure the automounter with similar information. But as the automounter is a RHCSA skill, you'll have to refer to Chapter 6 for that information.

## CERTIFICATION OBJECTIVE 15.03

### Samba Troubleshooting

Samba is complex. With a complex service, simple mistakes may be difficult to diagnose. Fortunately, Samba includes excellent tools for troubleshooting. The basic testparm command tests syntax. Log files can tell you more. Of course, unless appropriate changes are made in local firewalls, Samba might not even be accessible from remote systems.

### Samba Problem Identification

Samba is a forgiving service. It includes synonyms for a number of parameters. Some of the parameters are misspelled; for example, writable is a synonym for writeable. But beyond those parameters, the testparm command can help identify problems. For example, Figure 15-7 illustrates a number of problems. Unrecognized parameters are highlighted with the "unknown parameter" message.

Some parameters don't work with each other. For example, the following message in the testparm output highlights two incompatible directives:

```
ERROR: both 'wins support = true' and 'wins server = <server list>' cannot be set in the smb.conf file. nmbd will abort with this setting.
```

Sometimes, troubleshooting commands come in the output to other commands. For example, problems often appear in the output to various commands. Sometimes the output is straightforward, such as the following output to a specific mount.cifs command, associated with an incorrect share name. It also suggests that the case of share names is less important on networks associated with Microsoft operating systems.

```
Retrying with upper case share name
```

Sometimes, messages may appear to be more straightforward, such as

```
mount error(13): Permission denied
```

But that message could refer to an incorrect password, or a user that has not been configured in the Samba database.

Sometimes problems may seem more annoying. For example, if you mount a remote home directory and no files show up in that directory, it could mean that the SELinux samba_enable_home_dirs boolean has not been enabled. If you mount a remote directory other than a user home directory, it could mean that the directory and associated files are not properly labeled with the samba_share_t file type.

### FIGURE 15-7
Review the Samba Configuration with testparm

```
[root@mini ~]# testparm /etc/samba/smb.conf
Load smb config files from /etc/samba/smb.conf
rlimit_max: rlimit_max (1024) below minimum Windows limit (16384)
Unknown parameter encountered: "security"
Ignoring unknown parameter "security"
Unknown parameter encountered: "passdb backend"
Ignoring unknown parameter "passdb backend"
Processing section "[homes]"
Processing section "[printers]"
Processing section "[public]"
Unknown parameter encountered: "write list"
Ignoring unknown parameter "write list"
Loaded services file OK.
ERROR: both 'wins support = true' and 'wins server = <server list>' cannot be set in the smb.conf file. smbd will abort with this setting.
Server role: ROLE_STANDALONE
Press enter to see a dump of your service definitions
```

### Local Log File Checks

Problems associated with Samba may appear in the /var/log/messages file, or they may appear in different files in the /var/log/samba directory. First, syntax errors revealed in the output to the testparm command may also appear in the /var/log/messages file. As the Samba services are started, errors in the configuration file are problems worth reporting in the standard system log file.

In addition, when an attempted mount of a shared Samba directory fails, associated messages also appear in the /var/log/messages file. Sometimes the messages are straightforward such as cifs_mount failed, or NT_STATUS_LOGON_FAILURE.

Most Samba log files are located in the /var/log/samba directory. As shown in Figure 15-8, the log files are classified by the host or IP address of the client that connects to the server. In general, fewer messages mean success. For example, a connection to a localhost system, useful for troubleshooting, may include the following message in the log.__ffff_127.0.0.1 log file:

```
__ffff_127.0.0.1 (::ffff:127.0.0.1) connect to service michael
initially as user michael (uid=1000, gid=1000) (pid 23800)
```

The information therein suggests the use of both IPv4 and IPv6 addresses. The connected user is identified by UID, GID, and PID numbers. If an unauthorized user connects, these numbers can help identify a problem user and/or a compromised account, along with an associated process ID number.

Most of the other files in this directory relate to various services as named; for example, the log.smbd, log.nmbd, and log.winbindd files collect messages associated with the daemons named in each respective log file.

### Enable Remote Access

Network services aren't much good unless access is allowed from other systems. As with other RHEL 6 systems, each server has a firewall. The ports associated with Samba are closed by default. It's easy to set up access for a Samba server and a Samba client through the Firewall Configuration tool. All you'd need to do is to specify that the server or client is a trusted service.

As discussed in previous chapters, it's possible to limit remote access to certain IP addresses on a firewall. The -s switch in an iptables-based firewall configures source addresses. For example, the following rule would limit communication to the NetBIOS name service to any system but that on IP address 192.168.122.150:

```
-A INPUT -m state --state NEW -m udp -p udp -s !192.168.122.150 --dport 137 -j
ACCEPT
```

Remember, such specialized iptables-command rules can only be configured as a "Custom Rule" as described in Chapter 10.
