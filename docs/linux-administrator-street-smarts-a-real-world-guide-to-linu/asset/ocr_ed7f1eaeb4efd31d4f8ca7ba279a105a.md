# Scope of Task

This task requires using the `route` command in more advanced ways than have been described previously. You must also use a few other commands to enable routing between the networks.

# Duration

This task should take about half an hour to complete. The individual actions, of course, take less time than this, and once you’re familiar with routing configuration, you should be able to do the job in just a few minutes.

# Setup

You must have `root` access to the computer in order to configure routing. Configuring a computer as a router also requires that it have two network interfaces. If you don’t have access to such a computer, you should read this task but not attempt to implement its actions.

> It’s possible to configure routing on certain types of virtual networks. For example, you can use a network of emulated computers running in virtual environments such as those provided by VMware (http://www.vmware.com). Configuring such software to bring it to the point where you could route traffic for it is a topic that’s beyond the scope of this task, though.

# Caveats

The usual caveats concerning `root` access apply to this task. In addition, router configuration poses certain risks and opportunities, most of which are security related. At its simplest, a router provides no security protection for any of the networks it links. More complex routers can block certain types of traffic, protecting one or both networks from certain types of network attacks. Such routers are referred to as `firewalls`. Although firewalls are very useful, firewall configuration is beyond the scope of this task. (Consult Phase 7 for information on basic Linux firewall features.) You should be concerned with your router’s security, particularly if you configure it as a firewall; a breach of a router, or especially a firewall, can put the network it protects at risk.

# Procedure

Basic router configuration involves two specific tasks. First, you must use the `route` command to ensure that network routes exist for both the networks to which the computer is connected. Second, you must configure the computer to forward packets between the two networks. An ancillary task, which might not involve Linux at all, is to configure computers on both of the linked networks to recognize the Linux system as a router.