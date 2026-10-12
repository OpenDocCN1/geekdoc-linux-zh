# Why is it called Apache?

According to the information about the Apache Web server project on www.apache.org/foundation/faq.html, the Apache group was formed in March 1995 by a number of people who provided patch files that had been written to fix bugs in NCSA HTTPd 1.3. The result after applying the patches to NCSA HTTPd was what they called a patchy server (that's how the name Apache came about). The Apache Group has now evolved into The Apache Software Foundation (ASF), a nonprofit corporation that was incorporated in Delaware, U.S.A., in June 1999. ASF has a number of other ongoing projects. You can read about these projects at www.apache.org. In particular, visit httpd.apache.org for more information about the Apache Web server project.

According to the July 2003 Netcraft Web Server Survey at news.netcraft.com/archives/web_server_survey.html, the Apache Web server is the most popular — 63.72 percent of the 42,298,371 sites reported using the Apache server. Microsoft Internet Information Server (IIS) is a distant second, with 25.95 percent of the sites.

The output should show a number of httpd processes. It's a common approach to run several Web server processes — one parent and several child processes — so several HTTP requests can be handled efficiently by assigning each request to an httpd process.

If there is no httpd process, errors may be lurking in the Apache configuration file. If this is the case, some error messages should appear and give you a clue about the cause of the error. You have to fix the problem in the configuration file and start the server again.

If the httpd processes are up and running, you can use the TELNET program to see whether it works, but first you have to add a default home page in the /var/www/html directory. If you don't have time to prepare one, copy the Web page that's supposed to be sent out in case of errors. Here's the command you type (while logged in as root) to get it:

```
cp /var/www/error/noindex.html /var/www/html/index.html
```

Now you have a default home page and you can type the following command in a terminal window to check whether the Web server is working:

```
telnet localhost 80
```

After you get the Connected message, type

```
HEAD / HTTP/1.0
```