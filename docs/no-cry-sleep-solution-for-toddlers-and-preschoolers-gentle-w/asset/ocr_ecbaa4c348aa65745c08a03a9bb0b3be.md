from a user’s current directory to the user aleina’s birthday directory, located on the rabbit.mytrek.com host:

```
scp party aleina@rabbit.mytrek.com:/birthday/party
```

Of particular interest is the -r option (recursive) option, which enables you to copy whole directories. See the scp Man page for a complete list of options. In the next example, the user copies the entire reports directory to the user justin’s projects directory:

```
scp -r reports justin@rabbit.mytrek.com:/projects
```

In the next example, the user george copies the mydoc1 file from the user cecelia’s home directory:

```
[george@turtle george]$ scp cecelia@turtle.mytrek.com:mydoc1
cecelia@turtle.mytrek.com's password:
mydoc1      0% |                    |   0 --:--:--
ETA
mydoc1    100% |********************************|  17 00:00
[george@turtle george]$
```

From a Windows system, you can also use scp clients such as winscp, which will interact with Linux scp-enabled systems.

# sftp and sftp-server

With sftp, you can transfer FTP files secured by encryption. sftp uses the same commands as ftp (see Chapter 21). This client, which works only with ssh version 2, operates much like ftp, with many of the same commands. Use sftp instead of ftp to invoke the sftp client.

```
sftp ftp.redhat.com
```

To use the sftp client to connect to an FTP server, that server needs to be operating the sftp-server application. The ssh server invokes sftp-server to provide encrypted FTP transmissions to those using the sftp client. The sftp server and client use the SSH File Transfer Protocol (SFTP) to perform FTP operations securely.

# Port Forwarding (Tunneling)

If, for some reason, you can connect to a secure host only by going through an insecure host, ssh provides a feature called port forwarding. With port forwarding, you can secure the insecure segment of your connection. This involves simply specifying the port at which the insecure host is to connect to the secure one. This sets up a direct connection between the local host and the remote host, through the intermediary insecure host. Encrypted data is passed through directly. This process is referred to as tunneling, creating a secure tunnel of encrypted data through connected servers.