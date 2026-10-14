
如果你对编程和内核相关事务比较熟悉，可以查看内核源码中 /usr/src/linux-2.6/ 目录下的 MAINTAINERS 文件，找到相应代码的维护者。建议的做法是联系维护者，看他是否了解你遇到的问题。如果针对特定错误没有相关文档记录，也可以将错误提交到内核邮件列表。相关指南在内核源码根目录的 README 文件中，位于 "If Something Goes Wrong." 一节。

## 运行时错误、引导加载程序问题和内核 Oops

运行时错误在内核加载时发生。错误信息会显示在屏幕上，或写入 /var/log/messages 文件。引导加载程序问题会将信息显示在屏幕上，不会生成日志文件。内核 Oops 是运行中的内核出现的错误，错误信息会写入 /var/log/messages 文件。

互联网上已有大量优秀的文档，可用于排查 LILO、GRUB 或内核在启动时可能出现的几乎各种错误。查找这些文档的最佳方式是使用你常用的搜索引擎，输入你所遇错误的关键字。随着搜索的深入，你可能需要调整关键字。

在这一类问题中，最常见的是 LILO 配置问题。这些问题的诊断和解决方案可以在 Linux 文档项目网站上的 LILO mini-HOWTO 中找到，网址为 http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/LILO.html.

如果遇到 GRUB 问题，GRUB 手册在线地址为 http://www.gnu.org/software/grub/manual/.

## 提示

为了获得最佳结果，请访问 http://www.google.com/linux 查找互联网上所有与 Linux 相关的内容。Google 专门在其数据库中创建了 Linux 专区，应该能比其他搜索引擎更快地访问 Linux 信息。
Usenet 新闻组的帖子可在 http://www.google.com/grphp 搜索。
邮件列表讨论可在 Mailing list ARChives (MARC) 中搜索，网址为 http://marc.theaims group.com/.

## 相关的 Ubuntu 和 Linux 命令

在 Ubuntu 中管理内核及其模块时，你将使用以下命令：

- gcc—GNU 编译器系统
- make—GNU 项目及文件管理命令
- mkbootdisk—Ubuntu 的启动盘创建工具
- sysctl—在运行时操作内核变量的接口
- mkinitrd—创建用于引导加载支持的 RAM 磁盘文件系统

## 参考

- http://www.kernel.org/—Linux 内核档案。所有 Linux 内核开发讨论的源头。
- http://www.kerneltraffic.org/kernel-traffic/index.html—Linux Kernel Traffic。每周生成的 Linux 内核邮件列表的摘要和评论。
- http://www.gnu.org/—自由软件基金会。提供内核编译过程中所用程序的手册和软件。make 和 gcc 等工具的官方文档都在这里。
- http://slashdot.org/article.pl?sid=01/08/22/1453228&mode=thread—著名的 AC 补丁，源自 Alan Cox，并以他的名字命名。
- http://www.digitalhermit.com/linux/Kernel-Build-HOWTO.html—Linux 内核重建指南；涵盖配置、编译和故障排查。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/KernelAnalysis-HOWTO.html—KernelAnalysis HOWTO。描述内核神秘的内在运作机制。
- http://www.tldp.org/HOWTO/Module-HOWTO/—内核模块 HOWTO。包含关于未解析符号的深入讨论。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Modules.html—Linux 内核模块安装 HOWTO；一份较老的文档，讨论重新编译内核模块。
- http://www.tldp.org/—Linux 文档项目。所有 Linux 文档的圣地。优秀的 HOWTO 文档、FAQ 和在线书籍来源，全部关于 Linux。
- http://www.minix.org/—非官方的 minix 网站。其中包含一系列关于 minix 信息的链接，以及指向实际主页的链接。尽管 minix 仍然受版权保护，但其所有者已授予所有人无限权利。亲自了解一下用于开发 Linux 的操作系统。
- http://jungia.dit.upm.es/~jmseyas/linux/kernel/hackers-docs.html—网页，提供 Linux 内核文档、书籍、黑客巨著以及其他有用信息的链接，面向新手和经验丰富的 Linux 内核及内核模块开发者。如果你安装了 Ubuntu 内核源码，还可以在 `/usr/src/linux-2.6/Documentation/kernel-docs.txt` 文件中找到该列表。

