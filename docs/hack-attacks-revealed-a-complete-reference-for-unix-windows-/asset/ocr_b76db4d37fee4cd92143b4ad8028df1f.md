does not rely on predefined application information. Stateful inspection also takes less processing power than application level analysis. On the downside, stateful inspection firewalls do not recognize specific applications, hence are unable to apply dissimilar rules to different applications.

# ### Proxy Firewall

A *proxy firewall* host is simply a server with dual network interface cards (NICs) that has routing or packet forwarding deactivated, utilizing a proxy server daemon instead. For every application that requires passage through this gateway, software must be installed and running to proxy it through. A proxy server acts on behalf of one or more other servers; usually for screening, firewalling, caching, or a combination of these purposes.

The term *gateway* is often used as a synonym for proxy server. Typically, a proxy server is used within a company or enterprise to gather all Internet requests, forward them to Internet servers, receive the responses, and in turn, forward them to data to the original requestor within the company (using a *proxy agent*, which acts on behalf of a user, typically accepting a connection from a user and completing a connection with a remote host or service).

# ### Application Proxy Gateway

An *application proxy gateway* is the enhanced version of a proxy firewall, and like the proxy firewall, for every application that should pass through the firewall, software must be installed and running to proxy it. The difference is that the application gateway contains integrated modules that check every request and response. For example, an outgoing file transfer protocol (FTP) stream may only download data. Application gateways look at data at the application layer of the protocol stack and serve as proxies for outside users, intercepting packets and forwarding them to the application. Thus, outside users never have a direct connection to anything beyond the firewall. The fact that the firewall looks at this application information means that it can distinguish among such things as FTP and SMTP. For that reason, the application gateway provides security for each application it supports.

![](bbox=[0.12, 0.68, 0.2, 0.74])

> Most vendor security architectures contain their own **unique security breaches** (see Chapter 9 for more information).

# ### Implementing a Backdoor Kit

Exploiting security breaches with backdoors, through firewall architectures, is not a simple task. Rather, it must be carefully planned to reach a successful completion. When implementing a backdoor kit, frequently, four actions take place:

+   - *Seizing a virtual connection*. This involves hijacking a remote telnet session, a VPN tunnel, or a secure-ID session.

+   - *Planting an insider*. This is a user, technician, or socially engineered (swindled) individual who installs the kit from the internal network. A much simpler and common version of this action involves spoofing email to an internal user with a remote-access Trojan attached.

+   - *Manipulating an internal vulnerability*. Most networks offer some suite of services, whether it be email, domain name resolution, or Web server access in a demilitarized zone (DMZ; the zone in front of the firewall, often not completely protected by a firewall). An attack can be made on any one of those services with a good chance of gaining access. Consider the fact that many firewalls run daemons for mail relay.

+   - *Manipulating an external vulnerability*. This involves penetrating through an external mail server, HTTP server daemon, and/or telnet service on an external boundary gateway. Most