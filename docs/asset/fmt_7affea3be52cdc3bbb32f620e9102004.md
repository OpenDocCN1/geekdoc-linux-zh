
```
Boot Opts:  
[CPU Details]  
Min/Max: 1/3  
Bound by User [Path]:  
Bound by Monitor [Path]: 37 <!-- one CPU in use at 37 -->  
Unbound [Path]:  
[IO Details]  
0.8.0.0.8.0.5.0.0.0 BOOT  
3.0.0.0.0  
[Memory Details]  
Specified [Base /Range]:  
(bytes) (MB)  
Total Memory (MB): 1024  
#
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_138_0.png)

这两个 `vparstatus` 命令的输出显示，`cable1` 有一个 绑定 CPU，`cable2` 也有一个 绑定 CPU。在这些 vPars 所创建的 L 类系统上，总共有四个 CPU。这意味着应该有两个 CPU 可用。让我们运行 `vparstatus -A` 来查看系统中的可用组件：

```
# vparstatus -A
[Unbound CPUs (path)]: 97 101
[Available CPUs]: 2

[Available I/O devices (path)]: 0.1 0.2 0.3 0.4 0.5 0.9 0.12 32 36 96 100
[Unbound memory (Base /Range)]: 0x0/64 0xC000000/1856 (bytes) (MB)
[Available memory (MB)]: 2048
#
```

此输出确认在硬件路径 97 和 101 处有两个 CPU 可用。我们可以通过多种方式添加这些 CPU。让我们使用 `vparmodify` 命令将 `cable1` 中的 `num` 个 CPU 更改为两个 CPU。我们通过使用 `-a` 在当前 CPU 数量的基础上 添加 一个来实现这一点。这是一个相对操作，即将在当前 CPU 数量的基础上添加一个 CPU。如果你希望指定 vPar 的绝对 CPU 数量而不是相对数量，可以使用 `vparmodify -m`。以下是该 `vparmodify` 命令的示例：

![](img/eff8b9287a5f38c5adf538f24aacf29e_139_0.png)

```
# vparmodify -p cable1 -a cpu::1
#
```

我们现在可以运行 `vparstatus -p cable1 -v` 来确认 CPU 已被添加，如下所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_139_1.png)

```
# vparstatus -p cable1 -v

[Virtual Partition Details]
Name:             cable1
State:            Up
Attributes:       Dynamic,Manual
Kernel Path:      /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:  1/3
Bound by User [Path]:       <-- original CPU @ 33
Bound by Monitor [Path]:  33
Unbound [Path]:   97       <-- unbound CPU @ 97

[IO Details]
    0.0
    0.0.1.1.2.0  BOOT

[Memory Details]
Specified [Base  /Range]:
                (bytes) (MB)
Total Memory (MB):  1024
#
```

`vparstatus` 的输出显示，位于硬件路径 97 的 CPU 确实已通过 `vparmodify` 命令作为 未绑定 CPU 添加到 `cable1` 中。

此外，我们可以运行 GlancePlus 或 `top` 来确认在 `cable2` 中有两个 CPU 正在使用。以下是在 `cable2` 上运行的 `top` 输出：
