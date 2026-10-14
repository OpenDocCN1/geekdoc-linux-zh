# 17.10.1 Forming a Cluster without Enough Votes and/or a Failed Quorum Disk

If we modify our previous scenario to include a quorum disk that failed, can we boot interactively by simply using the cluster_expected_votes value alone? Yes and no. While you can boot a cluster with a failed quorum disk, the quorum disk thread will attempt to retry the disk for some time before finally giving up. Prior to V5.1A, this would delay the boot process. As an alternative, at the interactive boot prompt, add a second attribute, cluster_qdisk_votes.

```
# vmunix clubase:cluster_expected_votes=3 clubase:cluster_qdisk_votes=0
```

Another option would be to add the cluster_qdisk_major and cluster_qdisk_minor attributes to the interactive boot prompt so that the cnx will not load the qdisk attributes at all.

```
# vmunix clubase:cluster_expected_votes=2 clubase:cluster_qdisk_votes=0 clubase:cluster_qdisk_major=0 clubase:cluster_qdisk_minor=0
```

# CAUTION:

The interactive boot prompt line must be one continuous line. Do not put in a "\" to continue onto the next line; it will not work. Also, be extremely careful to type everything correctly. Typos are generally ignored by the subsystem. This, unfortunately, will not give you the desired effect since you will not have successfully overridden the attribute value(s).

# 17.11 References

+   - The TruCluster Server Technical Overview Guide.
+   - The TruCluster Server Cluster Administration Guide.
+   - The TruCluster Server Internals Course Material.
+   - Reference pages (noted within the text).