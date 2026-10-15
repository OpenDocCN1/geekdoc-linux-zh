
| Directive | Description |
|---|---|
| AllowFilter regular-expression | Allows the configuration of a regular expression that must be matched for all commands sent to ProFTPD. |
| AllowUser user-expression | Users allowed access. |
| <Anonymous root-directory> | Creates an anonymous FTP login, terminated by a matching </Anonymous> directive. The root directory parameter is the directory proftpd first moves to and then chroot to, hiding the rest of the file system. |
| Bind address | Allows additional IP addresses to be bound to a main or VirtualHost configuration. Multiple Bind directives can be used to bind multiple addresses. |
| DefaultRoot directory [group-expression] | Default root directory assigned to user on login. The group-expression argument restricts the DefaultRoot directive to a group or set of groups. Default: DefaultRoot / |
| Deny ["from"] "all"/"none"/host/network [,host/network[...]] | List of hosts and networks explicitly denied access to a given <Limit> context block. all indicates all hosts are denied access, and none indicates no hosts are explicitly denied. |
| DenyAll | Denies access to a directory, anonymous FTP, or Limit block. |
| DenyFilter regular-expression | Specifies a regular expression, which must not match any command. |
| DenyUser user-expression | Users denied access within a Limit block. |
| <Directory pathname> | Directory-specific configuration. Used to create a block of directives that apply to the specified directory and its subdirectories. |
| DisplayLogin filename | Specifies the text file displayed to a user who logs in. |
| <Global> | Global configuration block |
| <Limit command/command-group [command2...]> | Access restrictions on FTP commands, within a given context. The command-group refers to groupings of commands as defined in the ProFTPD documentation. |
| LsDefaultOptions "options string" | Default options for directory listings (as in the ls command). |
| MasqueradeAddress host | Specifies public host name for FTP server. Used for FTP servers masqueraded by NAT tables (packet filtering). See Chapter 19. |
| MaxClients number/none message | Maximum number of connected clients allowed. The message specified is displayed when a client is refused connection. |
| MaxLoginAttempts number | Maximum number of times a client may attempt to log in to the server during a given connection. |
| Order allow, deny / deny, allow | Configures the order that Allow and Deny directives are checked inside a <Limit> block. Default: Order allow,deny Context: <Limit> |
| PersistentPasswd on | off | When on, proftpd during login, opens the system-wide /etc/passwd, /etc/group files, accessing them even during a chroot operation that changes the root directory. |
| ServerAdmin "admin-email-address" | E-mail address of the server or virtual host administrator. |
| ServerType type-identifier | The server daemon's operating mode, either inetd or standalone. |
| TimeoutIdle seconds | Maximum number of seconds proftpd allows clients to stay connected without any activity. Default: TimeoutIdle 600 |
| Umask octal-mask | Permissions applied to newly created file and directory within a given context. |
| User userid | The user the proftpd daemon runs as. |
| UserAlias login-user userid | Maps a login name used by a client to a user ID on the server. A client logging in as login-user is actually logged in as user ID. Often used inside an <Anonymous> block to allow specified login-names to perform an anonymous login. |
| <VirtualHost address> | Configuration directives that apply to a particular hostname or IP address. Often used with virtual servers that run on the same physical machine. The block is terminated with a </VirtualHost> directive. |

## The Washington University FTP Daemon: WU-FTPD

The Washington University FTP server, though widely used, is no longer included with Red Hat 9 and up. The name of the Washington University FTP daemon is wu-ftpd; it must be running to allow FTP access by remote users. As with other servers, you can start the FTP server at boot time, through xinetd when a request is received, or directly from the command line. By default, the wu-ftpd server is installed to run using xinetd. The use of xinetd for the servers is described in detail in Chapter 20. The command name for the FTP server invoked
