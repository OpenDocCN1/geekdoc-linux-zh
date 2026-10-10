
server's performance and log files just to be aware if anything bad is about to happen or has already happened.

There are several monitoring tools available in the Linux world. The Nagios software package is quickly becoming a popular tool, especially in cloud Linux systems. Nagios uses SNMP to monitor the performance and logs of Linux servers and provide results in a simple graphical window environment.

## Improving Performance

Developers and administrators of high-volume Linux applications are always looking for ways to improve the performance of the applications. There are three common methods for improving performance that all Linux administrators should be aware of. This section covers these methods.

## Clustering

A computer cluster improves application performance by dividing application functions among multiple servers. Each server node in the cluster is configured the same and can perform the same functions, but the cluster management software determines how to split the application functions among the servers. Since each server in the cluster is working on only part of the application, you can use less powerful servers within the cluster than if you had to run the entire application on a single server.

The cluster management software is the key to the performance of the cluster. One of the earliest attempts at creating clusters of inexpensive Linux servers was the Beowulf cluster. The Beowulf cluster relied on parallel processing libraries, such as the Parallel Virtual Machine (PVM) library, to distribute an application's library calls between multiple Linux servers.

Newer versions of clustering include the Apache Hadoop project and the Linux Virtual Server (LVS) project.

## Load Balancing

Load balancing is a special application of clustering. A load balancer redirects entire client requests to one of a cluster of servers. While a single server processes the entire request, the client load is distributed among the multiple servers automatically.

Common Linux load-balancing packages include HAProxy, the Linux Virtual Server (LVS), and even the nginx Web server.

## Containers

One of the biggest problems for application developers is creating a development environment that mirrors the actual server environment the applications run in. All too often a developer will get an application working just fine in a workstation development environment only to see it crash and burn when ported to the server.

Linux **containers** help solve this problem by creating a self-contained environment to encapsulate applications. A container packages all of the necessary application files, library files, and operating system libraries into a bundle that you can easily move between environments.

Several Linux server packages are available that support containers. Currently, the two most popular ones are **Docker** and **Kubernetes**. You can use these packages to easily port application containers to any Linux server, whether it's a physical server, a virtual server, or in the cloud.

## Summary

Linux servers provide network applications that support both clients and network devices. Server applications are called services and are launched by the Linux server without human intervention. When a Linux server can launch services directly, they're called daemons. The daemon runs in the background and listens for client connection requests. A super-server runs in the background and listens for client connection requests for multiple services. When a connection request is accepted, the super-server launches the appropriate service.

Linux supports services for all types of applications. The Apache and nginx services provide web server applications for Linux. For database applications, PostgreSQL, MySQL, and MongoDB are the most popular. If you're looking to run an email server, the sendmail, Postfix, or Exim application should do the trick. Linux also works well as a server for a local network environment. There are open source packages for file, print, and network server resources as well as packages for security authentication and certificate applications.

Finally, you can configure Linux servers for fault tolerance by clustering a large group of small servers together to create one large server. The clustering software can either work to split an application to run over several servers simultaneously or assign individual clients to specific servers to implement load balancing. To support application development, Linux servers also support containers. Containers allow developers to migrate the same environment used to develop an application to a production environment, ensuring that applications will work the same in both development and production.

## Exam Essentials

- Describe the ways to start server programs in Linux. Server programs in Linux can either run continually in the background as a daemon process or be started from a super-server daemon when requested by a client.

- Explain how clients know how to contact a server program. Server applications listen for client connections on well-known ports. Clients must send a connection request to the server on the well-known port for the application they want to interact with.

- Explain the components commonly used in a LAMP stack. The LAMP stack uses the Linux operating system, the Apache web server, the MySQL database server, and the PHP programming language to provide a platform for web applications.

- Describe the difference between a relational database and a NoSQL database. A relational database stores data records in individual data tables. Each data type consists of one or more data fields that contain individual data elements. A data record is an instance of data for each data field in a table. A NoSQL database stores data values in documents. Each document is independent of all of the other documents in the database. Each document can also contain different data elements.

- Understand the ways a Linux server can share files in a local network. Linux servers can use the nfs-utils package to communicate with other Linux servers to share folders using NFS. The local Linux server can mount folders from the remote Linux server as if they were local disks. Linux servers can also use the Samba package to share files on Windows local networks with Windows clients and servers as well as map folders located on Windows servers.

- Understand which server packages are commonly used to support network features on a local network. The DHCPd package provides DHCP server services to assign IP addresses to clients. The BIND package provides DNS server services to both clients and servers on a local network for hostname resolution. The net-snmp package allows you to implement remote device management using SNMP, and you can use the ntpd package to create an NTP time server for the local network.

- Describe how to create a network directory server using Linux. The OpenLDAP package allows you to create an LDAP directory of users and devices on the local network. Clients and other servers can use the LDAP directory to authenticate users and devices on the network.

- Explain how to improve the performance of a network application. For network applications in a high-volume environment, you can improve performance by implementing either a cluster or load balancing environment. In a cluster, you can split application functions between multiple servers by using a cluster package such as Apache Hadoop. With load balancing, you can distribute client connections between multiple servers using packages such as HAProxy and Linux Virtual Server (LVS).

## Review Questions

1. Which web server is used in the popular LAMP stack?
   - **A.** nginx
   - **B.** Apache
   - **C.** Lighttpd
   - **D.** PostgreSQL

2. A \_\_\_\_\_\_\_\_ runs in the background and listens for client connection requests for a single application.
   - **A.** Daemon
   - **B.** Super-server
   - **C.** Shell
   - **D.** Graphical desktop

3. Which open source database provided fast performance and became a popular choice for web applications?
   - **A.** MongoDB
   - **B.** PostgreSQL
   - **C.** MySQL
   - **D.** NoSQL

4. How does a server know what client request is sent to which application daemon?
   - **A.** IP addresses
   - **B.** Ports
   - **C.** Ethernet addresses
   - **D.** Services

5. What popular open source web servers can also perform as a load balancer?
   - **A.** nginx
   - **B.** Apache
   - **C.** PostgreSQL
   - **D.** Lighttpd

6. What format does MongoDB use to store data elements in the database?
   - **A.** Relational
   - **B.** YAML
   - **C.** JSON
   - **D.** Encrypted
