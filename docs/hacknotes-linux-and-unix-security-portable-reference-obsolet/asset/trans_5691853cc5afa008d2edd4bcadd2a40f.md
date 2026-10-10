

当启用此选项时，Nessus 会扫描与目标机器开放端口上运行的应用程序相关的漏洞。`script_require_ports` 函数可用于设置远程机器上与漏洞相关的端口，在我们的案例中，该端口被设置为 www (HTTP)。

上述描述的函数用于为插件设置各种描述值。插件的描述可以通过双击 Nessus GUI 客户端中 Plugins 选项卡显示的插件列表中相应的插件名称来查看。图 10-1 展示了相应的截图。`http_func.inc` 文件包含了一组方便我们使用的有用 HTTP 函数。由于我们使用了该文件中定义的函数，因此我们通过 `include` 函数包含了此文件。

`get_port_state` 函数用于检查目标主机上特定端口的状态。在我们的案例中，我们检查 80 端口。如果该端口已关闭，继续操作就没有意义，因此我们调用 `exit(0)`。

为了检查 Web 服务器上是否存在 `/src/passwd.inc` 文件，连接到 Web 服务器时发送的 HTTP 请求必须如下格式：

```
GET /src/passwd.inc HTTP/1.0
```

![](img/77287f6ef97ef0bed6e23f6610950d06_219_0.png)

**图 10-1.** Nessus GUI 客户端显示的插件描述

上述 GET 请求可以通过使用 `http_get` 函数来创建。然后，该请求可以作为 `send` 函数的参数，该函数通过 `http_open_sock` 函数打开的套接字连接将请求发送到目标主机。使用 `http_recv` 函数读取来自 Web 服务器的结果数据，并将其内容存储在 `myrec` 变量中。完成后，使用 `http_close_socket` 关闭套接字描述符。然后检查 `myrec` 的内容中是否包含子字符串 `404`，如果 Web 服务器上不存在该文件，则会存在该子字符串。这使用 `<<` 运算符完成，该运算符用于检查给定字符串变量中的子字符串。如果在来自 Web 服务器的返回数据中未找到 `404`，则很可能该文件存在，并通过调用 `security_hole` 函数将此事实告知 Nessus。

