
这种设置是非常直观的。第一行指定从哪些端口转发流量，第二行指定应该将镜像到哪个端口。你需要参考你特定交换机硬件的用户指南，查看是否支持端口镜像，以及如果支持，如何配置它。

（注：由于提供的原文在后部分出现了部分重复和乱码，上述译文已根据逻辑对核心内容进行了整合与翻译。）

# 配置入侵检测系统 • 第 27 章

- 9. “第 1 步”部分的最后几行允许你为资源有限的系统配置检测引擎。除非你遇到了问题，否则可以保持此选项不变。

- 10. 之后，配置文件的“第 2 步”和“第 3 步”部分允许你启用或禁用特定功能并检测特定类型的攻击，例如碎片攻击、状态检查和流重组选项。深入研究这些每个选项的细节超出了本章的范围，对于许多人来说，默认设置已经足够用。

- 11. 标记为`Step #4`的章节包含 Snort 的输出选项。该部分有非常有价值的选项。取消注释 `output alert_syslog: host=hostname, LOG_AUTH_ALERT` 并输入你的 syslog 服务器的主机名。`LOG_ALERT` 是告的优先级。在我的示例中，我使用了命令：`output alert_syslog:host=192.168.1.99, log_local log_notice`，它将作为通知（notice）记录到本地设施。注意，Snort 并不支持所有设施和严重级别的组合。你还需要在命令行中包含 `-s` 关。我们将在下一章详细讨论 syslog。如果你没有用于记录的 syslog 服务器，只需记住该设置，等你的 syslog 服务器设置完成后回来。

- 12. 修改系统 #2 中动态加载库的路径。按如下方式修改：`C:\snort\lib\snort_dynamicpreprocessor` 和 `dynamicpreprocessor C:\snort\lib\snort_dynamicmicengine\sf_engine.dll`。注意，对于预处理器目录，你编辑的是绝对路径（无尾斜杠）。对于动态引擎（dynamicengine），你将路径从默认的 `libsf_engine.so` 修改为 Windows 使用的 `sf_engine.dll`。

- 13. 将 `classification.config` 改为绝对路径，例如 `include C:\classification.config`。对 `include reference.config.` 执行相同的操作。

- 14. 该章节允许你指定要检查哪些规则集。某些规则默认是禁用的，例如 `chat.rules`，它是通过各种即时消息客户端触发的。要启用或禁用规则集，只需在 `include` 行开头添加或删除 `#` 即可。此条目可以是相对路径（即 `include $RULE_PATH/local.rules`），因为 `RULE_PATH` 变量将被展开并形成绝对路径。

- 15. 对你的更改满意后，保存并关闭配置文件。

- 16. 基础安装不包含任何规则。访问 `www.snort.org` 并点击网页左侧的 RULES。在下一个页面，点击页面右侧的 DOWNLOAD RULES。向下滚动到 Sourcefire VRT Certified Rules – The Official Snort Ruleset (unregistered release) 并下载最新的规则集。它将是一个压缩文件，因此你需要一个程序来解压它；IZZip 或 FileZip 都是不错的选择。页面底部还有一组由社区提供的规则。如果你在寻找某些不常的内容，可能可以在那里找到，而无需自己创建规则。

- 17. 将压缩包中 `signatures` 文件夹下的所有文件提取到 `C:\snort\doc\signatures`，并将压缩包中 `rules` 文件夹下的所有文件提取到 `C:\snort\rules\`。这需要一些时间，因为目前有大约 3,700 条规则。

你现在已准备好启动 Snort 并查看它的运行情况。进入命令行提示窗口，并将工作目录更改为 `\snort\bin` 目录（`snort.exe` 所在地）。输入 `snort -W` 列出可用接口。在我的情况下，我得到的输出如图 4.6 所示。

# 图 4.6 Snort 接口列表

```
C:\Snort\bin>snort -W

--* Snort! |<*-

" ) -    Version 2.6.0-ODBC-MySQL-FlexRESP-WIN32 (Build 57)

    '''

    By Martin Roesch & The Snort Team: http://www.snort.org/team.html

    (C) Copyright 1998-2006 Sourcefire Inc., et al.
```

![](img/0eb7273a8d9e486628f6e18d37ab22c6_243_0.png)

![](img/0eb7273a8d9e486628f6e18d37ab22c6_243_1.png)

# 配置入侵检测系统 • 第 4 章

| 接口 | 设备描述 |
| :--- | :--- |
| 1 | `\Device\NPF_GenericDialupAdapter` (通用拨号适配器) |
| 2 | `\Device\NPF_{F95B71A4-C943-40BA-9F65-CD73D4B20769}` (Intel R) PRO/100B PCI 适配器 (TX) |
| 3 | `\Device\NPF_{A7F703C5-7567-49BC-B61-1A1F14614CAF}` (SIS NIS SISNIC) |

（注：接口 2 的行已折叠到本页。）

## 22

当我们启动 Snort 时，可以使用 `-i` 指定要监听的接口。如果不指定，它将使用第一个接口，在我的情况下它将看不到任何内容，因为那是一个未使用的拨号适配器。`-c` 选项告诉 Snort 使用哪个配置文件。配置多个配置文件是有用的，以便根据特殊情况快速切换配置。你可以为某些问题准备不同的配置文件，或者更深层次的日志。另一个重要的选项是 `-A`，它告诉 Snort 生成什么告警。选项有 `fast`、`full`、`console` 或 `none`。

以下命令将启动 Snort 监听接口 3，告警仅发送到控制台，使用 `C:\snort\etc\snort.conf` 配置文件。`-K` 关告诉 Snort 生成什么类型的日志。ASCII 日志对人类来说更容易阅读，但记录它们需要更多时间。如果速度不是问题，ASCII 日志可能是最易读和分析的。

```
snort -i 3 -c C:\snort\etc\snort.conf -A console -K ascii
```

# 配置入侵检测系统 • 第4章

```
=======================================================================

[**] 测试规则 [*]

08/10-20:25:52.282888 192.168.1.199 -> 192.168.1.107

ICMP TTL:128 TOS:0x ID:13274 IpLen:20 DLen:60

Type:8 Code:0 ID:512 Seq:29184 ECHO

61 62 63 64 65 66 67 68 69 6A 6B 6C 6D 6E 63 abcdefghijklmnop

71 72 73 74 75 76 77 68 61 62 63 64 65 66 67 68 69 qrstuvabcdefghi

========================================================================
```
