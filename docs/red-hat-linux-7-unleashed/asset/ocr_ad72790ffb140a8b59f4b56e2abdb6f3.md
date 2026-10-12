| Variable | Description |
| :--- | :--- |
| `%{HEADER}o` | The contents of *HEADER*, header line(s) in the reply. |
| `%p` | The canonical port of the server serving the request. |
| `%P` | The process ID of the child that serviced the request. |
| `%q` | The contents of the query string, prepended with a `?` character. If there is no query string this will evaluate to an empty string. |
| `%r` | First line of request. |
| `%s` | Status. For requests that were internally redirected, this is the status of the *original request*—`%s` for the last. |
| `%t` | Time, in common log format time format. |
| `%{format}t` | The time, in the form given by *format*, which should be in strftime(3) format. See the section “Basic SSI Directives” for a complete list of available formatting options. |
| `%T` | The time taken to serve the request, in seconds. |
| `%u` | Remote user from *auth*; may be bogus if return status (`%s`) is 401. |
| `%U` | The URL path requested. |
| `%v` | The server name according to the `UseCanonicalName` directive. |
| `%V` | The canonical `ServerName` of the server serving the request. |

In each variable, you can put a conditional in front of the variable that will determine whether the variable is displayed. If it is not displayed, `-` will be displayed instead. These conditionals are in the form of a list of numerical return values. For example, `%{401}u` will display the value of `REMOTE_USER` unless the return code is 401.

You can then specify the location and format of a log file using the `CustomLog` directive:

`CustomLog logs/access_log common`

If it is not specified as an absolute path, the location of the log file is assumed to be relative to the `ServerRoot`.

# ## Dynamic Content

The most common way to provide dynamic content on Web sites is with CGI (Common Gateway Interface) programs. The CGI is a specification of communication between server processes (such as programs that generate dynamic documents) and the server itself. Server-Side Includes (SSIs) allow output from CGI programs, or other programs, to be inserted into existing HTML pages.