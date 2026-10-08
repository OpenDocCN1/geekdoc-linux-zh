
# 470 LINUX IN A HETEROGENEOUS NETWORK

Intensive use, however, may turn this situation into the opposite. If one computer is used by many users as a file and print server, reasonable interactive work on that computer is no longer possible. Since, for example, Windows for Workgroups has not been designed as a server operating system, problems will now occur with the maintenance of this computer, which is probably now standing in a locked room.

The SMB protocol is used by many products; besides the Windows family, the most widely used ones are LAN manager (by Microsoft and IBM) and Pathworks (by DEC). The SMB specification is now being enhanced to the Common Internet Filesystem (CIFS), which should address some of the SMB and NFS problems.

## 19.2.1 LINUX as an SMB client

If a workgroup or a domain already exists in your network, you can use LINUX to participate in this group. The smbfs file system required for this is implemented in the kernel. In addition, you will need the smbount program, which mounts the exported volume into the LINUX file system.

To set up the smbfs, you will need root privileges. Also, this file system is not portable to other systems. In exchange, the shares are integrated into the normal LINUX directory tree. For the user, it does not matter at all whether the files are stored locally, on an NFS server, or on an SMB server.

The samba package includes an SMB client (smclient) which is handled in a similar way to the ftp program. This program can be used without special privileges; help is obtained by the help command inside the program. On other UNIX systems, this is a simple way to access SMB shares. In contrast to LINUX's npcfs this does not provide seamless access.

The syntax of the shares name is exactly as under Windows: first two backslashes, the computer name, and separated by another backslash, the share name. Note, however, that you must quote the special characters of the shell (backslash) (Listing 19.8).

```
(Linux) >> smclient -L pea
(Linux) >> smclient \\pea\jochen
```

Listing 19.8 The use of smclient.

With the option -l, you will get a list of the shares available from this server (disks and printers). You can obtain access to these shares if you specify their names as in the second example.

# LINUX AS AN SMB CLIENT AND SERVER 471

This method is available for practically every UNIX system. Under Linux, however, an SMB share can be directly inserted into the directory tree. For this purpose, the smbfs must be compiled into the kernel or loaded as a module, and the smbount program must be installed. An example for mounting of a share is shown in Listing 19.9.

```
(Linux):~ /usr/sbin/smbount //pea/jochen mount -C
```

Listing 19.9 Mounting of an SMB share.

In the smbount program, normal slashes instead of backslashes are used as separators inside the share names. Thus, the user does not need to bother about quotes or other special characters. The share name is expected as the first parameter, the mount point as the second. If the smbount program is installed setuid-root, every user can use this program.

The program smbount has a number of options which are used to influence the behaviour of the program. If you have problems with logging in, you should try the option -C which prevents the password from being converted into upper case before it is transmitted to the server.

| Additional Information and Sources |
|---|---|
| ftp server: | ftp.gwdg.de |
| ftp path: | /pub/linux/misc/smbfs |
| File name: | smbount-1.3.tar.z |
| Size: | about 32 K |

## 19.2.2 SMB servers over LINUX

With samba, a powerful SMB server is available for UNIX systems. The program can also be compiled and installed under LINUX. Modern distributions include preconfigured versions of this package; however, it may be sensible to install it.

Distributions exported from the USA normally do not include packages that use cryptographic methods. Thus, the samba package is usually compiled without password encryption (this is currently changing). With the Service Pack 3 for Windows NT 4.0, however, transmission of encrypted passwords becomes the default under NT, which leads to the consequence that these computers can no longer log in to a samba server.

Weigh the advantages and disadvantages of using the libdes library yourself. The advantages are:

- NT computers can log in to a samba server without reconfiguration of the registry.
- No passwords are transmitted that could be read with a password sniffer.
- Windows NT can then also browse via a samba server.

There are also well-known disadvantages; the following list should help you to make your decision:

- A 'password equivalent' is stored on the hard disk of the server.
- The UNIX server and samba no longer use the same passwords from the file /etc/passwd or /etc/shadow.

Do you use services such as telnet, ftp or pop3? Then the passwords are transmitted via the network in clear text anyway, and you do not gain much.

If you have Windows NT 4.0 computers in your network, you should use encrypted passwords. This is the default since Service Pack 3. You can, however, also reconfigure the Windows NT clients by inserting the entry EnablePlainTextPassword with a value of 1 (as REG_DWORD) into the HKEY_LOCAL_MACHINE tree of the registry under \system\currentset\services\rdr\parameters. This setting must be carried out on every client.

You can use encrypted passwords if the SMB server has been compiled with the libdes library. This is often not the case with distributions exported from the USA. In this situation you need to activate the entries for the libdes library in the samba Makefile and also install it. Furthermore, you must include the encrypted passwords = yes in the file smb.conf, section [global]. More information on the subject of encryption can be found in the file ENCRYPTION.TXT in the samba package.

When you use encrypted passwords for samba, you need to create a samba user in addition to the normal LINUX user. The simplest way to do so is the command smbpasswd -a user (as user root). Each user can change his password with smbpasswd alone.

For the compilation of samba, you must activate the settings for LINUX in the file ./source/Makefile and adapt the paths to be used. Subsequently, you can compile samba with make and install it with make.

# LINUX AS AN SMB CLIENT AND SERVER 473

install. You must include the lines shown in Listing 19.10 in the file /etc/services if they are not yet included.

| netbios-ns | 137/udp |
| netbios-ssn | 139/tcp |

Listing 19.10 New entries in /etc/services.

You can start the daemons smbd and nmbd either directly (for example in rc.local) or by means of the inetd server. for this, you must include the two lines shown in Listing 19.11, adapted to the paths specified in the Makefile, in the file /etc/inetd.conf and restart the inetd server. This is certainly sensible for testing, since a new samba process is started for every new connection which needs the configuration.

| netbios-ssn stream tcp nowait root /usr/local/bin/smbd smbd |
| netbios-ns dgram udp wait root /usr/local/bin/nmbd nmbd |

Listing 19.11 New entries in /etc/inetd.conf.

Many distributions include this package in a preconfigured form. For reasons of speed, the daemons are usually not started by the inetd, but in the start-up scripts.

In practice, you will probably start with exporting the home directories of your users. For this, you will need the entry shown in Listing 19.12 in the file smb.conf. You can carry out a first test with the smclient program locally under UNIX. All possible settings are extensively documented in the man page for smb.conf.

```
[Chomes]
comment = home directories
browseable = no
read only = no
create mode = 0750
```

Listing 19.12 Exporting the home directories.
