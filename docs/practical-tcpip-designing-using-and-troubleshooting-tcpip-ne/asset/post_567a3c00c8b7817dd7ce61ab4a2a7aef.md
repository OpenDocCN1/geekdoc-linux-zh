
### 14.11 URLs and Web page names

For simple Web pages, the page name is often the path name of the file containing the HTML code for the page, on the Web server machine. The path is usually not the full path of the file on the machine, but is relative to some base “document root directory” beneath which are stored all the Web page files. For example, the URL **http://www.uit.co.uk/training/course-index.htm** refers to the page name

/training/course-index.htm

which in fact refers to the file on our UNIX Web server machine (Figure 14.8):

/usr/local/netscape/doc/training/course-index.htm

![](img/a2132b646d336d5f9a21102d6320e537_403_0.png)

Because the page name often refers to a real file, the page name is case-sensitive if the filename is too. In practice this means that page names are case-sensitive on UNIX servers and not on Windows-NT servers. As you usually don’t know which is which, the best policy is to enter page names exactly as you were given them.

If no page name is specified, it is interpreted as “/”, which is what is referred to as the *home page* of the Web site. This is why we usually use the request **“GET /”** when we’re testing a Web connection using **telnet**.

The page name doesn’t have to refer to a relative path name. It’s entirely up to the server to interpret the page name as it wishes. Mapping page names to filenames as above is very easy on a conventional computer. However, if the Web server is the interface to a special-purpose box such as a router, or a network printer, or a firewall, there may be no conventional file system or even operating system on the box, and in these cases page names are interpreted by the server to display some internal data or to present a form for modifying the configuration.

### **“Dynamic” Web pages**

The course-index.htm page in Figure 14.8 is a *static* page: it consists of HTML contained in a text file on disk. The contents of the file don’t change, and each time you request this page you get exactly the same content.

However, it’s often necessary to include dynamically generated information in a page. For example, when you search a Web site for a particular term, the list of matches depends (we hope) on what you’re searching for; or, if you use a Web-based tool like our sub-net calculators from Part 1, the results displayed are generated from the network details you input earlier.

Pages like this are created by special applications or scripts that run under the control of the Web server. Typically, you enter some information via a form on a Web page. When you press “Enter” or “Submit” or “Go,” the data you entered on the form are sent to the Web server, which runs the application configured to handle this form, and the Web server copies the input data to the application. The application performs its calculations or searches the pages on disk or whatever it’s supposed to do, and generates an HTML page containing the results (Figure 14.9). This stream of HTML data is passed to the Web server, which serves it to the client. These applications are often called *CGI scripts* or *CGI programs* because the standard for exchanging information between server and application is the *Common Gateway Interface (CGI)*.

![](img/a2132b646d336d5f9a21102d6320e537_404_0.png)

**Figure 14.9** Browser retrieving a dynamic page from a server

Another type of page is where some of the page is stored as HTML on disk, but it also contains special commands that are interpreted by the Web server before it serves the page to the client. *Server-side includes* and Microsoft’s *Active Server Pages (ASP)* and PHP work in this way. They can be used for simple tasks (e.g., to insert a “last updated” time on the page automatically), or for very complex applications interrogating and updating databases.

## 14.12 Web proxy servers

A "proxy" in both human and computing senses is an agent that does something on your behalf, so you don't have to do it yourself. A common example is appointing someone as your proxy to vote for you at a shareholders' meeting when you can't attend. For HTTP, a proxy server is a server that your browser connects to for some or all of its transfers; your browser sends requests to the proxy server, and then the proxy server retrieves the pages from the real servers (which are called origin servers). Figure 14.10 shows how a proxy server is typically installed on a LAN; all clients on the LAN connect to the proxy, and it retrieves the pages from the remote Web sites.

![](img/a2132b646d336d5f9a21102d6320e537_405_0.png)

Figure 14.10 Typical proxy server configuration on a LAN

The proxy appears as a server to the client, and as a client to the origin server. Figure 14.11 shows a small network that we've used to show proxying in operation. The browser client requests the page /images/navtop.gif from the Web server on 192.0.2.29, via the proxy server on 192.0.2.17. (Neither server is using port 80 just to emphasize that it's not essential.) Figure 14.12 shows an ngrep trace for the conversations. (Because ngrep doesn't have the facility to print host addresses as named, we've cheated and edited the trace by hand to show names instead of numbers, to make it easier to see what each machine is doing.)

