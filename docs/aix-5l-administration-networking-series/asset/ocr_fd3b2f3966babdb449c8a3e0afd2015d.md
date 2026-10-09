# **324**

AIX 5L Administration

The NIS daemons are as follows:

+   ypserve NIS server daemon
+   ypbind NIS server binding manager
+   ypasswdd NIS passwd update daemon
+   ypupdated NIS map updated invoked by inetid
+   keyserver Public key server daemon
+   portmap RPC program to port manager

# ## Automounter

The **automount** daemon can be run in a large NIS network to simplify NFS filesystem access. The **automount** daemon will automatically mount a filesystem whenever a file or directory in the filesystem is opened. Files and directories associated with an **automount** filesystem are kept in an NIS map. The **automount** daemon forks child processes that appear as NFS clients that monitor filesystems drawing on the information in the maps. The daemons unmount filesystems that have not been accessed in the last five minutes. The master **automount** map file is `auto.master`.

```
# /usr/sbin/automount
```

# ## NIS+

NIS+ was not an enhancement to NIS. It replaced NIS. NIS+ was designed to address several shortcoming of NIS such as meeting the needs involved in managing a complex and big network, decentralizing the network administration tasks, and providing network security. You will still need both `bos.net.nis` server and client file sets installed as prerequisites for the NIS+ `bos.net.nisplus` file set.

An NIS+ namespace can be organized in hierarchical domains. Conceptually, you can think of an NIS+ namespace as like a UNIX filesystem structure, where you have a root directory and subdirectories below it. In NIS+, the root directory is called the root domain, while subdirectories are called subdomains. The depth in levels of subdomains depends on the size and complexity of your organization. In subdomains can be managed autonomously; however, clients can access information in other subdomains under the same root domain.

Another difference in NIS+ is that information for the domains is stored in NIS+ relational database tables instead of maps as in NIS. You must use a set of administrative commands provided by NIS+ to view and update the tables. The tables are kept in the directory `/var/nis/data`. Updates to the tables do not require the tables to be remade, and they are propagated to the replica servers incrementally.

NIS+ includes authentication and authorization for security. In order for a user, a host, or a process, called an NIS+ principal, to access NIS+ information, called an NIS+ object, it must be authenticated using DES (the Data Encryption Standard). After the authentication process, the principal is categorized in an authorization class (**owner, group, world,** or **nobody**) of the object. In each class, there are permissions to specify