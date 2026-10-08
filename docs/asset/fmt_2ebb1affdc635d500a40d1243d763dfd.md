
## 更多文档

有关更多关于 `ipsec` 的信息，请查看 `man ipsec`：

- `ipsec` - 调用 IPSec 工具。
- `add` - 将地址转换为 ASCII。
- `set` - ASCII、子网或范围。
- `bytos` - 将二进制数据转换为 ASCII。
- `deatas` - 将数据转换为 ASCII。
- `toda` - 将 IPSec 安全关联 ID 转换为 ASCII。
- `subnet` - 将子网/转换为 ASCII。
- `utos` - 将虚拟密钥转换为 ASCII。
- `auto` - 自动密钥的 IPSec 连接。
- `bar` - 输出 IPSec 调试信息。
- `bitmap` - 将计数转换为子网掩码。
- `route` - 管理 IPSec 路由表。
- `goodmask` - 子网掩码是否有效？
- `host` - 给 IP 地址和子网掩码返回主机。
- `klpsdebug` - 显示调试信息。
- `look` - 使虚拟密钥 IPSec 连接启动或关闭。
- `maksbits` - 将子网掩码转换为计数。
- `optionfrm` - 从文件读取命令行选项。
- `puto` - IPSec 密钥守护进程。
- `rambits` - 生成 ASCII 形式的随机位。
- `range` - 将 IP 地址范围转换为 ASCII。
- `setup` - 生成 RSA 签名密钥。
- `spi` - 管理 IPSec 子系统。
- `security` - 分组 IPSec 安全关联。
- `subsetno` - 给 IP 地址和子网掩码返回子网号。
- `tcfg` - 将 IPSec 虚拟接口与真实接口关联。
- `whack` - IPSec 密钥守护进程的控制接口。
- `conf` - IPSec 配置和连接。
- `secrets` - 用于 IKE/IPSec 认证的密钥。

# 第 14 章

## GnuPG

本章内容

- 1. 编译 - 优化与安装 GnuPG
- 2. 在 Linux 终端中使用 GnuPG

# Linux GnuPG
第 4 章

### 摘要

此时，我们已经准备好在 Linux 服务器上进行软件的编译、配置、优化和安装。是的，是时候了，我们将从强大且易于安装的 GnuPG 工具开始我们的冒险。我们为什么选择从 GnuPG 开始？答案很简单，我们正在操作一台高安全的服务器，而每次当我们想在安全机器上安装某些新软件时，采取的首要任务就是确保相关软件来自可信源并创建数字签名。通过 GnuPG 工具，我们可以验证提供的源码并确保软件未被修改。因此，建议在安装任何其他程序之前安装此程序。

数据源加密是一项无价的功能，为我们的工作提供了高程度的机密性。像 GnuPG 这样的工具远不止是加密电子邮件。它可以用于各种数据加密，其应用仅限于想象力。

GnuPG 是 GNU 用于安全数据管理和存储的工具。它可以用于加密数据，并符合 RFC2440 中描述的建议 OpenPGPG 网络标准。它包含高级的密钥管理设施，并符合 RFC2440 中描述的建议 OpenPGPG 网络标准。由于 GnuPG 没有使用任何专利算法，它与 PGP2 版本不兼容。

# 这些安装说明假设

- 命令兼容 Unix。
- 源码路径为 `/var/tmp`（注意，可以根据个人意愿选择其他路径）。
- 安装已在 OpenNA Linux 和 Red Hat Linux 7.3 上测试过。
- 安装中的所有步骤将使用超级用户账户 "`root`" 执行。
- 是否需要重新编译内核：否。
- 最新 GnuPG 版本为 1.0.7

本章给出的步骤可能适用于所有 Linux 平台，但我们仅在 OpenNA Linux 和 Red Hat Linux 上进行过测试。

# 包

请定期检查 `http://www.gnupg.org/` 以获取最新状态。我们选择从源码安装，是因为它提供了调整安装的功能。

源码可以从此处获取：
GnuPG 主页：`http://www.gnupg.org/`
GnuPG FTP 站点：`217.69.76.44`

你必须确保下载：`gnupg-1.0.7.tar.gz`

## 前提条件

GnuPG 要求系统中预先安装列出的软件才能成功编译。如果情况并非如此，你必须从你的 Linux CD-ROM 或源码归档文件中安装。请确保在继续阅读本章之前，你的机器已安装了此程序。

