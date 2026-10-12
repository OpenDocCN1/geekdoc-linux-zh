
## Note

Some people tend to confuse HTTP and HTML. Keep in mind that the Hypertext Markup Language (HTML) is the format that web pages are written in, while HTTP is the transfer protocol for moving those pages (among other things) from the server to your browser.

### Headers

When a web client connects to a web server, the client's default method of making this connection is to contact the server's TCP port 80. Once connected, the web server says nothing; it's up to the client to issue HTTP-compliant commands for its requests to the server. Along with each command comes a *request header*, which includes information about the client. For example, when using Mozilla under Linux as a client, a web server will receive the following information from a client:

```
GET / HTTP/1.1
Host: localhost:80
User-Agent: Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.0.0) Gecko/20020809
Accept:
  text/xml,application/xml,application/xhtml+xml,text/html;q=0.9,text/plain;q=0.8,
  video/x-mng,image/png,image/jpeg,image/gif;q=0.2,text/css,*/*;q=0.1
Accept-Encoding: gzip, deflate, compress;q=0.9
Accept-Charset: ISO-8859-1, utf-8;q=0.66, *;q=0.66
Keep-Alive: 300
Connection: keep-alive
```

The first line contains the HTTP **GET** command, which asks the server to fetch a file. The remainder of the information is a collection of key: value pairs that make up the header. This tells the server about the client, the kind of file formats the client will accept, and so forth. Many servers use this information for logging purposes, as well as to determine what can and cannot be sent to the client.

Along with the request header, additional headers may be sent. For example, when a client uses a hyperlink to get to the server site, a header entry showing the client's originating site will also appear in the header.

When it receives a blank line, the server knows a request header is complete. Once the request header is received, it responds with the actual requested content, prefixed by a server header. The server header tells the client information about the server, the amount of data the client is about to receive, and the type of data coming in. For example, when sent to a default installation of the Apache HTTP server under Red Hat 8, the request header shown in the preceding code listing results in the following server response header.

```
HTTP/1.1 200 OK
Date: Mon, 28 Oct 2002 12:59:42 GMT
Server: Apache/2.0.40 (Red Hat Linux)
Last-Modified: Sat, 07 Sep 2002 12:17:54 GMT
ETag: "16411d-20-c571d380"
Accept-Ranges: bytes
Content-Length: 33
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: text/html; charset=ISO-8859-1
```

The response header is followed by a blank line and then the actual content of the transmission.

### Nonstandard Ports

The default port for HTTP requests is port 80, but you can also configure a web server to use a different (arbitrarily chosen) port that is not in use by another service. This allows sites to run multiple web servers on the same host, each server on a different port. Some sites use this arrangement for multiple configurations of their web servers, to support various types of client requests.

When a site runs a web server on a nonstandard port, you can see that port number in the site’s uniform resource locator (URL). For example, this address,

```
http://www.redhat.com/
```

with an added port number, would read

```
http://www.redhat.com:80/
```

> **CAUTION**
> Don’t make the mistake of going for “security through obscurity.” If your server’s on a nonstandard port, that doesn’t guarantee that Internet troublemakers won’t find your site. Because of the automated nature of tools used to attack a site, it takes fewer than 100 lines of C code to scan a server and find which ports are running web servers. Using a nonstandard port does not keep your site “secure.”

### Process Ownership and Security

As discussed in other modules, running a web server under UNIX means that you get to deal with the Linux (and UNIX in general) model. In terms of permissions, that means each process has an owner, and that owner has limited rights on the system.

Whenever a program (process) is started, it inherits the permissions of its parent process. For example, if you're logged in as root, the shell in which you're doing all your work has all the same rights as the root user. In addition, any process you start from this shell will inherit all the permissions of that root. Processes may give up rights, but they cannot gain rights.

> **NOTE**
> There is an exception to the Linux inheritance principle: Programs configured with the SetUID bit (see the **chmod** command in Module 6) do not inherit rights from their parent process, rather, they start with the rights specified by the owner of the file itself. For example, the file containing the program **su** (/bin/su) is owned by root and has the SetUID bit set. If the user **michael** runs the program **su**, that program doesn't inherit the rights of **michael** but instead will start with the rights of root.

### How Apache Processes Ownership

To perform network setups, the Apache HTTP server must start with root permissions. Specifically, it needs to bind itself to port 80 so that it can listen for requests and accept connections, and only root can take control of low numbered ports. Once it does this, Apache can give up its rights and run as a nonroot user, as specified in its configuration files. Although, many implementations select the user "nobody" for this purpose, Red Hat has created a special user and group, both named "apache," just for this role.

Running as user **apache**, the Apache **httpd** server can read only the files that user **apache** has permission to read. Thus, if a file's permissions are set so that they are readable only by the file's owner, the owner must be **apache**. For any file that you want available to user **apache** but don't want to change its ownership, set that file's permission to world readable:

```
chmod a+r filename
```

where *filename* is the name of the file.

Security is especially important for sites that use CGI scripts. By limiting the permissions of the web server, you decrease the likelihood that someone can send a malicious request to the server. And the server processes and corresponding CGI scripts can break only what they can access. As user **apache**, the scripts and processes don't have access to the same key files that root can access. (Remember that root can access everything, no matter what the permissions.)

> **CAUTION**
> In dealing with CGI scripts, most successful attacks on sites are typically possible because of improperly configured web servers or poorly written CGI scripts.

### Ask the Expert

**Q:** If I do have CGI scripts on my server, what precautions should I take to make them more secure?

**A:** In the event that you decide to allow CGI scripts on your server, pay strict attention to how they are written. Be sure it isn’t possible for input coming in over the network to make the CGI script do something it shouldn’t.

### Progress Check

- 1. What special user and group name does Red Hat use for running apache?
- 2. Why is security for root important?

## 12.2 Setting Up the Apache HTTP Server

Installing Apache HTTP Server can be as simple as selecting the Web Server option when installing your system. If you’re adding Apache by hand, the packages you’re most interested in are **httpd**, and optionally **httpd-manual** and **redhat-config-httpd**. Merely installing the base packages will give you basic web-serving capabilities, but you’ve barely scratched the surface of Apache’s capabilities.

### Changes in Apache 2

Red Hat 8 includes Apache version 2 which introduces many changes from the long standing 1.3 series. If you’re familiar with past versions of Apache, you should at least browse through the differences in the newer version. Some of the highlights of Apache 2 include:

| Feature | Description |
|---|---|
| POSIX threading | A hybrid setup that uses multiple threads as well as multiple processes to improve scalability for some configurations. |
| Multi-Processing Module | A new mechanism for taking advantage of the native capabilities of whichever platform the server is running on. |

- 1. To run apache, Red Hat uses the user and group name “apache.”
- 2. The security for root is important because root can access any and all files no matter what permissions are set on those files.
