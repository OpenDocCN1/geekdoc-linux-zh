

如果您急于获取证书以开始测试，或者有其他原因需要快速获取临时证书，请咨询您的 CA。他们可能提供某种方式来为您发放临时、不受信任的证书。例如，Thawte 允许您通过 Web 提交 CSR 以获取临时证书，您将在几分钟内通过电子邮件收到该证书。

从商业 CA 获取服务器证书后，您可以按照其说明安装证书文件。这一步通常相当简单。您可能会被要求将文件复制到某个目录并重启服务器。

如果您对获取来自商业 CA 的签名证书不感兴趣，您可以创建自己的 CA，并随时对服务器或用户等实体进行认证。我将在以下章节中向您展示操作方法。

## 创建私有证书颁发机构

如前所述，私有自签名证书不适合用于 Internet 场景，因为广大用户不应信任此类证书。然而，如果您希望向各部门颁发内部、全公司范围的证书，又不想经历第三方商业 CA 验证的麻烦，您必须使用私有 CA。

**注意**

您可能能够从商业 CA 获得您私有 CA 的交叉签名证书。在这种情况下，您的私有 CA 将与商业 CA 链接，因此每个人都应该信任您签发的任何证书。但是，商业 CA 可能会限制您的证书颁发权限，使其仅限于您自己的组织，以确保您不与 CA 竞争。

请遵循以下步骤，使用 OpenSSL 创建私有自认证 CA：

1.  从 OpenSSL 网站的用户贡献软件部分（`www.openssl.org/contrib`）下载 `ssl.ca-version.tar.gz` 脚本发行版的最新版本。将此文件解压到您选择的目录中。将创建一个名为 `ssl.ca-version` 的子目录。您将在目录中找到一组 `sh` 脚本。
2.  运行 `new-root-ca.sh` 脚本为您的私有 CA 创建自签名根证书。系统将提示您输入密码短语。此密码短语对于签署未来的证书是必需的。
3.  要创建服务器证书，运行 `new-server-cert.sh www.domain.com` 脚本来创建服务器的私钥和公钥。系统将提示您输入新服务器证书的区分名域。该脚本还将生成一个 CSR，如果您愿意，之后可以将其发送给商业 CA。
4.  运行 `sign-server-cert.sh` 脚本批准并签署您使用 `new-server-cert.sh` 脚本创建的服务器证书。
5.  运行 `new-user-cert.sh` 脚本创建用户证书。当由商业证书颁发机构签署时，用户证书可以与 Web 浏览器一起用于向远程服务认证用户。然而，由于对它们的理解不足以及可用的客户端和服务器软件缺乏，用户证书并不常见。
6.  运行 `sign-user-cert.sh` 脚本签署用户证书。此外，运行 `p12.sh` 脚本将私钥、签名密钥和 CA 的公钥打包到扩展名为 `.p12` 的文件中。然后可以将此文件导入到电子邮件客户端等应用程序中使用。

现在，您已准备好在各种应用程序中使用 OpenSSL。OpenSSL 是安全的重要组成部分。您越是使用 OpenSSL，就会越发发现将其集成到许多服务中很容易。

## 访问 SSL 页面

如果您在 `/usr/local/apache` 目录中安装了 Apache，请运行 `/usr/local/apache/bin/httpsdctl start` 命令以启动启用了 SSL 的 Apache 服务器。如果收到错误消息，请检查日志文件以获取详细信息。`httpd.conf` 文件中的拼写错误或路径缺失是常见错误原因，因此请留意这些情况。服务器启动后，您可以使用 HTTPS 协议访问它。例如，要访问名为 `shea.evoknow.com` 的启用 SSL 的 Apache 服务器，我可以将 Web 浏览器指向 `https://shea.evoknow.com`。如果您使用的是测试证书或自有 CA 签发的证书，Web 浏览器将显示一条警告消息，指出证书无法验证。这是正常的，因为没有已知的 CA 签署该证书。您应该接受该证书并浏览您启用了 SSL 的网站。

✦ ✦ ✦

## 在 Windows 上运行 Apache

Windows 平台上的 Apache 2 比以往任何时候都更加稳定。这一部分专门介绍 Windows 平台上的 Apache。我将向您展示如何在 Windows 平台上安装和配置 Apache，以及如何使用仅有的几个 Windows 专属 Apache 指令。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_597_0.png)

