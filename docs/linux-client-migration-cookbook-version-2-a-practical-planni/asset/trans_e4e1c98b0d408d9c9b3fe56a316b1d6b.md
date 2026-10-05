
在第277页。由于我们有十多个工作站，因此我们决定使用带有模板的命令行界面来使迁移步骤更容易。我们还编写了一个脚本，将迁移分为两个简单的步骤。

首先，我们创建一个模板，该模板包含了我们想要迁移的所有数据，并将其保存到我们的网络共享中。然后对于 Windows 存储操作，我们使用以下批处理文件安装 .NET 框架和 Progression Desktop，并将设置存储到网络共享的平台中包（PNP）中。

# 示例 8-9 在 Windows 上安装并运行 Progression Desktop 的批文件

```cmd
cmd / c itsont5\data\ProgressionDesktop\Windows\dotnet.exe /q:c:\install /q /1
cmd / c msiexec /quiet \itsont5\data\ProgressionDesktop\Windows\zf7fg42j.msi
"C:\Program Files\VirtualProgram\ProgressionDesktopCore." --store
--file=\:itsont5\data\%userDomain%%username%
--template=\:itsont5\data\template.xml
```

接下来，我们为 Linux 操作创建了一个脚本，该脚本会在桌面上临时安装 Mono（因为 Red Hat 桌面版不带 Mono），然后我们运行 Progression Desktop 以应用来自网络共享的用户设置。最后，bash 脚本通过删除 Mono 来清理机器。

# 示例 8-10 在 Linux 上安装并运行 Progression Desktop 的 bash 脚本

```bash
#! /bin/bash
/shares/data_g/monoinstaller-mono-1.8.2-1-installer.bin \
--mode unattended --prefix var/tmp/mono --AddMonoToPath 0 \
/var/tmp/mono/bin/mono/shares/data_g/ProgressionDesktop/Linux/ProgressionDesktopCore.exe \
--apply --file=/shares/data_g/$USER.pnp --template=/shares/data_g/$ITSOtemplate.xml
rm -rf /var/tmp/mono
rm -f ~/Desktop/mono
```

要将任何机器从 Windows 迁移到 Linux，我们需要在 Windows 机器上执行第一个批文件，一旦完成，在 Linux 目标上运行 bash 脚本。

## 个制化

修改 Linux 桌面的外观和感受具有极高的灵活性。对于我们的迁移场景，我们选择了修改几个设置来展示一些可能性。我们做的第一件事是调整默认背景颜色并在背景上插入另一张图像。你可以使用 GNOME 的背景设置应用程序来实现此点。另一种可能性（特别是将此桌面图像设置为强制性）是使用示例 8-11 所示带有命令语法的 gconf。

### 示例 8-11 使用 gconf 替换所有用户的桌面图像

```bash
gconf --direct --config-source write:/etc/gconf/gconf.xml --type string desktop/gnome/background/filename=itso-logo
```

关于如何更改 GNOME 数据库中值的更多信息，可以查阅第 317 页的“桌面个性化”。关于使用 gconf 进行更改的具体细节，可以在第 7.2 节“GNOME 锁定选项”。你可以通过插入另一个图标创建一个创建一个精美的菜单。默认情况下，Red Hat 已经用它自己的图像替换了 GNOME 图标。我们通过编辑以下文件替换了它：

```
/usr/share/pixmaps/redhat-main-menu.png
```

虽然此文件的重命名是在 GConf 中设置的，但我们决定采取简单的方法，将其重命名为 redhat-main-menu.png。当然，它的大小必须是 48x48 像素，而且为了更好看，图标必须是透明的。最后的自定义是创建指向映射的 Windows 共享的链接。这些自定义的输出可以在第 194 页的图 8-5 中查看。

### 8.3.4 屏幕截图：客户端到 Linux

在接下来的页面中，我们提供了运行在 Linux 客户端上最重要的应用程序截图：

| 应用程序 | 图 | 页码 |
| --- | --- | --- |
| Windows 终端服务器上的 Adobe FrameMaker | 图 8-1 | 190 |
| Linux 上的 GIMP | 图 8-2 | 191 |
| 连接到 Microsoft Exchange 2000 的 Novell Evolution | 图 8-3 | 192 |
| Linux 客户端上的 Mozilla Firefox | 图 8-4 | 193 |
| 显示为 ITSO 定制的新桌面 | 图 8-5 | 194 |

![](img/23b94da14ff7bab87620f0361af394_217.png)

## 

本章演示了将 Linux 客户端集成到现有 Windows 域（NT4 或 Active Directory）的其他方法。涵盖了许多集成问题，包括登录时从 SMB 共享挂载主目录。验证用户到 Windows 域有两种方法：

- 使用 Samba 提供的 winbind
- 使用 LDAP 直接连接到 Active Directory（这需要更改 Active Directory 架构）

本章的章节包括：

- 9.1节，“如何加入 Windows 域”，第 196 页
- 9.2节，“使用 winbind 使用户本地化”，第 199 页
- 9.3节，“自动使用 LDAP 连接到 Active Directory”，第 204 页
- 9.4节，“可插拔认证模块与域”，第 207 页
- 9.5节，“如何在 Linux 客户端上挂载共享”，第 214 页
- 9.6节，“登录时自动挂载主目录”，第 216 页
- 9.7节，“如何在域中使用网络打印机”，第 219 页

本节中的示例和指南均假设至少使用 Samba 3.0。某些功能在较旧版本中不存在或尚未成熟。

## 9.1 如何加入 Windows 域

大多数指南详细讨论了如何将 Linux 服务器加入域。本指南描述了将 Linux 客户端加入域。加入 NT4 域与加入 Active Directory 域不同。我们将对两者进行详细讨论。

在本节的大多数示例中，我们使用域 AD6380，主域控制器为 SMB26，备份域控制器为 SMB277。在某些示例（使用 Windows 2003 Active Directory）中，我们使用域控制器 W2K3AD。

### 9.1.1 加入 NT4 域

我们使用 Samba 连接到域。最小的 smb.conf 如示例 9-1 所示。

```
# 示例 9-1 加入 NT4 域的 smb.conf
[global]
workgroup = AD6380
security = domain
password server = SMB26,SMB277
```

将域和密码服务器替换为您自己的域以及主（和备份）域控制器的正确名称或地址。

然后您可以加入域：

```bash
net join -S SMB26 -U administrator
```

将 SMB26 替换为您主域控制器的名称（或 IP 地址），并使用任何具有向域添加机器权限的域账户。加入 NT4 域的更多细节可以找到当前的 Samba-HOWTO。该集合可以在以下位置找到：

```
http://samba.org/samba/docs/
```
