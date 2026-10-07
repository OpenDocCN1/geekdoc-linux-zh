# Chapter 18: Web Security Issues and Internet Firewalls

# Using Application-Level Firewalls

Application-level firewalls provide another method of protecting your systems. These firewalls are not part of the Linux kernel, but must be added separately. They may be considered applications themselves.

It could be said that application-level firewalls have more intelligence than protocol firewalls, which actually just have a narrower range of specialized capabilities. These firewalls are sometimes gateways or proxies.

An example of an application-level firewall is a proxy server. The proxy server receives a request for a service, either from an outside client or an internal client. The proxy then determines an action based on the firewall rules that you've set up for the proxy. For example, it might be set up that all internal people on Web browsers who request the CNN Sports page receive the monthly monthly newsletter instead. Or it might allow everyone to use the GET command, but not the POST command, so no one can submit forms from Web pages.

The type of firewall just described examines specifics about the application being used and can decide which features or actions are allowed or refused, either from an internal user or an external user.

Other examples might be firewalls that limit external users of databases to a specific set of commands or firewalls that discarded e-mail messages that totaled more than 2 megabytes.

# Using Firewalls

The best way to use firewalls depends on your individual circumstances, the two types mentioned—packets filtering and application processes—are usually best together. As you watch for security problems and refine your configurations, or even add other firewall tools as needed, your understanding of the types of firewalls and security your system needs will increase.

Using both packet-based and application-based firewalls gives you the fine-grained control of packets and protocols for overall system protection, plus the fine-grained control of applications that might be better at controlling the use of Internet resources within your own organization.

As mentioned earlier, many "black box" firewall products are available that can provide protection for your network. Most of these operate only on the packet and protocol levels, leaving the application-level firewall to a special application running on your system. Many of these black-boxes are actually running Linux, though they don't say so. With adequate configuration, your Linux system (or a separate computer Linux if you have a busy network) can provide all the firewall protection you should ever need.

# Learning More About Firewalls

There are many resources on the Web about firewalls, both for technical details on setting them up and maintaining them, and for theory and advice on using them to protect your networks.