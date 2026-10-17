
从这里你可以看到，我需要许多枯燥的编译尝试才能获取构建 `MyVT` 所需的所有包。识别这些包可能非常耗时，即使在本章之前的小节“确定哪个包提供了缺失的文件”中讨论了 `apt-file` 程序的帮助。`apt-build` 命令消除了这些烦恼，让你专注于软件本身，而不是它所需的基础设施。

### 第三部分：面向系统管理员的 Ubuntu 和 Kubuntu

## 使用 aptitude 添加和删除软件

个人而言，我认为面向终端的图形化界面充多只能算勉强可以。我更倾向于在绝对必要的情况下不使用它们，特别是当它们被像 Synaptic 和 Apt 软件包管理器所提供的图形化用户界面所取代时。

> 当使用 `aptitude` 安装软件时，你可能在安装过程中偶尔需要提供额外的配置相关的信息。在这些情况下，`aptitude` 显示的信息请求与第 23 章之前所示 `apt-get` 显示的相同。当你看到此屏幕时，必须回答它提出的任何问题，并在包安装继续之前提供任何请求的信息。

使用 `aptitude` 可以通过命令行界面 `install` 命令轻松安装软件，并使用 `remove` 命令删除。正如稍后标题为“使用 aptitude 推荐软件”的部分中所讨论的，`aptitude` 提供了一些选项，使得它在某些情况下从命令行使用 `aptitude` 很有吸引力。许多人也是 `aptitude` 界面的粉丝，主要是那些理解它的人。下一节将讨论 `aptitude` 界面的基础知识，重点介绍如何让它对凡人变得易读。

## 添加、删除和更新软件

### 使用 aptitude 用户界面的技巧和窍门

图 23-11 显示了当你第一次在 GNOME Terminal 中不带参数启动 `aptitude` 时看到的默认 `aptitude` 界面。

图 23-11
GNOME Terminal 中默认的 aptitude 界面
![img/e324f698da647444053422df5_990.png](img/e324f698da647444053422df5_990.png)

如果你坚持要使用此界面但遇到了视觉问题，那么你有点没辙了，因为 `aptitude` 界面没有提供更改配色的命令行选项。然而，一切并非没有——你可以通过更改终端应用程序对终端类型的认知来让界面更容易阅读。一个很好的选择是 `vt`，这是一个只支持黑白的经典终端。要进行此更改，退出 `aptitude` 并输入以下命令

> `$ TERM=vt`

执行此命令后，你可以重启 `aptitude`，它将如图 23-12 所示。

更改配色并没有让 `aptitude` 界面变得更有吸引力，但对我来说，至少让它变得可用。

## 第三部分：面向系统管理员的 Ubuntu 和 Ubuntu

图 23-12
黑白模式下的 aptitude 界面
![img/e324f698da647444053422df5_991.png](img/e324f698da647444053422df5_991.png)

一旦 `aptitude` 运行，以下是我最喜欢的命令：

- `Q`：允许退出 `aptitude`。
- `?`：显示一个包含 `aptitude` 界面使用摘要信息的面板。
- `Ctrl+T`：按住 `Ctrl` 键并按 `T` 显示 `aptitude` 的菜单，你可以使用方向键导航，或通过按下高亮的快捷键执行特定命令。

23-13 显示了使用 `aptitude` 默认配色的菜单。我必须说明：这种事情会让习惯了 Macintosh（甚至是 Windows）图形界面对 Linux 有坏印象。

关于使用 `aptitude` 界面的详细（且无偏见的）信息，请参 `aptitude` 的在线参考（`man aptitude`）或在 Web 上搜索相关信息。

## 使用 aptitude 安装推荐软件

如果你一直使用 `apt-get` 安装新软件，并且 `apt-get` 实用程序提示你有其他推荐或建议安装的包，你可以考虑使用 `aptitude` 的命令行界面而不是 `apt-get`。Ubuntu 使用的 DEB 包标识了不同的依赖，分为五类：

