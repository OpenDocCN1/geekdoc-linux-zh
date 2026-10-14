![](bbox=[0.07, 0.12, 0.95, 0.52])

# Figure 15-8: Load Balancing Multiple Devices on a Semi-Shared Bus

Notice that the configuration theoretically more balanced, but depending on the workload of member2 and member3, this may not necessarily have been the best move.

Another solution might be to balance the load of several disks on the semi-shared bus between the two members as illustrated in Figure 15-8.

In this figure, member2 serves odd numbered disks to member1 and member4, while member3 serves the even numbered disks to member1 and member4. Notice that member2 and member3 will directly access all of the disks since they have direct access.

# NOTE:

Even though we have illustrated a cluster that contains a semi-shared bus configuration, we still recommend having all buses shared by all members, if possible, as it is the highest availability solution and easiest to manage. The only situation where we are not opposed to a private bus solution is for swap, /tmp, and/or non-critical data where high-availability is not a priority.

# 15.2.2 Changing the Server

Changing the server for a device is something that you may want to do for a served device on a shared bus. If you’ll recall from section 15.1.2.2, a served device cannot have more than one active server at a time, so if you want a particular member to have direct access to a served device and it is being served by another member, you’ll need to change the server.