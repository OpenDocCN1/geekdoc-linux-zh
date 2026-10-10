
zone information. The location of the chrooted DNS configuration files in Fedora (/var/named/chroot) is set in the /etc/sysconfig/named file.

> **NOTE:** If you run BIND in a non-chrooted environment, configuration files are located in /etc/named.conf file and the /var/named directory. You must uninstall the bind-chroot package to do this.

*   **DNS lookup tools** — You can use several tools to check that your DNS server is resolving hostnames properly. These include commands such as host, dig, and nslookup (which are part of the bind-utils software package).

To maintain your DNS server correctly, you can also perform the following configuration tasks with your DNS server:

*   **Logging** — You can indicate what you want to log and where log files reside.
*   **Remote server options** — You can set options for specific DNS servers to perform tasks such as blocking information from a bad server, setting encryption keys to use with a server, or defining transfer methods.

You don't need to give out DNS information to everyone who requests it. You can restrict access to those who request it based on the following:

*   **Access control list (acl)** — This list can contain those hosts, domains, or IP addresses that you want to group together and apply the same level of access to your DNS server. You create acl records to group those addresses, and then indicate what domain information the locations in that acl can or can't access.
*   **Listen-on ports** — By default, your name server accepts only name server requests that come to port 53 (TCP and UDP) on your name server. You can add more port numbers if you want your name server to accept name service queries on different ports.
*   **Authentication** — To verify the identities of hosts that are requesting services from your DNS server, you can use keys for authentication and authorization. (The key and trusted-keys statements are used for authentication.)

> **CROSS-REFERENCE:** You should already know what domain names and IP addresses are. Refer to Chapter 14 for IP addresses and Chapter 15 for DNS information if you need to refresh your memory.

## DNS name server example

To get an idea of what you need to set up your DNS server, the following sections step you through an example of a DNS server for a domain called yourdomain.com. In the example, you're creating a DNS server for a small office network that includes the following:

*   A private, local network that resides behind a firewall
*   A server providing DNS service

In this office, other computers on the LAN are using the same Internet connection for outgoing communications, so the firewall on the server does network address translation (NAT) to enable the client computers to use the firewall as a router to the Internet. Figure 24-1 shows the configuration of the example *yourdomain.com* domain.

Figure 24-1 illustrates a small office network that’s sharing a single Internet connection. The DNS, Web, mail, and FTP servers all have public IP addresses. (These addresses are fictitious, so please don’t try to use them.) Behind the DNS server (which is also operating as a firewall) are four client computers that have private IP addresses. (You can reuse these addresses and other private addresses that I describe in Chapter 14.)

> **NOTE:** Because this is an example of how DNS works, it doesn’t deal with all the complexities you might face in setting up the computing infrastructure at your company. In particular, you will probably want to separate routing and firewall features from your DNS server. Often, DNS and other servers are placed into what is referred to as a demilitarized zone (DMZ) that is separated from the company LAN.

![](img/c78bdcb5b7842a0d73dcc98921f872a2_914_0.png)

**Figure 24-1:** The sample *yourdomain.com* DNS server has a combination of public servers and private client computers.

The job of the DNS server, in this configuration, is to map the names of the public servers (*www.yourdomain.com*, *mail.yourdomain.com*, *ftp.yourdomain.com*, and *ns1.yourdomain.com*) into the static IP addresses that the ISP assigns (123.45.67.1, 123.45.67.2, 123.45.67.3, 123.45.67.89, in our example). The DNS server also provides DNS service from the private addresses on the LAN, so each computer can reach the others on the LAN without needing to store all computer names in their own /etc/hosts file.

A key feature to this example is that it divides the view of this domain between what the outside world can see and what the computers on the private network can see. Using the `view` feature of BIND, I create an *outside* view that lets queries from the Internet find only public servers (Web, Mail, and FTP) in the domain. Then I create an *inside* view that lets queries from the local LAN find both the public servers and private computers (red, blue, green and yellow) in the domain.

