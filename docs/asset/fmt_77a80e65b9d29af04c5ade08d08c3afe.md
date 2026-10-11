
既然我们已经为虚拟分区创建了可启动的恢复归档，我们就可以使用它来恢复我们的 vPar。您可以使用 `vparboot` 命令从一个 vPar 恢复另一个 vPar。这意味着，当其中一个 vPar 正在运行时，您可以使用以下 `vparboot` 命令在同一系统上恢复另一个 vPar：

![](img/eff8b9287a5f38c5adf538f24aacf29e_577_1.png)

```
vparboot -p vp_name -I ignite_kernel
```

这与在第 2 章中我们使用位于同一系统上的内核（而非 Ignite-UX 服务器上的内核）启动 vPar 时使用的 `vparboot` 形式不同。那种形式的 `vparboot` 如下所示：

```
vparboot -p vpar_name [ -b kernel_path ] [ -o boot_opts [ -f boot_addr] ]
```

在前面的章节示例中，我们只需指定我们要启动的虚拟分区的名称，例如 `vparboot -p cable1`。使用这种形式的 `vparboot`，我们通过 `-b` 选项指定本地系统上的启动内核。`vparboot` 和其他 vPar 命令的手页可以在附录 A 中找到。

通常，您会从 PDC 提示符启动恢复归档，也就是说，您的系统已停止并且您正在恢复它。由于我们的系统上有多个 vPar，我们可以使用 `vparboot` 从同一系统上正在运行的 vPar 恢复该系统上的另一个 vPar。

我们将在正在运行的 vPar 中发出以下 `vparboot` 命令，以通过命令行从 Ignite-UX 服务器恢复 vPar `actappd1`：

```
# vparboot -p actappd1 -I 161.228.212.110,/opt/ignite/boot/WINSTALL
```

指定了我们的 Ignite-UX 服务器的 IP 地址。在此 `vparboot` 命令中使用的 `WINSTALL` 文件与用于常规 HP-UX 恢复（没有 vPars）的文件不同。vPars 需要可重定位内核，因此 `vparboot` 命令中使用的 `WINSTALL` 是 vPars 所需的那个。该 `WINSTALL` 随 vPars 提供。

使用 `vparboot` 从正在运行的 vPar 恢复虚拟分区的能力意味着受影响的更少。正在运行的 vPar 中的用户不会受到正在另一个 vPar 上进行的恢复的影响。在根卷组（`vg00`）的恢复完成后，您可以从最新的备份恢复 vPar 上的其余信息。请确保经常创建可启动的恢复归档，以便您的整个根卷组可以使用最新的数据进行恢复。

![](img/eff8b9287a5f38c5adf538f24aacf29e_578_0.png)

## 使用 Ignite-UX 安装虚拟分区

本节包含设置 Ignite-UX 服务器以安装 vPars 的分步程序。该程序由 HP 实验室工程师 Geoff Blaha 提供。由于您将在 vPars 环境中安装许多 HP-UX 11i 和 vPars 软件实例，该程序可以为您节省大量时间。

在前面的章节示例中，我们只需指定我们要启动的虚拟分区的名称，例如 `vparboot -p cable1`。使用这种形式的 `vparboot`，我们通过 `-b` 选项指定本地系统上的启动内核。`vparboot` 和其他 vPar 命令的手页可以在附录 A 中找到。

### Ignite-UX 和 vPars 实用指南

![](img/eff8b9287a5f38c5adf538f24aacf29e_579_0.png)

使用 `vparboot` 命令从虚拟分区安装 HP-UX 和 vPar 软件到目标 vPar。Ignite-UX 服务器用作此安装过程的源仓库。

以下是整体的 vPars 安装过程（假设正在安装新服务器）

- 安装服务器和外围设备
- 安装 vPars 所需的补丁（即，Gold Quality Pack 等）
- 安装 HP-UX 11i（独立安装）
- 安装 vPars 软件。
- 规划所需的 vPars。

![](img/eff8b9287a5f38c5adf538f24aacf29e_579_1.png)

