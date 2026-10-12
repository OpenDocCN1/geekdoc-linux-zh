> **NOTE:** Previous to Red Hat Linux 7, the location of the FTP home directory was `/home/ftp`. Because administrators often shared `/home` directories across a group of computers so users could have access to their files from different computers, it was not useful to share the FTP home directory in this way. The FTP home directory is now `/var/ftp`. The home directory for your Web server (www directory) has also been moved to `/var`.

# ## Creating FTP users

The different types of users who can use the FTP services from your server include the anonymous user name, any of the real users who have been added to your computer (in `/etc/passwd`), and any special guest accounts that you set up. The following sections describe each of these types of users and how to set them up.

# ### The anonymous FTP user

Because most visitors to your FTP site from the Internet will not have an individual login account to your computer, the anonymous user name is used on public FTP sites. With the anonymous user name, anyone who can reach the FTP site from the network can log in to the server and have minimal permission for its use. Typically, minimal means that an anonymous user can only copy files from (and not write files to) the FTP server and that only selected directories are even visible to the anonymous user.

Here is an example of a login session from an anonymous user:

```
```
$ ftp maple
Connected to maple.
220 maple FTP server (Version wu-2.6.1-18) Mon Nov 26 09:21:53
EDT 2000) ready.
Name (pine:mike): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password: ********
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
ftp> bye
221-You have transferred 0 bytes in 0 files.
221-Total traffic for this session was 313 bytes in 0 transfers.
221-Thank you for using the FTP service on maple.trees.
221 Goodbye.
```
```

After connecting to the server, I typed anonymous at the login prompt. The server says that anonymous is okay and to enter my e-mail address as the password. (The password doesn’t appear; I’ve used asterisks here to represent the password.) The server accepted my password as valid. If it had been invalid, I could have continued, but the server would have warned me to type a valid e-mail address next time. Because this is an illustration, I just ended the session by typing `bye` and I was logged off.