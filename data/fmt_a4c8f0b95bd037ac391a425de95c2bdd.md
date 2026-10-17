
## bash-1.14.7-16

`bash-1.14.7-16`

## MAKEDEV-2.5-2

`MAKEDEV-2.5-2`

## curses-4.2-25

`curses-4.2-25`

## info-3.12h-2

`info-3.12h-2`

## ORBit-0.4.95-2

`ORBit-0.4.95-2`

## ORBit-devel-0.4.95-2

`ORBit-devel-0.4.95-2`

## SysVinit-2.77-2

`SysVinit-2.77-2`

## XllR6-contrib-3.3.2-6

`XllR6-contrib-3.3.2-6`

## chkconfig-1.0.7-2

`chkconfig-1.0.7-2`

## fileutils-4.0-8

`fileutils-4.0-8`

## utempter-0.5.1-2

`utempter-0.5.1-2`

etc ...

```
```

如果你知道包名称的一部分并想检查它是否已安装，可以将 `grep` 命令与 `rpm` 结合：

```bash
# rpm -qa | grep <partial package name><ENTER>
```

## 让 LINUX 运行起来：核心技巧与技术

### 技巧 2.3: 卸载 RPM 包

你可以使用 `rpm` 命令的 `-e` 标志来卸载 RPM 包：

```
# rpm -e <RPM package name><Enter>
```

如果你不确定包名，可以像技巧 2.2 “查询 RPM 包”中所讨论的那样查询已安装的包。

或者，你可以在 Gnome 中使用 `GnoRPM` 卸载包：

- 点击 Gnome 主菜单按钮。Gnome 随后将显示主菜单。
- 点击 Gnome 主菜单中的“程序 (Program)”项。Gnome 随后将显示“程序”子菜单。
- 点击程序子菜单中的“系统 (System)”项。Gnome 随后将显示“系统”子菜单。
- 点击系统子菜单中的“GnoRPM”项。Gnome 随后将启动 `GnoRPM`，如图 10.4 所示。

![](img/1a9080c03c91a8cc232a677fdc119548_679_0.png)

- 在包层次结构中找到你想卸载的组所在的文件夹并选择它。`GnoRPM` 随后将在 `GnoRPM` 窗口的右侧显示所选组中的包，如图 10.5 所示。
- 选择你想卸载的包，并点击 `GnoRPM` 工具栏上的“卸载 (Uninstall)”按钮。`GnoRPM` 随后将显示“继续删除 (Continue Removal)”对话框，如图 10.6 所示。
- 点击“包 (Packages)”菜单。`GnoRPM` 随后将卸载所选包。

![](img/1a9080c03c91a8cc232a677fdc119548_680_0.png)

图 10.5 选择包组。

![](img/1a9080c03c91a8cc232a677fdc119548_680_1.png)

图 10.6 继续删除对话框。

- 点击“包 (Packages)”菜单中的“退出 (Quit)”项。Gnome 随后将关闭 `GnoRPM`。

### 10.2.4: 用于处理 RPM 包的 X Windows 工具

多个 X Windows 工具可用于 RPM 包，包括：

