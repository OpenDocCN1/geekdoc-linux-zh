+   7. Finally, it's worth mentioning that RPM packages can be installed directly from the Internet. We can use HTTP or FTP addresses to install directly. If you wanted to install say the vnc-server directly from the Red Hat web site, you'd type this:

```
```bash
# rpm -ivh
http://ftp.redhat.com/pub/redhat/linux/9/en/os/i386/RedHat/RPMS/vnc-server-3.3.3r2-47.i386.rpm
```
```

# How It Works

We've used the RPM command for installation, much as we did for querying earlier, this time, however, the options are slightly different. Each of the three install commands used the option - ivh here, which translates as follows:

+   - i indicates that we intend to perform an installation
+   - v indicates that we want RPM to display "additional information". For example to display package file names while performing multiple package installation with one rpm command.
+   - h indicates that we want RPM to print hash (#) marks during the installation process to show the progress of the installation.

# Removing Packages

Removing unwanted packages from your system is an important task. RPM makes package removal easy. It keeps record of all the files installed by each package, so we can easily clean our system by removing all the files associated with an unwanted package.

# Try It Out Removing Packages using the RPM

OK, so we probably don't actually need the vnc-server, lynx, and balsa packages on our system. So, here's how we go about removing them:

+   1. First, type the following to remove the vnc-server package:

```
```bash
# rpm -e vnc-server
```
```