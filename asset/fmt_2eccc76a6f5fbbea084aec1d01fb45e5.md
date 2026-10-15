
对于更重要的升级，如主要版本升级，使用 `apt full-upgrade`。使用此指令，即使需要删除某些过时包或安装新依赖项，`apt` 也将完成升级。这也是你应该用于 Kali Rolling 系统常规升级的命令。它非常简单，几乎不需要解释：`APT` 的声誉基于此强大功能。

与 `apt` 和 `aptitude` 不同，`apt-get` 不认识 `full-upgrade` 命令。相反，你应该使用 `apt-get dist-upgrade`（发行版升级），这是一个众所周知的命令，`apt` 和 `aptitude` 也接受此命令以保持向后兼容性。

> **注意重要变更** 为了预见其中一些问题，你可以安装 `apt-listchanges` 包，它会在包升级开始时显示关于潜在问题的信息。此信息由包维护人员编译并放入 `/usr/share/doc/package/NEWS`。Debian 文件旨在供你受益。阅读这些文件（可能通过 `apt-listchanges`）应有助于你避免不愉快的意外。

自成为滚动发行版以来，Kali 每天可以接收多次升级。然而，这可能不是最佳策略。那么，你应该多久升级一次 Kali Linux？没有硬性规定，但有一些指导原则可以帮助你。你应该在以下情况下升级：

- 当你意识到某个安全问题已在更新中修复时
- 当你怀疑更新版本可能修复你正在经历的 bug 时
- 在报告 bug 之前，以确保它在你可获得的最新版本中仍然存在
- 频率足够高，以确保获取你尚未听说过的安全修复

也存在最好不升级的情况。例如，以下情况下可能不建议升级：

- 如果你无法承受任何破坏（例如，因为你需要离线，或者你即将用电脑进行演示）；最好在之后你有足够时间排查过程中引入的任何问题时再执行升级。
- 如果最近发生了（或仍在进行中）破坏性变更，且你担心并非所有问题都已被发现。例如，当发布新版本的 GNOME 时，并非所有软件包都会同时更新，你很可能会遇到旧版本和新版本软件包的混合情况。大多数时候这没问题，也有助于大家渐进式地发布这些更新，但总有例外，某些应用程序可能会因这种不一致而损坏。
- 如果 `apt full-upgrade` 的输出告诉你它将移除你认为对工作重要的软件包。在这种情况下，你需要审查该情况并尝试理解 `apt` 为什么想要移除它们。也许这些软件包目前处于损坏状态，这种情况下你可能希望等待修复版本可用；或者它们已被废弃，你应该找出它们的替代方案，然后无论如何继续执行完整升级。

通常，我们建议你每周至少升级一次 Kali。你当然可以每天升级，但更频繁地执行没有意义。即使镜像每天同步四次，来自 Debian 的更新通常也只是一天到达一次。

### 8.2.4. 移除和清除软件包

移除软件包比安装软件包还要简单。让我们看看如何使用 `dpkg` 和 `apt` 移除软件包。

若要使用 `dpkg` 移除软件包，请提供 `-r` 或 `--remove` 选项，后跟软件包名称。然而，这种移除并不完全：所有配置文件、维护脚本、日志文件（系统日志）、由守护进程生成的数据（例如 LDAP 服务器目录的内容或 SQL 服务器数据库的内容）以及该软件包处理的大多数其他用户数据都保持完整。移除选项使得卸载程序后使用相同配置重新安装变得容易。请记住，依赖项不会被移除。考虑以下示例：

```bash
##### dpkg --remove kali-linux-gpu
(Reading database ... 317681 files and directories currently installed.)
Removing kali-linux-gpu (2016.3.2) ...
```

你还可以使用 `apt remove package` 从系统中移除软件包。APT 将自动删除依赖于被移除软件包的软件包。与 `dpkg` 示例一样，配置文件和用户数据不会被移除。

通过对软件包名称添加后缀，你可以使用 `apt`（或 `apt-get` 和 `aptitude`）在同一命令行上安装某些软件包并移除其他软件包。在 `apt install` 命令中，在你想移除的软件包名称前添加“ -”。在 `apt remove` 命令中，在你想安装的软件包名称前添加“ +”。

下一个示例展示了安装 `package1` 并移除 `package2` 的两种不同方法。

```bash
##### apt install package1 package2-
[...]
##### apt remove package1+ package2
[...]
```

这也可以用于排除其他情况下会被安装的软件包，例如由于推荐依赖（Recommend，稍后讨论）。通常，依赖解析器会将此信息作为提示，以寻找替代解决方案。

若要移除与软件包关联的所有数据，你可以使用 `dpkg -P package` 或 `apt purge package` 命令清除该软件包。这将完全移除软件包及所有用户数据，对于 apt 而言，还会删除依赖项。

```bash
##### dpkg -r debian-cd
(Reading database ... 97747 files and directories currently installed.)
Removing debian-cd (3.1.17) ...

##### dpkg -P debian-cd
(Reading database ... 97401 files and directories currently installed.)
Removing debian-cd (3.1.17) ...
Purging configuration files for debian-cd (3.1.17) ...
```

**警告！** 鉴于清除操作的不可逆性质，请谨慎执行。你将失去与该软件包相关的一切。

### 8.2.5. 检查软件包

接下来，让我们看看一些可用于检查 Debian 软件包的工具。我们将了解用于查询和可视化软件包数据库的 `dpkg`、`apt` 和 `apt-cache` 命令。

#### 查询 `dpkg` 数据库并检查 `.deb` 文件

我们将从几个查询内部 `dpkg` 数据库的 `dpkg` 选项开始。该数据库位于文件系统上的 `/var/lib/dpkg`，包含多个部分，包括配置脚本（`/var/lib/dpkg/info`）、软件包安装的文件列表（`/var/lib/dpkg/info/*`）以及已安装软件包的状态（`/var/lib/dpkg/status`）。你可以使用 `dpkg` 与该数据库中的文件进行交互。请注意，大多数选项都有长版本（一个或多个相关单词，前面带有双破折号）和短版本（单个字母，通常是长版本中某个单词的首字母，前面带有单破折号）。这一约定非常普遍，是 POSIX 标准。

首先，让我们看看 `--listfiles package`（或 `-L`），它列出由指定软件包安装的文件：

```bash
$ dpkg -L base-passwd
/.
/usr
/usr/sbin
/usr/sbin/update-passwd
/usr/share
/usr/share/lintian
/usr/share/lintian/overrides
/usr/share/lintian/overrides/base-passwd
/usr/share/doc-base
/usr/share/doc-base/users-and-groups
/usr/share/base-passwd
/usr/share/base-passwd/group.master
/usr/share/base-passwd/passwd.master
/usr/share/man
/usr/share/man/pl
/usr/share/man/pl/man8
/usr/share/man/pl/man8/update-passwd.8.gz
[...]
/usr/share/doc
/usr/share/doc/base-passwd
/usr/share/doc/base-passwd/users-and-groups.txt.gz
/usr/share/doc/base-passwd/changeLog.gz
/usr/share/doc/base-passwd/copyright
/usr/share/doc/base-passwd/README
/usr/share/doc/base-passwd/users-and-groups.html
```

接下来，`dpkg --search file`（或 `-S`）查找包含参数中传入的文件或路径的任何软件包。例如，要查找包含 `/bin/date` 的软件包：

```bash
$ dpkg -S /bin/date
coreutils: /bin/date
```

`dpkg --status package`（或 `-s`）命令显示已安装软件包的头部信息。例如，要查找 coreutils 软件包的头部信息：
