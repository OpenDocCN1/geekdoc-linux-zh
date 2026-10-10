
# 使用 DNS 安全扩展

DNS 安全扩展 (`DNSSEC`) 是 `DNS` 协议的一组安全扩展，使用加密数字签名提供数据完整性和身份验证。

（注：原文中该部分包含大量重复的句子和OCR错误，已根据实际内容进行清理。）

`BIND 9 ARM` 讨论了在安全 `split-DNS` 配置中运行 `BIND` 的多个细节。

- `http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Chroot-BIND-HOWTO.html`—一个关于 `chroot` 如何与 `BIND 9` 工作的指南。
- `http://langfeldt.net/DNS-HOWTO/`—适用于 `BIND` 版本 `4`、`8` 和 `9` 的 `DNS HOWTO` 主页。
- `http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/DNS-HOWTO.html#s3`—设置一个解析型、缓存名称服务器。注意，被引用为 `/var/named/root.hints` 的文件在 `Fedora` 中被称为 `/var/named/named.ca`。
- `http://spf.pobox.com/`—发送者策略框架（Sender Policy Framework）主页，一种防止电子邮件地址伪造的方法。

# 第 24 章 LDAP

## 概述

轻量级目录访问协议（`LDAP`），发音为 `ell-ldap`，是那些虽然在后台运行但构成了企业计算核心基础设施部分的技术之一。它的任务很简单：存储关于用户的信息。它的强大之处在于它可以与许多其他服务关联。`LDAP` 可以支持登录身份验证、公钥分发、邮件路由和地址验证等，最近还成为推动单点登录技术的核心。

### 本章内容

- 配置服务器
- 配置客户端
- 管理
- 参考

对于大多数人来说，当将 `LDAP` 视为一种高度专门的数据库服务器时，这个概念会变得更容易理解。在后台，`Fedora` 使用数据库来存储所有 `LDAP` 信息；然而，`LDAP` 并没有提供任何像 `SQL` 那样直接的数据操作方法！

`OpenLDAP` 使用 `Sleepycat` 的 `Berkeley DB (BDB)`，强烈建议保持该默认设置。尽管如此，如果你有特殊需求，也有其他方案。

本章将介绍 `LDAP` 服务器的相对基础的安装，包括如何托管包含员工姓名和地址的范围范围目录服务。`LDAP` 是一个客户端/服务器系统，这意味着 `LDAP` 服务器会对其进行查询。`Fedora` 自带了 `OpenLDAP` 作为其 `LDAP` 服务器，以及几个支持 `LDAP` 的电子邮件客户端，包括 `Evolution` 和 `Mozilla Thunderbird`。本章将涵盖所有这些应用程序。

由于 `LDAP` 数据通常可以在互联网上（或至少在你的局域网内）访问，因此必须尽一切确保你的服务器安全。本章提供了关于 `OpenLDAP` 密码配置的具体指令，我们建议你紧密遵循我们的说明。

## 配置服务器

如果你已经使用 `LDAP` 多年，你会意识到它巨大的力量和灵活性。另一方面，如果你是第一次尝试 `LDAP`，它看起来就像是你能想象到的最糟糕的组件。`LDAP` 有特定的配置要求，极缺乏图形化工具，并且有大量的缩写需要记忆。好的一面是，你所做的努力都是值得的，因为当它运行良好时，`LDAP` 将极大提升你的网络体验。

配置 `LDAP` 服务器的第一步是安装客户端和服务器应用程序。选择“添加/删除应用程序”，点击“网络服务器”旁边的“详情”按钮，并勾选 `openldap-servers`。然后点击“系统工具”旁边的“详情”按钮并选择 `openldap-clients`。安装完成后，关闭对话框并打开终端。

现在切换到 `root` 用户，用你选择的文本编辑器编辑 `/etc/openldap/slapd.conf`。这是 `slapd`（`LDAP` 守护进程）的主要配置文件。向下滚动直到你看到 `database`、`suffix` 和 `rootdn` 这几行。

这是你 `LDAP` 系统最基础的配置。你的服务器名称是什么？`dc` 代表域名组件（domain component），即存储在 `DNS` 中的域名名称——例如 `example.com`。在我们的示例中，使用了 `hullzilla.org`。`LDAP` 将域名的每个部分（用句号分隔）视为一个域名组件，因此域名 `hullzilla.org` 由域名组件 `hullzilla` 和域名组件 `org` 组成。

修改 `suffix` 行以匹配你的域名组件，并用逗号分隔。例如：

```
suffix "dc=hullzilla,dc=org"
```

接下来的几行定义了 `root DN`，这是另一个缩写，意为区分名（distinguished name）。`DN` 是你目录中某人的描述符：她的姓名和她所在的域名。例如：

```
rootdn "cn=root,dc=hullzilla,dc=org"
```

`CN` 是另一个 `LDAP` 缩写，这次代表通用名称（common name）。通用名就是——人的称呼。有些人有多个通用名。`Andrew Hudson` 是一个通用名，但该用户可能也有通用名 `Andy Hudson`。在我们的 `rootdn` 中，我们定义了一个完整的用户：在 `hullzilla.org` 域名下的 `root` 用户。这些行本质上是从反向读取的。`LDAP` 进入 `org`，搜索 `hullzilla`，然后在 `hullzilla` 中搜索 `root`。

`rootdn` 非常重要，因为它不仅仅是目录中的一个人。`root LDAP` 就是 `Linux` 中的 `root` 用户。它是对系统拥有完全控制权并可以进行任何他想要更改的人。

现在到了稍微复杂的部分：`LDAP` 用户需要设置密码。实现此最简单的方法是在现有的窗口旁边打开一个新终端窗口。同样切换到新终端，并输入 `slapppasswd`。该工具使用 `SHA1` 哈希算法为 `OpenLDAP` 生成密码哈希。在提示你时输入密码。当你输入并确认密码后，你应该能看到输出行：

```
{SHA1}qMVx...
```

（注意：OCR 中的哈希被截断/损坏了，但结构是的）

```
{SHA1}qMVx...dc=hullzilla,dc=org
```

最后的配置是：

```
chkconfig ldap on
service ldap start
```

## 填充你的目录

安装、配置并运行 `LDAP` 后，你现在可以填充目录了。这涉及到更多的 `LDAP` 缩写，绝非易事。

首先，创建 `ldif` 文件。使用该文件定义你系统的基础组件：域名和地址录。`LDIF` 是 `LDAP` 数据交换格式（`LDAP Data Interchange Format`）的缩写，它是向 `LDAP` 目录插入用户数据的标准方法。以下是我们示例中使用的内容：

```
dn: dc=hullzilla,dc=org
objectClass: top
objectClass: dcObject
objectClass: organization
dc=hullzilla
o=Huzilla Org
dn: ou=People,dc=hullzilla,dc=org
ou=People
objectClass: top
objectClass: organizationalUnit
```
