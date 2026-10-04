# Using the xinetd Super Server 605

The first two lines of the listing that begin with telnet show the port number of the TELNET service is 23. This number tells xinetd that any connection requests arriving at port 23 are meant for TELNET service. The configuration file /etc/xinetd.d/telnet then tells xinetd what to do to care of these requests.

The attributes in /etc/xinetd.d/telnet, enclosed in curly braces, have the following meanings:

+   * The flags attribute provides specific instructions on how to run the servers that xinetd starts. The REUSE flag means that the service is left running if xinetd restarts. *Note:* The REUSE flag is now implicitly assumed to be set for all servers.

+   * The socket_type attribute is set to stream, which tells xinetd that the TELNET service uses a connection-oriented TCP socket to communicate with the client. For those that use connectionless UDP packets, this attribute is set to dgram.

+   * The wait attribute is set to no, which tells xinetd to start a new server for each request. If this attribute is set to yes, xinetd waits until the server exits before starting the next one.

+   * The user attribute provides the user ID that xinetd uses to run the server. In this case, the server runs the TELNET service as root.

+   * The log_on_failure attribute tells what to log when it cannot start a server. In this case, the attribute is set to HOST, which means if xinetd cannot start the TELNET service, it logs the name of the remote host that requested the service.

+   * The server attribute specifies the program to run for this service. In this case, xinetd runs the /usr/sbin/in.telnetd program to provide TELNET service.

+   * The disable attribute turns off the service if it is set to yes. By default, the disable attribute is set to yes and TELNET is turned off.

Browse through the files in the /etc/xinetd.d directory on Fedora Core system to find out the kinds of services xinetd is set up to start. Many of these services, such as finger, provide information that intruders may use to break into your system. If they are not already disabled, you may want to turn off these services by placing the following line inside the curly braces that enclose all attributes:

```
disable = yes
```

On the other hand, if you can't seem to connect to your Fedora Core system by using telnet, check the appropriate file in the /etc/xinetd.d directory

| Book VIII |
| Chapter 1 |
| Managing the Servers |