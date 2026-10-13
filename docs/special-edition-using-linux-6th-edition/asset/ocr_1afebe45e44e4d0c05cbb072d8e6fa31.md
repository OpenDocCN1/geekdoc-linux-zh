First, this section walks you through setting up Webmin securely. If you’ve installed OpenSSL and the Perl Net::SSLeay, you’re ready to continue. First, ensure you’ve installed the Webmin RPM and that it’s running. You can check that it’s installed as discussed in Chapter 16, “Software Package Management.” You can check that it is running either by using grepping `netstat -an` for 1000 to see if it’s binding port 1000, or by looking in the process listings for a line similar to the following:

```
/usr/bin/perl /usr/libexec/webmin/miniserv.pl /etc/webmin/miniserv.conf
```

If Webmin isn’t running, the following simple command takes care of running it:

```
/etc/rc.d/init.d/webmin start
```

After you have Webmin running, open Netscape (unfortunately, Lynx will no longer work with Webmin as of version 0.78, and this problem might not be rectified in the future) and go to the following URL:

```
http://localhost:1000/
```

You should be prompted for a username and password. Use your root username and root’s password to access Webmin.

When Webmin opens, you’ll see a screen containing several tabs across the top. The active tab should be the Webmin tab, and you should see below it several icons that include Webmin Configuration and Webmin Users.

Select the Webmin Configuration icon. This opens a page with another selection of icons. Here, you can configure a large number of options regarding how Webmin looks, feels, and runs. Change your language if you so desire, and then go to the Port and Address module.

The Port and Address module has one small configuration box inside. This box contains two text boxes, the first of which is blank, and the leading selection is All, which means Webmin will listen on all IP addresses the host has. If your situation requires, you can limit the addresses to which Webmin will listen. The default should be fine for most situations. The second box is the port. Caldera installs Webmin to run on the privileged port 1000. Unfortunately, this poses a problem when running with SSL. So change port 1000 to 10000 (just add a 0) and select Save.

When you select Save, Webmin stops the server process as it has binding port 1000 and restarts on port 10000, so you will be forced to log in again. Do so.

Now you’ll want to go the Webmin index and select Webmin configuration again. This time, you should see an icon for SSL Encryption. This icon will show up only if you have OpenSSL and the Perl net::SSLeay modules installed. Select this icon.

In the SSL Encryption configuration box you will see two mutually exclusive buttons: one to enable SSL support, and one to disable SSL support. Select the Enable option and save it.

When you select Save, you will again be logged out of Webmin. This time, you’ll need to ensure that you change your URL to the following:

```
https://localhost:10000/
```