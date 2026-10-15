
(2/2): nmap-6.40-4.el7.x86_64.rpm

| 3.9 MB 00:00:01

总

3.2 MB/s | 4.1 MB 00:00:01

运行事务检查

运行事务测试

事务测试成功

运行事务

正在安装 : 2:nmap-ncat-6.40-4.el7.x86_64

1/2

```
正在安装 : 2:nmap-6.40-4.el7.x86_64
2/2
正在验证 : 2:nmap-6.40-4.el7.x86_64
1/2
正在验证 : 2:nmap-ncat-6.40-4.el7.x86_64
2/2

已安装：
nmap.x86_64 2:6.40-4.el7

已安装依赖：
nmap-ncat.x86_64 2:6.40-4.el7

完成！
[root@localhost]#
```

在列表 11.6 中，你可以看到 `yum` 首先分析将要安装的内容。一旦明确了这些内容，它会提供将安装的软件包的概述，包括其依赖项。然后，软件包本身会被安装到系统中。

要从机器上删除软件软件包，请使用 `yum remove` 命令。该命令也会进行依赖分析，这意味着它不仅会删除选定的软件包，还会删除所有依赖于它的软件包。这有时会导致出现长长的待删除软件包列表。为了避免不快的意外，你不应该总是配合 `-y` 选项使用 `yum remove`。

> 注意：某些软件包受保护的。因此，你无法轻易删除它们。如果你在删除时遇到受保护的软件包，它将拒绝删除。

# 显示软件包列表

在与 `yum` 工作时，你也可以使用 `yum list` 命令来显示软件包列表。在不带参数的情况下，`yum list` 会显示所有可用软件软件包的列表，包括它们安装自哪个存储库。你可以看到表 11.2 列出的存储库名称以及 `@anaconda` 存储库。如果显示了存储库名称，则该软件包在特定存储库中可用。如果列出了 `@anaconda`，则该软件包已安装在该系统上。列表 11.7 显示了 `yum list` 命令的部分输出。

## 列表 11.7 `yum list` 命令的部分输出

| 已安装软件包 | | |

|---|------|--|

| ... | | | |

| zenity.x86_64 | 3.8.0-4.el7 | @anaconda |

| zip.x86_64 | 3.0-10.el7 | @anaconda |

| zlib.x86_64 | 1.2.7-13.el7 | @anaconda |

| 可用软件包 | | |

| 389-ds-base.x86_64 | 1.3.3.1-16.el7_1 | updates |

| 389-ds-base-devel.x86_64 | 1.3.3.1-16.el7_1 | updates |

| 389-ds-base-libs.x86_64 | 1.3.3.1-16.el7_1 | updates |

| Cython.x86_64 | 0.19-3 | base |

| ElectricFence.1686 | 2.2.2-39.el7 | base |

| ElectricFence.x86_64 | 2.2.2-39.el7 | base |

| GConf21686 | 3.2.6-8.el7 | base |

如果你想查看服务器上安装了哪些软件包，可以使用 `yum installed` 命令。当将 `yum list` 命令与特定软件包名称作为参数使用时，它也可能非常有用。例如，输入 `yum list kernel` 来显示实际安装了哪个版本的内核，以及哪个版本作为存储库中的最新版本可供。列表 11.8 显示了该命令的结果。

## 列表 11.8 使用 yum list 查看已安装和可用版本

```
[root@localhost ~]# yum list kernel
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
* base: centos.mirror.triple-it-nl
* extras: centos.mirror.triple-it-nl
* updates: centos.mirror.triple-it-nl
Installed Packages: kernel.x86_64 3.10.0-123.el7 @anaconda
Available Packages: kernel.x86_64
```

# 更新软件包

使用 `yum` 的主要优势之一是存储库使得更新软件包变得非常简单。存储库的维护者会将更新后的软件包复制到存储库中。存储库中的索引始终包含软件包的当前版本。在本地机器上，也有一个数据库包含了所用软件包的当前版本。

事务摘要

=================

安装 1 个软件包

总下载大小：95 M
