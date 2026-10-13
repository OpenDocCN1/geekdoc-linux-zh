
| xftp | 151623 | X11 ftp 客户端 |

| xhtalk | 70532 | X11 对话 |

| xinfo | 56557 | X11 GNU info |

| xirc | 88420 | 基于 X 的 IRC 客户端 |

| xkeys | 100798 | 键盘映射 |

| xless | 42179 | X11 less |

| xli | 265488 | X11 图像 |

| xlife | 56289 | X11 生活 |

| xlock | 44044 | X11 锁 |

| xlogin | 35811 | X11 登录 |

| xmftp | 145392 | X11 FTP |

| xmine | 27255 | X11 矿 |

| xmix | 15708 | X11 混合器 |

# 表 B.1 续

| 包名 | 大小 (字节) | 描述 |

|---|---|---|

| xmp | 19696 | X 播放器 |

| netload | 138111 | X11 加载 |

| xntp | 357125 | 网络时间协议 (NTP) |

| xview | 206195 | X11 查看 |

| xshared | 329063 | Usenet 新闻阅读器 |

| xrn | 25734 | X11 新闻 |

| xsc | 241804 | X11 屏幕 |

| xat | 111203 | X11 cat |

| xselect | 220539 | X11 选择 |

| xsnow | 361823 | X11 雪花 |

| xspeak | 96124 | X11 语音 |

| xgaf | 351672 | X11 前端 |

| xga | 219738 | X11 SVGA |

| x11 | 355574 | 用于 X11 系统的 X11 客户端 |

| xysinfo | 270125 | X11 info |

| xtail | 138321 | X11 tail |

| xtalk | 778502 | X11 对话 |

| xtar | 129265 | X11 tar |

| xtris | 514537 | X11 俄罗斯块 |

| xtexit | 440441 | X11 退出 |

| xtool | 344232 | X11 工具 |

| xtpl | 221290 | X11-pl |

| xv | 505765 | X11 |

| xv32aout | 328070 | X11-out |

| xv32base | 246891 | X11-base |

| xv32dev | 124140 | X11-dev |

| xv32slib | 205260 | X11-lib |

| xvga16 | 214787 | X11-16 |

| xvier | 372937 | X11 查看器 |

# SuSE Linux 包列表

| 包名 | 大小 (字节) | 描述 |

|---|---|--|

| xwb | | 编程接口 |

| xwpe | 116304 | 编程环境 |

| xdb | 108760 | gdb 的图形界面 |

| xzap | 453217 | 显示运行的应用程序 |

| yacc | 9629 | "bison -y" 的反应应该完全相同 |

| yast | 37237 | SuSE 的 YaST 工具 |

| ypclient | 25734 | NIS 客户端 |

| ytree | 241804 | (DOS) XTree 克隆 |

| zip | 111203 | 压缩和文件打包工具 |

| ziptool | 220539 | I ZIP 和 JAZ 驱动器工具 |

| zircon | 15708 | 基于 Tcl/Tk 的 IRC 客户端 |

| zoo | 19696 | 基于 Lempel-Ziv 算法的压缩器 |

| zsh | 1981 | Zsh Shell |

# 附录 C

# SuSE Linux HOWTO

参考

信息（见表 C.1）是 HOWTO 文档集的方便交叉引用。这些文档安装在 `/usr/doc/howto/en` 目录下。它们包含了对 200 多个主题的指针、提示和参考信息。你可以通过 SuSE Linux 帮助命令 `usehelp`（它会启动 Netscape Navigator 或 lynx 纯文本浏览器）提供的索引访问这些文档，也可以使用 `zless` 命令读取单个文档，如下（文档已压缩以节省硬盘空间）：

```
# zless /usr/doc/howto/en/UUCP-HOWTO.gz
```

此命令将在你的控制台或 X11 终端窗口显示 UUCP-HOWTO。如果不压缩，这些 HOWTO 文档将占用 25MB 以上的硬盘空间；但只需要 17MB，因为它们是用创建本附录的 `find`、`sort`、`xargs` 和 `head` 命令压缩的，例如：

```
# gunzip /usr/doc/howto/en/*
# find /usr/doc/howto/en -name *HOWTO* | sort ; xargs head -v -n 50 >howto.index
```

HOWTO 文档可以帮助你在配置系统前后进行问题研究和故障排查，它们是你 Linux 发行版的宝贵资产。

文中包含另一个表格（表 C.2），其中包含了 mini-HOWTO 的索引，这是另一组 HOWTO 文档。这些文档比普通的 HOWTO 短得多，并且包含关于更特定主题的信息。

## 表 C.1 SuSE Linux 6.2 HOWTO 交叉引用

| HOWTO 文件名 | 说明 |

|---|---|

| 3Dfx-HOWTO | Linux 下 3Dfx 图形加速器芯片支持说明 |

| AX25-HOWTO | 如何安装和配置 AX.25 业余无线电支持 |

| Access-HOWTO | Linux 的自适应访问和禁用访问 |

| Alpha-HOWTO | Alpha CPU 概述及对 Linux 的支持 |

| Assembly-HOWTO | Linux 汇编语言和工具 |

| Bash-Prompt-HOWTO | 如何控制 Bash 提示符 |

| Benchmarking-HOWTO | Linux 的基准测试问题 |

| Beowulf-HOWTO | 使用 Linux 构建 Beowulf 超级计算机 |

| BootPrompt-HOWTO | 使用启动提示符传递内核消息 |

| Bootdisk-HOWTO | 制作 Linux 和根磁盘 |

| Busmouse-HOWTO | 在 Linux 下使用总线鼠标 |

| CD-Writing-HOWTO | 在 Linux 下写入 CD-ROM |

| CDROM-HOWTO | 配置和使用 CD-ROM 驱动器 |

| Chinese-HOWTO | 为 Linux 配置中文环境 |

| Commercial-HOWTO | Linux 商业软件 |

| Config-HOWTO | 如何精调你的 Linux 系统 |

| Consultants-HOWTO | Linux 商业咨询公司 |

| Cyrillic-HOWTO | 在 Linux 下使用俄语 |

| DNS-HOWTO | DNS 的设置与管理 |

| DOS-Win-to-Linux-HOWTO | 为新接触 Linux 的 DOS/Win9x 用户的信息 |

| DOS-to-Linux-HOWTO | 为新接触 Linux 的 DOS 用户的信息 |

| DOSEMU-HOWTO | 使用 dosemu DOS 仿真器 |

| Danish-HOWTO | 在 Linux 下使用丹麦语 |

| Diskless-HOWTO | 建立无盘 Linux 节点 |

| Distribution-HOWTO | 选择 Linux 发行版 |

### SuSE Linux HOWTO 参考

| HOWTO 文件名 | 说明 |

| --- | --- |

| ELF-HOWTO | 迁移到 ELF 二进制格式 |

| Emacspeak-HOWTO | 在 Linux 下使用语音输出 |

| Esperanto-HOWTO | 在 Linux 下使用世界语 |

| Ethernet-HOWTO | 如何在 Linux 下使用以太网 |

| Finnish-HOWTO | 如何在 Linux 下使用芬兰语 |

| Firewall-HOWTO | 在 Linux 下设置过滤和代理防火墙 |

| French-HOWTO | 在 Linux 下使用法语 |

| Ftape-HOWTO | 在 Linux 下使用软带驱动 |

| GCC-HOWTO | 使用 GNU C 编译器系统 |

| German-HOWTO | 在 Linux 下使用德语 |

| Glibc2-HOWTO | 安装和使用 libc6 GNU C 库 |
