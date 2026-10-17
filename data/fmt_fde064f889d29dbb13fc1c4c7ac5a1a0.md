
`lucy@somehost.mynet.net$`

```
由于 Kerberos 密码集中存储在 KDC 上，因此任何新密码将在该领域内的任何主机上生效，而不仅仅是输入密码的这台主机。同样重要的一点是，要理解 Kerberos 密码与任何主机上的登录密码没有关系。
```

## 加密数据流

Kerberos 5 包含的大多数客户端（包括 `telnet`、`rlogin`、`rsh` 和 `ftp`）都包含了内置加密选项，这将使它们更加安全。要完全加密会话，请使用 `-x` 参数：

```
lucy@somehost.mynet.net$ login -x anotherhost

This login session is using DES encryption for all data transmissions.

Last login: Fri Jan 12 14:46:53 from somehost

lucy@anotherhost.mynet.net$
```

尽管 Kerberos 文档警告加密会导致速度变慢，但这个警告并不适用于运行 Linux 的现代 PC 硬件，加密算法在这些硬件上只需要 CPU 一部分时间。

## 总结

在本小时中，你学习了如何编译和安装 Kerberos 5，以便为你的本地领域配置 KDC。你还学习了 Kerberos 管理任务，例如向你领域的 KDC 数据库中添加管理员、额外主机和用户主体。

最后，你学习了安装 Kerberos 后使用 Kerberos 的基础知识，包括如何获取并随之销毁票证、如何更改 Kerberos 密码，以及如何加密 Kerberos 5 包含的标准协议客户端的数据流。

## 问答

- 我无法启动 `krb5kdc`。
- 我无法启动 `kadmind`。

![](img/5b265b1d98ba2e1a657c3f9cdc5ce677_290_0.png)

重新检查一遍指令并双重确认一切，确保你遵循了所有步骤。你是否使用 `kdb5_util` 为你的领域创建了数据库？你是否记得使用 `-s` 选项隐藏密钥？在尝试启动 `kadmind` 之前，是否记得使用 `ktadd` 将 `admin/admin` 和 `kadmin/changepw` 添加到 `kdb5.keytab` 文件中？作为最后的手段，使用 `trace` 启动 `krb5dc` 或 `kadmind`；这应该能告诉你失败的原因。

问：我在一个或多个主机上安装了 Kerberos，现在 `telnet`、`ftp`、`login` 以及其他某些协议无法工作。发生了什么？

答：你必须运行特殊的启用 Kerberos 的客户端才能连接需要 Kerberos 认证的系统。确保你从 `/usr/local/kerberos/bin` 目录调用协议，而不是来自 `/usr/bin` 的二进制文件。

问：有方法制作其他协议吗？

答：绝对可以。许多 Linux 软件包支持 Kerberos，通常通过配置文件实现。例如，`SSH` 版本2（见第16 小时“加密数据流”）可以使用 Kerberos。

问：单一的 KDC 不是一个漏洞吗？

答：是的。这就是为什么尽可能加固你的 KDC，不在上面运行额外的服务，并频繁备份 KDC 非常重要。

还有一种允许辅助 KDC 在需要时运行的规定。此功能将详细讨论。

## 新术语

`export` Kerberos 协议的另一种实现方式，用于规避对 MIT Kerberos 代码的限制。

Kerberized 享受启用 Kerberos 的状态。Kerber化的系统或服务能够处理 Kerberos 认证。

key distribution center (KDC) 负责维护领域内所有主体信息并处理认证交换的系统。

primary 在某种意义上是账户的另一个词。主体是 KDC 数据库中的条目，指向用户、管理员或主机。每个主体都有密码，如果配置如此，还有描述主体属性和权限的策略信息。

realm Kerberos 网络的影响范围，或者更具体地说，通常是一个单一 KDC。在一个 Kerberos 领域内，通常可以找到许多用户、管理员和主机。按照惯，领域是转换为全大写的域名。

ticket 发给主体的小型识别单元，随后结合 KDC 用于该主体对领域内其他主体进行认证。

## 27 小时18

### 加密网页数据

