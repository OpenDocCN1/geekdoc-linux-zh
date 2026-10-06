# 468 Linux Administration: A Beginner's Guide

Of course, we'll need to start the service. Once you've learned how to start the daemon, the rest of this section will walk you through testing the FTP server by connecting to it using an FTP client.
Let's start a sample anonymous FTP session. But first we'll start the FTP service.

> TIP The ftp daemon is automatically started right after installing the software in Ubuntu via apt-get. Check to make sure it's already running before trying to start it again. You can examine the output of the command ps -aux | grep vsfptd to check this.

+   1. Start the FTP service:
`root@server -]# service vsfptd`

On Linux distributions systemd, you can alternatively start the vsfptd daemon using the systemctl command:
`root@fedora-server -]# systemctl start vsfptd.service`

> TIP If the service command is not available on your Linux distribution, you might be able to restart the service by directly executing its run control script. For example, you may be able to restart vsfptd by issuing the following command:
`root@server -]# /etc/init.d/vsfptd start`

+   2. Launch the command-line FTP client program, and connect to the local FTP server as an anonymous user:
`root@server -]# ftp localhost`nConnected to localhost (127.0.0.1).
220 (vsFTPd 3.**)
Name (localhost:root):

+   3. Enter the name of the anonymous user when prompted—that is, type ftp:
Name (localhost:root): ftp
331 Please specify the password.

> TIP Most FTP servers that allow anonymous logins often permit the implicit use of the username "anonymous." Instead of supplying ftp as the username to use to connect anonymously to our sample Fedora FTP server, we can instead use the popular username anonymous.