The ftpshut command supplied with standard wu-ftpd does not support shutdown of virtual sites, because it writes the shutdown message file in only a single location specified by the shutdown keyword in the /etc/ftpaccess file. Also, when the time comes to restart the server, you need to manually remove the shutdown message file. To overcome these nuisances, you might want to get the replacement ftpshut/ftprestart utilities from the following Web site: http://www.landfield.com/wu-ftpd/restart. You have to compile and build these utilities yourself.

# Creating a complete virtual FTP service

This method requires that you patch the wu-ftpd source and compile it on your own:

+   1. You can download the source code for wu-ftpd from ftp://ftp.academ.com/pub/wu-ftpd/private/. You also need the patch file from ftp://ftp.meme.com/pub/software/wu-ftpd-2.4.2/.
+   2. Read the README file that comes with the patch tar-ball and apply the patch to the wu-ftpd source you downloaded earlier. Compile and install the patched wu-ftpd per the instructions provided in the wu-ftpd source package. Install the new FTP server to the default location, /usr/sbin/in.ftpd.
+   3. The newly patched wu-ftpd program (in.ftpd) now accepts an argument for the -a option. Normally, -a tells the server that you want it to read the /etc/ftpaccess file. Now, the patched version allows it to specify a different path for the ftpaccess file. So, this allows the new server to look at different ftpaccess configuration files that will be needed to create virtual FTP sites.
+   4. Modify the /etc/inetd.conf file so that the FTP service has a line such as the following:
+      This invokes the FTP server via the TCP wrapper (tcpd).
+   5. Modify the /etc/hosts.allow file such that you have lines similar to the ones that follow for each FTP server (that is, the primary server and all the virtual FTP servers):

```
ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd
```

```
# For the primary server
ftp@206.171.50.50 : ALL : twist exec \
```