### 本部分包含内容

- **第 20 章** 在 Windows 上安装和运行 Apache
- **第 21 章** 为 Windows 配置 Apache

![](img/e11fcbd2818a3495ac70085e5d8d1c26_599_0.png)

## 在 Windows 上安装和运行 Apache

### 本章内容

- 在 Windows 上运行 Apache 的系统要求
- 在 Windows 上安装 Apache
- 启动、停止和重启 Apache

尽管 Apache 很久以前就被移植到了 Windows 平台，但 **Apache 2.0** 是第一个能够利用原生 Windows 系统调用的版本。所有之前版本的 Apache 都使用了 POSIX 抽象层，这在 Windows 上运行 Apache 时会降低性能。现在，Apache 终于可以与其他原生 Web 服务器（如 Microsoft IIS 和 Netscape Enterprise 服务器）进行正面竞争了。

在本章中，您将了解在 Windows XP、Windows 2000、Windows NT 和 Windows 9x/ME 等流行 Windows 平台下运行 Apache 的系统要求；您还将学习如何安装 Apache 并进行配置，以便您可以快速启动运行。

### 系统要求

Apache 要求您的 Windows 系统启用 **TCP/IP**。您应该确保为您的 Windows 平台安装了最新的 **TCP/IP 堆栈**（*Winsock*）。启用了 TCP/IP 的 Windows 2000 用户可以在没有其他 Windows 特定要求的情况下安装 Apache。Windows NT 4.0 用户应确保已安装最新的服务包。

Windows 2000 Advanced Server 是运行生产级 Apache Web 服务器的理想平台。Windows 2000 Advanced Server 针对网络服务进行了优化，因此它应该能为 Apache 以及其它 Internet 服务带来最佳性能。

> 注意
>
> 我使用 Windows 2000 Advanced Server 作为本书中 Windows 特定章节的 Windows 平台。

您还需要 Microsoft Installer 版本 1.10 或更高版本来安装 Apache。Windows 2000 和 Windows ME 都内置了 Microsoft Installer。对于其他版本的 Windows，您需要查阅手册或访问 Microsoft 网站以获取详细信息。

### 下载 Windows 版 Apache

Windows 版 Apache 可以以源代码发行版或二进制发行版的形式下载。不幸的是，与大多数 Unix 平台不同，Windows 并不附带开发功能，例如像 GCC 这样的标准 C 编译器。因此，实际上只有拥有 Microsoft Visual Studio 等开发工具的 Windows 开发人员才能编译 Apache。对于大多数人来说，二进制发行版是唯一可行的下载选项。虽然 gcc 在 Windows 上可用，但 Apache 源代码无法使用 Windows 版本的 gcc 编译。

Windows 版 Apache 二进制文件的官方下载站点是 `http://httpd.apache.org/dist/httpd/binaries/win32/`。二进制发行版的命名为 `httpd_version-win32-no_src-rrumber.msi`（例如，`httpd_2_0_16-win32-no_src-r1.msi`）。源代码发行版的命名为 `httpd_version-win32-wint_src.msi`。请下载最新、稳定的二进制发行版。

> 注意
>
> 如果您是一位计划下载并编译 Apache 源代码发行版的 Windows 开发人员，则可以下载源代码发行版的 zip 版本，而不是 _msi 安装程序版本。您将需要解压缩程序（例如 PKWARE 的 PKUNZIP 或 WinZip）来提取源文件，这些源文件具有 MS-DOS 行尾。不要下载以 .tar.gz 或 .tar.Z 结尾的源代码发行版，因为它们是 Unix 软件包，其行尾仅适用于 Unix 平台。

### 安装 Apache 二进制文件

双击下载的 `httpd_version-win32-no_src.msi` 文件将启动 Microsoft Installer 和 Apache 安装程序。单击“下一步”以开始安装。系统会提出一系列问题，下面将对此进行讨论。

- 阅读并接受图 20-1 中显示的许可协议。

您必须点击标记为“I accept the terms in the license agreement”的单选按钮以启用“下一步”按钮。单击“下一步”继续到下一个屏幕。

