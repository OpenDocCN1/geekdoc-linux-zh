
```
$ dpkg -S /bin/ls
coreutils: debian
```

## Linux 文档项目

Linux 文档项目（http://www.ldp.org/）提供免费的 Linux 文档，包括关于各种系统管理和编程主题的 HOWTO 指南和 FAQ（常见问题与解答）。该网站还提供了更多主题的电子书。

## GNU 项目

GNU 项目（http://www.gnu.org/）提供了大量的软件源码和相关文档。

## 新闻组

Usenet 新闻组通常是特定编程问题问题的良好来源。以下新闻组特别关注：

- `comp.unix.programmer` 处理一般的 UNIX 编程问题。
- `comp.os.linux.development` 专门处理与 Linux 应用开发相关的问题。
- `comp.os.linux.system` 是 Linux 系统开发新闻组，重点关注修改内核以及开发设备驱动和可加载模块的问题。
- `comp.programming.threads` 讨论线程编程，特别是 POSIX 线程。
- `comp.protocols.tcp-ip` 讨论 TCP/IP 网络协议族。

许多 Usenet 新闻组的 FAQ 可以在 http://www.faqs.org/ 找到。

在向新闻组发布问题之前，请检查该组的 FAQ（通常在组内定期发布），并尝试通过网络搜索找到问题的解决方案。http://groups.google.com/ 网站提供了基于浏览器的界面用于搜索旧的 Usenet 帖子。

## Linux 内核邮件列表

Linux 内核邮件列表（LKML）是 Linux 内核开发人员主要的广播通信媒介。它提供了内核开发动态的信息，并是提交内核报告和补丁的论坛。（LKML 并不是系统编程问题的论坛。）要订阅 LKML，请向 `majondomo@vger.kernel.org` 发送邮件，内容仅为单行：

```
subscribe linux-kernel
```

关于列表服务器工作原理的信息，请发送包含以下内容的邮件到 `majondomo@vger.kernel.org`：

## 网站

以下网站是特别感兴趣的：

- http://www.ldp.org/ Linux 文档项目
- http://www.minix.org/ Minix 项目
- http://www.gnu.org/ GNU 项目
- http://www.faqs.org/ FAQ
- http://groups.google.com/ Google 组
- `kernel@vger.kernel.org` 内核邮件列表地址

## 链接

以下链接是特别感兴趣的：

- http://www.kernel.org/ Linux 内核源码（Linux 源码）
- http://www.lwn.net/ Linux Kernel News（内核开发者参考）
- http://www.linuxnewbies.org/ Linux Newbies（初学者指南）
- http://www.debian.org/ Debian 社区（Debian 社区）
- http://www.ubuntu.com/ Ubuntu 社区（Ubuntu 社区）

---

*(注：由于提供的原文在后半部分出现了大量乱码或重复，上述翻译已根据上下文逻辑进行了对齐。针对 "Source code of existing applications" 之后的内容，原文's latter-half seems to contain encoding errors or partial translations.)*

**重新针对您提供的原始乱码文本进行完整翻译：**

POSIX 线程 API 在《Programming with POSIX Threads》（[Butenof, 1996]）中有详尽的描述。

《Linux and Unix Philosophy》（[Gancarz, 2003]）是对 Linux 和 UNIX 系统上应用设计哲学的简要介绍。

许多书籍提供了阅读和修改 Linux 内核源码的介绍，包括《Linux Kernel Development》（[Love, 2010]）和《Understanding the Linux Kernel》（[Bovet & Cesetti, 2005]）。

关于 UNIX 内核的更多通用背景，《The Design of the Unix Operating System》（[Bach, 1986]）仍然具有很可读性，并包含了与 Linux 相关的材料。《UNIX Internals: The New Frontiers》（[Vahalia, 1996]）综述了现代 UNIX 实现的内核内部原理。

对于编写 Linux 设备驱动程序，核心参考书籍是《Linux Device Drivers》（Corbet et al., 2005）。

《Operating Systems: Design and Implementation》（[Tanenbaum & Woodhull, 2006]）描述了使用 Minix 实现的操作系统。（另见 http://www.minix.org/）

## 现有程序的源码

查看现有应用程序的源代码可以为如何使用特定的系统调用和库函数提供良好的示例。对于使用 RPM 包管理器的 Linux 发行版，我们可以按照以下方法找到包含特定程序（如 `ls`）的包：

```
$ ls -ls
/bin/ls
$ rpm -qf /bin/ls
coreutils-5.075
```

相应的源码包将具有与上述类似的名称，后缀为 `.src.ls`。该包将位于发行版的安装媒体上，或者可以从发行者的网站下载。一旦获取该包，我们可以使用 `rpm` 命令进行安装，然后检查源码，源码通常放置在 `/usr/src/` 下的某个目录下。

在使用 Debian 包管理器的系统上，过程类似。我们可以使用以下命令确定创建程序的包（在本例中为 `ls` 程序）：

```
$ dpkg -S /bin/ls
coreutils: debian
```

## Linux 文档项目

Linux 文档项目（http://www.ldp.org/）提供免费的 Linux 文档，包括关于各种系统管理和编程主题的 HOWTO 指南和 FAQ（常见问题与解答）。该网站还提供了更多主题的电子书。

## GNU 项目

GNU 项目（http://www.gnu.org/）提供了大量的软件源码和相关文档。

## 新闻组

Usenet 新闻组通常是特定编程问题的良好来源。以下新闻组特别关注：

- `comp.unix.programmer` 处理一般的 UNIX 编程问题。
- `comp.os.linux.development` 专门处理与 Linux 应用开发相关的问题。
- `comp.os.linux.system` 是 Linux 系统开发新闻组，重点关注修改内核以及开发设备驱动和可加载模块的问题。
- `comp.programming.threads` 讨论线程编程，特别是 POSIX 线程。
- `comp.protocols.tcp-ip` 讨论 TCP/IP 网络协议族。

许多 Usenet 新闻组的 FAQ 可以在 http://www.faqs.org/ 找到。

在向新闻组发布问题之前，请检查该组的 FAQ（通常在组内定期发布），并尝试通过网络搜索找到问题的解决方案。http://groups.google.com/ 网站提供了基于浏览器的界面用于搜索旧的 Usenet 帖子。

## Linux 内核邮件列表

Linux 内核邮件列表（LKML）是 Linux 内核开发人员主要的广播通信媒介。它提供了内核开发动态的信息，并是提交内核报告和补丁的论坛。（LKML 并不是系统编程问题的论坛。）要订阅 LKML，请向 `majondomo@vger.kernel.org` 发送邮件，内容仅为单行：

```
subscribe linux-kernel
```

关于列表服务器工作原理的信息，请发送包含以下内容的邮件到 `majondomo@vger.kernel.org`：

## 网站

以下网站是特别感兴趣的：

- http://www.ldp.org/ Linux 文档项目
- http://www.minix.org/ Minix 项目
- http://www.gnu.org/ GNU 项目
- http://www.faqs.org/ FAQ
- http://groups.google.com/ Google 组
- `kernel@vger.kernel.org` 内核邮件列表地址

## 链接

以下链接是特别感兴趣的：

- http://www.kernel.org/ Linux 内核源码（Linux 源码）
- http://www.lwn.net/ Linux Kernel News（内核开发者参考）
- http://www.linuxnewbies.org/ Linux Newbies（初学者指南）
- http://www.debian.org/ Debian 社区（Debian 社区）
