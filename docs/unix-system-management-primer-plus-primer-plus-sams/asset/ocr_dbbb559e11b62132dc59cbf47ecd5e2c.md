# Chapter 14 INTERNAL COMMUNICATION 41

+   * Tracing optimal routes through your networks
* Identifying single points of failure

The only network devices depicted on a logical diagram are the hosts and routing devices. Firewalls and load balancers are valid devices to map on a logical diagram because they perform routing functions. Switches, however, are rarely included on these, except to indicate that they reside on a particular network. When logical diagrams include switches, they do not show individual connections from each machine to the switch.

Figure 14.2 depicts the logical diagram of the same small network presented by the physical diagram in Figure 14.1. Note how the two diagrams of the same network can differ widely.

# FIGURE 14.2

A logical network diagram for the same small network shown in Figure 14.1.

![](bbox=[0.305, 0.295, 0.895, 0.485])

# Host Functionality

Servers today are so powerful and have so many resources available to them that it makes sense for some of them to be dedicated to more than just one task. Dedicating a dual 900MHz Sun Enterprise 280R as a mail server for 25 people, for example, isn't a very efficient use of resources. You might find underutilizing a server in your system, simply because the server was available at the time you set up the network. In time, you can choose to run a few more services on that machine that has extra resources available. A gradual increase in server workload is a common occurrence in many IT organizations. As you change server load, however, you must properly document what services you've added to each server. Otherwise, you can forget what service is running on each server—a sure cause of headaches during a crash or maintenance event that requires quickly determining which services are down.

Host functionality documentation, which many call a functionality matrix, documents the services running on each system on a network. Host functionality documentation also indicates systems use use services. No standard format dictates how this data should appear, but it should be easy to read, to search through, and (most importantly) kept up to date. You can put a matrix into a spreadsheet like the one shown in Figure 14.3. A quick glance at this document tells you what services are running on each machine, and what services would be affected if any machine were to fail.