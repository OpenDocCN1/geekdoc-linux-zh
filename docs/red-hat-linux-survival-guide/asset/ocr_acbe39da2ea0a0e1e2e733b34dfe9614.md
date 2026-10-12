| % Specifier | Description |
|---|---|
| `%{ OutgoingHeader }o` | The contents of OutgoingHeader; that is, the header line(s) in the reply. The o character at the end denotes that this is a server (outgoing) header. |
| `%p` | The port to which the request was served. |
| `%P` | The process ID of the child that serviced the request. |
| `%q` | The query string. |
| `%r` | The first line of the request. |
| `%s` | Status returned by the server in response to the request. Note that when the request gets redirected, the value of this format specifier is still the original request status. If you want to store the redirected request status, use `%...`>s instead. |
| `%t` | Time of the request. The format of time is the same as in CLF format. |
| `%{format}t` | The time, in the form given by format. You can also look at the man page for the `strftime` function. |
| `%T` | The time taken to serve the request, in seconds. |
| `%u` | If the requested URL required a successful Basic HTTP authentication, then the user name is the value of this format specifier. The value may be bogus if the server returned a 401 status (Authentication Required) after the authentication attempt. |
| `%U` | The URL path requested. |
| `%v` | The name of the server or the virtual host to which the request came. |
| `%V` | The server name per the UseCanonicalName directive. |

It is possible to include conditional information in each of the preceding specifiers. The conditions can be the presence (or absence) of certain HTTP status code(s). For example, say that you want to log all referring URLs that pointed a user to a nonexistent page. In such a case, the server produces a 404 status (Not Found) header. So, to log the referring URLs, you can use the format specifier:

```
'$404{Referer}i'
```

Similarly, to log referring URLs that resulted in an unusual status, you can use the following specifier:

```
'$!200,304,302{Referer}i'
```