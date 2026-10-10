
# 创建虚拟专用网络 • 第8 章

为了让 IPSec 工作，你必须设置公钥加密。正如你在第 7 章中学到的，公钥加密使用私钥和公钥来确保身份验证。私钥仅主机已知，而公钥对其他人可用，即系统将要通信的所有主机。

> 注意
>
> RSA 算法的美国专利已于 2000 年 9 月 20 日过期。因此，RSA 用于 FreeSwan/WAN 的公钥加密，并将随着新程序的开发和新版本的发布，整合到许多额外的开源程序中。

在 FreeSwan/WAN 安装过程中创建了一个 RSA 密钥对。该密钥对被放置在 `/etc/ipsec.secrets` 文件。此文件必须保持安全，因为你的公钥列在其中。只有你（超级用户）应该拥有访问此 `/etc/ipsec.secrets` 文件的权限。

公钥应该放置在 `/etc/ipsec.conf` 文件。由于公钥对任何与你通信的人都可见，因此 `/etc/ipsec.conf` 文件的安全性并不重要。FreeSwan/WAN 的私钥和公钥位置总结在表 8.5 中。

## 表 8.5 FreeSwan/WAN RSA 密钥对的位置

| 密钥 | 文件名 | 在主机上的位置 |
|---|---|---|
| 私钥 | `ipsec.secrets` | `/etc/ipsec.secrets` |
| 公钥 | `ipsec.conf` | `/etc/ipsec.conf` |

你将在后续步骤中在 `host1` 和 `host2` 上配置这些文件，以便启动隧道。完成以下步骤来为你的系统配置 FreeSwan/WAN。FreeSwan/WAN 和 IPSec 将 VPN 端点称为“左”`left`和“右”`right`主机。在本节的演示中，`host1` 是左，`host2` 是右。

- 1. Host1: 首先，你将配置 `/etc/ipsec.secrets` 文件，该文件列出了系统的公钥和私钥。输入以下命令打开文件：

```
vi /etc/ipsec.secrets
```

![](img/a7a9caa80ec85507179284d91e216f9f_426_0.png)

你看到的内容将如图 8.28 所示。

## 图 8.28 配置 `/etc/ipsec.secrets` 文件

![](img/a7a9caa80ec85507179284d91e216f9f_427_0.png)

- 2. Host1: 你正在使用公钥认证，因此你需要注释掉 `#` 表示“共享密钥”`Shared secret` 的行。为了为此，按 `I` 并注释掉文件第二段的最后一行，如下（你的任意字符字符串可能会不同）：

```
# Shared secret（一个任意字符字符串，应该既长又难以猜测，并包含在引号内）用于一对
# 协商的主机。
# 10.0.0.1 10.12.12.1 : PSK
# "jcmxWkWkm4uV1m4Sw3SuWF1233Wu5S5U3S"
```

- 3. 注意文件中列出的公钥和私钥。`Pluto` 是 FreeSwan/WAN 上的 IKE 实现，它使用这些密钥来验证你的主机。

- 4. Host1: 按 `ESC` 键，然后等待并输入以下命令退出文件：

```
:wq
```

> 注意：IPSec（以及 FreeSwan/WAN）默认使用 RSA 密钥进行 VPN 主机之间的认证。加密默认通过 3DES 完成。

- 5. Host1: 接下来，你将配置 `/etc/ipsec.conf` 文件，该文件列出了 IPSec 的配置和连接信息。

- 6. Host1: 为 `/etc/ipsec.conf` 文件创建一个备份副本并命名为 `ipsec.conf-backup`。`ipsec.conf` 文件实际上是一个你必须配置的示例文件。

```
cp /etc/ipsec.conf /etc/ipsec-backup
```

- 7. 输入以下命令打开 `/etc/ipsec.conf` 文件：

```
vi /etc/ipsec.conf
```

- 8. Host1: 你的文件将类似于图 8.29（图 8.30）所示的文件。

## 图 8.29 配置 `/etc/ipsec.conf` 文件

![](img/a7a9caa80ec85507179284d91e216f9f_428_0.png)

![](img/a7a9caa80ec85507179284d91e216f9f_428_1.png)

