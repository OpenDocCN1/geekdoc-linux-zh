TABLE 9.8: NETWORK SERVICES DAEMONS (CONTINUED)

| Daemon | Function |
| :--- | :--- |
| `in.telnetd` | Allows same login procedure for local login and remote |
| `in.tftpd` | Used to boot or get information from a network; launched by `inetd` |
| `in.uucpd` | Unix-to-Unix copy; launched by `inetd` |
| `kerbd` | MIT's Kerberos, securely authenticates local and remote users |
| `named` | Supports the domain name service |
| `nfsd, statd, lockd, mountd, rquotad` | All work together to handle NFS operations; found in `/usr/1ib/fs/nfs` |
| `nscd` | Name service cache; requests data obtained from the pwswd, hosts |
| `pwerd` | Manages automatic and low-power shutdowns |
| `rdis c` | Router discovery service that runs with one interface |
| `routed` | Manages the routing tables for messages for distant networks |
| `rpcbind` | Integral to Solaris; maps incoming requests for RPC service numbers |
| `rpc.bootparamd` | Used on systems with a jumpstart server for new installations |
| `rpc.cmsd` | Used by calendar tools for remote or central distribution of calendars |
| `rpc.nisd` | Runs on IIS+ masters and handles requests for NIS+ databases |
| `rpc.rexd` | A poor service that should be commended out; security risk high |
| `rpc.rstatd` | Collects info about local system |
| `rpc.sprayd` | Handles connections from the spray utility; launched by `rpc.ttdb-serverd`; used by Tooltalk services for intertolnt communication |
| `sendmail` | De facto mail transfer program on the Internet |
| `syslogd` | System log; transcribes important system events |
| `utmpd` | Keeps the `/etc/utmp` and `/var/adm/utmp` files updated |
| `wall d` | Sends messages to all users logged in on all machines |
| `Xaserver` | X Window System daemon; plays sound over the network |
| `Xntpd` | Network time protocol; synchronizes with network time |
| `ypserv, ypxfrd, ypbind, rpc.yp passwd` | YP/NIS server package on Solaris operating system CD-ROM |

# Remote User Mail

If you know the name of the remote system or its domain and you know a user's login name, you can use an electronic mail program to send a message over the network