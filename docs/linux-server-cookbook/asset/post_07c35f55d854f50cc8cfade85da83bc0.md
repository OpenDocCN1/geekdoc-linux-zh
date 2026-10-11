
The FTP protocol separates the control (login and commands) and the data (transfer files) connections. The protocol uses port 21/tcp for the control communication and port 20/tcp for the data transmission. It is possible to protect the protocol using SSL/TLS, which is commonly named FTPS, and uses ports 989/tcp and 990/tcp.

The FTP protocol can work in two different modes:

- Active mode: The client connects to port 21/tcp and indicates which local port is used for the data transfer. The server sends the data to the port specified. This can be an issue when a firewall is involved because that communication usually is not allowed.
- Passive mode: This mode is used to avoid firewall issues. The client sends a signal called PASV, and the server answers with an IP and a port to start the data communication.

Figure 10.14 shows the differences between the two modes:

## Active Mode

FTP client opens a random port (>1023) and then sends the port number on which it is listening to the FTP server.

![](img/863afa537de4eed7deb11978bfbfa90e_320_0.png)

## Passive Mode

FTP client opens a random port (>1023) and then sends the port number on which it is listening to the FTP server requesting a passive connection.

![](img/863afa537de4eed7deb11978bfbfa90e_320_1.png)

> Figure 10.14: Active and passive mode for FTP. Source: Cisco

The most popular software to offer an FTP service is called **vsftpd**. The name stands for **very secure FTP daemon**. The main configuration file is /etc/vsftpd.conf, and the default options in Ubuntu servers are shown as follows:

```
listen=NO
listen_ipv6=YES
anonymous_enable=NO
local_enable=YES
dirmessage_enable=YES
use_localtime=YES
xferlog_enable=YES
connect_from_port_20=YES
secure_chroot_dir=/var/run/vsftpd/empty
pam_service_name=vsftpd
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
ssl_enable=NO
```

The option `listen` indicates if the service will be executed in standalone mode (YES) or using `systemd` (NO). The option `local_enable` indicates if the local users can log in, and the option `anonymous_enable` specifies if guest users can connect to the service.

One of the features of the FTP servers is that users, when connecting to the service, can access the files in their home directory. They can download, create directories, or upload files to the server.

The most popular client in a Linux system to access the FTP service is the software `lftp`. This client allows performing the normal tasks for FTP but also allows access to other protocols such as **Hypertext Transfer Protocol (HTTP)**, **Hypertext Transfer Protocol Secure (HTTPS)**, **File transferred over Shell protocol (FISH)**, and **Secure File Transfer Protocol (SFTP)**. It also supports the BitTorrent protocol. The argument required is to specify the destination; if the destination is an IP address, it will, by default, use FTP as a protocol. For other protocols, it is required to specify the method, such as `ftps://` or `http://`. The options for authentication are `-u` to specify the username and optionally the password separated by a comma (,). Figure 10.15 shows an example:

```
[root@rhel ~]# lftp 192.168.122.43 -u agonzalez,Start123
lftp agonzalez@192.168.122.43:~> ls
-rw-rw-r--    1 1000    1000           9 Sep 11 17:08 notes.txt
lftp agonzalez@192.168.122.43:~>
```

![](img/863afa537de4eed7deb11978bfbfa90e_321_0.png)

The command `lftp`, as observed, uses an interactive mode to operate with the server. Some of the popular options are described in Table 10.4:

| Command | Description |
|:---:|:---:|
| `ls [args]` | List the content of the current directory in the server, or it is possible to specify the directory to list. |
| `cd` | Change the directory in the server. |
| `lcd` | Change the directory in the local client. |
| `get` | Download a file from the *FTP server*. |
| `mget` | Download multiple files. |
| `put` | Upload a file to the *FTP server*. |
| `mput` | Upload multiple files. |
| `mkdir` | Create a directory in the server. |
| `rmdir` | Remove a directory from the server. |

*Table 10.4: LFTP commands*

