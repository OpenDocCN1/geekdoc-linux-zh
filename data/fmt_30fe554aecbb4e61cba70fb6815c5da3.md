
值得庆幸的是，推动 SSH 成为加密连接标准的行动已经展开，从而使该协议成为公开知识。这意味着许多其他人开始着手为非 UNIX 操作系统编写 SSH 客户端。不过，你不会看到太多新的 UNIX 开发工作，因为 SSH Communications Security 已经提供了一个带有完整源代码的免费客户端/服务器版本，访问地址为 http://www.ssh.fi/sshprotocol2。SSH Communications Security 与 Data Fellows 有关联，后者为 Windows 和 Mac OS 环境提供商业版本的 SSH 客户端。由于 Windows 和 Mac OS 都不支持多用户登录，因此它们没有对应的 SSH 服务器。

### SSH 版本

SSH 协议的第二版于 1998 年发布。随着这个新版本，新的客户端和服务器也随之而来，但它们与旧版本不向后兼容。目前大多数 Windows 和 Macintosh 客户端仅支持版本 1。

由于升级到支持 SSH 版本 2 是个好主意，你最好让这两个版本的服务器并行运行。如何在配置部分实现这一点将在本章稍后的章节中解释。

### SSH 客户端的替代供应商

你们中的许多人每天都在异构环境中工作。不可能忽视世界上所有的 Windows 95/98/NT 和 Mac OS 系统。为了让这些人能够使用真正的操作系统工作，他们需要某种从远程站点登录的机制。而且由于 Telnet 不安全，SSH 为我们提供了解决方案。

值得庆幸的是，Data Fellows 并不是唯一为非 UNIX 操作系统制作 SSH 客户端的组织。以下是几个 SSH 客户端的简要列表：

- NiftyTelnet，适用于 Mac OS

  - http://www.Lysator.liu.se/~jonroyd/freeware/niftyssh/

  - 由于 RSA 算法的专利法，无法在美国合法运行。（参见本章稍后的“使用 RSAREF”部分。）

- MindTerm（多平台）

  - http://www.mindbright.com/mindterm

  - 完全使用 Java 编写，适用于许多 UNIX 平台（包括 Linux）以及 Windows 和 Mac OS。有关已测试操作系统的完整列表，请参阅网页。

- TeraTerm SSH，适用于 Windows

  - http://www.zip.co.m.au/~roca/ttssh.html

  - 此包是 TeraTerm 终端模拟器的 DLL。DLL 和主包均免费。

- FreeSSH，适用于 Windows

  - http://akson.sgh.wav.pl/~chopin/sssh/index_en.html

  - 一个简单的 SSH 客户端，在 16 位和 32 位 Windows 下均可运行（对于那些尚未准备好放弃 Windows 3.11 的人来说很方便）。

- SecureCRT，适用于 Windows

  - http://www.vandyke.com/products/SecureCRT/

  - SSH 的商业实现。

- PilotSSH，适用于 PalmPilot

  - http://www.isaac.cs.berkeley.edu/~pilot/

  - 如果你必须从 PalmPilot 获得连接性，请使用此软件。

## 下载、编译和安装 SSH

如前所述，由于出口限制，Linux 发行版不包含 SSH。你必须从 http://www.ssh.fi/sshprotocol2 的 SSH 网站下载它。该包将以压缩的 .TAR 文件形式提供，命名类似于 `ssh-version-tar.gz`，其中 `version` 是你正在下载的 SSH 版本。截至今日发稿时，最新版本为 2.0.13。

除了 SSH 版本 2.x 的实现外，如果你希望为客户端提供 SSH 版本 1 的兼容性，你还希望下载最新的版本 1 实现 `1.2.27`。

下载 SSH 包后，将其移动到你希望进行编译的目录。就本章讨论而言，我们假设该目录是 `/usr/local/src`。包存储在 `/usr/local/src` 后，使用以下命令解包它：

```
[root@fund src]$ tar -xvzf ssh-2.0.13.tar.gz
```

这将把整个源代码解包到 `/usr/local/src/ssh-2.0.13` 目录中。

