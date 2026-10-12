

## 当你取消勾选已安装的软件包时，软件包管理器会移除该软件包

以下步骤描述了如何移除软件包：

- **1. 点击 GNOME 菜单按钮并选择系统设置：_添加/移除应用程序_。**

  打开 _软件包管理_ 窗口。

- **2. 如果在 _信息_ 窗口中提示，请输入 _root_ 密码。**

- **3. 点击包含你要移除的 _软件包_ 的软件包组旁边的 _详细信息_ 按钮。**

  例如，如果你点击开发工具组的详细信息按钮，就会打开开发工具 _软件包详情_ 窗口。

- **4. 点击你要移除的 _软件包_ 左侧的复选框。**

  对勾消失。

- **5. 点击 _关闭_ 按钮。**

  控制返回到 _软件包管理_ 窗口。

- **6. 点击 _更新_ 按钮。**

  _正在准备系统更新_ 对话框短暂打开，然后你返回到 _系统准备完成_ 窗口。

- **7. 点击 _继续_ 按钮。**

  软件包（或多个软件包）被移除。

- **8. 在 _更新完成_ 窗口中点击 _确定_ 按钮。**

- **9. 回到 _软件包管理_ 窗口，点击 _确定_ 按钮。**

![](img/41feae212f5c6612ff709354891f7b39_365_0.png)

> 务必确保你真的想要弃用该软件包，因为当你移除一个软件包时，它就消失了——彻底消失。好吧，也许我们说得有点夸张。你随时可以上网访问诸如 _www.freshmeat.net_ 或 _www.redhat.com_ 等网站，下载更多的软件包进行安装。我们建议你这样做。总是会有新的工具问世，可以帮助优化你的 Fedora Core 计算体验。

## 使用 RPM 手动操作

本章的第一部分集中介绍如何使用 Red Hat 软件包管理器来安装和移除软件包。你也可以选择使用 _rpm_ 命令。它为安装和移除功能提供了额外的特性。你可以使用 _rpm_ 来安装、更新、移除和查询软件包。本节提供了手动使用 _rpm_ 命令的示例。

### 手动安装和升级软件包

`rpm -i` 参数表示将进行安装。你可以通过使用 `-v` 选项添加*详细*模式（提供更多信息）。（你可以将选项组合成一个组；例如，`-i -v` 可以变成 `-iv`。）请按照以下说明安装和升级软件包：

- 1. 以 root 身份登录。
- 2. 通过点击 *GNOME 面板* 中的终端图标打开终端仿真器窗口（操作说明请参阅第 4 章）。
  打开 GNOME 终端仿真器窗口。
- 3. 要在终端窗口中添加软件包，请输入以下命令：

```bash
rpm -iv /media/cdrom/Fedora/RPMS/mozilla-mail*
```

或者，你可以升级系统中已安装的软件包。将 `RPM 升级` 选项 `-U` 替换 `安装` 选项 `-i`。例如，以下命令更新 Mozilla 电子邮件客户端软件包：

```bash
rpm -Uv /media/cdrom/Fedora/RPMS/mozilla-mail*
```

构成较新版本的 Mozilla-mail 软件包的文件将覆盖旧版本。不过，现有的配置会通过给配置文件添加 `.rpmsave` 后缀来保存。

### 手动移除软件包

`RPM` 软件包是计算机上很好的居民，因为它们便于移除。`rpm` 命令允许你通过 `erase (-e)` 功能移除软件包。

假设你不喜欢 Mozilla 电子邮件客户端，而更喜欢 Evolution 客户端。没问题：你可以移除 Mozilla 邮件软件包。要移除 RPM 软件包，请遵循以下步骤：

- 1. 以 *root* 身份登录并打开终端仿真器窗口。
  打开 GNOME 终端窗口。
- 2. 输入以下命令以查找要移除的软件包名称：

```bash
rpm -qa | grep mozilla
```

你应该看到这些结果：

```text
mozilla-nss-1.0.1-10
mozilla-1.0.1-10
mozilla-nspr-1.0.1-10
mozilla-psm-1.0.1-10
mozilla-mail-1.0.1-10
```

在移除软件包之前，你需要知道它的名称。我们使用这一步来显示所有已安装的 Mozilla 软件包，以找到该软件的名称。

- 3. 你还可以使用以下命令获取关于该软件包的信息：

```bash
rpm -qi mozilla-mail
```

或者，你可以使用 `rpm -qa` 命令显示所有已安装软件包的列表。运行 `man rpm` 命令以查找查询选项。

- 4. 输入以下命令以移除 Mozilla 电子邮件客户端：

```bash
rpm -e mozilla-mail
```

## 介绍 YUM

简单来说，Yellowdog Updater, Manager (YUM) 是一个绝妙的系统。YUM 通过提供 RPM 没有的三个功能，将软件安装和管理提升到下一个层次：

