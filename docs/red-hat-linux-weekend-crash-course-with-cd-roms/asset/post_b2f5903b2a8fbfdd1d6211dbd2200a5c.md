
His complete e-mail address is jdoe@someplace.net. Given that address, anyone on the Internet can send e-mail to John Doe.

To set up and use e-mail on your Red Hat Linux PC, you need two types of mail software:

- *Mail-user agent* software enables you to read your mail messages, write replies, and compose new messages. Typically, the mail-user agent retrieves messages from the mail server using POP3 or IMAP4 protocol. POP3 is the Post Office Protocol version 3 and IMAP4 is the Internet Message Access Protocol version 4. The Red Hat Linux CD-ROMs include several popular mail user agents such as `pine` and `elm`.
- *Mail-transport agent* software actually sends and receives mail-message text. The exact method used for mail transport depends on the underlying network. In TCP/IP networks, the mail-transport agent delivers mail using the Simple Mail Transfer Protocol (SMTP). This book’s Red Hat Linux CD-ROMs include `sendmail`, a powerful and popular mail-transport agent for TCP/IP networks.

Most mail-transport agents run as *daemons* — background processes that run as long as your system is up. Because you or another user on the system can send mail at any time, the transport agent has to be there to deliver the mail to its destination. The mail-user agent runs only when the user wants to check mail.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_190_0.png)

Typically, a mail-transport agent starts after the system boots. The system startup files for Red Hat Linux are set up so that the sendmail mail-transport agent starts when the Linux system is in multiuser mode. The shell script file `/etc/rc.d/init.d/sendmail` starts sendmail.

Because the system is already set up to start sendmail at boot time, all you have to do is use an appropriate sendmail configuration file to get e-mail going on your Linux system.

You cannot send or receive e-mail until the sendmail mail-transport agent is configured properly. The sendmail transport agent has the reputation of being a complex, but complete, mail-delivery system. If you take a quick look at sendmail’s configuration file, `/etc/sendmail.cf`, you can see that sendmail is indeed complex. Luckily, you do not have to be an expert on the sendmail configuration file. All you need is the predefined configuration files from this book’s companion CD-ROMs.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_191_0.png)

If you install the Mail/WWW/News Tools component during Red Hat Linux installation (see Session 3), your system should have a working sendmail configuration file — /etc/sendmail.cf. The default file assumes an Internet connection and a name server. Provided you have an Internet connection, you should be able to send and receive e-mail from your Linux PC once you connect it to the Internet. Then you can use a mail-user agent such as elm to compose and send mail messages.

## Setting Up the Apache Web Server

You probably already know how it feels to use the Web, but you may not know how to set up a Web server so that you, too, can provide information to the world through Web pages. To become an information provider on the Web, you have to run a Web server on your Red Hat Linux PC on the Internet.

Web servers provide information by using HTTP. Web servers are also known as HTTP daemons (because continuously running server processes are called daemons in UNIX), or HTTPD for short. The Web server program usually is named httpd.

Among the freely available Web servers, Apache Web server is the most popular. Apache is freely available over the Internet and it accompanies Red Hat Linux on this book’s companion CD-ROMs.

When you install Red Hat Linux from this book’s companion CD-ROMs, you also have the option of installing the Apache Web server. If you install the Mail/WWW/News Tools package during Red Hat Linux installation, then Red Hat Linux automatically starts the Apache Web server during system boot.

Perform the following steps to verify that the Apache Web server software is installed and running on your system:

1. Type the following command to check whether the Apache Web server is installed:
```
rpm -q apache
```
apache-1.3.12-21

If the output shows an apache package name, you have the Apache software installed on your system.

2. Type the following command to check whether the httpd process (the name of the Apache Web server program is httpd) is running:
```
ps ax | grep httpd
```

The output should show a number of httpd processes. It is common to run several Web server processes — one parent and several child processes — so that several HTTP requests can be handled efficiently by assigning each request to an httpd process.

3. Use the telnet program on your Linux system and employ the HTTP HEAD command to query the Web server as follows:
```
telnet localhost 80
Trying 128.0.0.1...
Connected to localhost.
Escape character is '^]'.
HEAD / HTTP/1.0
... Press Enter once more to type a blank line
HTTP/1.1 200 OK
Date: Sat, 19 Aug 2000 23:57:14 GMT
Server: Apache/1.3.12 (Unix)  (Red Hat/Linux)
Last-Modified: Mon, 07 Aug 2000 10:21:07 GMT
ETag: "328fe-b4a-398e8d93"
Accept-Ranges: bytes
Content-Length: 2890
Connection: close
Content-Type: text/html

Connection closed by foreign host.
```

If you get a response such as the preceding, your system already has the Apache Web server installed and set up correctly. All you have to do is understand the configuration so that you can place the HTML documents in the proper directory.

4. Use a Web server to load the home page from your system. Start Netscape Navigator by clicking the big “N” icon on the GNOME Panel, use the URL http://localhost/, and then see what happens. You should see a Web page with the title “Test Page for the Apache Web Server on Red Hat Linux.”

The Apache Web server is set up to serve the HTML documents from the /var/www/html directory. Therefore, you should place your Web pages in the /var/www/html directory. In particular, edit or replace the /var/www/html/index.html file with your own home page.

In addition to the HTML files, the Apache Web server also supports Common Gateway Interface (CGI) programs — programs that the Web server can invoke to access other files and databases. You should place any CGI programs in the /var/www/cgi-bin directory.

Also note the following useful information about the Apache Web server:

- The Apache Web server configuration files are located in the /etc/httpd/conf directory. There are three configuration files, access.conf, httpd.conf, and srm.conf. These configuration files control how the server runs, what documents it serves, and who can access these documents.
- The /var/log/httpd directory is where the Apache Web server’s log files (access logs and error logs) are located.
- The /etc/rc.d/init.d/httpd script starts the httpd process as your Red Hat Linux system boots.

## Setting Up the FTP Server

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_193_0.png)

Besides e-mail and Web, anonymous FTP is a common service on an Internet host. You may be familiar with FTP, which you can use to transfer files from one system to another on the Internet. When you use FTP to transfer files to or from a remote system, you have to log in to the remote system before you can use FTP.

If you install Red Hat Linux from this book’s companion CD-ROMs, you should have anonymous FTP set up on your system and the FTP server configured to run when needed. The default setup also employs the necessary security precautions.

Anonymous FTP refers to the user name anonymous, which anyone can employ with FTP to transfer files from a system. Anonymous FTP is a common way to share files on the Internet. Many businesses use anonymous FTP to support their customers.

If you have used anonymous FTP to download files from various Internet sites, you already know the convenience of that service. Anonymous FTP enables you to make information available to anyone on Internet. Even if you haven’t used anonymous FTP explicitly, your Web browser often employs anonymous FTP to download files. (You simply might click a link; the Web browser does the rest.)

To see anonymous FTP in action, you can try accessing your system using an FTP client. For example, here’s a sample session when I access my system from another PC on the LAN (my input appears in boldface):

```
ftp lnbp200
Connected to lnbp200
220 lnbp200.lnbsoft.com FTP server (Version wu-2.6.0(1) Fri Feb 4 23:37:48 EST 2000) ready.
220 lnbp200 FTP server (Version wu-2.6.1(1) Wed Aug 9 05:54:50 EDT 2000) ready.
Name (lnbp200:): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password:
```
