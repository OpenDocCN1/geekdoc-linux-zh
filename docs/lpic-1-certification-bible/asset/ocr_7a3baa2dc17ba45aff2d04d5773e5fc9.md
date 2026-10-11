# ## COPS

COPS, Computer Oracle and Password System, is a set of programs that monitors the security situation of a system. It monitors the following:

+   - File, directory, and device permissions/modes.
+   - Poor passwords.
+   - Content, format, and security of password and group files.
+   - The programs and files run in the `rc` directories and `crontab` files.
+   - Existence of SUID root files, their writability, and whether or not they are shell scripts.
+   - A CRC check against important binaries or key files to report any changes therein.
+   - Writability of users home directories and startup files (`.profile`, `.cshrc`, and so on).
+   - Anonymous FTP setup.
+   - Unrestricted `tftp`, `decode` alias in `sendmail`, SUID `uudecode` problems, hidden shells inside `inetd.conf`, `rex` running in `inetd.conf`.
+   - Miscellaneous root checks — current directory in the search path, a `"+"` in `/etc/host`, `equiv`, unrestricted NFS mounts, root in `/etc/ftppers` and so on.
+   - The dates of CERT advisories versus key files. This checks the dates that various bugs and security holes were reported by CERT against the actual date on the file in question. A positive result doesn't always mean that a bug was found, but it is a good indication that you should look at the advisory and file for further clues. A negative result, obviously, does not mean that your software has no holes, merely that it has been modified in some way (perhaps merely touched) since the advisory was sent out.
+   - The Kuang expert system. This takes a set of rules and tries to determine if your system can be compromised.

Generally COPS is run via `cron` every night to perform its checks. This way you are alerted right away of any changes that could be a problem.

COPS is available from `http://www.cerias.purdue.edu`.

# ## Tripwire

Tripwire is a tool that monitors the permissions and checksums of system files so that you can easily detect if they have been tampered with. When set up, Tripwire creates a database with the checksum information of all the configured files. It is best to keep this database and Tripwire's configuration files on a secure system on read-only media.