The sections that follow describe how to set up a DNS server for the example in Figure 24-1.

## Quick-starting a DNS server

The DNS server software that comes with the current Fedora version is Berkeley Internet Name Domain (BIND) version 9.6. To configure BIND 9.6, you work with the following components:

*   **Configuration file** (`/var/named/chroot/etc/named.conf`) — The main DNS server configuration file.
*   **Zone directory** (`/var/named/chroot/var/named`) — The directory containing files that keep information about Internet root DNS servers (`named.ca` file) and information about the zones that you create for your DNS server.
*   **Daemon process** (`/usr/sbin/named`) — The daemon process that listens for DNS requests and responds with information that the `named.conf` file presents.
*   **Debugging tools** (`named-checkconf`, `named-checkzone`, and `named-compilezone`) — What you use to determine whether you created your DNS configuration correctly.

> **NOTE:** Fedora comes with a GUI tool for configuring BIND called `system-config-bind`. (Type `yum install system-config-bind` to install it.) If you decide to use that tool, you need to be careful editing the BIND configuration files by hand. It is recommended that if there are changes you want to make to the `named.conf` file that are not supported by the `system-config-bind` window, you should put those changes in the `/etc/named.custom` file instead.

BIND 9.6 also includes tools for creating DNSSEC secured zones. By using these tools, you can create and generate keys to provide authentication and secure address resolution. The example illustrated in these sections doesn't include DNSSEC configuration.

The basic steps in creating a DNS server for your example are as follows:

*   Identifying your DNS servers
*   Creating DNS Configuration files (`named.conf` file and the `named` directory)
*   Starting the named daemon
*   Monitoring named activities

In the example configuration, you set up a primary master DNS server and a slave DNS server. The primary server holds the master copy of the authoritative records for the domain. The secondary server is there to share requests for information about the domain, particularly in case the primary goes down. The secondary (slave) typically gets its records from the primary server. The secondary is also considered to be authoritative in regards to the DNS records for the domains it controls. You can have multiple secondary (slave) DNS servers defined.

### Identifying your *DNS* servers

If you didn't have your *DNS* servers set up at the time that you purchased your domain name with a registration authority, you might have just “parked” the domain name there until you configured your *DNS* servers. Whenever you're ready to set up your DNS servers, return to that registration authority and provide the following information about your DNS servers:

*   DNS server IP addresses (the static IP addresses of your DNS servers, probably primary and slave)
*   DNS server hostnames (often *ns1.yourdomain.com*, where you replace *yourdomain.com* with your domain name for the primary; the slave hostname is *ns2.yourdomain.com*)

You should register both the primary and slave DNS servers. After you update this record, that information typically takes a day or two to propagate throughout the Internet. When your DNS servers are registered, you also need to tell the registration authority to use those DNS servers as the authority for addresses in your domain. The registration authority probably offers an online form you can fill out to identify your DNS servers.

### Creating DNS configuration files (*named.conf* and *var/named*)

In configuring a DNS server, you're actually creating definitions that apply to a particular *zone* in the public DNS tree, as well as several local zones that apply to your computer and local network. To create a useful DNS server for your example small-office environment, you have the following zones:

*   **Public DNS server zone** — The DNS server is authoritative for the domain that you're serving. This zone serves the names and IP addresses for your public servers. In the example *named.conf* file shown in the next section, you need to replace the name *yourdomain.com* with the domain that you're creating. These records become accessible to everyone on the Internet.
*   **Private DNS server zone** — So that each computer on the private network doesn't need to know the IP addresses for other computers on your private network, a zone is added in the example *named.conf* file to let the DNS server resolve these addresses. The names and IP addresses (which are private) are available only to computers on your LAN.

Note that by creating different views of these zones, different information will be returned to queries, depending on where the queries come from. For example, when someone from the
