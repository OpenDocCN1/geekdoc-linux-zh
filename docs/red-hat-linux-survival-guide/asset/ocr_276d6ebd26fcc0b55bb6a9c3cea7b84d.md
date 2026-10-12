# Controlling the DNS server

The named distribution comes with a nifty program called ndc that provides a simple command-line interface for controlling the name server. Using this tool you can start and stop the name server; reload DNS configuration files, and also view statistics.

# Starting the name server

Your name server should start automatically at boot. If it does not start automatically, you need to take the following steps:

+   1. Log into your name server system as root and change directory to `/etc/rc.d/init.d`. Make sure that you have a script called named in this directory. If you are missing this script, you should reinstall the BIND distribution RPM from your Red Hat CD-ROM.
+   2. After you have confirmed that you have the `/etc/rc.d/init.d/named` script, change to your default system run level's (see `/etc/inittab`) rc directory. For most systems the default run level is 3; if yours is also the same, change directory to `/etc/rc.d/rc3.d/`.
+   3. Make a symbolic link called SXXnamed that points to the `/etc/rc.d/init.d/named` script. Replace XX in SXXnamed with a high number such as 55 or 85 to ensure that the system does not try to start the name server before network interfaces are set up properly. For example, to make a symbolic link called S55named to point to the named script, you can run the following command:
+   ```
+   ln -s /etc/rc.d/init.d/named S55named
+   ```
+   After you have created this link, your system will start the name server every time you boot your system. If, however, you prefer to run the name server manually, you can use the ndc program as follows:
+   ```
+   ndc start
+   ```