The command **lftp** accepts the option **-e** to execute a command or combination of commands, which can include the command **quit** to exit the interactive mode. Refer to Figure 10.16 for an example:

```
[root@rhel ~]# lftp 192.168.122.43 -u agonzalez,Start123 -e "get notes.txt;quit"
9 bytes transferred
[root@rhel ~]# ls -l notes.txt
-rw-r--r--. 1 root root 9 Sep 11 18:08 notes.txt
```

*Figure 10.16: Example of the usage of the command lftp*

It is possible to use option **-d** to **debug** the communication to the FTP server; the following block shows the output communication to a **vsftpd** server:

```
---- Resolving host address...
---- IPv6 is not supported or configured
---- 1 address found: 192.168.122.43
---- Connecting to 192.168.122.43 (192.168.122.43) port 21
---- 220 (vsFTPD 3.0.5)
---> FEAT
<--- 211-Features:
<--- EPRT
<--- EPSV
<--- MDTM
<--- PASV
<--- REST STREAM
<--- SIZE
<--- TVFS
<--- 211 End
---> AUTH TLS
<---  530 Please login with USER and PASS.
---> USER agonzalez
<---  331 Please specify the password.
---> PASS start123
<---  230 Login successful.
---> PWD
<---  257 "/home/agonzalez" is the current directory
---> PASV
<---  227 Entering Passive Mode (192,168,122,43,35,39).
----  Connecting data socket to (192.168.122.43) port 8999
----  Data connection established
---> LIST
<---  150 Here comes the directory listing.
----  Got EOF on data connection
----  Closing data socket
-rw-rw-r--   1 1000   1000          9 Sep 11 17:08 notes.txt
<---  226 Directory send OK.
---> QUIT
<---  221 Goodbye.
----  Closing control socket
```

## TFTP Introduction

This simple protocol, **Trivial File Transfer Protocol (TFTP)**, is usually used to provide files to a remote node when the system is booting. This protocol is used to perform automatic installation in **baremetal** nodes mainly. It does not have a login or access control mechanism, and its normal use is in a private network. The protocol used is **User Datagram Protocol (UDP)**, and the port is 69.

This protocol is usually used with the **Preboot Execution Environment (PXE)**, which allows systems to boot from the network and load boot media. This boot media can be stored in a TFTP server. Modern systems can use iPXE, which allows using an HTTP server instead of a TFTP service to store the boot media. Figure 10.17 illustrates a PXE/TFTP overview:

![](img/863afa537de4eed7deb11978bfbfa90e_324_0.png)

> Figure 10.17: PXE/TFTP overview. Source: Wikipedia

## Conclusion

Sharing files with users and other devices in the network is required in most enterprises. Users and applications can store data in central shared locations, such as personal files or backups. The central server is responsible for protecting the files from unwanted access and can be used to be included in periodic backups.

This chapter covered the most important protocols, NFS and SMB, including the installation of the service and the usage of the clients. The protocol FTP is covered as well, showing the installation of the server and the use of the client.

## Key facts

- NFS protocol is the most popular one for Linux systems.
- SMB protocol is mainly used to interoperate with Windows systems.
- FTP was a popular protocol to share directories with users.
- TFTP is a protocol to store files for automatic installations using PXE.

## Questions

1. What is the default file to configure the NFS server?
   a. /etc/nfs.conf
   b. /etc/nfsd.conf
   c. /etc/nfs/nfsd.conf
2. What file includes the exported directories configuration?
   a. /etc/exportfs
   b. /etc/exports
   c. /etc/share.conf
3. What is the main configuration file for the Samba service?
   a. samba.conf
   b. smbd.conf
   c. smb.conf
4. What command is used to operate as the client to the SMB protocol?
   a. smbtree
   b. smbclient
   c. smbget
5. What ports are used on the FTP server?
   a. 19/tcp
   b. 20/tcp
   c. 21/tcp

## Answers

1. a
2. b
3. c
4. b
