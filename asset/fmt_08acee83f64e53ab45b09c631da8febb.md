
```
$ michael@debians:~/home/michael apt-cache showpkg synaptic
Package: synaptic
0.55cve20050208-1:/var/lib/apt/lists/debian.oregonstate.edu_debian_dist_test-
main_binary-1386:/var/lib/dpkg/status
Reverse Suggests:
 apt-synaptic,0.53.4
0.55cve20050208-1|lib-apt-libkb:6.2.3-2 (0 null)|lib64-libapt-1.0 (0 null)|1.7.2-1
|libapt2.2:2.2.1:2.2.1 (0 null)|libapt6-2:2.1.0 (0 null)|lib64-libapt:1.7.2-1
|libapt2-2:2.2.1.2.2.2.2:2.2.0 (0 null)|libapt6-2:2.6.0 (0 null)|0 0 2.2.1-n|||2...:.....116 (0 null)|libapt6:4.1.0 (0 null)|libapt2-4:2.1.0 (0002.2.0000000000.......11 (11 ( ( ( ( ( ( ( ( ( (0n)
synaptic (0 null)|
2-perl|apt-cache (0 null)|synaptic (0 null)
Provides:
 apt-synaptic, synaptic
Reverse Provides:
 debian:/home/michael#|
```

`图 5-9` 使用`apt-cache`列出版本和依赖关系

与`synaptic`相关的内容分为以下五类：

- `Versions`（版本）：指定了从你的存储库中提供的`synaptic`包的不同版本。
- `Reverse depends`（反向依赖）：列出了依赖于`synaptic`的包，或者你计划安装的包。
- `Dependencies`（依赖关系）：指定了在安装`synaptic`之前需要的那些包。
- `Provides`（提供）：列出了该包提供的软件包和关键文件。
- `Reverse provides`（反向提供）：列出了依赖于你正在安装内容的包。

### `apt-cache showsrc`

当你运行`apt-cache showsrc packagename`命令时，`apt-cache`会搜索可用的源包数据库，这些数据库是从`/etc/apt/sources.list`中指定的源仓库下载的；该文件中的源仓库应与`deb-src`或`rpm-src`命令相关联。

除此之外，输出包含了构建二进制包所需的源文件名称以及`Build-Dependencies`（构建依赖），其中包含了构建特定包所需的那些包和库。

### `apt-cache show`

如果你想获取有关可用软件包的更多信息，`show`选项适合你。当你运行`apt-cache show packagename`命令时，该包不需要安装。你只需要指定包名即可。

### `apt-cache depends`

如果你想获取可用软件包的更多信息，`show`选项适合你。当你运行`apt-cache show packagename`命令时，该包不需要安装。你只需要指定包名即可。

### `apt-cache repends`

如果你想获取可用软件包的更多信息，`show`选项适合你。当你运行`apt-cache show packagename`命令时，该包不需要安装。你只需要指定包名即可。

### `apt-cache pknames`

`apt-cache pknames`命令本身是有用的。它会搜索存储库中的可用包。例如，如果你想过滤结果，可以使用以下命令：

```
apt-cache pknames | grep gimp
```

### 5.4.2 详细分析 `apt-get`

花点研究一下`apt-cache`命令可以做什么是值得的。你可以通过`apt-cache -h | less`命令查看大多数可用选项。这个列表并不完整；你在本章前面的部分已经学习了`showgroup`和`groupnames`，并在第 4 章中学习了`search`。有几个选项很少使用，因为其他命令可能更有用。因此，本书中没有涵盖几个`apt-cache`选项。

默认的`apt-get`选项存在于`/etc/apt.conf`或目录。自然地，你可以使用正确的开关来覆盖这些默认值。

### `apt-get` Switches

在讨论选项之前，`apt-get`有许多可用开关，如表 5-3 所示。

#### 表 5-3 `apt-get` Switches

