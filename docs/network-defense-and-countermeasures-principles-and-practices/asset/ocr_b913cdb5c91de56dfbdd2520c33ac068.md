Perhaps the best advantage to router-based firewalls is the ease of setup. In many cases the vendor will even configure the firewall for you, and you simply plug it in. Most home-based routers today, such as those from Linksys, Belkin, or Netgear, have built a built-in firewall. And in fact virtually all higher-end routers include firewall capability.

# Screened Hosts

A screened host is a real combination of firewalls. In this configuration, a combination of a bastion host and a screening router is used. The combination creates a dual firewall that is effective at filtering traffic. The two firewalls can be different types. The bastion host (see the following FYI) might be an application gateway and the router packet screener (or vice versa). This approach (shown in Figure 3-5) gives the advantages of both types of firewalls and is similar in concept to the dual-homed host.

![](bbox=[0.07, 0.395, 0.56, 0.565])

FIGURE 3-5: Screened host

The screened host has some distinct advantages over the dual-homed firewall. Unlike the dual-homed firewall, the screened host needs only one network interface and does not require a separate subnet between the application gateway and the router. This makes the firewall more flexible but perhaps less secure because its reliance on only one network interface card means that it might be configured to pass certain trusted services to the application gateway portion of the firewall and directly to servers within the network.

The most significant concern when using the screened host is that it essentially combines two firewalls into one. Therefore any security flaw or misconfiguration affects both firewalls. When you use a DMZ there are physically two separate firewalls, and the likelihood of any security flaw being propagated to both is low.