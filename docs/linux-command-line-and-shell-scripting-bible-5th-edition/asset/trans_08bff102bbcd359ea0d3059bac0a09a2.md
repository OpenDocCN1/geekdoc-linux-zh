

## 使用 apt 安装软件包

既然您已经了解了如何列出系统中的软件包信息，本节将指导您完成软件包的安装。首先，您需要确定要安装的软件包名称。如何找到特定的软件包？请结合搜索命令使用 apt：

```
apt search package_name
```

搜索命令的美妙之处在于，您无需在 `package_name` 周围插入通配符。系统隐含了通配符。默认情况下，搜索命令会显示那些名称或描述中包含搜索词的包，这在某些时候可能会造成误导。如果您希望将输出限制为仅显示包名称，请包含 `--names-only` 选项：

```
$ apt --names-only search zsh
Sorting ... Done
Full Text Search ... Done

fizzsh/noble 1.0.9-1 all
    友好的交互式 ZSHell

python3-colcon-zsh/noble 0.5.0.1-1 all
    集体构建元构建工具 - zsh 扩展

zsh/noble,now 5.9-6ubuntu2 amd64 [installed]
    拥有众多功能的 shell

zsh-antidote/noble 1.9.4-1 all
    ZSH 插件管理器

zsh-antigen/noble 2.2.3-5 all
    管理您的 zsh 插件

zsh-autosuggestions/noble 0.7.0-1 all
    类似 Fish 的快速/侵入式 zsh 自动建议

zsh-common/noble,now 5.9-6ubuntu2 all [installed,automatic]
    Zsh 的架构无关文件

zsh-dev/noble 5.9-6ubuntu2 amd64
    拥有众多功能的 shell（开发文件）

zsh-doc/noble 5.9-6ubuntu2 all
    zsh 文档 - info/HTML 格式

zsh-static/noble 5.9-6ubuntu2 amd64
    拥有众多功能的 shell（静态链接）

zsh-syntax-highlighting/noble 0.7.1-2 all
    类似 Fish shell 的 zsh 语法高亮

zsh-theme-powerlevel9k/noble 0.6.7-4 all
powerlevel9k 是一个使用 powerline 字体的 zsh 主题
$
```

一旦找到了您想要安装的软件包，使用 apt 进行安装就很简单了：

```
apt install _package_name_
```

输出结果将显示有关该软件包的基本信息，并询问您是否要继续安装：

```
$ sudo apt install zsh
正在读取软件包列表... 完成
正在构建依赖树... 完成
正在读取状态信息... 完成
以下软件包是自动安装的，现在不再需要：
libllvm17t64 python3-netifaces
使用 'sudo apt autoremove' 将其移除。
建议安装的软件包：
zsh-doc
以下新的软件包将被安装：
zsh
0 升级，1 新安装，0 移除，1 未升级。
需要获取 812 kB 的归档。
此操作完成后，将额外使用 2,489 kB 的磁盘空间。
获取:1 http://us.archive.ubuntu.com/ubuntu noble/main amd64 zsh amd64
5.9-6ubuntu2 [812 KB]
在 1s 内获取了 812 kB (1,137 kB/s)
选择之前未选择的软件包 zsh。
(正在读取数据库 ... 当前已安装 209759 个文件和目录。)
正在准备解包 .../zsh 5.9-6ubuntu2_amd64.deb ...
正在解包 zsh (5.9-6ubuntu2) ...
正在设置 zsh (5.9-6ubuntu2) ...
正在处理 debutils (5.17build1) 的触发器 ...
正在处理 man-db (2.12.0-4build2) 的触发器 ...$
```

> **注意**
> 
> 在上面的列表中的 *apt* 命令之前，使用了 *sudo* 命令。*sudo* 命令允许您以 root 用户身份运行命令。您可以使用 *sudo* 命令执行管理任务，例如安装软件。

要检查安装是否成功处理，只需再次使用带有 `--installed` 选项的 `list` 命令即可。您应该看到该软件包出现，表明它已安装。

请注意，当安装所需的软件包时，*apt* 还要求安装其他软件包。这是因为 *apt* 会自动解决必要的软件包依赖关系，并安装所需的额外库和软件包。这是许多包管理系统中包含的一项出色功能。

## 使用 apt 升级软件

虽然 apt 有助于保护您避免在安装软件时出现问题，但尝试协调带有依赖关系的多软件包更新可能会变得复杂。要安全地升级系统中所有具有仓库新版本软件包，请使用 upgrade 命令：

```
apt upgrade
```

请注意，该命令不接受任何软件包名称作为参数。这是因为 upgrade 选项不会将所有已安装的软件包升级到仓库中可用的最新版本，这对于系统稳定性来说更安全。

