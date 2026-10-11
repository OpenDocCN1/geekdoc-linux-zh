for its own name(s). Additional names for **nmbd** to respond on can be set via parameters in the smbd.conf(5) configuration file.

**nmbd** can also be used as a WINS (Windows Internet Name Server) server. What this basically means is that it will act as a WINS database server, creating a database from name registration requests that it receives and replying to queries from clients for these names.

In addition, **nmbd** can act as a WINS proxy, relaying broadcast queries from clients that do not understand how to talk the WINS protocol to a WINS server.

# OPTIONS

-D If specified, this parameter causes **nmbd** to operate as a daemon. That is, it detaches itself and runs in the background, fielding requests on the appropriate port. By default, **nmbd** will operate as a daemon if launched from a command shell. nmbd can also be operated from the inetd meta-daemon, although this is not recommended.

-F If specified, this parameter causes the main **nmbd** process to not daemonize, i.e. double-fork and disassociate with the terminal. Child processes are still created as normal to service each connection request, but the main process does not exit. This operation mode is suitable for running **nmbd** under process supervisors such as supervise and svscan from Daniel J. Bernstein’s daemon tools package, or the AIX process monitor.

-S If specified, this parameter causes **nmbd** to log to standard output rather than a file.

-i If this parameter is specified it causes the server to run "interactively", not as a daemon, even if the server is executed on the command line of a shell. Setting this parameter negates the implicit daemon mode when run from the command line. **nmbd** also logs to standard output, as if the -S parameter had been given.

-h | --help Print a summary of command line options.

-H <filename> NetBIOS lhlhosts file. The lhlhosts file is a list of NetBIOS names to IP addresses that is loaded by the nmbd server and used via the name resolution mechanism name resolve order described in smbd.conf(5) to resolve any NetBIOS name queries needed by the server. Note that the contents of this file are NOT used by **nmbd** to answer any name queries. Adding a line to this file affects name NetBIOS resolution from this host ONLY.

The default path to this file is compiled into Samba as part of the build process. Common defaults are /usr/local/samba/lib/lmhosts, /usr/samba/lib/lmhosts or /etc/samba/lmhosts. See the lmhosts(5) man page for details on the contents of this file.