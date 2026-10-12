![](bbox=[0.06, 0.14, 0.14, 0.25])

If you have installed a previous version of sendmail during Red Hat Linux installation, remove the sendmail packages before you install a new version; they might not be exactly compatible. To uninstall an RPM package, use the rpm -e package_name command. You can also locate the exact package name of an RPM package using the rpm -q partial_package_name command.

After you install the packages, you are ready to configure sendmail. The primary configuration file for sendmail is /etc/sendmail.cf.

# Configuring sendmail to listen to network interface

By default sendmail only listens to the 127.0.0.1 interface, the loopback interface, which means that you cannot send or receive mail beyond your local mail server system. This is not ideal for most scenarios because you want to send and receive mail to and from other machines — that's the whole point in e-mail. In such cases, follow these steps to enable sendmail to accept connections from all hosts:

+   1. As root, remove the following line from the /etc/mail/sendmail.mc file:
+   
+   2. Back up your /etc/sendmail.cf file to /etc/sendmail.cf.good.
+   
+   3. Run m4 /etc/mail/sendmail.mc > /etc/sendmail.cf to create a new /etc/sendmail.cf file that has the network interface restriction either removed or commented out.

```
DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')
```

![](bbox=[0.06, 0.71, 0.14, 0.82])

If you wish to keep the line as a comment instead, simply add dnl in front of the line such that the line reads as follows:

```
dnl DAEMONOPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')
```