In this situation, the tree root partition is said to be a "parent" of the CLE partition because it resides higher in the tree hierarchy. The CLE partition is said to be a "child partition" of the root partition. Likewise, the CLE partition is the parent of the IF partition and the IF partition is a child of the CLE partition.

In eDirectory, parent/child relationships only go up or down one level, so the IF partition is not a child, or grandchild, of the tree root partition.

The first time I learned about partitioning back in the early 1990s, it scared me to death. I had some experience with hardware crashes, and the thought of taking a database and dividing it up among several servers made me cringe. What if one of the servers went down? The whole database could end up getting corrupted because a chunk of it would disappear.

Novell wisely accommodates for this reality. In addition to dividing up the eDirectory database into partitions, you can also place multiple copies of each partition on different servers. Each copy is called a *replica*.

eDirectory is designed such that changes made by an administrator (changing a password, for example) to one replica are quickly replicated to all the other replicas of that partition. All the servers that host a replica of a given partition are said to be members of the *replica ring*. Each replica has an attribute called **Replica**. This attribute contains a list of all the other servers in the replica ring for the given partition.

eDirectory uses this to make sure the data in all replicas of a given partition is always synchronized so that no matter what replica is used for a given network action, the data is always up to date.

For any given partition, four different types of replicas can be placed on servers in the tree:

+   - **Master replica**—The Master replica is created when a partition is defined. There can be only one Master replica per partition. As you can see in Figure 5.33, one partition was automatically created when you installed eDirectory that encompasses the whole tree. By default, your CLE1 server had a Master replica of the partition placed on it.
+   
+   Because CLE1 is the only server in the tree, there is only one replica of the partition. All major partition operations, such as moves, merges, and creates, must be initiated from the Master replica.