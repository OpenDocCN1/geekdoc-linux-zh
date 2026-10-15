
这需要修复，你可以通过使用命令行选项 `-C` 为 `sendmail` 命令提供配置文件的正确路径，例如 `sendmail -C/etc/sendmail.cf`。还需要编辑 `Sendmail` 的启动脚本以插入此命令行选项，以便在每次系统启动时都使用正确的配置文件。坦率地说，这麻烦得不偿手。只需将 `sendmail.cf` 文件移动到 `/etc` 即可。

# 第 3 章 运行 Sendmail

在宣布安装完成之前，应该检查的一个文件是 `sendmail.cf` 文件。新版本的 `Sendmail` 可能会添加新的配置语法，导致旧的配置文件与新发布版本不兼容。`Sendmail` 程序通过检查 `sendmail.cf` 文件内部的版本（`V`）命令来指示配置语法的层级。检查兼容性最简单的方法是使用 `sendmail` 命令发送一封测试邮件：

```
# sendmail -v -t -C/etc/sendmail.cf
```

警告：`.cf` 文件已过期：`sendmail` 8.11.0 支持版本 9，`.cf` 文件版本为 8

> ^D
未在头部中找到收件人地址

使用 `-v` 选项运行 `Sendmail` 会让程序提供详细信息，这正是你在测试时所需要的。`-t` 选项告诉 `Sendmail` 邮件将在控制台中输入。在这种情况下，我立即通过 `Ctrl+D` 终止了会话（这就是 `D` 所示所示的），因为我不想发送邮件，我只想查看警告信息。新的 `Sendmail` 程序对配置文件的版本级别表示不满。在特定情况下，邮件将无法成功送达，因为 `Sendmail` 8.9 和 8.11 之间变化太大。这并不总是如此。有时你可以强制通过任何配置发送邮件。但你不应该这样做。

此示例表明该配置与新发布版本不兼容。要解决这种不兼容性，你需要重新构建你的配置。理解基础 `Sendmail` 配置并构建你自己的自定义配置是本书第二部分的主题。

# 总结

`Sendmail` 以两种不同的模式运行以处理出站和入站邮件。`Sendmail` 实时启动以处理单封出站邮件，但作为守护进程运行以收集入站邮件。有几个工具可以帮助你控制哪些系统启动运行时 `Sendmail` 守护进程。

在运行 `Sendmail` 程序之前，必须对其正确安装。可以使用 Linux 软件包管理器安装 `Sendmail`，也可以从源码编译。尽管 Identity 具有复杂性，但它的安装方式与其他所有 Linux 软件包相同，并使用与任何其他 Linux 启动过程相同的工具来控制 `Sendmail` 的启动过程。安装和运行 `Sendmail` 是两个不具有任何特殊复杂性的任务。如果你知道如何安装和运行 Linux 进程，你就知道如何在 Linux 系统上安装和运行 `Sendmail`。

一旦安装，必须对 `Sendmail` 进行配置。配置 `Sendmail` 是第二部分的主题，从第 4 章“创建基础 Sendmail 配置”开始。

# 第二部分

# 核心配置

特色内容：

- `Sendmail` m4 目录和文件的位置及其作用
- 理解基础的 m4 宏语言
- 如何使用 m4 构建 `sendmail.cf`
- `generic-linux.mc` 文件包含的内容及其作用
- 理解 Linux `OSTYPE` 文件
- 理解 `DOMAIN` 文件以及如何修改它
- 分析并改进红帽（Red Hat）配置
- 如何为你的 `Sendmail` 程序及其配置添加数据库支持
- `local-host-names` 文件和 `relay-domains` 文件的作用
- aliases 数据库、用户数据库和 `genericstable` 的用途
- access 数据库的语法和结构
- `virtertable` 和 `mailertable` 的用途

# 创建基础 Sendmail 配置

在上一章的结束时，我们从源码发行编译了 `Sendmail` 8.11。令我们沮丧的是，我们发现即使将 `sendmail.cf` 配置移动到新 `Sendmail` 预期的查找目录 `/etc/mail` 之后，新的 `Sendmail` 程序仍然无法运行。`Sendmail` 8.11 抱怨 Linux 发行版提供的 `sendmail.cf` 文件是旧版本，与新软件发布不兼容。解决这个问题的方法是构建一个与新软件兼容的新 `sendmail.cf` 文件，在本章中我们正要这样做。

构建一个新的 `Sendmail` 配置（即使是非常基础的）也是一个多步骤的过程。`sendmail.cf` 配置文件是由 m4 宏构建的。要构建你自己的配置，你需要：

