# Network Administration Tasks

Network administration can be even more of a black art than traditional system administration. Most people tend to lump the two functions under one common heading, "system administration." For our purposes, we will consider them separately. This chapter addresses network administration issues as they pertain to the world of clusters.

Last time we checked, the network administration team just stampeded down the hall to track down a routing/NFS/NIS/hardware/BIND/some_other_arcane_network problem. Imagine the team's reaction when we introduce clustered machines into their already bubbling over cauldron of responsibilities! In the previous chapter on System Administration Tasks, we saw that some commands worked unchanged in a cluster and were common to all members, some worked with slight changes, and others were specific to cluster members. Here too some of the network-oriented services will be common, others will be member-specific, and a few will not be recommended.

# 20.1 Routing

An article appeared in SysAdmin magazine a few years ago in which the author was discussing routing and subnet masks. Just a few columns were enough to convince us that several misconceptions were being presented. Considering that the article was written by someone who thought he understood the concept of routing well enough to be published in a magazine, it's fair to say that routing is one of the least understood and most error prone aspects of network administration. The TruCluster Server Cluster Administration Guide suggests that the cluster not be configured as a router. This doesn't mean that it can't function as a router; they just don't recommend it. In a way, this is good news for you.

Go out and buy a piece of hardware/software to deal with routing. Why waste the beauty of the cluster on the narrowly focused job of forwarding IP packets from one network to another? Your cluster has much more important processing to do.