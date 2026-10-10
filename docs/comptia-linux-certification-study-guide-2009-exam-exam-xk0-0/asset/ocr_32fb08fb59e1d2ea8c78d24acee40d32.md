+   - **Network Time Protocol** NTP is the Transmission Control Protocol/Internet Protocol (TCP/IP) used to synchronize the clocks on computers across a network. NTP uses User Datagram Protocol (UDP) on port 123.

+   - **MySQL** It is an open-source relational database management system that is developed, distributed, and supported by Sun Microsystems, Inc.

# INTRODUCTION

The role of a server is to act as a central repository for data and to serve applications and services to local and remote clients. The server can be specific to one particular need, such as a Web server or print server, but often in small networks, the servers are multifunctional. The server can serve network services to clients, such as DNS and Dynamic Host Configuration Protocol (DHCP), or as an application server for commonly used services such as printing and mail. This chapter will explain how to configure these services.

Companies need to have a Web presence, and the setting up of the Apache Web server along with some of the additional modules that need to be added to it (PHP, Common Gateway Interface [CGI], and so forth) is defined. Testing of the Web server using the command-line interface is outlined. While it is not considered very secure into today's world, the setting up and use of a File Transfer Protocol (FTP) server is defined. Some methods to make this server more secure are outlined. Finally, the Squid proxy server is described, and how it can be used in a network to help speed up the throughput is also described.

Finally, the main applications that you may wish to run on a server are explained – printing, mail, and a database. The popular variants of these are outlined, along with details on some of their configuration options. The use of mail servers and how to secure these from spammers is discussed, along with the different methods that clients can connect to them.

# NETWORK SERVICES

The basics of setting up servers to act as a DNS and DHCP server are explained, along with an introduction to their configuration files. Most companies would benefit from installing a DHCP server into their environment to manage the allocation of IP addresses, among other data. The basics of configuring and testing a DHCP server are explained, and a sample DHCP