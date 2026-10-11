
这种结构为管理员和软件包维护者带来了一些灵活性，使他们能够通过添加文件来进行软件配置更改，而无需更改现有文件。这对于软件包维护者尤其有帮助，因为他们可以使用这种方法来调整其他软件的配置，以确保其与其软件包完美共存，同时不违反明确禁止修改其他软件包配置文件的 Debian 策略。由于 `.d` 配置机制，你不必手动遵循软件包的 `/usr/share/doc/package/README-Debian` 文件中通常发现的多个软件包配置说明，因为安装程序可以放入配置文件。

> 尽管 APT 原生支持其 `/etc/apt/apt.conf.d/` 目录，但这并非总是如此。对于某些应用程序（例如 exim），`.d` 目录是 Debian 特有的添加项，用作动态生成应用程序使用的规范配置文件的输入。在这些情况下，软件包提供一个“update-”命令（例如：`update-exim4.conf`），该命令将拼接来自 `.d` 目录的文件并覆盖主配置文件。

> 在这些情况下，你不应该手动编辑主配置文件，否则你的更改将在下次执行 update- 命令时丢失，而且你在编辑 `.d` 目录之外的文件后也不得忘记运行上述命令（否则你的更改将不会生效）。

了解 `.d` 配置机制后，让我们谈谈如何利用它来配置 APT。正如我们讨论过的，你可以通过 dpkg 的命令行参数来改变 APT 的行为，如下面执行 zsh 强制覆盖安装的示例所示：

```bash
##### apt -o Dpkg::Options::="--force-overwrite" install zsh
```

显然，这非常繁琐，特别是如果你频繁使用选项的话，但你也可以使用 `.d` 目录配置结构通过向 `/etc/apt/apt.conf.d/` 目录中的文件添加指令来配置 APT 的某些方面。例如，这个（或其他任何）指令可以轻松添加到 `/etc/apt/apt.conf.d/` 中的文件中。这个文件的名称有点任意，但常见的惯例是使用 `local` 或 `99local`：

```bash
$ cat /etc/apt/apt.conf.d/99local
Dpkg::Options {
	"--force-overwrite";
}
```

还有许多其他有用的配置选项，我们显然无法涵盖所有，但我们将提及的一个涉及网络连接。例如，如果你只能通过代理访问网络，请添加一行如 `Acquire::http::proxy "http://yourproxy:3128"`。对于 FTP 代理，请使用 `Acquire::ftp::proxy "ftp://yourproxy"`。

要发现更多配置选项，请通过 `man apt.conf` 命令阅读 `apt.conf(5)` 手册页（有关手册页的详细信息，请参见第 6.1.1 节，“手册页” [第 124 页]）。

### 8.3.2. 管理软件包优先级

APT 配置中最重要的方面之一是管理与每个软件包源相关联的优先级。例如，你可能希望用来自 Debian Unstable 或 Debian Experimental 的一两个较新软件包来扩展你的 Kali Rolling 系统。可以为每个可用软件包分配优先级（相同的软件包可以根据其版本或提供该版本的发行版具有多个优先级）。这些优先级将影响 APT 的行为：对于每个软件包，它始终会选择优先级最高的版本（除非该版本比已安装的版本旧，且其优先级低于 1000）。

APT 定义了几个默认优先级。每个已安装的软件包版本的优先级为 100。未安装版本的默认优先级为 500，但如果它是目标发行版的一部分（由 `-t` 命令行选项或 `APT::Default-Release` 配置指令定义），其优先级可以跳到 990。

你可以通过在 `/etc/apt/preferences` 文件中添加条目来修改优先级，其中包含受影响软件包的名称、其版本、其来源及其新优先级。

APT 永远不会安装软件包的较旧版本（即软件包版本号低于当前已安装软件包版本号的情况），除非其优先级高于 1000。APT 始终安装符合此约束的最高优先级软件包。如果两个软件包具有相同的优先级，APT 安装最新的一个（版本号最高的）。如果两个相同版本的软件包具有相同的优先级但内容不同，APT 安装未安装的那个版本（此规则旨在涵盖不增加修订号而进行软件包更新的情况，这通常是必需的）。

