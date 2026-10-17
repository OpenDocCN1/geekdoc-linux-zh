
返回你想查看安装过程的桌面，VNC 窗口应该会出现在包含 Fedora 欢迎的桌面上。继续安装。

## 执行 kickstart 安装

如果你在多台计算机上安装 Fedora 或 RHEL，可以通过预先配置安装过程中提问题的答案来节省一些麻烦。这种自动化安装过程的方法被称为 kickstart 安装。kickstart 文件不能用于驱动标准的 Fedora 安装，但也可用于创建 Fedora Live CDs。

> **注意：** 根据你在 `ks.cfg` 文件中提供的信息，kickstart 将静默地通过并安装 Fedora，而无需人工干预。如果此文件不正确，你可能会轻易删除你的主引导记录并擦除硬盘上的所有内容。请仔细检查 `ks.cfg` 文件，并在安装到存放关键数据的计算机之前先在非关键计算机上进行测试。

执行 kickstart 安装的一般步骤如下：

- 1. **创建一个 kickstart 文件。** 名为 `ks.cfg` 的 kickstart 文件包含了输入到安装过程的问题解答。
- 2. **安装 kickstart 文件。** 你需要将 `ks.cfg` 放在软盘或 CD 盘上、本地硬盘上，或网络上可访问的位置。
- 3. **启动 kickstart 安装。** 当你启动安装过程时，你需要识别 `ks.cfg` 文件的位置。

在本示例中，你可以直接使用文本编辑器创建 kickstart 文件。如果你愿意，可以使用 Kickstart 配置器（`system-config-kickstart` 命令，来自同名软件包），这是一个用于创建 kickstart 文件的图形化工具。

### 创建 kickstart 文件

开始创建 kickstart 文件的方法是从示例 `ks.cfg` 文件开始。当你安装 Fedora 或 RHEL 时，安装过程会将一个名为 `anaconda-ks` 的文件放入 `/root` 目录。你可以将其作为用于 kickstart 安装的 `ks.cfg` 文件的基础。

你获得的特定 `/root/anaconda-ks` 文件来自在标准安装（CD、NFS 等）期间输入的信息。推测，如果你为同一机构的其他计算机安装 Fedora，那么许多计算机可能具有许多相同的硬件和配置信息。这对于开始创建你的 `ks.cfg` 文件的绝佳文件。

> **注意：** 有关如何使用 kickstart 的更多详细信息，请参阅《红帽配置指南》。你可以从任何红帽镜像站点获取该指南。使用更具图形化的工具配置 kickstart，请运行 `system-config-kickstart` 命令（在通过 `yum install system-config-kickstart` 命令安装同名软件包后）。

开始，以 root 用户身份登录。然后复制 `anaconda-ks.cfg` 文件以进行操作。

```
# cp anaconda-ks.cfg ks.cfg
```

使用任何文本编辑器编辑 `ks.cfg` 文件。记住，必须的项目应按顺序排列，任何当你省略某项时，用户都会被提示提供答案。来自标准 Fedora DVD 安装创建的 `ks.cfg` 文件的条目被用作下面描述的模型。你应该从你的 `anaconda-ks.cfg` 文件开始。

## 第 2 章：安装 Fedora 55

`ks.cfg` 文件中第一行未注释的行应该指示安装是升级还是安装。`install` 选项运行新安装。你可以使用 `upgrade` 关键字来升级现有系统。对于升级，要求包括语言、安装方法、安装设备、键盘和启动引导加载程序。

```
install
```

安装方法在下一行标明。安装的可能位置包括：nfs (`nfs --server=servername --dir=installdir`)、FTP (`url http://passwd@server/dir`)、HTTP (`http --url http://server/dir`) 或硬盘 (`harddrive --dir=/partition/dev/partition`)。对于默认的 DVD 或 CD 介质，你将看到：

```
cdrom
```

所需的 `lang` 命令设置了安装 Fedora 的语言（更具体地说，还包括国家）。默认值为美国英语 (`en_US.UTF-8`)。

```
lang en_US.UTF-8
```

你可以在 Fedora 中安装以支持多种语言。以下是设置为美国英语的示例：

```
langsupport --default=en_US.UTF-8 en_US.UTF-8
```

所需的 `keyboard` 命令默认识别美国 (`us`) 键盘。支持超过 70 种其他类型的键盘。（运行 `system-config-keyboard` 查看可用键盘类型列表）。

```
keyboard us
```

可选的 `xconfig` 命令可用于配置你的显示器和显卡。如果你改用 `skipx` 命令（如下面的代码所示），则不安装 X 配置，请运行 `system-config-desktop` 来设置你的 X 配置。当你使用 `xconfig` 命令时，你可以根据显卡 (`--hsync` 和 `--vsync`) 识别要使用的 X 服务器类型。其他几个选项允许你设置以位为单位的色彩深度 (`--depth`)、屏幕分辨率 (`--resolution`)、默认桌面是 GNOME 还是 KDE (`--desktop`)、登录界面是否为图形化 (`--startxboot`) 以及显卡上的内存大小 (`--videam`)。（xconfig 之后的所有信息实际上应该同一行）。

```
skipx
```

```
or
```

```
xconfig --card="NVIDIA GeForce FX (generic)" --videoram=131072
--hsync=31.5-37.9 --vsync=50-70 --resolution=800x600
--depth=16 --startxbob --defaultdesktop gnome
```

# 第一部分：开始使用 Fedora 和 RHEL

```
xconfig --card="NVIDIA GeForce FX (generic)" --videoram=131072
--hsync=31.5-37.9 --vsync=50-70 --resolution=800x600
--depth=16 --startxbob --defaultdesktop gnome
```

可选的 `xconfig` 命令可用于配置你的显示器和显卡……如果你改用 `skipx` 命令（如下面的代码所示），则不安装 X 配置，请运行 `system-config-desktop` 来设置你的 X 配置。当你使用 `xconfig` 命令时，你可以根据显卡 (`--hsync` 和 `--vsync`) 识别要使用的 X 服务器类型。其他几个选项允许你设置以位为单位的色彩深度 (`--depth`)、屏幕分辨率 (`--resolution`)、默认桌面是 GNOME 还是 KDE (`--desktop`)、登录界面是否为图形化 (`--startxboot`) 以及显卡上的内存大小 (`--videam`)。

> **注意：** 有关如何使用 kickstart 的更多详细信息，请参阅《红帽配置指南》。你可以从任何红帽镜像站点获取该指南。使用更具图形化的工具配置 kickstart，请运行 `system-config-kickstart` 命令（在通过 `yum install system-config-kickstart` 命令安装同名软件包后）。

（注：OCR 文本有一些重复和重叠页面。自我纠正：OCR 文本提示处理提供的文本。）

```
%packages --resolvedeps
@base
@editors
@games
@graphical-internet
@kde-desktop
@office
@sound-and-video
```

> 注意：`%packages` 命令不支持升级。要安装所有内容，你可以删除所示的包名。然后，在 `%packages` 行之后，你可以添加一个 `@everything` 行。

`%post` 命令开始安装后处理部分。在它之后，你可以添加任何想要在安装完成后运行的命令。在安装过程中期间，一个非常实用的操作是为你想要添加安装的用户的用户添加 `useradd` 命令。你也可以使用 `usermod` 命令来添加用户的密码。（有关创建加密密码的信息，请参阅第 22 章）。请注意，默认情况下没有 `%post` 章节。

```
%post
/usr/sbin/useradd jake
chfn -John W. Jones' jake
/usr/sbin/usermod -p $1ikQYbFBh79ECntuaH. Jake
```
