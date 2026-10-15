

| 驱动名称 | 描述 |
| :--- | :--- |
| `generic3` | 通用三按钮串行鼠标 |
| `genericsps/2` | 通用双按钮 PS/2 鼠标 |
| `generic3ps/2` | 通用三按钮 PS/2 鼠标 |
| `geniusnm` | 串行 Genius Netmouse |
| `geniusnmps/2` | PS/2 Genius Netmouse |
| `geniusnpsps/2` | PS/2 Genius Netmouse Pro |
| `thinking` | 串行 Kensington Thinking Mouse |
| `thinkingps/2` | PS/2 Kensington Thinking Mouse |
| `logitech` | 串行 C7 Logitech 鼠标 |
| `logitechcc` | 串行 CC Logitech 鼠标 |
| `logibm` | Logitech 总线 (PS/2) 鼠标 |
| `logimman` | 串行 Logitech MouseMan/FirstMouse |
| `logimmanps/2` | PS/2 Logitech MouseMan/FirstMouse |
| `logimman+` | 串行 Logitech MouseMan+/FirstMouse+ |
| `logimman+ps/2` | PS/2 Logitech MouseMan+/FirstMouse+ |
| `microsoft` | 兼容 Microsoft 的串行鼠标 |
| `msnew` | Microsoft 串行鼠标 Revision 2.1A 或更高版本 |
| `msintelli` | 串行 Microsoft IntelliMouse |
| `msintellips/2` | PS/2 Microsoft IntelliMouse |
| `msbm` | Microsoft 总线 (PS/2) 鼠标 |
| `mousesytems` | 串行 Mouse Systems 鼠标 |
| `mmseries` | 串行 MM Series 鼠标 |
| `mmhittab` | 串行 MM HitTablet 鼠标 |

鼠标识别之后是时区，通过 `timezone` 项进行设置。根据你所在的国家以及该国是否足够大以跨越多个时区，有许多选项可供选择。一些常用的时区如图 10.1 所示——对于其他时区，请运行 `timeconfig` 命令来找到你的时区。同时，你可以添加 `--utc` 标志来告诉系统使用格林尼治标准时间 (GMT)。在我的 KickStart 文件中，这一行可能看起来像这样：

```
timezone --utc Canada/Pacific
```

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_329_0.png)

视频信息的设置更为复杂；复杂程度取决于你的硬件自动探测的情况如何。无论如何，这种设置仅仅依赖于了解你的硬件并进行研究。X 配置行以 `xconf` 开头。虽然你可以保持原样，但最终你会得到一张自动探测的视频卡（希望如此）和通用的 640x480 视频模式。与 `xconf` 项配套的可用选项如下：

- `--card`：识别你的视频卡的信息。你只需要此选项或 `--server` 选项其中之一，而不是两者都要。
- `--hsync`：你的监视器的水平同步频率。仅当监视器类型不在列表中时才需要此项和 `--vsync`。数字应为逗号分隔的列表或带破折号的范围。
- `--monitor`：识别你的视频显示的信息。如果你有此信息，就不需要 `--vsync` 或 `--hsync`。
- `--server`：安装哪个 X 服务器的说明。你只需要此选项或 `--card` 选项其中之一，而不是两者都要。
- `--vsync`：你的监视器的垂直同步频率。仅当监视器类型不在列表中时才需要此项和 `--hsync`。数字应为逗号分隔的列表或带破折号的范围。

监视器和视频卡太多，无法在此处列出全部。输入以下命令可将所有选项的列表保存到 `/root/xhardware` 文件中：

```
Xconfigurator --help 2> /root/xhardware
```

> **注意：** 你需要包含 `2>`，因为仅 `Xconfigurator --help` 会将信息发送到 STDERR，而不是 STDOUT，因此标准的 `>` 重定向将不起作用。

与这些选项相关的所有值都需要用引号括起来。在最简单的情况下，监视器类型已知且视频卡正确探测，你可以使用以下内容：

