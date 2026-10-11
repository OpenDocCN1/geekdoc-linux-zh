
```
# cat /tmp/cable2
vparcreate -p cable2 -B manual -b /stand/vmunix -a cpu::1
-a cpu::1:3 -a mem::1024 -a io:0/8
-a io:0/8/0/0.8.0.5.0.0.0:boot -a io:0/10
#
```

执行此文件后，我们可以通过运行 `vparstatus` 来确定第二个 vPar 是否已创建以及它由哪些组件组成：

```
# vparstatus -v

[Virtual Partition Details]
Name:    cable1
State:   Up
Attributes: Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33
Unbound [Path]:

[IO Details]
 0.0
  0.0.1.1.2.0 BOOT

[Memory Details]
Specified [Base /Range]:
           (bytes) (MB)
Total Memory (MB): 1024

[Virtual Partition Details]
Name:    cable2
State:   Down
Attributes: Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 37
Unbound [Path]:

[IO Details]
0.8
0.8.0.0.8.0.5.0.0.0.0, BOOT
0.10

[Memory Details]
Specified [Base /Range]:
(bytes) (MB)
Total Memory (MB): 1024
#
```

此输出显示第一个 vPar 保持完整，且第二个 vPar 已成功创建，包含我们指定的名称、内核文件、CPU、I/O 和内存组件。请注意，每个 vPar 都有一个分配给它的绑定 CPU。分配给 `cable2` 的 LAN 卡出现在输出中，是因为我们指定了 LBA `0/10` 作为 `cable2` 的组件之一。位于 `0/0/4/0` 的控制台和位于 `0/0/0/0` 的 LAN 接口是 `cable1` 的隐含组件，不会出现在 `vparstatus -v` 输出中。

创建好第二个 vPar 后，我们可以继续下一步并启动它。

![](img/eff8b9287a5f38c5adf538f24aacf29e_133_0.png)

### 9) 启动第二个虚拟分区

既然我们已经有一个名为 `cable1` 的第一个 vPar 在运行，并且已经创建了名为 `cable2` 的第二个 vPar，我们就可以从第一个 vPar 启动第二个 vPar。启动 vPars 有很多选项。由于第一个 vPar 已经在运行，我们将简单地使用 `vparboot` 从第一个 vPar 启动第二个 vPar，然后运行 `vparstatus -v`，如下例所示。如果我们输入后续的 `vparstatus` 命令，我们可以在下一个输出中看到 vPar `cable2` 的状态从 `Down` 变为 `Boot`，最后当 vPar 运行时变为 `Up`，如下所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_133_1.png)

## `vparboot -p cable2`

`vparboot`：正在引导 `cable2`。请稍候...

## `vparstatus`

`[虚拟分区]`

虚拟分区名称 状态 属性 内核路径 引导选项

`cable1` Up Dyn,Mani `/stand/vmunix`

`cable2` Load Dyn,Mani `/stand/vmunix`

`[虚拟分区资源摘要]`

CPU 轮换- 数量 内存 (MB)

| 虚拟分区名称 | CPU 最小/最大 | 绑定/ 未绑定 | I/O 设备 | # 范围/ 总计 MB | 总计 MB |
|---|---|---|---|---|---|
| `cable1` | 1/ 3 | 1 | 0 | 4 | 0/ 0 | 1024 |
| `cable2` | 1/ 3 | 1 | 0 | 4 | 0/ 0 | 1024 |

`cable2` 状态的这种演变反映了在此 vPar 所运行的第二个卷上引导操作系统所需的时间。

除了 `load`、`boot` 和 `up` 之外，你可能会发现虚拟分区处于其他状态。表 2-3 总结了撰写本文时虚拟分区的状态：

### 表 2-3 虚拟分区状态

| vPar 状态 | 描述 |
|---|---|
| load | 正在将虚拟分区内核映像加载到内存中。这是由虚拟分区监视器完成的。 |
| boot | 虚拟分区正在引导过程中。内核映像已由虚拟分区监视器成功加载。 |
| up | 虚拟分区已成功引导并正在运行。 |
| shut | 虚拟分区正在关闭过程中。 |
| down | 虚拟分区未运行且已停止。 |
| crash | 虚拟分区已发生恐慌并正在崩溃。 |
| hung | 虚拟分区无响应且已挂起。 |

当有多个 vPar 同时运行时，你可以使用内置的 vPar 驱动程序通过 `Ctrl-A` 在任意数量的虚拟分区之间切换控制台。图 2-5 展示了使用控制台查看主机名为 `cvhdcon3` 的 `cable1`。发出 `Ctrl-A` 连接到主机名为 `cvhdcon4` 的 vPar `cable2`。当你在控制台中发出 `Ctrl-A` 切换到下一个 vPar 时，系统会在方括号中提供你所连接的 vPar 的名称，例如 `[cable1]`。

![](img/eff8b9287a5f38c5adf538f24aacf29e_136_0.png)

**图 2-5 使用 Ctrl-A 在 vPar 之间切换时显示的控制台**

除了使用控制台在 vPar 之间切换外，还可以使用配置到特定 vPar 的 LAN 卡来打开 TELNET 或其他类型的会话到 vPar。这是你可以在网络上连接任何系统所使用过的同一种技术，而且它也是你始终希望在每个 vPar 中配置一个 LAN 卡的主要原因。

在本章中，我们没有涵盖在 vPar 中配置两个 LAN 卡的内容。为了在两个 vPar 中在网络操作中使用网卡，需要对两个 vPar 都完成 LAN 的配置。第 13 章涵盖了许多网络主题，包括 `/etc/hosts` 文件；`/etc/rc.configd/netconf` 文件，它必须在每个 vPar 上配置；以及许多其他内容。

### 10) 修改虚拟分区

你很可能会希望以多种方式修改你的虚拟分区。例如，你可能想要添加或移除一个 CPU。让我们来看看向虚拟分区添加 CPU 的一个示例。

在下面的示例中，有一个四处理器系统，其中包含我们刚才创建的两个虚拟分区：`cable1` 和 `cable2`。每个 vPar 都有一个绑定 CPU，这是在创建 vPars 时由 min 分配的。让我们运行 `vparstatus` 来查看这两个虚拟分区由哪些组件组成，并确认每个都有 1 个绑定 CPU：

```
# vparstatus -p cable1 -v

[Virtual Partition Details]
Name:                 cable1
State:                Up
Attributes:           Dynamic,Manual
Kernel Path:          /stand/vmunix
Boot Opts:
[CPU Details]
Min/Max:      1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33      < - one bound CPU @ 33
Unbound [Path]:

[IO Details]
0.0
0.0.1.1.2.0  BOOT

[Memory Details]
Specified [Base  /Range]:
        (Bytes)      (MB)
Total Memory (MB): 1024
#
```

```
# vparstatus -p cable2 -v

[Virtual Partition Details]
Name:                 cable2
State:                Up
Attributes:           Dynamic,Manual
Kernel Path:          /stand/vmunix
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_137_0.png)

## 创建虚拟分区的步骤
