
![](img/84d12236ddfe17cc29fd21173b9904ac_442_0.png)

# SUSE Linux Enterprise Server 10 管理

“下一步”将您带到对话框，您可以在其中为打印队列命名，并添加打印机及其位置的信息。

图 10-16

![](img/84d12236ddfe17cc29fd21173b9904ac_443_0.png)

再次点击“下一步”将您带回图 10-6 和图 10-4 中已过的对话框，您将返回打印机配置对话框（图 10-2）。

如果您想编辑打印机配置，请在打印机配置对话框中选择它并点击“编辑”。如果您想删除打印队列，请选择它并点击“删除”。

# CNI 专用 - 允许打印

严禁复制本手册的全部或部分或分发此类副本。如怀疑有复制行为，请拨打 1-800-PIRATES。

10-18

版本 1

# 从命令行添加打印机

除了 YaST 之外，您还可以使用命令行工具配置 CUPS。在收集所需信息（如 PPD（Postscript打印机描述）文件和设备名称）后，输入以下内容：

```
lpadmin -p <queue> -v <device-URI> -P <PPD-file>-E
```

选项 `-p` 指定打印机的队列名称，选项 `-v` 设置打印队列的设备 URI 属性（见第 10-8 页的“网络打印机”），选项 `-P` 用于指定 PPD 文件。

不要将 `-E` 作为第一个选项。对于所有 CUPS 命令，将 `-E` 作为第一个参数意味着使用加密连接，而在结尾使用 `-E` 则允许打印机接受打印作业。

例如，要启用并行打印机，输入类似下面的命令：

```
lpadmin -p ps -v parallel:/dev/lp0 -P /usr/share/cups/model/Postscript.ppd.gz -E
```

要启用网络打印机，输入类似下面的命令：

```
lpadmin -p ps -v socket://10.0.0.200:9100/-P /usr/share/cups/model/Postscript-level1.ppd.gz -E
```

# 练习 10-1

# 修改您的打印机配置

在此练习中，您将添加一个本地打印机并打印到远程队列。

您可以在练习册中找到此练习。

（练习结束）

## 目标 2

# 管理打印作业和队列

CUPS 带有几个命令行工具，用于启动、停止和修改打印队列。CUPS 打印系统的命令行工具及其 man页包含在 `cups-client` 软件包中。

这些工具的文档随 `cups` 软件包安装在 `/usr/doc/packages/cups/`：

- CUPS 软件用户手册：`sum.html` 和 `sum.pdf`

- CUPS 软件管理手册：`sam.html` 和 `sam.pdf`

CUPS 工具允许根据两种不同的样式或约定使用命令，这些样式被称为：

- Berkeley 风格（Berkeley 风格命令与用于 LPRng 打印系统使用的命令相同）

- System V 风格

与 Berkeley 风格相比，System V 为打印机管理提供了更广泛的功能。要管理打印队列，您需要知道如何执行以下操作：

- 生成打印作业

- 显示打印作业信息

- 取消打印作业

- 管理队列

- 配置队列

- 启动和停止 CUPS

打印队列也可以通过 Web 界面管理，这将在本节稍后介绍。

## 生成打印作业

使用以下命令生成打印作业：

- Berkeley: `lpr -P queue file`

- System V: `lp -d queue`

示例：

```
user@host # lpr -P color chart.ps
```

或者：

```
user@host # lp -d color chart.ps
```

使用这些命令，文件 `chart.ps` 将被提交到 `color` 队列。如果没有指定队列，作业将打印到默认队列。每当指定了额外的打印选项时，都需要使用 `-o` 参数：

```
user@host # lpr -P lp -o duplex=none order.ps
```

或者：

```
user@host # lp -o duplex=none order.ps
```

这这会将文件 `order.ps` 提交到 `lp` 队列，并禁用相应设备的双面打印（`duplex=none`）。要查看可能的选项，请输入 `lpoptions -l`（见第 10-26 页的“配置队列”）。命令必须以略有不同的形式给出，以便通过远程队列打印：

- Berkeley: `lpr -P queue file`

- System V: `lp -d queue`

示例：

```
user@host # lpr -P queue file
```

或者：

```
user@host # lp -d queue-file
```

使用这些命令将文件 `motd` 提交到 `lp` 队列，以便在 `server` 处打印。

关于这些命令行工具的更多信息，请输入 `man lpr` 和 `man lp`。

## 显示打印作业信息

使用以下命令显示打印作业信息：

- Berkeley: `lpq -P queue`

- System V: `lpstat -o queue`

`lpq` 命令显示默认队列的作业如下：

```
user@host # lpq ready and printing
Rank      Owner  Job  File(s)
active    14    fstab  
```

`lpq -l` 以略有不同的格式显示信息。

要显示另一个队列的打印机，输入选项 `-P queue`：

```
user@host # lpq ready
no entries
```

要显示所有可用队列的活动作业，输入 `lpq -a`：

```
user@host # lpq -a no entries
```

要以固定间隔更新输出，输入 `lpq -P queue +seconds`。

以下显示了 `lpstat -o queue` 的输出；`lpstat -a` 显示接收状态：

```
user@host # lpstat -o draft
draft-14 root Thu 30 15:08:54 2006
enabled since Jan 01 00:00
Connected to host, sending print job...
user@host # lpstat -a
draft accepting requests since Jan 01 00:00
printer accepting requests since Jan 01 00:00
```

![](img/84d12236ddfe17cc29fd21173b9904ac_449_0.png)

关于这些命令的更多信息，请输入 `man lpq 10`。

## 取消打印作业

使用以下命令取消打印作业：

- Berkeley: `lprm -P queue jobnumber`

- System V: `cancel [-h server] queue-jobnumber`

关于这些命令的更多信息，请输入 `man lprm` 和 `man cancel`。

## 管理队列

除了控制队列中的单个作业外，您还可以控制队列本身。

- 禁用打印但仍向其发送作业，请输入 `/usr/bin/disable printer`

禁用的队列仍然接收打印作业，但在重新启用之前不会实际打印任何文件。如果打印机故障且您需要时间修复，禁用打印队列是有用的。

- 对禁用的队列重新打印，请输入 `/usr/bin/enable printer`

如果有队列打印作业，它们将在启用打印机后进行打印。

- 您需要带路径命令，因为 `enable` 也是 bash 的内置命令。

- 通过输入 `/usr/sbin/reject printer` 停止接受作业

使用 `/usr/sbin/reject` 命令，打印机将完成队列中的打印作业，但拒绝任何新的打印作业。此命令在您需要对打印机进行维护且打印机在内不可用时非常有用。

注意：`lpstat -a` 显示队列的接收状态信息。

使用此命令，你可以重置打印队列以开始接受新的打印作业。（注意：如果队列也被禁用，则只有在重新启用队列后才会开始实际打印。）

## 配置队列

影响输出物理特性的打印机特定选项存储在目录 `/etc/cups/ppd/` 下每个队列的 PPD 文件中。

PPD（PostScript 打印机描述）是描述 PostScript 打印机属性（如分辨率）和选项（如双面打印单元）的计算机语言。这些描述对于在 CUPS 中使用各种打印选项是必要的。

在安装 SUSE Linux Enterprise Server 期间，系统会预装 PPD 文件。通过这种方式，即使是不内置 PostScript 的打印机也可以使用。
