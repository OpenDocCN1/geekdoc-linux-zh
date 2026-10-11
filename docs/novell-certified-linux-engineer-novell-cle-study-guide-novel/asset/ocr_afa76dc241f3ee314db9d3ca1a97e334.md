configured DA. The DA will process the query and respond with the
requested information—again using unicast transmissions.

This configuration is shown in Figure 5.6.

# FIGURE 5.6
Requesting serv-
ices from a
Directory Agent.

![](bbox=[0.33, 0.18, 0.85, 0.46])

When a service is shut down, the local SA deregisters the service with the DA.

As you can see from Figure 5.6, using a DA requires more work on the part
of the network administrator to configure. The bandwidth savings in larger
organizations, however, is usually worth the effort.

DA mode also prevents other problems. Recall that SA-Only mode is heavily
dependent on multicast transmissions. Most hardware and software routers,
however, are configured by default to not allow multicast traffic to cross
between network segments. If the servers in your organization lie on differ-
ent network segments separated by routers, you must enable multicast rout-
ing to use SLP in SA-Only mode.

As a better alternative, Novell recommends that you implement DAs on each
side of the router. I mentioned earlier that SAs still rely on multicast trans-
missions to discover DAs by default. You can, however, manually configure
each SA with the IP address of the DAs you want them to register their serv-
ices with. By doing this, multicast traffic is all but eliminated. We'll discuss
how to do this a little later in this chapter when we explore the SLP
daemon-configuration files.

Now that you understand the conceptual architecture of SLP, you need to
learn how to implement and configure SLP daemons.