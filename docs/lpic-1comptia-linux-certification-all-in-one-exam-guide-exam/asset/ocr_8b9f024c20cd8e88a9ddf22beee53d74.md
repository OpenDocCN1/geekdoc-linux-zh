rective. This directive specifies whether or not xinetd is allowed to start the daemon when requested. In the preceding example, this directive is set to yes, which means the daemon will not be started when requested. The daemon to actually start is specified by the server = directive. In the example, xinetd will start the /usr/sbin/vsftpd daemon. To enable this daemon, you need to edit this file and change the disable parameter to a value of no. After changing a value in any of the files in /etc/xinetd.d, you need to restart the xinetd daemon using its init script in /etc/rc.d/init.d.

> **TIP** If you enable a service provided by xinetd, you’ll need to create an exception in your Linux system’s host firewall to allow traffic for the IP port used by the daemon.

# Using TCP Wrappers

If you enable a particular service using its configuration file in the /etc/xinetd/ directory, any host can connect to it through xinetd. However, depending upon how your system is deployed, you may need to control access to these network services. You may want to limit access to only a specific set of hosts and deny access to everyone else. If this is the case, then you need to configure these services to use TCP Wrappers. TCP Wrappers are used by xinetd to start and run the server services using a set of configuration files that specify who can and who can’t access the service.

To use TCP Wrappers, you first need to enable the functionality in each service’s configuration file in /etc/xinetd/. Do the following:

+   1. Verify that the tcpd package has been installed on your Linux system.
+   2. Open the appropriate configuration file in a text editor.
+   3. Comment out the existing server = line from the file.
+   4. Add the following line:

```
```text
server    = /usr/sbin/tcpd
```
```

This will cause xinetd to start the tcpd daemon instead of the service daemon itself.

+   5. Add the following line:

```
```text
server_args    = path_to_daemon
```
```

This tells the tcpd daemon to then run the requested network daemon. In the example shown here, the /etc/xinetd.d/telnet file has been configured to run the vsftpd daemon within a TCP wrapper:

```
```text
service ftp
{
    socket_type     = stream
    protocol        = tcp
    wait            = no
    user            = root
    server          = /usr/sbin/vsftpd
    server          = /usr/sbin/tcpd
    server_args
```
```