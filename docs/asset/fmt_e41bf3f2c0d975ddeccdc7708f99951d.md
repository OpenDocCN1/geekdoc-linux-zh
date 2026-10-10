
使用`rpm -qi`命令验证包是否已安装，该命令会显示二进制包何时以及在哪个计算机上构建等信息。列表 2.1 展示了此命令。（`rpm -qi`还会显示关于该包内容的扩展英语摘要，该摘要在列表 2.1 中已省略。）

## 列表 2.1: RPM 查询输出

```
$ rpm -qi samba
Name            : samba
Epoch           : 2
```

## 第 2 章 • 管理软件

```
Version : 3.6.5
Release : 86.fc17.1
Architecture: x86_64
Install Date: Mon Jun 16 Jul 2012 12:28:51 PM EDT
Group : System Environment/Daemons
Size : 18503445
License : GPLv3+ and LGPLv3+
Signature : RSA/SHA256, Fri 04 May 2012 11:03:50 AM EDT, Key ID-50e94c1aca3465
Source RPM : samba-3.6.5-86.fc17.1.src.rpm
Build Date : Fri 04 May 2012 08:42:51 AM EDT
Build Host : x86-0.phx2.fedoraproject.org
Relocations : (not relocatable)
Packager : Fedora Project
Vendor : Fedora Project
URL : http://www.samba.org/
Summary : 与 Windows 机器协作的服务器和客户端软件
```

### 从 RPM 中提取数据

有时你可能在不安装包的情况下从 RPM 中提取数据。例如，这是从源 RPM 中获取原始源代码以编译软件（无需 RPM 工具帮助），或者为非 RPM 系统获取字体或其他非程序数据。

RPM 文件实际上是修改过的`cpio`归档。因此，将文件转换为`cpio`文件相对简单，随后你需要使用与大多数 Linux 发行版附带的`rpm2`程序。（你可以在不使用 RPM 的发行版上使用此工具。）该程序接受单个参数——RPM 文件名，并在标准输出输出`cpio`归档。因此，如果你想创建一个`cpio`归档，必须限制输出：

```
$ rpm2cpio samba-3.6.5-86.fc17.1.src.rpm >
```

重定向操作符(`>`)在第 1 章“探索命令行工具”中有更详细的描述，类似于稍后提到的管道操作符(`|`)。第 4 章“管理文件”详细描述了`cpio`。然后你可以使用`cpio`提取数据，它使用`-i`选项提取归档，并使用`--make-directories`创建目录：

```
$ cpio -i --make-directories samba-3.6.5-86.fc17.1.cpio
```

或者，你也可以使用管道将这两个命令连接起来，而不创建中间文件：

```
$ rpm2cpio samba-3.6.5-86.fc17.1.src.rpm | cpio -i --make-directories
```

在任何情况下，你都可以提取这种数据。另一种从 RPM 提取数据的方法是使用`alien`，它将在后文“转换包格式”中介绍。

### 使用 Yum

Yum（黄色 Updater）源于 Yellow Dog Linux 发行版，是多种管理器之一，但已被红帽、CentOS 和 Fedora 采用。它允许你通过命令行轻松地安装包及其依赖项。

使用 Yum 最基本的方法是使用`yum`命令，其语法如下：

```
yum [options] [command] [package...]
```

可用选项取决于你使用的命令。表 2.3 描述了常用的`yum`命令。

#### 表 2.3 常用 yum 命令

