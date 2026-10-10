
# 470 第 8 章：在 Linux 上安装和管理软件

## 练习题

- **9.** 你将一个名为 `evolution-2.6.0-41.i586.rpm` 的 RPM 包文件下载到了主目录。假设当前目录是 `~`，你可以使用哪种命令来检查下载文件的数字签名，以验证它没有被篡改？
    - A. `rpm --checksig /evolution-2.6.0-41.i586.rpm`
    - B. `rpm --verify /evolution-2.6.0-41.i586.rpm`
    - C. `rpm --tamperproof /evolution-2.6.0-41.i586.rpm`
    - D. `rpm --signature /evolution-2.6.0-41.i586.rpm`

- **10.** 你将一个名为 `evolution-2.6.0-41.i586.rpm` 的 RPM 包文件下载到了主目录。假设当前目录是 `~`，你可以使用哪种命令将该包安装到你的系统中，并在安装完成后显示进度指示？
    - A. `rpm -i /evolution-2.6.0-41.i586.rpm`
    - B. `rpm -ihv /evolution-2.6.0-41.i586.rpm`
    - C. `rpm -install /evolution-2.6.0-41.i586.rpm`
    - D. `rpm -install --progress /evolution-2.6.0-41.i586.rpm`

- **11.** 你刚刚将一个名为 `evolution-2.6.0-41.i586.rpm` 的 RPM 包文件下载到了主目录。假设当前目录是 `~`，你会使用哪种命令来检查该包的依赖关系？（选择两个）。
    - A. `rpm -i /evolution-2.6.0-41.i586.rpm`
    - B. `rpm -test /evolution-2.6.0-41.i586.rpm`
    - C. `rpm -V /evolution-2.6.0-41.i586.rpm`
    - D. `rpm -deps /evolution-2.6.0-41.i586.rpm`

## 管理已安装软件

- **12.** 你需要从 Linux 系统中卸载 Pure-FTPd 服务。你已经切换到了原始安装文件所在的目录。卸载此包，需要输入的第一个命令是什么？
    - A. `./configure`
    - B. `make`
    - C. `make remove`
    - D. `make uninstall`

- **13.** 你在 Linux 系统上安装了一个名为 `evolution-2.6.0-41.i586.rpm` 的 RPM 包文件。你会使用哪种命令卸载此包？
    - A. `rpm -U evolution`
    - B. `rpm --U remove evolution`
    - C. `rpm -i --remove evolution`
    - D. `rpm -e evolution`

- **14.** 你目前在 Linux 系统上安装了一个名为 `evolution-2.2.0-2.i586.rpm` 的 RPM 包。你最近从 `http://www.sourceforge.net` 下载了 `evolution-2.6.0-41.i586.rpm` 包。你会使用哪种命令来安装该包的更新版本？
    - A. `rpm -U evolution-2.6.0-41.i586.rpm`
    - B. `rpm -i evolution-2.6.0-41.i586.rpm`
    - C. `rpm -i--upgrade evolution-2.6.0-41.i586.rpm`
    - D. `rpm -install --progress /evolution-2.6.0-41.i586.rpm`

- **15.** 你刚刚将一个名为 `evolution-2.6.0-41.i586.rpm` 的 RPM 包文件下载到了主目录。假设当前目录是 `~`，你会使用哪种命令来检查该包的依赖关系？（选择两个）。
    - A. `rpm -i /evolution-2.6.0-41.i586.rpm`
    - B. `rpm -test /evolution-2.6.0-41.i586.rpm`
    - C. `rpm -V /evolution-2.6.0-41.i586.rpm`
    - D. `rpm -deps /evolution-2.6.0-41.i586.rpm`

## 答案解析

- **14.** A. `rpm -U evolution-2.6.0-41.i586.rpm` 命令将现有的 `rpm` 升级到新版本。
    B、C 和 D 都是错误的。如果系统中不存在该 `rpm`，则可以使用 B 来安装它。但由于系统中已经安装了之前的版本，运行时使用 `-i` 选项将产生错误。C 是一个使用了无效 `rpm` 命令的干扰项。D 理论上可以作为一个正确答案，该命令将从系统中安装旧版本。然而，你随后必须使用响应 B 中的命令来安装新版本。使用 `-U` 选项可以同时完成这两项操作。

