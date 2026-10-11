
### 40.1.2.2 通过 Subversion 访问

你还可以通过普通的 Subversion 客户端访问源代码。这使你对仓库的操作拥有更多的控制权，允许你签出完整的源代码树，并通过常规的 Subversion 命令使其保持最新。如果你是开发人员而不仅仅是随意浏览者，这是首选的访问方式。

为了能够从 Subversion 下载 Samba 源代码，你需要一个 Subversion 客户端。你的发行版可能已包含该客户端，或者你可以从 [http://subversion.tigris.org/](http://subversion.tigris.org/) 下载源代码。

要通过匿名 Subversion 获取访问权限，请遵循以下步骤。

#### 使用 SUBVERSION 获取 SAMBA

- 1. 安装最新版本的 Subversion。你真正需要的只是一个 Subversion 客户端二进制文件的副本。
- 2. 运行以下命令：

```bash
svn co svn://svnanon.samba.org/samba/trunk samba
```

这将创建一个名为 **samba** 的目录，其中包含最新的 Samba 源代码（通常是指下一个主要发布的分支）。目前对应的是 3.1 开发树。可以通过在签出的 URL 中添加 **branches/BRANCH_NAME** 来获取 trunk 以外的 Subversion 分支。分支名称列表可以在 Samba 网站上的“Development”页面找到。一个常见的请求是获取最新的 3.0 发布代码。可以使用以下命令完成：

```bash
svn co svn://svnanon.samba.org/samba/branches/SAMBA_3_0 samba_3
```

- 3. 每当你想合并最新的代码更改时，请在 Samba 目录内使用以下命令：

```bash
svn update
```

## 40.2 通过 rsync 和 ftp 访问 Samba 源代码

**pserver.samba.org** 还在 Samba pserver[^3] 位置导出 Subversion 树的大部分解包副本，并且还可以通过 Samba rsync[^4] 服务器位置使用匿名 rsync。我建议优先使用 rsync 而不是 ftp，因为 rsync 能够压缩数据流，而且它比 FTP 更有用，因为在部分更新期间，它只会传输缺失的数据加上少量开销。有关 rsync 的更多信息，请参阅 rsync 主页[^5]。

解包树的缺点是不像 Subversion 那样支持自动合并本地更改。**rsync 访问**对于初始安装最为方便。

[^3]: [http://pserver.samba.org/pub/unpacked/](http://pserver.samba.org/pub/unpacked/)
[^4]: `rsync://pserver.samba.org/ftp/unpacked/`
[^5]: *(链接至 rsync 主页)*

## 40.3 验证 Samba 的 PGP 签名

强烈建议你在安装任何源文件之前验证其 PGP 签名。即使你不是从镜像站点下载，验证 PGP 签名也应成为一种标准反射。如今，许多人使用 **GNU GPG** 工具集来代替 PGP。**GPG** 可以替代 PGP。

话虽如此，请继续下载以下文件：

```bash
$ wget http://us1.samba.org/samba/ftp/samba-3.0.20.tar.asc
$ wget http://us1.samba.org/samba/ftp/samba-pubkey.asc
```

第一个文件是 Samba 源文件的 PGP 签名；另一个文件是 Samba 公共 PGP 密钥本身。使用以下命令导入公共 PGP 密钥：

```bash
$ gpg --import samba-pubkey.asc
```

并使用以下命令验证 Samba 源代码的完整性：

```bash
$ gzip -d samba-3.0.20.tar.gz
$ gpg --verify samba-3.0.20.tar.asc
```

如果你收到类似“**Good signature from Samba Distribution Verification Key...**”（来自 Samba 发行版验证密钥的良好签名...）的消息，那么一切正常。关于信任关系的警告可以忽略。你不希望看到的示例如下：

```bash
gpg: BAD signature from Samba Distribution Verification Key
```

## 40.4 构建二进制文件

解压源 tarball 包后，下一步涉及配置，以使 Samba 适应你的操作系统平台。如果你的源目录不包含 **configure 脚本**，你需要先构建该脚本才能继续。构建 configure 脚本需要正确版本的 autoconf 工具包。如果存在所需版本的 autoconf，可以通过执行以下命令生成 configure 脚本：

```bash
root# cd samba-3.0.20
root# ./autogen.sh
```

要构建二进制文件，请在源目录中运行 `./configure` 程序。这应该会自动为 Samba 配置你的操作系统。如果你有特殊需求，可能希望先运行：

```bash
root# ./configure --help
```

这将帮助你查看可以启用哪些特殊选项。现在，使用 `./configure` 及其可能需要的任何参数执行：

```bash
root# ./configure [ ... arguments ... ]
```

执行以下命令以创建二进制文件：

```bash
root# make
```

一旦成功编译，你可以执行此处显示的命令来安装二进制文件和手册页：

```bash
root# make install
```

有些人喜欢单独安装二进制文件和手册页。如果这是你的愿望，可以通过执行以下命令安装二进制文件：

```bash
root# make installbin
```

手册页可以使用以下命令安装：

```bash
root# make installman
```

请注意，如果你正在从旧版本的 Samba 升级，旧版本的二进制文件将被重命名，并带有“old”扩展名。你可以通过执行以下命令回退到以前的版本：

```bash
root# make revert
```

正如你所见，构建和安装 Samba 并不一定会导致灾难！

### 40.4.1 编译支持 Active Directory 的 Samba

为了编译支持 ADS 的 Samba，你需要在系统上安装：

- MIT 或 Heimdal Kerberos 开发库（可以从源代码安装或使用软件包）。
- OpenLDAP 开发库。

如果你的 Kerberos 库位于非标准位置，请记住添加 configure 选项 `--with-krb5=DIR`。

运行 configure 后，确保它生成的 `include/config.h` 包含如下行：

```c
#define HAVE_KRB5 1
#define HAVE_LDAP 1
```

如果没有，则说明 configure 未找到你的 KRB5 库或 LDAP 库。查看 `config.log` 以找出原因并修复它。

#### 40.4.1.1 在 Debian 上安装所需的软件包

在 Debian 上，你需要安装以下软件包：

- libkrb5-dev
- krb5-user

#### 40.4.1.2 在 Red Hat Linux 上安装所需的软件包

在 Red Hat Linux 上，这意味着你至少应该有：

- krb5-workstation（用于 kinit）
- krb5-libs（用于链接）
- krb5-devel（因为你正在从源代码编译）

此外还需要标准的开发环境。

如果你的系统上没有安装这些文件，你应该检查安装光盘以找到哪个光盘包含它们，并使用你选择的工具安装这些文件。如果不确定使用什么工具，请参阅 Red Hat Linux 文档。

#### 40.4.1.3 SuSE Linux 软件包需求

SuSE Linux 安装 Heimdal 软件包，这可能使你能够构建二进制软件包所必需。你应该验证开发库是否已在系统上安装。

SuSE Linux Samba RPM 支持 Kerberos。请参阅你的 SuSE Linux 系统的文档以获取有关 SuSE Linux 特定配置的信息。此外，SuSE 在维护提供最大可用功能的 Samba 软件包方面非常活跃。你应该考虑使用可用的 SuSE 提供的软件包。

## 40.5 启动 smbd、nmbd 和 winbindd

你必须选择将 smbd、winbindd 和 nmbd 作为守护进程启动，或者从 inetd 启动。不要试图两者都做！你可以将它们放入 `inetd.conf` 中，由 inetd 或 xinetd 按需启动，或者作为守护进程从命令行或 `/etc/rc.local` 中启动。有关命令行选项的详细信息，请参阅手册页。特别注意阅读关于启动 Samba 所需用户的说明。在许多情况下，你必须以 root 身份启动。

使用推荐的守护进程方式启动 smbd 和 nmbd 的主要优点是，它们对初始连接请求的响应会稍快一些。

### 40.5.1 从 inetd.conf 启动

> **注意**：如果你使用 NIS、NIS+ 或 LDAP 分发服务映射，以下情况将会不同。

查看 `/etc/services`。在端口 139/tcp 上定义了什么？如果没有定义，则添加如下行：

```
netbios-ssn      139/tcp
```

同样，对于 137/udp，你应该有如下条目：

```
netbios-ns   137/udp
```

接下来，编辑你的 `/etc/inetd.conf` 并添加两行如下内容：

```
netbios-ssn stream tcp nowait root /usr/local/samba/bin/smbd smbd
```

