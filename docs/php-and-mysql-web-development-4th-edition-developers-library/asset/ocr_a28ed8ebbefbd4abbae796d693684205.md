+   -host=host_name, -h host_name

This option is used only by client programs. It indicates the host to connect to (that is, the host where the server is running). The default value is `localhost`.

+   --password={pass_val}, -p[pass_val]

This option is used only by client programs. It indicates the password to use when connecting to the server. If you specify no pass_val after the option name, the program asks you to enter a password. If you do specify pass_val after -p, it must immediately follow the option letter with no space in between. In other words, the short form must be given as -ppass_val, not as -p pass_val.

+   -pPipe, -W

Specifies use of a named pipe to connect to the server. This option is used only for client programs running under Windows, and only for connecting to Windows servers that have named-pipe support enabled.

+   --port=port_num, -P port_num

For `mysqld`, this option specifies the port on which to listen for TCP/IP connections. The default port number is 3306. For client programs, this is the port number to use when connecting to the server via TCP/IP.

+   --protocol=protocol_type

This option is used only by client programs. It indicates what type of connection to make to the server. The protocol_type value can be tcp (use TCP/IP), socket (use a Unix socket file), pipe (use a Windows named pipe), or memory (use shared memory). The value is not case sensitive.

Some connection types are platform specific or usable only to connect to a local server running on the same host as the client program:

+   - Socket, named-pipe, and shared-memory connections can be used only for connecting to a local server.
+   
+   - Socket connections can be used only on Unix.
+   
+   - Named-pipe and shared-memory connections can be used only on Windows.
+   
+   - TCP/IP connections can be used on any platform and can be used to connect to local or remote servers.

The --protocol option can be used in conjunction with other options that provide information about how to connect to the server:

+   - For TCP/IP connections, you can use the --host and --port options to specify the hostname and TCP/IP port number.
+   
+   - For socket and named-pipe connections, you can use the --socket option to specify the Unix socket filename on Unix or the named-pipe name on Windows.
+   
+   - For shared-memory connections, you can use the --shared-memory-base-name option to specify the shared-memory name.