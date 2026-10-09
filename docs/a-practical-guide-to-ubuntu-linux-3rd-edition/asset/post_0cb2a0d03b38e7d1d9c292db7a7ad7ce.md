
local configuration information and NIS source information.) An NIS server can include information from as many of the following source files as is appropriate:

- `/etc/group` Defines groups and their members
- `/etc/gshadow` Provides shadow passwords for groups
- `/etc/hosts` Maps local systems and IP addresses
- `/etc/passwd` Lists user information
- `/etc/printcap` Lists printer information
- `/etc/rpc` Maps RPC program names and numbers
- `/etc/services` Maps system service names and port numbers
- `/etc/shadow` Provides shadow passwords for users

The information that NIS offers is based on files that change from time to time. NIS is responsible for making the updated information available in a timely manner to all systems in the NIS domain.

Before NIS can store the information contained in a source file, it must be converted to a dbm (page 1144) format file called a map. Each map is indexed on one field (column). Records (rows) from a map can be retrieved by specifying a value from the indexed field. Some files generate two maps, each indexed on a different field. For example, the `/etc/passwd` file generates two maps: one indexed by username, the other indexed by UID. These maps are named `passwd.byname` and `passwd.byuid`, respectively.

> NIS maps correspond to C library functions. The `getpwnam()` and `getpwuid()` functions obtain username and UID information from `/etc/passwd` on non-NIS systems. On NIS systems, these functions place RPC calls to the NIS server in a process that is transparent to the application calling the function.

The names of the maps NIS uses correspond to the files in the `/var/yp/nisdomainname` directory on the master server, where `nisdomainname` is the name of the NIS domain. The examples in this chapter use the NIS domain named mgs:

```
$ ls /var/yp/mgs
group.byuid   netgroup.byhost  protocols.byname   services.by servicename
group.byname   netgroup.byuser  protocols.bynumber  shadow.byname
hosts.byaddr   netid.byname     rpc.byname         ypservers
hosts.byname   passwd.byname    rpc.bynumber
netgroup       passwd.byuid     services.byname
```

To make it easier to refer to NIS maps, you can assign nicknames to them. The `/var/yp/nicknames` file on both clients and servers holds a list of commonly used nicknames:

```
$ cat /var/yp/nicknames
    passwd          passwd.byname
    group           group.byname
    networks        networks.byaddr
    hosts           hosts.byname
    protocols       protocols.bynumber
    services        services.byname
    aliases         mail.aliases
    ethers          ethers.byname
```

You can also use the command `ypcat -x` to display the list of nicknames. Each line in **nicknames** contains a nickname followed by whitespace and the name of the map corresponding to the nickname. You can add, remove, or modify nicknames by changing the **nicknames** file.

The `ypcat` and `ypmatch` utilities display information from the NIS maps on the server. Using the nickname **passwd**, the following command, which you can run on any NIS client in the local domain, displays the information contained in the **passwd.byname** map:

```
$ ypcat passwd
sam:x:1000:1000:Sam,,,:/home/sam:/bin/bash
sls:x:1001:1001:Sam the Great,,,:/home/sls:/bin/bash
...
```

By default, NIS stores passwords only for users with UIDs greater than or equal to 1000 (see **MINUID** on page 753). Thus `ypcat` does not display lines for **root**, **bin**, and other system entries. You can display password information for a single user with `ypmatch`:

```
$ ypmatch sam passwd
sam:x:1000:1000:Sam,,,:/home/sam:/bin/bash
```

You can retrieve the same information by filtering the output of `ypcat` through `grep`, but `ypmatch` is more efficient because it searches the map directly, using a single process. The `ypmatch` utility works on the key for the map only. To match members of the group or other fields not in a map, such as the **GECOS** (page 1150) field in **passwd**, you need to use `ypcat` and `grep`:

```
$ ypcat passwd | grep -i great
sls:x:1001:1001:Sam the Great,,,:/home/sls:/bin/bash
```

This chapter uses the following definitions:

- **NIS source files** The ASCII files that NIS obtains information from
- **NIS maps** The dbm-format files created from NIS source files
- **NIS database** The collection of NIS maps

## MORE INFORMATION

**Local** man pages: **domainname**, **makedbm**, **netgroup**, **revnetgroup**, **ypbind**, **ypcat**, **ypinit**, **ypmatch**, **yppasswd**, **yppoll**, **yppush**, **ypset**, **ypservcr**, **ypserv.conf**, **ypwhich**, **ypxfr**, **ypxfrd**

