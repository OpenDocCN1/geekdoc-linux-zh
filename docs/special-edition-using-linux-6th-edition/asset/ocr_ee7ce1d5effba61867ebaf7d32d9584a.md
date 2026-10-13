| Command | Syntax (Example) | Description |
|---|---|---|
| ifconfig | ifconfig | Displays currently configured network interfaces. |
|  | ifconfig [interface] [options] | Configures a network interface. |
| netstat | netstat | Displays the status of network connections, routing tables, and interface statistics. |
| ping | ping <host> | Sends an ECHO_REQUEST packet to the specified host. A response packet is returned by reachable hosts. Commonly used to debug network connections. |
| nslookup | nslookup | A name server lookup utility. Used to query Domain Name Servers. |
| route | route | Displays the current configuration of the routing table. |
|  | route [options] | Configures the IP routing table. |
| traceroute | traceroute <host> | Displays the route of IP packets. Useful for debugging network problems. |

# SYSTEM UTILITIES

| Command | Syntax (Example) | Description |
|---|---|---|
| chage | chage [option] user | Changes password aging. |
| chgrp | chgrp <group> <file> | Changes the group to which a file belongs. |
| chmod | chmod <mode> <file> | Changes the access permissions of the specified file or files. |
| chown | chown <owner> <file> | Changes the owner of a given file or files. |
| coastool | coastool | Uses COAS to manage the system. |
| date | date | Displays the system date setting. |
|  | date <MMDDhhmmYY> | Sets the date. |
|  |  | MM = month |
|  |  | DD = day |
|  |  | hh = hour (Military) |
|  |  | mm = minute |
|  |  | yy = year |
| df | df | Displays a summary of free disk space for a given filesystem. |
| dmesg | dmesg | Displays the startup messages from the last system boot. |