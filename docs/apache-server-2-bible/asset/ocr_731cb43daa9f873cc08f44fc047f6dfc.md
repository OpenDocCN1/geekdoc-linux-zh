in this variable for the CGI program. The CGI program, however, will have no way of identifying the password used to access it. If this variable is set to a username, the CGI program can safely assume that the user supplied the appropriate password to access it.

# SERVER_PROTOCOL

SERVER_PROTOCOL is the protocol and version number the client used to send the request for the CGI program:

```
SERVER_PROTOCOL = HTTP/1.1
```

# REQUEST_METHOD

The REQUEST_METHOD variable is set to the HTTP request method used by the client to request the CGI program. The typical values are: GET, POST, and HEAD.

```
REQUEST_METHOD=GET
```

The input is stored in the QUERY_STRING variable when the request method is GET. When the method is POST, the input is stored in the STDIN of the CGI program.

# REQUEST_URI

The REQUEST_URI variable is set to the URI of the request.

```
REQUEST_URI = /cgi-bin/printenv2
```

# REMOTE_IDENT

REMOTE_IDENT will only be set if the IdentityCheck directive is set. This variable stores the user identification information returned by the remote identd (identification daemon). Because many systems do not run this type of daemon process, REMOTE_IDENT should not be considered a reliable means for identifying users. I recommend using this variable in an intranet or an extranet environment in which you or your organization is running an identd server.

# AUTH_TYPE

If a CGI program is stored in a section of the Web site where authentication is required to gain access, this variable is set to specify the authentication method used.

# CONTENT_TYPE

This variable specifies the MIME type of any data attached to the request header. For example:

```
CONTENT_TYPE = application/x-www-form-urlencoded
```