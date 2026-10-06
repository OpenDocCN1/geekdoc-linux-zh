# Distributed Computing

![](bbox=[0.238, 0.063, 0.843, 0.192])

**Figure 9-2** A fileserver

# Distributed Computing

When many similar systems are on a network, it is often desirable to share common files and utilities among them. For example, a system administrator might choose to keep a copy of the system documentation on one computer's disk and to make those files available for all remote systems. In this case the system administrator configures files so that users who need to access the online documentation are not aware that the files are stored on a remote system. This type of setup, which is an example of *distributed computing*, not only conserves disk space but also allows you to update one central copy of the documentation rather than tracking and updating copies scattered throughout the network on many different systems.

Figure 9-2 illustrates a *fileserver* that stores the system manual pages and users' home directories. With this arrangement, a user's files are always available to that user—no matter which system the user is on Each system's disk might contain a directory to hold temporary files, as well as a copy of the operating system. For more information refer to “exportfs: Stores Permissions to Mount Local Filesystems” and “autofs: Automically Mount Filesystems” on page 979.

# The Client/Server Model

Although there are many ways to distribute computing tasks on hosts attached to a network, the client/server model dominates UNIX and GNU/Linux system working. A server system offers services to its clients and is usually a central resource. In Figure 9-2 the system that acts as the repository is a server, and all the systems that contact it to display information are clients. Some servers are designed to interact with specific utilities, such as Web servers and browser clients. Other servers, such as those supporting DNS, communicate with one another in addition to answering queries from a variety of clients; in other words, a server can act as a client when it queries another server.