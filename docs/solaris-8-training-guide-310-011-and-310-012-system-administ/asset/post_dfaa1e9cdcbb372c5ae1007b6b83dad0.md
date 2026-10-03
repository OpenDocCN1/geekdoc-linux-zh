
The information in these files is put into NIS databases automatically when you create a NIS master server. Other system files can also be managed by NIS if you want to customize your configuration.

NIS makes updating network databases much simpler than with the /etc file system. You no longer have to change the administrative /etc files on every system each time you modify the network environment. For example, if you add a new system to a network running NIS, you only have to update the input file in the master server and run /usr/ccs/bin/make. This process automatically updates the hosts.byname and hosts.byaddr maps. These maps are then transferred to any slave servers and made available to all the domain's client systems and their programs.

Just as you use the cat command to display the contents of a text file, you can use the ypcat command to display the values in a map. Here is the basic ypcat syntax:

```
ypcat [-k] <mapname>
```

If a map is composed only of keys, as in the case of ypservers, use ypcat -k otherwise, ypcat prints blank lines.

In this case, mapname is the name of the map you want to examine.

You can use the ypwhich command to determine which server is the master of a particular map:

```
ypwhich -m <mapname>
```

In this case, mapname is the name of the map whose master you want to find. ypwhich responds by displaying the name of the master server.

These and other NIS commands are covered in the following sections.

## PLANNING YOUR NIS DOMAIN

Before you configure systems as NIS servers or clients, you must plan the NIS domain. Each domain has a domain name, and each system sharing the common set of maps belongs to that domain.

## STEP BY STEP

### 18.1 Planning Your NIS Domain

Follow these steps to plan your domain:

- 1. Decide which systems will be in your NIS domain.
- 2. Choose a NIS domain name. An NIS domain name can be up to 256 characters long, although much shorter names are more practical. A good practice is to limit domain names to no more than 32 characters. Domain names are case-sensitive. For convenience, you can use your Internet domain name as the basis for your NIS domain name. For example, if your Internet domain name is pdesigninc.com, you can name your NIS domain pdesigninc.com.
- 3. Before a system can use NIS services, the correct NIS domain name, and system name must be set. This must be done on the NIS servers as well as the clients. A system's name is set by the system's /etc/nodename file, and the system's domain name is set by the system's /etc/defaultdomain file. These files are read at startup, and the contents are used by the uname -s and domainname commands, respectively. A sample /etc/nodename file would look like this:

`more /etc/nodename`

The system responds with this:

`sparcserver`

A sample /etc/defaultdomain file would look like this:

`more /etc/defaultdomain`

The system responds with this:

`pdesigninc.com`

You are now ready to configure your NIS master server.

## Configuring a NIS Master Server

Before configuring a NIS master server, be sure the NIS package is installed. The package names are SUNWypu and SUNWypr. Use the pkginfo command to check for these packages. Both packages are part of the standard Solaris 8 release. The daemons that support the NIS service are described in Table 18.3.

### Table 18.3 NIS Daemons

| Daemon | Function |
|---|---|
| ypserv | This daemon is the NIS database lookup server. The ypserv daemon's primary function is to look up information in its local database of NIS maps. If the /var/yp/ypserv.log file exists when ypserv starts up, log information is written to it if error conditions arise. At least one ypserv daemon must be present on the network for the NIS service to function. |
| ypbind | This daemon is the NIS binding process that runs on all client systems that are set up to use NIS. The function of ypbind is to remember information that lets all NIS client processes on a node communicate with some NIS server process. |
| ypxfr | This daemon is the high-speed map transfer. ypxfr moves a NIS map in the default domain to the local host. It creates a temporary map in the directory /var/yp/ypdomain. |
| rpc.yppasswdd | This daemon handles password change requests from the yppasswd command. It changes a password entry in the passwd, shadow, and security/passwd.adjunct files. |
| rpc.ypupdated | This daemon updates NIS information. ypupdated consults the updaters file in the /var/yp directory to determine which NIS maps should be updated and how to change them. |

The commands that you use to manage the NIS service are shown in Table 18.4. I'll describe some of these commands in more detail later as I show examples of setting up NIS.

### Table 18.4 NIS Commands

| Utility | Function |
|---|---|
| make | This command updates NIS maps by reading the makefile (if run in the /var/yp directory). You can use make to update all maps based on the input files or to update individual maps. |
| makedbm | This command creates a dbm file for a NIS map. The makedbm command takes the infile and converts it to a pair of files in ndbm format. When you run make in the /var/yp directory, makedbm creates or modifies the default NIS maps from the input files. |
| ypcat | This command lists data in a NIS map. |
| ypinit | This command builds and installs a NIS database and initializes the NIS client's (and server's) ypservers list. ypinit is used to set up a NIS client system. You must be the superuser to run this command. |
| yppoll | This command gets a map order number from a server. The yppoll command asks a ypserv process what the order number is, and which host is the master NIS server for the named map. |
| yppush | This command propagates a new version of a NIS map from the NIS master server to NIS slave servers. |
| ypset | This command sets binding to a particular server. ypset is useful for binding a client node that is on a different broadcast network. |
| ypstart | This command is used to start NIS. After the host has been configured using the ypinit command, ypstart automatically determines the machine's NIS status and starts the appropriate daemons. |
| ypstop | This command is used to stop the NIS. |
| ypwhich | This command returns the name of the NIS server that supplies the NIS name services to a NIS client, or it returns the name of the master for a map. |

A NIS master server holds the source files for all the NIS maps in the domain. Any changes to the NIS maps must be made on the NIS master server. The NIS master server delivers information to NIS clients and supplies the NIS slave servers with up-to-date maps. Before the NIS master server is started, some of the NIS source files need to be created.

One of the primary uses of NIS is to manage user logins and host files in a large networked environment. In a large network of systems, with several hundred users, imagine trying to keep the /etc/hosts, /etc/passwd, and /etc/group files up-to-date. Without NIS, every time a new system is added or removed, the /etc/hosts file must be updated. It's important to keep your /etc/hosts files in sync on every system on the network. Furthermore, without NIS, if a user changes a password, that user must notify the system administrator that his or her password has changed. The system administrator must then be sure that all the /etc/shadow files are updated across the network. If they aren't, the user can't log in to another system using the new password.

The system administrator can manage the system configuration files, such as /etc/hosts and /etc/passwd, using NIS. With NIS, the system administrator sets up the /etc/hosts, /etc/passwd, and /etc/group files on one server. Rather than keeping a copy of the configuration file on each system, all systems look to this server for configuration information.

## Creating the Master passwd File

The first task in setting up a NIS master server is to prepare the source file for the passwd map. However, be careful with this source file. The source files can be located either in the /etc directory on the master server or in some other directory. Locating the source files in /etc is undesirable because the contents of the maps are then the same as the contents of the local files on the master server. This is a special problem for passwd and shadow files, because all users would have access to the master server maps and because the root password would be passed to all YP clients through the passwd map.

Sun recommends that for security reasons, and to prevent unauthorized root access, the files used to build the NIS password maps should not contain an entry for root. Therefore, the password maps should not be built from the files located in the master server's /etc directory. The password files used to build the passwd maps should have the root entry removed from them, and they should be located in a directory that can be protected from unauthorized access.
