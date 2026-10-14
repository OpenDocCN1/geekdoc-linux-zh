Make sure you listen carefully to what your user is telling you. While you may be the expert, the user knows what they need.

# KNOWING YOUR INFRASTRUCTURE

While infrastructure in many cases refers to the network, for our purposes, infrastructure refers to the support systems you have in place to make your day-to-day operations run smoothly. Infrastructure can include:

+   - Mail servers.
+   - NIS, DNS, and LDAP servers.
+   - File and print servers.
+   - Network infrastructure, including routers, switches, and bridges.

By understanding how your infrastructure is designed, you can architect your systems correctly from the start. Be aware of how many DNS, NIS+, and LDAP servers you have on each network segment. Use redundant services where possible. Be aware that multi-user systems require more resources than a stand-alone workstation, and may require you to install additional servers. If installing more servers is not an option, attempt to balance the load through proactive means instead of waiting for problems. DNS and NIS+ problems can be some of the hardest to debug, so kill the bugs early for best results. Configuring systems to use redundant services will be discussed in Chapter 6, "Name Resolution and Registration."

Understand how user groups work and what servers they use. Try to group or cluster users' filesystems with the workstations and servers they use most. Employ switches where users require high bandwidth. Don't be afraid to move servers around when you can take advantage of new network equipment. Faster routers and switches lose their purpose if they are underutilized

Be sure a user doesn't order the wrong network card if you don't support a particular speed or medium. Ordering the wrong network card can delay installation for days, and cost you big dollars if you cannot return the incorrect card. Be sure to order the right cables, too!

# PLANNING SUMMARY

As has been discussed, the first step in creating a successful system is asking the right questions. Use the information in Table 2.1 to help plan the installation of all new systems. By addressing these questions early in the