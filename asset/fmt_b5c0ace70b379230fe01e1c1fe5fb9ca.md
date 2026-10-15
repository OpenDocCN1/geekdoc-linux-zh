
你还可以通过指定文件作为参数使用单个 `lp` 命令指定多个打印机进行打印。在这种情况下，创建了一个打印任务来打印所有文件。将 `/etc/hosts` 和 `/etc/issue` 到打印机 `printer1`，你可以执行以下命令：

```bash
[root@server1] -lp -d printer1 /etc/hosts /etc/issue
request id is printer1-2 (2 file(s))
[root@server1]#
```

## 打印机管理

| Option | Description |
|---|---|
| `-d` | 指定打印机名称 |
| `-i` | 指定打印机 ID |
| `-n` | 指定份数 |
| `-q` | 显示队列中的任务 |
| `-r` | 指定操作原因 |
| `-p` | 显示打印机列表 |
| `-t` | 显示打印机的所有信息 |

发送到打印机 `printer1` 的任何打印任务都会被发送到打印队列，但在打印机启动之前将一直留在队列中。

`Spooling` `Printing`

**图 10-1** 打印过程

来源：Course Technology/Cengage Learning

图 10-1 展示了打印机 `printer1` 的此过程示例。

要查看系统上的打印机列表及其状态，可以使用 `lpstat` 命令的 `-t`（total）选项，输出如下：

```bash
root@server1]# # lpstat -t
scheduler is running
system default destination: printer1
device for printer1: parallel:/dev/lp0
printer1 accepting requests since Thu 26 Aug 2010 08:34:30 AM EDT
printer1 is enabled since Thu 26 Aug 2010 08:42:23 AM EDT
root@server1]# #
```

上述输出表明系统上只有一个打印机 `printer1`，它连接到计算机的第一个并行端口（`parallel:/dev/lp0`）。输出还告诉您打印队列中没有任务。此外，`cups` 守护进程（调度程序）正在运行，并接受从打印队列到打印机的任务，因为它是启用的。

你可以通过打印机名称使用 `cupsaccept`、`cupsreject`、`cupsenable` 或 `cupsdisable` 命令操作打印机状态。因此，要启用打印机 `printer1` 的打印和打印可以使用以下命令：

```bash
root@server1]# # cupsaccept printer1
root@server1]# # cupsdisable printer1
root@server1]# # lpstat -t
scheduler is running
system default destination: printer1
device for printer1: parallel:/dev/lp0
printer1 accepting requests since Thu 26 Aug 2010 08:51:21 AM EDT
printer1 disabled since Thu 26 Aug 2010 08:51:21 AM EDT -
Paused
root@server1]# #
```

### LPD 打印系统

虽然 `CUPS` 是 Linux 计算机的首选打印系统，但许多旧的 Linux 计算机使用传统的行打印守护进程（`LPD`）打印系统。在该系统中，`lpr` 命令用于将文档打印到打印队列，类似于 `lp` 命令；`lpc` 命令用于查看打印机状态；`lpq` 命令用于查看打印队列中的打印任务，类似于 `lpstat` 命令；而 `lprm` 命令可用于移除打印任务，类似于 `cancel` 命令。

对于那些习惯使用 `LPD` 打印系统的用户，`CUPS` 提供了 `lpr`、`lpc`、`lpq` 和 `lprm` 命令的版本。以下输出显示了系统上所有打印机的状态，将 `/etc/inittab` 打印两份到 `printer1`，查看队列中的打印任务并移除该打印任务：

```bash
[root@server1 ~]# lpr status
printer1:
printing enabled
queuing enabled
```

无项目

守护进程存在

```
[root@server1]# lpr -#2 -P printer1 /etc/inittab
[root@server1]# lpq
```

| 排序 | 任务 | 总大小 |
| --- | --- | --- |
| `lst root 1` | `inittab` | `2048 bytes` |

```
[root@server1]# lpm 1
[root@server1]# lpq
printer1 is ready
无项目
[root@server1]# _
```

