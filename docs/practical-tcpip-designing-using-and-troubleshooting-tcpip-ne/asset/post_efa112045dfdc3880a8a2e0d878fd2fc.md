
T 156.27.8.202:80 > 192.0.2.22:1290 [AP]
HTTP/1.1 304 Not Modified. Server: Microsoft-IIS/4.0. Date: Tue, 24 Jul 2001 08:35:40 GMT. Cache-Control: max-age=1800. Expires: Tue, 24 Jul 2001 09:05:40 GMT. ETag: "1a7f38aa313c11:1769". Content-Length: 0.

Browsers typically let you specify whether to perform the above validation checks every time a page is retrieved from the cache. To be completely up to date, you should check it every time. However, for most purposes it’s adequate to check only if the last time you retrieved the page was in a different browser session.

To configure the cache operation in Internet Explorer, select menu **Tools > Internet Options > General > Temporary Internet Files > Settings** (Figure 14.19). The meanings of the options are obvious, with one exception: **Automatically** (Internet Explorer 5 and later only). Microsoft “explains” this as follows: this setting is the same as **Every time you start Internet Explorer** but with a logic algorithm to understand the habits of Web page behavior. When you return to a page you viewed previously, it checks for new content only if you last viewed this page in an earlier session of Internet Explorer or on an earlier day. Over time, if Internet Explorer determines that images on the page are changing infrequently, it checks for newer images even less frequently.

The cache settings for Netscape are so similar we haven’t illustrated them.

![](img/a2132b646d336d5f9a21102d6320e537_414_0.png)

# Figure 14.19 Cache Settings

| Action | Internet Explorer | Netscape Navigator |
|:---|:---|:---|
| check with the origin server whether the page is up to date, re-loading if necessary | key F5<br>or *click Refresh* | key *Ctrl-R* or menu<br>**View > Reload** |
| force a re-load even if the cache appears up to date | key *Ctrl-F5* | *press key Shift* with menu<br>**View > Reload** |
| re-draw the page on-screen without retrieving the page from cache or the origin server | N/A | menu **View > Refresh**<br>(not in versions after 4.x) |

The history mechanism (**Back** and **Forward** buttons in the browser) doesn’t perform cache checking, deliberately. Its function is to provide a quick way to view what you were looking at previously.

## 14.17 Security – authentication

Web servers can “protect” specific pages or directories, so that when they are requested, the user has to authenticate in some way, e.g. enter a username and password. Internally, the server maintains a list of protected pages and how users must authenticate themselves to gain access; these details are usually specified in the server’s configuration files. A typical conversation is as follows:

- 1. the client requests a protected page, *ours/treasure-map.gif* from the server
- 2. the server sends back a 401 “Unauthorized” error status line, with a **WWW-Authenticate**: header saying what type of authentication is required, and usually a page containing the error message to be displayed to the user if the authentication isn’t successful. Below is an **ngrep** trace of a request and response:

```text
T 192.0.2.22:1926 --> 192.0.2.29:80 [AP]
GET /ours/treasure-map.gif HTTP/1.1. Accept: application/vnd.ms-excel,
application/msword. application/vnd.ms-powerpoint. image/gif, image/x
-xbitmap, image/jpeg, image/jpgpeg. */*. Accept-Language: en-gb. Accept
-Encoding: gzip, deflate. User-Agent: Mozilla/4.0 (Compatible; MSIE 5.
5; Windows NT 4.0). Host: mail. Connection: Keep-Alive....
T 192.0.2.29:80 --> 192.0.2.22:1926 [AP]
HTTP/1.0 401 Unauthorized. Date: Tue, 24 Jul 2001 14:44:23 GMT. Server
Apache/1.0.3. WWW-Authenticate: Basic realm="Metro-Client". Content
type: text/html ...<HEAD><TITLE>Authorization Required</TITLE></HEAD>
<BODY><H1>Authorization Required.</H1>. This server could not verify that you are authorized to access the document you requested. Either you supplied the wrong credentials (e. g., bad password), or your browser doesn’t understand how to supply the credentials required. <P>...</BODY>
```

The response says that the type of authentication is **Basic** (i.e. username and password) and that the **Realm** is “Metro-Client”. A *realm* is a name that tells the user which set of usernames and passwords this authentication request refers to. Here, the particular server has a set of usernames and passwords for clients of the machine Metro. In a large organization, there might be different Web servers in departments and sub-departments, and the realms might be named after these subdivisions; e.g. a realm “Finance” might indicate that to access this web page you must give a username from the list that’s specific to the finance department Web servers can tie in their user authentication with other mechanisms, such as Windows domains (Chapter 20) or RADIUS (Module 27.8).