如果你正在安装 SSH 版本 1 支持，请下载 `ssh-1.2.27.tar.gz`，将其移动到 `/usr/local/src` 目录，并使用此命令解包它：

```
[root@fund src]$ tar -xvzf ssh-1.2.27.tar.gz
```

如果你需要 SSH 版本 1 支持，请继续阅读关于编译版本 1 的以下部分；否则，你可以跳到关于编译版本 2 的部分。

## 编译 SSH 版本 1

影响 SSH 版本 1 行为的多个选项需要在编译时设置。这些选项作为 `./configure` 程序的命令行参数提供，并在表 17-1 中进行了描述。

让我们看一个例子：要配置 SSH1 使用 TcpWrappers 库 `/usr/lib/libwrap.a`，我们需要输入此命令：

```
[root@src ssh-1.2.27]# ./configure --libwrap=/usr/lib/libwrap.a
```

要编译和安装，请依次执行 `make` 和 `make install` 命令如下：

```
[root@src ssh-1.2.27]# make; make install
```

| 选项 | 描述 |
| :--- | :--- |
| `--with-none` | 允许未加密的连接（如果用户请求）。 |
| `--with-secureid=PATH` | 启用对 SecureID 卡的支持。对于 `PATH`，输入 SecureID 软件的路径。 |
| `--with-tls=PATH` | 启用对 TIS 的支持。对于 `PATH`，输入 TIS 软件所在目录。 |
| `--with-libwraps=PATH` | 启用 TcpWrappers 支持。对于 `PATH`，输入处理 TcpWrappers 的库（通常是 `/usr/lib/libwrap.a`）。 |
| `--with-ssocks` | 启用 SOCKS 防火墙支持。 |
| `--with-ssocks5=PATH` | 启用 SOCKS5 防火墙支持，其中 `PATH` 是 SOCKS5 库的位置。 |
| `--with-rserf=PATH` | 如果你在美国使用此 SSH 包，你必须使用 RSAREF 库进行编译，以避免侵犯 RSA Security 的专利。（默认使用标准的 RSA 算法。）对于 `PATH`，输入 `rserf.a` 文件所在的目录。（注意，你需要自己编译此库。） |

表 17-1. SSH 版本 1 的配置选项

# 第 17 章：安全外壳协议（SSH）

### 使用 RSAREF

RSA 是 SSH1 用于执行公钥交换的算法。不幸的是，该算法在美国拥有专利，因此未经授权的使用者必须向软件开发者支付版税。该算法的一个功能较弱的版本已对公众开放，称为 RSAREF。这种替代方案可以在免费软件中合法使用，而无需支付版税。SSH1 可以使用 RSAREF2 来替代实际的 RSA 算法。

> **警告：** 如果你在美国境内使用 SSH1，请务必在 http://ftp.funet.fi/pub/cryptocryptography/assmencrypt/rarsaref2.tar.gz 下载 RSAREF2 库。如果你不在美国，请务必使用默认的 RSA 算法。（这些专利会让你疯掉！）将 RSAREF2 文件移动到你想要编译的位置。在本讨论中，我们假设该位置为 `/usr/local/src`。使用以下命令解包归档文件：

```bash
[root@ford src]# tar -xvf rsaref2.tar.gz
```

这将创建一个名为 `rsaref2` 的目录。切换到 `/usr/local/src/rsaref2/install/unix` 目录并运行 `make`，如下所示：

```bash
[root@ford src]# cd /usr/local/src/rsaref2/install/unix; make
```

当你返回到命令提示符时，当前目录中会有一个名为 `rsaref.a` 的文件。将此文件复制到 `/usr/lib` 并将权限设置为 644，如下所示：

```bash
[root@ford unix]# cp rsaref.a /usr/lib/; chmod 644 /usr/lib/rsaref.a
```

这就完成了 RSAREF 的安装。若要将其作为 SSH1 `.configure` 命令行的一部分使用，请确保包含此命令行参数：

```
-rsaref=/usr/lib/rsaref.a
```

### 编译 SSH 版本 2
