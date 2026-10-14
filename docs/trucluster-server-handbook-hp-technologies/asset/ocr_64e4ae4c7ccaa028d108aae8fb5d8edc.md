```
ics_ll_mct:
ics_mct_debug_flags = 0
ics_mct_fsw_timeout = 4096
ics_mct_raw_timeout = 4096
ics_mct_old_vers = 1
ics_mct_new_vers = 1
ics_mct_heap_timeout = 30
ics_mct_small_bucket = 512
ics_mct_medium_bucket = 2048
ics_mct_large_bucket = 8192
ics_mct_frag_freeLim = 32
ics_mct_nodedown_timeout = 100
ics_mct_nodedown_paniclimit = 0
ics_mct_enabled = 1
ics_mct_auto_oobucket_up = 0
ics_mct_hb_disable = 0
ics_mct_yield_ticks = 10
Module_Config_Name = attribute does not allow this operation

icsnet:
hdw_addr = 42:00:00:00:00:01
verbose = 0
icsnet_mtu = 7000
```

ICS Low-Level Memory Channel Transport Attributes.

Network Interface Communication Attributes.

Internally managed MAC address.

In order to quickly handle spikes of activity from ICS client services requesting unordered activities (such as CFS and DRD), a pool of idle processes is kept ready. The ics_hl subsystem attribute ics_idle_daemons_lwm sets the low water mark for this pool. The process count may grow up to ics_idle_daemons_hwm and even grow beyond it to handle heavy bursts of activity.

```
# sysconfig -q ics_hl ics_idle_daemons_hwm
ics_hl:
ics_idle_daemons_hwm = 15
```

```
# ps aux | grep icsvr_daemon_fr | wc -l
18
```

Once the process count has been increased, it will never fall back below the high water mark, and it won’t decrease at all if it stays less than the high water mark. The previous output shows the attribute values and then counts the current number of processes. In this case, the count exceeds the high water mark. If this situation arises consistently, the ics_idle_daemons_hwm may need to be raised since it could indicate a constant creation and deletion of the ICS daemon processes. If the kernel process creator daemon shows noticeable CPU time, you should raise the high water mark.

```
# ps -eo user,pid,time,command | awk '/USER|kproc/ { print $0 }'
USER       PID   TIME COMMAND
root    524290 0:00.05 [kproc_creator_da]
```