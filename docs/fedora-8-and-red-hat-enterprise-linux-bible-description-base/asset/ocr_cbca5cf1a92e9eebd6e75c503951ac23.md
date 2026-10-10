+   * **DNS lookup tools** — You can use several tools to check that your DNS server is resolving hostnames properly. These include commands such as *host*, *dig*, and *nslookup* (which are part of the *bind-utils* software package).

To maintain your DNS server correctly, you can also perform the following configuration tasks with your DNS server:

+   * **Logging** — You can indicate what you want to log and where log files reside.
+   * **Remote server options** — You can set options for specific DNS servers to perform such tasks as blocking information from a bad server, setting encryption keys to use with a server, or defining transfer methods.

You don't need to give out DNS information to everyone who requests it. You can restrict access to those who request it based on the following:

+   * **Access control list (acl)** — This list can contain those hosts, domains, or IP addresses that you want to group together and apply the same level of access to your DNS server. You create acl records to group those addresses, and then indicate what domain information the locations in that acl can or can't access.
+   * **Listen-on ports** — By default, your name server accepts only name server requests that come to port 53 on your name server. You can add more port numbers if you want your name server to accept name service queries on different ports.
+   * **Authentication** — To verify the identities of hosts that are requesting services from your DNS server, you can use keys for authentication and authorization. (The *key* and *trusted-keys* statements are used for authentication.)

> **CROSS-REFERENCE**: You should already know what domain names and IP addresses are. Refer to Chapter 15 for IP addresses and Chapter 16 for DNS information, if you need to refresh your memory.

# ## DNS name server example

To get an idea of what you need to set up your DNS server, the following sections step you through an example of a DNS server for a domain called *yourdomain.com*. In the example, you're creating a DNS server for a small office network that includes the following:

+   * A private, local network that resides behind a firewall
+   * A server providing DNS service

In this office, other computers on the LAN are using the same Internet connection for outgoing communications, so the firewall on the server does network address translation (NAT) to enable the client computers to use the firewall as a router to the Internet. Figure 25-1 shows the configuration of the example *yourdomain.com* domain.

Figure 25-1 illustrates a small office network that's sharing a single Internet connection. The DNS, Web, mail, and FTP servers all have public IP addresses. (These addresses are fictitious,