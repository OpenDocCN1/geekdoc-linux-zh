

# 列出软件包

要在系统中获取已安装软件包的简洁列表，请使用以下命令：

```
dpkg --list <pattern>
```

或者：

```
dpkg -l <pattern>
```

对于此命令，`<pattern>` 是一个可选的搜索模式。如果没有该模式，dpkg 将显示系统可用的每个软件包。例如，要显示所有 Apache 软件包，您需要使用以下命令：

```
debian:/usr/doc/dpkg# dpkg --list apache*
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Installed/Config-files/Unpacked/Failed-config/Half-installed
|| Err?=none/Reinst-required/X=both-problems
(Status,Err: uppercase=bad)
||/ Name Version Description
++================ ======= =====================
pn apache <none> (no description available)
pn apache-common <none> (no description available)
pn apache-dev <none> (no description available)
pn apache-doc <none> (no description available)
un apache-modules <none> (no description available)
pn apache-perl <none> (no description available)
pn apache-ssl <none> (no description available)
```

列出了几个 Apache 软件包，但目前此系统上没有任何一个已安装。然而，曾经有几个软件包被安装过，但已被清除，现在未安装。左侧的三列表示以下信息：p 表示该文件已被清除，u 表示该文件已解包，n 表示该文件未安装。左侧列由文件列表上方的行记录。字母对应于信息的第一个字母。例如，i 表示已安装，h 表示半安装。

## 选择状态

选择状态用于 `dselect` 工具。可能的状态模式如下：

- **未知** — 当前状态未知。
- **安装** — 该软件包被标记为安装。
- **移除** — 该软件包已被选中移除。
- **清除** — 该软件包已被选中清除。
- **保持** — 该软件包被保持，可能无法升级。

## 当前状态

第二列显示软件包当前处于什么状态。可能的值如下：

- **未安装** — 该软件包当前未安装。
- **已安装** — 该软件包当前已安装在系统上。
- **配置文件** — 该软件包未安装，但配置文件存在。这在 `remove` 操作后很常见。
- **已解包** — 该软件包已解包，并准备好安装。
- **配置失败** — 在安装过程中，配置脚本失败。
- **半安装** — 在安装过程中发生问题，安装未完成。

## 错误条件

如果软件包存在问题，您会在第三列获得一个错误代码。值如下：

- **无** — 该软件包没有问题。
- **保持** — 该软件包已被置于保持状态，无法安装或移除。
- **需要重新安装** — 该软件包需要重新安装。

## 显示软件包状态

要单独显示软件包的完整详细状态，请使用以下命令：

```
dpkg --status package_name
```

或者：

```
dpkg -s package_name
```

例如：

```
debian:~# dpkg -s ethereal
Package: ethereal
Status: install ok installed
Priority: optional
Section: net
Installed-Size: 2996
Maintainer: Frederic Peters <fpeters@Debian.org>
Version: 0.8.13-2
Depends: libc6 (>= 2.1.94), libglib1.2 (>= 1.2.0), libgtk1.2 (>= 1.2.8-1), libpcap (>= 0.4.1), libsnu1.1, xlibs (>= 4.0.1-1), zlib1g (>= 1:1.1.3)
Description: Network traffic analyzer
Ethereal is a network traffic analyzer, or "sniffer", for Unix and Unix-like operating systems. It uses GTK+, a graphical user interface library, and libpcap, a packet capture and filtering library.
```

## 列出软件包文件

要列出由软件包安装的所有文件，请使用以下命令：

```
dpkg --listfiles *package_name*
```

或者：

```
dpkg -L *package_name*
```

例如：

```
debian:~# dpkg --listfiles wget
/
/usr
/usr/bin
/usr/bin/wget
...
/usr/share/doc/wget/copyright
/usr/share/doc/wget/changelog.gz
/usr/share/doc/wget/NEWS.gz
/usr/share/doc/wget/changelog.Debian.gz
/usr/share/doc-base/wget
/etc
/etc/wgetrc
```

## 显示文件所有权

要找出哪个软件包安装了某个文件，请使用以下命令：

```
dpkg --search package_name
```

或者：

```
dpkg -S package_name
```

例如：

```
debian:/etc# dpkg --search /etc/issue.net
base-files: /etc/issue.net
```

这表明 /etc/issue.net 文件是由 base-files 软件包安装的。

## 检查可用软件包

dpkg 命令显示和使用的大多数信息都存储在 /var/lib/dpkg 目录中。此目录中两个感兴趣的文件如下：

- available
- status

/var/lib/dpkg/available 文件列出了可供选择的可用软件包。以下是该文件的示例：

```
debian:/var/lib/dpkg# more available
Package: telnet
Priority: standard
Section: net
Installed-Size: 176
Maintainer: Herbert Xu <herbert@debian.org>
Architecture: i386
Source: netkit-telnet
Version: 0.16-4
Replaces: netstd
Depends: libc6 (>= 2.1.2), libncurses5
Filename: dists/potato/main/binary-i386/net/telnet_0.16-4.deb
Size: 5826
MD5sum: 9f3a865499f80b3b4975a67f0c65f2cd
Description: The telnet client.
  The telnet command is used for interactive communication with another host
  using the TELNET protocol.
```

`/var/lib/dpkg/status` 文件显示已安装软件包的状态。以下是该文件的示例：

```
Package: telnet
Status: install ok installed
Priority: standard
Section: net
Installed-Size: 176
Maintainer: Herbert Xu <herbert@debian.org>
Source: netkit-telnet
Version: 0.16-4
Replaces: netstd
Depends: libc6 (>= 2.1.2), libncurses5
Description: The telnet client.
The telnet command is used for interactive communication with another host
using the TELNET protocol.
```

通常，这些文件仅由 `dpkg` 使用，但可以查看或搜索有关可用和已安装软件包的信息。

虽然考试目标要求您知道如何编辑这些文件，但您很少会这样做。然而，它们可以包含关于系统上已安装和可用软件包的有用信息。

## 使用 dselect

### 2.2 安装和软件包管理

- 使用 **Debian 软件包管理**。使用 Debian 软件包管理系统，通过命令行（`dpkg`）和交互式工具（`dselect`）。

`dselect` 工具是 `dpkg` 的覆盖层，提供基于字符的图形界面，以增强易用性。当您运行 `dselect` 时，它会显示图 3-1 中所示的屏幕。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_159_0.png)

Debian GNU/Linux 'dselect' 软件包处理前端。

1. f@Access 选择要使用的访问方法。
2. fU@update 更新可用软件包列表，如果可能。
3. fS@elect 请求您希望在系统上拥有的软件包。
4. fI@n@all 安装和升级所需的软件包。
5. fO@nconfig 配置任何未配置的软件包。
6. fL@remove 移除不需要的软件。
7. fQu@it 退出 dselect。

使用 "^" 和 "^"，光标键，首字母或数字移动；按中心确认选择。"^L" 重绘屏幕。

版本 1.6.14 (130c)。版权 (C) 1994-1996 Ian Jackson。这是自由软件：请参见 GNU 通用公共许可证版本 2 或更高版本了解复制条件。没有保修。有关详细信息，请参见 dselect --license。

图 3-1：主要 dselect 菜单

