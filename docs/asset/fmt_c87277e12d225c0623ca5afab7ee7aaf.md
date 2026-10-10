
### 运行 CTM

当您开始收到 CTM 更新时，可以使用 `ctm_mail` 软件包来解包并应用它们。您可以直接从 `/etc/aliases` 中的条目使用 `ctm_mail` 程序，如果您想以全自动化的方式运行。更多详情请查看 `ctm_mail` 手册。

> 注意：无论您使用什么方式获取 CTM 增量，您都应该订阅 `ctm-announce` (http://lists.FreeBSD.org/mailinfo/listinfo/ctm-announce) 列表。未来，这里将是发布 CTM 系统安排的唯一地方。点击上面的列表名称并按照说明进行订阅。

CTM 了解哪些文件经过过 gzip 压缩，因此你不需要先进行 gunzip，这可以节省磁盘空间。

除非感觉这涉及到整个过程，否则 CTM 不会动你的树。要验证增量（delta），你也可以使用 `-c` 标志，CTM 不会动你的树；它仅仅会验证增量的完整性，并查看它是否适用于你当前的树。

CTM 还有其他选项，请参阅手册页或查看源码以获取更多信息。

真的就这些。每当你获得新的增量时，运行 CTM 处理它以保持你的源码是最新的。

如果增量很难下载，请不要删除它们。你可能想保留它们，以防发生意外情况。即使你只有软盘，也可以使用 `fwrite` 制作一份副本。

## A.4.5 保留你的本地更改

作为开发者，你可能会对源码树中的更改文件进行实验。CTM 以一种修改的方式支持本地修改；在检查文件是否存在之前，它会查找 `foo.cm`。如果该文件存在，CTM 将对它进行操作而不是 `foo`。

这种行为是维护本地更改的一种简单方法：只需将你计划修改的文件复制为带有 `.cm` 后缀的相应文件名。然后你就可以自由修改代码，而 CTM 会保持 `.cm` 文件是最新的。

## A.4.6 其他有趣的 CTM 选项

### A.4.6.1 确切找出更新将触及哪些内容

你可以使用 CTM 的 `-l` 选项来确定 CTM 将对你的源码库所做的更改列表。如果你喜欢保留更改日志、以任何方式对修改后的文件进行预处理或后处理，或者只是有点疑神，这非常用。

### A.4.6.2 在更新前进行备份

有时你可能想备份所有将被 CTM 更新更改的文件。

指定 `-B backup-file` 选项会导致 CTM 将给定 CTM 增量将触及的所有文件备份到 `backup-file`。

### A.4.6.3 限制更新触及的文件

有时你可能感兴趣限制给定 CTM 更新的范围，或者可能感兴趣从一系列增量中提取几个文件。

你可以通过使用 `-e` 和 `-x` 选项过滤正则表达式来控制 CTM 将操作的文件列表。

例如，要从你保存的 CTM 增量集中提取 `lib/libc/Makefile` 的最新副本，请运行命令：

```bash
# cd /where/ever/want/to/extract/it/
# ctm -e `~/libc/Makefile` -ctm-src-xxx.*
```

对于 CTM 增量中的每个文件，`-e` 和 `-x` 选项按照命令行给出的顺序应用。
只有当文件在应用 `-e` 和 `-x` 选项后被标记为合格时，CTM 才会处理该文件。

## A.4.7 CTM 的未来计划

有很多：

- 在 CTM 系统中使用某种身份验证，以便允许检测伪造的 CTM 更新。
- 清理 CTM 的选项，它们变得变得混乱且违背直觉。

## A.4.8 杂项

ports 集合也有一系列增量，但目前兴趣还不算高。

## A.4.9 CTM 镜像

CTM/FreeBSD 可以通过以下镜像站通过匿名 FTP 获取。如果你选择通过匿名 FTP 获取 CTM，请尝试使用离你附近的站点。

如果遇到问题，请联系 `ctm-users` (http://lists.FreeBSD.org/mailman/listinfo/ctm-users) 邮件列表。

加利福尼亚，湾区，官方源

- `ftp://ftp.FreeBSD.org/pub/FreeBSD/development/CTM/`

南非，所有增量的备份服务器

- `ftp://ftp.za.FreeBSD.org/pub/FreeBSD/CTM/`

台湾/R.O.C.

- `ftp/ctm.tw.FreeBSD.org/pub/FreeBSD/development/CTM/`
- `ftp/ctm2.tw.FreeBSD.org/pub/FreeBSD/development/CTM/`
- `ftp/ctm3.tw.FreeBSD.org/pub/FreeBSD/development/CTM/`

如果你没有在附近找到镜像或镜像不完整，请尝试使用搜索引擎如 alltheweb (http://www.alltheweb.com/)。

## A.5 使用 CVSup

### A.5.1 介绍

CVSup 是一个软件包，用于从远程服务器主机上的主 CVS 仓库分发和更新树。FreeBSD 源码维护在加利福尼亚的一台中央开发机器的 CVS 仓库中。通过 CVSup，FreeBSD 用户可以轻松地保持自己的源码是最新的。

CVSup 使用拉取（pull）模型。在拉取模型下，每个客户端在需要时向服务器请求更新。服务器被动等待客户端的请求。所有更新均由客户端发起。服务器不会发送计划外的更新。用户必须手动使用 CVSup 客户端获取更新，或者必须设置 cron 业定期自动运行。

`CVSup` 这个词（首字母大写）指的是整个软件软件包。它的主要组件是运行在每个用户机器上的客户端 `cvsup` 以及运行在每个 FreeBSD 镜像站的服务器 `cvupsd`。

## 附录 A. 获取 FreeBSD

节 A.7 包含了用户可能感兴趣的分支标签。在 CVS 配置文件中指定时，必须在前面加上 `tag=(RELENG_4)` 以变变为 `tag=RELENG_4)`。请记住，只有该标签对 Ports 集合（Ports Collection）有效。

> 警告：请小心按照所示的内容精确输入标签名称。CVS 无法区分有效和无效标签。如果你拼写错了标签，CVS 的行为将就像你指定了一个未引用任何文件的标签一样。在这种情况下，它可能会删除你现有的源码。

当你指定一个分支标签时，通常会收到该开发分支的最新版本。如果你想接收旧版本，可以通过 `date=value` 字段指定一个日期来实现。`cvsup(1)` 手册解释了如何操作。

对于我们的示例，我们希望接收 FreeBSD-CURRENT。我们在 sufile 的开头添加此行：
`default tag=`

如果你既没有指定 tag，也没有指定 `date=` 字段，就会有一个重要的特殊情况发生。开发者通常倾向于这种操作方法：从服务器的 CVS 仓库接收实际文件，通过在本地维护一个仓库，他们获得了检索修订历史和检查文件过去版本的能力。这在磁盘空间上付出了巨大的代价。

- 从哪里获取它们？

我们使用 `host=` 告诉 `cvsup` 从哪里获取更新。任何 CVS 镜像站点都可以，但你应该选择一个离你较近的。在这个示例中，我们使用一个虚构的 FreeBSD 发行站点 `cvsup99.FreeBSD.org`。
`default host=cvsup99.FreeBSD.org.`

在运行 CVSup 之前，你需要选择一个实际存在的 host。在每次运行 `cvsup` 时，你都可以在命令行中使用 `-h hostname` 来覆盖 host 设置。

- 将它们放在你自己的这里什么位置？

`prefix=` 字段告诉 `cvsup` 将接收到的文件放在哪里。在这个示例中，我们将源文件直接放入我们的主源码树 `/src` 中。`src` 目录在我们选择接收的集合中已经是隐式存在的，因此这是正确的指定：
`default prefix=/`

- `cvsup` 在哪里维护其状态文件？

CVS 客户端在所谓的“base”目录中维护某些状态文件。这些文件通过跟踪你已经接收了哪些更新，帮助 CVSup 工作得更高效。我们使用标准目录 `/var/db`：
`default base=/var/db`

#### 其他杂 sufile 设置：

sfile 中通常还需要包含另一行样板代码：
`default release=cvs delete user-rel-suffix compress`

`release-cvs` 表示服务器应该从 FreeBSD 主仓库获取其信息。这几乎总是如此的，但还有其他超出本文讨论范围的可能性。

`delete` 赋予 CVS 删除文件的权限。始终指定此项，以便 CVS 能够保持你的源码树完全是最新的。CVS 会非常小心地只删除它负责的文件。任何额外的文件将保持原样。

`use-rel-suffix` 是一个晦涩的选项。如果你想了解它，请参 `cvsup(1)` 手页。否则，只需指定它而无需担心。

`compress` 允许在通信通道上使用 gzip 风格的压缩。如果你的网络连接速度比 T1 还快，则不需要使用 compress。否则，它会有很大帮助。

- 将它们整合在一起：

以下是我们示例的示例 sufile：

```
default tag=
```
