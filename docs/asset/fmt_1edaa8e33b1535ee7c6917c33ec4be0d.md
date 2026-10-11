
### 7. 当 CD 刻录完成后，弹出它（或自动弹出）并对其进行适当标记（如发行版名称、版本号和日期）。

> 您的 Fedora 系统可能没有安装 `K3b`，可以通过终端窗口以 root 用户身份运行 `yum install k3b` 来安装。

## 图 A-1

使用 `K3b` 刻录你的安装光。

![](img/d7f79c91d15076e71790c1b4e1d072d0_855_0.png)

现在你已经准备好开始安装（或启动）你刚刚刻录的 Linux 发行版了。有关安装 Linux 的通用信息，请参阅第 7 章。然后查看介绍你特定发行版的章节，以查找其特定的安装程序。

如果你目前没有安装 Linux 或没有可用 `K3b`，可以使用你拥有的任何 CD 刻录应用程序来刻录 CD。Gentoo Web (`www.gentoo.org/doc/faq.xml`) 提供了关于 CD 安装工具以及如何使用它们刻录 CD 的简要概述。它描述了在 Windows、Mac OS 和 Linux 上可用的磁盘刻录工具。

如果你没有图形界面（`GUI`），或者不是在 shell 环境下操作，可以使用 `cdrecord` 命令来刻录 ISO 文件。在插入空白 CD 且当前目录下有想要刻录的 ISO 镜像的情况下，以下是使用 `cdrecord` 将镜像刻录到 CD 的简单命令行：

```
# cdrecord -v whatever.iso
```