- 使用 `vparcreate` 命令创建 vPars：这将创建 vPars 数据库 `/stand/vpdb`。
- 关闭 HP-UX 并将服务器置于 BCH（Boot Console Handler）模式。
- 从 HP-UX/vPars 磁盘启动，并在 ISL 提示符处停止（交互）。
- 加载并运行 vPars 监视器。
- 使用 `vparload` 命令启动第一个 vPar（之前安装的）。
- 使用 `vparboot` 命令安装 HP-UX 和 vPars 软件到所有剩余的 vPars。使用 `Ctrl/A` 命令切换虚拟控制台在 vPars 和监控器之间。

Ignite-UX 服务器用作 `vparboot` 安装过程的源库。如果尚未存在用于此过程的 Ignite-UX 服务器，请安装并配置一台，最好是在另一台系统上，从以下步骤 1 到 3 开始。如果已经存在 Ignite-UX 服务器，或者其版本早于 B.3.4.115，则需要更新。如果你的 Ignite-UX 服务器已经是 B.3.4.115 版本，请继续执行下面的步骤 4。

## 1) 获取 Ignite-UX 软件

来源包括 CDROM、 `software.hp.com` 和 SD-UX 库文件。

注意：vPars 首个发行版支持的 Ignite-UX 版本为 `B.3.4.115`：

```
= what /opt/ignite/bin/ignite
/opt/ignite/bin/ignite:
ignite user interface $Revision: 10.643 $
Ignite-UX Revision B.3.4.115
install/h $Revision: 10.102 $
```

可以在 2001 年 9 月的应用程序分发中找到此版本。虽然旧版本的 Ignite-UX 可能可以工作，但它们不被支持用于 vPars，并且在使用基于 Ignite-UX B.3.4.115 版本库构建的可重定位 `WINSTALL` 文件时可能会遇到问题。

## 2) 安装或更新 Ignite-UX 软件

使用 `swinstall` 安装 Ignite-UX。

## 3) 更新 `PATH`

将以下搜索路径添加到你的登录脚本中：

```bash
export PATH=${PATH}:/opt/ignite/bin
```

如果已经存在 Ignite-UX 服务器（版本 B.3.4.115），请将 HP-UX 11i 服务器 OE 和 vPars 软件添加到 Ignite-UX 服务器中（注意，在 Ignite-UX 服务器上安装和配置软件有多种方法；下面描述的是其中一种方法）：

## 4) 在 Ignite-UX 中设置要安装到目标 vPars 的软件

- 从 2001 年 9 月的介质创建 HP-UX 11i OE 库（使用 CDROM 设备 `c0t3d0` 的示例）：

```
make_depots -r B.11.11 -s /dev/dsk/c0t3d0
```

- 创建 vPars 应用程序库，以便它在安装期间的 `tool` 的 `Software` 选项卡中显示（使用 tar 格式的库文件，以及另一个使用 Ignite-UX 服务器的示例）：

```
make_depots -r B.11.11 -a 800 -s /tmp/vpar_iC9.tar
```

或者

```
make_depots -r B.11.11 -a 800 -s flatecat.cup.hp.com:/opt/VPAR/ic9/depot
```

> 注意：上述假设 vPars 源作为 tar（库）文件或另一个 Ignite-UX 库位于 `flatcat` 计算机上。CDROM 源也可以工作。上述示例命令将在 `"apps_800"` 库 中创建并复制 vPars。

- 为上述库（11i OEs 和 vPars）创建 Ignite-UX 配置文件：

```
make_config -r B.11.11
```

上述命令创建 `/var/opt/ignite/data/Rel_B.11.11/apps_800.cfg` 配置文件。

- 管理应用程序的 Ignite-UX 索引文件：

```
# manage_index -a -f /var/opt/ignite/data/Rel_B.11.11/apps_800_cfg
```

- 从 2001 年 9 月的介质创建 HP-UX 11i OE 库：

完成上述步骤后，将用于 vPars 的可重定位 `WINSTALL` 文件复制到 Ignite-UX 引导目录：
