
## 关于为什么某个更新是合理的说明

可以在 `updates` 目录下的 `README` 文件中找到。以下是简要总结：

- `apache` 安全问题
- `rotate` 偶尔故障
- `NetKit-B` 安全问题
- `rpm` 验证功能（verify function）问题
- `sendmail` 安全问题
- `slilogin` 无谓限制，错误的文档
- `timeconfig` 故障

进一步的更新可能会出现在 `RedHat` `ftp` 服务器上，用于编译随书的 CD-ROM。如果你可以访问互联网，你应该咨询以下 `WWW` 页面：

`http://www.redhat.com/support/docs/errata.html`

在你真正对你的 `Linux` 系统感到自在之前，还有很多工作要做。在许多示例中，特殊键（如 `Backspace`、`Del`、`Home` 和 `End`）的行为并不令人满意（达到预期效果），`x` 中的黑色背景不理想。这些细节的详细描述见第 6 章。

# 模块化内核

像大多数发行版一样，`RedHat` 现在使用模块化内核。这意味着，通常情况下，不再需要重新编译内核。在设置时区时，你必须指定……关于模块化内核的配置，可以查阅 `updates` 目录的 `README`。

进一步的更新可能会出现在 `RedHat` `ftp` 服务器上，用于编译随书的 CD-ROM。如果你可以访问互联网，你应该咨询以下 `WWW` 页面：

`http://www.redhat.com/support/docs/errata.html`

在你真正对你的 `Linux` 系统感到自在之前，还有很多工作要做。在许多示例中，特殊键（如 `Backspace`、`Del`、`Home` 和 `End`）的行为并不令人满意（达到预期效果），`x` 中的黑色背景不理想。这些细节的详细描述见第 6 章。

## 可插式认证模块 (PAM)

从第 4 版本开始，`RedHat` 配备了新的 `PAM` 工具用于用户认证（登录等）。`PAM` 允许引入新且更安全的系统。`PAM` 的配置通过 `/etc/pam.conf` 文件进行。关于 `PAM` 的文档非常少，可以在 `/usr/doc/pam` 中找到。（关于 `PAM` 的更多信息可以在 `RedHat` 的 `WWW` 服务器 `www.redhat.com` 上找到。）

首次，对 `PAM` 的更改对大多数用户没有产生影响。然而，您应该始终使用提供的工具来注册新用户（例如在文本模式下使用 `adduser name and password`，或在 `X` 环境下使用 `usercfg`）。

## 控制面板 (`fstools`, `netcfg`, `printtool`, ...)

配置的一部分可以通过控制面板中组合的一系列工具完成。这些程序仅在 `X` 环境下可用，并由 `root` 用户执行。程序代码位于 `/usr/lib/rhs`。这些程序中的一些也包含其他发行版中。

这些工具允许方便地配置文件系统、网络、打印机、调制解调器和用户账户（登录）。尽管界面漂亮，但处理这些程序需要扎实的基础知识。如有疑问，请查阅有关相关文件手动配置章节（第 6 章！）。

即使按照第 6 章和第 7.1 节配置了键盘，`Del` 键和 `Backspace` 键在几个 `RedHat` 配置程序（`netcfg`、`fstools` 等）中也无法正常工作。在这种情况下，错误不是缺少配置，而是配置错误：文件 `/usr/lib/rhs/control-panel/bindings.ctl` 两次包含了 `bind text <Delete>` 和 `bind text <Backspace>` 指令，必须将其注释掉！

## 控制面板

该程序（命令名 `control-panel`）唯一的功能是允许方便地启动其他工具。显然，只需输入文件名即可启动。

## 用户账户管理

通过 `usercfg`，您可以注册新用户、激活和禁用用户（后者会挂起登录）等。该程序修改 `/etc/passwd` 和 `/etc/group` 文件。作为标准，它会为每个用户创建一个同名组，并将他们分配到用户组中。可以方便地添加其他组组（另见第 136 页）。

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_636_0.png)

## 612 附 A：`REDHAT` 4.1

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_637_0.png)

图 A.1 控制面板和一些重要工具。