- 找到正确的 m4 宏库和文件
- 对 m4 宏语言有基础理解
- 选择合适的宏配置文件
- 根据需要修改文件
- 通过 m4 宏处理器处理你新创建的宏配置文件

本章涵盖了所有这些步骤，同时构建了一个非常基础的配置文件，该文件解决了我们在使用源码发行版升级到 `Sendmail` 8.11 时遇到的不兼容问题。请记住，在第 3 章“运行 Sendmail”中，我们在 Linux 下以两种不同的方式安装了 `Sendmail`。在从源码编译并安装 `Sendmail` 之前，我们使用 `RPM` 安装了它。在 `RPM` 安装期间出现了一些问题，但一旦安装成功，一切都准备好运行了。当时没有兼容性问题，因此没有理由构建简单的配置来解决兼容性问题。

然而，即使你使用 `RPM` 安装 `Sendmail`，本章涵盖的主题对你也很有用。构建这个简单的配置提供了 m4 的介绍，并为理解更复杂的配置奠定了基础。我们在后面的章节中将基于此简单配置，创建一个适用于生产环境电子邮件服务器的健壮、自定义配置。这个基础对于所有 `Sendmail` 管理员都是有用的，无论你是否使用 `RPM`。让我们从定位 `Sendmail` 发行版提供的 m4 宏语言源文件开始。

# cf 目录结构

m4 是一个通用的宏处理器。它有广泛的用途，并不是专门为 `Sendmail` 配置设计的。m4 定义由维护 `Sendmail` 的人员构建。`Sendmail` 发行版包含了用于构建配置的 m4 宏源文件，位于 `cf` 目录下。这些 m4 宏源文件用于构建 `sendmail.cf` 文件。由于 `Sendmail` 发行版包含了这些文件。由于文件发行版创建的 `cf` 目录名称为 `sendmail-8.11.0`，其中版本号即为版本。在我们的示例系统中，该命令显示 `cf` 目录位于 `/usr/local/src/sendmail-8.11.0/cf`。`cf` 目录的列表包含 10 个项目：

```
ls /usr/local/src/sendmail-8.11.0/cf
```

README mconfig

`cf` 目录包含一个 README 文件，提供了关于 m4 语言以及如何使用该语言构建 `sendmail.cf` 的有用文档。始终检查此文件以获取最新更改和新功能。

# cf 目录结构

稍后你会看到，大多数子目录（domain、feature、mailer、otype 和 siteconfig）的名字可以清楚地识别为用于构建配置的宏命令名称。只有 `cf`、`m4` 和 `sh` 目录与 m4 宏同名。然而，所有的目录都值得探索。

# sendmail-cf RPM 文件

在本章中，`cf` 目录及其子目录是作为源码发行版的一部分描述的。然而，这些相同的文件作为 `RPM` 安装可用。在第 3 章中，我们安装了 `cf` 目录的 `RPM` 版本。它是标识为 `sendmail-cf-8.11.0-1.i86` 的包。它包含了本章描述的所有文件。区别在于文件的位置。要找到文件存储的位置，运行 rpm 查询并请求文件列表如下：

```
$ rpm -q -l sendmail-cf
```

在我们的示例红帽系统中，该命令显示 `cf` 目录位于 `/usr/lib/sendmail-cf`。`/usr/lib/sendmail-cf` 的列表显示如下：

```
ls /usr/lib/sendmail-cf
```

README domain feature hack m4 mailer otype siteconfig

如果你使用的是 `RPM` 安装，`/usr/lib/sendmail-cf` 等于讨论中的 `cf`。相同的 README 文件和九个子目录出现在 `RPM` 安装的 `/usr/lib/sendmail-cf` 中。无论你如何安装 `Sendmail` 8.11，本章涵盖的内容都适用。

# 很少使用的目录

`cf` 目录中的三个目录（`hack`、`sh` 和 `siteconfig`）对大多数配置来说很少。对于其中两个目录，这种缺乏用途的情况与它们所代表的宏命令缺乏实用直接相关。

`cf/hack` 目录存放本地系统管理员构建的解决临时 `Sendmail` 配置问题的 m4 源文件。临时代码修复被称为 hack（破解），因此该目录以及使用它的命令以此命名。`HACK` 命令

## 84 第 4 章 创建基础 Sendmail 配置

它几乎从不被使用，因此 hack 目录也几乎不被使用。通过 `ls` 查看 hack 目录，它只包含一个文件。

```bash
$craig$ ls hack

cssubdomain.m4
```
