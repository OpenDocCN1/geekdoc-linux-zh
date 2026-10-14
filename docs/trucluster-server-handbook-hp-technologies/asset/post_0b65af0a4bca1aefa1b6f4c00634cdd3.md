
be more accurate when delivered from one NTP server as compared with another. The most accurate time is delivered from a "stratum 1" server that has an accurate time derived from some highly reliable source (see www.ntp.org for a list of public servers). If a member serves out time that was acquired from a stratum 1 server, the time value served out by that member is treated as if it came from a stratum 2 server and so forth. If an NTP client receives time from several NTP servers, it simply selects the time from the lowest stratum rated server.

According to the Tru64 UNIX Cluster Installation manual, NTP is automatically configured on the first member of your cluster when you issue the clu_create(8) command. However, as of V5.1A, the clu_create script simply checks to see if you have NTP configured, and if not, it errors out. Therefore, we recommend installing NTP prior to installing the first cluster member. If you will be using one or more external time sources, it is imperative to install NTP as described above because when/if the software catches up with the documentation, the clu_create and clu_add_member commands will set up the members as NTP peers of each other.

Additional cluster members have NTP automatically configured as they are added to the cluster. All members in the cluster are configured as NTP peers. This allows all cluster members to provide their version of time to other cluster members. This mechanism usually provides synchronization within ten thousandths of a second. Note that two members that are out of time sync will gradually (as opposed to instantaneously) be brought back in sync. This avoids the potential for software repercussions if time changes too drastically and too quickly.

To avoid the blind leading the blind, we would recommend configuring NTP on your initial system such that it is synched to an accurate external source; although for starters, you may want to have one member synch to 127.127.0.1 (the local reference clock – for more information see the ntp_manual_setup(7) and ntp.conf(4) reference pages).

## 20.7 Summary Chart

Table 20-1 yields handy information concerning network management tasks in a cluster.

### Network Services

| Service | Configuration | Cluster Aware | CAA | Notes |
| --- | --- | --- | --- | --- |
| DHCP client |  | x | x | Not Allowed. Static addresses only. |
| DHCP server | common | x | ✓ | Implemented as a single-instance, highly-available CAA application resource (dhcp). Clients should use the default cluster alias. |
| DNS/BIND client | common | x | x | /etc/resolv.conf is a cluster-common file. |
| DNS/BIND server | common | x | ✓ | Implemented as a single-instance, highly-available CAA application resource (named). |
| NFS client | common | x | x | By default, the NFS is configured and enabled on all members. |
| NFS server | common | ✓ | x | The NFS server implementation is cluster-aware. By default, the NFS is configured and enabled on all members. Clients must use the default cluster alias prior to V5.1A. As of V5.1A, alternate aliases can be defined in /etc/exports.aliases. |
| NFS server | common | x | ✓ | Server versions of rpc.statd & rpc.lockd are implemented as a single-instance, highly-available CAA application resource (cluster_lockd). |
| NFS autofs | common | x | ✓ | Implemented as a single-instance, highly-available CAA application resource (autofs). |
| NIS client | common | x | x | By default, the NFS is configured and enabled on all members. |
| NIS master server | common | ✓ | x | If configured on one member, it is configured the same on all members. ypserv is multi-instance, and is active on all the members. Although rpc.yppasswd runs on every node, it is single-instance; only one daemon is actually active at a time. Clients should use the default cluster alias. |
| NIS slave server | common | x | x | By default, the NFS is configured and enabled on all members. |
| NTP | member-specific | x | x | Time must be synchronized. Members are configured as peers. |
| Routing | member-specific | x | x | Must be enabled prior to V5.1A PK1. |
| Routing gated | common | x | x | Member-specific routing information added and maintained by CLUA (aliasd). |
