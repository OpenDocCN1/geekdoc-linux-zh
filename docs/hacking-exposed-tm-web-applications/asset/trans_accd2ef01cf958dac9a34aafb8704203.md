

## 第 3 章：破解 Web 服务器

200 OK-> :/null.ida ^Code Red?

200 OK-> :/null.idq ^Code Red?

从这个示例中可以看出，Tux 允许用户轻松地指定他们期望在给定请求的响应中看到的 HTTP 返回码。图 3-6 显示了该 .exe 文件在默认安装的 IIS 5 上运行时的界面。

## Stealth HTTP 扫描器

| 优点: | 可扩展性，定期更新 |
| 缺点: | 3.0 版本每个 IP 费用为 $250，界面不直观 |
| 最终分析: | 如果掌握了它，检查非常全面 |

目前可用较新且初印象深刻的 Web 漏洞扫描器之一是 Felipe Monet 开发的 Stealth HTTP Scanner。截至本文编写，最新的商业版本 N-Stealth 3.0 声称可以扫描超过 18,000 种 HTTP 安全问题，并可以使用极其简单的脚本语言向其添加自定义检查。以下信息适用于 Stealth 2.0  35 版本，因为我们未能能在出版前及时获得 N-Stealth。

尽管 Stealth 是图形化工具，但使用起来可能有些棘手。例如，一旦你填充了 Scanner 按钮上的“Host”字段，扫描 IP 地址范围的选项就会消失；恢复它的唯一方法是清除 Host 字段并勾选 IP Range 框。此外，清除屏幕上的 Clean List 需要手动编辑

![](img/2c61c2d28445b774d9266972920f432d_111_0.png)

图 3-6. twwwscan 的部分，正在运行自定义 .exe 文件

## 破解的 Web 应用程序

Stealth 目录下的 Scanlist.lst 文件。因此，每当 Stealth 提示要将当前服务器添加到扫描列表时，我们总是回答“否”。无论你只能扫描服务器列表还是一个，无论指定的端口是否可用，Stealth 都会进行分析。这可能是它最令人烦恼的功能之一，真的导致该工具太慢，无法扫描大范围的系统。

