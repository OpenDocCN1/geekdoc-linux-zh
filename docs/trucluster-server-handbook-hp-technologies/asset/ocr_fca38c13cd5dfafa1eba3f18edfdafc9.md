```
The next available member ID for a cluster member is '2'.
To use this default value, press Return at the prompt.

A member ID is used to identify each member in a cluster.
Each member must have a unique member ID, which is an integer in the range 1-63, inclusive.

Enter a cluster member ID [2]: 2
Checking cluster member ID: 2

You entered '2' as the member ID.
Is this correct? [yes]: yes
```

By default, this new cluster member is given 1 vote. In this case, it makes perfect sense to accept this default value. For more detailed information on quorum and the Connection Manager, please review Chapter 17.

```
By default, when the current cluster's expected votes are greater then 1,
each added member is assigned 1 vote(s). Otherwise, each added member is assigned 0 (zero) votes.
To use this default value, press Return at the prompt.

The number of votes for a member is an integer usually 0 or 1
Enter the number of votes for this member [1]: 1
Checking number of votes for this member: 1

You entered '1' as the number votes for this member.
Is this correct? [yes]: yes
```

# 11.2.3 Enter the Member Boot Disk

As each individual cluster member must have its own boot device or boot_partition, we are prompted to enter the name of the disk that will be used for this new cluster member. Given that we had planned for this, we refer to our completed Cluster Preparation Checklist and Worksheet for the information on the disk that has been reserved and already properly partitioned for the boot_partition of this new cluster member.

```
Each member has its own boot disk, which has an associated device name; for example, 'dsk5'.

Enter the device name of the member boot disk []: dsk2
Checking the member boot disk: dsk2
```

1 Please refer to section 11.1.2.2 on The New Member Boot Disk and section 10.1.2 on Disks for the Cluster.