| 开关 | 说明 |
| :--- | :--- |
| `-d` | 下载但不安装任何包 |
| `-f` | 尝试修复损坏的依赖关系 |
| `-m` | 忽略不下载任何包或下载错误的包 |
| `-Q` | 在下载安装过程中静默所有消息 |
| `-s` | 模拟下载和安装 |
| `-y` | 对所有提示回答是是 |
| `-u` | 列出所有升级的包 |
| `-V` | 显示升级的完整版本号（当前和未来的） |
| `--no-upgrade` | 不执行升级 |
| `--purge` | 清除删除包，包括相应的配置文件 |
| `--reinstall` | 重装已是最新版本的包；替换所有缺失的配置文件 |
| `--no-remove` | 如果删除了包，进程将自动终止 |
| `--config-file` | 如果你设置了`apt.conf`的替代方案，使用此开关指定它 |

### `apt-get upgrade`

我通常不建议使用`apt-get upgrade`命令，因为会导致大多数已安装的包升级到新版本。然而，此选项不会删除任何已安装的包；升级需要哪些

### `apt-get dist-upgrade`

如果你准备好升级系统，`apt-get dist-upgrade`命令可能适合你。它提供了通过`Synaptic`包管理器提供的“智能升级”选项。详细选项涉及到仅适用于 Debian 类型的发行版的`apt-preferences`命令的使用。由于升级通常涉及数百个包，某些冲突是不可避免的。通过智能升级功能，更重要包的升级具有优先级。

### `apt-get check`

如果你在使用依赖时遇到问题，请运行`apt-get check`命令。它可以更新当前的软件包缓存并列出所有未满足的依赖项。

### 5.4.3 仅限 Debian 的 `apt` 命令

对于 Debian 类型发行版，有多个`apt`相关的命令。虽然`Conectiva`已将这些命令大部分移植到其基于 RPM 的发行版中，但它们通常在其他基于 RPM 的发行版中不可。它们包含了第 4 章中描述的几个命令，包括：

- `apt-build`下载与特定下载相关的源码和构建包，并针对特定架构进行了优化。
- `apt-ftarchive`为基于`apt`的存档生成索引文件。如前所述，对应的 RPM 的命令是`genbasidir`，它是`apt-server` RPM 软件包的一部分。
- `apt-howto`包含最新版本的 APT HOWTO；你也可以从`www.debian.org/doc/manuals/apt-howto`获取它。
- `apt-listbugs`通常不会单独运行；安装后，它会被其他`apt`命令自动调用以下载构建报告。

### 5.4.4 仅限 RPM 的 `apt` 命令

有三个`apt`脚本仅适用于基于 RPM 的发行版。截至本文写作，它们尚未移植到基于 Debian 的发行版。根据发行版的不同，它们可能作为`apt`或`apt-server` RPM 软件包的一部分可用。这些脚本如下：

- `genbasidir`在章的早期描述过；它允许你创建一个适用于`apt`仓库的数据库。
- `genpkg`通过`genbasidir`运行以创建软件包列表存档。
- `gensclist`同样通过`genbasidir`运行以创建源程序包存档。

### 5.5 总结

在本章中，你学习了如何将`apt`知识扩展到基于 RPM 的发行版。这是解决安装 RPM 软件包时经常遇到的“依赖地狱”的替代方案。巴西`Conectiva` Linux 开发者的工作使这一切成为可能。你现在可以使用`apt`来保持`SUSE`、`Fedora`甚至某些`Red Hat Enterprise Linux`的重新编译版发行版处于最新状态。

多个发行版背后的开发者已经配置了自身的`apt`仓库并将其放在网上。独立开发者还配置了额外的`apt`仓库，供你使用并在你的本地网络上进行镜像同步。

如果你的发行版没有可用的`apt`仓库，你可以创建自己的。你仍然可以在你的网络上创建一个标准仓库的镜像。通过`genbasir`命令并花一点精力将软件包组织到本地目录中，你可以创建出数据库，从而让你的本地镜像作为`apt`仓库时变得有用。
