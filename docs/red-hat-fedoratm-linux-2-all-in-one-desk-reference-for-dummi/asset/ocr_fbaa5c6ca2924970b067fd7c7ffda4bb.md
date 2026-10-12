Unfortunately, the convenience of anonymous FTP comes at a price. If you don't configure the anonymous FTP service properly, intruders and pranksters may gain access to your system. Some intruders may simply use your system's disk as a temporary holding place for various files; others may fill your disk with junk files, effectively making your system inoperable (this sort of attack is called a Denial of Service attack). At the other extreme, an intruder may gain user-level (or, worse, root-level) access to your system and do much more damage. The default anonymous FTP setup in Fedora Core employs the necessary security precautions.

# ## Trying Anonymous FTP

To see anonymous FTP in action, try accessing your system by using an FTP client. For example, in the following sample session, I accessed the FTP server from a terminal window on the same system (my input appears in boldface):

```
```
ftp localhost
Connected to localhost (127.0.0.1).
220 (vsFTPD 1.2.1)
Name (localhost:naba): anonymous
331 Please specify the password.
Password: < - I can type anything as password
230 Login successful. Have fun.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -l
227 Entering Passive Mode (127,0,0,1,169,190)
150 Here comes the directory listing.
drwxr-xr-x   2     0         0     4096 Jun 06 04:36 pub
226 Directory send OK.
ftp> bye
221 Goodbye.
```
```

When you successfully log in for anonymous FTP, you access the home directory of the user named ftp (the default directory is /var/ftp). Place the publicly accessible files — the ones you want to enable others to download from your system — in the /var/ftp/pub directory.

# ### Key features of anonymous FTP

The key features of an anonymous FTP setup are as follows:

+   * A user named ftp whose home directory is /var/ftp. The user does not have a shell assigned. Here is what you get when you search for ftp in the /etc/passwd file:

```
grep ftp /etc/passwd
```