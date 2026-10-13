Use the ErrorDocument directive to customize the error response for a particular error condition. This directive can be used multiple times, to specify a response for each different error code that the server generates. Common error codes used by the Web server are shown in Table 33.5.

**TABLE 33-5  COMMON HTTP ERROR CODES**

| Error Code | Summary | Meaning |
|---|---|---|
| 400 | Bad Request | The request from the client was malformed. |
| 401 | Unauthorized | Client must provide a name and password to access the item. Note that the error response for this code cannot be customized because the client automatically displays a login prompt (and not the returned page) when it receives this error from the server. |
| 402 | Payment Required | Access to the requested item requires that the client provide some kind of payment. |
| 403 | Forbidden | Client is not allowed to access the item. Providing a name and password does not help. |
| 404 | Not Found | The server did not find a document or directory matching the URL submitted by the client. |
| 500 | Fatal Error | The server encountered some unresolvable condition and could not fulfill the request. |
| 501 | Not Implemented | The server does not support the requested functionality. |
| 502 | Temporary Overload | The server cannot service the request because of high load. It can possibly service the request at a later time. |

The error document can be specified in several ways. First, you can specify just a string to return to the user as the value for the ErrorDocument. You can also refer to a local file to return a static error page, or to a CGI script to generate one at the time of the request. Using a CGI script enables you to customize the response to exactly match your situation because the script can examine information about the client, its request, and the local filesystem at the time that the request is made. Finally, you can also specify an external document as an error response.

For each ErrorDocument directive, specify the error code, and then the item with which you want the server to respond for that error. Following are some examples of ErrorDocument lines:

```
ErrorDocument 400 "Hey, you sent invalid request."
ErrorDocument 402 http://www.example.com/pay_me.html
ErrorDocument 500 /fatal.html
ErrorDocument 404 /cgi-bin/missing.pl
```

# ## CONFIGURING SETTINGS ON A PER DIRECTORY BASIS

When you use the configuration directives for controlling file information, directory indexing, error responses, and authorization (discussed later) in httpd.conf, they apply to the entire document tree that the Web server provides. However, you can also apply these directives to specific directories and files on your system.