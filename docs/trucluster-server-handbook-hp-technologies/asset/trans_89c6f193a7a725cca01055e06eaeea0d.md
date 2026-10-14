
自顶向下命令（表 14-1）旨在消除使用 LSM 时的许多复杂性。借助一条命令（volassist），您可以创建由两个条带化 plex 组成的卷。

随着您对 LSM 越来越熟悉，您可能会发现自顶向下命令有些

## LSM 自顶向下命令

| 命令 | 位置 | 手册 | 类型 | 描述 |
|---|---|---|---|---|
| volassist | /sbin | 8 | binary | 用于创建、镜像、备份、扩展、收缩和移动 LSM 卷的程序。 |
| voldiskadd | /usr/sbin | 8 | sh | 添加一个或多个磁盘供 LSM 使用。 |
| voldisksetup | /usr/sbin | 8 | sh | 设置一个磁盘供 LSM 使用。 |
| volevac | /usr/sbin | 8 | sh | 从磁盘中迁移出所有卷。 |
| volmirror | /usr/sbin | 8 | sh | 在磁盘上镜像卷或控制默认镜像。 |

## 表 14-1：LSM 自顶向下命令

## LSM 自底向上命令

| 命令 | 位置 | 手册 | 类型 | 描述 |
|---|---|---|---|---|
| voldg | /sbin | 8 | binary | 管理 LSM 磁盘组。 |
| voldisk | /sbin | 8 | binary | 创建并管理 LSM 磁盘。 |
| voledit | /sbin | 8 | binary | 创建、删除和修改 LSM 记录。 |
| volmake | /sbin | 4/8 | binary | 创建 LSM 对象。这是一个高级命令，可用于快速创建许多 LSM 对象。它运行时看起来像自顶向下命令，但准备过程绝对是更自底向上的方式。非常强大。 |
| volmend | /usr/sbin | 8 | binary | 修复（修补）LSM 配置记录中的简单问题。 |
| volplex | /sbin | 8 | binary | 管理 LSM plex。 |
| volsd | /sbin | 8 | binary | 管理 LSM 子磁盘。 |
| volume | /sbin | 8 | binary | 管理 LSM 卷。 |

## 表 14-2：LSM 自底向上命令

限制性（或者对于需要完成的特定操作而言可能过于宽泛）。自底向上命令（表 14-2）允许更细粒度的控制。

例如，如果使用一条自顶向下命令即可创建镜像条带化卷，那么使用自底向上命令完成同一目标需要多少条命令？答案是八条。

- volmake(8) volmake sd - 创建一个子磁盘（4）
- volmake plex - 创建一个条带化 plex（2）
- volmake vol - 创建一个卷（1）
- volume(8) volume start - 初始化并启动卷（1）

通常，您可以使用自顶向下命令向 LSM 添加磁盘并添加新卷，并使用自底向上命令管理 LSM 对象。GUI 和基于菜单的程序见表 14-3。

除了创建和操作 LSM 对象之外，还有可用于显示 LSM 配置信息和统计信息的命令（表 14-4）、管理命令和

## LSM GUI 和基于菜单的程序

| 命令 | 位置 | 手册 | 类型 | 描述 |
|---|---|---|---|---|
| dxlsm | /usr/bin/X11 | 8X | binary | 已被 lamsa 命令取代。 |
| lamsa | /usr/bin | 8 | ksh | 此脚本启动基于 Java 的存储管理员程序。 |
| lamsad | /usr/sbin | 8 | ksh | 此脚本启动基于 Java 的存储管理员守护进程。 |
| voldiskadm | /usr/sbin | 8 | sh | 用于管理 LSM 磁盘的菜单驱动界面。 |

## 表 14-3：LSM GUI 和基于菜单的程序

## LSM 信息命令

| 命令 | 位置 | 手册 | 类型 | 描述 |
|---|---|---|---|---|
| volinfo | /usr/sbin | 8 | binary | 打印卷的可访问性和可用性。 |
| volnotify | /usr/sbin | 8 | binary | 显示 LSM 配置事件。 |
| volprint | /sbin | 8 | binary | 显示 LSM 配置。 |
| volstat | /usr/sbin | 8 | binary | 显示 LSM 统计信息。 |

## 表 14-4：LSM 信息命令

守护进程（表 14-5），以及有助于将数据移入和移出 LSM 的命令（表 14-6）。

### 14.6 导入磁盘组

在涉及集群的情况下导入磁盘组与处理独立系统不同。

在集群中导入磁盘组时，需要考虑几种场景：

- 从独立系统将磁盘组导入到集群。
- 从集群将磁盘组导入到独立系统。
- 从集群将磁盘组导入到另一个集群。

| 命令 | 位置 | 手册 | 类型 | 描述 |
|---|---|---|---|---|
| lsmbstartup | /sbin | 8 | sh | 系统启动时启动 LSM 的脚本。 |
| lsmsetup | /usr/sbin | 8 | symlink | 指向 volsetup 命令的符号链接。 |
| vold | /sbin | 8 | binary | LSM 卷配置守护进程。 |
| voldctl | /sbin | 8 | binary | 控制 LSM 卷配置守护进程（vold）。 |
| volinstall | /usr/sbin | 8 | sh | 在 LSM 安装后设置 LSM。创建 LSM 设备特殊文件等。 |
| voliod | /sbin | 8 | binary | 启动、停止并报告 LSM 内核 I/O 守护进程。 |
| volrecover | /sbin | 8 | binary | 执行卷恢复操作。 |
| volrestore | /usr/sbin | 8 | sh | 从 volsave 命令保存的信息中恢复完整或部分 LSM 配置。 |
| volrootmir | /usr/sbin | 8 | sh | 创建在新磁盘上启动所需区域的镜像。集群中不支持！ |
| volsave | /usr/sbin | 8 | sh | 保存 LSM 配置。 |
| volsetup | /usr/sbin | 8 | sh | 通过创建 rootdg 磁盘组来初始化 LSM。 |
| voltrace | /usr/sbin | 8 | binary | 跟踪卷上的操作。 |
| volunroot | /usr/sbin | 8 | sh | 在独立系统上从 LSM 中删除 root 和 swap。集群中不支持！ |
| volwatch | /usr/sbin | 8 | sh | 监视 LSM 的故障事件并执行热备用。 |

表 14-5：LSM 管理命令与守护进程
