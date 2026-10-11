| lcd | Change the directory in the local client. |
| --- | --- |
| get | Download a file from the *FTP server*. |
| mget | Download multiple files. |
| put | Upload a file to the *FTP server*. |
| mput | Upload multiple files. |
| mkdir | Create a directory in the server. |
| rmdir | Remove a directory from the server. |

*Table 10.4: LFTP commands*

The command **lftp** accepts the option **-e** to execute a command or combination of the commands, which can include the command **quit** to exit the interactive mode. Refer to *figure 10.16* for an example:

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
```