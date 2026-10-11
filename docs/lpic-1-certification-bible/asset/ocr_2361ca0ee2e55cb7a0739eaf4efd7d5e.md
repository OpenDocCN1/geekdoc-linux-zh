+   7. The `LogFormat` and `CustomLog` directives control logging in Apache. `LogFormat` changes the standard logging, while `CustomLog` does that and lets you output logs to a new file.

+   8. The `nfstat` tool displays statistics about the NFS server that can help troubleshooting and performance tweaking.

+   9. The `smbclient` tool is used to connect to remote Windows and Samba shares.

+   10. BIND v4 uses the `named.boot` file, while BIND v8 uses the `named.conf` file.

# Assessment Questions

+   1. B. The `stream` type is always used with TCP, and `dgram` is used with UDP. For more information see the “Configuring inetd” section.

+   2. B. Any time the `inetd.conf` file is changed, `inetd` needs to be restarted for the changes to take effect. For more information see the “Restarting the inetd process” section.

+   3. C. Anonymous FTP accounts should not have a valid shell statement in `/etc/passwd`. This limits login to FTP only. For more information see the “Setting up anonymous FTP” section.

+   4. A. If a user exceeds the limit set by `loginfail`, they are disconnected. For more information see the “The ftpaccess file” section.

+   5. D. The `ftpwho` command shows who is connected to the FTP server. For more information see the “The ftpwho command” section.

+   6. A and C. Mail aliases are stored in `/etc/aliases`. Any time an entry is added the `newaliases` command needs to be run. For more information see the “Aliasing and forwarding mail” section.

+   7. `mailq`. The `mailq` command shows any messages waiting in the queue as well as any errors that may keep them from being delivered. For more information see the “Managing sendmail” section.

+   8. B. Only run Apache through `inetd` for a web server that expects very few hits. The overhead of starting the Apache daemon every time a client connects severely impacts performance. For more information see the “Starting and stopping httpd” section.

+   9. B and C. An entry needs to be added to the `inetd.conf` file so that `inetd` knows to start the service when a user connects. The `ServerType` entry needs to be set correctly in `httpd.conf` so that Apache knows not to keep running when a connection completes. For more information see the “Server configuration” section for Apache.

+   10. B. Apache uses a file created by `htpasswd`. For more information see the “Authentication” section for Apache.

+   11. B and C. Restrictions can be set using CIDR notation or using wildcards with domains. For more information see the “Configuring exports” section.