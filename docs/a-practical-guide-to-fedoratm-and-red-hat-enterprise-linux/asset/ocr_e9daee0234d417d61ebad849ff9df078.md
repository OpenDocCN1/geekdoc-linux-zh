Prerequisites Install the dovecot package. The rpm installation script creates the self-signed certificates dovecot requires in the files named /etc/pki/dovecot/certs/dovecot.pem and /etc/pki/dovecot/private/dovecot.pem. Typically, you do not need to modify the dovecot configuration file (/etc/dovecot/dovecot.conf).

Enable and start dovecot Run systemctl to cause dovecot to start when the system enters multiuser mode and then start dovecot. Use the systemctl status command to make sure the service is running.

```
```
# systemctl enable dovecot.service
# systemctl start dovecot.service
```
```

After modifying a dovecot configuration file, give the same command, replacing start with restart, to cause dovecot to reread its configuration files.

# # AUTHENTICATED RELAYING

If you travel with a portable computer such as a laptop, you might connect to the Internet through a different connection at each location where you work. Perhaps you travel for work, or maybe you just bring your laptop home at night.

This section does not apply if you always dial in to the network through your ISP. In that case, you are always connected to your ISP's network and it is as though you never moved your computer.

On a laptop you do not use a local instance of sendmail to send email. Instead, you use SMTP to connect to an ISP or to a company's SMTP server (a smarthost), which then relays your outgoing mail. To avoid relaying email for anyone, including malicious users who would send spam, SMTP servers restrict who they relay email for, based on IP address. By implementing authenticated relaying, you can cause the SMTP server to authenticate, based on user identification. In addition, SMTP can encrypt communication when you send mail from your email client and use an SMTP server.

An authenticated relay provides several advantages over a plain connection:

+   - You can send email from any Internet connection.
+   - The secure connection makes it more difficult to intercept email as it traverses the Internet.
+   - The outgoing mail server requires authentication, preventing it from being used for spam.

You set up authenticated relaying by creating an SSL certificate or using an existing one, enabling SSL in sendmail, and telling your email client to connect to the SMTP server using SSL. If you have an SSL certificate from a company such as VeriSign, you can skip the next section in which you create a self-signed certificate.