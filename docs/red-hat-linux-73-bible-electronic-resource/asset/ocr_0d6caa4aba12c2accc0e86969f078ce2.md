# ## Using the Very Secure FTP Server (vsFTPd)

You can use the Very Secure FTPD Server instead of WU-FTPD as your FTP server. Although it hasn’t been around as long as WU-FTPD, vsFTPd is becoming the FTP server of choice for FTP sites that need to support hundreds or thousands of concurrent downloads. It was also designed to secure your systems against most common attacks.

The vsFTPd server was added to Red Hat Linux 7.3. In fact, Red Hat even uses vsFTPd on its own FTP servers (ftp.redhat.com). Other organizations in the Linux/GNU world have also made the switch to vsFTPd, including Debian Linux (ftp.debian.org), the GNU Project (ftp.gnu.org), and RPM Find (ftp://rpmfind.net).

Besides security and scalability, vsFTPd was designed for simplicity. Therefore, fewer options exist for configuring vsFTPd than you find in WU-FTPD, so you are expected to rely on standard Linux file and directory permissions to provide refined access to your server. Getting started with vsFTPd, or using it to replace WU-FTPD, is fairly straightforward.

# ## Quick-starting vsFTPd

By enabling the vsFTPd service, you can almost immediately have an FTP service running with the default values (set in the `/etc/vsftpd.conf` file). The following is a quick procedure for getting your vsFTPd server up and running.

> NOTE: If you have been using the WU-FTP server on your computer and you are switching to vsFTPd, you need to turn off WU-FTP. To do that, change `disable=no` to `disable=yes` in the `/etc/xinetd.d/wu-ftpd` file. Then, once you have completed the following procedure, vsFTPd will take control of the default FTP configuration, allowing access to the `/var/ftp` directory and listening on the default FTP port. Because the two packages have some different default settings, however, you may want to do additional tuning to get vsFTPd to perform as you would like it to.

+   1. To use the vsFTPd server, you need to make sure that the software packages vsftpd and anontftp are installed.

+   2. Enable the vsFTPd server by changing the `disable=yes` line in the `/etc/xinetd.d/vsftpd` file. Open the file as root user, using any text editor, and change the line to the following:

```
```
    disable       =       no
```
```

+   3. Restart the xinetd server as follows:

```
```
# /etc/init.d/xinetd restart
```
```

+   4. Try to log in to the FTP server as anonymous (using any e-mail address as the password):

```
```
$ ftp localhost
Connected to yourhost
220 ready, dude (vsFTPd 1.0.1: beat me, break me)
```
```