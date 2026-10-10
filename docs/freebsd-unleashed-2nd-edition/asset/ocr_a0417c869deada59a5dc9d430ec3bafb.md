# NOTE

> Note that the access denied message appears immediately after the server receives the username—it doesn't prompt for a password. This prevents passwords from being sent over the wire, providing an extra security precaution in the case where you've disabled a user out of concern regarding an eavesdropper sniffing for passwords.

You can also add any group name to `/etc/ftpusers`; simply precede the name with an "at" (@) symbol (for example, @users). Any user who is part of any group listed in the file will be disallowed access.

# The `/etc/shells` File

After seeing whether the user is listed in `/etc/ftpusers`, ftpd checks the shell associated with the user and sees whether it's listed in `/etc/shells`. If it isn't, the user will get the same kind of access denied message as with `/etc/ftpusers`. You can leverage this functionality to prevent a user from logging in with a terminal program or with FTP, by changing the user's shell to `/sbin/nologin` (which you saw in Chapter 11—it simply prints out an account not available message and exits, and it's not listed in `/etc/shells` or something similarly constructed.

# The `/var/run/nologin` File

To turn off FTP logins completely, without modifying `/etc/inetd.conf` or any other such config files, you can simply place a file called `nologin` in `/var/run`. If `ftpd` sees this file, it will respond to all connections as follows:

```
```
# ftp localhost
Connected to localhost.somewhere.com.
530 System not available.
ftp>
```
```

You can use `touch /var/run/nologin` to create the file (with zero length) and disable FTP logins. Remove the file (`rm /var/run/nologin`) to re-enable the FTP server.

# Allowing Anonymous FTP Access

By default, anonymous FTP is not enabled; the easiest way to enable it, if you choose to do so, is through `sysinstall`. Run `/stand/sysinstall`; then enter the Configure and Networking sections. Scroll to the Anon FTP option and press the spacebar to enter the Anonymous FTP Configuration screen, shown in Figure 26.2.

The default options are generally appropriate for a typical FreeBSD system. The UID, Group, and Comment fields control how the new ftp user will be created. This user's home directory is set to `/var/ftp`, which is how anonymous FTP works—the `ftp` login is treated as a regular user that behaves as if it's listed in `/etc/ftphroot`, so anybody logging in as `ftp` (or its alias, `anonymous`) will be put into a chroot jail at `/var/ftp`.