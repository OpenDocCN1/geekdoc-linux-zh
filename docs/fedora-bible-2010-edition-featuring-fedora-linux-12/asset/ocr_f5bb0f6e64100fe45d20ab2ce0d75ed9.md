466 **Part III: Adminstering Fedora**

| Run-Level Scripts | What Does It Do? |
|---|---|
| httpd | Starts the **httpd** daemon, which allows your computer to act as an HTTP server (that is, to serve Web pages). |
| ip6tables | Starts the *ip6tables* firewall daemon, which manages any *iptables*-style firewall rules set up for your computer for IPv6 networking. |
| iptables | Starts the *iptables* firewall daemon, which manages any *iptables*-style firewall rules set up for your computer. |
| killall | Shuts down any subsystems that may still be running prior to a shutdown or reboot. |
| ldap | Starts the Lightweight Directory Access Protocol daemon (**slapd**), which listens for LDAP requests from the network. |
| messagebus | Runs the dbus-daemon for broadcasting system message to nterested applications. |
| mysqld | Runs the MySQL database daemon (**mysqld**) to listen for requests to MySQL databases. |
| named | Starts and stops the BIND DNS server daemon (**named**) to listen for and resolve domain name system requests. |
| netfs | Mounts or unmounts network (NFS, SMB, and NCP) file systems. |
| network | Starts or stops all configured network interfaces and initializes the TCP/IP and IPX protocols. |
| NetworkManager | Switches automatically to the best available network connections. |
| nfs | Starts or stops the NFS-related daemons (**rpc.nfsd**, **rpc.mountd**, **rpc.statd**, and **rpc.rquotad**) and exports shared file systems. |
| ntpd | Runs the Network Time Protocol daemon (**ntpd**), which synchronizes system time with Internet standard time servers. |
| openvpn | Runs the OpenVPN virtual private network service. |
| portmap | Starts or stops the **portmap** daemon, which manages programs and protocols that utilize the Remote Procedure Call (RPC) mechanism. |
| routed | Starts or stops the **routed** daemon, which controls dynamic-routing table updates via the Router Information Protocol (RIP). |
| rsyslog | Starts or stops the **klogd** and **syslogd** daemons that handle ogging events from the kernel and other processes, respectively. |
| sendmail | Controls the **sendmail** daemon, which handles incoming and outgoing SMTP (Simple Mail Transport Protocol) mail messages. |
| smb | Starts or stops the **smbd** and **nmbd** daemons for allowing access to Samba file and print services. |
| snmpd | Starts or stops the **snmpd** (Simple Network Management Protocol) |