- Conflicts（冲突）：与某个包冲突的包（或包版本），在安装指定包时无法在系统上安装这些包。

# 添加、删除和更新软件

- **Depends（依赖）**：某个软件包正确运行所必需的包，因此在安装给定软件包时也必须安装这些包。
- **Enhances（增强）**：由于安装了某个软件包而其操作得到改进或简化的软件包，但它们之间没有直接关系。
- **Pre-Deps（前置依赖）**：在安装某个软件包之前必须在你的系统中完全安装的软件包。
- **Recommends（推荐）**：你可能需要的软件包，但对于某个软件包的正确运行并不是绝对必需的。
- **Suggestions（建议）**：可能有用的软件包，通常会安装在安装了某个软件包的系统中。

![](img/e3248f698da647444405a34229bd9df5_992_0.png)

标记为 `Pre-Deps` 的需求（很少使用或并非必要）必须在安装给定软件包之前满足。标记为 `Depends` 的需求将与给定的软件包一起自动安装。安装软件包，`aptitude` 工具允许你通过在 `aptitude install` 命令中包含 `--recommends` 命令行选项来自动安装推荐安装的软件包。

`aptitude` 工具是唯一的命令行软件包安装工具，它允许你在安装必需软件包的同时自动安装推荐软件包。在从命令行安装软件包时指定 `--recommends` 命令行选项会非常方便，如果你以后发现自己想使用某个推荐的软件包，这可以为你节省时间。对于 `apt-get`，类似于 `aptitude` 的 `--recommends` 选项以及用于安装建议软件包的相关的 `--suggests` 选项，长期以来一直被“建议”为 `apt-get` 引入，但在我见过的任何 `apt-get` 版本中都不可用。正如我将在本章关于 Synaptic 的章节中讨论的，`synaptic` 工具提供了将推荐软件包视为依赖并自动安装它们的选项；同样地，它的界面提供了一个运行时选项，可以手动选择建议软件包并将其作为软件包安装过程的一部分。

# 第三部分 面系统管理员的 Ubuntu 和 Kubuntu

# 使用 aptitude 安装和删除软件的优势

尽管我不怎么喜欢 `aptitude` 的用户界面，但 `aptitude` 本身确实提供了一些实用的功能。它的功能在本章前面的“列出你的可用软件包”部分中讨论过，既易用又强大——这正是你对一个工具所要求的。同样，当前版本的 `aptitude` 在安装特别是删除软件包方面具有某些优势。其中最显著的一点是，`aptitude` 在安装软件包时会记住依赖信息。每个 Ubuntu 软件包管理工具都会记住这些信息，并在你决定删除软件包时使用它们。

下面的示例输出显示了使用 `apt-get` 从我的 Ubuntu 系统删除 PostgreSQL 数据库系统的尝试：

```
$ apt-get remove postgresql

Password:

Reading package lists... Done

Building dependency tree... Done

The following packages will be REMOVED

postgresql

0 upgraded, 1 to remove and 0 not upgraded.

Need to get 0 of archives.

After unpacking 45.1kb disk space will be freed.

Do you want to continue [Y/n]?

Abort.
```

使用 `aptitude` 删除同一个软件包要有用得多，因为它提议删除与 `postgresql` 软件包一起安装的包，但在下面的示例中，如果使用了 `postgresql` 包，这些包在系统中已不再需要了：

```
$ aptitude remove postgresql

Reading package lists... Done

Building dependency tree... Done

Reading extended state information

Initializing package states... Done

Building database... Done

The following packages are unused and will be REMOVED:

postgresql-libperl-7.4 postgresql-python-7.4 postgresql-plt-7.4

The following packages will be REMOVED:

postgresql

0 packages, 0 newly installed, 4 to remove \
and 0 not upgraded.

Need to get 0 of archives. After unpacking 651kb will be freed.

Do you want to continue [Y/n]? Y
```
