# Domain Name System server

A Domain Name System (DNS) server is set up to translate host names to IP addresses on a TCP/IP network. Fedora can be configured as a DNS server using the named daemon.

By default, the DNS server is not configured to start automatically in Fedora. Before starting the service, you must configure the /etc/named.conf file and configure zone files (in the /var/named directory). To turn on a DNS server, type chkconfig named on. To start the service, type service named start.

# Reverse Address Resolution Protocol server

The Reverse Address Resolution Protocol (RARP) daemon responds to requests from RARP clients that must obtain their own IP addresses. Today, RARP is not used very often.

By default, the RARP package (rarpd) is not installed by default. When it is installed, the service is off. To turn on an RARP server, type chkconfig rarpd on. To start the service, type service rarpd start. When requests come in for addresses, the /usr/sbin/rarpd daemon checks the /etc/ethers or NIS databases for addresses.

# Database services

Database servers provide tools for accessing and managing databases of information. The PostgreSQL service uses the postmaster daemon to handle requests for its services. The MySQL server runs the mysqld daemon to handle access to its databases. These daemons are started from startup scripts in /etc/init.d: postgresql and mysqld scripts, respectively.

Many other databases run on Linux, including open source databases such as Firebird as well as commercial products such as Oracle and DB2.

> **CROSS-REFERENCE:** Chapter 23 describes how to set up a MySQL database server.

# User services

Fedora can provide end users with a variety of network services. These services let users send messages in real time and get information on active users.

# Talk server

Use the in.talk or in.ntalk servers to allow users to communicate using the talk command. The talk command enables users to type messages back and forth in real time. The talk daemon handles requests on port 517, and the ntalk daemon handles requests on port 518.

Both services are turned off by default. To turn on either service, edit the /etc/xinetd.d/talk and/or /etc/xinetd.d/ntalk files and change the disable = yes entry to disable = no. Then restart the xinetd daemon: service xinetd restart.