Note that each system contains its own list of cluster members (or potential members) that is used to determine what systems it can communicate with and to calculate the expected vote value and ultimately the quorum vote value.

Since we have been asked many times, "What are all those ICS Server threads use for?," we chose to include Figure 17-5 to illustrate the interaction between the various CNX threads and the ICS threads. As you can see, this remote procedure call (RPC) communication between members in a cluster is done using the ICS. The ICS Server threads are kernel threads that are used to send and receive communication to and from many of the cluster subsystems.

For more information on the ICS, see Chapter 18.

# 17.6.2 Cluster Formation

After ten seconds, if the node has not heard from a cluster, it will attempt to form a cluster.

```
CNX MGR: insufficient votes to form cluster: have 1 need 2
```

As you can see by the console output, the node initially counts its own vote toward forming the cluster. The system will effectively loop here until enough votes are attained to reach quorum.

If there is a quorum disk configured, then you will see a message similar to the following:

```
CNX QDISK: Adding 1 quorum disk vote toward formation.
```

In the last two lines of output, you can see that enough votes have been added to attain quorum because the first message stated, "have 1 need 2". In other words, the CNX has determined that it needs 2 votes to reach quorum. When the quorum disk's vote is added, the CNX will have the necessary second vote.

Once enough votes have been added to reach quorum, the cluster will form as shown in the output below.

```
CNX MGR: Cluster babylon5 incarnation 0x94a1e has been formed
CNX MGR: Founding node id is 1 csid is 0x10001
CNX MGR: membership configuration index: 1 (1 additions, 0 removals)
CNX MGR: quorum (re)gained, (re)starting cluster operations.
CNX MGR: Node molari 1 incarn 0x94a1e csid 0x10001 has been added to the cluster
```

# 17.6.2.1 Cluster Formation – The Details

You want additional details? Hold on tight.

When a system decides to form a cluster, it does the following: