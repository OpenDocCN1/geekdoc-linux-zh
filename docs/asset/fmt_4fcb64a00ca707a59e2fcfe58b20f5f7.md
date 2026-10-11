
`监控`是 Linux 管理员花费时间最多的活动，涉及定期检查日志文件并运行性能实用程序以识别问题及其产生的原因。`主动维护`涉及采取必要的步骤来最大限度地减少未来出现问题的概率或其影响。执行定期系统备份和识别潜在问题区域是`主动维护`的示例。所有`主动维护`任务都应该记录下来以备后参考。这些信息连同任何数据备份，对于系统遭受灾难性故障时重建你的系统至关重要。

`响应性维护`涉及在监控期间出现问题时进行纠正。当问题解决后，需要对其进行记录并主动调整系统，以减少未来发生相同问题的概率。此外，记录问题的解决方案创建了一个行动模板，允许对后续或类似的问题进行更快的补救。

![](img/bafa5678973f896b93838a140b8f7840_653_0.png)

**图 14-1** 维护周期

来源：Course Technology/Cengage Learning

## 故障排除方法

任何系统文档都应该打印并保留在日志文件中，因为如果保存在 Linux 系统本身，这些信息在系统故障期间可能会丢失。

`响应性维护`进一步由许多被称为`故障排除`步骤的程序组成，用于以系统化的方式高效解决问题。

当问题发生时，你需要尽可能收集有关该问题的信息。这可能包括检查系统日志文件、查看 `/proc` 文件系统的内容，以及运行信息工具（如 `ps` 或 `mount`）。此外，你可能可以在互联网、网站和新闻组上研究问题的症状，并查找用于检查某些特定问题的日志文件和命令。

```
tail -f /path/to/logfile 命令对特定日志文件进行连续查看。这允许你在新条目被添加时就看到它们，这在收集系统问题信息时非常有用。
```

随后，你需要通过检查收集的信息来隔离问题。确定问题是持续的还是间歇性的，以及它影响影响所有用户还是仅影响你。

根据这些信息，你可能会生成一个可能的原因和解决方案列表，并按概率最大的解决方案排在列表顶部，概率最小的解决方案放在底部。利用互联网进行此操作是有益的，因为许多 Linux 问题都发布在网站或新闻组上。此外，在本地 Linux 用户组发布问题可能会产生许多解决方案。

接下来，你需要实施并测试每个可能的解决方案，直到问题得到解决。一次只应用一个更改是非常重要的。如果你进行了多处修改，将不清楚是哪种修改起作用以及为什么。

问题解决后，记录解决方案以备后参考，并继续采取主动措施以减少未来相同问题再次发生的概率。这些`故障排除`步骤如图 14-2 所示。

图 14-2 列出的`故障排除`步骤可作为指南。你可能需要针对某些问题更改方法。记住，`故障排除`是一门艺术，然而，有两条黄金法则应该在`故障排除`期间指导你：

- **问题优先级排序**——如果你需要解决多个问题，请根据严重程度对问题进行排序，并将时间花在严重的问题上。固结于小问题而忽略大问题会导致效率大大降低。如果问题在时间内难以解决，寻求帮助是良好的做法。
- **尝试解决根源**——某些解决方案在短期内可能是有效的，但从长期来看会由于底层问题而失效。有效的`故障排除`需要良好的直觉，而直觉源于对硬件和配置的扎实知识。为了避免错过任何问题的底层原因，尝试证明为什么某个解决方案有效。如果不清楚为什么解决方案有效，你可能错过了问题的底层原因，该原因可能在未来需要处理以防止相同问题再次发生。

![](img/bafa5678973f896b93838a140b8f7840_655_0.png)

**图 14-2** 常见`故障排除`步骤

来源：Course Technology/Cengage Learning

## 解决常见系统问题

Linux 系统上可能的问题太多，无法在此列出。然而，作为`故障排除`者，你最常遇到本节描述的常见问题。所有 Linux 问题可以分为三类：硬件相关、软件相关和用户界面相关。

## 硬件相关问题

虽然硬件问题可能是硬件损坏，但许多硬件相关问题涉及硬件或软件配置不当。如果硬件问题在安装 Linux 后立即出现，通常就是这种情况。

可能是外设电缆或计算机内部松动或连接不当的内存条。

某些与硬件相关的问题会阻止 Linux 操作系统使用硬件。这些问题通常特定于硬件类型。通过查看 `dmesg` 命令的输出或 `/var/log/boot.log` 和 `/var/log/messages` 日志文件的内容可以隔离硬件问题。

缺少设备驱动程序会导致操作系统无法使用关联硬件设备。通常，Linux 内核会在启动时检测新的硬件设备，并自动为它们配置驱动模块。然而，如果内核无法访问某些设备的适当驱动模块，则该设备无法使用。你可以通过查看 `dmesg` 命令的输出来查看 Linux 内核检测到的硬件。要查看 Linux 检测到的 USB 设备，可以使用 `lsusb` 命令，如下：

```
[server1~]# lsusb
Bus Device 002: 05ac:0302 Apple, Inc. Optical Mouse (Fujitsu)
Bus Device 002: 01ID 1d6b:0001 Linux Foundation 1.1 root bus
Bus Device 001: 01ID 1d6b:0002 Linux Foundation 2.0 root bus
```

同样，要查看 Linux 内核检测到的 PCI 设备，你可以使用 `lspci` 命令，并查看以下输出：

```
[server1~]# lspci
000:00.0 Memory: nvidia Corporation C51 Host Bridge (rev a2)
000:01.1 Memory: nvidia Corporation C51 Memory Controller 0 (rev a2)
000:02.2 Memory: nvidia Corporation C51 Memory Controller 1 (rev a2)
000:03.3 Memory: nvidia Corporation C51 Memory Controller 5 (rev a2)
000:04.4 Memory: nvidia Corporation C51 Memory Controller 4 (rev a2)
000:05.5 Memory: nvidia Corporation C51 Host Bridge (rev a2)
000:06.6 Memory: nvidia Corporation C51 Memory Controller 3 (rev a2)
000:07.7 Memory: nvidia Corporation C51 Memory Controller 2 (rev a2)
00:03.0 PCI bridge: nvidia Corporation C51 PCI Express Bridge (rev a1)
00:05.0 VGA compatible controller: nvidia Corporation C51 [GeForce Go 6100] (rev a2)
00:09.0 Memory: nvidia Corporation MCP51 Host Bridge (rev a2)
00:0a.0 Isa bridge: nvidia Corporation MCP51 LPC Bridge (rev a3)
00:0a.1 SMBus: nvidia Corporation MCP51 SMBus (rev a3)
00:0a.3 Co-processor: nvidia Corporation MCP51 PMU (rev a3)
00:0b.0 USB Controller: nvidia Corporation MCP51 USB Controller (rev a3)
00:0b.1 USB Controller: nvidia Corporation MCP51 USB Controller (rev a3)
00:0d.0 IDE interface: nvidia Corporation MCP51 IDE (rev f1)
00:10.0 PCI bridge: nvidia Corporation MCP51 PCI Bridge (rev a2)
00:10.1 Audio device: nvidia Corporation MCP51 High Definition Audio (rev a2)
00:14.0 Bridge: nvidia Corporation MCP51 Ethernet Controller (rev a3)
00:18.0 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron]
```

![](img/bafa5678973f896b93838a140b8f7840_656_0.png)

Hyper Technology Configuration

14

© Cengage Learning. 版权所有。未经许可不得分发。

# 故障排除、性能与安全
