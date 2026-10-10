
# Note

> Note that the access denied message appears immediately after the server receives the username—it doesn't prompt for a password. This prevents passwords from being sent over the wire, providing an extra security precaution in the case where you've disabled a user out of concern regarding an eavesdropper sniffing for passwords.

You can also add any group name to `/etc/ftpusers`; simply precede the name with an "at" (@) symbol (for example, @users). Any user who is part of any group listed in the file will be disallowed access.

### The `/etc/shells` File

After seeing whether the user is listed in `/etc/ftpusers`, ftpd checks the shell associated with the user and sees whether it's listed in `/etc/shells`. If it isn't, the user will get the same kind of access denied message as with `/etc/ftpusers`. You can leverage this functionality to prevent a user from logging in with a terminal program or with FTP, by changing the user's shell to `/sbin/nologin` (which you saw in Chapter 11—it simply prints out an account not available message and exits, and it's not listed in `/etc/shells`) or something similarly constructed.

### The `/var/run/nologin` File

To turn off FTP logins completely, without modifying `/etc/inetd.conf` or any other such config files, you can simply place a file called `nologin` in `/var/run`. If `ftpd` sees this file, it will respond to all connections as follows:

```
$ ftp localhost
Connected to localhost.somewhere.com.
530 System not available.
ftp>
```

You can use `touch /var/run/nologin` to create the file (with zero length) and disable FTP logins. Remove the file (`rm /var/run/nologin`) to re-enable the FTP server.

### Allowing Anonymous FTP Access

By default, anonymous FTP is not enabled; the easiest way to enable it, if you choose to do so, is through `sysinstall`. Run `/stand/sysinstall`; then enter the Configure and Networking sections. Scroll to the Anon FTP option and press the spacebar to enter the Anonymous FTP Configuration screen, shown in Figure 26.2.

The default options are generally appropriate for a typical FreeBSD system. The UID, Group, and Comment fields control how the new ftp user will be created. This user's home directory is set to `/var/ftp`, which is how anonymous FTP works—the `ftp` login is treated as a regular user that behaves as if it's listed in `/etc/ftphroot`, so anybody logging in as `ftp` (or its alias, `anonymous`) will be put into a chroot jail at `/var/ftp`.

![](img/48eec858cce7dfb89da36a4d40b7daf3_651_0.png)

FIGURE 26.2 Anonymous FTP configuration options.

You can change any of the fields to suit your system (for instance, if you already have a user with a UID of 14, or if you want a name for the upload directory that’s different from incoming). When you select OK at the bottom of the screen, the ftp user will be created, as will the /var/ftp tree with its necessary subdirectories.

Note that /stand/sysinstall doesn’t provide the capability to disable anonymous FTP after it has been enabled, but you can do this a number of ways. The following methods are ranked in descending order of preferability:

- Add the ftp user to /etc/ftpusers (probably the easiest and cleanest method).
- Change the permissions on the /var/ftp tree so that its contents can’t be read by regular users—0700 will work.
- Remove the /var/ftp tree.
- Remove the ftp user.

Similarly, you can disable the upload (incoming) directory by simply removing it, or else by changing its permissions to 755 (the default directory permissions, in which only the owner—root—can write into it). Re-enable it (or any other directory to which you want anonymous users to be able to upload files) by changing its permissions to 1777—for instance, chmod 1777 /var/ftp/incoming.

### Virtual Hosting

If you have multiple IP addresses bound to your machine, you can map different FTP server behaviors to each one. This virtual hosting mechanism is controlled with the /etc/ftphosts file, which does not exist in the default FreeBSD system (you need to create it).

Each virtual host is defined on its own line, with fields specifying alternate config files for each host separated by whitespace. Table 26.2 describes the various fields, their meanings, and the default values (the ones that the server uses without an /etc/ftphosts file present).

TABLE 26.2 Virtual Hosting Table Fields in /etc/ftphosts

