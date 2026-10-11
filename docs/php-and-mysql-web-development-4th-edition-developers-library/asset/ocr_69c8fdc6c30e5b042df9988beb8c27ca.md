# 12.3 Controlling How the Server Listens for Connections

the tables, you can change the root password with SET PASSWORD or UPDATE, as shown in Section 12.1, “Securing a New MySQL Installation.” For example:

```
mysql> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('rootpass');
```

Be sure to change the password for all root accounts if there is more than one.

+   3. After changing the root password, shut down the server and restart it using your normal startup procedure. You now should be able to connect to it as root using the new password.

Should you be forced to terminate the server with kill -9 under Unix or with the Task Manager under Windows, the abrupt nature of the shutdown gives the server no chance to flush any unsaved changes to disk. To help deal with problems that may occur due to this kind of shutdown, it’s a good idea to enable auto-recovery in the server. For details, see Section 14.2.1, “Using the Server’s Auto-Recovery Capabilities.”

# 12.3 Controlling How the Server Listens for Connections

The MySQL server listens for connections on several network interfaces, which you can control as follows:

+   ■ On all platforms, the server listens on a network port for TCP/IP connections, unless started with the --skip-networking option. The default port number is 3306; to specify a different number, use the --port option. If the server host has more than one IP number, you can specify which one the server should use when listening for connections by starting it with a --bind-address option.

+   ■ Under Unix, the server listens on a Unix domain socket file for connections from local clients that connect to the special hostname localhost or that specify the --protocol=socket option. Use of the socket file by the server cannot be turned off. The default socket file usually is /tmp/mysql.sock, although operating system distributions that include MySQL often use a different location. To specify a socket file pathname explicitly, use the --socket option.

+   ■ For Windows servers that include support for named pipes, named-pipe connections are disabled by default. To enable this capability, start the server with the --enable-named-pipe option. This enables local clients to connect through the named pipe by specifying the --protocol=pipe option or by connecting to the special hostname ‘..’ (period). By default, the pipe name is MySQL (not case sensitive). To specify a different name, use the --socket option.

+   ■ MySQL supports shared-memory connections on Windows, but this capability is disabled by default. To enable it, start the server with the --shared-memory option. When enabled, it becomes the default connection protocol for local clients. Local clients also can use the --protocol=memory option to specify use of shared memory