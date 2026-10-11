
- C. `.deb`

- D. `.tgz`

## 场景

以下场景测试你对某些资源的知识。

- 1. 如果你不确定如何或使用哪个程序完成任务，你应该去哪里？

- 2. 你刚刚安装了最新的内核 `2.5.0`，但它在你的系统上运行异常且不稳定。最可能的原因是什么？

- 3. 你需要为用户安装软件包。

## 实验

### 2-1 查看内核信息

- 1. 使用连接互联网的 PC 和网络浏览器，在 `kernel.org` 上查找内核版本并记录。

- 2. 注意内核是稳定的还是开发性的。

- 3. 查找更新内核到新版本的文档。

- 4. 查找执行升级的详细和快速指南。

- 5. 验证升级对于你正在使用的 PC 是否。

## 章节问题答案

- 1. Linux 内核通过互联网发布，自其诞生以来一直如此。

- 2. Torvalds 发布最新的内核版本。

- 3. 它显示了主功能、稳定性和修订号。

- 4. 你可以找到许多资源，最好的是 `www.linux.org` 和 `www.linuxdoc.org`。

- 5. 软件包是创建程序的二进制代码集。

# 48 第 2 章 + 学习指南

- 3. 内核版本中的次版本号用于指示内核的重大变化。次版本号表示稳定性，修订号表示每次更改，而答案 D 是 Red Hat 系统中应用的补丁。回顾请参阅“内核版本 (Kernel versions)”章节。

- 4. 奇数表示开发内核，偶数表示稳定内核，预发布版可以是任何数字，且 Linux 不使用 Beta 内核。回顾请参阅“内核版本 (Kernel versions)”章节。

- 5. 偶数次版本号表示稳定内核，奇数表示开发内核，预发布版可以是任何数字，且 Linux 不使用 Beta 内核。回顾请参阅“内核版本 (Kernel versions)”章节。

- 6. 之前的内核版本存储在 `www.kernel.org`；`www.linux.org` 支持关于 Linux 的信息但会将你引导到 `www.kernel.org`；`www.linux.com` 不支持之前的 Linux 存档；最后，`www.kernel.com` 是一个商业网站。回顾请参阅“Linux内核 (Linux Kernel)”章节。

- 7. 关于 Red Hat 的最新信息位于 `www.redhat.com`，`www.linux.org` 和 `www.kernel.org` 并不致力于 Red Hat，且 `www.redhat.linux.com` 不受 Red Hat 支持。更多信息请参阅“Red Hat”章节。

- 8. Yellow Dog 使用 PowerPC 平台；Bluecat 用于嵌入式系统；Red Hat 支持所有平台；而 DragonLinux 的创建是为了在微软产品上运行。更多信息请参阅“Linux 发行版 (Linux Distributions)”和“Yellow Dog Linux”章节。

- 9. A. Kevin Fenzi 是 Security HOWTO 的共同作者；他没有为 tar、内核或 Hurd 编写 HOWTO。更多信息请参阅“KRUD”章节。

- 10. KYZO Linux 从紧凑闪存中运行；它不从硬盘或 CD-ROM 运行。更多信息请参阅“KYZO”章节。

- 11. Hard Linux 正在 IBM 的基于 PowerPC 的机顶盒中使用。Elstone 是一个服务器 Linux 发行版；Bluecat 用于嵌入式设备但不用于此特定设备；而 LEM 未被选用于 IBM 盒子。更多信息请参阅“Hard Linux”章节。

- 12. TurboLinux 是一个集群设备；Corel 和 DragonLinux 不进行集群；LinuxPPC 用于 PowerPC 且不是集群设备。更多信息请参阅“TurboLinux”章节。

- 13. NASA 的 Linux 内核是 FlightLinux。Astaro 是路由器替代品；KYZO 针对 PC 优化；而 KRUD 是 Red Hat 的定制版本。更多信息请参阅“FlightLinux”章节。

- 14. 创建程序的程序称为包 `package`。发行版是一组包；Tarball（压缩包）是由许多文件制成的单个文件；源代码创建程序。更多信息请参阅“软件包与打包解决方案 (Packages and Packaging Solutions)”章节。

