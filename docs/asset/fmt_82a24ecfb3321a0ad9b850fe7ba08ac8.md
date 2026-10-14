
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
// 获取范围
为了采集显存，你可以重新定义 `LINE_RAMSTR` 为 `Video ROM`（以仅采集显存），或在代码中添加额外的检查以同时采集系统内存和显存。

# 验证采集工具

如第 4 章所述，与设备和硬件资源预留的内存范围交互的采集工具会导致内存损坏和/或错误。通过通过内存样本上使用 `linux_iomem` 插件，你可以验证采集工具是否获取了预期的内存区域。为了说明，你将看到一个使用 LiME 采集的内存示例，但你也可以使用相同的方法验证生成结构化文件格式的其他工具。

## 注意

使用非结构化（原始或 dd 风格）零填充内存样本正变得越来越常见，因为 64 位系统拥有巨大的空间，原始 dump 是不切实际且浪费资源的。

# 内核内存迹

以下输出显示了如何使用 `limeinfo` 插件打印 LiME 采集的内存范围：

```
$ python vol.py --profile=LinuxDebian-3_x64 -f debian.lime limeinfo
```

| 内存 | 结束 | 大小 |
| :--- | :--- | :--- |
| 0x0000000000000000 | 0x00000000009eff | 0x00000000008f00 |
| 0x0000000010000000 | 0x00000003deffff | 0x000000002fde00 |
| 0x00000003ff000000 | 0x0000ffffffff | 0x0000c00000 |

你看到了三个范围，并得到了每个范围的起始地址、结束地址和大小。下一个命令显示了如何使用 `linux_iomem` 插件并过滤输出以显示系统 RAM：

```
$ python vol.py --profile=LinuxDebian-3_x64 -f debian.lime linux_iomem | grep "System RAM"
```

| 资源名称 | 起始地址 | 结束地址 |
| :--- | :--- | :--- |
| System RAM | 0x10000 | 0xFFFF |
| System RAM | 0xC0000 | 0xDFFFF |
| System RAM | 0xFF0000 | 0xFFFFF |

如果你将地址与 `limeinfo` 输出进行比较，它们是相同的。这表明 LiME 了正确的系统范围。如果采集了额外的范围或缺少任何 RAM 范围，说明工具可能运行异常。这种行为的主要原因是工具设计不当和恶意干扰。如果你确定工具设计不正确（例如导致省略范围的错误），应考虑不要使用该工具。另一方面，如果由于恶意软件操作内存范围导致范围跳过，你可以利用这些细节定位数据。

# 虚拟内存映射

Linux 在虚拟地址空间中预留了若干区域来存储数据类型。与 Windows 类似，Linux 在用户和内核内存之间设置了边界。例如，在 32 位系统上，用户态是下方 3GB，内核模式是上方 1GB。这意味着内核从 `0xC00000` 开始，直到内存结束 `0xFFFFFFFF`。在 64 位系统上，内核从 `0xFFFFFF800000` 开始。这种划分如图 23-1 所示，带有你可以应用于内核内存区域的标签。

![](img/9e59079ff6684b5d70128a9edb2f4c_687_0.png)

图 23-1：Linux 虚拟内存布局

如图所示，内核地址空间的起始是内核的映射，包含了内核的可执行代码 `.text`、读/写数据 `.data` 和未初始化变量 `.bss`。你可以根据相应的符号在内存中找到这些每一项。例如，文本段从 `_text` 到 `_etext`，数据段从 `_sdata` 到 `_edata`，bss 段从 `_bss_start` 到 `_bss_end`。精确地址在链接脚本中指定，但在编译时才计算，它们在系统之间不同。然而，它们在 `System.map` 文件中填充，因此在构建配置后，你可以为特定机器找到它们。

你可以看到以下 Volatility 代码如何使用代码符号：

```
is_kernel_text(addr_space, addr):
    profile = addr_space.obj_vm
    text_start = profile.get_symbol("_text")
    text_end = profile.get_symbol("_etext")
    return (addr_space.address_compare(addr, text_start) != -1 \
        and addr_space.address_compare(addr, text_end) == -1)
```

`is_kernel_text` 函数可以被想要地址是否在内核代码段内的调用者调用。正如你在 26 中看到的，某些函数（如实现系统调用的函数）在干净系统中位于内核段内，但经常被恶意软件在别处覆盖。例如，`linux_check_syscall` 函数遍历每个系统处理程序，并使用与 `is_kernel_text` 函数类似的逻辑来确定处理程序是否在受信任区域（假设 `vmlinux` 文件在磁盘或内存中未被感染）。

图 23-1 显示了 `vmalloc` 区域，它用于存储虚拟连续的区域，例如内核模块、视频缓冲区和交换页。`System.map` 文件指向 `vmalloc` 的起始和结束，即 `VMALLOC_START` 和 `VMALLOC_END`。你还可以看到存储在内核数据段中的 `module_addr_min` 和 `module_addr_max` 变量。这些变量识别了 vmalloc 内部存储已加载模块的范围。因此，你可以利用它们寻找隐藏的模块（通过扫描范围内的所有内存）。

# 第三部分：Linux 内存取证

## 分析目标

你的目标如下：

* **恢复 USB 序列号**：调试缓冲区（debug buffer）包含了最近插入计算机的可移动媒体设备的详细信息（序列号、驱动器名称等）。这可以帮助你将物理设备（如 USB 或 Firewire 火线驱动器）与读取或写入该设备的机器匹配起来。
* **检查网络活动**：你通常会在调试缓冲区中发现网络设备进入混杂模式（promiscuous mode）的痕迹。此外，你还可能能够识别出与无线网络连接、远程网络共享和文件传输的交互。
* **构建事件时间线**：除了调试缓冲区的内容外，缓冲区中的每个条目还包含一个时间戳，指示该条目记录的时间。你可以将其与磁盘和内存一起用于构建时间线。

## 数据结构

从 3.5.x 内核版本开始，Linux 通过一系列日志结构来跟踪缓冲区内的消息。此版本之前的内核将缓冲区存储为简单的字符数组。以下是日志结构外观的示例：

```
>>> (*log)
'log' (16 bytes)
0x0 : ts_nsec ['unsigned long long']
0x8 : len ['unsigned short']
      : len ['unsigned short']
0xa : text_len ['unsigned short']
0xc : dict_len ['unsigned short']
0xe : facility ['unsigned char']
0xf : flags ['BitField', {'end_bit': 5, 'start_bit': 0}]
      : level ['BitField', {'end_bit': 8, 'start_bit': 5}]
```

## 关键点

关键点如下：
* `ts_nsec`：显示调试消息被记录的时间戳。记录的时间自机器启动以来的纳秒数。
* `text_len`：日志中文本部分的长度。
* `len`：文本部分加上头部信息的总长度。
* `level`：该成员决定消息的严重程度，例如信息性或错误状态。

# 内核内存制品

`linux_dmesg` 插件可以恢复内核调试缓冲区。对于所有版本，恢复过程都从记录 `log_buf` 和 `log_buf_len` 变量的地址开始。如前所述，数据的格式取决于内核版本，插件要么解析字符（3.5 之前），要么解析日志结构（3.5 及以后）。

以下显示 `linux_LinuxDebian-3.2_64 -f debian.linux_dmesg` 的输出：

```
$ python vol.py --profile LinuxDebian-3.2_64 -f debian.linux_dmesg
[0.00000] Initializing cpus cpu
[0.00000] Linux Version 3.2.0-amd64 (linux-kernel@lists.debian.org)
[0.00000] gcc 4.6.3 (Debian 6.3-14) #1 SMP Debian 3.2.51-1
```
