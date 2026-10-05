# FastCGI

Last-Modified: Sat, 01 Aug 2009 16:20:22 GMT
Content-Length: 7044
Content-Type: text/html

```
<contents of your default file appear here>
Connection closed by foreign host.
```

In this case, the told server we were going to speak HTTP protocol version 1.1 and named the virtual host from which we were requesting information. The server returned a status code (HTTP/1.1 200 OK), its idea of the current date and time, name and version of the server software it was running, the date that the requested file was last modified, the length of the requested file, and the requested file's content type. The header information is separated from the content by a blank line.

# Content generation on the fly

In addition to serving static documents, an HTTP server can provide the user with content that has been created on the fly. For example, if you wanted to provide the current time and temperature to users visiting your site, you might the HTTP server execute a script to obtain this information. This amazing-trick is often accomplished with the Common Gateway Interface, or CGI.

CGI is not a programming language but rather a specification by which an HTTP server exchanges information with other programs. CGI scripts are most often written in Perl, Python, or PHP. But really, any programming language that can perform real-time I/O is acceptable.

# Embedded interpreters

The CGI model provides complete flexibility in that the web developer is free to use any interpreter or scripting language. Unfortunately, starting a separate process for every script can be a performance nightmare on web servers that serve a significant amount of dynamic content.

In addition to supporting external CGI scripts, web servers define a plug-in architecture that allows script interpreters as Perl and PHP to be embedded within the web server itself. This bundling significantly increases performance because the web server no longer needs to fork a separate process to deal with each request. The architecture is largely invisible to script developers. Whenever the server sees a file ending in a specified extension (such as .pl or .php), it sends the contents of the file to the embedded interpreter to be executed. Table 23.2 on the next page lists some common embedded interpreters that run inside Apache.

# FastCGI

Another trick to use in some systems is FastCGI (fastcgi.com). This module improves the performance of scripts by starting them once and leaving them running to service multiple requests. This arrangement amortizes the cost

![](bbox=[0.943, 0.381, 0.986, 0.503])