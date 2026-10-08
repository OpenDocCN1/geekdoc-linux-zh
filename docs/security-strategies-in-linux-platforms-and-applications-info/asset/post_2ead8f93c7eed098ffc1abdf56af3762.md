
| TABLE 6-2 continued |
| SERVICE SCRIPT | DESCRIPTION | ACTION |
| :--- | :--- | :--- |
| netconsole | For remote recording of kernel panic messages; may disable until kernel panic issue becomes difficult. | Disable |
| netfs | For system mounting of remotely shared directories from NFS and Samba servers. | Depends |
| netplugd | A daemon that monitors connections to LANs. | Depends |
| network | For basic networking. | Enable |
| NetworkManager | Automates switching between network connections; useful for systems with wired and wireless connections. | Disable |
| nfs | Required for shared Network File System (NFS) connections. | Disable |
| nfslock | For the NFS file-locking service. | Disable |
| nscd | Name service caching daemon (NCSD) for networked authentication services. | Enable |
| pand | For Bluetooth connections to Ethernet networks. | Disable |
| pcscd | Smartcard support. | Depends |
| portmap | To convert remote procedure call (RPC) numbers to TCP/IP ports; used by NFS and the Network Information Service (NIS). | Disable |
| psacct | For kernel process accounting log files. | Enable |
| rawdevices | For connections to Oracle databases. | Disable |
| rc.local | Runs commands in /etc/rc.local; avoid if possible. | Depends |
| rdisc | For router discovery. | Depends |
| readhead_early | Loads programs during the boot process; the NSA recommends disabling. | Disable |
| readhead_late | Loads programs during the boot process; the NSA recommends disabling. | Disable |
| restore | SELinux monitor for files. | Enable |
| rhnsd | Red Hot Network (RHN) action monitor, needed if you administer this system from RHN. | Enable |
| rpcgssd | Supports credential searches for NFS. | Disable |
| rpcidmap | The NFS name-mapping daemon. | Disable |
| rpcscgssd | Server-side credential searches for NFS. | Disable |

## CHAPTER 6 | Every Service Is a Potential Risk

| TABLE 6-2 continued |
| SERVICE SCRIPT | DESCRIPTION | ACTION |
|---|---|---|
| saslauthd | Simple authentication and security layer service, used for some services such as sendmail. | |
| sendmail | An open source Simple Mail Transfer Protocol (SMTP) e-mail service. | Depends |
| smartd | Monitor for modern hard drives. | Enable |
| sshd | SSH server. | Enable |
| syslog | Log service. | Enable |
| wpa_supplicant | Wireless network access. | Disable |
| x11-common | Filesystem infrastructure for additional GUI software. | Disable |
| xinetd | Extended internet server. | Disable |
| ybind | Binding for NIS clients and servers. | Depends |
| yum-updatesd | Automatic updates. | |

If the service noted in Table 6-2 is to be disabled, look at the description. You may actually need the service; if so, be aware of the risks. If the rationale applies to your system, try to uninstall the first service. Unless the process also uninstalls something important, proceed with uninstalling the service. Otherwise, stop the service with the script in the /etc/init.d/ directory. Disable the service in all runlevels with the chconfig or update-rc command described earlier.

If you're having trouble identifying the name of the service, the rpm -q command can help. For example, on Red Hat systems, the following command identifies the bluez-utils package as the owner of the bluetooth service script in the /etc/init.d/ directory.

```
# rpm -qf /etc/init.d/bluetooth
```

The best-practice status of a few services is in dispute. For example, while the NSA suggests that the Hardware Abstraction Layer daemon be disabled, documentation from the Red Hat Magazine suggests otherwise. While many distributions are aggressively moving toward IPv6, the NSA suggests most administrators should avoid that network standard. In a similar fashion, while Red Hat recommends to keep the Kudos hardware-probing service active, the NSA disagrees.

