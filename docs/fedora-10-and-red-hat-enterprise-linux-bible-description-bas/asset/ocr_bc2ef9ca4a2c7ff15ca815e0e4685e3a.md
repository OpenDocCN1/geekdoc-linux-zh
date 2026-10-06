# Part IV: Fedora RHEL Network and Server Setup

zone information. The location of the chrooted DNS configuration files in Fedora and RHEL (/var/named/chroot) is set in the /etc/sysconfig/named file.

NOTE: If you run BIND in a non-chrooted environment, configuration files are located in /etc/named.conf file and the /var/named directory. You must uninstall the bind-ch package to do this.

+   - DNS lookup — You can use several tools to check that your DNS server is resolving hosts properly. These include commands such as host, dig, and nslookup (which are part of the bind-utils software package).

To maintain your DNS server correctly, you can also perform the following configuration tasks with your DNS server:

+   - Logging — You can indicate where to log and where files reside.
- Remote server options — You can set options for specific DNS servers to perform tasks as blocking information from a bad server, setting encryption keys to use with a server, or defining transfer methods.

You don't need to give DNS information to everyone who requests it. You can restrict access to those you want based on the following:

+   - Access control list (acl) — This list can contain hosts, domains, or IP addresses that you want to group together and apply the same level of access to your DNS server. You create acl records to group these addresses, and then indicate domain information the locations that acl can or can't access.
- Listen-on ports — By default, your name server accepts only name server requests that come to port 53 on your name server. You can add more port if you want your name server to accept name service queries on different ports.
- Authentication — To verify the identities of hosts that are requesting services from your DNS server, you can use keys for authentication and authorization. (The key and trusted-keys statements are used for authentication.)

> CROSS-REFERENCE: You should already know what domain names and IP addresses are. Refer to Chapter 15 for IP addresses and Chapter 16 for DNS information, if you need to refresh your memory.

# DNS name server example

To get an idea of how to set up your DNS server, the following sections show you through an example of a DNS server for a domain yourdomain.com. In the example, you're creating a DNS server for a small office network that includes the following:

+   - A private, local network that resides behind a firewall
- A server providing DNS service