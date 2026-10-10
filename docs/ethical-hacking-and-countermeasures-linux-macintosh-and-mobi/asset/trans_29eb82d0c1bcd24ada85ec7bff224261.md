
## 网络安全

- 默认情况下拒绝来自网络的访问。
- 停止所有未使用的服务，如 sendmail 和 NFS。
- 定期查看 */var/log* 中的系统日志，特别是 */var/log/secure*。

## Linux 加固步骤

以下是加固 Linux 的一些步骤：

1. 选择一个广泛使用且能及时发布安全更新的 Linux 发行版。
2. 预先规划文件系统的布局。
3. 不要安装不必要的软件包。
4. 更改默认密码并创建普通用户。
5. 禁用不必要的守护进程和网络服务。
6. 禁用通过 SSH 进行远程 root 登录。
7. 设置并启用 IPTables。
8. 配置与安全相关的内核参数。
9. 安装基于主机的入侵检测系统（HIDS）。
10. 应用最新的更新。
11. 精简所有已安装的软件。
12. 提高登录和用户的安全性。
13. 增加审计和日志信息。

## 章节总结

- Linux 正逐渐流行，并迅速成为一个稳定的工业级操作系统。
- 一旦获知目标系统的 IP 地址，攻击者就可以开始端口扫描，寻找系统漏洞以获取访问权限。
- Linux 有可用的密码破解工具。
- Linux 的嗅探器以及数据包组装/分析工具赋予了攻击者在处理其他操作系统时同样的优势。
- 特洛伊木马、后门和蠕虫在 Linux 环境中也很常见。
- 与其他系统一样，应建立一套完善的、集成的流程来应对存在的威胁。

## 复习题

1. 列出 Linux 操作系统的优点。
2. Linux 操作系统有哪些缺陷？
3. 什么是 Rootkit？
4. 在 Linux 中如何编译程序？
5. 描述 chroot 监狱的功能。
6. 描述 Linux 的文件和目录结构。
7. 描述用于导航 Linux 文件系统的命令。
8. 列出 IPChains 和 IPTables 之间的区别。

![](img/0c79e6db97822eb68322dfe40d8564fe_64_0.png)

# 动手项目

- 安装、配置并编译 Linux 内核。
  - 步骤 1：
    - 以 root 身份登录。
    - 运行 `cp linux-2.4.2.tar.gz /usr/src/`。
    - 运行 `cd /usr/src/`。
    - 检查 `/usr/src/linux` 中的旧内核源码。
    - 通过运行 `mv /usr/src/linux linux-X.X.X` 将当前版本移动为备份，以便将来使用。
    - 运行 `tar -zxvf linux-2.4.2.tar.gz`。
    - 通过运行 `mv /usr/src/linux /usr/src/linux-2.4.2` 移动新的内核源码。
    - 通过运行 `ln -s /usr/src/linux-2.4.2 /usr/src/linux` 创建指向新内核源码的链接。
  - 步骤 2：
    - 配置内核。
    - 在 `/usr/src` 中运行 `cd` 进入内核源码目录。
    - 如果您更喜欢文本模式，请输入 `make menuconfig`，但推荐 `xconfig`。
  - 步骤 3：
    - 返回命令行并输入 `make dep` 以进行内核编译。
  - 步骤 4：
    - 通过输入 `make clean` 清理编译过程中创建的所有文件（.o 或对象文件）。
  - 步骤 5：
    - 通过运行 `make bzImage` 创建可启动的 Linux 映像（实际的 Linux 文件）。
    - 通过运行 `make modules` 制作用于安装的新模块。
    - 完成编译后，输入 `make modules_install`。
    - 通过运行 `mv /usr/src/linux-2.4.17/arch/i386/boot/bzImage /boot/vmlinuz-2.4.17` 将 bzImage 文件移动到内核位置。
  - 步骤 6：
    - 将新文件定位到 Linux 启动管理器 LILO 或 GRUB。
    - 编辑文件 `/etc/lilo.conf` 或 `/etc/grub.conf` 并添加以下行：
      ```
      image=/boot/vmlinuz-2.4.17label=linux-2.4.17
      root=/dev/hda3
      read-only
      ```
    - 保存 lilo.conf 或 grub.conf 文件。
    - 运行 LILO 程序 /sbin/lilo。如果使用 GRUB，可以跳过此步骤。
    - 重启机器。

- 下载并安装内核补丁。
  - 从 `http://www.linux.org` 下载 Linux 内核补丁。
  - 将下载的内核补丁复制到 `/usr/src/linux` 目录。
  - 通过运行 `cd /usr/src/linux` 导航到下载目录。
  - 使用 tar、gzip 或其他解压缩工具将补丁解压到 `/usr/src/linux` 目录。
  - 应在 `/usr/src/linux` 目录中创建一个名为 `patch-2.x.x` 或 `patch-2.x.x-yy` 的文件。
  - 要将补丁应用于内核，请运行 `patch -p1 < patch-2.x.x` 或 `patch -p1 < patch-2.x.x-yy`。

- 阅读有关 Linux 安全的内容。
  - 导航到学生资源中心的第 1 章。
  - 打开 *Security Evaluation of the Linux Operating System.pdf* 并阅读内容。

- 阅读有关 Linux 内核黑客技术的内容。
  - 导航到学生资源中心的第 1 章。
  - 打开 *Linux Kernel Hacking.pdf* 并阅读内容。

![](img/0c79e6db97822eb68322dfe40d8564fe_66_0.png)

# Mac OS X 黑客技术

## 目标

完成本章后，您应该能够：

- 识别 Macintosh OS 中的漏洞
- 识别可以感染 Macintosh OS 的蠕虫和病毒
- 熟悉 Macintosh OS 的防病毒软件
- 熟悉 Macintosh OS 的安全工具

