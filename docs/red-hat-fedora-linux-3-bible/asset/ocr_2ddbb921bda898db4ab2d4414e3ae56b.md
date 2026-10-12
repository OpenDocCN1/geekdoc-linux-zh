for requests for many different services. As a result, when you type `ps -ax` to see what processes are running, dozens of fewer daemon processes will be running than there would be if each service had its own daemon.

+   * **Access control and logging**. By using `xinetd` to oversee the management of services, consistent methods of access control (such as PAM) and consistent logging methods (such as the `/var/log/messages` file) can be used across all of the services.

When a request comes into your computer for a service that `xinetd` is monitoring, `xinetd` uses the `/etc/xinetd.conf` file to read configuration files contained in the `/etc/xinetd.d` directory. Then, based on the contents of the `xinetd.d` file for the requested service, a server program is launched to handle the service request (provided that the service is not disabled).

Each server process is one of two types: single-thread or multithread. A single-thread server will handle only the current request, whereas a multithread server will handle all incoming requests for the service as long as there is still a client holding the process open. Then the multithread server will close and `xinetd` will begin monitoring that service again.

The following are a few examples of services that are monitored by `xinetd`. The daemon process that is started up to handle each service is also listed.

+   * **comsat** (`/usr/sbin/in.comsat`) — Alerts the `biff` client that new mail has arrived.
+   * **elogin** (`/usr/kerberos/sbin/login`) — Kerberos-related login daemon.
+   * **finger** (`/usr/sbin/in.fingerd`) — Handles incoming finger requests for information from remote users about local users.
+   * **gsftpd** (`/usr/kerberos/sbin/ftpd`) — Kerberos-related daemon for handling file transfer requests (FTP).
+   * **ntalk** (`/usr/sbin/in.ntalkd`) — Daemon for handling requests to set up chats between a remote user and a local one (using the `talk` command).
+   * **rlogin** (`/usr/sbin/in.rlogind`) — Daemon for responding to remote login requests (from a remote `rlogin` command).
+   * **rsh** (`/usr/sbin/in.rshd`) — Handles requests from a remote client to run a command on the local computer.

Other services that can be launched by requests that come to `xinetd` include services for remote telnet requests, Samba configuration requests (swat), and Amanda network backups. A short description of each service is included in its `/etc/xinetd.d` file.

# ## Manipulating run levels

Aside from the run level chosen at boot time (usually 3 or 5) and the shutdown or reboot levels (0 and 6, respectively), you can change the run level at any time while you're logged in (as root user). The `telinit` command (really just a symbolic link to `init`) enables you to