**vsftpd** This server aims to excel at security, stability, and speed. In doing so, its developers have chosen to eschew some of the more advanced features of servers such as ProFTPD and WU-FTPD. If you don't need those features, this trade-off may be more than acceptable. You can learn more from its Web site, `http://vsftpd.beasts.org`. It's available with most Linux distributions.

**WU-FTPD** The Washington University FTP Daemon (WU-FTPD) is an old standard in the Linux world. Unfortunately, it has collected more than its fair share of security problems and isn't the speediest FTP server available. For these reasons, it ships with fewer Linux distributions today than in years past. Its main Web site is `http://www.wu-ftpd.org`.

**PureFTPD** This server, headquartered at `http://www.pureftpd.org`, is another FTP server that emphasizes security.

**oftpd** This server is unusual because it's designed to function *only* as an anonymous FTP server; it doesn't support logins using ordinary user accounts. This feature can be appealing if you only want to run an anonymous server, but it makes this server unsuitable for many other purposes. It's available from `http://www.time-travellers.org/oftpd/`.

![](bbox=[0.15, 0.46, 0.25, 0.53])

> This list of FTP servers is far from complete. The oftpd Web page describes the primary developer's search for a name for the server. He wanted a name of the form xftpd, where x was a single letter. Starting with a ftpd, he found that oftpd was the first name that wasn't already in use!

Because FTP can potentially provide users with substantial access to the system—the ability to read or write any file, within limits imposed by Linux file ownership and permissions—FTP servers are unusually sensitive from a security point of view. As a result, the Web pages for many of the servers in the preceding list emphasize their developers' attention to security.

For a small FTP site, chances are any of the servers in the preceding list will work well, with the exception of **oftpd** if you want authenticated user logins rather than anonymous access. **ProFTPD** and **vsftpd** are both popular choices on modern Linux systems.

# # FTP Server Configuration

Details of FTP server configuration vary greatly from one server to another, so I don't describe most features in detail. Broadly speaking, though, you should pay attention to several features:

+   - **Configuration files** Most FTP servers have configuration files, such as `/etc/proftpd/proftpd.conf` for ProFTPD or `/etc/vsftpd/vsftpd.conf` for vsftpd. You should consult your server's documentation to learn the details of the configuration file format and the options that the server supports.
+   - **Launch method** Many FTP servers can run either stand-alone (via a SysV or local startup script) or from a super server. Some servers work better when launched in one way or the other, and distributions sometimes provide startup scripts for one method but not the other. Chapter 4, “Managing System Services,” describes both methods of launching servers, so you should consult it and check to see what startup scripts are provided with your package.