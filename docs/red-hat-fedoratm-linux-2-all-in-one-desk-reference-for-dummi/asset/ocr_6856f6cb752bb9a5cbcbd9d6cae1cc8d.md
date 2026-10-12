A quick look through the entries in the /etc/services file shows the breadth of networking services available under TCP/IP.

REMEMBER

Note: Port number 80 is designated for Web server. In other words, if you set up a Web server on your system, that server listens to port 80. By the way, IANA—the Internet Assigned Numbers Authority (www.iana.org)—is the organization responsible for coordinating the assignment of port numbers below 1,024.

# Using the *inetd* Super Server

The client/server architecture of Internet services requires that the server be up and running before a client makes a request for service. A simplistic idea would be to run all the servers all the time — impractical because each server process would use up system resources in the form of memory and processor time. Besides, you don’t really need all the services up and ready at all times. A smart solution to this problem is to run a single server, xinetd, that listens to all the ports and then starts the appropriate server when a client request comes in. (The xinetd server is a replacement for an older server named inetd, offering improved access control and logging. The name xinetd stands for extended inetd.)

For example, when a client tries to connect to the TELNET port, xinetd starts the TELNET server and lets it communicate directly with the client (and the TELNET server exits when the client disconnects).

Because it starts various servers on demand, xinetd is known as the Internet super server. Typically, a UNIX system starts xinetd when the system boots. The xinetd server reads a configuration file named /etc/xinetd.conf at startup. This file tells xinetd which ports to listen to and what server to start for each port. The file can contain instructions that include other configuration files. In Fedora Core, the /etc/xinetd.conf file looks like the following:

```
```bash
# Simple configuration file for xinetd
#
# Some defaults, and include /etc/xinetd.d/

defaults {
		instances		= 60
		log_type		= SYSLOG authpriv
		log_on_success	= HOST PID
		log_on_failure	= HOST
		cps			= 25 30
}

includedir /etc/xinetd.d
```
```