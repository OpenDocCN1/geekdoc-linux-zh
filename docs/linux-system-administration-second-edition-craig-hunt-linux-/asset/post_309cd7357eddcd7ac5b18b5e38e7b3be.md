
topic, such as Charles Auld’s *Linux Apache Server Administration* (Sybex, 2001).

### X servers

An *X* server is a program that displays the windows created by *X*-based programs. On an isolated workstation installation of Linux, the X server (typically XFree86) runs on the same computer as the *X* programs that are being run. You can, however, connect to a remote computer (using a login protocol like Telnet or SSH) and run *X* programs from that remote system using your local *X* server. Note that, unlike most servers, the *X* server runs on the computer that’s nearest you; the remote system runs the client programs. This makes sense when you think of it from the program’s point of view: to the program, the server—and you—are at the distant location, and the server provides remote services (a display and input devices). Chapter 13 covers XFree86 (http://www.xfree86.org/), the *X* server that ships with all major Linux distributions.

### Warning

All servers are security risks. Bugs in servers, misconfigured servers, and flaws in local security (such as poor password selections by your users) make it possible for undesirables to break into your computer. In addition, some servers provide other possibilities for abuse. For instance, it’s easy to misconfigure a mail server so that it can be used to *relay* mail from anywhere to anywhere. Those who send unsolicited bulk e-mail (“spam”) frequently look for open relays to obscure their true location. Because of the great potential for abuse, you should run as few servers as possible on your Linux computer. Many Linux distributions install many servers by default, so you should check through your inetd.conf or xinetd.conf file (described shortly) and disable anything you’re not using.

## Using a Super Server

One problem with servers is that when they’re running, they consume system resources—primarily memory, but also some CPU time. These resources might be better used by other processes, particularly when the servers are used only occasionally. Systems that host many seldom-used servers therefore turn to a *super server* to control the servers. A super server is a program that looks for incoming packets addressed to several other servers. When the super server detects such packets, it launches the appropriate server program. When the individual servers aren’t needed, they don’t run. This approach can save a great deal of memory when you want to run several servers, most of which aren’t in use at any given moment.

Another benefit to using a super server is that it’s usually possible to implement additional security features with such a server. One approach to this is to use an intermediary package, such as TCP Wrappers (described in greater detail in Chapter 15), to filter connection requests. TCP Wrappers can examine the IP address of the calling system and allow or deny access based on this address. This can be extremely useful if some servers, such as a Telnet or SSH server, should only be accessible from certain computers.

## Using *xinetd*

Modern versions of Red Hat and Mandrake Linux use the *xinetd* (pronounced “zi-net-dee”) super server. Even administrators of other distributions frequently replace their standard inetd with *xinetd* in order to obtain the benefits of *xinetd*’s improved security features, which are described in greater detail in Chapter 15. This program’s greatest advantage is that it combines many of the features of TCP Wrappers in the super server proper. It’s particularly useful on systems that have multiple network cards, because it can block access to particular servers based on the network card. If your distribution doesn’t ship with *xinetd*, you can obtain it from http://www.xinetd.org/.

The xinetd configuration file is /etc/xinetd.conf. In a standard Red Hat or Mandrake installation, though, this file just sets a few default values and loads the files in the /etc/xinetd.d directory, each of which contains the configuration for one server. This configuration allows packages to easily add and remove xinetd configuration files. Listing 12.2 shows a sample xinetd service entry.

### Listing 12.2: A Sample xinetd Service Entry

```
service ftp
{
    disable         = no
    socket_type     = stream
    protocol        = tcp
    wait            = no
    user            = root
    server          = /usr/sbin/in.ftpd
    server_args     = -l -a
    interface       = 192.168.203.7
}
```

The meanings of the entries shown in Listing 12.2 are as follows:

- **service**: The definition begins with the service keyword, which identifies the server that this entry controls. You'll find service names in the /etc/services file, along with the port number associated with the service. xinetd "listens" on the port number associated with the service, and when it detects traffic directed at that port, xinetd launches the server. Following the service line is an opening curly brace, which marks the beginning of a block of configuration lines for this service. This block ends with the closing curly brace.

- **disable**: xinetd enables you to easily disable individual servers with this line; set the value to yes to do so. This example's entry is not disabled, but some servers install with their xinetd configurations disabled as a security precaution; you must actively enable the server to use it, so that accidentally installing the server won't open the system to its security vulnerabilities.

  > **Tip**: One easy first step to securing a Linux server is to disable all unnecessary servers from xinetd.d. In fact, none of the servers configured in this directory is necessary for Linux to boot. Some servers may sound like they're critically important, but they aren't. The login server, for example, is a very low-security remote login server; it is not required for ordinary text-mode logins or even for remote logins via Telnet or SSH.

- **socket_type**: Every service is associated with a socket type. Common values are stream and dgram.

- **protocol**: This is the type of TCP/IP connection—tcp or udp. Most network servers use TCP, which establishes a lasting two-way connection; but some use UDP, which is less robust but requires less overhead because it doesn't establish a full two-way connection.

- **wait**: Datagram-based services (those that specify a dgram socket type) either remain connected to the caller and specify yes here, or are multithreaded and split off a separate thread to handle the connection. This latter type specifies no. This entry isn't meaningful for streaming connections, but by convention they specify no.

- **user**: xinetd launches every server using a particular username. Many servers must be launched as root, but some may be launched under some other username to improve security.

- **server**: This item specifies the server that's to be launched when traffic directed at the service's port is detected. Normally, xinetd requires a complete path to the program.

- **server_args**: This option provides arguments that should be passed to the server. Some require special arguments when run from a super server, or you might simply want to launch them with arguments to have them behave in some nonstandard way (such as increase their debugging output).

- **interface**: The final entry in this example is the IP address associated with the network interface on which xinetd is to listen for connections. This entry is often omitted from xinetd configuration entries, but it's very useful on systems with multiple network interfaces. On such systems, xinetd doesn't respond to access attempts on interfaces that aren't explicitly enabled, which can be a very effective security tool.

xinetd is an extremely powerful package, so you should consult its documentation for information on more advanced options. Chapter 15 also covers some of xinetd's security-related features.

After you've made changes to your xinetd configuration, you must restart it. You can do this using its SysV startup script, as follows:

```
# /etc/rc.d/init.d/xinetd restart
```

## Using inetd

Although xinetd has been gaining in popularity in recent years, the most common super server in most Linux distributions remains inetd. This server is controlled through the /etc/inetd.conf file. Each line in this file corresponds to a single server. An example that uses TCP Wrappers is as follows:

```
ftp stream tcp nowait root /usr/sbin/tcpd in.ftp -l -a
```

The meaning of each element of this entry is similar to the meanings presented earlier, in "Using xinetd," with respect to xinetd configuration. Where xinetd relies upon named entries on separate lines, though, inetd relies upon a fixed order of entries on a single line. Specifically, using the xinetd names outlined earlier, the order is:

```
service socket_type protocol wait user server server_args
```

Most of these elements take the same values as their equivalents in xinetd. The *wait* field, though, takes values of wait and nowait, rather than yes and no. The *server* field frequently points to tcpd, the TCP Wrappers binary. The name of the server is passed to TCP Wrappers as the first argument in the *server_args* field.

In the default inetd.conf file, you'll find entries for most common servers. Most of these entries are commented out with pound signs (#), however. You can therefore uncomment the appropriate entries when you add a server of a particular type. Conversely, if you remove a server or want to disable it, you can comment out the appropriate line if it's active. You can use this feature rather
