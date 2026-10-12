+   • /etc/passwd — Defines the users who have accounts set up on the computer.

+   • /etc/shadow — Contains encrypted passwords for the users set up in the /etc/passwd file.

+   • /etc/gshadow — Contains encrypted passwords associated with groups contained in the /etc/group file. (This file is optional and is usually not used.)

+   • /etc/passwd.adjunct — Secures password entries if your system doesn’t use shadow passwords. (This file is used with SunOS systems.)

+   • /etc/aliases — Contains user aliases used with e-mail. It allows mail that is sent to a particular user name to be directed to a different user (or set of users). On some systems, this file may be /etc/mailaliases instead.

+   • /etc/ethers — Used by the RARP to map Ethernet addresses into IP numbers. This file is optional. (By default, RARP support is not configured in Fedora.)

+   • /etc/bootparams — Contains entries needed to start diskless workstations (typically used to boot Sun Microsystems diskless workstations).

+   • /etc/hosts — Contains the names and IP addresses of computers that can be reached on TCP/IP networks. (Often used to contain all the addresses for a private LAN, while Internet addresses would be determined from a DNS server.)

+   • /etc/networks — Used to attach a name to a network. In this way, you can refer to networks by name rather than by number.

+   • /etc/printcap — Contains printer definitions.

+   • /etc/protocols — Identifies numbers that are assigned to different Internet network protocols (such as IP, TCP, UDP, and others).

+   • /etc/publickey — Used on some UNIX systems to contain user names and associated public and private keys for secure networking in NFS and related features.

+   • /etc/rpc — Contains listings of supported Remote Procedure Call (rpc) protocols. These protocols are used with Sun Microsystems UNIX systems to allow requests for network services, such as NIS and others.

+   • /etc/services — Contains listings that identify port number and protocols for supported network services that are used with Internet protocols.

+   • /etc/netgroup — Used to define users (from particular hosts and domains) for permission-checking associated with remote mounts, remote shells, and remote logins.

+   • /etc/netid — Contains information that maps RPC network names to UNIX credentials.

> NOTE: Some of the files just shown may not be applicable to your Fedora system. Don’t worry if some of these files don’t exist. In the course of setting up your system (adding users, configuring networks, and so on), you will set up the files you need.