
```text
Listing 19.1  The Contents of the /etc/nsswitch.nisplus File (continued)

services:   nisplus [NOTFOUND=return] files
networks:   nisplus [NOTFOUND=return] files
protocols:  nisplus [NOTFOUND=return] files
rpc:        nisplus [NOTFOUND=return] files
ethers:     nisplus [NOTFOUND=return] files
netmasks:   nisplus [NOTFOUND=return] files
bootparams: nisplus [NOTFOUND=return] files

publickey:

netgroup:   nisplus

automount:  files nisplus
aliases:    files nisplus
sendmailvars:   files nisplus

printers:   user nisplus files xfn

auth_attr:  files nisplus
prof_attr:  files nisplus
project:    files
```

## Network Information Service (NIS)

NIS, like other network applications, follows the client/server architecture model. The following sections describe the NIS components, how to configure these components, and how to add and update NIS maps.

### NIS Components

NIS consists of a master server, possibly slave servers, and one or more clients. The servers store NIS maps and make the information contained in the maps available to clients on request.

### NIS Maps

NIS stores information in a set of files called *maps*, which are two-column tables. The first column is used as a key, and the second column is the information associated with that key. Because the maps are organized by key, the same information might appear in more than one map. For example, host and associated IP addresses appear in two maps: hosts.byname (the hostname is the key and the IP address is the information) and hosts.byaddr (the IP address is the key and the hostname is the information). Table 19.3 lists the NIS maps, which are physically located under the /var/yp directory along with several other NIS files.

| Keyword | Maps | Description |
|---|---|---|
| aliases | mail.aliases, mail.byaddr | Mail addresses and aliases |
| bootparams | bootparams | Location of root, swap, and dump partitions for diskless workstations |
| ethers | ethers.byaddr, ethers.byname | Ethernet addresses of systems |
| group | group.bygid, group.byname | Group name, group ID (GID), and member information |
| hosts | hosts.byaddr, hosts.byname | Hostnames and network (IPv4) addresses |
| ipnodes | ipnodes.byaddr, ipnodes.byname | Hostnames and network (IPv6) addresses |
| netgroup | netgroup, netgroup.byhost, netgroup.byuser | Network groups and members defined in the domain |
| netmasks | netmasks.byaddr | Netmasks associated with known networks |
| networks | networks.byaddr, networks.byname | Networks and their associated names |
| passwd | netid.byname, passwd.adjunct.byname, passwd.byname, passwd.byuid | Password information for user accounts |
| protocols | protocols.byname, protocols.bynumber | IP protocols used within the domain |
| rpc | rpc.bynumber | RPC program numbers for RPC services used within the domain |
| services | services.byname, services.byservice | IP services and their port numbers |

![](img/b957f979417d9f16274c2eb52c8f2c9f_421_0.png)

NIS was previously known as “Yellow Pages.” For this reason, many of the NIS files and commands contain the yp prefix.

### NIS Master and Slave Servers

Each NIS environment, or domain, must have only one NIS master server. The NIS maps reside on the master server. To provide load distribution and redundancy, one or more slave servers can be configured. Whenever the NIS maps are updated on the master server, they are propagated to the slave servers.

### NIS Clients

NIS clients request information contained in the maps from NIS servers. The clients do not make any distinction between the master server and slave servers.

![](img/b957f979417d9f16274c2eb52c8f2c9f_422_0.png)

NIS servers can also be NIS clients, depending on the configuration of the `/etc/nsswitch.conf` file. Keep in mind that NIS servers also need to resolve hostnames, network addresses, and so on for their own use.

### Configuring NIS Servers and Clients

The procedures used to configure an NIS master server, slave server, and client are somewhat similar. The steps for each procedure are given in the following sections.

Each system should be identified as a member of the domain. You do so by using the **domainname**(1M) command and specifying the domain name as an argument. For example, if a system will be part of the sun.com domain, you use the following command to set the domain:

```sh
# domainname sun.com
#
```

An alternative approach is to enter the domain name in the `/etc/defaultdomain` file.

#### NIS Master Server

Before you can configure an NIS master server, you must prepare the data used to build the maps. By default, the maps will be built from the /etc files. However, it is recommended that you copy the /etc files to another directory so that you can make any necessary changes to these source files without affecting the local system. Use the following procedure to prepare the data:

1. Verify that the /etc files are up to date. These files are auto_home, auto_master, bootparams, ethers, group, hosts, netgroup, netmasks, networks, passwd, protocols, rpc, services, and shadow.
2. Select a directory for building most of the maps (the DIR directory) and another directory for building the passwd map (the PWDIR directory).
3. Copy all the files (except /etc/passwd) to the DIR directory, and copy the /etc/passwd file to the PWDIR directory.
4. Verify that the /etc/mail/aliases file is up to date, but do not copy it to the DIR directory.
5. Remove comments and other unnecessary information from the copied source files. Verify that the file formats are correct.
6. Modify the /var/yp/Makefile to identify the selected DIR and PWDIR directories.

Use the following procedure to configure an NIS master server. As part of the procedure, the maps will be built automatically:

1. To be sure that the system is using the /etc files configuration for the name service switch, copy the /etc/nsswitch.files file to the /etc/nsswitch.conf file.
2. Add entries to /etc/hosts for each NIS slave server.
3. If necessary, use the **domainname**(1M) command to set the domain name.
4. Run the **ypinit**(1M) command to initialize the NIS master server and build the maps, as shown here.
5. Provide the information in response to the prompts from the **ypinit** command. This information includes a list of NIS slave servers and whether the **ypinit** command should exit if an error is encountered.
6. Enable NIS by copying the /etc/nsswitch.nis file to the /etc/nsswitch.conf file.

```
ypinit -m
```

To start the NIS master server, either reboot the system or run the **ypstart**(1M) command, as shown here:

```
/usr/lib/netsvc/yp/ypstart
```

#### NIS Slave Server

You can use the following procedure to configure a system as an NIS slave server:

1. Configure the system as an NIS client. If necessary, use the **domainname** command to set the domain name.
2. Update the /etc/nsswitch.conf file to use NIS by copying the /etc/nsswitch.nis template file to it or by manually editing the appropriate configuration.
3. Log in to the system as the root account and run the **ypinit** command, as shown here:

    ```
    ypinit -c
    ```

4. The **ypinit** command will prompt for one or more NIS servers. Enter the hostnames of the closest NIS servers. This step completes the client setup.
5. Add an entry for the NIS master server to the /etc/hosts file.
6. If the **ypbind**(1M) command is running, stop it by using the following command:

    ```
    /usr/lib/netsvc/yp/ypstop
    ```

7. Restart the **ypbind** command by using the following command:

    ```
    /usr/lib/netsvc/yp/ypstart
    ```

8. Run the **ypinit** command from the /var/yp directory, as shown here (**master** is the hostname of the NIS master server):

    ```
    # cd /var/yp
    # ypinit -s master
    ```

To start the NIS slave server, reboot the system or repeat steps 6 and 7.

Only the maps generated on the master server are copied to the slave server. The original files used to generate the maps reside only on the master server.

#### NIS Client

You can use the following procedure to configure a system as an NIS client:

1. If necessary, use the **domainname** command to set the domain name.
2. Update the /etc/nsswitch.conf file to use NIS by copying the /etc/nsswitch.nis template file to it or by manually editing the appropriate configuration.
3. Log in to the system as the root account and run the **ypinit** command, as shown here:

    ```
    ypinit -c
    ```

4. The **ypinit** command will prompt for one or more NIS servers. Enter the hostnames of the closest NIS servers.
