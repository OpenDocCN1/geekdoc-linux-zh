
## ICS Services per ICS Channel

| Channel # | Services | Cluster Subsystem | # of Services | ICS Server Daemon |
|---|---|---|---|---|
| BOOT 0 | CNX (CLUSTER_PANIC) | cnx | 3 | per node |
|  | SIGNAL | ics_hl |  | custom |
|  |  | ics_hl |  | from pool |
| PRI0 1 | none | n/a | 0 | n/a |
| PRI1 2 | none | n/a | 0 | n/a |
| CFS 3 | ADVFS, CFS, FS | cfs | 4 | from pool |
|  | CMS | cms |  | from pool |
| NET 4 | CLUMGT | cluabase | 2 | from pool |
|  | ICSNET | icsnet |  | custom |
| CLSM 5 | CLSM | clsm | 1 | from pool |
| DRD 6 | DRDV1, DRDV2 | drd | 2 | from pool |
| TUNL 7 | TUNNEL | clua | 1 | per node |
| CLUA 8 | CLUA | clua | 1 | per node |
| KEV M 9 | KEV M | kevm_clu | 1 | per node |
| CFSR 10 | CFSREC | cfs | 1 | from pool |
| RBLD 11 | RBLD | cnx | 2 | from pool |
|  | SSN | n/a |  | from pool |
| KCH 12 | KCH | kch | 1 | from pool |
| DLM 13 | DLM | dlm | 1 | per node |
| TEST 14 | (TEST1), (TEST1), (TEST2), (TEST3), (TEST4), (TEST5), (TEST6), (TEST7) | n/a | 7 | varies |
| PBT 15 | MCTCTL_SVC | ics_ll_met | 1 | per node |

### Table 18-1: ICS Services per ICS Channel

### 18.1.2.5 ICS Server Nanny Process [icssvr_nanny]

So who’s in charge of all these hale and hearty ICS server processes? When you were young, you may have had a nanny looking after you (or maybe you just had your older brother, a neighbor, or weird old Hal from down the street); similarly, the ICS server processes are watched over by the "nanny" process. It will cause the creation of the pool-based processes when needed and will cause the creation of the per-node based processes as members come and go from the cluster.

If you were a really rambunctious kid, and you had lots of siblings, you may have needed a second nanny. Similarly, when the ICS server nanny is overstressed, it may be joined by other nannies. (We guess they just call for backup assistance when necessary.) Note that, as of this writing, it would be unusual to see more than one nanny.

## 18.1.3 ICS Attributes

The following output provides information on the sysconfig attributes supporting ICS.

### NOTE:

A typical cluster member will use ics_ll_tcp or ics_ll_mct attributes but not both, although both sets of attributes will be visible. Also, note that the low-level attributes are undocumented and should not be altered unless you are directed to change them by HP engineering. We include them here to show the existence of software levels within the ICS subsystem.

```
# for i in $(sysconfig -m | grep ics | cut -d: -f1)
> do
> print
> sysconfig -q $i
> done

ics_hl:
ics_hl_debug = 1
Module_Config_Name = attribute does not allow this operation
ics_hl_verbose = 2
ics_idle_daemons_lwm = 4
ics_idle_daemons_hwm = 15

ics_ll_tcp:
Module_Config_Name = attribute does not allow this operation
ics_tcp_rendezvous_port = 0
ics_tcp_ports[0] = 0
...
ics_tcp_ports[15] = 0
ics_tcp_inetaddr0 =
ics_tcp_netmask0 =
ics_tcp_adapter0 =
ics_tcp_ipmtu0 = 1500
ics_tcp_nro[0] =

ics_tcp_nro[7] =
```

ICS High-Level Attributes.

ICS Low-Level TCP Attributes.

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
