

## 13.4 章节总结

在本章中，我们研究了 Linux 性能工具集存在不足的几个领域，并提出了一些理想的解决方案。我们还讨论了为什么 Linux 是进行性能调查和优化的良好平台。

改进 Linux 性能取决于你，这位读者。Linux 性能和 Linux 性能工具的改进机会随处不在。如果你发现了一个困扰你的性能问题，请修复它，或者将其报告给开发者并与他们合作修复。无论哪种方式，都不会再受到该问题的影响，整个 Linux 社区都从中受益。

## 附录 A 性能位置

书中描述的性能工具源自互联网的许多地方。幸运的是，大多数分发版已经将它们整合在一起并包含在当前的发行版版本中。表 1 描述了所有工具，提供了它们原始位置的链接，并指示了它们是否包含在以下发行版中：Fedora Core 2 (FC2)、Red Hat Enterprise Linux (EL3) 和 SUSE 9 (S9)。

### 表 A-1 性能工具的位置

| 工具 | 发行版 | 源位置 |
| :--- | :--- | :--- |
| bash | FC2, EL3, S9 | http://www.kernel.org/~bash/bash.html |
| etherape | 无 | http://sourceforge.net/etherape/ |
| tool | FC2, EL3, S9 | http://sourceforge.net/projects/kernel/ |
| proc | FC2, EL3, S9 | http://sourceforge.net/procps/ |
| gcc | FC2, EL3, S9 | http://gnu.org/ |
| gdb | FC2, EL3, S9 | http://sources.redhat.com/gdb/ |
| gkrellm | FC2, EL3, S9 | http://sourceforge.net/~gkrellm/gkrellm |
| gnome-system-monitor | FC2, EL3, S9 | ftp://ftp.gnome.org/pub/sources/gnome-system-monitor/ |
| gnumeric | FC2, EL3, S9 | http://www.gnome.org/projects/gnumeric/ |
| gprof | FC2, EL3, S9 | http://sources.redhat.com/binutils |
| ifconfig | FC2, EL3, S9 | http://www.debian.org.uk/net-tools/ |
| iostat | FC2, EL3, S9 | http://www.debian.fr/sysstat/ |

## 附录 B 安装 profile

系统性能分析器 profile 是一项强大的性能工具，其安装/使用可能会很复杂。本附录描述了在 Fedora Core 2 (FC2)、Red Hat Enterprise Linux (EL3) 和 SUSE 9 (S9) 上安装 profile 时遇到的一些问题。

### B.1 Fedora Core 2 (FC)

对于 FC2，Red Hat 提供了 profile 的软件包，应该使用这些包而不是 profile 网站上的。单处理器内核不提供必要的 profile 驱动程序。Red Hat 将必要的内核模块与 SMP 版本的内核一起打包。如果你想运行 profile，即使你是在单处理器机器上运行，也必须使用 SMP 内核。

### B.2 Enterprise Linux 3 (EL3)

对于 EL3，Red Hat 再次提供了 profile 的软件包，应该使用这些包而不是 profile 网站上的。单处理器内核不提供必要的 profile 驱动程序。Red Hat 在 SMP 或大内存版本的内核中包含了必要的内核模块。如果你想运行 profile，即使你是在单处理器机器上运行，也必须使用 SMP 或大内存内核。在 EL3 中使用 profile 的更多信息请参阅 http://www.redhat.com/docs/manuals/enterprise/RHEL-3-Manual/sysadmin-guide/profile.html。

### B.3 SUSE 9.1

对于 SUSE 9.1，SUSE 提供了 profile 的软件包，应该使用这些包而不是 profile 网站上的。所有版本的 SUSE 内核（默认、SMP 和 bigSMP）都支持 profile，因此所提供的任何内核都可以工作。

## 索引

- [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [R] [S] [T] [U] [V] [W] [X]
- % time 选项
- trace 工具
- strace 工具
- %MEM 选项, top (v.2.x 和 3.x) 工具
- %memused 选项
- sar (II) 工具
- %swpused 选项
- sar (II) 工具
- +D 目录选项
- lsof (列出打开的文件) 工具，磁盘/O 子系统使用
- +d 目录选项
- lsof (列出打开的文件) 工具，磁盘/O 子系统使用
- --annotated-source 选项, gprof 命令
- --assembly 选项, profile 工具
- --brief 选项, gprof 命令
- --delay 选项, slabtop 工具
- --details 选项
- --flat-profile 选项, profile 工具, gprof 命令
- --follow-exec 选项, memprof 工具，应用程序内存使用
- --follow-fork 选项, memprof 工具，应用程序内存使用
- --graph 选项, gprof 命令
- --help 选项, kachegrind 工具，应用程序内存使用
- trace 工具, strace 工具
- --interfaces=name 选项, netstat 工具，网络 I/O
- --long-filenames 选项, profile 工具
- --raw-i -w 选项, netstat 工具，网络 I/O
- --sort 选项, slabtop 工具
- --source -- 选项, profile 工具
- --statistics-c 选项, netstat 工具，网络 I/O
- --symbol 选项, profile 工具
- --tcp-t 选项, netstat 工具，网络 I/O
- --trace-jump=yes/no 选项, kachegrind 工具，应用程序内存使用
- --udpi-u 选项, netstat 工具，网络 I/O
- -/+ buffers/cache 选项, free 工具
- -A 选项, gprof 命令
- -a 选项, profile 工具 第2次
- -o 选项
- [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [R] [S] [T] [U] [V] [W] [X]
- %A
- slabtop 工具
- memused, 第2次
- [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [R] [S] [T] [U] [V] [W] [X]
- %time
- top (v.2.x 和 3.x) 工具
- memused, 第2次
- 2, 3, 4, 5, 6, 7, 8, 9
- 性能工具, 第2次
- 用法 (usage)
- 性能调查
- 优化
- 性能工具, 第2次, 3次, 4次, 5次, 6次, 7次, 8次, 9次, 10次, 11次, 12次
- 性能工具, 第2次
- 性能工具, 第2次
- 统计 (statistics)
- 性能工具, 第2次--
- 性能工具, 第2次
- 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12
- 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12
- 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12
- 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12
- 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12
- 2, 3, 4, 5, 6, 7
- 2次, 3次, 4次, 5次, 6次, 7次, 8次, 9次, 10次, 11次, 12次
- 2次, 3次, 4次, 5次, 6次, 7次, 8次, 9次
- 2次, 3次, 4次, 5次, 6次, 7次, 8次, 9次
... (此处省略重复数字索引，与原文逻辑保持一致)

