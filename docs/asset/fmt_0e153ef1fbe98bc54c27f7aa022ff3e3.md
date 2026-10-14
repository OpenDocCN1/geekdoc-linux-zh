
```
Name Mtu Network Address Ipkts Ierrs Opkts Oerrs Coll

f0a 4352 <Link> 00:60:d5:da:54 0 0 326 0 0

f0a 4352 DLI none 0 0 326 0 0

tu 1500 <Link> 00:f8:la:de:7b 0 0 324 0 0

tu 1500 DLI none 0 0 324 0 0

tul 1500 <Link> 00:f8:la:d5:54:44 97600 708 5283 32 388

tul 1500 DLI none 97600 708 5283 32 388

tul 1500 violet-net beach 97600 708 5283 32 388

slo* 296 <Link> 0 0 0 0 0

lo0 4096 <Link> 12861 0 12861 0 0

lo0 4096 loop localhost 12861 0 12861 0 0
```

接下来，为了确定计数器是否在增加，我们使用了 `netstat` 命令，这次指定了五秒的间隔，并仅检查单个接口。间隔时间的选择是非常随机的，尽管五秒钟已经足够观察错误是否在增加。如果你不基于间隔来查看计数器，那么错误可能发生在过去的某个时候，并表明存在持续的问题。

```
# netstat -I tul 5

input (tul) output input (Total) output

packets errs packets errs cols packets packets errs cols

985099 757 5943 32 411 998087 757 19587 359 411

513 1 5 0 0 513 1 7 1 0

551 0 5 0 0 566 0 20 0 0
```

## 7.1 网络硬件问题

| 562 | 1 | 18 | 0 | 2 | 562 | 1 | 18 | 0 | 2 |
| 530 | 0 | 25 | 0 | 0 | 537 | 0 | 32 | 0 | 0 |
| 529 | 0 | 12 | 0 | 0 | 529 | 0 | 12 | 0 | 0 |
| 518 | 0 | 12 | 0 | 0 | 525 | 0 | 19 | 0 | 0 |
| 519 | 5 | 13 | 0 | 1 | 519 | 5 | 13 | 0 | 0 |
| 548 | 1 | 21 | 0 | 0 | 557 | 1 | 30 | 0 | 0 |
| 611 | 1 | 12 | 0 | 0 | 611 | 1 | 14 | 1 | 0 |

最后，我们需要弄清 `tul` 上错误的性质。如前所述的，可以使用 `netstat` 命令查看链路统计数据，以帮助判断问题是否为硬件问题。结果如下：

```
# netstat -I tul -s

tul Ethernet counters at Wed May 8 13:41:55 2002

11819 seconds since last zero

185621263 bytes received

919489 bytes sent

994983 data blocks received

6190 data blocks sent

176092764 multicast bytes received

983931 multicast blocks received

46525 multicast bytes sent

341 multicast blocks sent

258 blocks sent, initially deferred

76 blocks sent, single collision

172 blocks sent, multiple collisions

33 send failures, reasons include:

0 collision detect check failure

76 receive failures, reasons include:

Block check error

Framing Error

Frame too long

0 unrecognized frame destination

0 data overflows

0 system buffer unavailable

0 user buffer unavailable
```
