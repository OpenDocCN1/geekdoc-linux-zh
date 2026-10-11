**ftp_data_port** With **connect_from_port_20** set to **NO**, specifies the port that **vsftpd** uses for PORT connections.
Default: 20

# TIMEOUTS

**accept_timeout** The number of seconds the server waits for a client to establish a PASV data connection.
Default: 60

**connect_timeout** The number of seconds the server waits for a client to respond to a PORT data connection.
Default: 60

**data_connection_timeout**
The number of seconds the server waits for a stalled data transfer to resume before disconnecting.
Default: 300

**idle_session_timeout**
The number of seconds the server waits between FTP commands before disconnecting.
Default: 300

**local_max_rate** For local users, the maximum data transfer rate in bytes per second. Zero (0) indicates no limit.
Default: 0

**anon_max_rate** For anonymous users, the maximum data transfer rate in bytes per second. Zero indicates no limit.
Default: 0

**one_process_model** **YES** establishes one process per connection, which improves performance but degrades security. **NO** allows multiple processes per connection. **NO** is recommended for a more secure system.
Default: **NO**

# MISCELLANEOUS

This section describes parameters not discussed elsewhere.

**pam_service_name**
The name of the PAM service used by **vsftpd**.
Default: **ftp**
Fedora/RHEL: **vsftpd**

**tcp_wrappers** **YES** causes incoming connections to use **tcp_wrappers** (page 447) if **vsftpd** was compiled with **tcp_wrappers** support. When **tcp_wrappers** sets the environment