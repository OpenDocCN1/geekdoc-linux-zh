# WARNING:

If the UFS file system is not mounted, the clu_quorum command will add the disk as the quorum disk. It will replace the existing disk label with a new one, and no error will be given.

# 17.8.3.2 How to Remove the Quorum Disk

If you have a quorum disk but wish to remove it, the clu_quorum command with the "-d remove" option should do the trick.

```
# clu_quorum -d remove
Collecting quorum data for Member(s): 1 2

Quorum disk successfully removed.
```

What reason could you have for removing the quorum disk? If you add or remove a member from the cluster resulting in an odd number of members, you should remove the quorum disk or at least adjust its votes to a value of zero.

Once the quorum disk is removed from the cluster, the CNX quorum disk thread is stopped. We can verify this by running the cnxthreads program we wrote and grep for "qdisk". No output should be displayed.

```
# cnxthreads | grep qdisk
```

# 17.8.3.3 How to Adjust the Quorum Disk Votes

If you have a quorum disk and need to shutdown a member of the cluster for an extended period of time but do not want to remove the quorum disk, you can use the clu_quorum command with the "-d adjust" option.

```
clu_quorum -d adjust #votes
```

Set the #votes value to zero.

```
# clu_quorum -d adjust 0
Collecting quorum data for Member(s): 1 2

Quorum disk votes successfully adjusted.
```