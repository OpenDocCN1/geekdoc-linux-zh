# Setting default file permissions for FTP

If many of your users FTP their files on the server, you can control the default umask setting for the FTP server such that one user's file is not accessible by another. For example, if you want to set permissions such that only the user and her group can read a file uploaded on a Web server via FTP, you can modify the in.ftpd line in the /etc/inetd.conf file. This line by default looks as follows:

```
ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd -l -a
```

To set a default umask for all files uploaded via FTP, you need to add a -u argument with the appropriate umask value. For example, to set 640 (rw-r-----) permission for each file uploaded, you can set the umask to 026. So, change the preceding line as follows:

```
ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd -l -a -u026
```

Restart the inetd server (killall -HUP inetd) and FTP a file via a user account to see whether the permissions are set as expected.

This could be very handy for systems that act as Web servers for many different clients. If you do not want one client to see another client's files, you can use this option along with a special ownership setting. For example, suppose that you keep all of your Web client files in the /www partition or directory, where each client site has a directory of its own (for example, /www/myclient1, /www/myclient2, and so on). You probably already gave each client an FTP account to upload files in these directories. To stop a client from seeing another client's files, use umask, as described, with the FTP server and also reset the ownership of each client site as follows:

```
chown -R client.Web server user /www/client dir
```

For example, if you run your Web server as httpd and have a client user called myclient, then the preceding command will look like this:

```
chown -R myclient.httpd /www/myclient
```