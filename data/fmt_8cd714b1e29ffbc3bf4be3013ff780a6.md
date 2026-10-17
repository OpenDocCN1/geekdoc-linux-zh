
## 第 23 章：理解高级 Linux 安全

因此，`encryptfs`工具允许你在文件系统上创建一个位置，以便快速加密和解密文件。然而，当该目录不再作为`encryptfs`类型挂载后，文件就是安全的，无法解密。

### 加密 Linux 文件

Linux 系统上最流行的文件加密工具是 OpenPGP GNU Privacy Guard，即`gpg`。它的灵活性、多种选项，以及它在大多数 Linux 发行版中默认安装的特性都增加了它的魅力。

> 如果你的组织使用第三方云存储公司，你需要知道像 Dropbox 这样的一些公司在接收到文件之前不会对其进行加密。这意味着该公司拥有解密你文件的密钥，可能会使你组织的数据处于危险状态。在将文件发送到云端之前在你的 Linux 系统上加密文件可以增加额外的保护。

然而，你可以使用 Linux 系统上的其他几种加密工具来加密文件。就像`gpg`一样，许多此类工具允许你执行比文件加密多多的操作。以下是你可以用于加密文件的一些流行的加密工具：

- aescript：使用对称密钥 Rijndael，也称为 AES。这个第三方开源软件（FOSS）工具可以从 aescript.com 下载。
- bcrypt：此工具使用对称密钥 blowfish。它不是默认安装。安装`bcrypt`后，可以使用手册（man pages）。
  - 对于 Fedora 和 RHEL：`yum install bcrypt`
  - 对于 Ubuntu：`sudo apt-get install bcrypt`
- ccrypt：此工具使用对称密钥 Rijndael，也称为 AES。它是为了取代标准的 Unix`crypt`工具而创建的，不是默认安装。安装`ccrypt`后，可以使用手册（man pages）。
  - 对于 Fedora 和 RHEL：`yum install ccrypt`
  - 对于 Ubuntu：`sudo apt-get install ccrypt`
- gpg：此工具可以使用非对称密钥对或对称密钥。它是默认安装的，是 Linux 服务器的首选加密工具。默认密算法在`gpg.conf`文件中设置。可以通过`info gnupg`查看手册。

请记住，此列表涵盖了更流行的工具。此外，请记住，许多文件加密工具可以用于文件加密之外之处。

### 使用杂杂工具加密 Linux

你可以对 Linux 中的几乎所有内容进行加密。除了文件系统、目录和文件外，你还可以加密备份、Zip 文件、网络连接等。

表 23 列出了一些杂杂 Linux 加密工具及其功能。如果你想查看当前 Linux 发行版上安装的加密工具完整列表，请在命令行输入`man -k crypt`。

#### 表 23.2 Linux 杂杂加密工具

| 工具 |  |
| --- | --- |
| Duplicity | 加密备份。Fedora 和 RHEL 默认安装。要在 Ubuntu 上安装，请在命令行使用`sudo apt-get install multiplicity`。 |
| gpg-zip | 使用 GNU Privacy Guard 加密或签名存档中的文件。默认安装。 |
| Opensl | 一个实现套接层 (SSL) 和传输层安全 (TLS) 协议的工具包。这些协议默认需要加密。 |
| Seahorse | GNU Privacy Guard 加密管理器。Ubuntu 默认安装。在 Fedora 和 RHEL 上安装，请在命令行安装`seahorse`。 |
| SSH | 加密跨网络的远程访问。默认安装。 |
| Zipcloak | 加密 Zip 文件中的项目。默认安装。 |

与 Linux 系统上的其他项目一样，可用的加密工具非常丰富。这为你提供了所需的灵活性和多样性，以实施你特定组织所需的加密标准。

### 为桌面使用加密

“密码和密钥”（Passwords and Keys）窗口提供了从 GNOME 桌面查看和管理密钥及密码的方法。可以通过在“活动”屏幕上选择“密码和密钥”或运行`seahorse`命令来启动此窗口。通过该窗口你可以进行以下操作：

- **密码**——当你访问某服务并输入用户名和密码（并选择保存该密码）时，它会被存储在你的系统中，以便下次访问该网站时使用。选择“密码”标题下的“登录”条目可以查看每个保存的用户名和密码。
- **证书**——你可以查看与 Gnome G2 密钥库、用户密钥存储、系统信任和默认信任相关的证书。
- **GPG 密钥**——你可以查看正在创建的 GPG 密钥。条目 23.6 显示了在本章早些创建的 John Doe 条目的结果，以查看有关该用户私钥的详情。
- **安全外 (Secure shell)**——你可以创建公钥和私钥 SSH 密钥，让你使用这些密钥而不是密码通过`ssh`、`scp`、`rsync`、`sftp`和相关命令登录远程系统。选择“OpenSSH 密钥”以查看你为此目的创建的任何密钥。（有关创建此类密钥的信息，请参见第 13 章的“基于密钥的无密码身份验证”）。

图 23.6：
从“密码和密钥”窗口 (`seahorse`) 查看系统上的私钥。

![](img/3886a4c1a684ab63e25e82e0a2d63de9_686_0.png)

对于图 23.6，我为早些时候 John Doe 创建的私钥选择了“详细信息”标签页。从该标签页，你可以看到诸如密钥何时创建、何时过期、密钥类型及其指纹，以及可以过期或撤销的子密钥。

# 章节：学习 Linux 安全技术

继续

![](img/3886a4c1a684ab63e25e82e0a2d63de9_687_0.png)

Pyrite 是 Linux PAM 上提供的另一种强大的安全工具。本章的下一节将介绍 PAM 的基本概念以及你如何利用这些概念进一步增强 Linux 系统的安全性。

# 使用 PAM 实现 Linux 安全

可插件认证模块（Pluggable Authentication Modules，简称 PAM）由太阳微笑（Sun Microsystems）发明，最初在 Solaris 操作系统实现。Linux-PAM 项目始 1997 年。今天，大多数 Linux 发行版都使用 PAM。

PAM 简化了认证管理过程。请记住，认证（参见第 22 章“理解基础安全”）是确定主体（即用户或进程）是否知道其身份的过程。这个过程有时被称为“身份识别与验证”。PAM 是为 Linux 系统和应用程序提供认证的集中方法。

应用程序可以使用 PAM 编写，并被称为“PAM 感知（PAM-aware）”。PAM 感知应用程序在更改认证设置时，不需要重写或重新编译。任何所需的更改都是在 PAM 感知应用程序的 PAM 配置文件中完成。因此，这些应用程序的认证管理是集中且简化的。

你可以查看特定的 Linux 应用程序或工具是否是 PAM 感知的。检查它是否使用 PAM 库`libpam.so`编译。在接下来的示例中，将检查`crontab`应用程序的 PAM感知性。`ldd`命令检查文件的共享库依赖。为了简单起见，使用`grep`搜索 PAM 库。如你所示，在这个特定的 Linux 系统上，crontab 是 PAM 感知的。

```
# ldd /usr/bin/crontab | grep pam

libpam.so.0 => /lib/libpam.so (0x44d12000)
```
