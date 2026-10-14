```
```text
$ showlocks -d dlm

dlm:
dlm_name             = Distributed Lock Manager - V2.0
dlm_lkbs_allocated    = 36
dlm_rems_allocated    = 36
dlm_tot_lkids         = 8191
dlm_lkids_inuse       = 36
dlm_deadlkqlen        = 0
dlm_timeout_len       = 0
```
```

Note that the following is a kdbx (8) command. It displays many of the Resource Block (RSB) resource names supporting the cluster components, as well as the one supporting our “gen” resource (array element 2605). This command takes a while to complete and this particular run was stopped before it finished. It would be interesting to run this command on both members in a two-member cluster to see if the per member lock databases are the same. Remember that this component is called the Distributed Lock Manager because portions of the in-memory lock database can be distributed across the members of the cluster. However, if the locking can be accomplished using one member only, then the other members need little or no knowledge of the locking activities.

But what happens if another cluster member asks for a lock that is currently in use on only one member of the cluster? How will the member that is new in the locking scenario become aware that the resource he wants to lock is already locked on another member? One solution would be to really distribute the lock database (in its entirety) in the memory of all cluster members. This solution wastes memory and causes traffic between members each time a lock is created, tested, deleted, or accessed in any way.

The actual solution distributes a lock mastering table, which will be exactly the same on each cluster member. When access to a lock is requested, the resource name (representing the lock) is passed through a hashing algorithm that ultimately generates an offset into the lock mastering table (called the lock directory vector table). The appropriate entry in the table will identify the cluster member who is the director for the lock traffic involving this particular resource. All requests for new locks for a particular resource are funneled to the same director cluster member, who will be responsible for directing the lock traffic to the cluster member who is mastering the lock structures for this resource (see Figure 18-3 & Figure 18-4). Note that once a requesting member is told where

![](bbox=[0.274, 0.684, 0.734, 0.895])