### 文件系统管理

`fstools` 允许编辑 `/etc/fstab` 文件并挂载新的文件系统（包括 `NFS`）。在首次启动时，程序会为找到每个分区插入一行。随后，您可以点击这些行并进行编辑。

### 网络管理

通过 `netcfg`，您可以设置主机名、构建网络接口（以太网、`PPP`、`SLIP`）等。`netcfg` 修改 `/etc/HOSTNAME`、`/etc/hosts`、`/etc/resolv.conf`、`/etc/sysconfig/network` 以及 `/etc/sysconfig/network-scripts` 目录下的文件。

如果您手动编辑了配置文件而没有其他操作，有一些提示：在 `/etc/hosts` 中，指定的名称必须分配给运行中网络的有效 `IP` 地址。（简单地 `ping $HOSTNAME` 可）在未连接网络的计算机上，回环掩码必须分配本地主机名和计算机名称（两行）。

在系统启动期间，只有当 `/etc/sysconfig/network-scripts` 包含 `ifcfg-eth0` 文件并指定网络参数分配时，才会建立与本地网络的连接！（此文件由 `netcfg` 创建/删除。）如果您遇到问题，请参考关于 `System V init` 过程的基础章节（第 119 页）和关于网络配置章节（第 150 页）。

## 打印机配置

`printtool` 用于设置打印机（通过网络）。更改应用于 `/etc/printcap` 和 `/var/spool/lpd/lp/filter` 文件。如果您没有 `PostScript` 打印机，将调用 `gs` 来转换您的打印机的 `PostScript` 格式。因此，只能打印 `PostScript` 文件。文本文件之前可以通过 `mpage` 转换为 `PostScript` 格式。

## `Init` 进程管理

`tksys` 是一个易于处理的控制 `init` 进程（`System V`）的程序。通过鼠标点击，您可以指定运行级别（`runlevel`）启动/停止哪些进程/守护进程。但不要被漂亮的界面所迷惑：更改 `init` 进程需要非常深入的知识！`HELP` 命令提供了 `System V init` 进程的简短描述；更多信息见第 118 页。

## 内核守护进程管理

原则上，`kernelcfg` 的说明也适用于 `tksys`：仅供专家使用！此程序可配置内核守护进程，负责根据需要自动加载内核模块。`kernelcfg` 修改配置文件 `/etc/conf.modules`。

## 调制解调器接口设置

通过 `modemtool`，您可以为调制解调器选择串口接口。该程序简单地创建一个从 `/dev/modem` 到接口 `/dev/cuan` 的链接。

## 设置系统时间

通过 `timtool`，您可以设置系统时间。在启动程序之前，您应该终止所有运行中的进程。

## 查找在线文档

`helptool` 帮助查找在线文档。该程序提供 `HTML` 文档。

![](img/dbea4db79f2183ab7081a3efe6a8_638_0.png)

## 软件包管理 (`rpm` 和 `glint`)

`RedHat` 发行版最突出的特点是其软件包管理。在其他发行版中没有如此方便地安装新包、检查现有包、更新包或删除包。软件包管理基于两个程序：负责管理的 `rpm` 和提供图形界面的 `glint`。

- `rpm` 和 `glint` 仍在开发中。以下描述涉及 `rpm` 版本 2.3 和 `glint` 版本 2.1.5。

在 `Linux` 用户中，`*.rpm` 文件已获得地位。尽管它们具有不可争议的优势，但也有一个致命缺点：它们不如构成所有发行版的 `*.tgz` 文件那样具有移植性。如有必要，可以使用 `tar` 直接安装 `*.tgz` 文件，而无需依赖发行版的工具。凭借经验，可以在 `RedHat` 上安装 `SuSE` 并使其运行。但在非 `RedHat` 发行版上使用 `rpm` 包要复杂得多。此外，`rpm` 无法提供 `tar` 的相同功能。例如，目前无法安装单个文件——您必须安装整个软件包。

大量的当前软件包可以通过互联网获取——直接从 `RedHat` 的 `ftp` 服务器或各种镜像服务器获取。
