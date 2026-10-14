# The Connection Manager

> "We must all hang together, or assuredly we shall all hang separately."
> — Benjamin Franklin

In the previous sixteen chapters, we have discussed what a cluster is; why you would want to have a cluster as your computing platform; how to plan, install, and configure a cluster; and some of the components that make a cluster work. What we haven’t touched on yet is how a cluster is formed and how individual systems become members.

A cluster is formed when there are a sufficient number of voting members to reach a quorum. Quorum is defined as a simple majority. A quorum must be present in order for a cluster to be formed. Similarly, a quorum must be present for an existing cluster to continue performing useful work, or when a member shuts down or leaves the cluster.

The first step in determining a quorum is calculating the cluster’s expected votes. The cluster’s expected votes value is the maximum number of votes that would be available if every voting member were up and the quorum disk¹, if configured with a vote, were available. In a cluster that consists of five members, the cluster’s expected votes value would be equal to five, assuming that each member has one vote. As of this writing, members can have one vote or zero votes.

Once a cluster’s expected votes value is determined, the number of votes required for quorum is calculated. If the cluster has enough votes to meet or exceed the quorum vote value, the cluster is formed.

The kernel subsystem responsible for determining whether or not a cluster has reached quorum is the Connection Manager (CNX).

In this chapter, we will cover the Connection Manager cluster component, voting and quorum strategies, and the quorum disk. Additionally, we will cover what occurs as a system boots, which subsystems are configured, the boot messages that you can expect to see, how a cluster is formed, and how a system becomes a member of an existing cluster.

¹ We will cover the quorum disk in more detail in sections 17.2.4 and 17.8.3.