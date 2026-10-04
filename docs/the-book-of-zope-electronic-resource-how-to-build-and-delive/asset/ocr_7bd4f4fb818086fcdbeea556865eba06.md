Once the FTP program connects to your Zerver, the following message should appear:

```
Connected to localhost.localdomain.
-----
2001-06-18T04:22:59 INFO(0) ZServer Incoming connection from 127.0.0.1:3160
220 my.mydomain.com FTP server (Medusa Async V1.13 [experimental]) ready.
Name (localhost:username):
At the prompt above, enter the Zope username to log in as and press enter. Then
enter the password.
331 Password required.
Password:
230 login successful.
-----
2001-08-18T04:23:21 INFO(0) ZServer Successful login.
Remote system type is UNIX.
Using binary mode to transfer files.
tfp>
If you have successfully logged in, you can execute standard FTP commands,
such as ls, cd, get, and put.
For example, to get a listing of objects in the current folder, use the ls
command:
ftp> ls
227 Entering Passive Mode (127,0,0,1,12,92)
150 Opening ASCII mode data connection for file list
drwkxtw--- 1 Zope Zope 0 Jan 20 21:39 Control_Panel
drwkxtw--- 1 Zope Zope 0 May 31 04:36 QuickStart
 1 Zope Zope 0 Dec 30 1998 acl_users
-TW-IW---- 1 Zope Zope 92 Jan 20 21:39 index_html
-TW-IW---- 1 Zope Zope 1365 Jan 20 21:39 standard error_message
-TW-IW---- 1 Zope Zope 53 Jan 20 21:39 standard_html_footer
-TW-IW---- 1 Zope Zope 128 May 21 17:32 standard_html_header
226 Transfer complete
ftp> get index_html
local: index_html remote: index_html
227 Entering Passive Mode (127,0,0,1,12,94)
150 Opening Binary mode data connection for file 'index_html'
226 Transfer complete
92 bytes received in 0.00787 secs (11 Kbytes/sec)
```

To download an object (such as a DTML document) from Zope to your local computer, use the get command: