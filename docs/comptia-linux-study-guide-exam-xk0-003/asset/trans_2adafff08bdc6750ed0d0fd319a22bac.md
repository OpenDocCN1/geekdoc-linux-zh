
在另一个极端情况下，是一行只包含一个单词：*broadcast*。这告诉工具发送一个广播查询，以寻找合适的 NIS 服务器。你应该咨询你的网络管理员，了解哪种选项最适合你的网络。

一旦你告诉 NIS 工具你的服务器信息，你还必须配置 Linux 以使用 NIS。这可以通过编辑 `/etc/nsswitch.conf` 文件来实现，该文件告诉 Linux 使用什么工具进行名称解析、账户信息等。依赖大量 NIS 的配置如清单 12.2 所示。如果你只想使用 NIS 进行用户身份验证，只需将 `passwd`、`group` 和 `shadow` 行添加 `nis` 到现有选项即可。

## **清单 12.2：** NIS 的 `/etc/nsswitch.conf` 文件示例

```
passwd:         compat
group:         compat
# For libc5, you must use shadow: files nis
shadow:        compat

passwd_compat: nis
group_compat: nis
shadow_compat: nis

hosts:         nis files dns

services:      nis [NOTFOUND=return] files
networks:      nis [NOTFOUND=return] files
protocols:     nis [NOTFOUND=return] files
rpc:           nis [NOTFOUND=return] files
ethers:        nis [NOTFOUND=return] files
netmasks:      nis [NOTFOUND=return] files
netgroup:      nis
bootparams:    nis [NOTFOUND=return] files
publickey:     nis [NOTFOUND=return] files
automount:     files
aliases:       nis [NOTFOUND=return] files
```

设置完成后，你应该启动或重启 ypbind 守护进程，该守护进程必须在 NIS 客户端上始终运行。客户端工具会联系此守护进程以获取通常存储在 `/etc/passwd` 及其他地方的信息；ypbind 守护进程联系 NIS 服务器，而 NIS 服务器提供所请求的信息。通常，通过其 SysV 启动脚本启动 ypbind。

一旦 NIS 启动并运行，你可以使用一系列以 yp 开头的命令来管理系统。例如，`ypasswd` 像 `passwd` 一样修改密码，但 `ypasswd` 在 NIS 服务器上修改密码。在服务器系统上，`ypinit` 初始化用户账户数据库。

## 使用 LDAP

轻量级目录访问协议（LDAP）在某些方面与 NIS 类似，但其目的更加复杂和通用。在 LDAP 的上下文中，目录是一种数据库。LDAP 服务器可以在其目录中存储大量数据，包括与本章主题相关的 Linux 计算机账户信息。

虽然将 Linux 系统配置为 LDAP 服务器远远超出了本章的范围，但将 Linux 配置为用于身份验证的 LDAP 客户端则简单得多。简而言之，除了（或代替）常规本地账户文件外，你还必须配置 NSS 和 PAM 以使用 LDAP。

首先，你必须安装 LDAP 身份验证包。细节因发行版而异，但包名可能是 pam_ldap 和 nss_ldap，或类似的名称。（有时 lib 位于这些包名的开头。）使用你的发行版的包工具找到并安装这些包。

安装包后，你应该编辑 `/etc/ldap.conf` 文件。在此文件中查找 host 和 base 选项，并根据你的网络适当设置：

```
host 172.24.21.102
base dc=luna,dc=edu
```

host 行指定 LDAP 服务器的主机名或 IP 地址，而 base 指定存放账户信息的 LDAP 目录树的基座。如果你不知道这些值，请咨询维护你的 LDAP 服务器的人。

要配置 NSS 以使用 LDAP，你需要编辑 `/etc/nsswitch.conf`，如前文“使用 NIS”中所述。很可能在 passwd、shadow 和 group 行末尾添加 ldap 就能达到你的目的：

```
passwd:  compat ldap
shadow:  compat ldap
group:   compat ldap
```

PAM 配置更为棘手，因为细节因发行版而异，如前文“配置 PAM”中所述。你应该添加对 pam_ldap 的引用，以便对于应该使用 LDAP 的任何服务，都将它添加到 auth 和 account 堆栈中：

```
auth    sufficient    pam_ldap.so try_first_pass
account sufficient    pam_ldap.so
```

有了这些更改，用户应该能够使用在 LDAP 服务器上定义的账户登录。

## 理解 RADIUS

RADIUS 是一种网络身份验证协议，旨在作为多种类型网络访问的单一身份验证工具。RADIUS 服务器经常将网络门户作为客户端——拨号网络服务器、无线接入点（WAP）等。这些客户端中的每一个都需要对整个网络的用户进行身份验证，为了简化管理网络配置，RADIUS 服务器被配置为集中处理与各种访问方法相关的身份验证任务。

RADIUS 反过来可能使用另一种网络工具，如 LDAP 服务器，来保存其身份验证数据。结果可能是复杂的配置。尽管存在这种复杂性，RADIUS 在具有多种需要身份验证的访问方法的大型网络中仍然值得使用。

你可以在 Linux 上运行 RADIUS 服务器，如 FreeRADIUS ([http://freeradius.org](http://freeradius.org))。由于 RADIUS 配置的复杂性和敏感性，我在这里不详细描述。对于 Linux+ 考试的目的，你应该了解什么是 RADIUS。如果你实际需要安装和使用它，我建议你查阅其文档。

### 使用双因素身份验证

普通的 Linux 身份验证涉及要求用户输入用户名和密码。这种方法适用于大多数安装环境；然而，在某些情况下，需要更强的安全性。在这种情况下，你可以诉诸双因素身份验证。这个术语指的是使用两种不同类型的身份验证数据的任何身份验证系统。这些类型包括以下：

- 用户拥有的信息，如用户名、密码或用户最喜欢的颜色
- 用户拥有的物品，如钥匙或身份证件
- 描述用户的特征，如指纹或视网膜图像

第一类信息显然是通过 Linux 最容易获取的。你可以使用计算机上的物理钥匙来提供第二身份验证因素，但当然，如果入侵者窃取了计算机，这种障碍很容易克服。生物特征识别，如指纹扫描器，在一些高安全安装环境中用于提供额外的安全性。虽然可以从各种来源获得此类设备，但你必须找到合适的 Linux 软件将其集成到 PAM 身份验证堆栈中。

### 使用 GNU 隐私卫士（GPG）

有时你可能想加密通过其他方式发送给另一个人的电子邮件消息或文件。电子邮件从未被设计为安全的数据传输工具，大多数电子邮件消息通过多个电子邮件服务器和网络路由器。在这任何一点上的妥协都可能使黑客嗅探电子邮件流量并提取敏感数据，如信用卡号或社会安全号码。加密你的电子邮件可以保护这些细节的隐私。

加密电子邮件的常用工具是 GNU 隐私卫士（GPG 或 GnuPG；[http://www.gnupg.org](http://www.gnupg.org)）包。这个包是专有“Pretty Good Privacy”（PGP）的开源重新实现。除了加密整个消息外，GPG 还允许你数字“签名”消息。以这种方式使用时，缺少 GPG 软件或适当密钥的接收者可以阅读消息，但拥有这些工具的人可以验证内容未被篡改。

## 生成和导入密钥

要开始使用 GPG，你应该首先安装软件。你的发行版很可能将其作为标准包包含在内，因此你可以以这种方式安装。完成此操作后，你必须生成密钥。GPG 密钥在概念上类似于 SSH 密钥：你需要一个私钥（也称为秘密密钥）和一个公钥。顾名思义，私钥是私有的，但公钥是公开可用的。你可以用你的私钥签名消息，读者可以用你的公钥验证；或者你可以用另一个用户的公钥加密消息，该消息只能用该用户的私钥解密。

要生成密钥，你使用带有 `--gen-key` 选项的 `gpg` 程序：

```
$ gpg --gen-key
```

该程序会问你一系列问题。在大多数情况下，使用默认答案应该效果良好，尽管你可能需要输入你的全名和电子邮件地址。密钥存储在 `~/.gnupg` 目录中。

一旦你生成了密钥，你就可以*导出*你的公钥：

```
$ gpg --export name > gpg.pub
```

此命令将与*name* 关联的公键保存在文件 `gpg.pub` 中。你可以使用你的电子邮件地址作为*name*。（如果你创建额外的公钥或添加其他人的公钥，你可以指定它们的名称来导出那些密钥。）然后你可以让你的密钥可供他人使用，以便他们可以加密发送给你的电子邮件消息或验证你签名的消息。添加 `--armor` 选项会产生 ASCII 输出，如果你打算通过电子邮件发送公钥，这可能更可取。你可以使文件在你的网站上可访问，作为电子邮件附件传输，或以其他各种方式分发。

要加密你发送给其他人的电子邮件，你必须获得他们的公钥。询问你的联系人如何获取它们。一旦你做到了，你可以将他们的密钥添加到你的*密钥环*（即 GPG 维护的密钥集合）中：

```
$ gpg --import filename
```

此命令将*filename* 添加到属于其他人的公钥集中。

![](img/9903a4d3f7abd8dcbef1035fa04a3406_566_0.png)

> 虽然公钥按定义是公开的，但与其相关的安全性问题。具体来说，你应该确保你使用的是*合法*的公钥。假设，不良行为者可能会发布伪造的公钥，以获取敏感通信或伪造签名电子邮件。例如，George 可能会分发一个伪造的 GPG 公钥，声称它来自 Harold。然后 George 可以签名看似来自 Harold 的消息，或拦截使用伪造密钥加密并发送给 Harold 的电子邮件。因此，你应该使用尽可能安全的通信方法来分发你的公钥并从他人那里接收公钥。

