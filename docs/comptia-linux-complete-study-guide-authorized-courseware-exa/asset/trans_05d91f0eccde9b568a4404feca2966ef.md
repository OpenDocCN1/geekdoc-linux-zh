

## 可信主机
一种安全系统，服务器信任一组指定的客户端来管理安全的关键方面。可信主机模型被 NFS 和其他一些 Linux 服务器使用，但在广泛的互联网上使用时存在风险。

## 隧道
使用一种协议来承载另一种协议流量的过程。隧道功能使你在另一种协议中使用时能够获得一种协议的优势。例如，*Secure Shell (SSH)* 可用于隧道传输各种其他协议，从而为未加密的协议添加加密。

## 双绞线
一种布线类型，其中导线对相互缠绕（通常包裹在塑料护套中）。双绞线电缆常用于以太网和其他某些网络布线。许多电话线也使用双绞线电缆。

## U

- **UDF** 参见 *Universal Disc Format* (UDF)。
- **UDP** 参见 *User Datagram Protocol* (UDP)。
- **UHCI** 参见 *Universal Host Controller Interface* (UHCI)。
- **UID** 参见 *user ID* (UID)。
- **umask** 参见 *user mask* (*umask*)。

## Unicode
用于表示多种字母和其他书写系统文本的标准。另见 *Unicode Transformation Format* (8-bit)。

## Unicode 转换格式 (8-bit)
*Unicode* 的可变长度编码格式。UTF-8 正在逐步取代 ASCII 作为标准编码方法。

## 通用光盘格式 (UDF)
下一代光盘文件系统，常用于 DVD-ROM。

## 通用主机控制器接口 (UHCI)
管理 USB 1.x 端口的常见硬件标准。

## 通用串行总线 (USB)
一种用于低中速外部设备的接口类型，例如键盘、鼠标、摄像头、调制解调器、打印机、扫描仪和可移动磁盘驱动器。USB 2.0 提高了速度，使得 USB 在要求较低的应用中可用于硬盘。

## 非特权端口
编号大于 1024 的端口（参见 *port number*）。任何用户都可以访问此类端口，因此常用于客户端程序和可能合法地由普通用户运行的少数服务器。另见 *privileged port*。

## 不可共享文件
不应与其他计算机共享的文件。示例包括特定系统的配置文件（如 *`/etc`* 的大部分内容）以及 *`/var`* 某些子目录中的特定系统队列目录。

## USB
参见 *Universal Serial Bus (USB)*。

## USB 集线器
一种硬件，允许将多个 USB 设备连接到计算机上的单个 USB 连接器。

## 用户 cron 任务
由个人用户创建的 cron 任务，用于处理该用户的任务，例如在深夜其他用户不会受到该任务 CPU 需求干扰时运行 CPU 密集型任务。另见 *system cron job*。

## 用户数据报协议 (UDP)
用于 TCP/IP 栈的传输层协议。UDP 是一个简单且高效的协议，但缺乏错误检查和其他有助于维持连接的高级功能。

## 用户 ID (UID)
与特定账户关联的数字。Linux 内部在大多数操作中使用 UID，并且仅在与人交互时才转换为关联的用户名。

## 用户掩码 (umask)
表示在进程创建新文件时将从文件权限中移除的权限位的位模式。

## 用户名
与账户关联的名称，例如 *theo* 或 *miranda*。Linux 用户名区分大小写，长度可以是 1 到 32 个字符，尽管它们通常全为小写且不超过 8 个字符。

## UTC
参见 *Coordinated Universal Time (UTC)*。

## UTF-8
参见 *Unicode Transformation Format (8-bit)*。

## V

## 变量
在计算机编程或脚本中，数据的占位符。变量可能从一个程序运行到另一个运行发生变化，甚至在单个程序运行期间也会发生变化。

## 变量文件
数据可能随时更改的文件。示例包括用户数据文件和服务器维护的队列。

## 虚拟文件系统
不与真实磁盘分区、可移动磁盘或网络导出对应的文件系统。一个常见示例是 */proc*，它提供了对计算机硬件信息的访问。

## W

## 控件
GUI 显示中的控件或装饰，例如按钮或菜单。

## 控件集
帮助程序员创建 GUI 显示的编程工具集合，例如对话框、菜单和滚动条。

