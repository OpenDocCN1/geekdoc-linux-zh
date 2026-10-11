Please note that there are significant security implications to running this server, and the smb.conf(5) manual page should be regarded as mandatory reading before proceeding with installation.

A session is created whenever a client requests one. Each client gets a copy of the server for each session. This copy then services all connections made by the client during that session. When all connections from its client are closed, the copy of the server for that client terminates.

The configuration file, and any files that it includes, are automatically reloaded every minute, if they change. You can force a reload by sending a SIGHUP to the server. Reloading the configuration file will not affect connections to any service that is already established. Either the user will have to disconnect from the service, or smbd killed and restarted.

# OPTIONS

**-D** If specified, this parameter causes the server to operate as a daemon. That is, it detaches itself and runs in the background, fielding requests on the appropriate port. Operating the server as a daemon is the recommended way of running smbd for servers that provide more than casual use file and print services. This switch is assumed if smbd is executed on the command line of a shell.

**-F** If specified, this parameter causes the main smbd process to not daemonize, i.e. double-fork and disassociate with the terminal. Child processes are still created as normal to service each connection request, but the main process does not exit. This operation mode is suitable for running smbd under process supervisors such as supervise and svscan from Daniel J. Bernstein’s daemontools package, or the AIX process monitor.

**-S** If specified, this parameter causes smbd to log to standard output rather than a file.

**-i** If this parameter is specified it causes the server to run “interactively”, not as a daemon, even if the server is executed on the command line of a shell. Setting this parameter negates the implicit daemon mode when run from the command line. smbd also logs to standard output, as if the -S parameter had been given.

**-V** Prints the program version number.

**-s** <configuration file> The file specified contains the configuration details required by the server. The information in this file includes server-specific information such as what printcap file to use, as well as descriptions of all the services that the server is to provide. See smb.conf for more information. The default configuration file name is determined at compile time.