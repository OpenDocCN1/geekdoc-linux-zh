firewall can limit the ways an intruder may break into your Linux system. Here are your choices for configuring a firewall during installation:

+   - **Disabled** — Select this security level if you are not connected to a public network and do not want to deny requests for services from any computer on your local network. Of course, you can still restrict access to services by starting up only the services you want to offer and by using configuration files to restrict access to individual services.

+   - **Enabled** — Select this security level if you are connecting your Linux system to the Internet for Web browsing and file downloading (FTP). By default, only services needed to allow Web browsing and basic network setup, DNS replies, and DHCP (to serve addresses) are allowed at this level.

+   - **Trusted Services** — If you enable the firewall and you know you want to allow access to particular services, you can click the appropriate check boxes and allow incoming requests for the following services: SSH (secure shell to allow remote login), NFS4 (network file system file sharing) Telnet (an insecure method of remote login), WWW HTTP (standard Web server) Secure WWW HTTPS (act as a Web server), Mail SMTP (act as a mail server), or FTP (act as an FTP server).

+   - **Other Ports** — To allow incoming requests on other ports, click the down arrow and select Add. Enter the port number for the services you want to open access to on your computer and select the protocol (TCP or UDP).

> **TIP:** *Adding firewall rules here results in rules being added to the* /etc/sysconfig/iptables *file. The rules are run from the* /etc/init.d/iptables *start-up script when you boot your system. To make permanent changes to your firewall rules and to SELinux features, you can use the Security Level Configuration window, as described in Chapter 14.*

+   - **SELinux** — On the SELinux screen you can select to Enable SELinux (Enforcing), have it disabled but warn you when requests would be denied (Permissive), or have it turned off (Disabled). SELinux has improved enough to leave it enabled in most cases.
+   
+   Most of the restrictions SELinux puts on your system, by default, apply if you are turning on network services such as CUPS, Samba, NFS, or HTTP. Therefore, if you are setting up a server, you should look carefully at the limitations SELinux puts on your server before enabling it. (See Chapter 10 for information about SELinux.)

+   - **Date and Time Configuration** — You can manually enter the date (click the calendar) and time (select hour, minutes, and seconds) or use the Network Time Protocol tab to have your date and time set automatically from a known time server. Click Enable Network Time Protocol (NTP) to start the ntpd daemon. Network Time Protocol (NTP) is a service that allows computers to synchronize their date and time clocks with reliable time servers. Fedora offers several servers from the virtual clusers available from the *pool.ntp.org* site (*0.fedora.pool.ntp.org*, *1.fedora.ntp.org*, etc.).