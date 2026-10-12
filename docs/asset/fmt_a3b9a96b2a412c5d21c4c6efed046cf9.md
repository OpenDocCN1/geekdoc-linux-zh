
# Linux & 开源指南

## 05 块级条带化

两个大阵列是`RAID 5`和`RAID 6`，它们使用条带化在硬盘之间创建校验位，允许你使用比可用更多的空间。如果你没有安装所需的模块（使用 `sudo apt install mdadm`），你无法安装。

## 06 其他 RAID

`RAID 5`至少需要三块硬盘，`RAID 5`的每组硬盘中有一个空闲硬盘，允许在其中一个硬盘丢失时恢复数据。你可以使用`mdadm`创建软件`RAID`，也可以管理它们并进行更高级的任务。

`RAID 6`至少需要四块硬盘，校验位分布在两块硬盘上。为了增加安全性，你可以在丢失两块硬盘的情况下获得`RAID 5`。在额外的存储空间上，速度不会增加。

它们的组合是最常见且实用的。`RAID 5`具有极好的传输率，但无法同时处理两块硬盘的故障。还有用于视频编辑和文件读取的阵列。你可以像`RAID 0`或`RAID 5`那样使用更多组合来创建更多空间，同时在每个阵列上仍有校验位。

还有其他阵列，当你使用单块硬盘时可以使用。`RAID`级别取决于你的主板或`RAID`卡。并不是所有的`RAID`卡都有Linux驱动程序，所以你需要确保获得正确的卡。

要设置`RAID 5`，你首先需要确保所有的硬盘都已安装到系统中。在这个示例中，我们假设你有不同的硬盘，但可以使用类似的设置来创建`RAID 5`。

磁盘 0 磁盘 1 磁盘 2 磁盘 4

Linux 在内核级别支持设置软件`RAID`，并可以在系统设计上提供更大的灵活性，因为它支持我们讨论过的所有`RAID`类型，且不需要额外空间。通常，这种设置可以使用四块硬盘获得，并在桌面机上。你需要通过检查内核中是否有正确的模块来准备添加`RAID`：

| 分区 | 文件系统 | 标签 | 已用 | 标记 |
|---|---|---|---|---|
| `/dev/sdb1` | 未知 | 微软预留分区 | 128.00 MB | `mftres` |
| `/dev/sdb2` | `ext4` | | 465.64 GB | |

格式：在安装之前将 `/dev/sdb2` 格式化为 `ext4`。进入 Linux 并打开终端开始。首先，我们需要搞清楚硬盘在系统中称为什么，所以使用 `fdisk` 获取列表（`/dev/sdb`、`/dev/sdc` 等）。记录它们，我们可以设置 `RAID`。

Linux 在内核级别支持软件 `RAID`，无论你使用命令行还是 GUI 工具，都可以提供更大的灵活性——由于内核在处理 `RAID` 通信，你不需要担心删除任何信息。如果 `RAID` 在启动时挂载，那么你的 `RAID` 就完成了。值得深入研究 `RAID` 主页，学习未来如何管理你的 `RAID` 并保持其状态。

> `RAID 0:`
> ```
> # mdadm --create --verbose /dev/md0 --nlevel=stripe
> # mdadm --devices=2 /dev/sdb1 /dev/sdc1
> ```

> `RAID 1:`
> ```
> # mdadm --create --verbose /dev/md0 --nlevel=mirror
> # mdadm --devices=2 /dev/sdb1 /dev/sdc1
> ```

> `RAID 6:`
> ```
> # mdadm --create --verbose /dev/md0 --nlevel=6
> # mdadm --devices=3 /dev/sdb /dev/sdc1 /dev/sdd1
> ```

> `RAID 10:`
> ```
> # mdadm --create --verbose /dev/md0 --nlevel=10
> # mdadm --devices=4 /dev/sdb1 /dev/sdc1 /dev/sdd1
> ```

## 07 RAID

### 5 保存并格式化
一旦你创建了阵列（或阵列），就可以保存它。你可以在 Ubuntu 服务器上执行：

`JBOD`

`RAID` 的简单版本是 `JBOD`，或者称为一组硬盘。它通过连接硬盘来增加硬盘的存储容量。如果一个硬盘死亡，你将只会丢失跨在它们上的文件，但在没有替换的情况下它仍然工作。

```
# mdadm --create --verbose /dev/md0 --nlevel=5

# mdadm --devices=3 /dev/sdb1 /dev/sdc1 /dev/sdd1
```

或者对大多数其他的使用：

```
# mdadm --detail --scan -- /etc/mdadm/mdadm.conf
```

运行 `/proc/mdstat` 查看文件中列出了哪些阵列，它应该包含你刚刚设置的那个。如果不是，你只需要

## 开发者指南

无论你在何处部署应用，`Capistrano` 都能轻松地将 `Rails`（以及其他平台）部署到 `*nix` 服务器上。

由于其模块化的结构，在生产环境之后添加带有 `qa.rb` 的 QA 阶段等更改既可行又简单。

`Capistrano 3` 基于 `Ruby` 构建，最初为 `Rails` 设计，现在也是部署其他 Web 平台的理想选择。

`Capistrano` 的灵活性和强大功能意味着大量的配置，但操作起来相对直观。

### 使用 Capistrano 持续部署应用

告别痛苦地将你的 Web 应用开发版本从阶段环境移动到数据库和 Web 服务器上的测试环境。

#### 顾问

Richard Smedley
一位 Unix 全能型人才，Richard 描述了一个在任何语言上都花时间直到变得真正精通的人，但他总是开着 shell 以便通过远程进行学习。

#### 资源

- `Ruby = 1.9` (使用 `RBENV` 让这一切变得简单)

```
git www-capistrano.com
```

```
Capistrano 3 www.capistrano.com
```

`Capistrano` 自动将 Web 应用部署到你的服务器，处理诸如在任何你有 `SSH` 权限的服务器上运行远程命令等任务。`Capistrano` 的主脚本是 `deploy`：部署诸如 `rollback` 等任务，这些任务由命令组成。`Capistrano` 需要应用服务器、Web 服务器和 `db` - 数据库服务器。通过这个（可扩展的框架），很容易为你的插件和服务器集合调整 `Capistrano` 的配置。基础设置非常简单，`Capistrano 3` 是一个灵活的框架，如果你想开始充分利用它的功能，你需要远超这些简单的操作。我们需要较新版本的 `Ruby`、`Git`（加上 `GitHub` 账号）以及你正在运行的 `Rails` 项目。此外，如果使用 `Rails` 和 `capistrano-deploy` 工作，请确保 `Capistrano` 为部署连接了正确的 `Ruby` 版本。无论你运行 `Passenger`、`Unicorn` 还是 `Puma` 作为服务器，都没有关系，但请注意，插件可以帮助处理所有服务器的额外任务。可以在 `rubygems.org` 上搜索选择。

10 Linux & 开源通用指南

## Linux & 开源天才指南

文件 编辑 视图 书签 设置 帮助

```
File /home/user/.vimrc

set number
```
