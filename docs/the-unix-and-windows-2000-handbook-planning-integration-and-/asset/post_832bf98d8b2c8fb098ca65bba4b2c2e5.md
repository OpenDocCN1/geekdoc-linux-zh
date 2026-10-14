
## Network Information System

The Network Information System (NIS) was developed by Sun Microsystems to aid in the administration of distributed networks. NIS provides centralized control of configuration files utilized by UNIX workstations. It was later followed by NIS+, which has more functionality. NIS+, however, does not run on all of the major UNIX operating systems, so NIS is still widely used. We will begin by covering NIS, and then provide information on NIS+.

The configuration files used in NIS are grouped together into domains. A simple rule to follow in NIS domain name selection is to use your DNS domain. The most common configuration files distributed by NIS are summarized in Table 7.1.

| Table 7.1 NIS Files and Maps |
| File | Information | Maps | DBM Files |
| /etc/passwd | User ID, Group ID, Password, Name, Shell, Home directory | Passwd.byname Passwd.byuid | Passwd.byname.dir Passwd.byname.pag Passwd.byuid.dir Passwd.byuid.pag |
| /etc/group | Groups and members by user ID | Group.by gid Group.by name | Group.by gid Group.by gid.pag Group.by name.dir Group.by name.pag |
| /etc/hosts | Hostnames and IP addresses | Hosts.byaddr Hosts.by name | Hosts.byaddr.dir Hosts.byaddr.pag Hosts.by name.dir Hosts.by name.pag |
| /etc/networks | Name and IP address | Networks.byaddr Networks.by name | Networks.byaddr.dir Networks.byaddr.pag Networks.by name.dir Networks.by name.pag |
| /etc/services | Service names, port numbers/protocol | Services.by name | Services.by name.dir Services.by name.pag |
| /etc/protocols | Official protocol name, protocol number, and aliases | Protocols.by name Protocols.by number | Protocols.by name.dir Protocols.by name.pag Protocols.by number.dir Protocols.by number.pag |
| netgroup | Hostname, username, and domain name | Netgroup.by host Netgroup.by user | Netgroup.by host Netgroup.by user |

NIS converts the information contained in text files into NIS maps. The maps are derived from DBM database files. DBM database files consist of a key value and information associated with the key. Information lookup is accomplished by matching the key value. Some configuration files contain information requiring the generation of multiple maps with different key values. The passwd file is a good example. UNIX provides two functions to look up information about a user. One function utilizes the user's login name and the other utilizes the user's ID (UID). NIS generates two maps with key values of the login name (passwd.byname) and the UID (passwd.byuid) for the passwd file. DBM database files are actually comprised of two files. The hashed index file has a .dir extension and the data file has a .pag extension. This allows much faster lookup of information than a sequential scan of an ASCII file.

NIS uses the client/server model to distribute information. There is one master server that maintains the master configuration files for the domain (the master server can serve multiple domains) on a local filesystem. The NIS maps are located under the /var/yp directory on the master server. Changes are made to the configuration files, a make is performed in the /var/yp directory, and new maps are built and pushed to slave servers for all changed files. Slave servers have the domain maps “pushed” from the master server, or they can “pull” the maps from the master server. Clients “bind” to a server (master or slave) and query the server for information contained in a map.

The next few sections will cover the important basics of NIS administration. We will assume that NIS is not running on our example network. The first section will cover the steps required to set up the NIS master server. The second section will cover creation of a slave server. The third section will cover the set up of an NIS client and explain the process of binding. The final section will cover important NIS commands.

## NIS MASTER SERVER CREATION

The installation of an NIS master server will be covered in three steps. The first step will be the initialization of the master server’s NIS maps. The second step will be enabling the rpc.ypasswdd daemon. The final step will be to ensure that the NIS services will start automatically at boot.

### Initialization

The first step is to carefully select your master server. This process was covered earlier in the chapter. You also need to have the slave server names. The NIS maps are based on configuration files utilized by UNIX to aid in the boot process and limit access to a workstation. The man pages of ypinit or ypfiles contain a listing of the files that will generate NIS maps for
