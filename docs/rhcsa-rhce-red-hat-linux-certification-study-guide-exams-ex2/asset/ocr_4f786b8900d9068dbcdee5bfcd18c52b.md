# LAB ANSWERS

For most of these labs, you may be using an e-mail client like mutt. To send an e-mail to say user michael@localhost, take the following steps:

+   1. Run the mutt michael@localhost command. The To: michael@localhost message should appear.
+   2. Press ENTER. At the Subject: prompt, enter an appropriate test subject name and press ENTER.
+   3. You're taken to a blank screen in the vi editor. Use commands appropriate to that editor to a screen similar to that shown in Figure 13-5.
+   13. From the screen shown in Figure 13-5, press y to send the noted message.

In addition, you may be verifying e-mail receipt in files a username file in the /var/spool/mail directory. Normally, such e-mail can be reviewed from within a user account with the mail command. In addition, you may be verifying access to a running SMTP server with the telnet ip_address 25 command, where ip_address is the IP address of the SMTP server.

After making a configuration change, don't forget to process the file appropriately. For Postfix, the postmap filename command processes the file. For sendmail, the /etc/mail/make script processes the file. For the common /etc/aliases file, the newaliases command processes the file. And don't forget to make sure the service actually re-reads the new configuration files.

# Lab I

In Postfix, to disable local-only access in the /etc/postfix/main.cf file, change the inet_interfaces directive to accept all connections:

```
inet_interfaces = all
```

FIGURE 13-5

The mutt e-mail client.

![](bbox=[0.18, 0.75, 0.92, 0.95])