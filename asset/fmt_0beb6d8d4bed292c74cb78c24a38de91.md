
```bash
# vparstatus -p cable2 -v

[Virtual Partition Details]
Name:	cable2
State:	Up
Attributes:	Dynamic, Manual
Kernel Path:	/stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:	1/3
Bound by User [Path]:
Bound by Monitor [Path]:	37	<-- one CPU in use at 37
Unbound [Path]:

[IO Details]
0.8.0.0.8.0.5.0.0.0	BOOT
0.10

[Memory Details]
Specified [Base	/Range]:
		(bytes)	(MB)
Total Memory (MB):	1024
#
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_367_0.png)

这两个 `vparstatus` 命令的输出显示 `cable1` 有一个已绑定 CPU，`cable2` 也有一个已绑定 CPU。在这些 vPar 被创建的 L-Class 系统上，总共有四个 CPU。这意味着应该有两个 CPU 可用。让我们运行 `vparstatus -A` 来查看系统上的可用组件：

```bash
# vparstatus -A
[Unbound CPUs (path)]:	97
				101
[Available CPUs]:	2

[Available I/O devices (path)]:	0.1
0.2
0.3
0.4
0.5
0.9
0.12
32
36
```

```text
          96
         100

[Unbound memory (Base  /Range)]:  0x0/64
                (bytes) (MB)     0xc000000/1856
                                 0x18000000/128

[Available memory (MB)]:   2048
#
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_368_0.png)

此输出证实有位于硬件路径 97 和 101 的两个 CPU 可用。我们可以通过多种方式来添加这些 CPU。让我们使用 `varmodify` 命令将 `cable1` 中的 `num` CPU 数量更改为两个 CPU。我们通过使用 `-a` 在当前 CPU 数量的基础上 *添加* 一个来实现这一点。这是一个相对操作，即会在当前 CPU 数量的基础上增加一个 CPU。如果你想指定 vPar 的绝对 CPU 数量而不是相对数量，可以使用 `varmodify -m`。以下展示了该 `varmodify` 命令：

```bash
# varmodify -p cable1 -a cpu::1
#
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_368_1.png)

现在我们可以运行 `vparstatus -p cable1 -v` 来确认 CPU 已添加，如下列清单所示：

```bash
# vparstatus -p cable1 -v

[Virtual Partition Details]
Name:          cable1
State:         Up
Attributes:    Dynamic,Manual
Kernel Path:   /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:   1/3
Bound by User [Path]:
Bound by Monitor [Path]:  33    <-- original CPU @ 33
Unbound [Path]:   97           <-- unbound CPU @ 97
[IO Details]
     0.0
     0.0.1.1.2.0  BOOT
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_369_0.png)

```text
[Memory Details]

    Specified [Base /Range]:
    (bytes)(MB)

Total Memory (MB) : 1024
```

`vparstatus` 的输出显示，位于硬件路径 97 的 CPU 确实已通过 `varmodify` 命令添加到 `cable1` 中。

此外，我们可以运行 GlancePlus 或 `top` 来确认 `cable1` 上有两个 CPU 正在使用。以下是在 `cable1` 上运行的 `top` 输出：

![](img/eff8b9287a5f38c5adf538f24aacf29e_369_1.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_369_2.png)

```bash
# top

System: cvcub0002                         Thu Oct 4 15:30:42 2001

Load averages: 0.19, 0.51, 0.62
124 processes: 110 sleeping, 14 running

Cpu states:

      CPU LOAD USER NICE SYS IDLE BLOCK SWAIT INTR SSYS
      0  0.37 0.03 0.23 0.01 99.5% 0.0% 0.0% 0.0% 0.0%
      1  0.02 0.0% 0.0% 0.0% 99.9% 0.0% 0.0% 0.0% 0.0%
      avg 0.19 0.0% 0.2% 0.4% 99.4% 0.0% 0.0% 0.0% 0.0%

Memory: 93636K (57E16K) real, 322124K (239363K) virtual, 746264K free PageS 1/4
```