自定义检查被导出并包含在 .exp 文件中。程序的 `Db Files\Stealth\` 目录下有几个带有 Stealth 1.0 的 .exp 文件。查看与标准 Stealth 软件包一起运行的 doublecode.exe 脚本——该脚本由 Arjun Shunn 编写，是 Stealth 能够实现的全面性和灵活性的良好示例。

你可以编写自己的 .exp 文件并将其存储，以便 Stealth 访问（在 Database 选项卡 | Stealth's Export 中查看保留在 Db 目录中的 .exp 文件列表；如果你的自定义 .exp 没有显示，请点击右下角的刷新按钮）。你可以选择想要运行的 .exp 文件，然后通过点击 Scanner 按钮、选择 Hacking Techniques 选项卡并勾选 Include Stealth's Techniques 复选框来告诉 Stealth 在扫描期间使用它们。

编写 .exp 文件非常简单。你可以编写两种类型的检查：标准检查和缓冲区溢出测试。一个标准的示例检查是：

```
#GET /null.printer #500
```

这是一个简单的检查，用于查看 IIS 5 Web 服务器是否容易受到本章中讨论的互联网打印协议漏洞的影响。你可以看到使用 GET HTTP 方法请求 /null.printer，并期望获得 HTTP 500 Internal Server Error 响应，这表明服务器可能存在漏洞。

以下是编写简单的缓冲区溢出测试的方法：

```
bofgen=/sample.exe?%bofstr,"bytes=9","chars=a"
```

Stealth 对目标服务器生成的检查结果为：

```
GET /sample.exeaaaaaaaaaaaa
```

这是一个实验边界条件的有趣工具，带有缓冲区溢出测试（就像标准检查一样），因此，除非你在目标服务器上运行调试器或通过其他监控请求的影响，否则它的效用有限。

版本 2.0 现在包含了一个 Expl 开发工具，它本质上为 .exp 文件开发过程提供了一个图形化界面。它允许你指定请求字符串、预期响应和选项。2.0 版本还包含一个更新实用程序，它可以自动访问用户定义的服务器并获取和安装任何更新。

Stealth HTTP Scanner 将扫描结果导出为易于阅读的 HTML 报告。图 3-7 显示了查看 IIS 5 系统扫描的 Stealth 界面。

![](img/2c61c2d28445b774d9266972920f432d_113_0.png)

## Typhon

| 优点: | 简单的图形界面，在线更新 |
| 缺点: | 无自定义漏洞检查，一次只能处理一个主机 |
| 最终分析: | 等待 Typhon II |

Typhon 是 Cerberus Internet Scanner (CIS) 的重生版，由 David Litchfield 编写，并在他们英国的 Cerberus Internet Security 公司进行了重新设计。David 曾短暂经手 @Stake 之手，现在通过其新公司 Next Generation Security Software (NextGenSS Ltd.) 再次单独营销 Typhon。

图 3-7. Stealth HTTP 扫描器

CIS 是一个基础的安全扫描工具——它在检查数量上的短板通过其所执行的检查的质量得到了弥补。Typhon 延续了这一传统，评估远程目标主机上的各种已 own安全问题，包括与 NT、SNMP、RPC、SQL-、SMTP- 和 FTP 相关的安全漏洞。它甚至包含一个集成的端口扫描器。图 3-8 显示了 Typhon I 的简单配置。

在本课程中，我们主要关注 Web 检查，Typhon 在这方面并不令人失望，它将结果格式化为整洁的 HTML 报告。与我们审查过的扫描器相比，Typhon 的主要缺点是无法编写自定义检查。虽然提供在线更新，但它们替换了整个 Typhon 二进制文件且无法模块化添加。与能够扫描系统范围的扫描器相比，Typhon I 只能扫描一个主机。2002 年，NextGenSS 发布了名为 Typhon II 的 Typhon 商业版，称更加强大。

| 选项 | |
|---|---|
| 端口 | 80 |
| SQL Server 端口 | 1433 |
| SNMP 端口 | 161 |
| UDC 扫描超时 (ms) | 50 |
| 起端口 | 1 |
| 结束端口 | 1024 |
| SMTP 中继地址: | |
| 收件人 | nobody@domain2890.com |
| 要运行的检查 | |
| [ ] 全部 | |
| [ ] Web 检查 | |
| [ ] FTP 检查 | |
| [ ] SMTP 检查 | |
| [ ] POP3 检查 | |
| [ ] NT 检查 | |
| [ ] SQL 检查 | |
| [ ] SNMP 检查 | |
| [ ] 服务 | |
| [ ] 协议 | |
| [ ] 端口扫描 | |
| [ ] Einger | |
| [ ] DNS | [ ] BPC |
| [ ] 其他 | 取消全部 |

图 3-8. Typhon 的扫描选项

## WebInspect

| 优点: | 界面简洁、快速、全面、易于更新、报告详细、基础自定义检查 |
| 缺点: | 昂贵，按目标 IP 地址授权 |
| 最终分析: | 潜力巨大，但价格高 |

来自 SPI Dynamics 的 WebInspect 是一款令人深刻的 Web 服务器和应用程序级漏洞扫描工具。它收集网站内容并进行应用程序级问题分析，寻找超过 1,500 种已 Web 服务器和应用程序漏洞，例如未索引的常见 Web 文件、密码猜测、参数传递和隐藏参数检查。该工具很容易更新，并且可以扩展以使用自定义检查，速度很快——它能够在四分钟内对基础 Web 服务器进行全面分析，包括 1,500 个 HTML 页面。

WebInspect 也有一些缺点。其一是——我们在报价时，每台服务器的永久许可费用为 $5000，加上每年 20% 的维护和支持费用。另一个不满是许可是绑定到目标 IP 范围的，对于大型组织来说是一个负担。当我们使用从 SPI Dynamics 收到的演示版扫描测试网络时，收到的消息也让我们好奇：

> 您正在使用的是 WebInspect 版本，该版本通过安全连接将所有扫描站点的 IP 地址提供给 SPI Dynamics，以便验证您的许可。

希望这仅是演示版的情况。
我们的一点批评是扫描需要手动一个站点地配置——对于大型环境，读取 IP 文本文件要好得多。总的来说，该工具前景良好，但在目前的定价模式下，可能只有资金充足的组织才能使用。WebInspect 如图 3-9 所示。

