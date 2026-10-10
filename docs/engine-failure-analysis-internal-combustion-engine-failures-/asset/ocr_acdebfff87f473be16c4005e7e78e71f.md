# AT A GLANCE (CONT.)

| How Do I | See This Entry | Example |
| --- | --- | --- |
| Display information about all the TCP/IP sockets currently in operation? | `netstat` | `netstat -a` |
| Look up the numerical address for a domain name? | `nslookup` | `nslookup www.yahoo.com` |
| Determine whether external Internet services are available? | `ping` | `ping www.yahoo.com` |
| Copy a file to a remote server (for which I have appropriate permissions)? | `rpc` | `rcp essay1.doc essay1.bak@lothlorien:/home/suzanne/Documents/Backup` |
| Determine whether the NFS daemons are running? | `rpcinfo` | `rpcinfo -p` |
| View available NFS shares? | `showmount` | `showmount -a` |
| Mount a Samba share on a remote system? | `smbmount` | `smbmount //lothlorien/suzanne /home/suzanne/lothlorien` |
| Display the status of Samba networking? | `smbstatus` | `smbstatus -d` |
| Unmount a remote Samba share? | `smbumount` | `smbumount //lothlorien/suzanne /home/suzanne/lothlorien` |
| Connect to a remote Telnet service? | `telnet` | `telnet lothlorien.myetwork.org` |

# Configuring Networking and Internet Settings

Linux includes a full implementation of the TCP/IP protocol suite, the communication standards that underlie the operation of the public Internet. You can also use TCP/IP to set up internal networks (called local area networks or LANs) that use the same protocols. To connect your Linux system to a computer network using TCP/IP, you