在本小时中，你将学习如何编译并配置一个经过 `mod_ssl` 软件包增强的 `Apache` 服务器，使其能够处理 SSL（安全套接层）通信以提高安全性。你还将学习如何为此类通信创建一个自签名证书，以便你能够立即通过你的 Web 浏览器接受 https 连接。

然而，请理解，网络安全是一个庞大且复杂的研究领域，在许多方面远出了这本书的范畴。本小时将不会讨论 SSL 的底层机制，或通过知名的证书机构（CA）如 VeriSign 或 Sectigo 为你的 Web 服务器进行认证的过程。

为了对 SSL 涉及的许多问题进行初步了解，`mod_ssl` 用户手册是一个极好的起点。你可以在 http://www.modssl.org/docs/2.7/ 找到它。

# 编译并安装 Apache+mod_ssl

遗憾的是，升级您的 Apache 安装以支持 SSL 意味着重新编译并安装 Apache 二进制文件。正因如此，从头开始安装 Apache 比尝试将新组件放入旧位置要简单得多。

因此，建议在开始之前，先备份您现有的 Apache 配置和数据文件，然后使用您发行版的包管理器删除 `apache` 或 `httpd` 系列软件包。不需要删除您实际的 Web 文档树；它可以保持在原位，您可以更新您的新配置文件以反映其位置。

![](img/5b265b1d98ba2e1a657c3f9cdc5ce677_295_0.png)

> 随着最近几个月对 SSL 出口限制的解除，某些 Linux 发行版已开始将 Apache+mod_ssl 作为标准发行版组件进行发布。

在执行本章的步骤之前，您可能想要检查 Apache+mod_ssl 是否是您的 Linux 发行版的标准组件。

# 下载 Apache、OpenSSL 和 mod_ssl

要编译并安装 `mod_ssl`，你实际上需要下载并编译三个软件 tar 包：一个用于 Apache，一个用于 OpenSSL，一个用于 `mod_ssl`。

OpenSSL 的首页可以在 http://www.openssl.org 找到。最新版本的 OpenSSL 源码可以从 http://www.openssl.org/ 下载。

`mod_ssl` 的首页可以在 http://www.mod_ssl.org/ 找到；最新版本的 `mod_ssl` 源码可以从 http://www.mod_ssl.org/source/ 下载。你会发现每个 `mod_ssl` tar 包都有两个版本号，请参考 `mod_ssl` 网站上的以下名称：

```
mod_ssl-2.7.1-1.3.14.tar.gz

mod_ssl-2.6.6-1.3.12.tar.gz

mod_ssl-2.5.1-1.3.11.tar.gz

mod_ssl-2.4.10-1.3.9.tar.gz
```

在这些名称中，第二个连字符之前的版本号（2.7.1, 2.6.6, 2.5.1, 2.4.10）代表 `mod_ssl` 版本号，而第二个连字符之后的版本号（1.3.14, 1.3.12, 1.3.11, 1.3.9）代表该 `mod_ssl` tar 包旨在运行的 Apache 版本。请确保获取与计划使用的 Apache 版本匹配的 `mod_ssl` tar 包，反之亦然。

Apache Web 服务器的首页可以在 http://httpd.apache.org/ 找到；最新版本的 Apache Web 服务器源码可以从 http://httpd.apache.org/dist/ 下载。对于此项目，请下载与您的 `mod_ssl` tar 包匹配的 1.3 版本 Apache 服务器，而不是更新的 Apache 2.0 版本。这是必要的，因为 `mod_ssl` 尚不支持 Apache 2.0 或更高版本。

# 解压并编译 OpenSSL

对于本次安装，必须从解压和编译 OpenSSL 开始。如果您已经在第 16 小时“加密数据流”中完成了此安装，并且仍然保留源码目录，则可以跳过此步。

解压源码并进入新创建的源码目录：

```
$ tar - xf openssl-0.9.6.tar.gz

$ cd openssl-0.9.6

$
```

现在配置、编译并安装 OpenSSL：

```
$ ./config

... [ output of config ...]

$ make

... [ output of make ...]

$ su

Password:

# make install

... [output of make install ...]

$
```
