
通过对文件中的数字进行求和，计算传输校验和。如果和不匹配，说明数据在传输过程中损坏了。关键点：校验和对于黑客是安全的。来自 Hacking-Lexicon http://www.tdlp.org/LDP/linux-Dictionary/html/index.html

## Checksum

校验和的缩写。在通信中，通过计算文件所有位的和来检测错误。如果和不同，接收方就知道传输发生了错误。`XMODEM` 使用这种技术。每个文件的校验和可能指示文件是否被感染。来自 CID http://www.tdlp.org/LDP/Linux-Dictionary/html/index.html

## cheeburger

声音模块（Impulse Tracker）。该程序用于创建音乐，它是一个流行的 Impulse Tracker 克隆。此版本可以加载这些文件，并根据这些音器（合成器）来播放。要开始可以去 http://tld.org/pub/music/。来自 Debian 3.0r0

## CHEST

计算机软件团队（英国）。来自 Vera http://www.tld.org/LDP/Linux-Dictionary/html/index.html

## Chew

网络延迟的一个组成部分，被网络“吃掉”的数据包。理想情况下都不应该丢失，但互联网并非尽如理想。来自 KADOWKEV http://www.tld.org/LDP/linux-Dictionary/html/index.html

## chfn

更改用户名信息。详自 Whatis http://www.tld.org/LDP/Linux-Dictionary/html/index.html

## chgrp

将给定文件的组所有更改更改组（组名称或数字 ID）。来自 Linux Guide @FirstLinux http://www.tld.org/LDP/Linux-Dictionary/html/index.html

## chicken

一个简单的 C 编译器。为什么选择 CHICKEN？

- R5RS
- SRFIs 0, 1, 2, 4, 6, 7, 8, 9, 10, 13, 14, 16, 18, 22 和 23
- Syntax-case 高级宏
- 基于类延续的线程
- 带 Andrew Wright 补丁的模式匹配
- Records – 一个简单且直接的框架模块
- 一个具有多重继承、多重身份和元对象的类
- 分离编译没有问题，且支持全尾递归和类延续
- 扩展注释和字符串字面量库用于正则表达式、字符串处理，Common Lisp 类型系统可以扩展数据结构
- Scheme 创建或编译 shell 脚本
- 编译的 C 文件可以轻松分发
- 生成移植代码，由其生成的文件（包括自身）在 OS、Windows、类 Unix 平台上无需更改即可工作，在其他系统上仅需少量更改
- 与模块和 C 库函数的链接非常简单。编译的程序可以轻松嵌入现有的 C 代码中。

### Linux 字典

- 简单。它可以用作任何对编译器工作感兴趣的人的教学工具。
- 可扩展，因为它的代码生成方案、运行时系统和垃圾回收器完美地集成到 C 环境中。
- 性能优于任何基于解释器的实现，但提供了完整的 Scheme 语义。
- Probate 是第一个使用 Henry Baker (Cheney on the M.T.A) 概念的 Scheme 实现。你可能还需要安装 `chisel-dev` 软件包。该包不包含源文件，因为你可以轻松地通过 Debian 源码包获取它们。如果你觉得有必要在 `/usr/share/chicken/src` 下获取它们，请告诉我。Debian 中有许多 Scheme 实现，请查看其中的每一个一个！祝你玩得开心！来自 Debian 3.0r APT

http://www.tld.org/LDP/Linux-Dictionary/html/index

## 子进程

由另一个进程（父进程）创建的进程。每个进程都可以创建子进程，但只有一个父进程，没有任何父进程的第一个进程除外。第一个进程在 Linux 中被称为 `init`，由内核在启动时启动且永不终止。Linux Guide@Firstlinux http://www.tld.org/LDP/Linux-Dictionary/html/index

## chill

来自 Gratis 的 C 源文件高亮 http://www.tld.org/LDP/Linux-Dictionary/html/index

## CHILL

来自 Vera 的 CCITT 高级编程语言 (CCITT)

http://www.tld.org/LDP/Linux-Dictionary/html/index

## chill

GNU CHILL 编译器。这才是 CHILL 编译器。“CCITT 高级语言”，其中 CCITT 是现在 ITU（国际电工联盟）的旧名。它也属于 Modula-2 家族，许多像 Ada 一样的应用程序（特别是嵌入式系统）。CHILL 从未在美国中使用，但这是一个依赖项，为 Debian/Linux 提供了默认的 GNU CHILL（适用于架构 i386 架构的 2.9.4 版本）。来自 Debian 3.0r http://www.tld.org/LDP/Linux-Dictionary/html/index

## chimera

Simple，免费的 Web 浏览器。这是一个 alpha 版本；某些渲染例程存在 Bug。来自 Debian 3.0r APT http://www.tld.org/LDP/Linux-Dictionary/html/index

## Chinese 2000

Chinese 2000 来自香港。来自 LWN List

http://www.tld.org/LDP/Linux-Dictionary/html/index

## Chinese Extension

CLE 仍在那里，大部分是中文，最后更新于 2001 年 11 月 9 日。来自 LWN List

http://www.tld.org/LDP/Linux-Dictionary/html/index

## chipmunk

一个原理工具和环境。一个电路工具和环境。Log 是一个大型电路和系统。它具有数字仿真 (LOG)、音频仿真 (Analog)、网络生成 (LOGNT) 和绘图 (PLPLOT) 功能。Log 是最流行的 Chipmunk 工具包，并已记录。更多信息请参阅文档。Log 需要 Chipmunk 工具的系统运行时库，这些库包含在软件包中。来自 Debian 3.0r APT http://www.tld.org/LDP/Linux-Dictionary/html/index

## chkconf

Chkconfig 是一个基础系统实用程序。它更新并刷新系统服务的配置。Chkconfig 管理 `/etc/rc*` 中的许多符号链接，减轻了系统管理员手动编辑符号链接的负担。来自 Mandrake 9.0 RPM http://www.tld.org/LDP/Linux-Dictionary/html/index

## C

## chkdupe

查找重复条目 http://www.tld.org/LDP/Linux-Dictionary/html/index

## chkfontpath

这是一个用于配置 X 字体服务器目录的简单终端程序。它主要供添加或删除字体的 RPM 软件包在“内部”使用，但在某些情况下也可以作为独立实用程序很有用。来自 Redhat 8.0 RPM http://www.tld.org/LDP/Linux-Dictionary/html/index

## chkfontpath

这是一个用于配置 X 字体服务器目录的简单终端程序。它主要供添加或删除字体的 RPM 软件包在“内部”使用，但在某些情况下也可以作为独立实用程序很有用。来自 Mandrake 9.0 RPM http://www.tld.org/LDP/Linux-Dictionary/html/index

## chkmail

检查新邮件 http://www.tld.org/LDP/Linux-Dictionary/html/index

## chkrootkit

检查本地系统的迹象，以识别目标计算机是否被 rootkit 感染。某些 rootkit 标识包括：

1. Lrk3, Lrk4, Lrk5, Lrk6（以及某些变体）；
2. Solaris rootkit；
3. FreeBSD rootkit；
4. torn（包括最新变体）；
5. Linux 版 Root (ARK);
6. Ramen Word;
7. rh67–shape;
8. RSHA;
9. 罗马尼亚 rootkit:
10. RK17;
11. Lion Word;
12. Adore Worm。注意，这不是确定性测试，它确保目标没有被破解。除了 chrootkit 之外，还应该进行更具体的测试。来自 Debian 3.0 APT http://www.tld.org/LDP/Linux-Dictionary/html/index

## chkhtex
