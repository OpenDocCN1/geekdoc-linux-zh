The following output shows maximums and minimums pertaining to RDG.

```
# sysconfig -Q rdg
rdg:
version -      type=INT    op=Q    min_val=1      max_val=10000
ident -        type=STRING op=Q    min_len=1      max_len=256
max_objs -     type=INT    op=CQ   min_val=0      max_val=90000
msg_q_size -   type=INT    op=CQ   min_val=0      max_val=10000
msg_size -     type=INT    op=CQ   min_val=0      max_val=1048576
stats_collect - type=INT   op=CRQ  min_val=0      max_val=1
stats_zero -   type=INT    op=CRQ  min_val=0      max_val=1
assertions -   type=INT    op=CRQ  min_val=0      max_val=1
...
```

The following output would be of more use in a cluster running applications built using the RDG API (such as some database products).

```
# rdgstats
Cluster membership status of node molari-ics0 is MEMBER

RDG statistics - time duration: 0
RDG statistics:
molari-ics0:
  snd_msg_attempts = 0
  snd_buf_attempts = 0
  snd_blocks = 0
  snd_msg_successes = 0
  snd_buf_successes = 0
  snd_thread_wakeups = 0
  snd_kernel_queued_local = 0
  snd_kernel_queued_remote = 0
  rcv_msg_attempts = 0
  rcv_blocks = 0
  rcv_msg_successes = 0
  rcv_thread_wakeups = 0
  bytes_sent = 0
  bytes_rcvd = 0

Aggregate sends: 0
Aggregate receives: 0
```

The following performance comments are approximations only.

If the "Aggregate sends" divided by the count of Memory Channel rails approaches 300-400 MB/s, the cluster may perform better by adding another Memory Channel rail. Additionally, for each system, sum the "bytes_sent" and "bytes_rcvd" attributes and divide the sum by the number of Memory Channel rails. If the total for each system is greater than 60 MB/s, adding an additional rail may provide benefit. Contact your HP representative for more details on RDG performance and statistics.