```
xconfig --monitor "mag DX700T"
```

现在，你需要设置 `root` 密码。虽然加密和非加密选项都可用，但如果通过网络安装，最好发送加密版本。如果你只是使用软盘和 CD-ROM 在本地安装，则不需要加密。设置此密码的语句是 `rootpw`，它可以以两种方式之一使用。对于非加密密码，输入以下内容：

```
rootpw password
```

如果你希望密码经过加密，首先你需要在另一台机器上的某个账户设置此密码。然后，打开 `/etc/shadow` 或 `/etc/passwd`，并复制密码的加密版本，如下所示：

```
rootpw --iscrypted encryptedpassword
```

遵循同样的主题，下一项涉及机器如何处理身份验证。处理身份验证的基本语句是 `auth`。此语句有三个主要选项：NIS（参见第 16 章）、`shadow` 密码和 `MD5` 密码（参见第 9 章）。如果你希望使用 `shadow` 密码——强烈建议如此，除非你使用的特定工具不支持——请包含标志 `--usesshadow`。若要包含 `MD5`——同样建议——请使用标志 `--enablemd5`。

如果你希望使用 `NIS` 来集中管理网络管理目的的用户，首先添加标志 `--enablisis`。然后，你需要包含标志 `--nismdomain` `domain`，其中 `domain` 是分配给你的 NIS 域的名称。你还需要 `--nisservice` `server`，其中 `server` 是你的 NIS 服务器的主机名。

如果你不使用 NIS，但使用 `shadow` 和 `MD5`，则你的行可能看起来像这样：

```
auth --usesshadow --enablemd5
```

然而，如果你使用 NIS，你可能会拥有：

```
auth --enablemd5 --enablisis --nismdomain hidden.dom --nisservice 192.168.0.14
```

> 注意：通常，上面的代码需要全部在同一行。在这种情况下，为了印刷目的必须将其拆分。

最后，但同样重要的是 `LILO` 配置部分。这行以 `lilo` 开头，事实上，如果你不需要任何选项，可以只保留这一个词。LILO 安装标志是 `--location`，它指的是 LILO 安装的位置。可用选项如下：

- `mbr`：默认位置
- `partition`：具体而言，是根分区
- `none`：不安装 LILO

在此行中，你可能只有 `lilo`，或者你有

```
lilo --location none
```

> **提示：** 如需查看创建此文件的图形化操作指南，请访问 [www.fezbox.com](http://www.fezbox.com)。

## 软件包

本节列出了需要在新机器上安装的所有 `RPM` 软件包。无需指定路径。所有软件包都假定位于同一位置。在 `CD-ROM` 上，此位置为 `/mnt/cdrom/RedHat/RPMS`。关于 `NIS` 配置的详细讨论将在第 16 章中进行。

以下是你的软件包部分开头的一个小片段示例：

```
%packages
filesystem
basesystem
ldconfig
glibc
mktmp
termcap
bash
ncurses
sed
gawk
```

现在请查看 `/mnt/cdrom/RedHat/RPMS` 目录。所有这些名称都是某个 `RPM` 的开头部分。实际上，输入 `rpm -qi sed` 即可获取关于此软件包的信息。`RPM` 安装完成后，版本号及其他扩展文件名信息就不再重要。这里列出的软件包也是如此。

> **提示：** 如果你正在执行 `NIS` 安装，你可以将任何 `RPM` 添加到软件包目录中，并在此处列出以便自动安装。将此选项与制作你自己的 `RPM`（参见第 4 章）结合使用，KickStart 工具会显得功能强大得多。

## 安装后指令

安装后指令部分是 KickStart 文件的最后一部分。通常，此部分在开始时是空白的，你可以选择是否填写。如果你只是想克隆初始安装环境，大多数人无需填写此部分。然而，如果你希望在此之后继续配置，`%post` 部分允许你这样做。

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_333_0.png)

