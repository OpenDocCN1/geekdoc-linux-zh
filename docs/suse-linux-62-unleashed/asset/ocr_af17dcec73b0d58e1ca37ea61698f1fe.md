# Apache Server CHAPTER 11

# 11

%P
The process ID of the child that serviced the request.

%r
First line of request.

%s
Status. For requests that were internally redirected, this is status of the original request—%>s for the last.

%t
Time, in common log time format.

%{format}t
The time, in the form given by format, which should be in str(t).

%T
The time taken to serve the request, in seconds.

%u
Remote user from auth; may be bogus if return status (%) is 401.

%U
The URL path requested.

%v
The canonical ServerName of the server serving the request.

In each variable, you can put a conditional in front of the variable that will determine whether the variable is displayed. If it is not displayed, - will be displayed instead. These conditionals are in the form of a list of numerical return values. For example, %401u will display the value of REMOTE_USER unless the return code is 401.

You can then specify the location and format of a log file using the CustomLog directive:

```
CustomLog logs/access_log common
```

If it is not specified as an absolute path, the location of the log file is assumed to be relative to the ServerRoot.

# CGI and SSI

The most common way to provide dynamic content on Web sites is with CGI (Common Gateway Interface) programs. The CGI is a specification of communication between server processes (such as programs that generate dynamic documents) and the server itself. SSI allow output from CGI programs, or other programs, to be inserted into existing HTML pages.

# CGI

By default, you may put any CGI program in the ScriptAlias directory on your server. These programs must be executable by the user as the server is running. This usually means that you will need to change the mode of the file to 755 so that the user www can execute them.

```
chmod 755 program.cgi
```