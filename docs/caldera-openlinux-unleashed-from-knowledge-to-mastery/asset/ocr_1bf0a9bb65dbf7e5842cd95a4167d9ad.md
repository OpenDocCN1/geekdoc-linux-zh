NIS (the Network Information System) is a method for sharing information across a computer network. NIS enables you to log on to any computer in a network (with the same login name and password) by using a shared password database. NIS can also be used to share the /etc/hosts information (providing a service analogous to DNS).

By distributing system configuration across a network, all computers appear almost identical. In addition, the master files are centralized, easing the maintenance of configuration information if you need to add or move hosts.

# # How NIS Works

An NIS server maintains databases of information. NIS clients send requests to the server, which looks up information in its databases and returns the results to the clients.

NIS networks are divided into administrative groupings called NIS domain names. Note that NIS domains have nothing to do with DNS domains: they are simply groups of hosts created for administrative purposes. Having said that, an NIS domain typically corresponds to all the computers on a LAN.

For example, even though all computers in a fairly large organization (Sun Microsystems, say) will be under the same DNS domain sun.com, they will be divided into many NIS domains, each of which corresponds to a local area network.

Originally, NIS was called Yellow Pages, or YP. However, British Telecom holds the trademark to Yellow Pages and forced Sun Microsystems to drop the name. Nevertheless, many NIS-related command names begin with y p as a result of the heritage.

# ## NIS Maps

An NIS server maintains its information in databases called NIS maps. The maps are usually generated from normal system configuration files. Table 14.1 lists some typical NIS maps and the corresponding system configuration files.

**TABLE 14.1 NIS Maps**
|System File|Maps|
|/etc/passwd|passwd.byname, passwd.bynid|
|/etc/hosts|hosts.byname, hosts.byaddr|
|/etc/group|group.byname, group.bygid|