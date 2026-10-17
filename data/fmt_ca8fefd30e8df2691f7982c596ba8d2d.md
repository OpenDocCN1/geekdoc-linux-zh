
此时，你有两个选择：

- 修复错误并重新编译
- 移除故障模块并等待

# 运行时错误、引导程序和内核

运行时错误发生在内核加载期间。错误消息显示在屏幕或写入`/var/log/messages`文件。引导程序问题显示在屏幕上；不产生日志文件。内核`oops`是运行内核中的错误，错误消息写入`/var/log/messages`文件。网上有很多文档可以排除`LILO`、`GRUB`或内核在启动期间提供的任何错误。找到这些文档的最佳方法是访问你喜爱的搜索引擎并输入你收到的错误关键词。你需要调整使用的关键词以缩小范围。

在此类别中，最常见的问题涉及`LILO`配置问题。这些问题的诊断和解决方案可以在 Linux 文档项目网站上的`LILO` mini HOWTO 中找到：`http://www.ibo.org/pub/Linux/docs/HOWTO/other-formats/html_single/LILO.html`。

如果你有`GRUB`问题，在线有`GRUB`手册：`://www.gnu.org/software/grub/manual/`

Google 专门为其数据库创建了 Linux 区域，这应该比任何其他搜索引擎都能更快地获取 Linux 信息。
Usenet 群组可以通过`http://www.google.com/grphph`进行搜索。
邮件列表讨论可以在邮件列表存档 (`MARC`) 中搜索：`http://marc.theamsgroup.com/`

## 相关的 FEDORA 和 LINUX 命令

在 Fedora 中管理内核及其模块时，你将使用到以下命令：

- `gcc`—GNU 编译器系统
- `make`—GNU 项目和文件管理命令
- `mkbootdisk`—Fedora Core 的启动磁盘创建工具
- `sysctl`—运行时操作内核变量的接口
- `mkinitrd`—为启动加载程序创建内存磁盘（RAM-disk）文件系统

# 参考资料

[`http://www.kernel.org/`](—Linux 内核存档。Linux 内核所有开发讨论的源地。

[`http://www.kerneltraffic.org/kernel-traffic/index.html`](—Linux 内核流量（Linux Kernel Traffic）。每周生成的 Linux 邮件列表摘要版本和评论。

[`http://www.gnu.org/`](—自由软件基金会。内核开发过程中使用的程序的手册和软件来源。`make`和`gcc`等工具在此处有它们的官方文档。

[`http://slashdot.org/article.php?id=01/08/22/145328&mode=thread`](—著名的 Alan Cox AC 补丁（以他的名字命名）。

[`http://www.digitalhermit.com/linux/Kernel-Build-HOWTO`](—Linux 重编译指南；配置、编译和故障排查。

[`http://www.ibiblio.org/pub/Linux/docs/other-formats/html_single/KernelAnalysis-HOWTO.html`](—内核分析（KernelAnalysis）HOWTO。描述内核的神秘机制。

[`http://www.ldp.org/HOWTO/Module-HOWTO/`](—内核模块 HOWTO。包含了关于未解析符号的良好讨论。

[`http://www.ibiblio.org/pub/Linux/docs/other-formats/html_single/Modules.html`](—Linux 模块安装 HOWTO；一份关于重新编译内核模块的旧文档。

[`http://www.ldp.org/`](—Linux 文档项目（Linux Documentation Project）。所有 Linux 文档的圣地。关于所有 Linux 的 HOWTO 文档、常见问题解答（FAQs）以及在线书籍的极佳来源。

[`http://www.minix.org/`](—minix 非官方网站。它包含了关于 minix 的链接以及指向实际主页的链接。虽然 minix 仍受版权保护，但所有者对所有人拥有无限权利。它是开发 Linux 时使用的操作系统。

[`http://jungla.dit.upm.es/-jmseyas/linux/kernel/hackers-docs.html`](—一个包含 Linux 内核文档、书籍、黑客巨著以及对初学者和丰富的 Linux 内核及内核模块开发人员有用信息的网页。如果你安装了 Fedora 内核源码，此列表位于`/usr/src/kernels/linux-2.6/Documentation/kernel-docs.txt`文件中。

# 第七部分

# 附录

在本部分

- 附录 A Fedora 和 Linux 互联网资源 999

本页特意留

# 附录 A

# Fedora 和 Linux 互联网资源

# 在附录中

- 网站与搜索引擎
- Usenet 新闻组
- 邮件列表
- 互联网中继聊天（IRC）

Linux 拥有丰富的互联网支持，形式包括：提供技术信息的网站、特定程序文档、针对性白皮书、错误修复、用户体验、第三方商业技术支持，甚至是经过特定微调的克隆版发行版的免费版本。

本附录列出了许多支持网站、FTP 仓库、Usenet 新闻组和电子邮件列表，你可以通过它们获取更多信息并为你的 Fedora 获取帮助。

如果你需要 24/7 服务

如果你是小型企业、公司或企业级 Red Hat Linux 用户，不要忘记你随时可以寻求供应商 Red Hat 或 Dell、HP 等第三方公司。这些公司提供 24/7 的现场服务、电话、电子邮件甚至按事件付费的服务，为 Red Hat 服务器提供商业技术支持。Red Hat 为其软件产品提供多种支持选项。在购买 Red Hat 软件时，可以在[`http://www.redhat.com/rhel/purchase/`](http://www.redhat.com/rhel/purchase/)了解更多支持选项。请记住 Fedora 不是 Red Hat 的官方支持产品。如果你需要帮助，请尝试[`http://fedorapro.org/`](http://fedorapro.org)。

附录分为以下章节：

- 按类别分类的 Linux 信息网站
- 与 Linux 相关的 Usenet 新闻组

# 附录 A Fedora 和 Linux 互联网资源

- 提供 Linux 用户和开发者讨论的邮件列表
- 用于 Linux 信息的互联网中继聊天组

本附录还列出了在使用 Fedora 或`Xorg`等特定组件时可能产生通用兴趣的网站。我们已尽力确保 URL 的准确性，但请记住，互联网是不断在变化的！

使用`yum`保持更新

了解错误修复、安全更新和其他错误说明对于 Fedora 系统的成功和健康至关重要。在使用 Fedora 时，为了跟上最重要的进展，请务必注册 Fedora 公邮件列表。该列表会告诉你发布了哪些更新以及结果修复了哪些问题。访问：[`http://www.redhat.com/mailing/listinfo/fedora-announce-list`](http://www.redhat.com/mailing/listinfo/fedora-announce-list)注册此邮件列表。你还应该使用`yum`命令（root 权限）来保持更新。
