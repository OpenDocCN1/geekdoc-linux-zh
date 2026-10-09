
# 终端配置

使用`TC Shell (tcsh)`，将名称替换为你正在使用的终端名称。在`tcsh`下，你可以将此命令放置于`~/.login`文件中。例如，在`tcsh`下，你可以执行此命令将你的终端名称设置为`vt100`：

```
setenv TERM vt100
```

# LANG

为了让某些程序正确显示信息，你可能需要设置`LANG`变量。在`bash`下使用：

```
export LANG=C
```

在`tcsh`下使用：

```
setenv LANG C
```

![](img/bf988828a6235ca4c80ee1f4)

# 附录 C 保持系统更新

| 特性 | yum | Apt | BitTorrent |
| :--- | :--- | :--- | :--- |
| **角色** | 它们安装并更新软件包 | 它们安装并更新任何额外文件 | 分发大量的静态数据 |
| **方法** | 将仓库（通常在互联网上）中的文件与本地系统上的文件进行比较 | 根据你的指令更新本地系统上的文件 | 安装 ISO 镜像 |
| **优** | 更容易配置和使用 | 稍快，尤其是在慢连接上；支持更多功能，如撤销升级 | 不进行依赖检查 |

# yum - 更新和安装软件包

Linux 的早期版本不包含管理更新的工具。`RPM` 工具可以安装或升级单个软件包，但定位它们所依赖的软件包和更新取决于用户。当`Terra Soft`为`PowerPC`制作其`Linux`发行版时，该公司创建了`Yellow Dog Updater`来填补这一空白。该程序已移植到其他架构和发行版。结果命名为`Yum Updater (yum)`，包含在许多 Linux发行版中。`yum`的主页为`linux.duke.edu/projects/yum`，更多信息可以在`apt.freshrpm.net`获取。

# 配置 yum

`yum`工具的设计非常易于易用。配置文件`/etc/yum.conf`包含两个部分：`[main]`部分包含通用设置，文件的其余部分包含服务器列表。为了让`yum`运行，必须存在`[main]`部分。`cachedir`指定了`yum`用于存储下载的软件包的目录，`logfile`是`yum`保留日志的地方。日志记录的信息量由`debuglevel`指定，其值为`1`时产生最多的信息。

```
cat /etc/yum.conf

[main]

cachedir=/var/cache/yum

debuglevel=2

logfile=/var/log/yum.log

pkgpolicy=latest

distrepo=fedora-release

tolerant=1

exactarch=1

...
```

`pkgpolicy`定义了`yum`安装软件软件包的哪个版本；始终将其设置为`newest`以安装软件包的最新版本。你还可以配置`yum`尝试从特定服务器安装，在失败时退回到其他服务器并忽略软件包版本。`distropkg`指定了系统运行的是哪个发行版。将`tolerant`设置为`1`，`yum`会自动修正简单的命令行错误，例如尝试安装已于系统的软件包。将`tolerant`设置为`0`则关闭此项功能。将`exactarch`设置为`1`，`yum`将仅用相同架构的软件包更新软件包——例如，防止`i686`软件包替换`i386`软件包。

最后的部分包含持有更新的服务器列表。它们由`[core]`、`[updates]`或类似的标签标记。通常，最后一个部分包含尚未准备好发布的更新并被注释掉了；除非你正在测试软件包，否则不要取消注释。永远不要在生产系统中取消此部分的注释。每个服务器部分都包含`name`、`baseurl`和`gpgcheck`标志：

```
cat /etc/yum.conf

...

[core]

name=Fedora Linux $releasever - $baseurl - core

baseurl=http://yum.freshrpms.net/fedora/linux/$releasever/$baseurl/

gpgcheck=1
```

```
Is this ok [y/N]: y

Getting pango-1.6.0-7.i386.rpm

pango-1.6.0-7.i386.rpm      100% |--------------------------------| 341 kB 00:06

...
```

你可以通过在命令行`update`后面指定包名称来更新单个软件包。
要安装新软件包及其依赖的包，请使用`yum install`命令并跟上包名称，如首页所示。

```bash
#yum install tcsh

Gathering header information file(s) from server(s)

Server: Fedora Core 3 - i386 - Base

Server: Fedora Core 3 - i386 - Released Updates

Finding updated packages

Downloading needed headers

getting /var/cache/yum/base/headers/tcsh-0-6.13-9.i386.hdr

tcsh-0-6.13-9.i386.hdr      100% |--------------------------------| 3.8 kB 00:00

Resolving dependencies

Dependencies resolved

I will do the following:

[install: tcsh 6.13-9.i386

Is this ok [y/N]: y

Getting tcsh-6.13-9.i386.rpm

tcsh-6.13-9.i386.rpm      100% |--------------------------------| 443 kB 00:10

Running test transaction:

Test transaction complete, Success!

tcsh 100 % done 1/1

Installed:  tcsh 6.13-9.i386

Transaction(s) Complete
```

你也可以使用`yum`移除软件包，语法类似的的：

```bash
# yum remove tcsh
```

```bash
Gathering header information file(s) from server(s)

Server: Fedora Core 3 - i386 - Base

Server: Fedora Core 3 - i386 - Released Updates

Finding updated packages

Downloading needed headers

Resolving dependencies

Dependencies resolved

I will do the following:

[erase: tcsh 6.13-9.i386]

Is this ok [y/N]: y

Running test transaction

Test transaction complete, Success!

Erasing: tcsh 1/1

Erased: tcsh 6.13-9.i386

Transaction(s) Complete
```

