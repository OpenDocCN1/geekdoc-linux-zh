+   7. Modify the clubase kernel subsystem on each member, changing the cluster_interconnect attribute to "mct", and remove the ics_ll_tcp subsystem from sysconfigtab.

+   8. Shut down all members.

+   9. Boot each member.

# 22.8 Name and Address Changes

After building your cluster, you may want or need to change its identity. For example, you may need to change the IP address or the name of the cluster or cluster members. These changes are discussed in Best Practices documents and the TruCluster Server Cluster Administration Guide, Chapter 5, so we won’t go into great detail here other than to briefly outline the steps required to make these changes.

# 22.8.1 Changing the Cluster Name

For the cluster name change to take effect, the entire cluster must be shut down and restarted after the changes are complete.

+   1. Create a stanza file that contains the name change attributes: clubase:cluster_name.

```
# cat > clubase-cluster_name.stanza
clubase:
    cluster_name=jetsons
^D
```

+   2. Merge the stanza file into the sysconfigtab file on each member.

```
# sysconfigdb -t /etc/sysconfigtab.cluster -m -f \
clubase-cluster_name.stanza clubase
```

```
# /usr/sbin/clu_update_sysconfig /etc/sysconfigtab.cluster
```

+   3. Change the cluster name in both /etc/hosts and /etc/hosts.equiv.

In /etc/hosts

```
192.168.0.159    minnow.dec.com  minnow   # Global cluster alias
```

becomes

```
192.168.0.159    jetsons.dec.com jetsons  # Global cluster alias
```