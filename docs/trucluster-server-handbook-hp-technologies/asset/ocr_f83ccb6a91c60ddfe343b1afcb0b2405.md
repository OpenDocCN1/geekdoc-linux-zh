There is no reference page to support the sub-system attributes shown in the output below. We are presenting our best estimation of the meaning of the attributes. Before examining them, here are some additional terms and concepts.

The first member to initiate a "set" will be the "synchronizer" member (think of the director in the lock manager – it uses a similar strategy). Other references to the set are resolved by hashing the set name into a number, using the number as an offset into a directory weight table containing cluster system IDs (csids). The csid found at the calculated offset in the hash table will be the ID of the director to the synchronizer member for that set. Note that the director member may also be the synchronizer. The director member (found through the directory weight table) checks its "set" information to see if it knows which member is the "synchronizer" for the requested set. The "director" responds to the "initiator" and indicates who the "synchronizer" member is. Subsequent requests for that set are sent directly to the synchronizer. The idea is to distribute the KGS activities over the members of the cluster. If you have a member of the cluster with much more capacity than the others, you may improve its odds of being chosen as a "synchronizer" by increasing the kch_dirwt attribute below (maximum value is 4). Note that as of this writing, the kch_dirwt value is fixed at 1.

# CAUTION:

These attributes should not be altered unless directed to do so by HP engineering.

```
# sysconfig -q kch
kch:
kch_enabled = 1
kch_sets_allocated = 25
kch_mbrs_allocated = 25
kch_lstnrs_allocated = 0
kch_dirwt = 1
kch_set_tbl_hash_size = 8192
```

+   Service enabled (1=yes)
+   Existing set count
+   Members are active set participants
+   Listeners are nonvoting members of a set
+   Directory table weighting factor
+   Hash table size

```
# sysconfig -Q kch
kch:
kch_enabled - type=INT op=CQ min_val=0 max_val=1
kch_sets_allocated - type=UINT op=Q min_val=0 max_val=4294967295
kch_mbrs_allocated - type=UINT op=Q min_val=0 max_val=4294967295
kch_lstnrs_allocated - type=UINT op=Q min_val=0 max_val=4294967295
kch_dirwt - type=INT op=Q min_val=0 max_val=4
kch_set_tbl_hash_size - type=UINT op=CQ min_val=8192 max_val=32768
```