- 3. the browser realizes the error message means authentication is required. Instead of displaying an error message, it displays the authentication dialog (Figure 14.20), which includes the realm so the user knows which of their many usernames and passwords to use
- 4. the user enters the username and password, which are read by the browser. The browser then re-issues the request for the page to the server, but includes an extra header, **Authorization:**, which contains the authentication information the user typed, and the type of authentication being used. In our example, as shown in Figure 14.21, the authentication type is **Basic**, as requested by the server, and the information following is the username and password, separated by a colon, all converted to base64 encoding.
    (See the Notes for how to un-encode base64 data.)

![](img/a2132b646d336d5f9a21102d6320e537_416_0.png)

![](img/a2132b646d336d5f9a21102d6320e537_416_1.png)

- 5. if the authentication is successful, the server returns the requested page; otherwise it returns the 401 Unauthorized status code again. The browser re-issues the authentication dialog, and the cycle is repeated. After a certain number of failures (usually three) the browser gives up and displays the error page returned in the 401 Unauthorized response (Figure 14.22).

If the user requests other protected pages in the same “realm,” the browser retrieves it without asking you to authenticate. It appears that you have “logged on” to the Web server and that it knows who you are. However, this is *not* the case at all — the server doesn’t handle “logins” or maintain state information. What’s happening is much simpler: the client is including the Authorization: header in *every* request it sends for URLs that begin with the same path as the one that first caused the server to demand authentication.

```text
T 192.0.2.22:1927 -> 192.0.2.29:80 [AP]
GET /ours/treasure-map.gif HTTP/1.1  Accept: application/vnd.ms-excel,
application/msword, application/vnd.ms-powerpoint, image/gif, image/x
-xbitmap, image/jpeg, image/pjpeg, */*  Accept-Language: en-gb  Accept
-Encoding gzip, deflate  User-Agent: Mozilla/4.0 (compatible, MSIE 5.
5, Windows NT 4.0)  Host: mail. Connection: Keep-Alive. Authorization:
Basic btGVcG9sZDpb69vbXMK
```

Figure 14.21 tcpdump trace of Basic authentication showing Base64 – encoded password

![](img/a2132b646d336d5f9a21102d6320e537_416_2.png)

Figure 14.22 Error displayed by browser when authorisation fails

## 14.18 Miscellaneous Web topics

### HTTPS and SSL

SSL (*Secure Sockets Layer*) is an encryption system that runs over TCP. HTTPS is HTTP secured by SSL; its well-known port is 443, and its protocol scheme in a URL is https. SSL uses public-key encryption (see Notes) for the client to verify that the server it's connecting to really is who it says it is, using a *digital certificate*. Once the client and server are conversing, they exchange a *secret*, i.e. a *secret key*, that they then use to encrypt further communications using symmetric-key encryption. The reason for this two-phase operation is that public-key encryption uses very large keys, which are very CPU-intensive, so this is used only for the preliminary phase. Once the secret has been exchanged, symmetric encryption is used because it's very much faster, and is suitable for encrypting large data transfers.

### Retrieving Web pages automatically

In Module 14.2 we explained that a browser doesn't have to be a graphical program and that there are several non-graphical browsers. Because these run from the command-line, you can use them non-interactively in a script, to retrieve and store pages, e.g. to search them for particular content, or use them as a local copy of a Web site (assuming that you're not breaching someone's copyright), etc.

The lynx character-terminal browser has a “-dump” option – retrieve the specified page, print it on the standard output, and then exit. For example, to capture a specific image file from a site and save it locally, you could use something like

```bash
lynx -dump http://www.sun.com/pics/sunlogo.gif > stolen.gif
```

wget is a non-interactive “browser” or program to retrieve pages. It is available for Linux and other versions of UNIX. It lets you retrieve individual pages, or recursively retrieve whole sites or directories.

We use wget in a script that is run automatically twice a week to retrieve the national lottery results and see if we are now fantastically rich:

```bash
lynx -dump "http://lottery.merseyworld.com/" > /tmp/lot
/usr/local/bin/extract-lottery-result.pl < /tmp/lot > /tmp/result
mailx -s 'lottery result' fred@example.com < /tmp/result
```

We use another script that runs every five minutes to retrieve pages from our important Web servers, to make sure they are up and running; if the retrieve fails, the script mails an alert to the administrators. This is much better than just pinging the server since ping will respond even when the machine is in a half-crashed state. Below is an extract from a wget session retrieving a whole sub-tree of a Web site. In this case we want to get the Linux “SSL Certificates HowTo” which consists of many separate Web pages. We give wget the URL of the main document, and then specify option “-r” (recursive). wget then retrieves this document and all the links within it. (wget has extra options to prevent it following links to other sites, or links higher up within this site, etc.)
