
Apple 的 ImageIO 框架包含一个内存损坏漏洞，可能允许攻击者在易受攻击的系统上执行代码。RAW 图像文件格式是一种流行的图像格式，受到许多 Apple Mac OS X 应用程序的支持。ImageIO 框架允许应用程序读取和写入 RAW 格式。在处理 RAW 图像的过程中存在内存损坏问题。当用户打开一个恶意制作的图像时，攻击者可以触发该问题，这可能导致应用程序意外终止或任意代码执行。远程未经身份验证的攻击者可能能够执行任意代码或导致拒绝服务状况。用于利用此漏洞的特制 RAW 文件可能通过网页提供，作为电子邮件附件或包含在电子邮件中，或者通过其他方式说服用户打开该恶意文件。此问题不影响 Mac OS X v10.4 之前的系统。针对 Mac OS X 10.4 (Tiger) 系统的 Mac OS X 10.4.9 和针对 Mac OS X 10.3 (Panther) 系统的安全更新 2007-003 解决了此问题。此更新通过对 RAW 图像执行额外验证来解决该问题。

## Safari 中的代码执行漏洞

Apple Safari Web 浏览器包含一个漏洞，可能允许攻击者执行任意代码。Safari 在处理 `feed:` URL 时存在内存损坏问题。当用户访问恶意设计的 URL 时，远程未经身份验证的攻击者可能导致应用程序意外终止或任意代码执行。此问题不影响运行 Mac OS X 10.5 或更高版本系统的系统，但确实影响随 Mac OS X 10.4 及更早版本发布的 Safari 版本。为解决此问题，请安装 Mac OS X 10.5 或更高版本，或更新 Safari。此更新对 `feed:` URL 执行额外验证，并在 URL 无效时提供错误消息。

## UFS 整数溢出漏洞

`ffs_mountfs()` 函数中存在整数溢出，该函数用于 Mac OS X 处理 UFS 磁盘映像。Unix 文件系统 (UFS) 是 UNIX 和其他类似操作系统使用的文件系统。Apple OS X 支持 UFS、分区和映像。当 OS X 系统打开 UFS 磁盘映像时，可能会发生整数溢出错误。攻击者需要说服用户打开一个特制的磁盘映像来触发溢出。Safari Web 浏览器的默认设置将 UFS 磁盘映像视为安全的文件类型，并在下载后自动打开它们。

能够供应特制 DMG 文件的远程未经身份验证的攻击者可以利用此漏洞导致受影响的系统崩溃或执行任意代码。

此漏洞可以通过以下步骤禁用 **下载后打开“安全”文件** 选项来防止：

1. 选择“偏好设置”菜单；将打开图 2-1 中的窗口。

2. 点击“通用”选项卡。

3. 为下载文件设置特定文件夹。

4. 取消选择 **下载后打开“安全”文件** 选项。

## 内核 “fpathconf()” 系统调用漏洞

Mac OS X 内核中的一个漏洞可能允许经过身份验证的本地攻击者导致拒绝服务。`fpathconf()` 系统调用提供了一种方法，使应用程序能够确定与文件描述符相关的可配置系统限制或选项变量的当前值。随 Mac OS X 内核 (XNU) 提供的 `fpathconf()` 版本被编程为在传递与其无法处理的其他类型关联的文件描述符（例如由 `sem_open()` 系统调用返回的命名信号量描述符）时发生恐慌。经过身份验证的本地攻击者可能导致受影响的系统因内核恐慌而崩溃。这种情况导致拒绝服务。此问题已在针对 Mac OS X 10.4 (Tiger) 系统的 Mac OS X 10.4.9 以及针对 Mac OS X 10.3 (Panther) 系统的安全更新 2007-003 中得到解决。

![](img/0c79e6db97822eb68322dfe40d8564fe_69_0.png)

**图 2-1** 此屏幕显示了用户为避免 UFS 整数溢出漏洞应在 Safari 中选择的选项。

## UserNotificationCenter 权限提升漏洞

Apple 的 UserNotificationCenter 包含一个权限提升漏洞。此漏洞发生是因为 UserNotificationCenter 以提权的特权运行，同时处理由具有正常特权的用户提交的输入。拥有有效登录凭证的用户可以以提权的特权运行命令或修改系统文件。

## Mac OS 中的其他漏洞

