
然而，如果没有额外的帮助，你的 CUPS 服务器可能不会让网络上的其他打印机知道它的存在。为了让你的 CUPS 服务器广播自己的存在，你需要在 `cupsd.conf` 中设置 `BrowseAddress` 参数。例如，为了向网络上尽可能多的主机发送数据包（基本上是路由器允许的范围），使用：

`BrowseAddress 255.255.255.255`

你可以将数字广播地址理解为 IP 地址的反向子网。例如，为了向 `10.1.2.0/255.255.255.0` 定义的子网发送数据，请尝试：

`BrowseAddress 10.1.2.255`

尽管如此，最佳可能是“本地”接口选择，它向除 PPP 链路以外的网络接口发送广播包：

`BrowseAddress @LOCAL`

如果你有一个具有多个太网接口的服务器，但不想在所有接口上进行广播，请使用 `@IF`。例如，向 `eth1` 广播的方法：

`BrowseAddress @IF(eth1)`

## 12.5.13 CUPS 故障排除

当你遇到 CUPS 问题时，一步步进行排查尤为重要。你可能会发现以下顺序有所帮助：

- 通过创建一个没有过滤器（原始模式）且设备为 `file:/dev/null` 的测试打印机，确保 CUPS 工作正常。使用 Web 界面和 `lp` 向打印机发送测试文件，并使用 `lpstat` 验证作业是否完成：

```
lpstat -w -o test_printer_name
lpstat -o test_printer_name
```

- 使用打印机的 PPD 文件激活你的过滤器。如果出现问题，请参考第 12.5.4 和 12.5.6 节。打印更多测试文件，确保作业已完成。

- 添加打印机的实际设备，然后尝试另一个测试作业。如有必要，尝试打印到文件，然后将文件直接发送打印机。

如果测试作业失败并挂起，打印机状态将变为“未就绪”（not ready），你需要启动打印机以重试作业或运行任何新作业。你可以通过打印机或 Web 界面执行此操作。但在开始更改之前，你应该查看日志文件，这些文件将在下一节中描述。

## 错误消息

打印后台程序和过滤器的复杂性，使得你密切关注日志消息至关重要。最重要的日志文件是 `/var/log/cups/error_log`（该名称略有误导性，因为文件也包含正常的诊断信息）。

查看日志可以发现如下内容：

```
[timestamp] Started filter /usr/lib/cups/filter/pstops (PID 3144) for job 26.
[timestamp] ProcessPPDRequest: 10 status code=0
[timestamp] Process[26] unable to open file - : Permission denied
```

行首的字母表示消息的严重程度或优先级。前一个示例中的三个字母如下：

- 信息日志消息。这些通知指示了某些重要事件，例如过滤器调用或作业提交。

- 详细调试消息。除非你遇到问题，否则你不应该关注这些信息。

- 错误消息，表示某些内容未正常工作。如果发生错误，CUPS 调度器通常仍会继续运行。但是，你可能会丢失某些功能或导致打印机挂起。

你可以通过 `cupsd.conf` 文件中的 `LogLevel` 参数更改日志级别。大多数安装中，默认级别为 `info`。如果你需要调试消息，必须使用 `debug`。如果你更改了 `logLevel` 参数，记得在更改后通过向 `cupsd` 发送 HUP 信号来重新加载配置文件。

## 过滤器问题

在打印过滤器阶段遇到问题后，你应该第一件事确保 `mime.convs` 中的 CUPS 过滤器运行正常。

要做到这一点，请禁用打印机 PPD 文件中可能任何过滤器，这样你就可以从可能出错列表中排除后端过滤器。只有在你使用非 PostScript 打印机时才会有此类过滤器。如果是你的情况，请编辑打印机的 PPD 文件（位于 `/etc/cups/ppd` 中的文件），寻找 `cupsFilter` 参数（见第 12.5.7 节）。在 `*: `之后直接添加一个 `%` 将其注释掉，例如：

```
*cupsFilter: "application/vnd.cups-postscript 0 fomatic-rip"
```

