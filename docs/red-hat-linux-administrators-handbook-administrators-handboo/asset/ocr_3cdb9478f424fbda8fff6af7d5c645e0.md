# lynx

Syntax:

```
lynx [-dump] [-head] [URL]
```

lynx is the most popular interactive text-based Web browser. To run the browser, simply enter the desired URL as the command-line argument. For example,

```
lynx http://www.integrationlogic.com/
```

displays the top page of the site. lynx is a very handy program to have around. For example, to find out quickly what kind of Web server the site uses, without asking the Webmaster, run the following command:

```
lynx -head http://www.integrationlogic.com/
```

The preceding command displays the HTTP header the lynx browser receives from the Web server. An example of its output is shown here:

```
HTTP/1.1 302 Moved
Date: Tue, 02 Mar 1999 06:47:27 GMT
Server: Apache/1.3.3 (Unix)
Location: http://www.integrationlogic.com/index.shtml
Connection: close
Content-Type: text/html
```

This header shows that www.integrationlogic.com runs on the Apache 1.3.3 Web server on a UNIX platform. Note that not all Web sites will give out their Web server platform information, but most do. If you want to avoid the interactive mode, you can use the -dump option to dump the page on the screen (STDOUT). For example,

```
lynx -dump -head http://www.integrationlogic.com/
```

dumps the header to stdout. The -dump feature can be quite handy. For example,

```
lynx -dump -head http://webserver/new.gif > new.gif
```

allows you to save new.gif on the Web server host on a local file called new.gif.