# 178 Part II ♦ Running the Show

After you have TCP/IP (the primary set of protocols used the Internet) configured to connect to your ISP, requests for data can pass in either direction between your computers and the Internet unless you use a firewall to restrict traffic. So the same connection you use for Internet can be used to offer services to the Internet, with a few caveats:

+   * Permanent IP address — Each time you reboot your computer, your ISP's DHCP server dynamically assigns your DSL/cable modem's IP address. For that reason, your IP address could change at each reboot. If you want your servers to be reachable on a permanent basis, you usually need at least one permanent IP address at which you ask your ISP for a permanent IP, and it might cost you extra money to have.

A service Dynamic DNS can be used in place of paying for a permanent IP address. With Dynamic DNS, you hire a service to constantly check whether your IP address has changed and assign your DNS host name to the new address if it does. You can search the Web for "Dynamic DNS" to find companies that offer that service.

+   * Acceptable policy — Check that you are allowed to have incoming connections. Some ISPs, especially for inexpensive, home-use broadband service, will block incoming connections to Web servers or mail servers.

+   * DNS host name — Although typing an IP address into a browser box works fine, most people prefer to use names (such as `www.trouble.com`) to reach a server. That requires you to purchase a DNS domain name and have an entry set in a DNS server to resolve the name to the IP of your server.

There is nothing magical about setting up an Internet server, given the few issues just mentioning, that a public server can be like opening the doors of your house so that strangers can wander in. You want policies in place to restrict where strangers can go and what they can do.

For home or small-office locations that have a single Internet connection (represented by one IP address), servers can be more exposed to the Internet than desktop systems by keeping them in one area that's referred to as the DMZ (demilitarized). In this configuration (illustrated in Figure 5-4), servers are directly behind the outside firewall. Desktop systems (that aren't accessible by people from the Internet) are behind a second, more restrictive firewall.

Whether you use Linux or dedicated firewall devices to provide service, the outside firewall allows requests for Web services (port 80), FTP services (ports 20 and 21), simple mail transfer protocol (port 25), and possibly other services. The internal firewall blocks any requests for services from the outside and allows only Internet communications that were initiated from computers behind the inside firewall.

![](bbox=[0.115, 0.345, 0.163, 0.385])