**Web** www.linux-nis.org
*NIS-HOWTO*

## RUNNING AN NIS CLIENT

This section explains how to set up an NIS client on the local system.

### PREREQUISITES

- `nis`
- `portmap` (installs automatically with nis)

When you install the **nis** package, the **dpkg postinst** script starts an NIS client. See the "nis init script" section below if you want to start an NIS server or do not want to start an NIS client. The **dpkg postinst** script asks you to specify the NIS domain name of the local system if it does not find one in `/etc/default/domain`. If necessary, the script creates this file and stores the NIS domain name in that file. If this file does not exist, the NIS client (ypbind) will not start. If there is a server for the domain you specify, the client quickly binds to that server.

If there is no NIS server for the NIS client to bind to when you install or start an NIS client or boot the system, the client spends several minutes trying to find a server, displaying the following message while doing so:

```
Setting up nis (3.17-14ubuntu2) ...
* Setting NIS domainname to: mgs
* Starting NIS services
* binding to YP server...
* ...
* ...
```

Finally the client (ypbind) gives up on finding a server and runs in the background in broadcast mode:

```
$ ps -ef | grep ypbind
root        16832     1  0 19:33 ?          00:00:00 /usr/sbin/ypbind -broadcast
sam        17390  5839  0 19:38 pts/0      00:00:00 grep ypbind
```

Broadcast mode is less secure than other modes because it exposes the system to rogue servers by broadcasting a request for a server to identify itself. If ypbind starts in this mode, it is a good idea to restart it after you set up an NIS server (page 750) and configure an NIS client as explained in the next section.

After you configure **nis**, call the nis init script to restart **nis**. However, as explained earlier, starting **nis** takes a while if it cannot connect to a server. The `/etc/default/nis` file specifies whether this script starts an NIS client, server, or both:

```
$ sudo service nis restart
```

After changing the **nis** configuration on an active server, use **reload** in place of **restart** to reload **nis** configuration files without disturbing clients connected to the server.

### NOTES

If there is no NIS server for the local system’s NIS domain, you need to set one up (page 750). If there is an NIS server, you need to know the name of the NIS domain the system belongs to and (optionally) the name or IP address of one or more NIS servers for the NIS domain.

An NIS client can run on the same system as an NIS server.

**/etc/default/nis** The `/etc/default/nis` file controls several aspects of NIS running on the local system, including whether the nis init script starts a client, a server, or both. As installed, this file causes the nis init script to start an NIS client (ypbind) and not to start an NIS server (ypserv). Set NISSERVER to *false* if the local system is not an NIS server or to *master* or *slave* as appropriate if it is a server. Set NISCLIENT to *true* if the local system is an NIS client; otherwise set it to *false*.

```
$ head /etc/default/nis

# Are we a NIS server and if so what kind (values: false, slave, master)?
NISSERVER=false

# Are we a NIS client?
NISCLIENT=true
```

In the nis file you can also specify which ports the NIS server uses (refer to “Firewall” on page 751) and control which values in `/etc/passwd` users can modify (refer to “Allow GECOS and Login Shell Modification” on page 757).

## CONFIGURING AN NIS CLIENT

This section lists the steps involved in setting up and starting an NIS client.

### /etc/defaultdomain: Specifies the NIS domain name

**A DNS domain name is different from an NIS domain name**

> The DNS domain name is used throughout the Internet to refer to a group of systems. DNS maps these names to IP addresses to enable systems to communicate with one another.
> 
> The NIS domain name is used strictly to identify systems that share an NIS server and is normally not seen or used by users and other programs. Although some administrators use one name as both a DNS domain name and an NIS domain name, this practice can degrade security.

The `/etc/defaultdomain` file stores the name of the NIS domain the local system belongs to. If you change this value, you need to reload the client and/or server daemon to get NIS to recognize the change. The nis init script reads the defaultdomain file and sets the name of the system’s NIS domain. If the defaultdomain file does not exist when you install NIS, the dpkg postinst script prompts for it (refer to “Install” on page 745). You can use the nisdomainname utility to set or view the NIS domain name, but setting it in this manner does not maintain the name when the nis init script is executed (for example, when the system is rebooted):

```
$ sudo nisdomainname
(none)
$ sudo nisdomainname mgs
$ sudo nisdomainname
mgs
```

![](img/2344fc4a798f29dca9e8b5ed7288171a_795_0.png)

![](img/2344fc4a798f29dca9e8b5ed7288171a_795_1.png)

![](img/2344fc4a798f29dca9e8b5ed7288171a_795_2.png)
