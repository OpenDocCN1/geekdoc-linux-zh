The `httpd.conf` file in the `/etc/httpd/conf` directory includes a commented sample virtual host stanza. You can use it as a template for both virtual hosts. You should also use the SELinux contexts of the `/var/www/html` directory as a template as well for the `/web` subdirectory.

+   4. If you are successful, users `elizabeth` and `fred`, and no others, will have access to the `cubs` subdirectory of the main directory. Both users will have access only from systems on the local network. In the Apache `httpd.conf` file, there is a template for single home directories. It can be modified to accommodate a group of users.

+   5. The CGI application should be accessible from the following URL:
+   `http://test1.example.com/cgi-bin/good.pl`. When you navigate to that URL, the browser should tell you "Good Job!"

+   6. Given the presumed change to the SELinux `ftp_home_dir` boolean, you need to pay attention to the `vsftpd.conf` configuration file in the `/etc/vsftpd` directory. And in that directory, you’ll see that logins by regular users are enabled by default.

+   7. The default `named.conf` configuration file is itself sufficient for a caching-only DNS server. To that file, you’ll need to add a **forwarders** directive, with the IP address of the remote DNS server.

+   8. In principle, it should not matter whether you configure Postfix or sendmail as the SMTP server. You should be able to check access with commands like `telnet server1.example.com 25`, only from systems within the local network. The response should reveal the name of the SMTP server. Of course, you can go further with an e-mail client like mutt.

+   9. When user `mike` attempts to connect from a given client, the system should prompt for and accept the passphrase defined in the exam question. (“Linux rocks, Windows does not.” with the comma and period, but without the quote marks.)

+   10. When masquerading is configured, connections from internal systems such as `server1.example.com` appear as if they come from the physical host system. That can be confirmed in log messages associated with user connections. In an **iptables**-based configuration, it adds forwarding rules.

+   11. Users with an account on the Samba server should be able to connect to their home directories on that server. But the files on that directory won’t be accessible unless the `samba_enable_home_dirs` boolean is enabled.