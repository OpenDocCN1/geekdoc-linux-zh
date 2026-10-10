# Part III  Administration

If this is the first time you have ever logged in to that system using the ssh command, it will ask you to confirm that you really want to connect. Type **yes** and press [Enter] when it asks this:

```
```
The authenticity of host 'ratbert.glaci.com (199.170.177.18)'
can't be established.
RSA key fingerprint is xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx.
Are you sure you want to continue connecting (yes/no)? **yes**
```
```

> > **CAUTION** If you see an auth request a second time, this could possibly be a man-in-the-middle attack.

If you don’t specify a username when you start the ssh connection, the SSH daemon assumes you want to use the username you are logged in as from the client. If you want to log in as a different username (e.g., chris), you could type the following:

```
```
$ ssh chris@ratbert.glaci.com
```
```

or

```
```
$ ssh -l chris ratbert.glaci.com
```
```

Once you are logged in, a shell prompt appears, and you can begin using the remote system as you would from a local shell.

The scp command is similar to the rcp command for copying files to and from Linux systems. Here is an example of using the scp command to copy a file called memo from the home directory of the user named sally to the /tmp directory on a computer called flashg:

```
```
$ scp /home/sally/memo flashg:/tmp
sally@flashg’s password: ********
memo        100% 153   0:00
```
```

Enter the password for your username (if a password is requested). If the password is accepted, the remote system indicates that the file has been copied successfully.

Similarly, the sftp command starts an interactive FTP session with an FTP server that supports SSH connections. Many security-conscious people prefer sftp to other ftp clients because it provides a secure connection between you and the remote host. Here’s an example:

```
```
$ sftp ftp.handsonhistory.com
Connecting to ftp.handsonhistory.com...
sally@ftp.handsonhistory.com’s password: ********
sftp>
```
```

At this point, you can begin an interactive FTP session. You can use **get** and **put** commands on files as you would using any FTP client, but with the comfort of knowing that you are working on a secure connection.