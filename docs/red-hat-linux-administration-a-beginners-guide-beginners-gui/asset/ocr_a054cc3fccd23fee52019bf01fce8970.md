```
Enter passphrase for .ssh/id_dsa:
Identity added: .ssh/id_dsa (.ssh/id_dsa)
[michael@pinkymichael]$ ssh brain
Last login: Sun Oct 27 21:43:19 2002 from localhost.localdomain
[michael@brain michael]$ 
```

# Applications Related to SSH

The OpenSSH package actually comes with some additional programs that use the same encryption technology, such as Secure Copy Protocol (SCP) and Secure FTP.

The **scp** command is meant as a secure replacement for the **rcp** command, which allows you to do remote copies from one host to another. The most significant problem with the **rcp** command is that users tend to arrange their remote-access settings to allow far too much access into your system. To help mitigate this, instruct users to use the **scp** command instead. The format of **scp** is identical to **rcp**, so users shouldn’t have problems with this transition. For example, if I’m logged in to shells as user **michael** and I want to copy the **amy.jpg** file from **brain**, I would type:

```
[michael@shell5 michael]$ scp michael@brain:amy.jpg /home/michael/images/
```

For SSH servers running protocol version 2, Secure FTP also allows you to copy files between hosts without transferring files or passwords in cleartext, only this time it mimics an FTP client, which may be more familiar for some users.

```
[michael@shell5 michael]$ sftp brain
Connecting to localhost...
sftp> cd pix
sftp> ls
drwxr-xr-x   14 michael  michael    3312 Sep  9 18:47 .
drwxr-xr-x    19 michael  users      712 Aug  5 23:34 ..
-rw-r--r--    1 michael  michael  14873 Jan  7  2002 safetux.jpg
-rw-r--r--    1 michael  michael   74378 Jan  4  2002 amy.jpg
-rw-r--r--    1 michael  michael   47558 May 21 17:05 wrongmuppet.jpg
sftp> get amy.jpg
Fetching /home/michael/pix/amy.jpg to amy.jpg
sftp> exit
```

# Module Summary

The Secure Shell tool is a superior replacement to Telnet for remote logins. Adopting the OpenSSH package will put you in the company of many other sites that are disabling Telnet