
libpng 软件包包含一个函数库，用于创建和处理 PNG（便携网络图形）图像文件。PNG 是一种位图格式，类似于 GIF 格式。

## User Interface/X

`XFree86-75dpi-fonts` 包含了大多数 Windows 系统使用的 75 dpi 字体。

35 标准 PostScript 字体的免费版本。出厂标准 35 个 PostScript 字体的 Ghostquality 版本。

关于此页面的意见和建议应邮邮件至 `gmourani@videotron.ca`

此时，安装程序将对您选择的每个格式分区进行格式化。取决于您的机器的速度，这可能需要几分钟。一旦所有分区格式化完成，安装程序将开始安装软件包。

## 如何使用 RPM 命令

本节概述了在 Linux 系统上使用 RPM 进行安装、卸载、升级、查询、检查和构建 RPM 软件包的主要模式。

- 若要安装 RPM 软件包，请使用命令：

```
[root@deep]# rpm -ivh foo-1.0-2.i386.rpm
```

RPM 软件包的文件名为 `foo-1.0-2.i386.rpm`，它包含包名 (`foo`)、版本号 (`1.0`) 和架构 (`i386`)。

- 若要卸载 RPM 软件包，请使用命令：

```
[root@deep]# rpm -e foo
```

请注意，我们使用的是包名 `foo`，而不是原始包文件名 `foo-1.0-2.i386`。

- 若要升级 RPM 软件包，请使用命令：

```
[root@deep]# rpm -Uvh foo-1.0-2.i386.rpm
```

RPM 会自动卸载 `foo` 包的旧版本并安装新版本。请始终使用 `rpm -Uvh` 安装包，因为即使系统中没有安装该包之前的版本，也可以有效。

- 若要查询 RPM 软件包，请使用命令：

```
[root@deep]# rpm -q foo
```

此命令将打印已安装软件包 `foo` 的包名、版本和发布版本。使用此命令可以验证系统是否安装了该包。

- 若要显示包信息，请使用命令：

```
[root@deep]# rpm -qi foo
```

此命令显示包信息，包括已安装程序的名称、版本和描述。

- 若要列出包中的文件，请使用命令：

```
[root@deep]# rpm -ql foo
```

此命令将列出在 RPM 软件包中安装的所有文件。

- 若要检查 RPM 软件包的签名，请使用命令：

```
[root@deep#] rpm -checksig foo
```

此命令检查软件包的 PGP 签名以确保其完整性和来源。PGP 配置信息从配置文件读取。在系统上安装新的 RPM 软件包之前，请始终使用此命令。此外，在使用此命令之前，您的系统中必须已安装 `GNUPG` 或 `Pgp` 软件：

- 若从源码安装包，请使用命令：

```
[root@deep#] rpm -iv -rebuild foo.src.rpm
```

上述命令将配置并编译 `foo` 包，在 `/usr/src/redhat/RPM/i386/` 目录下生成一个二进制 RPM。然后您可以像往常一样使用类似命令安装该包：

## 启动和停止守护进程

Init 是内核在启动时运行的程序。它负责启动所有启动时需要运行的标准进程。这些包括 `APACHE` 守护进程、`NETWORK` 守护进程以及您希望在机器启动时运行的任何内容。

`init` 如何启动和停止服务？每个脚本都编写为接受一个参数，该参数可以是 `start` 或 `stop`，并位于 `/etc/rc.d/init.d/` 目录下。您可以通过类似命令手动执行这些脚本：

例如：

- 在 Linux 下手动启动 `httpd` Web 服务器。

```
[root@deep#] /etc/rc.d/init.d/httpd start
```

- 在 Linux 下手动停止 `httpd` Web 服务器。

```
[root@deep#] /etc/rc.d/init.d/httpd stop
```

检查您的 `/etc/rc.d/init.d/` 目录查看可用服务，并使用命令 `start | stop` 操作。

## 安装服务器后将卸载的软件