## 关键术语

**对称多处理（SMP）** 一种计算机体系结构，其中多个处理器共享相同的内存，并被分配不同的任务来执行

## 案例示例

许多 Mac 用户为其 Apple 计算机的安全性感到自豪。一位居住在瑞典的 Mac 爱好者向攻击者发起公开挑战，要求他们获取其 Mac Mini 系统的 root 控制权。他将该 Mac Mini 设置为服务器，并赋予参与者对该目标系统的本地客户端访问权限。

赢得该挑战的攻击者仅用 30 分钟就获取了系统的 root 控制权。根据赢得挑战的个人所说，在 Mac OS X 上获取 root 访问权限实际上非常容易。他利用了一个 Apple 未发布或打补丁的漏洞。据安全研究员 Neil Archibald 称，Mac OS X 中存在多种漏洞，攻击者可以利用这些漏洞。攻击者可以在系统上获得完全权限，以删除文件和文件夹或安装恶意应用程序。

## 介绍 Mac OS X 黑客技术

本章专注于 Mac OS X 的黑客技术。它介绍了 Mac OS X 的一些功能，然后讨论了影响该操作系统的漏洞。本章最后描述了可用于 Mac OS X 的各种防病毒和安全工具。

## 介绍 Mac OS

Apple 邀请开发者在 Apple 网站 http://developer.apple.com/macosx/ 上创建用于 Mac OS X 的产品。Mac OS X 包含 Cocoa，这是一组框架、API 和配套运行时，允许使用众多开源 Web、数据库、脚本和开发技术。内置的 Xcode 工具使 Mac OS X 成为一个多面化的开发平台。它包含 Automator、Core Data、Core Animation 和 Core Image 等技术，使 Mac OS X 成为最先进的操作系统。

开发者可以访问这些功能并创建应用程序，通过 AppleScript 共享视频和控制 iChat。Mac OS X 包含一个 64 位、开源的 UNIX 内核。OS X 中包含了带有 Mach 3.0 微内核的 FreeBSD 5 UNIX 发行版。其他功能包括抢占式多任务处理、对称多处理（SMP）和受保护的内存。对称多处理是一种计算机体系结构，其中多个处理器共享相同的内存，并被分配不同的任务来执行。

Mac OS X 具有面向对象的应用程序结构、过程 API 和紧密集成的 Java SE、BSD UNIX API 和库以及 X11 实现的运行时灵活性。开发者可以使用各种免费工具来构建、编译、调试、分析和改进应用程序。开发平台包括基于 GCC 4 编译器和 GNU 调试器之上的 Xcode 3 层。Mac OS X 的图形支持包括强大的图形技术，如 OpenGL、Core Animation 和 Core Image。图形层处理应用程序窗口化、2D 和 3D 绘制、动画以及多媒体。为了支持其国际市场，Apple 提供了转换实用工具，以一致地管理区域设置、日期、货币和度量系统。Mac OS X 的 Unicode 工具处理多样化的文本系统，并且国际化和本地化软件版本可以从单个应用程序图标启动。

## Mac OS X 中的漏洞

### 构造的 URL 漏洞

远程未认证的黑客可能会利用 Mac OS X 处理特制 URL 的方式来执行任意代码。当用户访问恶意设计的网页时，应用程序可能会自动启动并执行破坏性代码。这是由于 Terminal.app 在处理 URL 方案时存在的输入验证问题所致。此漏洞影响 Apple Mac OS X v10.4.11、Mac OS X Server v10.4.11、Mac OS X v10.5 和 v10.5.1，以及 Mac OS X Server v10.5 和 v10.5.1。

### CoreText 未初始化指针漏洞

Apple Mac OS X CoreText 包含一个未初始化指针漏洞，这可能允许远程未认证的攻击者在易受攻击的系统上执行任意代码。Apple Mac OS X CoreText 是用于处理 Mac OS X Tiger（10.4）及更高版本上文本的框架。如果 Mac OS X Apple CoreText 未正确初始化指针，则可能发生内存损坏。使用 CoreText 框架处理文本的应用程序可能易受攻击。通过说服用户查看特制的文本，远程未认证的 attackers 可能能够在易受攻击的系统上执行任意代码或导致拒绝服务。此漏洞已在 Mac OS X 10.4.11 和 Apple 安全更新 2007-008 中修复。

### ImageIO 整数溢出漏洞

Apple 的 ImageIO 框架包含一个整数溢出漏洞，这可能允许攻击者在易受攻击的系统上执行代码。图形交换格式（GIF）是许多 Mac OS X 应用程序支持的流行图像格式。ImageIO 允许应用程序读取和写入各种图像文件格式，包括 GIF。整数溢出漏洞仅存在于处理 GIF 文件的过程中。当用户打开恶意构造的图像时，会导致应用程序崩溃或任意代码执行。此问题不影响早于 Mac OS X v10.4 的系统。远程未认证的 attackers 可以执行任意代码或导致拒绝服务状况。恶意构造的 GIF 文件可以通过网页提供，作为电子邮件附件，或在电子邮件内部。Apple 已发布 Mac OS X 10.4.9 用于 Mac OS X 10.4（Tiger）系统，以及安全更新 2007-003 用于 Mac OS X 10.3（Panther）系统，以响应此问题。此更新通过对 GIF 文件执行额外的验证来解决此问题。

### DirectoryService 漏洞

Mac OS X 中的 DirectoryService 漏洞可能允许非特权 LDAP 用户更改本地 root 密码。这是由 DirectoryService 中的实现缺陷引起的。此问题已在 Mac OS X 10.4.9（用于 Mac OS X 10.4（Tiger）系统）和 Mac OS X 10.3（Panther）的安全更新 2007-003 中修复。

