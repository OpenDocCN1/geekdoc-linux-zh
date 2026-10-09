Change the directive to read as follows:

```
local_enable=NO
```

Then restart the vsftpd service using the **Server Configuration** dialog, or typing the following at the command line:

```
# service vsftpd restart
```

Now, if you try using an FTP client to gain FTP access via a system user account, you’ll be refused:

```
$ ftp 192.168.0.99
Connected to 192.168.0.99 (192.168.0.99) .
220 (vsFTpd 1.1.3) .
Name (192.168.0.99:none): eziodm
530 This FTP server is anonymous only.
Login failed.
```

# ### Blocking FTP Access for User Accounts

Alternatively, we can deny FTP access to individual users (rather than to all users). We control this using the file /etc/vsftpd.ftppers file, which contains the list of users that are *not* allowed FTP access to the server.

To try this, first change the local_enable directive back from NO to YES, in /etc/vsftpd/vsftpd.conf, to enable FTP access via system accounts:

```
# Uncomment this to allow local users to log in.
local_enable=YES
```

Then, open the /etc/vsftpd.ftppers file (using root privileges), add an account name at the bottom, and save the file. There’s no need to restart the vsftpd service; changes to the /etc/vsftpd.ftppers file take effect immediately.

Then use the account to try to gain FTP access via an FTP client:

```
# ftp 192.168.0.99
Connected to 192.168.0.99 (192.168.0.99) .
220 (vsFTpd 1.1.3) .
Name (192.168.0.99:none): eziodm
331 Please specify the password.
Password:
530 Login incorrect.
Login failed.
```