Host1: 正如图 8.29 所示，`/etc/ipsec.conf` 是 FreeSwan/WAN 的主配置文件，包含三个部分。图中显示了“基础配置”`basic configuration`和“后续连接描述的默认值”部分。“连接”`connection`部分将在这两个部分完成后讨论。

> 注意
>
> 有关 `ipsec.conf` 配置选项的更多信息，请参考以下文档：
>
> * www.freeswan.org/freeswan-1.9/doc/manpage/ipsec.conf.html
>
> * man ipsec.conf
>
> * /root/freeswan-1.9/doc/examples

Host1: 按照所示读取“基础配置”部分。你不需要对此部分进行任何更改。额外的注释如下：

```
# basic configuration
config
# 此设置必须正确，否则将无法工作。
# @defaultroute 大多数情况下可以。它定义了
# IPSec 使用的接口。例如，你也可以为
# 值添加 "ipsec0-eth0"。
@defaultroute
# 调试日志：指定 Pluto 调试输出。默认为 "none"。需要所有日志时输入 "all"。
debug=none
plutebug=none
# Pluto 指定连接名称（在文件的第三
# 部分指定），启动时加载到
# 数据库。在调用之前不会尝试启动。
plutoload=host-to-host
```

![](img/a7a9caa80ec85507179284d91e216f9f_429_0.png)

```
# 当新连接建立时关闭旧连接。
uniqueids=yes
```

- 11. Host1: 你必须修改“后续连接默认值”部分。你在这里启用的配置将决定后续“连接”部分的行为。由于你使用的是公钥加密，不需要手动条目。该部分应如下（不需要输入注释）：

```
# defaults for subsequent connection
%default
# 密钥协商的次数（0 表示从不）。
keying tries=0
# 表示 VPN 连接将使用 RSA 认证。
# 要生成你的公钥，打开终端并
# 'ipsec show host'。将你的公钥复制到 leftasignkey 值。将 host2 的公钥复制到 rightasignkey。
authby=rsa
leftasignkey=
```

> 注意 `host1` 的公钥也列在 `/etc/ipsec.secrets` 文件中，并以 `pubkey=0x` 开始（见图 8.28）。只需要十六部分，不需要 `pubkey=""` 部分。你可以从 `host1` 复制公钥并粘贴到 `leftasignkey` 值中。你可能想使用比 `vi` 其他文本编辑器来复制公钥。

- 12. Host1: 你必须修改“示例连接”`sample connection`部分，使其适用于主机对连接。连接部分如图 8.30 所示。

![](img/a7a9caa80ec85507179284d91e216f9f_430_0.png)

## 图 8.30 配置 `/etc/ipsec.conf` 文件的连接部分

![](img/a7a9caa80ec85507179284d91e216f9f_431_0.png)

如果你在为网络配置 VPN，将输入“`leftsubnet`”和“`rightsubnet`”选项（如图 8.30 所示）。这些选项标识网关连接的局域网地址。如果你在配置涉及远程用户的 VPN，你只需要在一侧标识子网，因为远程用户没有网关，它是一个主机。

- 13. Host1: 修改主机对 VPN 解决方案的连接部分。按如下修改该部分（不需要输入注释）：

- 13. Host2：通过输入以下内容确保 Apache 已安装：

- 14. Host2：如果已安装 Apache，你将收到类似下内容的响应：

- 15. Host1：如果没有收到响应，故障排除你的网络，直到两个主机之间建立连通性。

- 16. Host2：通过输入以下内容确保 Apache 已安装：

- 17. Host2：如果已安装 Apache，你将收到类似下内容的响应：

- 18. Host1：如果没有收到响应，故障排除你的网络，直到两个主机之间建立连通性。

- 19. Host2：通过输入以下内容确保 Apache 已安装：

- 20. Host2：如果已安装 Apache，你将收到类似下内容的响应：

- 21. Host1：如果没有收到响应，故障排除你的网络，直到两个主机之间建立连通性。

- 22. Host2：通过输入以下内容确保 Apache 已安装：

- 23. Host2：如果已安装 Apache，你将收到类似下内容的响应：

- 24. Host1：如果没有收到响应，故障排除你的网络，直到两个主机之间建立连通性。
