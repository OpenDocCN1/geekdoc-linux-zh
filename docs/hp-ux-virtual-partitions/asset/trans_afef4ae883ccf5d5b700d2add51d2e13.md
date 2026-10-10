
虽然这是一个展示如何修改虚拟分区（Virtual Partition）的简单示例，但它也展示了 vPars 的强劲能力。当系统上的两个 vPar 都在运行时，可以在不中断 vPar 中正在运行的程序的情况下，向其中一个或两个 vPar 添加处理器。

请注意，**vparmodify** 的 `-a` 选项会根据当前 CPU 数量*相对地*更改 CPU 数量。在我们的案例中，当前的 CPU 数量为 1，使用 `-a cpu:1` 会在当前数量 1 的基础上增加 1 个 CPU，结果变成 2 个 CPU。使用 **vparmodify** 的 `-d` 选项移除处理器时，也是如此。以下示例展示了运行 **vparstatus** 以查看这两个 CPU，使用 **vparmodify** 将 CPU 数量改回 1（这也是相对于当前 CPU 数量而言的，当前数量为 2），以及运行 **vparstatus** 以确认该更改已生效：

```
# vparstatus -p cabiel -v

[Virtual Partition Details]
Name:                  cabiel
State:                 Up
Attributes:            Dynamic,Manual
Kernel Path:           /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:               1/3
Bound by User [Path]:  33      <-- bound CPU @ 33
Bound by Monitor [Path]:
Unbound [Path]:        97      <-- unbound CPU @ 97

[IO Details]
  0-0
  0.0.0.0
  0.0.1.1.2.0 BOOT
  0.0.4.0  CONSOLE

[Memory Details]
Specified [Base /Range]:
             (bytes) (MB)
Total Memory (MB):  1024

# vparmodify -p cabiel -d cpu:1

# vparstatus -p cabiel -v

[Virtual Partition Details]
Name:                  cabiel
State:                 Up
Attributes:            Dynamic,Manual
Kernel Path:           /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:               1/3
Bound by User [Path] : 33 <-- original CPU @ 33
Bound by Monitor [Path] :
Unbound [Path] : <-- no unbound CPUs

[IO Details]
0.0
0.0.0.1.2.0 BOOT
0.0.4.0 CONSOLE

[Memory Details]
Specified [Base /Range] :
(bytes) (MB) :
Total Memory (MB) : 1024
#
```

我们可以利用可用的两个未绑定 CPU 对 vPars 进行许多其他修改，例如向其中一个 vPar 添加两个 CPU，或者向每个 vPar 各添加一个 CPU。

在使用 vparmodify 时，请记住组件的相对性质，并且截至本文撰写时，某些更改，如修改内存或添加 I/O 组件，需要 vPar 处于停机状态。第 5 章对此有详细说明。

![](img/eff8b9287a5f38c5adf538f24aacf29e_141_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_141_1.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_142_0.png)

## 虚拟分区转储文件

当虚拟分区崩溃时，会在 /stand/vpmon.dump 中创建一个转储文件。当虚拟分区启动时，文件会在 /var/adm/crash/vpar 中创建。这些文件带有数字扩展名，指示发生转储的次数。例如，vpmon.1、vpmon.dump.1 和 summary.1 指示保存在 /var/adm/crash/vpar 中的第一组文件。

以下清单展示了与转储相关的、您可能会在 /stand 和 /var/adm/crash/vpar 中看到的示例：

