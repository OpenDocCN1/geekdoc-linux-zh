# ## 14.17 Security – authentication

Web servers can “protect” specific pages or directories, so that when they are requested, the user has to authenticate in some way, e.g. enter a username and password. Internally, the server maintains a list of protected pages and how users must authenticate themselves to gain access; these details are usually specified in the server’s configuration files. A typical conversation is as follows:

+   1. the client requests a protected page, *ours/treasure-map.gif* from the server
+   2. the server sends back a 401 “Unauthorized” error status line, with a **WWW-Authenticate**: header saying what type of authentication is required, and usually a page containing the error message to be displayed to the user if the authentication isn’t successful. Below is an **ngrep** trace of a request and response:

```
T 192.0.2.22:1926 --> 192.0.2.29:80 [AP]
GET /ours/treasure-map.gif HTTP/1.1. Accept: application/vnd.ms-excel,
application/msword. application/vnd.ms-powerpoint. image/gif, image/x
-xbitmap, image/jpeg, image/jpgpeg. */*. Accept-Language: en-gb. Accept
-Encoding: gzip, deflate. User-Agent: Mozilla/4.0 (Compatible; MSIE 5.
5; Windows NT 4.0). Host: mail. Connection: Keep-Alive....
##
T 192.0.2.29:80 --> 192.0.2.22:1926 [AP]
HTTP/1.0 401 Unauthorized. Date: Tue, 24 Jul 2001 14:44:23 GMT. Server
Apache/1.0.3. WWW-Authenticate: Basic realm="Metro-Client". Content
type: text/html ...<HEAD><TITLE>Authorization Required</TITLE></HEAD>
<BODY><H1>Authorization Required.</H1>. This server could not verify that you are authorized to access the document you requested. Either you supplied the wrong credentials (e. g., bad password), or your browser doesn’t understand how to supply the credentials required. <P>...</BODY>
```

The response says that the type of authentication is **Basic** (i.e. username and password) and that the **Realm** is “Metro-Client”. A *realm* is a name that tells the user which set of usernames and passwords this authentication request refers to. Here, the particular server has a set of usernames and passwords for clients of the machine Metro. In a large organization, there might be different Web servers in departments and sub-departments, and the realms might be named after these subdivisions; e.g. a realm “Finance” might indicate that to access this web page you must give a username from the list that’s specific to the finance department Web servers can tie in their user authentication with other mechanisms, such as Windows domains (Chapter 20) or RADIUS (Module 27.8).

+   3. the browser realizes the error message means authentication is required. Instead of displaying an error message, it displays the authentication dialog (Figure 14.20), which includes the realm so the user knows which of their many usernames and passwords to use
+   4. the user enters the username and password, which are read by the browser. The browser then re-issues the request for the page to the server, but includes an extra header, **Authorization:**, which contains the authentication information the user typed, and the type of authentication being used. In our example, as shown in Figure 14.21, the authentication type is **Basic**, as requested by the server, and the information following is the username and password, separated by a colon, all converted to base64 encoding.
+   (See the Notes for how to un-encode base64 data.)