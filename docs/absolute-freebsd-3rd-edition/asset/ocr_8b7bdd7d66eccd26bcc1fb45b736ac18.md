This means, "Look for IP addresses in the local files first, and then query DNS." The other information sources work similarly. FreeBSD, like most other Unix-like operating systems, supports name service switching for the information sources listed in Table 20-1.

Table 20-1: Lookups Supporting Name Service Switching

| Lookup Function | Description |
| :--- | :--- |
| groups | Group membership checks (*/etc/group*) |
| hosts | Hostname and IP checks (DNS and */etc/hosts*) |
| networks | Network entries (*/etc/networks*) |
| passwd | Password entries (*/etc/passwd*) |
| shells | Checks for valid shells (*/etc/shells*) |
| services | TCP and UDP services (*/etc/services*) |
| rpc | Remote procedure calls (*/etc/rpc*) |
| proto | TCP/IP network protocols (*/etc/protocols*) |

Most of these you don't want to muck with, unless you like breaking system functionality. If you have a Kerberos or an NIS domain, for example, you might want to have your FreeBSD box attach to them for user and group information—but if you don't, reconfiguring the password lookups would make your system slow at best or entirely stop working at worst!

For each name service, you must specify one or more sources of information. Many of these name services are very simple and default to having a single authoritative source of information—a file. Others, such as the host's name service, are more complicated and have multiple sources. A few are very complicated simply because of the vast array of information available and the many possible ways to get that information. As this book doesn't cover Kerberos, NIS, or any other enterprise-level user management systems, we won't cover changing password, group, and shell information sources. If you're in such an environment, read nsswitch.conf(5) for details.