恶意用户可以利用以下在 Mac OS X 中提到的任何漏洞导致拒绝服务：

- 当在 BOMArchiveHelper 中解压格式错误的 ZIP 存档时，`BOMStackPop()` 函数中存在一个可被利用的错误。

- 在处理格式错误的 BMP 图像时，`ReadBMP()` 函数中存在一个可被在 Safari 或预览应用程序中利用的错误。

- 在处理格式错误的 GIF 图像时，`CFAAllocatorAllocate()` 函数中存在一个错误，当用户访问恶意网站时，可被像利用 Safari 一样利用。

- 在处理格式错误的 TIFF 图像时，`_cg_TIFFSetField()` 和 `PredictorVSetField()` 函数中存在两个错误，可被在 Finder、预览、QuickTime 或 Safari 应用程序中利用。

## 格式错误的安装程序包如何破解 Mac OS X

Apple 安装程序程序中有一个关键的接口问题，允许安装程序获取 root 访问权限。安装程序在访问 Admin 时请求 AdminAuthorization 密钥。Admin 用户帐户提供对 root 级别的完全访问权限，并且在安装期间不向用户提供任何密码。AdminAuthorization 密钥和 RootAuthorization 密钥之间的区别在于 admin 用户没有任何密码。攻击者创建的恶意包中的授权级别设置为 AdminAuthorization。root 拥有的文件可以被修改，命令可以以 root 身份执行，或者可以在用户不知情的情况下安装 setuid-root 程序。大多数 Mac OS X 用户运行由系统创建的默认管理员用户。另一个问题是，出于预防措施，使用 RootAuthorization 密钥创建的包可以被修改为 AdminAuthorization。如果账户保持登录状态，这些包可以在没有管理员密码的情况下安装。

运行安装程序直至完成需要管理权限。在安装之前，应用程序安装程序会检查当前用户是否是系统管理员。如果用户检查退出，安装程序包将安装完整的程序。然后在系统中安装前置和后置脚本。它不需要用户的任何管理员账户密码。因此，个人可以打开格式正确的安装程序包，并使用已登录的系统和平包中的脚本创建新帐户。

## 已演示的损害

安装程序包需要管理员访问临时文件，用于前置和后置脚本。攻击者用无需密码要求的版本替换 `/etc/sudoers` 文件。如果任何系统以管理员身份登录，则打开并运行该包。所有脚本操作均以 root 身份执行。

### UID 结果

前置和后置脚本将用户报告为 root：

```
cat /tmp/uid
uid=0(root) gid=0(wheel) groups=0(wheel), 81(appserveradm), 79(appserverusr), 80(admin)
```

### 管理员创建结果

可以使用 `nicl` 在后置脚本中添加用户。后来，它被添加到 wheel 组。

```
nicl . -read /groups/wheel users
users: root haxxor
```

### Sudoers 结果

运行前：

将 sudoers 文件与包版本进行比较。

```
diff /etc/sudoers sudoers
20c20
< %admin    ALL=(ALL) ALL
---
> %admin    ALL=(ALL) NOPASSWD: ALL
```

运行后：

```
diff /etc/sudoers sudoers
```

因此，系统不能以 admin 用户身份运行日常活动。如果以管理员身份运行，则无法安装来自非知名来源的包。

## Mac OS X 中的蠕虫和病毒

### OSX/Leap-A 蠕虫

OSX/Leap-A 是一种即时消息蠕虫，通过 iChat 消息系统传播。它通过名为 latestpics.tgz 的文件将自身发送到受感染用户的联系人列表中可用的联系人。此蠕虫试图通过用蠕虫副本覆盖原始应用程序并将原始应用程序存储在文件的资源分叉中来感染最近使用的应用程序。归档文件由 latestpics（蠕虫可执行文件）和 .latestpics（将可执行文件伪装为 JPEG 图像的隐藏资源文件）组成。

该蠕虫自身安装为应用程序挂钩（application hook）。如果系统以 root 用户身份运行，则 `/Library/InputManagers/` 目录下的 apphook 子目录会被删除。如果系统以非 root 用户身份运行，则 `~/Library/InputManagers/` 目录会被删除。该蠕虫用以下文件替换它：

- apphook/Info

- apphook/apphook.bundle/Contents/Info.plist

- apphook/apphook.bundle/Contents/MacOS/apphook

受感染的应用程序文件具有以下扩展属性：