# 第 2 章 ✦ 学习指南

- 15. A. Red Hat Package Manager 受 GNU GPL 保护。它不是免费软件 `Freeware`，也不受艺术许可 `Artistic License` 或闭源许可 `Closed Source license` 保护。更多信息请参阅“Red Hat Package Manager”章节。

- 16. RPM 提供所有包依赖；它通知安装程序缺失的依赖，但不安装或重新安装它们。RPM 提供升级、验证和原始源功能。更多信息请参阅“Red Hat Package Manager”章节。

- 17. B. Red Hat Package Manager 使用 `rpm` 扩展名：Debian 使用 `.deb`；Tarballs 使用 `.tar`；GZIP Tarball 使用 `.tar.gz`。更多信息请参阅“`rpm`”章节。

- 18. B. 你可以在 `www.linuxdoc.org` 找到 Linux HOWTOs；其他资源以其他方式支持 Linux 或不存在。更多信息请参阅“Linux 资源 (Linux Resources)”章节。

- 19. C. 当你尝试使用 `PING` 命令时，查找信息的第一个地方是 MAN 页面（帮助手册）；其他方法可能有效，但不确定时请使用 MAN 页面。更多信息请参阅“Linux 资源 (Linux Resources)”章节。

- 20. A. Tar 是归档——不是压缩；tar 通常用 GZIP 压缩；RPM 和 Debian 是压缩文件。更多信息请参阅“Tarball”章节。

## 场景

- 1. 最佳起点是 `www.linuxdoc.org`，因为该网站支持指南、HOWTOs、微型 HOWTO 和 FAQ。次要查找的地方是 `www.redhat.com`。更多信息请参阅“Linux 资源 (Linux Resources)”章节。

- 2. 内核 `2.5.0` 是开发内核，可能没有配置支持你的硬件，或者非常稳定。回顾请参阅“Linux 内核 (Linux Kernel)”章节。

- 3. RPM 设计用于完全安装程序，而 Tar 只是在打开它的任何地方打开并倾出文件。更多信息请参阅“Red Hat 包管理器 (Red Hat Package Manager)”章节。

## 安装

在你决定了所需的 Linux 发行版类型以及该系统将扮演的角色后，必须计划实施方案。识别所有系统硬件并验证其受 Linux 支持对于成功实施至关重要。本部分的章节将引导你通过 GUI（图形用户界面）或文本环境进行实施前规划和安装过程。安装 Linux 是为了确保正确配置系统以提供所需的内容。

## 第 3 章：实施前规划

## 第 4 章：安装

## 第 5 章：高级安装

## 文字处理

运行微软（Microsoft）操作系统的 PC 可能会使用 Microsoft Word 或 Corel WordPerfect 进行文字处理任务，而基于 Linux 的系统可以使用 Corel Word Perfect、Kword、AbiWord、StarOffice Writer 或许多基于 Linux 的文字处理器之一。使用 Linux 而不是微软或苹果操作系统在文字处理方面可能会遇到问题，因为微软没有提供 Linux 版本的 MS Word。这可能会导致文件格式兼容性出现某些问题，但所有这些文字处理器都以与其他文字处理器兼容的格式保存，因此兼容性已不再像以前那样是一个棘手的问题。使用兼容的文字处理能力使得 Linux 能够轻松地集成到企业文字处理解决方案中。

## 电子表格和数据库

尽管文字处理可能是企业环境中需求最需要的工具之一，但电子表格和数据库在工作中可能具有同等甚至更高的性。通过 Linux，用户可以使用 Corel Quattro、StarOffice Base、Kspreadsheet 以及许多其他程序创建高质量的电子表格和数据库文件。这些程序具有极高的易用性，能够在任何环境中创建电子表格或数据库。Linux 能够提供与其它操作系统中使用的程序所需的所需的兼容性。例如，Quattro、StarOffice Base 和 Kspreadsheet 可以轻松创建在格式上与其他商业应用程序兼容的电子表格或数据库。这种兼容性至关重要，因为与其他版本的电子表格和数据库的互操作使得 Linux 成为企业环境中可行的选择。

## 网页浏览