![](img/a2132b646d336d5f9a21102d6320e537_405_1.png)

Figure 14.11 Proxying in operation

The trace shows all the headers, in both directions, and illustrates:

- the conversation from browser to proxy is almost the same as if the client was talking to a normal Web server
- however, the client sends the full URL to the proxy, including the protocol scheme, host address, port number and page name. The proxy needs this information to know which Web server to connect to, and on which port
- the proxy specifies only the page name when connecting to the real (origin) Web server – it specified the IP address and port number implicitly when it established the TCP connection to this server.

```
alice% ngrep port 80 or 81 or 91
interface: eth0 (192.0.2.0/255.255.255.128)
filter: ip and ( port 80 or 81 or 91 )
###
T myclient:4003 -> myprox:81 [AP]
GET http://mail.91/images/navtop.gif HTTP/1.1 Accept: */*. Accept-Language: en-gb. User-Agent: Mozilla/4.0 (compatible; MSIE 5.5; Windows NT 4.0). Host: mail.91. Proxy-Connection: Keep-Alive. Pragma: no-cache.
####
T myprox:1246 -> myorig:91 [AP]
GET /images/navtop.gif HTTP/1.0 ...
##
T myprox:1246 -> myorig:91 [AP]
Accept: */*. Accept-Language: en-gb. User-Agent: Mozilla/4.0 (compatible; MSIE 5.5; Windows NT 4.0). Host: mail.91. Proxy-Connection: Keep-Alive. Pragma: no-cache....
##
T myorig:91 -> myprox:1246 [AP]
HTTP/1.0 200 Document Follows. MIME-Version: 1.0. Content-Type: image/gif. Content-Length: 179. GIF89a ...
...I......0...L...DI...j
 d z. e $..s2 xu ...x]. S.%J5. 92. }.."0c.a...k.7...;
##
T myprox:81 -> myclient:4003 [AP]
HTTP/1.0 200 Document Follows..
####
T myprox:81 -> myclient:4003 [APP]
MIME-Version: 1.0. Content-Type: image/gif. Content-Length: 179. GIF
89a ...
...I......0...L...DI...j...d...z...e...$...s2...xu...
##...x]. S.%J5. 92. }.."0c.a...k.7...;
alice%
####exit
alice%
```

**Figure 14.12 ngrep trace of Web page retrieved via proxy on network in Figure 14.11**

## 14.13 Why use a Web proxy server?

The two main reasons for using a proxy are performance and security.

1. proxy servers can improve performance by caching the Web pages they retrieve. If another client on the LAN requests a page that the proxy server has cached, the proxy can send it to the client straight away, without having to contact the origin server again. This is very much faster because the proxy server is on the LAN, and the data are transferred over 10Mbps or 100Mbps Ethernet, instead of using the Internet connection, which is often 100 times slower. Caching can give big performance improvements because there’s usually a lot of duplication in the sets of Web pages retrieved by different people in the same organization. An unusually nice side effect of this is that the more clients that use the proxy, the more pages are cached, the better the chance that any given page is already in the cache, and the better the average response time.

Other benefits are that the load on the Internet connection is reduced, making it more responsive for retrievals and other traffic that have to go to the Internet, and that the overall traffic on the Internet is reduced too.

Because the proxy caches pages, caching in the desktop clients, i.e. in the Web browsers, can be disabled, saving a lot of disk space over the network as a whole, with little performance penalty.

Some proxy servers allow you to specify a list of Web sites or pages that your users commonly refer to. These pages are then downloaded off-peak, ready for use from the cache in the proxy next day. This may allow users to retrieve the information they need even if the Internet connection fails during the day.

2. proxies are also used for security reasons. In many organizations, desktop PCs on the LAN don’t have direct access to the Internet as a matter of policy: they are blocked by the firewall (Chapter 24). However, clients can access a proxy server on the LAN, which in turn retrieves Web pages for them, because it is allowed access to the Internet.

![](img/a2132b646d336d5f9a21102d6320e537_407_0.png)