- **接管寻找和获取软件包的任务：** YUM 可以从互联网（或专用网络）、DVD 或 CD-ROM、或本地硬盘下载软件包。
- **计算软件包依赖项：** 如果你想安装一个碰巧需要安装其他软件包的 RPM 软件包，你通常需要确定这些软件包是什么，找到它们并手动安装。
- **更新你的计算机：** YUM 可以更新你的整个 Fedora Core 计算机，也可以安装和移除单个软件包或软件包组。RPM 可以更新单个软件包，但不能更新整个系统。YUM 更新选项执行与 Red Hat up2date 系统相同的功能。

YUM 配置简单，并且可以访问多个软件仓库（镜像）。这是默认的 YUM 配置 /etc/yum.conf：

```ini
cachedir=/var/cache/yum
debuglevel=2
logfile=/var/log/yum.log
pkgpolicy=newest
distroverpkg=fedora-release
tolerant=1
exactarch=1
exclude=

[base]
name=Fedora Core $releasever - $basearch - Base
baseurl=http://fedora.redhat.com/releases/fedora-core-$releasever

[updates-released]
name=Fedora Core $releasever - $basearch - Released Updates
baseurl=http://fedora.redhat.com/updates/released/fedora-core-$releasever

#[updates-testing]
#name=Fedora Core $releasever - $basearch - Unreleased
# Updates
#baseurl=http://mirrors.kernel.org/fedora/core/test/1.90/$basearch/os
```

YUM 配置选项列表如下：

- **cachedir:** 此选项设置 YUM 存储 RPM 软件包及其头部文件（存储文件和关于该包的其他信息）的位置。YUM 在安装或更新 RPM 软件包（和头部文件）之前会下载它们。默认位置是 /var/cache/yum 目录。
- **debuglevel:** 此选项设置传输到日志文件的信息详细程度。范围是从 0 到 10，其中 0 表示无信息，10 表示信息过多。默认值为 2。
- **logfile:** 日志文件的位置。不出所料，默认位置是 /var/log/yum.log；/var/log 是大多数（如果不是全部的话）Linux 日志文件的默认位置。
- **pkgpolicy:** 有两个选项：newest 和 last。newest 选项告诉 YUM 安装软件包的最近版本。last 选项选择字母顺序服务器列表中最后一个服务器上找到的软件包。我们想不出使用 last 选项的任何理由。
- **distroverpkg:** 你的 Fedora Core 计算机包含一个名为 fedora-release 的 RPM 软件包。该软件包包含关于你安装版本的信息。（Red Hat Linux 计算机包含一个名为 redhat-release 的软件包，包含相同类型的信息。）由于 YUM 是平台独立的（适用于多个 Linux 发行版），此选项告诉 YUM 在哪里查找发行版名称和版本号。默认值是 fedora-release。
- **tolerant:** YUM 可以严格也可以不严格。当 tolerant 设置为 1（默认值）时，YUM 会忽略操作过程中发生的小错误。
- **exactarch:** YUM 也可以严格对待所安装软件包的架构。当 YUM 设置为默认值 `1` 时，如果已安装的软件包是 `i686`，它就不会安装 `i386`。
- **exclude:** 你可以告诉 YUM 不安装某些软件包。例如，如果你不想让 YUM 自动更新你的 Linux 内核，请设置 `exclude-kernel*`。

`/etc/yum.conf` 的其余内容包含 Server 部分。这些部分告诉 YUM 在哪里查找 RPM 软件包。Server 部分还让 YUM 了解软件包的一般用途。以下列表详细描述了每个 Server 部分选项：

- **serverid:** 服务器标识（serverid）字段告诉 YUM 它控制哪种类型的软件仓库（在 Red Hat 更新系统中称为*通道*）。Fedora Core 配置为与以下类型配合使用：`base`、`updates-released`、`updates-testing` 和 `development`。基础仓库的内容与你附带的 DVD 上相同——它包含“基础”Fedora Core 2 发行版。updates-released 仓库包含对基础安装的所有经过官方测试和认可的升级；updates-testing 类型包含尚未正式发布待定更新。development 类型包含旨在用于下一个 Fedora Core 版本的软件包。它基本上就是下一个版本的测试版。
  到你阅读本书时，Development 仓库将包含旨在成为 Fedora Core 4（或更高版本，取决于你阅读本书的时间）的软件。你可以通过下载并安装 Fedora Core 3 测试发行版来参与 Fedora Core 测试周期。或者，你可以使用 YUM 从 Development 仓库更新你的计算机。这就是我们在写这本书时所做的。
- **name:** 此选项设置显示在运行 YUM 时用于 *serverid* 的描述。
- **baseurl:** 此选项指向 *serverid* 仓库 URL。你可以使用 base、updates-released、updates-testing 和 development 仓库类型。默认 URL 是 `fedora.redhat.com`，但你可以添加一个或多个镜像。
  例如，你可以将基础服务器 ID 更改为
  `baseurl` =
    `http://fedora.redhat.com/releases/fedora-core-$releasever/`
    `http://mirrors.kernel.org/fedora/core/$releasever/i386`
  此示例为 YUM 提供了两个要使用的仓库（按顺序）：如果一个不可用，则使用第二个。请注意，每个镜像可能使用略微不同的目录结构来存储其仓库。Fedora Core 项目的默认仓库 `download.fedora.redhat.com` 使用 `/fedora/linux/core/3/i386/` 作为其基础目录，但是

