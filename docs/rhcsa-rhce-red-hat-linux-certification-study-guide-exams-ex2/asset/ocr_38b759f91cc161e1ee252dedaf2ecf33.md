# FIGURE 10-9

Take advantage of custom rules.

![](bbox=[0.25, 0.17, 0.9, 0.62])

# CERTIFICATION OBJECTIVE 10.03

# The Extended Internet Super-Server

Linux typically supports network communication between clients and servers. For example, even though it's insecure, it is still possible to use Telnet on Linux to connect to a remote system. The Telnet client on a local computer makes a connection with a Telnet server daemon on the remote system. This section assumes that you've installed the default RHEL xinetd and telnet-server packages. The use of Telnet in this section is for illustration purposes only. This book does not endorse the use of Telnet or any clear-text protocol for private data.

While the focus in this section is on Telnet, other xinetd packages of note include rsync, which is popular for backups; and cvs, popular for software development version control. As no xinetd service is explicitly cited in the RHCE objectives, I keep the