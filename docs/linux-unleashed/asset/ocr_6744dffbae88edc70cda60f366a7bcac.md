If you are using inetd to start your Web server software, you need to make a change to the /etc/services file to permit the Web software. Add a line similar to this to the /etc/services file:

```
http port/tcp
```

where port is the port number used by your Web server software (usually 80).

Next, modify the /etc/inetd.conf file to include the startup commands for the Web server where the last entry is the path to the httpd binary:

```
httpd stream tcp nowait nobody /usr/web/httpd
```

Once this is done, restart inetd by killing and restarting the inetd process or by rebooting your system, and the service should be available through whatever port you specified in /etc/services.

If you are running the Web server software as a daemon, you can start it at any time from the command line with the command:

```
httpd &
```

Even better, add the startup commands to the proper rc startup files. The entry usually looks like this:

```
# start httpd
if [ -x /usr/web/httpd ]
then
    /usr/web/httpd
fi
```

substituting the proper paths for the httpd binary, of course. Rebooting your machine should start the Web server software on the default port number.

To test the Web server software, use any Web browser and enter the following in the URL field:

```
http://machinename
```

where *machinename* is the name of your Web server. You can do this either over the Internet through a connection or from another machine on your network (if you have one). If you see the contents of the root Web directory or the `index.html` file, all is well. Otherwise, check the log files and configuration files for clues as to the problem.

If you haven't installed a Web browser yet, check to see if the Web server is running by using telnet. Issue a command like this, substituting the name of your server (and your Web port number if different than 80):

```
telnet www.wizard.tpci.com 80
```