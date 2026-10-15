
# 软件软件包管理

- `lisa` 的软件软件包管理功能 (全部)
- 按你的需要安装和删除软件包...
- 帮助帮助
- 关于可用软件包的信息
- 删除已安装的软件包

![](img/c48ad0dbc61332ca39f773da7141f4e1_61_0.png)

### 2 选择软件包

接下来，`lisa` 会查询你系统的 `rpm` 数据库，并在“卸载软件包”（Un-install Software Packages）对话框中显示已安装软件包的列表。滚动软件包列表并按空格键选择一个软件包。左侧列会出现一个 X。你可以使用空格键选择或删除多个软件包。完成后，按回车删除该软件包。

### 3 开始安装软件包

在“软件软件包管理”对话框中，选择“选择安装源”（Select Installation Source）并按回车。

--- 软件软件包管理

- `lisa` 的软件软件包管理功能 (全部)
- 按需要安装软件包。按 `F1` 获取更多详情。
- 选择安装源
- 安装额外的软件包
- 删除已安装的软件包

![](img/c48ad0dbc61332ca39f773da7141f4e1_61_1.png)

--- 未安装的软件包

选择要从列表中删除的未安装软件包 (全部)

未安装的软件包：

- Lisa 正在搜索并匹配软件包...
- Linux 系统工具和实用程序
- Linux内核相关工具
- Python 配置
- Python 开发
- Perl 开发
- C 开发库和头文件
- Python 开发
- Linux 开发用户空间

![](img/c48ad0dbc61332ca39f773da7141f4e1_61_2.png)

## 选择源

确保你的 CD-ROM 已挂载。在“选择安装源选择”对话框中选择“CD-ROM”并按回车。

![](img/c48ad0dbc61332ca39f773da7141f4e1_62_0.png)

## 选择源

接下来，`lisa` 确定你拥有的 CDROM 类型；按回车。会出现一个小的信息。

![](img/c48ad0dbc61332ca39f773da7141f4e1_62_1.png)

## 选择，安装软件包

滚动软件包列表。选择一个软件包，然后按回车。显示信息。

![](img/c48ad0dbc61332ca39f773da7141f4e1_62_2.png)

## 提示

### 获取信息
`lisa` 命令显示软件包。在“软件软件包管理”对话框中，向下滚动到第 4 项“删除已安装的软件包”，并按回车。

### 使用 Netscape 搜索
Lisa 正在搜索并匹配软件包... 在“可用软件包”中，滚动列表。按回车。

![](img/c48ad0dbc61332ca39f773da7141f4e1_62_3.png)

使用 LISA 49 管理你的软件

## 使用 BRU 2000 备份

如果你使用 Linux（如 `/dev/fd0`），你可以轻松做到。然而，这非常简单易用，你不需要手册！例如，要启动备份话并使用软盘作为备份介质，输入 `taper -r`。

### 1 配置

在“文件”（File）菜单中，点击“配置”（Configure）。显示信息。

![](img/c48ad0dbc61332ca39f773da7141f4e1_63_0.png)

### 2 启动设备

出现“软件软件包管理”对话框。点击“启动”（Start）。

![](img/c48ad0dbc61332ca39f773da7141f4e1_63_1.png)

### 3 选择设备

在“新设备”（New Device）对话框中，选择 `/dev/fd0`，并点击。

![](img/c48ad0dbc61332ca39f773da7141f4e1_63_2.png)

## 命名设备

点击“设备”字段，输入 Floppy，并点击。

## 选择新设备

在“新设备”对话框中，选择 `/dev/fd0`，并点击。

![](img/c48ad0dbc61332ca39f773da7141f4e1_64_0.png)

## 选择文件

在“备份到存档”（Backup to Archive）窗口中，选择要备份的文件或目录，并点击“添加”（Add）。完成后，将软盘插入电脑并点击“开始备份”（Start Backup）。BRU 2000 会询问存档标签，给你需要多少磁盘的估计，并开始备份。

![](img/c48ad0dbc61332ca39f773da7141f4e1_64_1.png)

## 提示

### BRU 2000 可使用的其他设备

BRU 2000 的配置文件列出了近 40 种备份设备，但你也可以自定义。你只需要知道 `dev` 下设备名称（例如用于并行端口驱动器的 `/dev/sda`）以及设备容量（每个磁盘 100MB）。

### 你可以使用另一个备份程序

使用 `taper` 命令 `-T` 后跟备份设备名称启动备份。`taper` 命令不需要 X Window 系统，可以从任何控制台命令行启动。确保阅读 `/usr/doc/taper` 目录下的 `taper` FAQ。然而，这非常简单易用，你不需要手册！

## 使用 tar 命令

你可以使用 `tar` 命令将文件备份到软盘驱动器。例如，使用命令 `cvf /dev/fd0 -m myfiles` 来备份 `myfiles` 目录的内容。M 选项告诉 `tar` 该备份是一个多卷存档。当第一张磁盘满时，按 `tar` 插入下一张磁盘。

![](img/c48ad0dbc61332ca39f773da7141f4e1_64_2.png)

![](img/c48ad0dbc61332ca39f773da7141f4e1_64_3.png)

使用 BRU 2000 备份文件 51

### 7

### 开始

## 如何管理您的服务

### 1 选择系统配置

Lisa 命令可以帮助你管理系统的几乎任何方面。本节将向你展示如何在系统上配置不同的软件服务。Lisa 程序不需要 X，因此你可以在控制台的命令行界面使用它。你必须以 root 操作员身份登录。

滚动到 LISA 主菜单窗口中的“系统配置”（System Configuration）项，并按回车。

![](img/c48ad0dbc61332ca39f773da7141f4e1_65_0.png)

### 2 选择系统配置（再次）

### 3 选择软件服务

出现系统配置菜单。滚动到“系统配置”并按回车。

滚动到“配置守护进程/服务器自启动”（Configure Daemon/Server Autostart），并按回车。守护进程是在你在启动 Linux 时经常启动的程序。它们在后台运行，仅在需要时激活，并且如果产生自身的副本和新进程（守护进程或已死亡但仍显示 `ps` 命令显示的进程表中进程），则被称为“僵尸进程”（zombies）。

![](img/c48ad0dbc61332ca39f773da7141f4e1_65_1.png)

![](img/c48ad0dbc61332ca39f773da7141f4e1_65_2.png)

## 查看当前服务

`lisa` 命令列出了几乎 30 种不同的软件服务（取决于你在系统中安装的软件）。在启动 Linux 时，至少至少至少四个服务启动：用于调度事件的 Cron；用于打印的 Print server；用于发送电子邮件的邮件传输代理（Mail Transfer Agent）；以及在 `/var/log` 目录下创建系统日志的 System Logger。

## 选择 Web 服务器

例如，为了让 Apache Web 服务器在下次启动 Linux 时启动，滚动到“Web Server (Apache)”项，按空格键，然后按回车。

```
Configure server autostart

Select all services that should be started automatically.

AutoMount Daemon (NFS) local

- AutoMount Daemon (NFS) local

  - Large filesystem support (ext3)

  - AutoMount Daemon (NFS) local

  - AutoMount

- network daemon (nell) local

  - network daemon (nell) local

  - network daemon (nell)

Continue
```