## 通配符
一个字符或字符组，当在 shell 中作为文件名的一部分使用时，匹配多个字符。例如，b??k 匹配 book、back 和 buck 以及其他许多可能性。

## 窗口管理器
为 X 提供的简单窗口提供装饰和功能扩展的程序。Linux 支持数十种窗口管理器。

## Y

## Yellow Dog Updater, Modified (YUM)
与 RPM 包相关的包管理工具。YUM 允许直接从网络仓库安装包和更新，包括依赖项解析。

## YUM
参见 *Yellow Dog Updater, Modified (YUM)*。

## X

## X
参见 *X Window System*。

## X 核心字体
由 X 服务器管理的字体。

## X 显示管理器控制协议 (XDMCP)
用于跨网络管理 X 连接的协议。XDMCP 也用于为 Linux 工作站显示本地 GUI 登录屏幕。Linux 常见的 XDMCP 服务器包括 X Display Manager (XDM)、GNOME Display Manager (GDM) 和 KDE Display Manager (KDM)。

## X 逻辑字体描述 (XLFD)
描述 X 核心字体的格式。程序在告知 X 显示字体时使用 XLFD，XLFD 也出现在 X 核心字体配置文件中。

## X 服务器
为计算机实现 X 的程序；特别是与视频硬件直接交互最多的组件。

## X 窗口系统
Linux 的 GUI 环境。一种支持网络、跨平台的 GUI，依赖于几个额外组件（如窗口管理器和控件集）以提供完整的 GUI 体验。另见 *X server, XFree86,* 和 *X.org-X11*。

## XDMCP
参见 *X Display Manager Control Protocol (XDMCP)*。

## XFree86
Linux 和其他操作系统的一套 X 服务器及相关实用程序。大多数发行版已放弃 XFree86，转而使用 X.org-X11。

## XFS
参见 *Extents File System (XFS)*。

## XLFD
参见 *X logical font description (XLFD)*。

## X.org-X11
Linux 最常见的 X 服务器。衍生自 XFree86。

## 索引

给读者的注：在本索引中，**粗体**页码表示主题的的主要讨论。*斜体*页码表示插图。

- **A**
  - .a 文件名扩展名, 79
  - Accelerated-X 服务器, 269–270
  - 访问
    - 文件。*参见 permissions*
    - 远程, 291–295, 292
    - root, 494–495
    - SSH, 503
    - xinetd 配置, 481–482
  - CUPS 打印中的访问控制行, 310
  - 访问控制列表 (ACLs), **199**
  - 访问时间, 文件, 185, 205
  - 无障碍问题, 295–297, 296
  - 无障碍选项卡, 296, 296
  - 账户。*参见 users and user accounts*
  - ACLs (访问控制列表), **199**
  - 操作
    - 运行级别, 243
    - 系统日志文件, 351
  - Active Directory (AD) 域, 343
  - 活动分区, 240
  - 地址解析协议 (ARP), 392
  - 地址
    - DMA, 113
    - I/O, 112–113
    - IP。*参见 IP 地址*
    - 网络。*参见网络地址*
  - adduser 命令, 334–335
  - 管理。*参见系统管理*
  - 管理员, 组, 346
  - Advanced Linux Sound Architecture (ALSA) 音频驱动程序, 443
  - 高级技术附件 (ATA)
    - 硬盘接口, 106
  - Aladdin 免费公共许可证 (AFLPL)
    - Ghostscript, 307
  - alias 命令, 433
  - 别名
    - 命令, 433, 495
    - 电子邮件, 453
    - root, 494
  - 别名文件, 453
  - 字体别名, 287
  - alien 实用工具, 73–74
  - 允许的 IP 和网络地址, 481
  - 允许用户列表
    - at 命令任务, 373
    - cron 任务, 369
  - SELECT 中的字母测试, 462
  - ALSA (Advanced Linux Sound Architecture) 音频驱动程序, 443
  - 备用配置文件, 232
  - 美国标准信息交换码 (ASCII), 302
  - 和号 (&)
    - 后台程序, 91, 432
    - 重定向, 15
    - 脚本, 437, 442
  - anacron 程序, 371–373
  - 系统日志文件分析工具, 357
  - and 运算符
    - 脚本, 442
    - SELECT, 462
  - 匿名 FTP 站点, 418
  - 字体反锯齿, 287
  - aplay 命令, 443
  - APM (Apple Partition Map), 131
  - 外观首选项对话框, 298, 298

