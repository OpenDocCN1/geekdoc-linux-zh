Tripwire started off as a free product that was later turned commercial. However, a free version is still available and maintained. It is available at http://www.tripwire.org.

# Bastille Linux

Bastille Linux is a hardening script for Red Hat. It runs through a series of questions, and based on the information given the administrator has the choice of taking the scripts advice or not. Bastille provides no services itself; it only locks down the security of an existing system.

If you are new to security it is a good idea to go through the Bastille script not only to secure your system, but also teach you about security. The script provides excellent information on what it does, and why it does the things it does.

Bastille Linux is available from http://www.bastille-linux.org.

# Key Point Summary

Security is a very important piece of the system administrator's job. If done properly it can take up a large portion of your time, but it is time well spent. The information provided in this chapter is a very good starting point on the road of knowledge.

+   - TCP wrappers uses the `hosts.allow` and `hosts.deny` files to provide security for TCP services.
+   - `tcpdchk` is used to check the syntax of your `hosts.allow` and `hosts.deny` files.
+   - `tcpdmatch` is used to provide theoretical connections to your system to test your `hosts.allow` and `hosts.deny`.
+   - SUID executables and scripts can be very large security risks.
+   - The validity of RPM packages can be checked with PGP and GPG.
+   - Any package or file can be checked with the `md5sum` tool.
+   - The SGID bit can be used to create directories that let users share files.
+   - If a directory has the SGID bit set, new files belong to the group of the directory and not the user.
+   - The Berkeley r commands are very insecure.
+   - The `.rhosts` file is used to give remote users access to a local account.
+   - The `hosts.equiv` file is used to allow or deny access to the r commands from other hosts.
+   - `rlogin` is used to remotely log in to another system.