- 在系统上运行 GnuPG 需要 `gettext`。
- 在系统上运行 GnuPG 需要 `python-1.5`。
- 在系统上运行 GnuPG 需要 `expat`。
- 在系统上运行 GnuPG 需要 `gmp`。

## 原始源码

如果你不使用 RPM 包来安装此程序，那么将来你想要更新该包时，将很难找到系统上安装的所有文件。为了解决这个问题，一个好的主意是在安装 GnuPG 之前对系统文件列出一个列表，然后在安装之后再列一个，并使用 `diff` 对它们进行比较，以找出 GnuPG 文件被放置的位置。

- 在安装软件之前，简单地运行以下命令：
```
[root@deep]# find /* > GnuPG1
```
- 在安装软件后，运行以下命令：
```
[root@deep]# find / > GnuPG2
```
- 然后使用以下命令获取更改内容的列表：
```
[root@deep]# diff GnuPG1 GnuPG2 > GnuPG-Installed
```

通过此程序，如果发生任何升级，你只需要读取程序生成的添加或更改的文件列表，并在安装新软件之前手动从你的系统中删除它们即可。在上面的示例中，我们使用系统的 `/root` 目录来存储所有生成的文件列表。

# 编译 - 优化与安装 GnuPG

## 第 1 步

一旦你从主软件网站获取了程序，你必须将其复制到 `/var/tmp` 目录并在切换到该位置之前执行解包。

- 可以可以通过命令完成：
```
[root@deep]# cp gnupg-version.tar.gz /var/tmp/
[root@deep]# cd /var/tmp/
[root@deep]# tar xzf gnupg-version.tar.gz
```

### 第 2 步

为了检查你将安装的 GnuPG 版本是原始且未修改的，请使用下面描述的命令并检查提供的签名。由于我们系统中尚未安装 GnuPG，我们必须验证程序的 MD5 校验和。

- 要验证 GnuPG 的 MD5 校验和，使用命令：
```
[root@deep]# md5sum gnupg-version.tar.gz
```

这应该产生类似的输出：
```
d8b36d4fd2d23a1027b1877acbc897 gnupg-1.0.7.tar.gz
```

现在检查这个新创建的文件是否与 `http://www.gnupg.org/download/` 发布的一。

### 第 3 步

接下来，进入新创建的目录并执行以下步骤来配置和优化系统。

- 进入新创建的目录，使用：
```
[root@deep]# cd gnupg-version/
```

- 配置并优化你的系统，使用以下行：
```
[root@deep]# export CFLAGS="-O2 -march=i86 --prefix=/usr --mandir=/usr/share/man --infodir=/usr/share/info --enable-shared --disable-ls"
```

### 第 4 步

现在，我们在安装 GnuPG 之前对系统文件列出一个列表，然后在之后使用 `diff` 对它们进行比较，以找出 GnuPG 文件被放置的位置。

```
[root@deep]# find /* > GnuPG1
[root@deep]# find / > GnuPG2
[root@deep]# diff GnuPG1 GnuPG2 > GnuPG-Installed
```

### 第 5 步

一旦完成 GnuPG 的配置、优化和安装，我们可以删除程序包和源码目录来释放空间。

- 删除 GnuPG 及其目录使用以下命令：
```
[root@deep]# cd /var/tmp/
[root@deep]# rm -rf gnupg-version/
[root@deep]# rm -f gnupg-version.tar.gz
```

# 在 Linux 终端中使用 GnuPG

在这里我们展示如何使用终端通过 GnuPG 管理 GPG 密钥。列出的命令是我们经常使用的，但也有很多。更多信息请查阅帮助页 `gpg (1)`。

创建密钥对：

如果这是第一次使用 GnuPG 软件，我们必须创建一个新的密钥对（公钥和私钥）以便使用其加密功能。

## 第 1 步

GnuPG 的 `--gen-key` 用于生成新的（公钥和私钥）密钥，每当我们需要在系统上创建新的 GnuPG 密钥时都要使用它。当我们第一次执行此命令时，GnuPG 将为我们创建所需的目录和配置文件。

- 创建新的密钥对，使用以下命令：
```
[root@deep]# gpg --gen-key
```

## GnuPG |1
## 第 4 章

### 步骤 2
命令执行后，我们需要再次运行它来创建公钥和私钥，因为在第一次使用时，它会我们创建所需的目录和选项。然后，它将创建密钥。

