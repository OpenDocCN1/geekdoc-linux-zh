Active FTP operates on both server port 20 (for data transfers) and port 21 (for control commands) and involves a reply connection from the server to the client, which may be blocked by a firewall behind which the client is sitting. Passive FTP involves only server port 21 and is unlikely to cause problems with a standard firewall configuration that allows established connections. For more firewall configuration, see Chapter 24.

Note that all options in the configuration file are specified in the form:

```
option=value
```

and that there should be no white space before or after the = sign.

For a standard anonymous Internet FTP download server, you have done all need to do.

# Setting Up User FTP with vsftpd

In this section we assume that you want users with accounts on the system to be able to access their home directories by FTP.

Please be aware that this could constitute a security risk if the system is available to the Internet, you should think carefully about whether you want to do it.

One common reason why you might want to do this is to set up a system to receive incoming files; you can set up "artificial" users to own each home directory for type of incoming file. You can then give the relevant usernames and passwords to each person needing the ability to upload to these directories.

You need to make further changes in the configuration file /etc/vsftpd.conf. You need to enable these lines:

```
local_enable=YES
root_local_user=YES
```

The second of these lines means that users will not be able to change directories out of their home directories. Users will be locked in a "chroot jail.".

If you now log in as a user, you will see something similar to Listing 23-1.

# Listing 23-1: Logging in to FTP Server as a User

```
user@client:/home/user > ftp bible
Connected to bible.
220 (vsFtpd 2.0.2)
```