
## 18.6 Token Subsystem

Now that we have the file system mounted up, our users can start doing I/Os to it. But how do we coordinate the software running on various cluster members as they access the file? File locking is completely supported in a cluster, so any application level locking will work just fine. Think a little lower in the food chain (closer to the belly of the beast – the kernel). The following output shows the only system attribute that supports the token subsystem.

```shell
# sysconfig -q token
token:
svrtok_hash_size = 3183
```

```text
# man sys_attrs_token
(...)

svrtok_hash_size
    Determines the size of the svrcfstok hash table.

    On a CFS server, the svrcfstok hash table manages data structures that
    represent each active file in the cluster.

    For better hashing performance, the value you assign should be an odd
    number. Because of this, if you set svrtok_hash_size to an even value,
    the software automatically adds a 1 to it.

    On a system that is strictly a CFS client, you can set svrtok_hash_size to its
    minimum value, 64.

    Supported operations: Query; Configure at boot time

    Default value: 797

    Minimum value: 64

    Maximum value: 16384
```

Apparently, these tokens are important enough to merit a hash table so the system can quickly locate token information. Note that the CFS server will have a much larger hash table to promote quicker access to the token data. There are usually fewer tokens needed on a CFS client.

Doesn’t the kernel cache file system data in the Unified Buffer Cache (UBC)? And doesn’t each member have a UBC? The answer to both questions is yes, and therein lies some of the complexity. How does the system know that file system data that is currently cached in the local memory (UBC) is still synchronized with data from the disk (or in other members’ caches)? Note that cache coherency is discussed in Chapter 13 on CFS.

This issue is dealt with through the token subsystem. Bottom line: if the token representing file system data is held by the CFS client, then the cached data is OK. If the token is not held by the client, the client will request the token from the CFS server, and the data will be acquired from the CFS server's cache (if possible) or from the CFS server's disk.

You're thinking, "What if another CFS client currently holds the token?" In that case, the CFS server notifies all clients that the tokens have been "revoked," so if any client requests the data again, they know that they have to check in with the CFS server. The sequence of events is covered in Chapter 13.

The following output provides some statistics on the use of tokens in a cluster (more examples are found in Chapter 13).

```shell
# cfstat -S tokstat | more

Total CFS messages processed: 1736541
    token messages: 97978 ( 5%)
tok_rets      tok_grants    tok_reqs      tok_revs
87777 89%     3672 3%       3672 3%        2857 2%
```

```shell
# cfstat -S tokens | more

Client token stats:
Request stats:
    0               total number of otw requests (requests_sent)
Request hold failures:
    3647            ( 0%) holds causing otw requests (tok_hold_reqent)
Release stats:
    14              release with revokes waiting (tok_release_revoke)
    14              delayed releases (tok_release_delayed)
Grant stats:
    3647            total number of grants received (grants_received)
    3647            (100%) total number of grants processed (tok_grants)
Installs stats:
    179931          total number of installs received (tok_installs)
Revoke stats:
    2605            total revokes received (revokes_received)
    739             (28%) total revokes processed (tok_revokes)
    173901          total returns sent (returns_sent)
    206             ( 7%) revoke failure due to no cnode. (fhtovp_nocp)
    13              ( 0%) revoke failure due to hold count (tok_revokes_hcnt)

Server token stats:
Return stats:
426758          total number of returns received (returns_received)
Requests stats:
5720            total number of requests received (reqs_recvd)
297960          (520%) total number of requests processed (tok_reqs)
5720            (100%) total number of grants sent (grants_sent)
889             (15%) requests granted w/out revoking (tok_req_grants)
4831             (84%) requests causing revokes (tok_req_revoke)
Installs stats:
636490          total number of installs tried (tok_insts)
259014          (40%) number of successful installs (tok_insts_grants)
revoke stats:
4831            total number of revokes sent (revokes_sent)
Miscellaneous Stats

Server token processing stats:
10551           messages queued to client
  5720           (54%) grants (msg_queued[1][0])
  4831           (45%) revokes (msg_queued[1][1])
10551           messages sent to client
  5720           (54%) grants (msg_processed[1][0])
  4831           (45%) revokes (msg_processed[1][1])
Client token processing stats:
6253            messages queued to server
  3647           (58%) requests (msg_queued[0][0])
  2606           (41%) returns (msg_queued[0][1])
6253            messages sent to server
  3647           (58%) requests
  2606           (41%) returns
2606            total returns processed
```

## 18.7 References

- TruCluster Server Cluster Administration Guide.
- TruCluster Server Technical Overview.
- HP TruCluster Server Internals Course Materials.
- Tru64 UNIX Reference Pages (noted within the text).
