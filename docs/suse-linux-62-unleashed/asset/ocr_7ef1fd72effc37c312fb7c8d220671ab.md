# Issue the following command:

```
kill -f1 PID
```

The easiest way to find inetd's process ID is to type ps -ef | grep inetd. The process ID will be in the second column from the left.

The procedure should successfully enable SWAT on a typically SuSE server. The next step is to access Samba configuration through SWAT.

# Configuring smb.conf from Your Browser Using SWAT

Security Caution

After completing your SWAT work, you must close all browsers on your workstation. All open browsers will “remember” the password, allowing anyone with physical access to your workstation (or server terminal) access to Samba configuration, including password administration.

Additionally, if SWAT is used on a browser at a remote workstation, passwords are sent across clear text and can be sniffed.

For best security, use SWAT only on the server's terminal and, when done, all browsers.

From your favorite browser, including Netscape Navigator, Microsoft Internet Explorer, or Lynx, navigate to port 901 of the server's IP address:

```
#Lynx http://192.168.100.1:901
```

The browser asks for a username and password. To enable read-write access, use root and root's password. Once authenticated, a page appears with links for HOME, GLOBALS, SHARES, PRINTERS, STATUS, VIEW, and PASSWORD. CHOOSING GLOBALS, SHARES, OR PRINTERS brings up a page in which you can edit options. Each contains a button that can be toggled between Advanced View and Basic View, with Advanced View showing every possible configuration option. Note that with the SHARES and PRINTER pages, you'll need to choose the share or printer from a drop-down list and then click the Choose button before you edit the share or printer.

Assuming you're logged in to SWAT as root, a Commit Changes button will be visible on certain screens. After making changes, clicking this button will write smb.conf. If you click the Reset Values button, the options will revert to values in the present smb.conf file.