- 我们使用相同的命令启动 GnuPG：
```
[root@]# gpg --gen-key
```
```
gpg (GnuPG) 1.0.7 - Copyright (C) 2002 Free Software Foundation, Inc.
本程序没有任何保证。这是一个免费软件，欢迎在符合条件的情况下重新分发。详情请参阅 COPYING 文件。
gpg: keyring='//root/.gnupg/secring.gpg' created
gpg: keyring='//root/.gnupg/pubring.gpg' created
请选择您想要的密钥类型：
(1) DSA 和 ElGamal (默认)
(2) RSA (仅签名)
(4) ElGamal (签名和加密)
(5) RSA (仅签名)
selection: 1

DSA 密钥对将具有 1024 位。
要生成新的 EL-E 密钥对：
最小密钥长度为 768 位
默认密钥大小为 1024 位
建议的最大大小为 2048 位
您想要什么密钥大小？(按回车)
请求密钥大小为 1024 位
请指定密钥的有效期。
0 = 密钥永不过
<n> = 密钥在 n 天后过期
<w> = 密钥在 w 周后过期
<m> = 密钥在 m 个月后过期
<y> = 密钥在 y 年后过期
有效期?(y) 按回车
密钥永不过
这正确吗？(y/n)

您需要一个用户 ID 来标识您的密钥；软件将根据
真实姓名、注释和电子邮件地址构造如下格式：
"Heinrich Heine (Der Richter) <heinrichh@duesseldorf.de>"

真实姓名：Gerard Mourani
电子邮件：gmourani@openapi.com
注释：按回车
您选择了此用户 ID：
"Gerard Mourani <gmourani@openapi.com>"

更改 (N)、(C) 注释、(E) 邮件或 (O)/(Q) 退出? O
您需要一个密码短来保护您的私钥。

输入密码短：mpass
重复密码短：mpass

我们需要生成大量的随机字节。在生成质数期间，执行一些操作（在键盘上打字、移动鼠标、使用磁盘）是一个好主意；这让随机数生成器更有机会获得足够的熵。
........................................................................
......................................................................................................................................................
......

```

<+++++.>.+.......<+.....+

      .+++++++

公私钥已创建并已签名。

```

注意：由于我们是以 "`root`" 运行此 GnuPG 命令，在 "`root`" 家目录 `~/root` 下的 `.gnupg` 子目录下创建一个新的密钥对（私钥和公钥）。如果您在系统的其他用户下运行上述命令，生成的密钥将位于服务器上其家目录下。

## 为用户导出 GPG 密钥：

一旦创建了密钥对，您就可以通过在全球分发您的公钥来扩展您的视野（永远不要导出您的私钥）。这可以通过发布到主页、通过互联网上可用的密钥服务器或任何可用方法来实现。GnuPG 有实用的选项帮助您发布公钥。

### 步骤 1

首先，我们必须提取公钥的 ASCII 文本以进行分发。ASCII 文本是一种安全的格式，因为它允许人们轻松地获取。这样，当他们想与您通信时，您只需要剪并粘贴您的公钥即可。

- 要以 ASCII 封装输出导出您的密钥，请使用以下命令：
```
[root@deep #] gpg --export -ao UID
```

例如：
```
[root@deep #] gpg --export -ao Gerhard Mourani
```

`"--export"` 用于通过发布您的加密文件来导出公钥，`"a"` 用于创建 ASCII 封装输出，您可以将其通过邮件、发布或放置在网页上，`"o"` 用于将结果放入文件中，`UID` 代表您想要导出的用户，在我们的示例中，就是我们之前创建的 `"Gerhard Mourani"` 密钥。

### 步骤 2

一旦提取了密钥，生成的输出将在您执行上述命令的目录下创建一个名为 `"Gerhard"` 的文件，打印出要提取的用户密钥的名。在我们的示例中，该文件名为 `"Gerhard"`，因为这是我们想要以 ASCII 格式导出的密钥名称。注意，您的公钥 ASCII 格式密钥的名称将会不同。

- 以 ASCII 封装输出格式编辑您的密钥并分发：
```
[root@deep #] vi Gerhard
-----BEGIN PUBLIC KEY BLOCK-----
Version: GnuPG v1.0.7 (Linux)
Comment: 更多信息请访问 http://www.gnupg.org

```

mG1bGZnQQCRBAQ+1NJFCMYtcJ51hMTNFEHEQY82Dbv0QMCkDI1J90T5V

G3WtG3R4A30MnWTuN2II8BQ9R3S3FEGBAWiaYjushhkhk

```
<+++++.>.+.......<+.....+
      .+++++++
公私钥已创建并已签名。
```
