
- `-A` Set alert mode: fast, full, console, or none (alert file alerts only)

`"unsock"` enables UNIX socket logging (experimental).

...

## 11.4.2 配置 Snort

Snort 的源代码包含一个示例配置文件。如果你是从发行版的软件包安装的，那么它也应该包含一个示例 Snort 配置文件。通常这个文件名为 `snort.conf`。在大多数流行发行版中，包括 SUSE 和 Debian，该文件（以及许多 Snort 规则）被放置在 `/etc/snort` 中。

如果你正在使用源代码安装，示例 `snort.conf` 配置文件位于 `<snort-source>/etc/` 中，示例规则位于 `<snort-source>/rules/` 中。对于使用源代码版本的人，我建议创建 `/etc/` 或 `/usr/local/etc/` 下的一个名为 `snort` 的目录，并将 `snort.conf` 配置文件和 Snort 规则放在该目录中。此外，默认的 Snort 配置文件还会调用各种映射和额外配置文件。这些文件也可以在 `<snort-source>/etc/` 目录中找到。创建目录并将所有文件复制进去看起来像这样（再次说明，这只适用于从源码编译 Snort 的人）：

```
mkdir /etc/snort

cp <snort-source>/etc/snort.conf /etc/snort/

cp <snort-source>/etc/*.map /etc/snort/

cp <snort-source>/etc/*.config /etc/snort/

cp <snort-source>/rules/* /etc/snort/
```

对 `snort.conf` 配置文件进行另一个重要更改。在你将其复制到 `/etc/snort` 目录后，编辑该文件并将 `RULE_PATH` 变量从其默认值 `../rules` 更改为 `/etc/snort`。完成后，该行应看起来像这样：

```
var RULE_PATH /etc/snort
```

最后，使用以下命令创建 Snort 日志目录：

```
mkdir /var/log/snort
```

所有基础工作完成后，是时候正式启动 Snort 了。如果你是从发行版的软件包安装的，很可能你可以通过正常的运行控制机制（例如 `/etc/init.d/snort start`）来启动 Snort。如果你是从源码编译的，你需要手动启动 Snort 并指向其配置文件的位置：

```
/usr/local/bin/snort -c /etc/snort/snort.conf
```

如果你收到任何错误，很有可能缺少文件。根据配置文件，检查 Snort 源目录结构中的缺失文件并将其复制到适当的位置。

如果一切顺利，你应该会在输出的末尾看到类似以下的消息：

```
=== Initialization Complete ===
```

如图所示，shell 提示符未返回。这是因为未告知 Snort 分叉到守护进程模式。按 `Ctrl+C` 终止 Snort 并在命令行中添加 `-D`。现在它应该看起来像这样：

```
/usr/local/bin/snort -c /etc/snort/snort.conf -D
```

Snort 将再次启动，这次它会分叉到后台，返回 shell 提示符。

当然，Snort 配置远不止于使用默认选项和规则集让其运行。有关特定 Snort 配置的更多信息，请参阅 Snort 文档。

### 11.4.3 测试 Snort

既然 Snort 现在在后台运行，你可能会假设它运行得非常完美，并且日志条目会被放入 `/var/log/snort` 供你使用。然而，我并不是一个喜欢假设的人，尤其是在计算机安全方面。因此，为了测试 Snort 安装，我将使用便捷的 `hping2` 工具来构造一个或两个数据包并将其发送到运行 Snort 的主机。

在这种情况下，我只是在验证 Snort 是否正在运行并监控某些内容。默认规则查找恶意数据包，因此使用 `hping2` 构造一个这样的数据包应该很简单。从网络上的另一台主机（`192.168.1.10`），我向运行 Snort 的主机（`192.168.1.2`）运行了以下 `hping2` 命令：

```
hping2 -X 192.168.1.2
```

`-X` 选项导致执行 Xmas 扫描。查看运行 Snort 的主机上的 `/var/log/snort` 发现告警文件收到了一些信息，并且还有一个名为 `192.168.1.10` 的新目录，这是测试数据包的来源。该目录内包含对应于我发送的数据包的文件，其内容如下所示：

```
[**] BAD-TRAFFIC tcp port 0 traffic [**]

06/07-16:19:00.712543 192.168.1.10:1984 -> 192.168.1.2:0

TCP TTL:64 TOS:0x0 ID:48557 Iplen:20 DgmLen:40

*2***** Seq: 0xED1609B Ack: 0x13E89C5 Win: 0x200 TcpLen: 20

=================================================================

[**] BAD-TRAFFIC tcp port 0 traffic [**]

06/07-16:19:00.712610 192.168.1.2:0 -> 192.168.1.10:1984

TCP TTL:64 TOS:0x0 ID:10034 Iplen:20 DgmLen:40 DF

***A*R** Seq: 0x0 Ack: 0xED1609B Win: 0x0 TcpLen: 20

=================================================================
```

从输出中可以看到，Snort 捕获了它认为（确实如此）的恶意 TCP 数据包。告警日志文件 `/var/log/snort/alert` 还包含对于排序告警特别有用的信息。以下是告警日志文件中与前面显示的特定主机文件条目对应的日志条目：

```
[**] [1:524:8] BAD-TRAFFIC tcp port 0 traffic [**]

[Classification: Misc activity] [Priority: 3]

06/07-16:19:00.712543 192.168.1.10:1984 -> 192.168.1.2:0

TCP TTL:64 TOS:0x0 ID:48557 Iplen:20 DgmLen:40

*2***** Seq: 0xED1609B Ack: 0x13E89C5 Win: 0x200 TcpLen: 20

[**] [1:524:8] BAD-TRAFFIC tcp port 0 traffic [**]

[Classification: Misc activity] [Priority: 3]

06/07-16:19:00.712610 192.168.1.2:0 -> 192.168.1.10:1984

TCP TTL:64 TOS:0x0 ID:10034 Iplen:20 DgmLen:40 DF

***A*R** Seq: 0x0 Ack: 0xED1609B Win: 0x0 TcpLen: 20
```

从这些条目中可以看到，有一些额外的项目，如 `Classification`（分类）和 `Priority`（优先级），可以帮助对告警进行分类和优先排序。分类和优先级都可以在告警日志文件中配置。

### 11.4.4 接收告警

我建议先与 Snort 合作，积累关于规则和配置选项的经验，然后再配置它通过电子邮件或其他方式发送告警。根据网络布局，使用默认 Snort 规则可能会导致你被告警淹没。

回忆一下第 10 章中介绍的日志文件监控软件，并给出了使用 Swatch 监控日志文件中特定事件的配方，此时它会基于告警发送电子邮件。如果你明白我的意思，恭喜你！

#### 使用 SWATCH 监控 SNORT 告警

使用默认配置，Snort 将日志记录到 `/var/log/snort/alert`。因此，创建一个 Swatch 配置来监控此文件非常容易。同样，使用 Swatch 的告警和电子邮件很容易让你或系统不堪重负，因此在你有机会进一步配置 Snort 之前，在基于 Snort 告警配置任何操作时应该谨慎。

回忆一下，Snort 在 `/var/log/snort/alert` 中记录一些优先级数据。因此，你可以设置一条 Swatch 规则来监视具有特定优先级（例如 3）的任何内容，并在看到该优先级时发送电子邮件。这将放置在你的 Swatch 配置文件中，默认情况下是 `~/.swatchrc`。这是配置条目：

```
watchfor /Priority: 3/

mail
```

启动 Swatch 并将其指向 Snort 告警文件 `/var/log/snort/alert` 看起来像这样：

```
swatch --tail-file=/var/log/snort/alert
```