以下是运行 apt upgrade 命令的示例输出：

```
$ sudo apt upgrade
正在读取软件包列表... 完成
正在构建依赖树... 完成
正在读取状态信息... 完成
正在计算升级... 完成
以下软件包是自动安装的，现在不再需要：
  libllvm17t64 python3-netifaces
使用 'sudo apt autoremove' 将其移除。
启用 'esm-apps' 可通过 Ubuntu Pro 获取更多安全更新：
  php-symfony-config libzvbl-common php-symfony-dependency-injection libjson1
  php-symfony-cache php-symfony-var-exporter libgpg-error0 php-twig
  libavcodec60 libavdevice60 libavutil58 libswscale7
  php-symfony-expression libswresample4 libavformat60 libavfilter9
  php-symfony-filesystem
在 https://ubuntu.com/pro 了解有关 Ubuntu Pro 的更多信息
以下新的软件包将被安装：
  linux-headers-6.11.0-26-generic linux-headers-6.11.1-headers-6.11.0-26
  linux-hwe-6.11-tools-6.11.0-26 linux-image-6.11.0-26-generic
  linux-modules-6.11.0-26-generic linux-modules-extra-6.11.0-26-generic
  linux-tools-6.11.0-26-generic
以下升级已因阶段控制而推迟：
  ubuntu-drivers-common
以下软件包将被升级：
  apparmor apparmor-profiles apparmor-utils binutils binutils-common
  binutils-x86-64-linux-gnu cloud-init distro-info-data fwupd ghostscript
  gir1.2-glib-2.0 gir1.2-gtk-3.0 gir1.2-gtk-4.0 gir1.2-javascriptcoregtk-4.1
  gir1.2-javascriptcoregtk-6.0 gir1.2-mutter-14 gir1.2-soup-3.0
  gir1.2-webkit-6.0 gir1.2-webkit-4.1 gnome-control-center
  gnome-control-center-data gnome-control-center-faces gnome-shell
  gnome-shell-common gnome-shell-extension-ubuntu-dock grub-common grub-pc
  grub-pc-bin grub2-common libapparmor-lts libmcsctl-microcode
  libabi32t64 libc6v2 libgccv10.1 libgccm2c7 libgccs2 libgccs1 libgccd0 libccrt-noabid5
  ...
122 升级，7 新安装，0 移除，1 未升级。
需要获取 880 MB 的归档。
此操作完成后，将额外使用 319 MB 的磁盘空间。
您想继续吗？[Y/n]
```

在输出中，请注意 **apt** 列出了将要升级的软件包，同时也列出了因升级而必须安装的任何新软件包。

**upgrade** 命令不会作为升级过程的一部分移除任何软件包。如果作为升级的一部分需要移除软件包，请使用此命令：

```
apt full-upgrade
```

虽然这看起来可能有点奇怪，但有时为了保持发行版升级之间的同步，移除软件包是必要的。

**注意**

显然，运行 **apt** 的 **upgrade** 选项是定期执行的事情，以保持您的系统处于最新状态。然而，在刚安装完发行版后运行它尤为重要。通常，自上次完整发布以来，已经发布了许多安全补丁和更新。此外，建议先运行 **update** 选项，该选项会更新仓库列表，以确保 **apt** 正在使用最新的仓库。

## 使用 apt 卸载软件

使用 **apt** 移除软件包与安装和升级它们一样简单。您真正需要做的唯一选择是之后是否保留软件的数据和配置文件。

若要移除软件包但不保留数据和配置文件，请使用 **apt** 的 **remove** 命令。若要移除软件包以及相关的的数据和配置文件，请使用 **purge** 选项：

```
$ sudo apt purge zsh
正在读取软件包列表... 完成
正在构建依赖树... 完成
正在读取状态信息... 完成
以下软件包是自动安装的，现在不再需要：
  libllvm17t64 python3-netifaces zsh-common
使用 'sudo apt autoremove' 将其移除。
以下软件包将被移除：
  zsh*
0 升级，0 新安装，1 移除，123 未升级。
此操作完成后，将释放 2,489 kB 的磁盘空间。
您想继续吗？[Y/n] Y
(正在读取数据库 ... 当前已安装 209817 个文件和目录。)
正在移除 zsh (5.9-6ubuntu2) ...
正在处理 debianutils (5.17build1) 的触发器 ...
正在处理 man-db (2.12.0-4build2) 的触发器 ...
(正在读取数据库 ... 当前已安装 209759 个文件和目录。)
正在清除 zsh (5.9-6ubuntu2) 的配置文件 ...
$
```

