
# Installing Sendmail

It is the worst-case scenario. We had hoped everything would be easy sailing. Now we need to track all the packages needed by Sendmail 8.11, install those packages, and then attempt to install sendmail-8.11.0-1.i386.rpm all over again. This bit of unpleasantness is a blessing in disguise. If we installed sendmail-8.11.0-1.i386.rpm from source and did not know that openssl and libssl are required, the features of Sendmail would not work as advertised. It could take a long time tracking down the problem. RPM makes sure that we know the problem right from the start. We could force RPM to install sendmail-8.11.0-1.i386.rpm without the dependencies by adding the --nodeps argument to rpm command. But the best thing to do is track down and install the required packages.

A search of rpmfind informs us that we need three different RPM packages to fix the six dependencies: openssl-0.9.sa-1.i386.rpm, lib5io-1999-1.i386.rpm, and cyrus-sas1-1.5.11-2.i386.rpm. The first two packages, openssl and libssl, are pretty obvious RPM lists them as the first two dependencies needed by sendmail-8.11.0-1.i386.rpm. An examination of the list of files provided by each package shows that they provide every dependency except libsas1.so. A search for libsas1-so.7 tells us that it is found in cyrus-sas1-1.5.11-2.i386.rpm. We download the three packages and install them as shown in Listing 3.8.

# Listing 3.8 Fixing Dependency Problems for Sendmail 8.11

```
[root]# - rpm openssl-0.9.sa-1.i386.rpm
error: file /usr/man/man/passwd from install of openssl-0.9.sa-1
conflicts with file from package passwd-0.58-1
[root]# - rpm --replacefiles openssl-0.9.sa-1.i386.rpm
[root]# - rpm lib5io-1999-1.i386.rpm
[root]# - rpm -u sendmail-8.11.0-1.i386.rpm
[root]# - rpm q sendmail
sendmail-8.11.0-1
```

Even this installation did not go perfectly. The openssl-0.9.sa-1.i386.rpm package creates a new passwd page. The problem is, it doesn't own the old page. That page was on the system by the passwd-0.58-1.i386.rpm package. RPM wontt let a new package change a file that belongs to another unless you tell it to. In this case, we want the new passwd documentation so we use the --replacefiles argument with the rpm command to replace the old passwd documentation with the new documentation.

All of the other installations run smoothly. Once the dependencies are resolved, sendmail-8.11.0-1.i386.rpm installs without complaint. A quick query to RPM shows that the new package is in place.

Next, restart Sendmail to make sure the newly installed daemon is running, and run a quick test to make sure new daemon is alive and serving the SMTP port. Listing 3.9 shows these two commands.

# 3.9 Restarting and Testing Sendmail

```
[root]# /etc/rc/init.d/sendmail restart
Shutting down sendmail:
Starting sendmail:
[root]# telnet localhost 25
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'
220. wen.foobirds.org SMTP Sendmail 8.11.0/8.11.0;
Sun, 13 Aug 2000 18:00:03 -0400
quit
221 2.0.0.wen.foobirds.org closing connection
Connection closed by foreign host.
```

As Listing 3.9 shows, Sendmail is installed and running. Despite all the problems encountered in this installation, Sendmail is upgraded and running after fewer than a dozen commands. Linux package managers have done much to simplify upgrades.

> NOTE I have never had a problem with dependencies upgrading Sendmail before version 8.11. This just turned out to be a lucky break. Normally, things go so smoothly when preparing examples for Linux books that problems have to be described without actual examples. This time we were lucky enough to have a real problem. You might never see dependency problems when installing Sendmail yourself, but it is good to know how they are resolved.

# X Tools for Installing Sendmail

In the previous section, we used the command-line version of rpm. It is easy to explain, and it runs on most Linux systems—even those that don't have X Windows running. But if you are using X Windows, there are some graphical tools for running the Red Hat Package Manager. Several systems use a tool named glint. Systems with the KDE desktop environment use a tool named kpackage, and systems with the GNOME desktop environment use a tool called gnorpm. Figure 3.6 shows gnorpm running on a Red Hat 6 system.

# Figure 3.6 gnorpm running on a Red Hat 6 system

![Figure 3.6 gnorpm running on a Red Hat 6 system](img/gnorpm_running_on_a_red_hat_6_system.png)

Understanding gnorpm is easy. The options are:

- -U (upgrade)
- -q (query)
- -v (verify)
- -e (uninstall)

Even if you are using the GUI, these are easier than the command line. Figure 3.6 shows what happens when you use gnorpm. The possible values are:

- S: indicates that the file has the wrong size.
- M: indicates that the file has wrong permissions or type.
- S: indicates that the file has an incorrect MD5 checksum.
- D: indicates that the file is located on the wrong device.
- L: indicates that the file is improperly a symbolic link.
- U: indicates that the file has the wrong user ID (UID) assigned.
- G: indicates that the file has the wrong group ID (GID) assigned.
- T: indicates that the file has the wrong creation time.
- C: indicates that the file is a configuration file that is expected to change.

# Cleaning Up After Mail

In the previous example, two files have the wrong checksum and the creation date, and they are the wrong size. These are all things you would expect these are not the original files. Two files were installed over the original files. All of the other files associated with the Sendmail RPM check out. But for this reason

Even if your Linux system comes with its own version of Sendmail, obtaining the latest Sendmail source code distribution provides useful documentation, tools, and sample configuration files. Additionally, there are times when you need a security fix or update and the latest version of Sendmail has not yet been posted as an RPM or other binary distribution.

To compile the Sendmail program, download the compressed tar file as a binary file and then uncompress and extract it with the tar command, as shown in Listing 3.10.

# Downloading the Sendmail Source Code

```
[craig]$ ftp ftp.sendmail.org
Connected to ftp.sendmail.org.
```
