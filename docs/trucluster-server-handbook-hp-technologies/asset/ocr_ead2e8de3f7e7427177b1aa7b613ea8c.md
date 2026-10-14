# 17.2.4 The Quorum Disk

The quorum disk can be thought of as a virtual cluster member in that it can add an additional vote to a cluster with an even number of members to increase the cluster's availability. In order for a disk to be used as a quorum disk, the following conditions must be met:

+   - The disk must be unused because the quorum disk is dedicated for use by the CNX.
+   - It is highly recommended that the disk be on a shared bus that is connected to all voting cluster members.
+   - There can be only one quorum disk in a cluster.

The quorum disk can be used to contribute one vote or zero votes to a cluster.

We will cover the quorum disk in greater detail in section 17.8.3.

# 17.2.5 The cnx Partition

The quorum disk contains a cnx partition, 1 MB (2048 sectors) in size, located on the "h" partition. In fact, this is the only partition that can be used on the entire disk! Due to the small amount of space that is used on the disk, we recommend using the smallest disk possible.

Every member's boot disk also has a cnx partition that is located on the "h" partition.

Although both types of disks contain cnx partitions, they use different portions of the partition (as we will learn in section 17.8.5.1).

The following series of Korn shell commands displays the cnx partition information from the disk label of our cluster's disks.

```
# for i in dsk2 dsk3 dsk4
> do
> echo ; echo "$(i)" "\n"
> disklabel -r $(i) | 
> awk '/label:/ { printf ("%s - %s",$2) } \
> /h:/ { printf ("partition: h, type: %s, size: %s sectors\n",$4,$2) }'
> done

[dsk2] clu_member1 - partition: h, type: cnx, size: 2048 sectors

[dsk3] clu_member2 - partition: h, type: cnx, size: 2048 sectors

[dsk4] Quorum - partition: h, type: cnx, size: 2048 sectors
```

In section 17.8.5 we will discuss how to manage the cnx partition.