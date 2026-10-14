

### pmake-customs — (Version 2.1.33, 982K)

Customs 是 PMake 的远程执行设施。Customs 设计用于在具有一致共享文件系统的机器网络上运行。Customs 需要 Sun RPC 以使用 XDR（外部数据表示）例程进行日志功能。指定一台服务器作为主代理，它还负责记录机器何时宕机、哪些机器会接受来自给定机器的任务以及将可用机器分配给请求客户端。主任务不会分配给任何一台机器，而是当之前的 master 死亡时由活动代理之间决定。客户端提供以下功能：

-   修改本地机器的可用性标准（importquota）
-   查找网络上所有注册主机的状态（reginfo）。
-   中止、重启或 ping 网络上任何 customs 代理（cctrl）。
-   从 shell 导出命令（export）。
-   接受网络上所有主机的日志信息（logd）。

### rcs — (Version 5.7, 536K) [W][S]

修订控制系统（RCS）是一种管理文件多个版本的管理系统。RCS 自动化了文件修订的存储、检索、记录、标识和合并。RCS 对于频繁修订的文本文件很有用（例如程序、文档、图形、论文和格式化信件）。如果您需要一个管理文件不同版本的管理系统，则应安装 rcs 软件包。

## Documentation

### bash2-doc — (Version 2.03, 2,275K)

这是 GNU Bourne Again shell 的独立文档包。

### faq — (Version 5.2, 891K)

faq 软件包包含来自 SunSITE 网站（http://sunsite.unc.edu/pub/Linux/docs/faqs/linux-faq/Linux-FAQ）的关于 Linux 的常见问题解答（FAQ）文本。Linux FAQ 是关于 Linux 的绝佳信息来源。如果您想在自己的机器上阅读 Linux FAQ，请安装 faq。

### gimp-manual — (Version 1.0.0, 17,979K)

（FrameMaker）源代码。提供了 FrameMaker 源代码，供希望为图形文档项目做出贡献的人使用。对 GUM 的提交受手册的许可协议和条款约束，该协议和条款包含在文件 COPYING 中。GUM 是使用 GIMP 的完整指南。此版本的 GUM 相对于以前的版本有所改进。请务必查看新的图库章节，其中提供了 GIMP 功能的良好概述。图库展示了很酷的图像，并为您提供使用 GIMP 创建它们的提示。有关 GUM 的更多信息，请查看 GUM 网站 http://manual.gimp.org/。

### gnome-users-guide — (Version 1.0.5, 3,564K) [W]

此软件包将在您的计算机上安装 GNOME 桌面环境的用户指南。如果您将使用 GNOME 并希望有一个快速、方便的参考资料，则应安装此软件包。

### helptool — (Version 2.4, 23K) [W][S]

helptool 为搜索许多可用的帮助来源（包括手册页和 GNU texinfo 文档）提供统一的图形用户界面。如果您想使用它来搜索帮助文件，请安装 helptool。您需要安装 X Window System 才能使用 helptool。

### howto — (Version 6.0, 11,103K)

Linux HOWTO 是描述配置或使用 Linux 的特定方面的详细文档。Linux HOWTO 是关于系统的实用信息的绝佳来源。这些文档的最新版本位于 http://sunsite.unc.edu/linux。如果您想能够从自己的系统访问 Linux HOWTO 文档，请安装 howto 软件包。

### howto-chinese — (Version 6.0, 13,445K)

howto-chinese 软件包包含已翻译成中文的 Linux HOWTO 文档。Linux HOWTO 是描述配置或使用 Linux 的特定方面的详细文档。如果您想使用中文 Linux HOWTO 文档，请安装 howto-chinese 软件包。请注意，并非所有 HOWTO 都已翻译。如果您需要完整的 HOWTO 集合，您需要安装英文版本（howto 软件包）。

