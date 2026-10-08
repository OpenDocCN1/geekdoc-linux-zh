```
# rpcinfo -p
program vers   proto   port
  100000    2   tcp    111  portmapper
  100000    2   udp    111  portmapper
  100024    1   udp    779  status
  100024    1   tcp    779  status
  100021    1   tcp    783  nlockmgr
  100021    1   udp   1035  nlockmgr
  100021    3   tcp    787  nlockmgr
  100021    3   udp   1036  nlockmgr
  100020    1   udp   1037  llockmgr
  100020    1   tcp    792  llockmgr
  100021    2   tcp    795  nlockmgr
  100068    2   udp   1040  cmsd
  100068    3   udp   1040  cmsd
  100068    4   udp   1040  cmsd
  100068    5   udp   1040  cmsd
  100083    1   tcp   1036  ttbdserver
  100005    1   udp    976  mountd
  100005    1   tcp    978  mountd
  100003    2   udp   2049  nfs
  150001    1   udp   1003  pcnfstd
  150001    2   udp   1003  pcnfstd
  150001    1   tcp   1006  pcnfstd
  150001    2   tcp   1006  pcnfstd
#
```

Many daemons are running on the system that are important to the functionality I like to use. **mountd** is running, which indicates that a server could NFS mount file systems on this computer. There is other setup required for the mount to take place, but at least the daemon is running to support this functionality. In addition, **pcnfstd** is running, meaning that we have support for Windows-based NFS access.