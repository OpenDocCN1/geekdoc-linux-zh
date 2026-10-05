# TRANSFERRING FILES USING THE SECURE FILE TRANSFER PROGRAM

To interactively upload or download files from a SSH server, use the Secure File Transfer Program, sftp. A session with the sftp command uses the secure authentication mechanism and encrypted data transfer to and from the SSH server.

Using just the scp command, the sftp command uses [user]@host to identify the target system and user. If you do not specify a user, the command will attempt to log in using your local user name as the remote user name. You will be presented with an sftp> prompt.

```
[user@host ~]$ sftp remoteuser@remotehost
remoteuser@remotehost's password: password
Connected to remotehost.
sftp>
```

The interactive sftp session accepts various commands that work the same way on the remote file system as they do in the local file system, such as ls, cd, mkdir, rdir, and pwd. The put command uploads a file to the remote system. The get command downloads a file from the remote system. The exit command exits the sftp session.

To upload the /etc/hosts from the local system to the newly created directory /home/remoteuser/hostbackup on remotost. The sftp session always assumes that the put command is followed by a file on the local file system and starts in the connecting user's home directory; in this case, /home/remoteuser:

```
sftp mkdir hostbackup
sftp> cd hostbackup
sftp> put /etc/hosts
Uploading /etc/hosts to /home/remoteuser/hostbackup/hosts
/etc/hosts                               100%  227      0.8KB/s    00:00
sftp>
```

To download /etc/yum.conf from the remote host to the current directory on the local system, execute the command get /etc/yum.conf and exit the sftp session with the exit command.

```
sftp> get /etc/yum.conf
Fetching /etc/yum.conf to yum.conf
/etc/yum.conf                               100%  813      0.8KB/s    00:00
sftp> exit
[user@host ~]$
```

+   REFERENCES
scp(l) and sftp(1) man pages