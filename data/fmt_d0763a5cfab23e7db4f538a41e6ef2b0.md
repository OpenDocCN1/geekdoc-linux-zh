
2012年11月22日 01:11:40,.., [IIS MFT STD_INFO] `ENGINE-1\pumps\pump99.dw` (偏移: `0x25f8000`)

2012年7月27日 01:11:40,mac,.. [IIS MST STD_INFO] `WINDOWS\webui\netstat.dll` (偏移: `0x1ced800`)

2012年7月27日 01:11:40,m..., [ENG MST STD_INFO] `WINDOWS\webui\netstat.dll` (偏移: `0x10b97400`)

`netstat.dll` 文件（一个 RAR 压缩包）随后通过命令与控制服务器下载到攻击者的本地机器：

```
2012年7月27日 01:15:44,mac, [Gh0st Decode] 172.16.150.20:1238->58.64.132.141 COMMAND: DOWN

C:)WINDOWS\webui\netstat.dll

2012年7月27日 01:15:44,mac, [Gh0st Decode] 172.16.150.20:1238->58.64.132.141 TOKEN: FILE DATA (2713)

2012年7月27日 01:15:44,mac, [Gh0st Decode] 172.16.150.20:1238->58.64.132.141 TOKEN: FILE DATA (8183)

2012年7月27日 01:15:44,mac, [Gh0st Decode] 172.16.150.20:1238->58.64.132.141 TOKEN: FILE SIZE

C:)WINDOWS\webui\netstat.dll [10992]
```

## 现代获取方法

之前描述的 32 位系统历史获取方法存在局限性，这导致取证社区的开发人员创建了专门的内存获取工具。这些工具为执业人员在获取过程中提供了更大的灵活性，但也要求你向目标系统加载第三方软件以收集证据。随着 64 位系统的出现，另一个用户态接口 `/proc/kcore` 再次开启了直接从用户态获取物理内存的可能。在本节中，我们将讨论 `/proc/kcore`、`fmem` 和 `LiME` 获取工具，以及各自的优缺点。

## fmem

为了缓解在 32 位系统上使用 `/dev/mem` 时遇到的问题，人们创建了 `fmem` (http://hysteria.sk/~niekt0/foriana/fmem_current.tgz) 项目。`fmem` 通过加载一个内核驱动来运行，该驱动会创建一个设备名称 `/dev/mem`。该设备的操作与 `/dev/mem` 类似，都会导出物理内存供其他程序访问，但具有许多优势。第一个优势是它在访问内存之前会检查页面是否存在于内存中（通过调用 `page_is_ram_function` 函数）。这防止了调查人员意外读取内存或未映射的物理地址，从而导致了稳定性问题（第 4 章）。`fmem` 的另一个优势是它可以访问 896MB 边界以上的物理页，而 `/dev/mem` 则不能。

`fmem` 的唯一缺点是要求调查人员检查 `/proc/iomem` 以确定 RAM 的映射位置。如前所述，对于未将所有主内存映射到物理偏移 0 的机器来说，这是必要的。在某些系统上，RAM 被划分为许多不同的段。例如，在具有 304MB 物理内存并启用 PAE 的 VMware Debian 工作站上，`/proc/iomem` 的初始输出如下：

```
$ cat /proc/iomem

00000000-000ffff : reserved

00010000-000f3fff : System RAM

0009f400-000ffff : reserved

000a0000-00bffff : PCI Bus 0000:00

000a0000-00bffff : Video RAM area

000c0000-00c7fff : Video ROM

000ca000-00cbfff : reserved

000ca000-00caffff : Adapter ROM

000cc000-00cffff : PCI Bus 0000:00

000d0000-00d3fff : PCI Bus 0000:00

[snip]
```

在输出输出中，你可以看到每个内存范围的起始和结束物理地址以及其名称。你感兴趣的获取范围是那些命名为 `System RAM`（系统内存）的范围。要专门地找到这些范围，你可以在文件中进行搜索：

```
$ grep "System RAM" /proc/iomem

00100000-009f3ff : System RAM

00100000-bffff : System RAM

bff000000-bffff : System RAM

10000000-10bffff : System RAM
```