## 配置打印机

回想打印的核心组件是 `cups` 守护进程 (`cupsd`)，它接受打印任务并将其队列，然后将其发送到打印机。包含 `cups` 设置的文件是 `/etc/cups/cupsd.conf`，而包含系统上安装的每台打印机信息的文件是 `/etc/cups/printers.conf`。你不需要手动编辑这些文件，而是可以使用打印机配置工具，如图 10-2 所示。要访问此工具，你可以在桌面环境的终端中输入 `system-config-printer`，或者在 `GNOME` 桌面环境中导航到“系统”菜单、“管理”下的“打印”。

图 10-2 所示的打印机配置工具显示系统上没有配置打印机。要添加打印机，你可以点击“添加”按钮并指定打印机设备，如图 10-3 所示。

> 当你尝试执行任何需要特殊权限的操作（例如访问设备文件或打印机配置）时，打印机配置工具都会提示你提供 `root` 用户密码。

![](img/bafa5678973f896b93838a140b8f7840_460_0.png)

| 打印：`localhost` |
| 服务器 打印机组视图 帮助 |
| 添加过滤器：`Q` |
| 已连接到 `localhost` |

**图 10-2** 打印机配置工具

## 第 10 章 常见管理任务

![](img/bafa5678973f896b93838a140b8f7840_461_0.png)

图 10-3 指定打印机设备

来源：Course Technology/Cengage Learning

大多数打印机都即插即用 (`PnP`)，并且在插入系统时会自动配置一个默认名称。因此，你不需要在打印机配置工具中添加这些打印机。相反，如果需要，你可以使用打印机配置来修改它们的设置。

如图 10-3 所示，你可以选择打印到使用惠普 `JetDirect` 技术连接到网络的打印机，或者打印到通过互联网打印协议 (`IPP`)、行打印机守护进程 (`LPD`) 或 `Windows` (`SAMBA`) 打印服务跨网络位于远程计算机上的打印机。如果你想打印到不支持 `PnP` 的本地打印机，你必须在图 10-3 中选择“其他”并指定统一资源标识符 (`URI`)。`URI` 标识设备的类型和路径；在图 10-3 中，`URI` `parallel:/dev/lp0` 指定打印机端口设备文件 `/dev/lp0`。

点击图 10-3 中的“下一步”后，系统将查询你选择的设备以确定打印机型号，以便 `CUPS` 找到合适的驱动程序。如果无法确定打印机型号，系统会提示你手动选择打印机的制造商和型号，如图 10-4 和 10-5 所示。

无论你的打印机驱动程序是自动选择还是手动选择的，你都会看到图 10-6 中的屏幕，你可以在为打印机选择一个名称，该名称可以在程序和命令中标识它。此外，你还可以可选地指定描述和位置，当搜索打印机或显示其属性时，这些内容将出现在打印机名称旁边。做出选择后，点击“应用”。从现在起，系统会提示你可以选择打印测试页。接下来，你的打印机被添加到系统中并准备好使用，如图 10-7 所示。

### 选择驱动程序

- 从数据库中选择打印机
- 提供 `PPD` 文件
- 搜索下载打印机驱动程序

格式打印机数据库包含各种制造商提供的 `PostScript` 打印机描述 `PPD` 文件，还可以为大量（非 `PostScript`）打印机生成 `PPD` 文件。但总的来说，制造商提供的 `PPD` 文件可以更方便地访问打印机的特定功能。

制造商

![](img/bafa5678973f896b93838a140b8f7840_462_0.png)

**图 10-4** 选择打印机制造商

*来源：Course Technology/Cengage Learning*

### 选择驱动程序

| 型号 | 驱动程序 |
| --- | --- |
| `ColorStyler 4500` | `ImageWriter II Fomatic/iwi [en] (rec` |
| `ColorStyler 6500` | |
| `Dot Matrix` | |
| `ImageWriter II` | |
| `ImageWriter LQ` | |
| `LaserWriter 4/600` | |
