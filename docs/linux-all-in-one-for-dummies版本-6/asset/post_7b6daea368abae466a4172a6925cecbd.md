
uses system resources in the form of memory and processor time. Besides, you don’t really need all the services up and ready at all times. Instead, run a single server that listens to all the ports and starts the appropriate server when a client request comes in. Such a server is known as an Internet super server because it starts various services on demand.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_252_0.png)

The two Internet super servers are inetd and xinetd. The inetd server is the older one and is still used in Linux distributions such as Debian, Knoppix, and Ubuntu. The xinetd server is a replacement for inetd, offering improved access control and logging. The name xinetd stands for extended inetd. Distributions such as Fedora and SUSE use xinetd.

## Using inetd

In Linux distributions that use inetd, the system starts inetd when the system boots. The inetd server reads a configuration file named /etc/inetd.conf at startup. This file tells inetd which ports to listen to and what server to start for each port. The entry in the /etc/inetd.conf file that starts Internet Message Access Protocol (IMAP) on one server looks like this:

```
imaps stream tcp nowait root /usr/sbin/tcpd /usr/sbin/imapd
```

The first item on this line, imaps, tells inetd the name of the service. inetd uses this name to look up the port number from the /etc/services file. If you type grep imaps /etc/services, you find that the port number of the IMAP service is 993. This specification tells inetd to listen to port 993 for FTP service requests.

The rest of the fields in the IMAP entry have the following meanings:

- The second and third fields of the entry, stream and tcp, tell inetd that the FTP service uses a connection-oriented TCP socket to communicate with the client. For services that use the connectionless UDP sockets, these two fields are dgram and udp.
- The fourth field, nowait, tells inetd to start a new server for each request. If this field is wait, inetd waits until the server exits before starting the server again.
- The fifth field provides the user ID that inetd uses to run the server. In this case, the server runs the FTP server as root.
- The sixth field specifies the program to run for this service and the last field is the argument that inetd passes to the server program. In this case, the /usr/sbin/tcpd program is provided /usr/sbin/imapd as an argument.

The /usr/sbin/tcpd program is an access-control facility, or a TCP wrapper, for Internet services. Because unnecessary Internet services are often the sources of security vulnerabilities, you may want to turn off any unneeded services or at least control access to the services. The tcpd program can start other services, such as FTP and Telnet, but before starting the service, tcpd consults the /etc/hosts.allow file to see whether the host requesting service is allowed that service. If nothing is in /etc/hosts.allow about that host, tcpd checks the /etc/hosts.deny file to see whether the service should be denied. If both files are empty, tcpd allows the host access to the requested service. You can place the line ALL:ALL in the /etc/hosts.deny file to deny all hosts access to any Internet services.

Browse through the /etc/inetd.conf file on your system to find out the kinds of services that inetd is set up to start. Nowadays, most inetd services are turned off, and many others, such as FTP, are started by stand-alone servers. In any case, if you see any services that you want to turn off, simply place a hash mark (#) at the beginning of the lines that start these services. When you make such a change in the /etc/inetd.conf file, type /etc/init.d/inetd restart to restart the inetd server.

## Using xinetd

Linux distributions that use xinetd start xinetd when the system boots. The xinetd server reads a configuration file named /etc/xinetd.conf at startup. This file tells xinetd which ports to listen to and what server to start for each port. The file can contain instructions that include other configuration files. In Linux, the /etc/xinetd.conf file looks like the following:

```
# Simple configuration file for xinetd
#
# Set some defaults and include /etc/xinetd.d/
defaults
{
instances = 30
log_type = FILE /var/log/xinetd.log
log_on_success = HOST EXIT DURATION
log_on_failure = HOST ATTEMPT
cps = 50 10
}
includedir /etc/xinetd.d
```

Comment lines begin with the hash mark (#). The default block of attributes, enclosed in curly braces ({ ... }), specifies default values for some attributes. These default values apply to all other services in the configuration file. The instances attribute is set to 30, which means that no more than 30 servers can be simultaneously active for any service.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_254_0.png)

The last line in the /etc/xinetd.conf file uses the includedir directive to include all files inside the /etc/xinetd.d directory, excluding files that begin with a period (.). The idea is that the /etc/xinetd.d directory contains all service-configuration files — one file for each type of service the xinetd server is expected to manage. Type ls /etc/xinetd.d to see the xinetd configuration files for your system. Each file in /etc/xinetd.d specifies attributes for one service that xinetd can start.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_254_1.png)

SUSE Linux uses xinetd to start some services, including the vsftpd (Very Secure FTP daemon) server. (A daemon is a process that runs continuously and never dies.) Type cat /etc/xinetd.d/vsftpd to see the xinetd configuration for the vsftpd service. Here's a typical listing of that file on a SUSE system:

```
# default: off
# description:
# The vsftpd FTP server serves FTP connections. It uses
# normal, unencrypted usernames and passwords for authentication.
# vsftpd is designed to be secure.
service ftp
{
socket_type = stream
protocol = tcp
wait = no
user = root
server = /usr/sbin/vsftpd
}
```

The filename (in this case, vsftpd) can be anything; what matters is the service name that appears next to the service keyword in the file. In this case, the line service ftp tells xinetd the name of the service. xinetd uses this name to look up the port number from the /etc/services file.

The attributes in /etc/xinetd.d/vsftpd, enclosed in curly braces ({ . . . }), have the following meanings:

- The socket_type attribute is set to stream, which tells xinetd that the FTP service uses a connection-oriented TCP socket to communicate with the client. For services that use the connectionless UDP sockets, this attribute is set to dgram.
- The wait attribute is set to no, which tells xinetd to start a new server for each request. If this attribute is set to yes, xinetd waits until the server exits before starting the server again.
- The user attribute provides the user ID that xinetd uses to run the server. In this case, the server runs the vsftpd server as root.
- The server attribute specifies the program to run for this service. In this case, xinetd runs the /usr/sbin/vsftpd program to provide the FTP service.

Browse through the files in the /etc/xinetd.d directory on your Linux system to find out the kinds of services xinetd is set up to start. If you want to turn off any service (many services are already disabled), you can do so by editing the configuration file for that service and adding the following line inside the curly braces that enclose all attributes:

```
disable = yes
```

When you make such a change in the xinetd configuration files, you must restart the xinetd server by typing the following command:

/etc/init.d/xinetd restart

![](img/322157d1fa7d965f05bcd68ed0ffc36b_255_0.png)

Typically, you can configure services to run under xinetd or as a stand-alone service. SUSE starts the Very Secure FTP daemon (vsftpd) under the control of xinetd. Debian and Fedora, however, run vsftpd as a stand-alone server.

## Running Stand-Alone Servers

Starting servers through inetd or xinetd is a smart approach but not always efficient. A web server controlled by inetd or xinetd would be started often because every time a user clicks a link on a web page, a request arrives for the web service. For such high-demand services, starting the server in a stand-alone manner is best. In stand-alone mode, the server can run as a daemon, which means that the server listens on the assigned port, and whenever a request arrives, the server handles it by making a copy of itself. In this way, the server keeps running as long as the machine is running — in theory, forever. A more efficient strategy, used for web servers, is to run multiple copies of the server and let each copy handle some of the incoming requests.

You can easily configure your Linux system to start various stand-alone servers automatically, as shown in this section.