```
VPARNAME = extrans1

# ll /stand
total 100400
-rw-r-- 1 root sys 19 Jul 13 25:04 bootconf
drwxr-xr-x 4 root sys 2048 Oct 18 13:43 build
drwxrwxrwx 5 root sys 1024 Oct 18 13:06 dkkm
drwxrwxrwx 5 root root 1024 Oct 18 13:21 dkkm.vmunix.prev
-rw-r-r- 1 root sys 3388 Oct 18 13:16 iootlddfig
-r-r-r-r- 1 root sys 82 Jul 13 15:34 kernel
drwxr-xr-x 2 root sys 1024 Oct 18 13:18 krs
drwxr-xr-x    2 root     root       1024 Oct 18 13:16 krs.1kg
drwxr-xr-x    2 root     root       1024 Oct 18 13:18 krs.tmp
drwxr-xr-x    2 root     root       8192 Jul 13 13:04 test-founds
-rw-------    1 root     root        12 Oct 18 13:16 rootconf
-r--r--r--.   1 root     sys       2035 Oct 18 11:42 systemd
-r-x-r--r--.   1 root     sys        994 Jul 13 15:28 systemd.01
-r--r-x-x-x    1 root     sys       999 Jul 13 15:56 systemd.02
-r-x-r--r--.   1 root     sys       2354 Oct 18 13:28 systemd.base
-r-x-x-x-x-x   2 root     sys       1024 Jul 13 15:37 systemd.02
-r-x-x--x-x    1 root     sys        2035 Oct 18 10:58 systemd
-r-xwr-xr-x    1 root     root      226825568 Oct 18 13:16 vpars.prev
-rwxr-xr-x    1 root     root      226825568 Oct 18 11:04 vmunix
-rw-------    1 root     sys        8232 Oct 18 13:16 vpdx
-rw--------    1 root     root        8232 Jul 17 14:11 vPod.OLD
-T-x-------    1 bin     bin      5078504 Aug 31 18:59 vpson <--- vPar dump
--wx-------    1 root     root      5078504 Oct 10 10:43 vppon

# 11 /var/adm/crash/vpar                    <--- vPar dump directory
total 44644
-rw-r--r--.   1 root     root          2 Oct 10 10:43 count
-rw-f--r--.   1 root     root       16794 Jul 17 13:26 summary.0
-rw-f--r--.   1 root     root       15993 Jul 18 10:15 summary.1
-rw-f--r--.   1 root     root       19318 Jul 18 11:36 summary.2
-rw-f--r--.   1 root     root       10012 Oct 10 10:43 summary.3
-r-x-r-x-x-x    1 root     root      855928 Jul 17 13:26 vpars
-r-x-r-x-x-x    1 root     root      855928 Jul 18 10:15 vpars
-r-x-r-x-x-x    1 root     root      855928 Jul 18 11:36 vpars
-r-x-r-x-x-x    1 root     root       837614 Oct 10 10:43 vpar
-rw-------    1 root     root      5078504 Jul 17 13:26 vpar.tmp
-rw-------    1 root     root      5078504 Jul 18 10:15 vpar.tmp
-rw-------    1 root     root      5078504 Jul 18 11:36 vpar.tmp
-iw-------    1 root     root      5078504 Oct 10 10:43 vpar.tmp
```

**/var/adm/crash/vpar** 目录中包含四次 *(0-3)* 崩溃的 vPar 转储相关文件。

在 **stand** 中创建的转储文件被保存在 **/var/adm/crash/vpar** 中，并带有崩溃编号作为扩展名。每次崩溃时，**stand** 中的转储文件会被覆盖，但您在 **/var/adm/crash/vpar** 中拥有包含所有转储文件和相关信息的完整历史。请保留 **/stand/vpmon.dump** 文件不要移除。

![](img/eff8b9287a5f38c5adf538f24aacf29e_143_0.png)

## 摘要

在表 2-1 中总结的 **vparreset** 和 **vparremove** 命令在此示例中根本未被执行。**vparremove** 命令可以在任何处于*关机状态*的 vPar 上运行。启动并运行 vPars 以及执行某些修改的一般步骤已为您展示，旨在为您提供一个简单的操作框架。还有其他一些未涵盖的命令，附录 A 中也提供了它们的手册页。

![](img/eff8b9287a5f38c5adf538f24aacf29e_143_1.png)

关于特定领域的更多细节出现在本书的其他章节中，我建议您查阅附录 A 中所有 vPar 的在线手册页。

还有一些与服务器技术相关的考虑事项，我们没有涵盖。如果您在服务器上使用了 Instant Capacity on Demand (iCOD)，为了让 vPars 正常工作，必须激活所有 CPU。在 vPar 中使用处理器集（psets）时，请使用已绑定的 CPU。

# 第 3 章

# 启动与 vPars

# vpmon, vparload, vparboot, PDC, ISL, hpux, 安全 Web 控制台, GSP 配置

## 背景

我们在之前的章节中已经在系统上做了大量工作，以加载和配置 HP-UX 11i 和虚拟分区（vPars）。现在让我们退后一步，考察 HP 9000 启动的细节。在系统上加载 vPars 后，启动过程中有一些变化。让我们先讨论带有 vPars 的启动，然后在本章稍后部分考察一般性启动。首先，我们将讨论在系统上安装 vPars 之后的启动，以查看 vPars 对启动过程的影响。然后，在本章中非 vPars 特定的部分，您将得到以下内容的概述：HP 9000 的低级启动和配置；设置 HP 安全 Web 控制台；以及配置 Guardian 服务处理器（GSP）。

本章示例中使用的绝大多数系统，无论是 vPars 特定部分还是非 vPars 特定部分，都是 L 类系统。我特意使用了一个简单的系统，以便我们可以专注于启动过程，同时最大限度地减少与硬件相关的消息。由于启动过程因系统而异，即使在
