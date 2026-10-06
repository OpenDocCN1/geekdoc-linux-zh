# The Apache Web Server 501

+   - Section 2, the main server configuration
- Section 3, virtual host configurations

The directives included in Section 1 affect the operation of the server as a whole, including the main configuration and all virtual host configurations. Directives in Section 2 affect only the main server configuration. Directives in Section 3, if present, affect only the virtual host configuration to which pertain. The next subsections examine the `httpd.conf` file and its directives more closely.

# Section 1: The Global Environment

+   - The type of configuration: stand-alone or `inetd` (generally stand-alone)
- The names and locations of available Apache Modules
- The number of server processes to start and the minimum and maximum number to maintain

Unless you want to operate the server in `inetd` mode, install custom modules, or modify the number of server processes, you may not need to modify the directives in Section 1. You can consult the Apache online documentation at www.apache.org for help for understanding unclear directives.

# Section 2: The Main Configuration

Section 2 of the `httpd.conf` file contains directives that affect the operation of only the main configuration of the server; the directives do not affect the operation of virtual hosts, if any are configured. Primary configuration items include:

+   - The host name of the server
- The port number on which the server listens (generally 80)
- The user and group IDs under which the daemon runs (generally `nobody`)
- The type of logging desired: logging by IP address or host name (generally logging by IP address, which is more efficient)
- The location of the root directory (generally `/home/httpd/html`)
- The name of users' HTML subdirectories (generally `~/public_html` or `~/www`)
- The path where CGI scripts reside

Copyright©2000 SYBEX, Inc., Alameda, CA www.sybex.com