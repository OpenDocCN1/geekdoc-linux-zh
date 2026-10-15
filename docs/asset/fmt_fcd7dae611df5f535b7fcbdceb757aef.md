
## 安全

![](img/97fdf078658cf34e6c480f18f1f2014d_73_0.png)

从文件系统的日志中获取必要信息，但由于我们不再继续进行操作，因为显然有更好的方法，正如你将在下一节中看到的。

加密原生文件是安全的，当你决定需要它时，它会为你提供额外的便利。然而，它留存在泄露密钥的风险，所以你应该考虑其他方法。

## 超越未检测

TestDisk 是一个强大的工具，尽管它缺乏对 ext3 和 ext4 的支持。如果支持的文件系统仍然完好地存在，就可以恢复任何支持的文件系统。如果是这种情况——尽管我们可以从损坏的文件系统是一场赛跑这一事实获得慰藉——我们需要进行一些取证工作。如果 TestDisk 发生崩溃，这些技术也可以用于 ext3 或 ext4。

在这些情况下，与其仅仅拒绝删除的文件，不如搜索文件碎片，然后对分区的结构进行详细了解。数据恢复操作提供了此类服务，但有一个程序可以让你自己完成。正如名称所示，这个特定工具完全能够恢复超过 480 种不同的格式，使用所有可以想象的格式，包括电影、音频文件和 LibreOffice 文档非常直接，所以我们希望你尝试一下，但我们确实提到一个可能被忽视的事实。

我们要求你选择一个已删除的分区，在选择之后，在继续之前，这会将你带到一个界面，询问你想要搜索的文件类型或通过详细信息。然后，通常你按 `S` 删除所有文件类型，然后在高亮你感兴趣的每种类型后，使用右箭头键。因为减少搜索的文件数量将显著提高速度——但在测试中，搜索所有文件类型将花费太长时间，而这将 JPG 的搜索缩短到了 15 分钟——只需确保你选择了感兴趣的类型即可。

```
mkfile-PC:\Users> photos shred P0079921.jpg -uvz -n 18
shred: P0079921.jpg; pass 1 ([random])
shred: P0079921.jpg; pass 2 ([aaaa])
shred: P0079921.jpg; pass 3 ([bbdd])
shred: P0079921.jpg; pass 4 ([cccc])
shred: P0079921.jpg; pass 5 ([random])
shred: P0079921.jpg; pass 6 ([random])
shred: P0079921.jpg; pass 7 ([random])
shred: P0079921.jpg; pass 8 ([random])
shred: P0079921.jpg; pass 9 ([random])
shred: P0079921.jpg; pass 10 ([random])
shred: 00000000; renamed to 00000000
shred: 00000000; renamed to 00000000
shred: 00000000; renamed to 00000000
shred: 00000000; renamed to 00000000
shred: 00000000; renamed to 00000000
shred: 00000000; renamed to 00000000
shred: 00000000; renamed to 00000000
shred: 00000000; renamed to 00000000
shred: 00000000; renamed to 00000000
shred: 00000000; renamed to 00000000
shred: 00000000; renamed to 00000000
shred: P0079921.jpg; removed
mkfile-PC:\Users> _
```

> Shred 删除的文件是不可替代的，取决于你使用的工具，它会处理得很彻底。

当 PhotoRec 运行后，你为恢复的文件选择的位置将被带有类似 dir 的扫描名称的文件夹填充，每个文件夹都包含恢复的文件。有一个障碍：PhotoRec 无法恢复它所恢复的文件名。那么找到你想要的文件并不容易。你当然可以在管理器中查看它们，这取决于你选择什么选项，这样你将能够通过扫描缩略图找到你的文件。但即使这也可能困难，取决于 PhotoRec 的工作原理。使用 TestDisk 时，你只会从成百上千个项目的列表中发现你的奖品——直到你找到那一个。

不幸的是，损坏的文件系统可能比意外删除的文件糟糕得多，情况可能会变得糟糕——糟糕得多。如果你曾经听过硬盘发出刮擦声或持续……

## 大力安全删除

![](img/97fdf078658cf34e6c480f18f1f2014d_73_1.png)

# 黑客手册 2024

## 软件

发现最强大的 Linux 软件并开始使用

- 78 OpenELEC  
  熟悉适用于桌面和嵌入式环境的媒体中心系统。
- 82 Virtual Box  
  通过我们的核心指南，确保你的虚拟系统发挥最大价值。
- 86 NextCloud  
  这个突破常规的、全新的云存储和文档系统为所有人服务。
- 90 Nagios  
  工业级监控系统，让你能够追踪所有的 Linux PC。

```python
import os
import random
import time
import subprocess

d_path = os.path.abspath("xlex.txt")

if not os.path.exists(d_path):
    with open(d_path, "w") as f:
        for i in range(100):
            f.write(f"line {i}: {random.randint(1, 100)}\n")

with open(d_path, "r") as f:
    lines = f.readlines()
    for line in lines:
        if random.random() > 0.5:
            print(f"Processing: {line.strip()}")
```
