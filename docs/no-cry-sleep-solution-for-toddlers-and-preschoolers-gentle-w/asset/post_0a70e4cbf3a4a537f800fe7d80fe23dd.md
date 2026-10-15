
| Directive | Description |
|---|---|
| `<IfDefine [ ]parameter-name ... </IfDefine>` | The `<IfDefine test>...</IfDefine>` section specifies conditional directives. Directives within an `IfDefine` section are processed if the test is true and are ignored otherwise. The test consists of a parameter name, which is true if the parameter is defined, and false if undefined. An `!` placed before the parameter makes the test true if the parameter is undefined (not). |
| `<IfModule [ ]module-name ... </IfModule>` | The `<IfModule test>...</IfModule>` section specifies conditional directives. The test checks to see if a module is compiled in Apache. It is true if present, and false if not. An `!` module-name is true if the module is not present. |
| Include filename | Inclusion of other configuration files. |
| KeepAlive on/off | Enables persistent connections, "Off" to disable. |
| KeepAliveTimeout seconds | The number of seconds Apache waits for another request before closing the connection. |
| Listen [IP address:]port number | Listens to more than one IP address or port. By default, it responds to requests on all IP interfaces, but only on the port given by the Port directive. Context: server config |
| ListenBacklog backlog | The maximum length of the queue of pending connections. |
| LoadFile filename filename ... | Links in the named object files or libraries when the server is started or restarted. Used to load additional code required for some module to work. |
| LoadModule module filename | Links in the object file or library filename and adds the module structure named module to the list of active modules. |
| LockFile filename | Path to the lockfile used when Apache is compiled. |
| MaxClients number | Limits the number of simultaneous requests that can be supported. Any connection attempts over the MaxClients limit are normally queued, up to a number based on the ListenBacklog directive. |
| MaxKeepAliveRequests number | Limits the number of requests allowed per connection when KeepAlive is on. |
| Port number | If no Listen or BindAddress directives exist, a port directive sets the network port on which the server listens. Ports for a virtual host are set by the VirtualHost directive. |
| ServerAdmin e-mail address | The e-mail address for the server administrator. |
| ServerAlias host1 host2 ... | Sets the alternate names for a host, for use with name-based virtual hosts. |

| Directive | Description |
|---|---|
| ServerName fully qualified domain name | Sets the hostname of the server. This is used only when creating redirection URLs. If it is not specified, the server attempts to deduce it from its own IP address. |
| ServerPath pathname | Sets the legacy URL pathname for a host, for use with name-based virtual hosts. |
| ServerRoot directory-filename | Sets the directory in which the server resides. |
| ServerSignature Off | On | EMail | Configures a trailing footer line under server-generated documents, such as error messages. |
| SetHandler handler-name | Forces all matching files to be parsed through the handler given by handler-name. |
| User unix-userid | Specifies the user ID for the server. The standalone server must be run as root initially. You can use a username or a user ID number. The user should have no access to system files. The recommendation is for you to set up a new user and group specifically for running the server. |
| UserDir directory/filename | Sets the real directory in a user's home directory to use when a request for a document for a user is received. |
| Redirect [ status ] url-path url | Maps an old URL into a new one. |
| ScoreBoardFile filename | Specifies the ScoreBoardFile file. |
| TimeOut number | Sets the timeout in seconds for receiving GET requests, receipt of POST and PUT requests, and TCP packet transmissions acknowledgments. |

## TABLE 22-4 Server Directives (continued)

Some directives require specific information about your system. For example, ServerName holds the hostname for your Web server. Specifying a hostname is important to avoid unnecessary DNS lookup failures that can hang your server. Notice the entry is commented with a preceding #. Simply remove the # and type your Web server's hostname in place of new.host.name.

```
# ServerName allows you to set a hostname which is sent
# back to clients for your server if it's different than the
# one the program would get (i.e. use
# "www" instead of the host's real name).

#ServerName new.host.name
```

On Red Hat systems, entries have already been made for the standard Web server installation using /var/www as your Web site directory. You can tailor your Web site to your own needs by changing the appropriate directives. The DocumentRoot directive determines
