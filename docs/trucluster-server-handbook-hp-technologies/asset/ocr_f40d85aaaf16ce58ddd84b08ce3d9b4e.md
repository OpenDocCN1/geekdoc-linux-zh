The following output displays ICS statistics per channel.

```
# cfstat -i 5 icschanbps
TOTAL BOOT PRI0 PRI1 CPS NET CLSM DRD TUNL CLUA KEVN CFSR RB LD KCH DLM TEST
680m 15k 90m 9k 282m 1m 520 265m 17k 32m 6m 0 0 316k 2m 0
136m 0 0 0 0 0 0 0 0 808 0 0 0 0 0 0
3k 0 0 0 0 0 0 0 0 3k 0 0 0 0 350 0
2k 0 1k 0 284 0 0 0 0 808 0 0 0 0 175 0
7k 0 0 0 7k 0 0 0 0 0 0 0 0 0 0 0
```

The following output gives you an idea of the spectacular quantity of statistics available from cfstat. The "-s" option requests that the display be sorted from largest to smallest and eliminates any zero statistics.

```
# cfstat -s ics | more

ICS static stats:
16 total number of channels (istat_num_chans)
3 total number of priority channels (istat_num_prios)
64 maximum number of services (istat_max_svcs)
27 number of elements per histogram (istat_hist_num_elems)
4 histogram element size (istat_hist_elem_size)

ICS client stats:
31554 number of sync rpcs sent (istat_clirpc)
8404 number of async rpcs sent (istat_climsg)
11 signals forwarded (istat_clisigforward)
1 signal forward retries (istat_clisigforward_retry)

ICS server stats:
319 number allocated handles (istat_svrhand_create)
319 number of handles in use (istat_svrhand)
110854 number of sync rpcs recvd (istat_svrrpc)
11849 number of async rpcs recvd (istat_svrm sg)
1 handle allocs deferred due to no memory (istat_svrhand_nomem)
13 number of daemons created (istat_svrdaemon_create)
13 number of waiting daemons (istat_svrdaemon)

ICS Channel Stats: Total bytes per interval: 403219489 (cli: 8% svr: 91%)
Channel Svcs Usage CliSend CliRecv SvrRecv SvrSend
6 DRD 2 70% 7796 21096 2661844 280235728
3 CPS 4 22% 6984632 16638304 37480556 29464584
9 PRI0 0 4% 2298888 67800 14105516 188824
8 CLUA 1 1% 5821840 1208 2545200 928
9 KEVN 1 1% 216940 0 2113344 0
13 DLM 1 0% 716276 0 685032 0
12 KCH 1 0% 1239311 72644 134066 62348
5 CLSM 1 0% 235564 4 0 0
4 NET 2 0% 118208 0 116964 0
7 TUNL 1 0% 2184 0 110080 0
0 BOOT 3 0% 10800 72 10316 32
15 PBT 1 0% 4912 1640 51596 1736
2 PRI1 0 0% 900 456 452 232
10 CF SR 1 0% 216 36 72 12
11 RB LD 1 0% 0 0 0 0
```