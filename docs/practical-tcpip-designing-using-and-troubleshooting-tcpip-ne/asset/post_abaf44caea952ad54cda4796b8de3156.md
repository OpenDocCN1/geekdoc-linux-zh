
## 14.7 Lab – more advanced HTTP sessions

First, we use `ngrep` to view what is exchanged between client and server. Below we give the trace of a browser retrieving one page, **std-index.htm** from a local Web server:

```text
alice$ ngrep port 80 and host carol and alice
interface: eth0 (192.0.2.0/255.255.255.128)
filter: ip and ( port 80 and host carol and alice )
T 192.0.2.21:3884 -> 192.0.2.17:80 [AP]
  GET /std-index.htm HTTP/1.1
  Accept: */*
  Referer: http://alice/
  Accept-Language: en-gb
  Accept-Encoding: gzip, deflate
  User-Agent: Mozilla/4.0 (compatible; MSIE 5.5, Windows NT 4.0)
  Host: alice
  Connection: Keep-Alive
  Pragma: no-cache
T 192.0.2.17:80 -> 192.0.2.21:3884 [AP]
  HTTP/1.0 200 OK
  Date: Sun, 15 Jul 2001 08:02:57 GMT
  Server: Apache/1.3.9 (Unix) Debian/GNU mod_layout/2.10.6 mod_perl/1.21.03-dev
  Last-Modified: Mon, 17 Mar 1997 13:11:41 GMT
  ETag: "1fe63-211-332d43d0"
  Accept-Ranges: bytes
  Content-Length: 529
  Connection: close
  Content-Type: text/html; charset=iso-8859-1
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 2.0 + all extensions//EN" "mapro3.dtd">
  <HTML> <HEAD> <TITLE>Standards - W3C</TITLE>. </HEAD>
  <BODY BGCOLOR="#FFFFFF">
  <H1 ALIGN="CENTER">UIT STANDARDS</H1>
  <CENTER>
  <TABLE>
  <TR> <TD></TD> <TD><A HREF="std-web.htm">UTNet web page layout</A></TD> <TD></TD>. </TR>
  <TR> <TD></TD> <TD><A HREF="std-cols.htm">Colour conventions</A></TD> <TD></TD></TR>
  <TR> <TD></TD> <TD><A HREF="std-mktmaterials.htm">Marketing materials</A></TD> <TD></TD>. </TR>
  </TABLE>
  </CENTER>
  </BODY></HTML>
```

`ngrep` shows you all the request and response headers clearly (even though they all run together because `ngrep` shows carriage returns and linefeeds as dots to save space). You can see that the headers are giving information both about the data that was transferred, and about the client and server involved in the transfer: the client is Microsoft Internet Explorer, and the server is Apache running on Debian Linux.

Now we connect to a Web server using `telnet` to run sessions by hand so we can control and observe what’s happening. The trace below illustrates what often happens nowadays when you use the old HTTP/0.9 simple request format with modern servers – you get an error reported in the page returned, saying there is no such site:

```text
alice$ telnet www.microsoft.com 80
Connected to www.microsoft.akadns.net.
GET /
  HTTP/1.1 404 Object Not Found
  Server: Microsoft-IIS/5.0
  Date: Thu, 19 Jul 2001 16:37:57 GMT
  Content-Type: text/html
  Content-Length: 111

    <html><head><title>Site Not Found;</title></head>
    <body>No web site is configured at this address.</body></html>
Connection Closed by foreign host.
alice$
```

What’s happening is that the server machine is hosting many different Web sites, all on the same IP address, and it doesn’t know which one you want. To get over this, you must include a Host: header, specifying the Web site name you want, and to do that, you must use the full-request format:

full-request must include protocol version

```text
alice% telnet www.microsoft.com 80
Trying 207.46.230.219...
Connected to www.microsoft.akadns.net.
Escape character is '^]'.
GET / HTTP/1.0
Host: www.microsoft.com

HTTP/1.1 200 OK
Server: Microsoft-IIS/5.0
P3P: CP="ALL IND DSP COR ADM CON CUR CUS IVA"
Content-Location: http://www.microsoft.com/D
Date: Thu, 19 Jul 2001 16:44:21 GMT
Content-Type: text/html
Accept-Ranges: none
Last-Modified: Thu, 19 Jul 2001 13:47:08 GMT
Content-Length: 24459

<HTML>
<HEAD>
<META HTTP-EQUIV="Content-Type" CONTENT="text/
<TITLE>Welcome to the Microsoft Corporate Wel
...
```

