# Understanding Network Information Service

Network Information Service (NIS) was created by Sun Microsystems as a way of managing information that is shared among a group of host computers on a network. Using NIS, computers can share a common set of user accounts, user groups, and TCP/IP host names, as well as other information.

> **NOTE:** NIS was originally called Yellow Pages, but Sun had to change this name because it was trademarked. Some people still refer to NIS as \emph{YP}, and many of the NIS commands (and even NIS package names) begin with the letters \emph{\textquotesingle{}yp.\textquotesingle{}}

The information you share with NIS comes from files that are used with UNIX systems and, therefore, compatible with other UNIX-like systems, such as Red Hat Linux. The group of computers that the master NIS server supports is referred to as an NIS domain. This domain is a defined set of host computers that may or may not be the same group of computers contained in a TCP/IP domain.

With NIS, an administrator creates information databases called \emph{maps} from common UNIX (or Linux) system files. The NIS maps are created on the \emph{master NIS server} and are accessible to other host computers from that server. Just in case the master server is down or inaccessible, one or more slave servers can be defined. The NIS slave servers contain copies of the NIS maps and can provide that information to client computers when the master is unavailable. However, NIS slave servers are not used to create the maps.

When the maps have been shared among the computers in the NIS domain, the main result is that all the computers share a common set of users and network configuration. The following is a list of files that are available for sharing by NIS (not all of them are set up for sharing by default).

+   *   `/etc/group` — Defines the groups to which users on the computer belong.
+   *   `/etc/passwd` — Defines the users who have accounts set up on the computer.
+   *   `/etc/shadow` — Contains encrypted passwords for the users set up in the `/etc/passwd` file.
+   *   `/etc/gshadow` — Contains encrypted passwords associated with groups contained in the `/etc/groups` file. (This file is optional and is usually not used.)
+   *   `/etc/passwd.adjunct` — Secures password entries if your system doesn’t use shadow passwords. (This file is used with SunOS systems.)
+   *   `/etc/aliases` — Contains user aliases used with mail. It allows mail that is sent to a particular user name to be directed to a different user (or set of users). On some systems, this file may be `/etc/mailaliases` instead.
+   *   `/etc/ethers` — Used by the RARP to map Ethernet addresses into IP numbers. This file is optional. (By default, RARP support is not configured into Red Hat Linux.)