更具体地说，优先级小于 0 的软件包永远不会被安装。优先级在 0 到 100 之间的软件包只有在没有该软件包的其他版本已安装时才会被安装。优先级在 100 到 500 之间，只有当没有其他较新版本的软件包已安装或在其他发行版中可用时，才会安装该软件包。优先级在 501 到 990 之间的软件包只有在目标发行版中没有较新版本已安装或可用时才会被安装。优先级在 990 到 1000 之间，除非已安装版本较新，否则该软件包将被安装。大于 1000 的优先级始终会导致安装该软件包，即使这迫使 APT 降级到较旧版本。

当 APT 检查 `/etc/apt/preferences` 时，它首先考虑最具体的条目（通常是那些指定相关软件包的），然后是更通用的条目（例如包括某个发行版的特定软件包）。如果存在多个通用条目，则使用第一个匹配项。可用的选择标准包括软件包的名称和提供该软件的源。每个软件包源都由 APT 与 `Packages` 文件一起下载的 `Release` 文件中的信息标识。这些文件指定来源，通常对于来自 Kali 官方镜像的软件包为 “Kali”，对于来自 Debian 官方镜像的软件包为 “Debian”，但对于第三方仓库，来源也可以是个人或组织的名称。`Release` 文件还提供发行版的名称及其版本。让我们通过一些关于此机制的实际案例研究来查看其语法。

#### Kali-Bleeding-Edge 和 Debian Experimental 的优先级

如果你在 `sources List` 文件中列出了 `kali-bleeding-edge` 或 Debian `experimental`，相应的软件包几乎永远不会被安装，因为其默认 APT 优先级为 1。这当然是特殊情况，旨在防止用户无意中安装最前沿的软件包。只有在输入 `apt install *package/kali-bleeding-edge*` 时才能安装这些软件包，当然假设你意识到处于前沿带来的风险和潜在麻烦。仍然可以（尽管*不推荐*）通过赋予 `kali-bleeding-edge/experimental` 软件包 500 的优先级来将其视为其他发行版的软件包。这是通过在 `/etc/apt/preferences` 中设置一个特定条目来实现的：

```
Package: *
Pin: release a=kali-bleeding-edge
Pin-Priority: 500
```

假设你只想使用来自 Kali 的软件包，并且只有在明确要求时才安装 Debian 软件包。你可以在 `/etc/apt/preferences` 文件（或 `/etc/apt/preferences.d/` 中的任何文件）中写入以下条目：

```
Package: *
Pin: release o=Kali
Pin-Priority: 900

Package: *
Pin: release o=Debian
Pin-Priority: -10
```

在最后两个示例中，您看到了 `a=kali-bleeding-edge`，它定义了所选发行版的名称；以及 `o=Kali` 和 `o=Debian`，它们分别将范围限制为源自 Kali 和 Debian 的包。

现在假设您有一台服务器，上面运行着多个依赖 Perl 5.22 版本的本地程序，您希望确保升级不会安装其其他版本。您可以使用以下条目：

```
Package: perl
Pin: version 5.22*
Pin-Priority: 1001
```

该配置文件的参考文档可在手册页 `apt_preferences(5)` 中查阅，您可以使用 `man apt_preferences` 命令显示它。

| **在 /etc/apt/preferences 中添加注释** |

|---|

| `/etc/apt/preferences` 没有官方的注释语法，但可以在每个条目前添加一个或多个 Explanation 字段来提供某些文本描述：<br>Explanation: 提供的包 xserver-xorg-video-intel<br>Explanation: 在 experimental 中可以安全使用<br>Package: xserver-xorg-video-intel<br>Pin: release a=experimental<br>Pin-Priority: 500 |

### 8.3.3. 处理多个发行版

鉴于 `apt` 是一个如此出色的工具，您很可能想要深入探索并开始尝试来自其他发行版的软件包。例如，在安装 Kali Rolling 系统后，您可能希望在不偏离系统初始状态太多的情况下，试用 Kali Dev、Debian Unstable 或 Debian Experimental 中可用的软件包。