- **host**: header says which Web site we want on this machine
- blank line signals end of request headers
- first response from server is status-line, not a header
- response headers follow, saying what type of content is being returned, how big it is, etc.
- blank line signals end of response headers
- at last the server sends the actual body – the Web page

You *must* include a **Host:** header with HTTP/1.1. If you omit it you get an error, although some servers may just say “Site not found”:

```text
alice% telnet www.netscape.com 80
Trying 207.200.89.193...
Connected to home-gs1b.netscape.com.
Escape character is '^]'.
GET / HTTP/1.1
HTTP/1.1 400 Bad request
Server: Netscape-Enterprise/4.1
Date: Thu, 19 Jul 2001 17:15:44 GMT
Content-length: 147
Content-type: text/html
Connection: close

<HTML><HEAD><TITLE>Bad request</TITLE></HEAD>
<BODY><H1>Bad request</H1>
Your browser sent a query this server could not understand.
</BODY></HTML>
Connection closed by foreign host.
alice%
```

host: header missing

In the next module we continue with headers, and see how the server uses MIME to specify the type of data being returned.

## 14.8 How MIME fits in with HTTP

As we explained in Module 12.2, MIME, the Multipurpose Internet Mail Extensions, performs two important functions for e-mail: allowing arbitrary binary content to be sent safely over links that can only handle 7-bit characters, and specifying the type of content in the message. In HTTP, the Web client and server also use MIME, but they use it only to exchange information about the type of data they are transferring to one another. (They don't need to worry about encoding binary data as 7-bit characters, because HTTP is running over TCP, which handles 8-bit binary data faithfully – it’s “8-bit safe” or “8-bit clean.”) Below we show a simple session using telnet to retrieve a GIF image file:

```text
alice% telnet dave 80
 Trying 192.0.2.5...
 Connected to dave.example.com.
 Escape character is '^]'.
GET /dir.gif HTTP/1.0  we're using HTTP/1.0 so
                        we don't have to include a
                        Host: header

HTTP/1.0 200 Document follows
MIME-Version: 1.0
Server: CERN/3.0pre6
Date: Thursday, 12-Jul-01 06:07:31 GMT
Content-Type: image/gif
Content-Length: 138
Last-Modified: Friday, 06-Dec-96 17:11:41 GMT
X-httpd-warning: Your browser didn't send the Accept header line for this
GIF89a…
Connection closed by foreign host.
alice%
```

This illustrates several points:

- the server says it's using MIME to describe the contents of the data it's returning
- the data are in **image**, specifically in the **gif** image format
- the data consist of 138 bytes
- browsers can use an **Accept:** header in their request to the server to tell it what type of data formats the browser is prepared to handle. We, as client, didn't send an **Accept:** header, so the server gives a warning. (We don't cover **Accept** any further; we only mentioned it here to avoid confusion in case you come across it.)
- the server transfers the data un-encoded, as raw binary data, because it's working over an 8-bit safe TCP transport. The contents of the file show as gobbleygook because that's how the binary characters in the GIF file print on our terminal.

MIME is important because it lets the browser take informed decisions about what to do with the content, relieving the user of having to specify what's to be done:

- the obvious examples are GIF and JPEG images, which are normally displayed inline as an integral part of the page
- when your browser downloads a page that is specified, say, as type **application/Zip** and you have configured your browser (or Windows Explorer if you're on Windows) to use the **WinZip** program to handle ZIP files, the browser can automatically prompt (Figure 14.7) and ask if you want to open the file when it's downloaded. This saves you having to save the file to disk, and then explicitly start WinZip to process the file
- if the browser doesn't recognize the content-type of the Web page, or if it doesn't have the necessary code in-built to handle it, or doesn't know what program to use to process the data, it will typically offer to save the file to disk for you.

![](img/a2132b646d336d5f9a21102d6320e537_398_0.png)

**ngrep** is a very easy way to see what MIME headers are being transmitted from the server in a live session. This is useful if a browser seems to be misbehaving and is doing something strange with a particular page or type of data – you can see whether the server is sending the correct information about content-type. If the server is specifying the wrong content-type, the client may be acting correctly but in response to incorrect data.
