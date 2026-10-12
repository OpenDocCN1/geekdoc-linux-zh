
You can identify this layout by looking through the listing that shows what the Web server returns in response to the GET command. Because the example uses a telnet command to get the document, you see the HTML content as lines of text. If you were to access the same Web site (www.gao.gov) with a Web browser (such as Mozilla), you see the page in its graphical form (as in Figure 2-1).

The example of HTTP commands shows the result of the GET command. GET is the most common HTTP command; it causes the server to return a specified HTML document.

The other two HTTP commands are HEAD and POST. The HEAD command is almost like GET: It causes the server to return everything in the document except the body. The POST command sends information to the server; it’s up to the server to decide how to act on the information.

## Exploring the Apache Web Server

You probably already know how to use the Web, but you may not know how to set up a Web server so you, too, can provide information to the world through Web pages. To become an information provider on the Web, you have to run a Web server on your Fedora Core PC on the Internet. You also have to prepare the Web pages for your Web site—a task that may be more demanding than the Web server setup.

![](img/9f89727199836b0f871f1745838aa8b2_644_0.png)

- Figure 2-1: The www.gao.gov Web site as viewed with the Mozilla Web browser.

### Why is it called Apache?

According to the information about the Apache Web server project on `www.apache.org/foundation/faq.html`, the Apache group was formed in March 1995 by a number of people who provided patch files that had been written to fix bugs in NCSA HTTPD 1.3. The result after applying the patches to NCSA HTTPD was what they called a *patchy* server (that’s how the name Apache came about). The Apache Group has now evolved into The Apache Software Foundation (ASF), a nonprofit corporation that was incorporated in Delaware, U.S.A., in June 1999. ASF has a number of other ongoing projects. You can read about these projects at `www.apache.org`. In particular, visit `httpd.apache.org` for more information about the Apache Web server project.

According to the April 2004 Netcraft Web Server Survey at `news.netcraft.com/archives/web_server_survey.html`, the Apache Web server is the most popular — 66.99 percent of the 49,750,568 sites reported using the Apache server. Microsoft Internet Information Server (IIS) is a distant second, with 21.49 percent of the sites.

Among the available Web servers, the Apache Web server is the most popular, and it comes with Fedora Core. The Apache Web server started out as an improved version of the NCSA HTTPD server but soon grew into a separate development effort. Like NCSA HTTPD, the Apache server is developed and maintained by a team of collaborators. Apache is freely available over the Internet.

### Installing the Apache Web server

Depending on the Fedora Core installation options, the Apache Web server may be already installed in your system. To find out whether it’s installed, type the following command:

```bash
rpm -q httpd
```

If the Web server is installed, you see an output like this:

```bash
httpd-2.0.48-16.1
```

If you get a message that `httpd` is not installed, you can install it easily from this book’s companion DVD-ROMs using these steps:

1. **Log in as root and insert the DVD-ROM into the DVD drive.**
   - If you’re in the GNOME or KDE graphical desktop, the DVD is automatically mounted. If not, type the command `mount /dev/cdrom` to mount the DVD-ROM.
2. **Type the following commands to install the Apache Web server:**

```bash
cd /mnt/cdrom/Fedora/RPMS
rpm -ivh httpd*
```

That's it! You can now run the Apache Web server.

### Starting the Apache Web server

Even if the Apache Web server is installed, it may not be set up to start at boot time. If you want to try it out, you have to start the server. To do so, log in as `root` and type the following command:

```bash
service httpd start
```

To see whether the `httpd` process (`httpd` is the name of the Apache Web server program) is running, type the following command:

```bash
ps ax | grep httpd
```

The output shows a number of `httpd` processes. Running several Web server processes — one parent and several child processes — is a common approach so several HTTP requests can be handled efficiently by assigning each request to an `httpd` process.

If you can't find an `httpd` process, errors may be lurking in the Apache configuration file. If this is the case, some error messages appear and give you a clue about the cause of the error. You have to fix the problem in the configuration file and start the server again.

If the `httpd` processes are up and running, you can use the TELNET program to see if it works, but first you have to add a default home page in the `/var/www/html` directory. If you don't have time to prepare one, copy the Web page that's supposed to be sent out in case of errors. Here's the command you type (while logged in as `root`) to get it:

```bash
cp /var/www/error/noindex.html /var/www/html/index.html
```

Now you have a default home page and you can type the following command in a terminal window to check out if the Web server is working or not:

```bash
telnet localhost 80
```

After you get the Connected message, type:

```bash
HEAD / HTTP/1.0
```

Then press Enter twice. You get a response that looks similar to the following (with different dates and numbers, of course):

```bash
HTTP/1.1 200 OK
Date: Sat, 13 Mar 2004 21:51:18 GMT
Server: Apache/2.0.48 (Fedora)
Last-Modified: Sat, 13 Mar 2004 21:51:08 GMT
ETag: "8c246-f30-3eec2c00"
Accept-Ranges: bytes
Content-Length: 3888
Connection: close
Content-Type: text/html; charset=UTF-8

Connection closed by foreign host.
```

The response shows some information about the Web server and the default home page. You can also check out the Web server by using a Web browser, such as Mozilla, running on your Fedora Core system. Use the URL `http://localhost/` and see what happens. You see a Web page with the title "Test Page for the Apache HTTP Server on Fedora Core."

![](img/9f89727199836b0f871f1745838aa8b2_647_0.png)

If you want to start the Apache Web server automatically at boot time, type the following command to set it up:

```bash
chkconfig --levels 35 httpd on
```

## Configuring the Apache Web Server

By default, the Apache Web server software is configured to use the following files and directories:

- The Web server program — *httpd* — is installed in the `/usr/sbin` directory.
- The Apache Web server configuration file — *httpd.conf* — is located in the `/etc/httpd/conf` directory. The configuration file is a text file with directives that specify various aspects of the Web server. The `/etc/httpd/conf` directory also contains information about the Secure Sockets Layer (SSL) implementation needs. (The SSL implementation comes as part of the Apache Web server.)
- The Apache Web server is set up to serve the HTML documents from the `/var/www/html` directory. Therefore, place your Web pages in this directory.
- If you have any Common Gateway Interface (CGI) programs — programs the Web server can invoke to access other files and databases — place these in the `/var/www/cgi-bin/` directory.
- The `/var/log/httpd` directory is meant for Web server log files (access logs and error logs).
- The `/etc/init.d/httpd` script starts the `httpd` process as your Fedora Core system boots, provided you enable it by using the `chkconfig` command.

### Using Apache configuration tools

Fedora Core comes with a graphical configuration tool that you can use to configure the Apache Web server. To run this configuration tool, log in as `root` and choose **Main Menu**→**System Settings**→**Server Settings**→**HTTP** from the GNOME desktop. The Apache Configuration window appears (as in Figure 2-2).

![](img/9f89727199836b0f871f1745838aa8b2_648_0.png)

The Apache Configuration window is organized into four tabs. You can set various options from each of these tabs:

- **Main:** From this tab, you can specify the IP addresses and port number where Apache expects requests for Web service. You can also set the e-mail address of the Webmaster.
- **Virtual Hosts:** Here you can set up virtual hosts. I discuss the options for virtual hosts later in this chapter. You can also edit the default settings that apply to all virtual hosts. Clicking the Edit Default Settings button on the Virtual Hosts tab brings up another window (shown in Figure 2-3) from which you can set a number of different options.
- **Server:** This tab has settings for the server such as the user and group names under which the HTTP server runs and the locations of the file where the process ID is stored.