Red Hat Linux 默认在您的系统中安装所有预设程序，且在安装设置期间不为您提供卸载它们的选择。因此，您必须在安装服务器后在系统中卸载以下软件：

| pump | apmd | isapntools | redhat-logos |
| :--- | :--- | :--- | :--- |
| mt-st | kernel-pcmia-cs | seterial | redhat-release |
| eject | linuxconf | kudzu | gd |
| bc | getty_ps | raidtools | pciutils |
| mailcap | setconsole | gnupg |  |

使用如下 RPM 命令来卸载它们：

- 卸载软件的命令是：

```
[root@deep#] rpm -e softenames
```

其中 `softenames` 是您想要卸载的软件名称，例如 (`foo`)。

像 `apmd`、`kudzu` 和 `sendmail` 等程序是以进程形式运行的守护进程。在从系统中卸载它们之前，最好停止这些进程。

- 停止进程使用以下命令：

```
[root@deep]# /etc/rc.d/init.d/apmd stop
```

```
[root@deep]# /etc/rc.d/init.d/sendmail stop
```

```
[root@deep]# /etc/rc.d/init.d/kudzu stop
```

现在您可以安全地卸载所有包，其余如下所示：

### 步骤 1

移除指定的包。

```
[root@deep]# rpm -e mt-st mailcap kernel-pcmia-cs getty_ps setconsole kudzu raidtools gnupg redhat-release pciutils
```

### 步骤 2

移除已安装的 `linuxconf`。

```
[root@deep]# rpm -e linuxconf
```

### 步骤 3

移除已安装的程序。

```
[root@deep]# rpm -e hdparm
```

### 步骤 4

移除已安装的程序。

```
[root@deep]# rpm -e kbconfig
```

### 步骤 5

移除已安装的程序。

```
[root@deep]# rpm -e timeconfig
```

### 步骤 6

移除已安装的程序。

```
[root@deep]# rpm -e mouseconfig
```

### 步骤 7

移除已安装的程序。

```
[root@deep]# rpm -e mailconfig
```

### 步骤 8

移除已安装的程序。

```
[root@deep]# rpm -e pump
```

### 步骤 9

移除已安装的程序。

```
[root@deep]# rpm -e eject
```

### 步骤 10

移除已安装的程序。

```
[root@deep]# rpm -e bc
```

### 步骤 11

移除已安装的程序。

```
[root@deep]# rpm -e mailcap
```

### 步骤 12

移除已安装的程序。

```
[root@deep]# rpm -e setconsole
```

### 步骤 13

移除已安装的程序。

```
[root@deep]# rpm -e seterial
```

### 步骤 14

移除已安装的程序。

```
[root@deep]# rpm -e kudzu
```

### 步骤 15

移除已安装的程序。

```
[root@deep]# rpm -e sendmail
```

### 步骤 16

移除已安装的程序。

```
[root@deep]# rpm -e procmail
```

### 步骤 17

移除已安装的程序。

```
[root@deep]# rpm -e mt-st
```

### 步骤 18

移除已安装的程序。

```
[root@deep]# rpm -e st
```

关于本页面的意见和建议请邮件至 `gmnouri@videotron.ca`

`redhat-logos` 软件包（“软件包”）包含 Red Hat “Shadow Man” 标志和 RPM 标志的文件（“这些标志”）。

Red Hat Linux 发布文件。

`Gd` 是一个用于绘制 `.gif` 文件的图形库。`Gd` 允许你快速绘制图像（线条、弧、文本、多颜色、从其他图像复制和粘贴、洪水填充）并将结果写出为 `gif` 文件。

此软件包 (`poiutils`) 包含各种用于检查和设置连接到 PCI 总线设备的工具。

`kbcdbus` 程序是一个终端模式程序，为设置系统的键盘映射提供了一个简单的接口。

`Mouseconfig` 是一个基于文本的配置工具。`Mouseconfig` 负责设置 Red Hat Linux 系统上配置和使用鼠标所需的文件和链接。
