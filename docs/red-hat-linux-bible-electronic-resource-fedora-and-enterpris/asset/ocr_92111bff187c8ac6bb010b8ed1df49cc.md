| Module | Description |
|---|---|
| mod_setenvif | Conditionally sets environment variables based on the contents of various HTTP header fields. |
| mod_so | The only module other than http\_core that must be statically compiled in the server, this module contains the directives necessary to implement loading dynamic shared objects. |
| mod\_speling | Attempts to automatically correct misspellings in requested URLs. |
| mod_ssl | Implements cryptography using SSL and TLS protocols. |
| mod_status | Provides a summary of the activities of each individual httpd server process, including CPU and bandwidth usage levels. |
| mod_suexec | Lets CGI scripts run with permission of particular user/group. |
| mod_unique_id | Attempts to assign a token to each client request that is unique across all server processes on all machines within a cluster. |
| mod_userdir | Specifies locations that can contain individual users' HTML documents. |
| mod\_usertrack | Uses cookies to track the progress of users through a Web site. |
| mod\_vhost\_alias | Contains support for dynamically configured mass virtual hosting. |

More information about each module (and the directives that can be defined within it) can be found on your server at http://localhost/manual/mod/.

# Setting the main server’s configuration

The second section of the http.conf file relates to directives handled by your main server. In other words, these values are used in all cases except when they are changed in virtual host definitions. To change the same directives for particular virtual hosts, add them within virtual host containers.

# Choosing the server's user and group

The httpd daemon doesn't have to run as the root user; in fact, your system is more secure if it doesn't. By setting User and Group entries, you can have the httpd daemon run using the permissions associated with a different user and group:

```
# If you wish httpd to run as a different user or group, you must run
# httpd as root initially and it will switch.
#
# User/Group: The name (or #number) of the user/group to run httpd as.
```