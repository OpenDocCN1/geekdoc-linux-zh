If the output of `ps ax` doesn’t show any Web server processes, errors may lurk in the Apache configuration file. If this is the case, you have to fix any problems in the configuration file and start the server again.

If the Web server is up and running, you can use the TELNET program to connect to port 80 and see if the server works. Begin by typing the following command in a terminal window:

```
telnet localhost 80
```

After you get the `Connected` message, type

```
HEAD / HTTP/1.0
```

Then press Enter twice. You get a response that looks similar to the following, but with different dates and numbers, of course:

```
HTTP/1.1 200 OK
Date: Sat, 17 Dec 2005 20:57:20 GMT
Server: Apache/2.0.54 (Fedora)
Last-Modified: Sat, 17 Dec 2005 20:57:05 GMT
ETag: "156946-25b-8f6d64a0"
Accept-Ranges: bytes
Content-Length: 603
Connection: close
Content-Type: text/html; charset=UTF-8

Connection closed by foreign host.
```

The response shows some information about the Web server and the default home page. You can also check out the Web server by using a Web browser, such as Firefox, running on your Linux system. Use the URL
http://localhost/ and see what happens.

![](bbox=[0.12, 0.72, 0.18, 0.77])

If you get an error message when you try the http://localhost/ URL in a Web browser, that means there is no `index.html` file (the default Web page) in the directory specified by the `DocumentRoot` configuration directive. To correct the problem, just create a simple HTML document named `index.html` in the appropriate directory (look in the HTTP server’s configuration file for the directory name specified by `DocumentRoot`). I explain configuration directives such as `DocumentRoot` in the next section.

# Configuring the Apache Web Server

The Apache Web server program files and configuration files are stored in different locations in different distributions. The Apache Web server configuration file is named `httpd.conf` in Fedora Core, Knoppix, SUSE, and