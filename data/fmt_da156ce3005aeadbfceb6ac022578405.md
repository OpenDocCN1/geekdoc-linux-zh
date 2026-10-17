
- 2. 编写一个 shell 脚本，查询整个系统中所有设置了粘滞位（sticky bit）的目录。限制查询不搜索 `/opt` 和 `/proc`。

- 3. 编写一个 shell 脚本，在系统中搜索过去 30 天内创建的、 world 可写的所有普通文件。

- 4. 编写一个 shell 脚本，在系统中搜索过去 10 分钟内修改过的所有目录。

- 5. 编写一个 shell 脚本，在系统中搜索在 5 到 10 分钟前被访问的所有普通文件。

# 第 27 章

使用 `rsync` 配合 `Dirvish` 创建快照类型备份

六个月前，我听说过 `Dirvish`，当时我使用 `rsync` 不足 10 次。现在，当我需要在本地或通过网络复制文件时，我喜欢使用 `rsync`，因为它具有压缩能力，并且在初始复制之后，它能够复制文件的变化而不是整个文件。通常，当一个文件被修改时，只有文件的一小部分发生了变化，仅发送更新将极大地减少网络传输的数据量。我们能够通过硬链接和索引节点（inodes）实现这一目标。继续读；这对任何机构来说都是非常有用的章节，而且是免费的

`Dirvish` 是一个备份程序，最初由 J.W. Schultz 编写，你可以从 www.dirvish.org 下载。`Dirvish` 使用 `rsync` 在网络上传输文件，它利用 `rsync` 协议允许我们只传输更改的文件增量备份，而不是整个磁带，我们在第 7 章学习过“使用 `rsync` 高效复制数据（Efficiently Replicate Data）”。

`Dirvish` 备份程序使用一个或多个备份服务器存储在磁盘上的镜像数据。理想情况下，该备份服务器应该位于异地，并按月进行备份。

在本章中，我想实现两个目标：

- 熟悉 `Dirvish` 的细节以及它是如何工作的。
- 编写一个脚本来完成我们需要的所有工作。这是一个菜单驱动的用户界面，允许我们与 `Dirvish` 交互以配置新服务器、删除备份、恢复文件。

# Dirvish 如何工作？

`Dirvish` 是一个备份程序，通过利用 `rsync` 协议在磁盘上产生快照式备份。传统上，备份一直存储在磁带上，最近是 CD-ROM 和 DVD 。`Dirvish` 的不同之处在于它在备份服务器上存储镜像。典型的备份包括周期性的全系统备份，随后是自上次以来更改文件的增量备份。此过程持续到下一次全备份，然后循环。当我们需要恢复时，我们在我们需要的地方复制文件。我们将编写一个脚本来处理这些细节。

# 我需要多少磁盘存储？

那么，“增量”是如何工作的？我们需要多少磁盘空间？为了理解 `Dirvish` 的核心，我们需要深入文件系统层面并理解索引节点（inode）的概念。文件系统中的每个单独文件和目录都有一个关联编号，称为 inode。操作系统通过 inode 引用系统文件。正如我们所知，目录是 UNIX 中的特殊文件。目录是一个包含映射到其中存储文件的 inode 列表。因此，通过任何指针，你都可以有一个多个指向同一个 inode 的目录。使用这种技术，`Dirvish` 能够通过指向同一个 inode 来表示多个文件，就像我们创建软链接和硬链接指向文件或目录一样。这本质上就是硬链接！因此，`Dirvish` 的磁盘空间需求将比你最初认为的少得多。取决于你备份的数据以及数据过期前的保留时间，你可以从源数据的 1 到 3 倍开始。这只是一个估计值。理想情况下，我们在执行新备份之前过期旧备份以节省空间。应该在 `Dirvish` 备份服务器上创建独立的文件系统来存储备份镜像数据。

# 配置 Dirvish

有一份关于使用 `Dirvish` 的优秀指南，《配置和使用 Dirvish 进行快照备份》，由 Jason Boxman 编写，位于：http://edseek.com/~jasonb/articles/dirvish_backup/index.html。你应该参考这份学习指南以获取更高级的

# 第 27 章 使用 rsync 与 Dirvish 创建快照类型备份

关于 `Dirvish` 的详细信息。我参考了此文档来编写本节，因为这是我找到的最好的文档。你可以在 http://www.dirvish.org/wiki?VaultBranch（这里的 V 和 B 如此处所示大写）找到关于 `Dirvish` 的另一个优质信息源，当然，还有 `Dirvish` 官方网站 http://www.dirvish.org。在本章的学习过程中，我还会指出你可以查看的帮助页以获取更多细节。

我们需要从 `dirvish lungo` 开始。`Dirvish` 使用了大型银行机构的类比。我们使用“银行”（bank）、分支”（branch）和“金库”（vault）等术语来描述存储备份镜像的位置。为 `Dirvish` 备份镜像创建一个独立的文件系统是一个好主意，例如 `/prod_backups` 或 `/backup_bank1`。“银行”是一个目录（例如 `/backup_bank`），其中包含多个“金库”（指定要备份名称的子目录，且仅指定顶层目录）。不要在银行目录中存储任何其他内容。银行在主配置文件 (`master.conf`) 中定义，允许我们在需要时配置多个银行。“金库”是存储特定文件系统备份镜像的地方。对于我们用 `Dirvish` 备份的每个文件系统都有一个金库。使用 `Dirvish` 的最佳方法是将根目录 (`/`) 指定为创建的备份树，并创建一个要排除在备份之外子目录和文件列表。“镜像”是备份操作产生的整个目录树结构。我们还有“分支”的概念。“分支”是通过共享同一个金库来归档多个具有非常相似数据的客户端的方法。例如，如果 yogi 和 boob 服务器包含几乎相同的数据，那么当我们执行备份时，共享金库中会创建两个目录树结构，分别对应文件和日期 `yogi-YMMDDHMMSS` 和 `boob-YMMDDHMMSS`。

## 安装 Dirvish

在我的 Linux 上，我使用 `yum` 安装了 `Dirvish`，尽管 `apt` 也可以。使用 `yum` 会处理 `Dirvish` 依赖的安装。有关设置 `yum` 或 `apt` 的详情，请参考相应的帮助页，`man yum` 和 `man apt`。`Dirvish` 需要两个 Perl 模块：`Time::ParseDate` 和 `Time::Period`。使用 `yum` 安装 `Dirvish` 是简单的方法，如列表 27-1 所示。

```
[root@booboo scripts#] yum install dirvish
Loading "installnononly" plugin
Setting up Install arguments
Parsing package install arguments
updates 100% ======================== 1.9 KB 00:00
primary.sqlite.bz2 100% ======================== 1.5 MB 00:02
freshrpm 100% ======================== 00:00
primary.sqlite.bz2 100% ======================== 89 KB 00:00
fedora 100% ======================== 2.1 KB 00:00
primary.sqlite.bz2 100% ======================== 4.7 MB 00:05
Resolving Dependencies
--> Running transaction check
--> Package dirvish.noarch 0:1.2.1-2.fc6 set to be updated
```

列表 27-1 在 Linux 上使用 `yum` 安装 `Dirvish`
