
```
soykozay ray 95> ping -s rosalyn

PINGalyn.biosci.ohio-state.edu: 56 data bytes

64 bytes from rosalyn.biosci.ohio (140.254.12.151):icmp_seq=0, time=1ms

64 bytes from rosalyn.biosci.ohio (140.254.12.151):icmp_seq=1, time=1ms

64 bytes from rosalyn.biosci.ohio (140.254.12.151):icmp_seq=2, time=1ms

64 bytes from rosalyn.biosci.ohio (140.254.12.151):icmp_seq=3, time=1ms

64 bytes from rosalyn.biosci.ohio (140.254.12.151):icmp_seq=4, time=1ms

64 bytes from rosalyn.biosci.ohio (140.254.12.151):icmp_seq=5, time=1ms

64 bytes from rosalyn.biosci.ohio (140.254.12.151):icmp_seq=6, time=1ms

64 bytes from rosalyn.biosci.ohio (140.254.12.151):icmp_seq=7, time=1ms

64 bytes from rosalyn.biosci.ohio (140.254.12.151):icmp_seq=8, time=1ms

64 bytes from rosalyn.biosci.ohio (140.254.12.151):icmp_seq=9, time=1ms

64 bytes from rosalyn.biosci.ohio (140.254.12.151):icmp_seq=10, time=1ms

rosalyn.biosci.ohio-state.edu PING Statistics

11 packets transmitted, 0% packet loss

round-trip (ms) min/avg/max = 1/1/1
```

## 故障排除

注意返回的数据中有几个值得关注的地方。首先是时间字段。该字段表示每个数据包从 `soykozay` 出发返回花费了 1 毫秒。这并不糟糕，但机器处于同一个局域网，所以这很出乎意料。看看如果 `ping` 一个跨国家的机器会发生什么。

```
soykozay ray 92> ping -s archive.wustl

PING archive.wustl: 64 bytes

64 bytes from archive.wustl (128.252.135.4): icmp_seq=0, time=101ms

64 bytes from archive.wustl (128.252.135.4): icmp_seq=1, time=82ms

64 bytes from archive.wustl (128.252.135.4): icmp_seq=2, time=89ms

64 bytes from archive.wustl (128.252.135.4): icmp_seq=3, time=92ms

64 bytes from archive.wustl (128.252.135.4): icmp_seq=4, time=83ms

64 bytes from archive.wustl (128.252.135.4): icmp_seq=5, time=80ms

64 bytes from archive.wustl (128.252.135.4): icmp_seq=6, time=82ms

64 bytes from archive.wustl (128.252.135.4): icmp_seq=7, time=81ms

64 bytes from archive.wustl (128.252.135.4): icmp_seq=8, time=86ms

64 bytes from archive.wustl (128.252.135.4): icmp_seq=9, time=97ms

64 bytes from archive.wustl (128.252.135.4): icmp_seq=10, time=88ms

---

archive.wustl PING Statistics ---

11 packets transmitted, 11 packets received, 0% packet loss

round-trip (ms) min/avg/max = 80/88/101
```

现在，时间上升到了 80–100ms 的范围。对于从俄亥州连接到密苏里州来说，这并不糟糕。现在注意 `icmp seq` 字段。该字段从零开始，每发送一个包增加一。如果 `ping` 返回列表中缺失数字，说明数据包丢失了。你可以看到每个 `ping` 都返回了，在使用 `Control+C` 时偶尔会丢失最后一个包，但任何多于最后一个包的丢失都表明你和你 `ping` 的主机之间的某个地方出了问题。

接下来，你应该查看 `netstat` 的结果。

| Name | Net/Dest Address | Ipkts | Ierr | Oppkts | Oerrs | Collis | Queue |
|---|---|---|---|---|---|---|---|
| le0 | 1500 loopback soykozay.bio | 2577282 | 11 | 185498 | 0 | 16996 | 0 |
| lo0 | 1536 localhost | 1678565 | 0 | 167856 | 0 | 0 | |

如所示，`netstat` 命令返回了每个网络接口的行为响应。`lo0` 接口是环回接口，用于让机器自通信而不是访问网络。`le0` 接口是物理以太网接口。注意该接口读取的数据包 `Ipkts` 字段和写入的数据包 `Opkts` 字段。`Colls` 字段表示有多少个数据包导致了冲突。在这种情况下，冲突占总输出的 0.9%。这个数字非常令人鼓舞。冲突率通常接近 1% 的利用率。`Queue` 字段只有在有排队进入网络的数据包时才会非零。在维护良好的网络中，拥有 0 个 `Oerrs` 是好事，但有 114 个 `Ierrs` 太高了。尽管这只是流量的一小部分，但这仍然是问题的迹象。对于一台只运行了 6 天的机器，`Ierrs` 和 `Oerrs` 也很高，但机器及其周围硬件启动时捕捉到一些初始错误并不罕见。如果下周这些数字再次翻倍，我就会开始担心。

总的来说，

`rosalyn` 看起来相对健康。唯一的警示信号是冲突率偏高，达到了 8%。这并没有违反健康网络“保持在 10% 以下”的规则，对于一台利用率如此低的机器来说，有如此高的冲突率有点奇怪。一种可能的原因是，如果这台机器在更活跃的机器网络中没有产生多少流量。另一种可能性是存在某个“附近”的网络错误，且该机器经常与自身冲突。（还记得绳波和反射波吗？）在没有其他信息的情况下，目前无法确定原因。

接下来使用 `spray` 程序。`spray` 命令字面上是在本地机器能够将数据包发送到线路上时，向远程主机“喷射”数据包：

```
soykozay ray 107 spray rosalyn

sending 1162 packets of length 86 to rosalyn ...

in 10.4 seconds elapsed time,

355 packets (30.55) dropped

112 packets/sec, 9.4k/sec

Sent Rcvd: 77 packets/sec, 6.5k/sec
```