- [GnomeRPM](http://www.daa.caa.com.au/~james/gnome/)。用于 Gnome 桌面环境的 RPM 管理工具。
- [Xrpm](http://www.gmys.com/rpm.html)。`Xrpm` 是 X Windows 的 RPM 管理器，可与任何窗口管理器或桌面环境配合。
- [Kpackage](http://www.general.uwa.edu.au/au/toivo/kpackage)。`Kpackage` 是用于 K 桌面环境 (KDE) 的 RPM 管理工具。
- [RPM Explorer](http://www.zoned.net-xahm/rpmexp/)。`RPM Explorer` 是一个 Gnome 程序，让你像浏览硬盘上的目录一样浏览 RPM 数据库。
- [ManageRPM](http://www.solucorp.qc.ca/linuxconfconf)。`ManageRPM` 是 `Linuxconf` 配置实用程序的一个模块，允许你通过 `Linuxconf` 管理 RPM 文件。
- [RPM Browser for Windows](http://www.laysi.com/rpmbw/)。`RPM Browser for Windows` 允许你在 Windows 系统上浏览并从 RPM 文件提取文件。

此外，你可以在 RPM 网站 `http://www.rpm.org/software.html` 找到大量与 RPM 相关的工具。

### 技巧 10.2.5: 安装 Debian 包

你可以使用 `dpkg` 命令和以下通用语法安装 Debian 包：

```bash
dpkg --install <package file name>
```

你可以通过在命令行中列出所有文件来用一个命令安装多个包：

```bash
dpkg --install <package file name> <package file name> <package-age file name> <package file name> etc ...
```

安装过程正如文件中概述的，解压包中的文件并对其配置。你可以手动分离这些步骤。首先，使用以下命令解压包中的文件：

```bash
dpkg --unpack <package file name>
```

在解压后的任何时候，你都可以使用命令对其进行配置：

```bash
dpkg --configure <package name>
```

包名应该是列出包时显示的包名，如技巧 2.6 “查询 Debian 包”中所述。如果你只是想配置所有已解压但未配置的包，而不是特定的一个，请使用以下命令：

```bash
dpkg --configure -pending
```

### 技巧 10.2.6: 查询 Debian 包

你可以使用 `dpkg` 命令查看匹配名称模式的可用已安装和未安装包的列表，如下：

```bash
dpkg --list <name pattern>
```

名称模式应该是包的全名，或者是带有标准通配符字符的子字符串（例如，`*`）。

# 让 LINUX 运行起来：核心技巧与技术

- 默认账户关联有一个默认 shell。当用户登录时，将执行该 shell 以为用户提供工作环境。

所有关于所有用户的这些信息都存储在系统数据库文件 `/etc/passwd` 中。正如技巧 3.7 “影子密码的工作原理”所讨论的，在 `/etc/passwd` 文件中存储密码会产生安全问题，这可以通过影子密码（shadow passwords）来解决。使用影子密码，密码将从 `/etc/passwd` 文件中分离并存储在 `/etc/shadow` 文件中。

用户认证是一个与用户和账户管理相关的广泛主题，但对该主题有一个概览可以帮助你理解如何处理系统安全和用户管理。广而言之，认证是识别用户（换言之，确定用户确实是其声称身份）并对该用户授权（换言之，授予某些权限）以访问某些资源的过程。

- 通常，Linux 身份验证在每个系统的本地发生，并使用用户名密码对。然而，情况并非总是如此。
- 认证可以使用网络信息系统 (NIS) 或轻量级目录访问协议 (LDAP) 等技术在认证服务器上集中进行。在这种情况下，每次登录尝试都会重定向到认证服务器，然后由服务器告知用户是否成功认证，并向客户端提供用户信息。
- 认证可以有多种形式。最传统的方法是使用用户名和密码，但也存在选项，包括智能卡、视网膜扫描、指纹、语音识别、临时密码以及基于位置的认证。为了最大安全性，系统会结合这些方法中的多种（例如用户名和密码结合智能卡）。

认证也可以发生在两个级别：系统级和应用程序特定。系统级认证发生在用户最初登录系统时发生。该认证信息随后用于管理对资源的访问，包括文件和服务。然而，并非所有软件都利用此认证信息来决定哪些用户允许使用哪些功能，而是实现它们自己的认证机制和用户数据库以确定资源的访问。有时应用程序会使用系统认证信息以及它们自己的机制。例如，FTP 服务器通常允许使用系统数据库或它们自己的用户数据库来验证匿名登录。

# 技巧 10.3.1：存储密码的加密方案

Linux 与所有 Unix 变体一样，在将密码存储在系统数据库文件 `/etc/passwd`、影子密码文件 `/etc/shadow` 时会对密码进行加密。然后，当用户登录时，输入的密码会与用户账户信息中的加密版本进行比较。如果匹配，则认为用户已成功认证。

传统上，Linux 使用标准的 Unix `crypt` 加密方案来存储密码。虽然使用 `crypt` 函数加密的密码对于具有恶意意的人是不可读的，但提供的安全性有限。

最近，Linux 选择了更高级的加密方案。例如，RedHat Linux 7 提供了 MD5 加密，这有助于让你的密码免受攻击。结合良好的安全策略，包括影子密码、强制用户定期更改密码以及强制使用复杂的密码，你的系统可以防止密码被窃取或破解。

# 技巧 10.3.2：查看 passwd 文件

标准的 `/etc/passwd` 文件用于定义你 Linux 系统上的所有本地用户。它包含一系列条目，每个用户一个。每个条目单独占一行。以下是 `/etc/passwd` 文件中典型条目的示例：

```
test:UGpFHrQv1xl5:502:2:/home/test:/bin/bash
```