执行此操作（并通过发送 HUP 信号让 `cupsd` 重新读取配置）后，提交一个测试作业，查看数据是否能通过 `mime.convs` 过滤器阶段到达打印机设备。虽然你不可能在 `mime.convs` 中 CUPS 提供的过滤器程序遇到任何问题，但此过程可能会让你发现打印目录权限问题（在下一节中讨论），因为这类问题通常出现在初始打印阶段。

在解决了不涉及 `cupsFilter` 过滤器的故障后，重新启用此参数并寻找更多问题：

- 验证 `cupsFilter` 过滤器是否存在于 `lib/cups/filter` 目录中。

- 对于 `Foromatic` 过滤器，从命令行手动运行 `fomatic-rip -v` 以检查是否有有效输出（见第 12.5.8 节）。

- 检查过滤器是否包含任何新程序的路径。

- 如果你的过滤器依赖于 Ghostscript，通过运行 `gs -help` 确保你已安装所需的驱动程序。

## 打印目录权限错误

在你的错误日志中查找此类内容：

```
E [timestamp] Job n] unable to open print file - : Permission denied
```

CUPS 通常以伪用户 `lp` 和组 `sys` 运行其过滤器，因此该用户必须具有访问打印目录 `/var/spool/cups` 的权限以便访问中间数据。在修复权限时，检查这些问题：

- 检查 `/var/spool/cups` 的所有组件目录。`lp` 用户可以访问每一个目录吗？

- 确保你在 `/etc/passwd` 文件中有 `lp` 用户。

- 验证 `lp` 是否属于 `sys` 组。（记得可以通过 `cupsd.conf` 中的 `User` 和 `Group` 参数更改伪用户和组。）

## 设备问题

在通过过滤器测试后，你就可以准备向设备发送输出了。幸运的是，最后阶段出错的情况相对较少：

- `lp` 用户必须对直接连接到系统的任何打印机设备具有写入权限。

- 对于网络打印机，确保你可以访问设备。

## Ghostscript

如果你想知道 Ghostscript 如何工作，不带参数运行。如前所述，Ghostscript 包含这些功能：

- 位图渲染

- PDF 打印

- 文档预览

要感受 Ghostscript，请使用以下命令运行它：

```
gs file.ps
```

如提示所示，按 `RETURN` 退出。

有几个前端程序（如 `gv` 和 `ggv`）提供了更好的界面。无论你是否使用这些程序，运行 `-preview` 都可以验证你是否有一个有效的 PostScript 文件。

### 12.6.1 命令行选项

一些 `gs` 命令行（如 12.5.8 节中的）可能看起来复杂，特别是涉及到设备规范时。然而，熟悉它们以使用 Ghostscript 功能并不困难。

仔细查看以下命令，它将 `old.ps` 过滤为 `new.ps`：

```
gs -q -dOPAUSE -dBATCH -sDEVICE=pswrite -sOutputFile=new.ps old.ps
```

前四个选项通常用于无用户输入的文件。具体如下：

- `-q`: 静默模式；抑制任何正常的诊断输出。

- `-dOPAUSE`: 在每页后等待用户按 `RETURN`。

- `-dBATCH`: 在解释所有输入后终止。

- `-dSAFER`: 禁止文件分配能力（以避免安全问题）。`-dPARANOIDSAF` 禁止文件读取能力。

创建输出文件时，接下来两个选项通常配合使用：

- `-sDEVICE=driver_name`: 使用 `driver_name` 作为输出驱动器。在此背景下，“驱动器”一词通常指文件格式驱动器，而不是操作设备的代码，尽管也有例外（例如用于预览窗口的 x11 驱动）。要查看驱动列表，请运行 `gs -help`

某些驱动器需要其他命令行参数才能正确运行。两个著名的例子是 `unprint` 和 `lj` 驱动。`unprint` 驱动在 Ghostscript 库中带有许多 `.upp` 文件（包含额外参数）。要使用这些设置，使用 `@file.upp`，例如：

```
gs @file.upp -dOPAUSE -dBATCH -sOutputFile=out ...
```

- `-sOutputFile=file`: 将输出写入文件（使用 `-` 表示标准输出）。如果你想为 PostScript 输入的每一页创建一个文件，请在文件名中插入 `%d`。Ghostscript 会用页码替换 `%d`。

## 12.6.2 更多 Ghostscript 技巧

这里是你可以使用 Ghostscript 进行的一些其他实用操作：