- **15.** C. `rpm -qi evolution-2.6.0-41.i586.rpm` 命令将查询该软件包并在屏幕上显示摘要信息。
    A、B 和 D 都是错误的。这些选项都是使用了错误 `rpm` 命令语法的干扰项。

- **16.** A. `rpm -q --provides /usr/bin/perl` 命令将显示其所提供的软件包名称。你只需插入 `rpm -q --provides perl` 来获取相同的信息。
    B、C 和 D 都是错误的。B 和 C 是使用了无效 `rpm` 命令语法的干扰项。D 是错误的，因为它将显示 `perl` 软件包提供的组件。

- **17.** A 和 C. 错误代码中的 `S`、`5` 和 `T` 表示文件大小、MD5 校验和和时间戳存在问题。`c` 表示该文件是配置文件，因此这些错误可能重要，也可能不。
    B、D 和 E 都是错误的。B 将由错误代码中的 `M` 表示。D 将由错误代码中的 `D` 表示。E 将由错误代码中的 `U` 表示。

## 实验答案

### 安装此软件包

如果在下载 tarball 归档的网站上提供了校验和（`checksum`），你应当输入 `sum /desktop-1.5.0.tar`，并将结果得到的校验和与原始校验和进行比较。如果它们相同，说明你的操作没问题了！如果不相同，你就知道本地硬盘上的文件副本在某种程度上与网站上的原始文件不同。这不是好事。你应该下载一个新副本，并再次对其运行 `sum` 命令以验证其是否完整送达。

# 471 实验答案

此时，你需要从归档中解压缩并提取安装文件。这可以通过在 shell 提示符输入 `tar -xzvf /rdesktop-1.5.0.tar.gz` 来。这样做会在 `/root` 下创建一个名为 `rdesktop-1.5.0` 的新目录。归档中的文件会被提取到该目录。

从 tarball 中提取文件后，你现在可以开始安装过程。要实现这一点，首先在 shell 提示符输入 `cd rdesktop-1.5.0` 切换到安装目录。你应该输入 `ls` 并验证运行安装所需的文件是否存在于目录中。

要开始安装，首先在 shell 提示符输入 `./configure`。该脚本将检查系统并验证其架构和 Linux 发行版。它还将验证你是否拥有在该特定系统上安装软件所需的所有组件。如果需要，可以使用 `less` 查看 `Makefile` 文件并验证它是否按照你想要的方式配置的。

配置脚本完成后，你可以在 shell 提示符输入 `make` 从源代码编译二进制可执行文件。完成后，你将输入 `make install` 将可执行文件及其相关的支持文件安装到文件系统中适当的位置。

软件安装后，你可以在 shell 提示符运行 `rdesktop` 可执行文件并验证程序是否运行正常。

![](img/8156850acb7240fabbc4667ef20f2fa8_514_0.png)

# 9 使用 Linux Shell

## 认证目标

- 9.01 使用 Bourne Again Shell
- 9.02 管理 Linux 环境变量
- 9.03 管理 Shell 命令的输入输出
- 9.04 创建 Shell 脚本
- 两分钟演练
- 问答自测

# 474 第 9 章：使用 Linux Shell

是时候更深入地熟悉 Linux shell 了。随着我们对这本书的不断学习，我们花费了大量时间在 Linux 系统上通过命令行进行操作。我们一直在使用的命令行界面是由 Linux shell 提供的。这就是为什么我们称其为 shell 提示符（`shell prompt`）。你已经学习了如何使用 shell 命令来管理文件系统、管理用户和组、编辑文本文件以及安装应用程序。`shell` 提示符非常适合执行此类命令。

然而，它也能很好地适用于许多其他任务。`shell` 本身实际上是管理 Linux 操作系统的非常强大的工具。在本章中，我们将探索如何做到这一点。我们将讨论以下主题：

- 介绍 Bourne Again Shell
- 使用 Linux 环境变量工作
- 管理 `shell` 命令的输入输出
- 创建 `shell` 脚本

![](img/8156850acb7240fabbc4667ef20f2fa8_515_0.png)

