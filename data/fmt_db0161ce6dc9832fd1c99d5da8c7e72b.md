
以下示例展示了如何使用定时器调查 ZeroAccess rootkit。该 rootkit 采用了多种反取证技术来防止其模块被检测，但结果是一个定时器指向了内核内存的未知区域。

```
$ python vol.py f zeroaccess.vmem
Volatility Foundation Framework 2.1_alpha
Offset Period(ms) Signed Routine
0x005890e 00000084:0xe8b591c 0 0x805232ee ntoskrnl.exe
0x082ae018 00000084:0xfdf3c0c 0 0xb2da3a85 afd.sys
0x081eb0f8 00000084:0xe951f84 0 0xb89c23f0 TDI.sys
0x081de8b7 00000013:0xe2e89642 0 0xf83faff NDIS.sys
0x081e8b40 00000013:0xe2e89642 0 0xf83faff NDIS.sys
0x081e8e28 00000013:0xe2e89642 0 0xf83faff NDIS.sys
```

*(注：原文后半部分多为重复的表格和页码片段，已按要求去重处理。)*

根据此输出，创建可疑驱动对象的内核模块的起始地址为 `0`。这可能是一种反取证技术，旨在防止分析师转储恶意代码。事实上，到目前为止提取该模块确实存在困难，你需要该模块的名称或基地址，而你已经知道名称是不可用的。然而，恶意代码内部包含各种指针；你只需要找到 PE 文件的起始位置。你可以在 `volshell` 中编写少量脚本，使用以下技术之一来实现：

- 选取其中一个地址并向后扫描，寻找有效的 `MZ` 签名。如果恶意 PE 文件中嵌入了其他二进制文件，第一个结果可能不是正确的。
- 在你所拥的最低指针下方 `20KB` 到 `1MB` 之间设置起始地址；然后向前扫描，寻找有效的 `MZ` 签名。

以下代码展示了如何执行该方法：

```
$ python vol.py -f spark.mem volshell
```

```
[snip]
>>> start = 0x81b9db0 - 0x100000
>>> end = 0x81b93690
>>> start < end:
    if addrspace().read(start, 4) == "MZ\x90\x00":
        print hex(start)
        break
    start += 1
0x81b9b80
```

或者，你可以通过调用 `addrspace().vtop(ADDR)` 函数将虚拟地址转换为物理偏移量。如果你有一个原始的、填充过的内存转储，可以在十六进制编辑器打开它并滚动到物理偏移量处——然后滚动寻找 `MZ` 签名。

你在 `0x81b9b80` 处找到了一个 `MZ` 签名，它比定时器和回调程序高约 `8KB`。你也可以在 `volshell` 中验证 PE 头：

```
>>> db(0x81b9b80)
0x81b9b80 4d5a 0000 0300 0400 0000 ffff 0000 MZ...
0x81b9b90 8200 0000 0000 0000 0000 0000 0000..@.
0x81b9b8a 0000 0000 0000 0000 0000 0000 0000
```

# 404 第二部分：Windows 取证

```
0x81b1bb0 0000 0000 0000 0000 0000 ......!.L.!Th
0x81b1bc0 0e1f 00a0 00b4 09cd 21b8 014c 02d 5468 is.program
0x81b1d80 6973 2070 72e6 6772 6176 2063 6216 6e6f t.be.run.in.DOS.
0x81b1ae0 6426 7255 2072 756e 7056 62e0 544f 5320 mode.
0x81b1bf0 6d6f 6465 24e5 00d0 02a0 0000 0000 0000 ......$.
```

最后，你可以为 `moddump` 插件提供一个基地址并从中提取模块：

```
$ python.py -f spark.mem dump -b 0x81b1b80 --dump-dir=OUTPUT
--profile=WinXSP3x6
```

Volatility Foundation Volatility Framework 2.4

| 模块基 | 结果 |
| :--- | :--- |
| 0x81b1b80 | UNKNOWN: driver.81b1b0.sys |

你需要修复找到的 PE 头中的 `ImageBase`：

```
$ python
Python 2.7(v2.7.6:a1b0d274e, Nov 10 2013, 00:42)
[GCC 4.2.1 (Apple build 5666)] on darwin
Type "help", "credits" or "license" for more information.
>>> import pe
>>> pe = pe.PE("driver.81b1b80.sys")
>>> pe.OPTIONAL_HEADER.ImageBase = 0x81b1b80
>>> pe.write("driver.81b1b80.sys")
>>> quit()
```

在 IDA Pro 中加载文件之前的最后一步是为 API 函数生成标签。通常情况下，IDA 可以解析导入地址（IAT）并显示名称，但前提是导入地址已经被修复。在这些情况下，你可以使用可疑模块的基地址和 `idc` 输出格式运行 `impscan`：

```
$ python.py -f spark.mem impscan --base=0x81b1b80 --output=idc
--profile=WinXSP3x6
```

Volatility Foundation Volatility Framework 2.4

```
MakeWord(0x81b1cb90)
MakeName(0x81b1cb90, "PsGetVersion")
MakeWord(0x81b1cb94)
MakeName(0x81b1cb94, "GetProcessFileName")
MakeWord(0x81b1cb98)
MakeName(0x81b1cb98, "ExAllocatePool")
MakeWord(0x81b1cb9c)
MakeName(0x81b1cb9c, "ZwWriteFile")
MakeWord(0x81b1cba0)
MakeName(0x81b1cba0, "ExFreePoolWithTag")
MakeDump(0x81b1cba4)
MakeName(0x81b1cba4, "ZwQueryInformationThread")
```

# 内核取证与 Rootkits

在 IDA Pro 中使用转储的模块，进入 File -> Script 并导出 `impscan` 插件的输出。完成这些步骤后，你应该得到一个具有准确字符串引用和 API 名称的已重建的二进制文件，如图 13-9 所示。

![](img/9e59079ff66884b5d70128a9edb2f4c_430.png)

**图 13-9：** 从内存中移除并在加载到 IDA 后修复了基地址和导入的内核模块

根据你的查询，你可能不需要深入到这种程度。通过 rootkit 在内存中留下的痕迹尽可能地确定其行为。然而，某些情况需要逆向工程才能完全理解代码——这些是可以避免的。你现在知道如何通过结合取证与静态分析来处理这种情况。

> 注意：在我们培训课程几个月后，我们的一位学生分析了内存中的 Uroboros rootkit。你可以在此处阅读分析：http://spresec.blogspot.com/2014/uroboros-rootkit-analysis.html

### 总结

内核领域是内存中一个迷人但广泛的方面。隐藏内核代码、更改操作系统行为的方法有很多。此外，许多分析师对该领域并不熟悉，这降低了他们的证据搜索能力。然而，你已经接触到了最常见的方法，并看到了使用内存取证检测知名 rootkit 的示例。通常情况下，运行在内核中的恶意软件保留在内存中以保持功能。需求通常涉及修改调用表、安装回调或创建新线程——所有操作都会留下供你恢复的痕迹，就像面包屑路径一样。一旦你找到恶意代码占据的内存范围并提取它，剩下的就都是历史了！

# 14 Windows 子系统，第一部分

Windows 图形用户界面（GUI）子系统负责管理用户输入，例如鼠标移动和击键。此外，它绘制显示表面；呈现窗口、按钮和菜单；并提供必要的隔离以支持通过控制台、RDP 和快速切换登录的并发用户。GUI 子系统在日常计算机使用中起着巨大的作用，恶意软件和攻击者在行动过程中修改 GUI 内存不可避免的。遗憾的是，没有取证工具能够分析并报告由该系统创建并维护的痕迹。
