
[master@fedora-server -]$ `rpm --query--all`

> 和大多数 Linux 命令一样，`rpm` 命令有自己的长形式和短（缩写）选项及参数。例如，`--query` 选项的短形式是 `-q`，`--all` 的短形式是 `-a`。我们在书中交替使用命令选项的短形式长形式。

![](img/206cceb3dded456e2347d07189576dd7_118_0.png)

## 查询特定包的详情

让我们关注上一个命令输出中列出的包之一：Bash 应用程序。使用 `rpm` 查看你的系统中是否安装了 Bash 应用程序：

```
[master@fedora-server -]$ rpm --query bash-*nbash-5.*x86_64
```

输出应该类似于第二行，显示 Bash 包已安装。它还显示了附加在包名后的版本号。

> 当你在 Linux 中处理软件包时，你系统上的确切软件版本号可能与我们示例系统的版本号不同。系统更新和 Linux 发行版本身等因素会影响并决定具体版本。

这就是我们有时在某些练习中截断包名版本号的原因之一。例如，我们可能不写 `bash-9.4.2`，而是只写 `bash-9`。你可以肯定的是主包名始终是相同的——即在 openSUSE、Fedora、Mandrake、CentOS、RHEL、Ubuntu 等系统中都是 Bash。

这引出了我们的下一个问题：什么是 Bash？它是做什么的？要找到答案，请输入以下：

```
[master@fedora-server -]$ rpm -qi bash

Name : bash

Version : 5.*

Group : System Environment/Shells

Vendor : Fedora Project

URL : http://www.gnu.org/software/bash

Summary : The Bourne Again shell

Description : The Bourne Again shell (Bash) 是一个与 shell (sh)...兼容的 shell 或命令解释器...
```

![](img/206cceb3dded456e2347d07189576dd7_119.png)

## 安装软件 (使用 RPM)

在接下来的章节中我们将使用 `dnf` 包管理器来下载包。下载包是 `dnf` 设计的众多功能之一。

或者，你可以直接从供应商网站浏览并下载任何文件：

```
http://dl.fedaproject.org/pub/fedora/linux/rawhide/Everything/x86_64/Packages/
```

让我们演示安装软件包的过程：

1. 以管理员权限的用户登录系统。我们在示例系统中使用 `master` 账户，你也可以使用 `root` 账户。如果你通过 GUI 登录，请通过虚拟终端完成以下步骤。
2. 使用 `mkdir` 和 `cd` 命令创建一个 `Downloads` 文件夹（如果不存在），然后将当前工作目录更改到主目录下的 `Downloads` 文件夹：
3. 使用 `dnf` 程序下载本章节压缩文件：

```
[master@fedora-server ~] mkdir ~/Downloads && cd ~/Downloads
```

```
[master@fedora-server Downloads$] dnf download lynx
```

4. 双击确认包是否正确下载。使用 `ls` 命令列出目标目录下以 **lynx** 开头的文件。

5. 现在你已经确认文件存在，对该包进行测试安装。这将在不实际向系统安装任何东西的情况下运行安装流程。对于确保包的所有需求（依赖项）已满足非常有用。输入以下：

```
[master@fedora-server Downloads$] rpm --install --verbose --hash --test lynx*

Verifying...

################# [100%]

Preparing...

################ [100%]
```

### 6. 现在执行实际安装：

```
[master@fedora-server Downloads]$ sudo rpm -ivh lynx-*

Verifying... ################# [100%]

Preparing... ################# [100%]

Updating / installing... ################# [100%]

1:lynx-*
```

### 7. 运行一个简单的查询以确认应用程序已安装在你的系统上：

```
[master@fedora-server Downloads]$ rpm -q lynx

lynx-x86_64
```

输出显示 lynx 现在可以在系统上使用了。
你会发现它正在工作，lynx 是一个基于文本的 浏览器。你只需在提示符处输入 `lynx` 即可启动它。按 `q` 退出。你会在终端的右下角看到一个提示，确认你是否想要退出 lynx。按回车键确认。

如你所见，通过 RPM 安装包可能是复杂的，有时是因为依赖项失败或缺失。例如，lynx 包可能要求在成功安装 lynx 之前系统上必须已安装 bash 包。

> 提示：你可以通过挂载 ISO 文件来轻松访问第 2 章使用的操作系统镜像内容。例如，要将名为 Fedora-Server-dvd-x86_64*.iso 的 Fedora DVD 镜像挂载到现有的 media/iso 目录，你可以输入以下：
`# mount Fedora-Server-dvd-x86_64*.iso /media/iso/`

在后续章节中尝试手动安装 gcc 时让你们经历的痛苦是有必要的，因为它让你窥了后台的运行机制，更重要的是，它能让你对我们之后讨论的更简单的方法（dnf, yum, zypper 等）有更好的理解。

让我们通过安装一个更复杂的包，来看看 RPM 是如何处理依赖关系的。我们将首先下载我们想要安装的包。

- 1. 这项清理工作并非严格强制，但强烈建议执行，特别是如果你运行的是前沿的 Fedora 原始流版本，就像我们在我们的示例服务器上运行的那样。

让我们将所有当前安装的包更新到最新版本。我们将使用 `dnf` 程序的 `update` 选项，如下：

```
[master@localhost Downloads]$ sudo dnf -y update --nogpgcheck
```

这个过程可能需要一些时间——取决于有多少新更新可用。

- 2. 现在我们回到原始目标。首先，将最新版本的 `gcc` 下载到 `Downloads` 文件夹：

```
[master@fedora-server Downloads]$ dnf download gcc
```

- 3. 通过输入以下命令尝试安装下载的 `gcc` 包：

```
[master@fedora-server Downloads]$ sudo rpm -ivhc gcc-*.rpm

error: Failed dependencies:

binutils >= * is needed by gcc-*.x86_64

cpp >= * is needed by gcc-*.x86_64

glibc-devel >= * is needed by gcc-*.x86_64

libisnl.so.* (64bit) is needed by gcc-*.x86_64

libmpc.so.* (64bit) is needed by gcc-*.x86_64
```

输出看起来并不理想。它告诉我们 `gcc`（及其依赖项）依赖（需要）其他包和库：`binutils`, `cpp`, `glibc-devel`, `libisnl.so.*` 和 `libmpc.so`。

- 4. 确定包名称并判断其用途的一种快速方法是使用 `dnf` 命令的 `whatprovides` 选项。这就是揭开有时晦涩的库和包名称的方法。例如，要确定上一个输出中显示的 `libmpc.so.*` 库由哪个包提供：

```
[master@fedora-server Downloads]$ dnf whatprovides libmpc.so.*

libmpc-* : C library for multiple precision complex arithmetic

Provide : libmpc.so.3
```

从输出中，我们可以知道名为 `libmpc` 的包提供了所需的库。对于任何包名不明确的依赖项，你都需要执行此操作。

- 5. 让我们继续使用 `dnf` 下载这些依赖项：

```
[master@fedora-server Downloads]$ sudo dnf download --arch=x86_64 \
binutils cpp glibc-devel is libmpc
```