| 命令 | 描述 |
|---|---|
| `install` | 通过包名安装一个或多个包。也会安装依赖项。 |
| `update` | 将指定的包更新到最新版本。如果没有指定包，`yum`将更新所有包。 |
| `check-update` | 是否有更新。如果有，`yum`将显示它们的名称、版本和仓库（例如 `extras`）。 |
| `upgrade` | 带有`--obsolete`标志的`update`，以更好的方式处理过期包。 |
| `remove` 或 `erase` | 从系统中删除包；类似于`rpm -e`，但也会删除被依赖包。 |
| `list` | 显示包的信息，例如已安装的版本以及是否有更新。 |
| `provides` 或 `whatprovides` | 显示提供指定程序或功能的包。例如，输入`yum provides samba`会列出所有与 Samba 相关的包，包括所有可用更新。 |
| `search` | 在包名、摘要、打包者描述中搜索指定的关键词。如果你不知道包名，但能想到一个可能出现在这些字段但在其他包字段中不出现的词，这很有用。 |
| `info` | 显示包的信息，类似于`rpm -qi`命令。 |
| `clean` | 清理 Yum 缓存。建议定期运行此命令，以免下载的包占用过多磁盘空间。 |
| `shell` | 进入 Yum shell，你可以在其中连续输入多个 Yum 命令。 |
| `resolvedep` | 显示匹配指定依赖的包。 |
| `localinstall` | 安装指定的本地 RPM 文件，使用你的 Yum 仓库解析依赖项。 |
| `localupdate` | 使用本地 RPM 文件更新系统，使用你的 Yum 仓库解析依赖项。除了本地文件更新的包及其依赖项外，不会更新其他包。 |
| `deplist` | 显示指定包的依赖关系。 |

在大多数情况下，使用 Yum 比直接使用 RPM 管理软件包更简单，因为 Yum 会找到最新的可用软件包，下载它并安装所有所需的依赖项。不过，Yum 也有它的局限性；它的功能取决于它所在的软件仓库（repositories），因此它无法安装未存储在这些仓库中的软件。

![](img/1624483a11d032df045f9465e0d0144d_112_0.png)

如果你使用 Yum 自动升级系统上的所有软件包，你实际上是将对系统的控制权交给了发行版维护者。虽然红帽（Red Hat）或其他发行版维护者不太可能尝试以此方式入侵你的电脑，但在你对更新过程进行极少监督的情况下，自动更新极可能会破坏你系统中的某些功能，特别是如果你过去从不寻常来源获取过软件包的话。

如果你不想安装软件包只是想获取它，可以使用`yumdownloader`。输入此命令并跟接包名，该软件包的最新版本将下载到当前目录。这对于需要更新未连接到互联网的系统来说非常有用；你可以使用另一台运行相同发行版的计算机来获取软件包并将其传输到目标系统。

如果你倾向于使用 GUI 工具而不是命令行工具，你应该知道存在`yum`的 GUI 前端。例如`yumy`和`kyum`。你可以使用文本模式的`yum`安装这些前端，命令为`yum install kyum`。

练习 2.1 将将介绍使用`rpm`工具进行软件包管理的过程。

### 练习 2.1

#### 使用 RPM 管理软件包

要使用`rpm`工具管理软件包，请按照以下步骤操作：

1. 以普通用户身份登录 Linux 系统。
2. 获取一个用于测试的软件包。你可以尝试从你所使用的发行版中找一个你尚未安装的软件包；但如果你尝试一个随机软件包，可能会发现它已经安装或存在未满足的依赖。本实验以安装`zsh-4.3.17-1.fc17.x86_64.rpm`为例，这是一个大多数系统默认未安装的 shell，将其从 Fedora 17 DVD 安装到 Fedora 17 系统上。如果你在测试中使用另一个 RPM 文件，则必须根据需要调整命令。
3. 如果你使用的是 GUI 登录，请从桌面环境的菜单系统中启动一个`xterm`。
4. 获取 root 权限。你可以通过在`xterm`中输入`su`、在 Konsole 窗口中选择“Session New Root Console”，或使用`sudo`（如果已配置）运行后续步骤中的命令。
5. 输入`rpm -q zsh`以验证该软件包当前未安装。系统应该返回消息`package zsh is not installed-`。
6. 输入`rpm -qpi zsh-4.3.17-1.fc17.x86_64.rpm`。（如果软件包文件不在当前目录，你需要提供该文件的完整路径）。系统应该响应并显示有关软件包的信息，例如版本号、供应商、构建该包的机器主机以及软件包描述。
7. 输入`rpm -ivh zsh-4.3.17-1.fc17.x86_64.rpm`。系统将安装软件包并在过程中显示一系列哈希值(`#`)。
8. 输入`rpm -q zsh`。系统应该响应完整的包名，包括版本号和构建号。此响应证实了软件包已安装。