## 考试要点

# 使用 Linux Shell

正如你在学习这本书的过程中所证明的，Linux+ 认证计划非常强调使用命令行来完成一切工作。你不会受到诸如 `linuxconfig` 或 `YaST` 这样的图形化配置工具的测试。因此，你需要精通 Linux `shell` 才能通过 Linux+ 考试。你应该特别熟悉 `bash` `shell`。

你应该非常熟练地处理环境变量以及从命令行重定向输入和输出。在 Linux+ 考试中，要准备好应对这类问题：它们要求你知道如何设置环境变量的值并使其在 `shell` 启动时持久化。此外，还要准备好应对那些要求你必须知道如何将命令的输出重定向到另一个程序进行处理的问题。此外，你还被要求知道如何创建基础 `shell` 脚本。你应该熟悉 `shell` 脚本的基本结构、如何使其变为可执行，以及如何读取用户输入并将数据分配给变量。

使用 Bourne Again Shell 475

让我们从介绍 Bourne Again Shell 开始这一章。

# 认证目标 9.01

# 使用 Bourne Again Shell

在书的前面部分，我们回顾了 Linux 系统中通过命令行介绍给你的几种 `shell`。根据你的需求和偏好，你可以从 Bourne `shell` (`sh`)、Korn `shell` (`ksh`)、C `shell` (`csh`) 等中进行选择。

然而，大多数 Linux 系统使用的默认 `shell` 是 Bourne Again `Shell` (`bash`)。（这也是你 Linux+ 考试需要掌握的 `shell`！）`bash` 已经存在很久了。它起源于 20 世纪 70 年代的 UNIX 操作系统，并在 90 年代初被移植到最早的 Linux 发行版中。今天，`bash` 已成为 Linux 以及其他操作系统（包括 Apple 的 OS X 甚至（可选）Novell 的 NetWare）中最常用的 `shell` 之一。

因此，我们将讨论重点放在 `bash` `shell` 上。`bash` `shell` 执行了一些酷炫，使其成为许多 Linux 用户和管理员的首选 `shell`。在本章的这一部分，我们将回顾以下内容：

- 回顾 `bash` 配置
- 使用命令历史
- 使用命令补全

## 回顾 `bash` 配置

你可以通过 `bash` 内部几个配置文件来自定义你的 `shell` 环境。实际使用的文件取决于你使用的是登录 `shell` (`login shell`) 还是非登录 `shell` (`non-login shell`)。如果你的 Linux 系统启动到文本登录屏幕并且你登录了系统，则正在使用登录 `shell`。换句话说，如果你的系统启动到运行级别 3，你使用的就是登录 `shell`。如图 9-1 所示。

# 第9章：使用 Linux Shell

即使你的系统配置为启动到图形界面（运行级别 5），你仍然运行着一个登录 `shell` (`login shell`)。它隐藏在你的桌面之后。然而，如果你在桌面环境中打开终端会话，你并没有使用登录 `shell`。相反，你正在运行一个非登录 `shell`（`non-login shell`）。这如图 9-2 所示。

我们为什么要关心这个呢？因为你所使用的 `shell` 类型决定了系统会读取哪些配置文件来定制你的 `shell` 环境。这些文件列在表 9-1 中。

如果你使用的是非登录 `shell`，事情就非常简单。`bash` 仅仅是从用户主目录读取 `~/.bashrc`。

如果你使用的是登录 `shell`，`bash` 会首先读取 `/etc/profile` 并运行该文件中指定的配置。然而，之后情况就会变得复杂一些。正如你可能在表 9-1 中注意到的，列出的几个文件看起来的作用完全相同。你是对的，它们的作用确实如此。这里的问题在于，并不是所有的发行版都使用所有这些文件。例如，Fedora 系统使用 `~/.bashrc`、`~/.bash_profile` 和 `~/.bash_logout`。这如图 9-3 所示。

或者，在 SUSE Linux 系统上，使用的是 `~/.bashrc` 和 `~/.profile` 文件。这如图 9-4 所示。

当运行登录 `shell` 时，`bash` `shell` 程序会按照以下顺序搜索配置文件：

1. `~/.bash_profile`
2. `~/.bash_login`
3. `~/.profile`