Several services are related to NFS. If you do not have a reason to use NFS for sharing directories, you should disable NFS and related services, nfs, nfslock, rpcbind, rpcsvgssd, and rpcmbind.

> NOTE: As of this writing, Red Enterprise Linux 6 suggests its beta release phase. Indications so far suggest that fewer services will be enabled by default this distribution release.

## Managing Super Servers and Deactivating Service Scripts

Two different Linux daemons are associated with the term "super server." While the first super server was configured in the /etc/inetd.conf file, it is still used on occasion on Ubuntu systems. But for most Linux distributions, the regular super server is obsolete. The current version known as the extended internet super server, configured in the /etc/xinetd.conf configuration file. Both super servers are designed as a single daemon that watches for connections on multiple ports, on behalf of multiple services. Both super servers are controlled by scripts in the /etc/inetd/ directory.

In most cases, both super servers communicate using Transmission Control Protocol (TCP) packets. As such, they can be protected with TCP Wrappers control files, as discussed in Chapter 7.

The /etc/inetd/ directory is important because it includes services that are started in various runlevels. Take a look at this directory on a standard (not) Red Hat or Ubuntu system. With a few exceptions, it includes scripts that control not only the super server, but also most regular services. Many Linux developers have been migrating to.

## The Original Server

The original super server was configured in the /etc/inetd.conf file. It is still used on occasion on Ubuntu systems. But for most Linux distributions, the regular super server is obsolete. The current version known as the extended internet super server, configured in the /etc/xinetd.conf configuration file. Both super servers are designed as a single daemon that watches for connections on multiple ports, on behalf of multiple services. Both super servers are controlled by scripts in the /etc/inetd/ directory.

In most cases, both super servers communicate using Transmission Control Protocol (TCP) packets. As such, they can be protected with TCP Wrappers control files, as discussed in Chapter 7.

The /etc/inetd/ directory is important because it includes services that are started in various runlevels. Take a look at this directory on a standard (not) Red Hat or Ubuntu system. With a few exceptions, it includes scripts that control not only the super server, but also most regular services. Many Linux developers have been migrating to.

## The Extended Super Server

The extended internet super server is known by its daemon, xinetd. It is configured in the /etc/xinetd.conf. Both super servers are designed as a single daemon that watches for connections on multiple ports, on behalf of multiple services. Both super servers are controlled by scripts in the /etc/inetd/ directory.

In most cases, both super servers communicate using Transmission Control Protocol (TCP) packets. As such, they can be protected with TCP Wrappers control files, as discussed in Chapter 7.

| TABLE 6-3 Directives from /etc/xinetd.d/vmware-authd. |
| DIRECTIVE | EXPLANATION |
|---|---|
| disable=no | The service is enabled, as long as xinetd is also running. |
| port=902 | Communication is on TCP/IP port 902. |
| socket_type=stream | For stream communication. |
| protocol=tcp | Communication with TCP packets. |
| wait=no | For a multi-threaded service. |
| user=root | Owned by the root administrative user, which may be a risk. |
| server=/usr/sbin/vmware-authd | The location of the actual daemon. |
| type=unlisted | Required when the TCP/IP port is not listed in /etc/services. |

The xinetd.conf file frequently includes logging information and access restrictions. Directives as the following can limit attacks. This directive makes a client wait 10 seconds after 50 attempts:

- cps = 50 10
- instances = 50

This instances directive limits the number of total simultaneous connections: ownThe per_source directive limits the number of simultaneous connections by source:
per_source = 10

## Regular Service Scripts

Regular service scripts are located in the /etc/init.d/ directory. With rare exceptions, these scripts can be used to at least start, stop, and restart a service. As these scripts are all text files, you should take a look. At the end of each of these scripts, you'll see a full list of available control commands. such as start, stop, restart, and status. For example, the following command stops and restarts the Samba service on a Red Hat system whether or not Samba is already running:

```
# /etc/init.d/smb restart
```
