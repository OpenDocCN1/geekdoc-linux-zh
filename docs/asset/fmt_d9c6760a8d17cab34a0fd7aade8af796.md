
测试此问题的一种方法是使用 `mount /dev/cdrom /media` 命令挂载 RHEL 6 DVD。接下来，在 `Packages/` 子目录中找到所注明的 `policycoreutils-gui` 软件包。或者，您可以使用 `yumdownloader policycoreutils-gui` 命令直接从 Red Hat Network 或配置的软件仓库下载该软件包。本章后面将讨论这些和其他 `yum` 命令。请注意，一些 Linux GUI 桌面环境会自动挂载插入相关驱动器的 CD/DVD 介质。如果是这样，您将在 `mount` 命令的输出中看到挂载目录。

当显示依赖项消息时，`rpm` 不会安装给定的软件包。请注意依赖项消息。首先，它需要相同版本号的 `policycoreutils-python` 软件包，以及一个定义较少的 `setools-console` 软件包。

## 工作中

当然，您可以使用 `--force` 选项让 `rpm` 忽略依赖项，但这可能会导致其他问题，除非您尽快安装这些依赖项。最佳选择是使用本章后面描述的适当的 `yum` 命令。在这种情况下，`yum install policycoreutils-gui` 命令将自动安装其他依赖的 RPM。

如果依赖项没有阻止您，有三个基本命令可以安装 RPM 软件包：

```
# rpm -i packagename
```

```
# rpm -U packagename
```

```
# rpm -F packagename
```

`rpm -i` 选项在软件包尚未安装时安装软件包。`rpm -U` 选项升级任何现有软件包，或在未安装较早版本时安装它。

`rpm -F` 选项仅升级现有软件包。如果软件包之前未安装，则不会安装它。

我喜欢在 `rpm` 命令中添加 `-vh` 选项。这些选项添加详细模式并使用哈希标记，有助于监控安装进度。因此，当我使用 `rpm` 安装软件包时，我运行以下命令：

```
# rpm -ivh packagename
```

还有一件事与设计良好的 RPM 软件包相关。当使用 `rpm` 命令解包时，它会检查是否会覆盖任何配置文件。`rpm` 命令尝试在这种情况下做出智能决策。如前所述，如果 `rpm` 命令选择替换现有配置文件，它会提供（在大多数情况下）类似的警告：

```
# rpm -i penguin-3.26.i386.rpm
warning: /etc/someconfig.conf saved as /etc/someconfig.conf.rpmsave
```

当使用 `-e` 开关删除软件包时，`rpm` 命令通常以相同的方式工作。如果配置文件已被更改，它也会在同一目录中以 `.rpmsave` 扩展名保存。

由您来查看这两个文件并确定是否需要进行修改。当然，并非每个 RPM 软件包都是完美的，存在此类更新会覆盖关键自定义配置文件的风险。在这种情况下，备份很重要。

通常，升级软件包的 `rpm` 命令仅在要安装的软件包为较新版本时才有效。有时，较旧版本的软件包是可取的。只要旧软件包没有安全问题，更多的管理员可能熟悉稍旧的版本。新软件包中可能存在问题的错误可能不存在于该软件包的旧版本中。因此，如果您想使用 `rpm -i`、`-U` 或 `-F` 命令“降级”软件包，`--force` 开关可以帮助您。

> 如果您已经自定义了软件包并使用 `rpm` 升级了它，请转到保存的配置文件。将其作为指南来更改新配置文件的设置。但请记住，在升级过程中可能需要进行额外的更改。因此，您应该为每一个可想到的生产环境测试结果。

## 卸载 RPM 软件包

`rpm -e` 命令卸载软件包。但首先，RPM 会检查一些事项。它执行依赖检查，以确保没有其他软件包需要您尝试卸载的内容。如果发现依赖软件包，`rpm -e` 将失败，并显示错误消息标识这些软件包。

对于配置正确的 RPM，如果您修改了相关的配置文件，RPM 会复制该文件，在文件名末尾添加 `.rpmsave` 扩展名，然后删除原始文件。然后它可以继续卸载过程。过程完成后，它会从数据库中删除软件包名称。

> 请非常小心从系统中删除哪些软件包。与许多其他 Linux 实用程序一样，RPM 可能会默默地让您自食其果。例如，如果您删除包含 `/etc/passwd` 或内核的软件包，它可能会使系统无法使用。

## 从远程系统安装 RPM

使用 RPM 系统，您甚至可以以 URL 格式指定与 Internet 地址类似的软件包位置。例如，如果您想将 `rpm` 命令应用于

在 `ftp.rpmdownloads.com` FTP 服务器的 `/pub` 目录中，`foo.rpm` 软件包，你可以用如下命令安装该软件包：

```
# rpm -ivh ftp://ftp.rpmdownloads.com/pub/foo.rpm
```

假设你与该远程服务器有网络连接，此特定 `rpm` 命令会匿名登录到 FTP 服务器并下载文件。不幸的是，使用通配符尝试在包名中使用此命令会导致与“文件未找到”相关的错误信息。需要完整的包名，这可能会很麻烦。

如果你按照第 1 章和第 2 章的说明从 FTP 服务器安装了 RHEL 6，你可以替换相关的 URL 以及包的确切名称。例如，基于第 1 章中配置的 FTP 服务器和前面提到的 `policycoreutils-gui` 软件包，适当的命令将是：

```
# rpm -ivh ftp://192.168.122.1/pub/inst/policycoreutils-gui-2.0.83-19.1.el6.x86_64.rpm
```

如果 FTP 服务器需要用户名和密码，你可以按以下格式包含它们：`ftp://username:password@hostname:port/path/to/remote/package/file.rpm`，其中 `username` 和 `password` 是你登录该系统所需的用户名和密码，而 `port`，如果需要，指定远程 FTP 服务器上使用的非标准端口。FTP 的缺点之一是所有信息都以明文传输。当这些信息包含用户名和密码时，这可能是一个安全风险。出于此类原因，可能更喜欢匿名 FTP 服务器。

基于前面的示例，如果用户名是 `mjang` 密码是 `lla451MS`，你可以用以下命令直接从服务器安装 RPM：

```
# rpm -ivh ftp://mjang:lla451MS@192.168.122.1/pub/inst/policycoreutils-gui-2.0.83-19.1.el6.x86_64.rpm
```

此系统的关键是 `rpm` 命令。不幸的是，globbing 在此命令中不再起作用，至少在 RHEL 6 上测试时如此。因此需要安装包的确切名称。

## RPM 安装安全

安全可能是一个问题，特别是在通过互联网下载 RPM 软件包时。如果黑客 somehow 渗透 RHN，或许第三方仓库，你如何知道来自这些来源的软件包是真实的？关键是 GNU Privacy Guard（GPG）密钥，它是 Pretty Good Privacy（PGP）的开源实现。

如果你尚未导入或安装 GPG 密钥，在安装软件包时你可能会注意到类似以下的消息：

```
warning: vsftpd-2.2.2-6.el6.1686.rpm: Header V3 RSA/SHA256
Signature, key ID f21541eb: NOKEY
```

如果你关心安全，这个警告应该会引起警报。在 RHEL 6 安装过程中，GPG 密钥存储在 `/etc/pki/rpm-gpg` 目录中。查看此目录的内容。你会找到像 `RPM-GPG-KEY-redhat-release` 这样的文件。要实际使用密钥验证软件包，它必须被导入。而导入 GPG 密钥的命令相当简单：

```
# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
```