图 9-2 使用非登录 `shell`

![](img/8156850acb7240fabbc4667ef20f2fa8_517_0.png)

# 表 9-1 `bash` Shell

| `bash` 配置文件 | `Shell` 类型 | 功能 |
| :--- | :--- | :--- |
| `~/.bashrc` | 非登录 `shell`（尽管大多数发行版的登录 `shell` 也会读取此文件。通常由下面列出的配置文件之一调用） | 存储单个用户的 `shell` 偏好 |
| `/etc/profile` | 登录 `shell` | 包含全局应用的配置参数 |
| `~/.bash_profile` | 登录 `shell` | 存储单个用户的 `shell` 偏好 |
| `~/.bash_login` | 登录 `shell` | 存储单个用户的 `shell` 偏好 |
| `~/.profile` | 登录 `shell` | 存储单个用户的 `shell` 偏好 |
| `~/.bash_logout` | 登录 `shell` | 指定用户从 `shell` 退出时执行的操作 |

# 图 9-3 Fedora 上的 `bash` 配置

```
root@fedora:/home/ksanders
File Edit View Terminal Tabs Help
[root@fedora ksanders]# ls -a
. . .. .bash_logout .bash_profile .gtkrc
[root@fedora ksanders]#
```

# 图 9-4 SUSE 上的 `bash` 配置

![](img/8156850acb7240fabbc4667ef20f2fa8_519_0.png)

它使用第一个文件并找到剩下的所有文件。如图 9-3 和 9-4 所示，这在 SUSE 和 Fedora 上并不是什么问题。记住，加载登录 `shell` 不会直接读取 `.bashrc`（尽管它通常由 `.bash_profile` 调用，因此在实际中它确实被登录 `shell` 使用）。因此，`bash` 在读取 `/etc/profile` 后，在 Fedora 系统上读取 `.bash_profile`。在 SUSE 系统上，`bash` 在读取 `/etc/profile` 后读取 `.profile`。

`.bash_logout` 文件仅在你退出 `shell` 时才使用。

你可以在 Linux 系统上同时运行多个终端会话。在图形界面中，你可以简单地运行多个终端程序，或者在一个终端程序内打开多个标签页。在文本环境中，你可以按下 `ALT-F1` 切换到第一个会话。

当运行登录 `shell` 时，`bash` `shell` 程序会按照以下顺序搜索配置文件：

让我们讨论一下这些 `shell` 的功能。

![](img/8156850acb7240fabbc4667ef20f2fa8_519_0.png)

## 场景与解决方案

**问：** 当用户从 `shell` 退出时会使用哪个配置文件？
**答：** 使用 `~/.bashrc`（尽管大多数发行版的登录 `shell` 也会读取此文件。通常由下面列出的配置文件之一调用）

**问：** 当你希望在 `shell` 中应用一个全局的更改时，使用哪个配置文件？
**答：** `/etc/profile`

**问：** 在 Fedora 系统上，`bash` 在读取 `/etc/profile` 后会读取哪个文件？
**答：** `~/.bash_profile`

**问：** 在 SUSE 系统上，`bash` 在读取 `/etc/profile` 后会读取哪个文件？
**答：** `~/.profile`

**问：** 使用非登录 `shell` 时，使用哪个配置文件？
**答：** `~/.bashrc`

## 使用命令历史

`bash` `shell` 支持命令历史。当你在 `shell` 中输入命令时，它都会保存在 `.bash_history` 文件中。

图 9-5 `bash` 命令历史

```
root@fedora:/home/ksanders
File Edit View Terminal Tabs Help
[root@fedora ksanders]# ls -a
. . .. .bash_logout .bash_profile .gtkrc
[root@fedora ksanders]#
```

图 9-6 `bash` 命令历史

![](img/8156850acb7240fabbc4667ef20f2fa8_519_0.png)

## 使用命令补全

除了命令历史，`bash` `shell` 还提供了命令补全。此功能在你需要输入很长的文件名时非常有用。命令补全允许你在 `shell` 提示符输入命令时只需按下 `TAB` 键。当你这样做时，`bash` `shell` 会“猜”你想输入什么并自动完成命令。