![](img/bf98da8888128a6a4235ca4c80ee1f24_1082_0.png)

# APT: yum 的替代方案

`Apt`（高级软件包工具）程序可以帮助解决依赖问题：`Apt`尝试通过查找你正在安装的包所依赖的包来自动解析依赖关系。它最初作为使用`.deb`包格式的`Debian`发行版的一部分，现在`Apt`已移植到基于`rpm`的发行版中。更多信息请访问`apt.freshrpms.net`。

`Apt`工具使用`rpm`文件仓库作为其操作的基础。为了提高速度，`Apt`会维护其所使用的每个仓库中保留的软件包列表。你想要安装或更新的任何软件都存储在仓库中。

当你向`Apt`安装软件包的命令时，`Apt`会其本地包列表中查找该包。如果包出现在列表中，`Apt`将获取该包以及你正在安装的包的依赖包，并调用`rpm`安装这些包。因为`Apt`使用`rpm`，所以维护了`rpm`数据库。

# 使用 Apt

本节介绍了如何配置`Apt`。

# 安装和设置 APT

一旦你下载了`apt.rpm`文件，就必须安装它（你的`Apt`版本号会有所不同）：

```bash
# rpm -Uvh apt-0.5.15cnc16-1.1.fc3.fr.i386.rpm

Preparing...                       ########################################### [100%]

1:apt                               ########################################### [100%]
```

# 更新本地包列表

主命令是`apt-get`；其参数决定了命令的功能。安装`Apt`后，执行`apt-get update`命令来更新本地包列表：

```bash
#apt-get update

Get:1 http://ayo.freshrpms.net fedora/linux/3/i386 release [1991B]

Fetched 1991B in 0s (4922B/s)

Get:1 http://ayo.freshrpms.net fedora/linux/3/i386/core pkglist [1445KB]

Get:2 http://ayo.freshrpms.net fedora/linux/3/i386/core release [151B]
```

```bash
Get:3 http://ayo.freshrpms.net fedora/linux/3/i386/updates pkglist [251KB]

Get:4 http://ayo.freshrpms.net fedora/linux/3/i386/updates release [157B]

Get:5 http://ayo.freshrpms.net fedora/linux/3/i386/freshrpms pkglist [98KB]

Get:6 http://ayo.freshrpms.net fedora/linux/3/i386/freshrpms release [161B]

Fetched 1847kB in 28s (64.7KB/s)
```

Reading Package Lists... Done
Building Dependency Tree... Done

可用软件包经常变化，创建一个`cron`任务自动更新本地包是一个好主意。创建一个文件每天执行此任务：

```bash
$cat /etc/cron.daily/apt-update

apt-get update
```

# 检查依赖树

`Apt`工具不允许损坏的`rpm`依赖树。要检查本地依赖树的状态，运行`apt-get check`：

```bash
# #apt-get check
```

Reading Package Lists... Done
Building Dependency Tree... Done

修复`apt-get`显示的错误的最简单方法是删除错误的包，然后使用`Apt`重新安装它们。
在本书编写，`Apt`与仙境桌面不兼容。

# 更新系统

`apt-get`的两个参数可以使其更新系统上的所有软件包：`upgrade`更新不需要安装新包的系统所有软件包，而`dist-upgrade`更新系统所有软件包并安装新包。

...

当你设置此处列出的`Clean-Installed`子节时，`Apt`会移除不再于仓库中的软件包。
`Get`部分的选项使用`apt-get`工具（`apt-get`工具的命令行参数与这些选项具有相同的名称）：

- `-Assume-Yes`: 设置为`TRUE`将使`apt-get`以批处理模式运行，在其他需要提示你输入内容时自动回答`YES`。
- `-Download-Only`: 设置为`TRUE`将从仓库检索软件包但不进行安装。`FALSE`则检索并安装软件包。
- `-Show-Upgraded`: 设置为`TRUE`将获取已升级软件包的列表。
- `-Fix-Broken`: 设置为`TRUE`将尝试修复依赖树问题，成功程度不一。`FALSE`则在发现依赖树问题时退出。
- `-Ignore-Missing`: 设置为`TRUE`将保留缺失或损坏的软件包并继续安装其他软件包。`FALSE`则在发现缺失或损坏的软件包时中止安装或升级。
- `-Compile`: 设置为`TRUE`将编译并安装你要求`apt-get`获取的源`rpm (SRPM)`包。`FALSE`则仅下载这些文件而不进行编译或安装。
- `-Acquire`: `Acquire`部分控制与获取软件包相关的选项。

```bash
$cat /etc/apt/apt.conf
```

...

```
Acquire {

  Retries "0";

  Http {

    Proxy ""; // http://user:pass@host:port/

  }

};
```

`Retries`选项指定了尝试失败时重新获取软件包的次数。`Http Proxy`设置指定了使用`HTTP`获取软件包时使用的代理。该选项的参数默认为空，表示`Apt`不应使用代理。注释中显示了一个示例代理。

# RPM 部分

以下是`apt.conf`中的`RPM`节：

```bash
$cat /etc/apt/apt.conf

...

RPM {

  Ignore { };

  Hold { };

  Allow-Duplicated { "kernel$"; "kernel-"; "kmodule-"; "gpg-pukey$" };

  Options { };

  Install-Options ""

  Erase-Options ""

  Source {

    Build-Command "rpmbuild --rebuild"

  }

}
```