请参见 [http://www.nessus.org/doc/nasl2_reference.pdf](http://www.nessus.org/doc/nasl2_reference.pdf) 以获取最新的 NASL 参考手册。

## 运行插件

请确保上述脚本放置在 Nessus 的插件目录中。该脚本的文件名必须以扩展名 ".nasl" 结尾。运行 Nessus GUI 并选择 Plugins 选项卡。确保选中 CGI Abuses。高亮显示 CGI Abuses 并确保名为 "Checks for `/src/passwd.inc`" 的插件已启用。如果您难以找到该插件，请点击 Filter 按钮并搜索 ID 为 `9999` 的内容。

要从我们的插件获得阳性结果，您必须配置一个本地 Web 服务器来提供 `/src/passwd.inc` 文件。如果某主机上正在运行 Apache Web 服务器，只需使用 `touch` 命令在 Web 服务器的 Web 根目录下创建 `/src/passwd` 文件：

```bash
mkdir /var/www/html/src
touch /var/www/html/src/passwd
```

在 Target Selection 选项卡中输入目标 Web 服务器的 IP 地址或名称，然后点击 Start The Scan。如果一切顺利，Nessus 将检测并报告我们的自定义漏洞，如图 10-2 所示。

![](img/77287f6ef97ef0bed6e23f6610950d06_221_0.png)

## 总结

本章展示了使用 NASL 语言为 Nessus 扫描器编写插件的便捷性。首先，介绍了一个 Web 应用程序漏洞示例。接着，详细讨论了创建一个用于检测此漏洞的 NASL 脚本的过程，并对脚本源代码进行了逐步说明。还提供了如何将 NASL 脚本集成到 Nessus 插件列表中的说明。大型组织经常使用自行开发的软件应用程序，其中可能会发现漏洞。此外，Nessus 扫描器包中可能不包含某些漏洞检查，而这些检测对于组织的安全态势至关重要。本章中的信息可用于从零开始编写 Nessus 插件，以检测此类漏洞。

# 第 11 章 无线入侵

本章内容：

- WEP 简介
- 天线
- 流行工具
- 保护无线网络
- 总结

无线网络搭建起来非常容易，对于讨厌被以太网线束缚的人来说是一大福音。然而，由于 802.11b 标准中使用的有线等效隐私 (WEP) 协议存在漏洞，从安全角度来看，它们也是一场噩梦。由于 Airospot 和 Kismet 等自由获取的开源工具的存在，任何拥有无线网卡和笔记本电脑的人都可以入侵无线网络。已知有人驾车在城市各处寻找那些无线网络覆盖范围可能超出其办公空间、可到达如停车场等可访问地点的公司，这种活动被称为“战争驱动”（war driving）。不幸的是，许多无线网络管理员并没有意识到这一点，也未意识到自己易受此类入侵者的攻击。本章描述了入侵者用于获取无线网络访问权限的工具和技术，并提出了如何更好地对此进行防护的建议。

### WEP 简介

由于 WEP 基于对称共享密钥系统，它使用相同的密钥来加密和解密数据。密钥 (k) 长度要么为 128 位，要么为 64 位，由一个 24 位的初始化向量 (IV) 组成。WEP 有效载荷的构造如下：

1. 将消息 M 与其自身的 CRC-32 校验和 c(M) 拼接：
   `M c(M)`
2. IV 在秘密密钥之前应用，并经过 RC4 流密码算法：
   `RC4(IV,k)`
3. 将步骤 1 和 2 的结果进行异或（XOR，即 eXclusive OR）运算以生成密文。然后，将 IV 与密文拼接以生成 WEP 有效载荷：
   `IV Cipher-text = ((M),c(M)) XOR (RC4(IV,k))`

从上述步骤可以看出，WEP 帧包含明文 IV。许多无线网卡随机选择其 IV，而另一些则从 0 开始顺序递增。由于 IV 仅 24 位长，无线网卡或接入点每隔几个小时就会重用一次。

请注意，最终传输的帧除了其他信息外，还包含明文的 MAC（媒体访问控制）源和目标信息。

Aircrort 等工具利用 RC4 密钥调度算法 (KSA) 中的弱点。这些弱点的细节由 Scott Fluhrer、Islik Mantin 和 Adi Shamir 在一篇研究论文中提出。该论文可以通过请求以下 URL 获取：http://www.drizzle.com/~aboba/IEEE/rc4_ksa proc.pdf。

### 天线

在对某个区域进行无线活动审计时，找到合适的天线非常重要。使用天线可以接收否则无法检测到的来自网络的无线信号。

**定向** 顾名思义，定向天线专注于特定方向来接收和发送信号。这些天线对于在两个位置之间创建无线桥接最为有用。定向天线通常用于建立两个远程位置之间的点对点链接。因此，在移动时或在信号方向未知的情况下，它们帮助不大。常见的定向天线类型包括八木天线和抛物面天线。

**全向** 全向天线通常用于扩展接入点的范围。它们在所有方向上传输和接收信号。因此，全向天线在实施“战争驱动”测试的个人中很受欢迎。以下是一些专营天线的知名供应商列表：

- Fleeman Anderson & Bird Corp: http://fab-corp.com/
- HyperLink Technologies: http://www.hyperlinktech.com/
- NetNimble: http://www.netnimble.net/
- SuperPass: http://www.superpass.com/
- Wireless Central: http://wirelesscentral.net/

想要自己制作低成本天线吗？请访问 http://www.turnpoint.net/wireless/has.html 上的“802.11b Homebrew Antenna Shootout”。

