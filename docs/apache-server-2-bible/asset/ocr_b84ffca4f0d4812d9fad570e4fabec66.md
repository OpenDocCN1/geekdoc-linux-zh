Notice that the entire message is quoted, and the server replaces $s with whatever information is available regarding the error. If you find this a bit limiting, however, you can use a file as your error message response. For example:

```
ErrorDocument 404 /errors/404.html
```

Whenever the missing file error occurs, the 404.html file found in the errors directory under the DocumentRoot directory is returned to the client (the Web browser).

If you want to do more than just return a static page, you can use a CGI script to perform some specific action. In such a case, you replace the filename with a call to your CGI script:

```
ErrorDocument 404 /cgi-bin/missingurl.cgi
```

This calls a CGI script called missingurl.cgi every time a 404 error occurs. You can also redirect the client to another site using a URL instead of a filename:

```
ErrorDocument 404 http://www.newsite.com/we.moved.html
```

This can be used when a page or an entire site has moved to another location.

You cannot point the client to a remote server if an error 401 (unauthorized) occurs. The value of this directive must be a local file or a message.

# <IfDefine>

The IfDefine container directive enables you to create a conditional configuration. The special_command_line_param option is specified by using the -D option with the httpd program.

Syntax: <IfDefine [!]special_command_line_param> ... </IfDefine>

Default setting: None

Context: All

For example, if you run the Apache server from the bin directory as ./httpd -D something then you can use:

```
<IfDefine something>
# #directives that should be executed only when
# -D something is specified
</IfDefine>
```

Placing a ! character in front of the special_command_line_param tells Apache to process the directives within the IfDefine container only when a -D something was not found in the command-line. For example:

```
<IfDefine !something>
# directives that should be executed only when
# -D something is NOT specified
</IfDefine>
```