| Field | Description | Default |
| :--- | :--- | :--- |
| Hostname | The hostname or IP address of the virtual host. Note that FTP has no equivalent of the Host: header of HTTP/1.1, so FTP virtual hosts are defined purely on the IP address of your machine where the client is connected. If you use a hostname in this field, ftpd uses the IP address to which it resolves. Bear this in mind when adding virtual hosts. | N/A |
| User | The user whose home directory is used for anonymous FTP access in this virtual host. Anonymous users are jailed (via chroot) into this directory, so equivalents of /var/ftp/etc and /var/ftp/bin should be present. | ftp |
| Statfile | The log file that tracks all FTP transfers for the virtual host. | /var/log/ftpd |
| Welcome | The welcome message displayed upon initial connection to the FTP server. | /etc/ftpdwelcome |
| MOTD | The second welcome message, presented after a successful user login. | /etc/ftpmotd |

A few sample virtual hosts in /etc/ftphosts follow. If a field is left blank or has a hyphen (-), the default value is used:

```
64.41.131.106  frank  /var/log/ftpd-frank  /home/frank/hi  /home/frank/hi2
ftp2.me.com    ftp2   -                  /etc/ftpd2welcome -
64.41.131.107  ftp3   /var/log/ftpd-3    -                  -
```

## Using Alternate FTP Servers

Many alternate FTP server packages exist; the two most popular are Washington University's WU-FTPD and the highly configurable ProFTPD. Both of these packages provide features that are not available in the default FTP server, including extremely flexible configurability and extra security measures.

### WU-FTPD

Originally developed at Washington University to host the WArchive (once one of the most popular file-sharing and distribution locations on the Internet), WU-FTPD has gained in popularity to become the most frequently used FTP server in the world. It's the default FTP daemon in Linux and many commercial Unix brands. WU-FTPD's configuration differs from FreeBSD's default ftpd in a few subtle ways, and it has a few features that the default ftpd does not, such as a configuration-checking tool, on-the-fly compression and archiving, and limitations on access and transfers by time and date. You might choose to install WU-FTPD to maintain compatibility with an existing non-FreeBSD system.

WU-FTPD is available as a package or in the ports (/usr/ports/ftp/wu-ftpd). After installing it, you can switch to it from the FreeBSD ftpd by commenting out the ftp line in /etc/inetd.conf and replacing it with one that points to the new ftpd:

```
#ftp	stream tcp	nowait	root	/usr/libexec/ftpd	ftpd -1
ftp	stream tcp	nowait	root	/usr/local/libexec/ftpd	ftpd -1
```

> WU-FTPD is installed as /usr/local/libexec/ftpd, and its man page can't be accessed directly with man ftpd—you'll get the page for the default system ftpd. To see the correct page, use the -M option to use an alternate man path, like so:
> 
> man -M /usr/local/man ftpd

More information on WU-FTPD is available at http://www.wu-ftpd.org.

### ProFTPD

ProFTPD was developed with the intention of creating an FTP server that could be managed with configuration files that resembled those of Apache. The server's config file has hierarchcal configuration blocks like those in httpd.conf (as you saw in Chapter 25) and directives that are similar in style to those of Apache. The result is a server that has very Apache-like, access-limiting features as well as a high level of configurability, especially for administrators familiar at all with Apache. It's available as a package or from the ports (/usr/ports/ftp/proftpd).

One difference between ProFTPD and its relatives is that it can be run in standalone mode, like Apache, rather than from inetd. If you do run it from inetd, replace the default ftp line with one pointing to /usr/local/libexec/proftpd:

```
#ftp	stream tcp	nowait	root	/usr/libexec/ftpd	ftpd -1
ftp	stream tcp	nowait	root	/usr/local/libexec/proftpd	proftpd
```

The ProFTPD home page, www.proftpd.org, has much more information on ProFTPD's capabilities and configuration directives.
