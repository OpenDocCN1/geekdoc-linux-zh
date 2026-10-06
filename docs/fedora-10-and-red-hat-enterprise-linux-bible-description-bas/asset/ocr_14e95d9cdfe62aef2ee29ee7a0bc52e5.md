# Part IV: Fedora and RHEL Network and Server Setup

| Response Code | Meaning |
|---|---|
| 404 Not Found | The requested page does not exist on the server. |
| 500 Internal Server Error | Usually encountered when running a CGI program, this response indicates that the program or script contains invalid code or was given input that it cannot handle. |
| 501 Not Implemented | The requested method (for example, GET, POST, PUT, DELETE, HEAD) is not understood by the server. |
| 502 Bad Gateway | With the Web server acting as a proxy server, an error was encountered when trying to fulfill the request to an external host. |
| 503 Service Unavailable | The server is currently processing many requests. |
| 505 HTTP Version Not Supported | The requested version (for example, HTTP/1.0, HTTP/1.1) is not understood by the server. |

To make easier to customize error messages and standardize how these messages are presented, the latest version of Apache includes what are referred to as variant pages (ending in a .var suffix). These variant pages, which offer output based on language, are stored in the /var/www//error directory.

Alias /error/ /var/www//error/*

```
<IfModule mod_negotiation.c>
<IfModule mod_include.c>
  <Directory "/var/www//error">
    AllowOverride None
    Options IncludesNoExec
    AddOutputFilter Includes html
    AddHandler type-map
    Order allow deny
    Allow from all
    LanguagePriority es de fr
    ForceLanguagePriority Prefer Fallback
  </Directory>

ErrorDocument 400 /error/HTTP_BAD_REQUEST.html
ErrorDocument 401 /error/HTTP_UNAUTHORIZED.html
ErrorDocument 403 /error/HTTP_FORBIDDEN.html
ErrorDocument 404 /error/HTTP_NOT_FOUND.html
ErrorDocument 405 /error/HTTP_METHOD_NOT_ALLOWED.html
```

The ErrorDocument directive associates a particular error code number with a particular .var file that contains multiple possible responses based on language.