
这里，可选的 `m` 请求使用 VESA 协调视频计时（Co-CVT），这是一种根据分辨率、刷新率、显示器类型（CRT 或数字显示器）和隔行来确定适当计时的系统方法。可选的 `r` 指定数字显示的消隐。可选的 `i` 指定隔行模式，可选的 `m` 请求在计时计算中增加 1.8% 的裕量。

除了此处列出的通用语法外，特定驱动程序可能支持其他选项，例如禁用加速。驱动程序之间的共同性很小；你可能需要咨询驱动程序的源码来查找这些选项。

## 验证你的帧缓冲区驱动程序设置

如果你成功加载了帧缓冲区驱动并让 `fbset -i` 命令报告了关于其配置的信息，你可以查看帧缓冲区的几何结构、计时和其他参数。

要查看已加载帧缓冲区驱动的配置数据，请尝试使用 `cat` 查看 `/proc/fb` 的内容以及 `/sys/class/graphics/fb0` 中的文件。并不是所有驱动程序都使用 `/sys` 目录，但当它们使用时，文件提供了访问帧缓冲区参数（如 `bits_per_pixel` 和 `color_map`）的方便方法。

有关关于 Linux 帧缓冲区的更多信息，请参见 http://ldp.org/HOWTO/Framebuffer-HOWTO.html 的（有些过时的）HOWTO。VBE 3.0 规范可以在 http://www.vesa.org/public/VBE/vbe3.pdf 获取。

## DB-TO-FILE 工具

![](img/a28f80056348678270f2ea0cfefd7891_354_0.png)

本附录描述了 `tbl2filed`，这是一个允许你使用 SQL 读取和写入 Linux 配置文件中的值的守护进程，就像这些值存储在数据库而不是文件中一样。如果你想为新的守护进程使用 RTA，并希望在读取和写入传统的、非 RTA 配置文件时保持相同的数据库比喻，那么这个实用程序就会非常方便。本附录讨论的话题包括：

- 概述
- 表定义
- 使用方法和 API
- 安全注意事项

## 概述

`tbl2filed` 守护进程的目标是允许你的 UI 程序使用 PostgreSQL 库来读取或写入（SELECT 或 UPDATE）RTA 表，并在 SELECT 或 UPDATE 的过程中扫描或修改底层的系统配置文件。该实用程序尝试模拟以下常见任务：

- 查看配置文件中的值（SELECT value ...）
- 编辑配置文件中的值（UPDATE value ...）
- 将文件原子地写入磁盘（`UPDATE tbl2filed SET do_commit...`）
- 在需要时重启服务（`UPDATE tbl2filed SET do_script...`）

`tbl2filed` 守护进程允许你通过两个 RTA 表使用 PostgreSQL 命令来读取和写入配置文件。第一张表 `tbl2filed` 描述由守护进程管理的文件，第二张表 `tbl2field` 描述受管理的字段。

图 D-1 展示了该实用程序如何将两个表映射到磁盘文件内部文本字段。

![](img/a28f80056348678270f2ea0cfefd7891_355_0.png)
图 D-1：使用 SQL 访问文件中的数据。

该守护进程还允许我们将所有系统服务的重启脚本放在一个文件中，并使用单一方法（写回调）来调用它们。这种方法可能有助于安全性，因为它允许非特权 UI 程序安全地更改系统配置。

## 表定义

本附录后文将给出示例，但为了理解其含义，你需要对 `tbl2filed` 表的内容有一定的了解。Laddie 使用 `tbl2filed` 来帮助网络配置，你可能会发现在运行的系统中查看这些表会更容易一些。启动 Laddie CD 并按照 `rta_apps.html` 中的 `tbl2filed` 链接。

### tbl2file 表

表信息 `tbl2file` 具有以下列：

```
name               // 文件名
path               // 文件的完整路径
do_commit          // 将值刷新到文件 0->1
timestamp          // 上次读取时间
do_script          // 脚本 0->1
script_parms       // 传递给脚本的参数
```

文件名是 UI 看到的名称。这也被用作进入 `tbl2field` 的索引，即该文件的助记符。路径是文件的完整路径，包括文件名。

`do_commit` 将值刷新到文件 0->1。`timestamp` 是上次读取时间。`do_script` 运行脚本 0->1。`script_parms` 是传递给脚本的参数。

`tbl2file` 表具有以下列：

`do_commit` 将值刷新到文件 0->1。`timestamp` 是上次读取时间。`do_script` 运行脚本 0->1。`script_parms` 是传递给脚本的参数。

文件名是 UI 看到的名称。这也被用作进入 `tbl2field` 的索引，即该文件的助记符。路径是文件的完整路径，包括文件名。

`do_commit` 将值刷新到文件 0->1。`timestamp` 是上次读取时间。`do_script` 运行脚本 0->1。`script_parms` 是传递给脚本的参数。

### tblfield 表

`tblfield` 表持有各个字段的值，具有以下列：

```
name      // 文件名，例如 "resolv"
field     // 字段名，例如 "search_domain"
pattern   // 提取值的正则表达式
regerr    // 如果模式字符串有错误则非零
skip      // 跳过这些模式
format    // 替换行的 printf 格式
value     // 字段的当前值
```

`name` 是文件名，必须匹配 `tbl2file` 表中的 `name` 列。`field` 是 UI 看到的字段名。这始终用于 `WHERE` 子句以识别要读取和更新的字段。`pattern` 是一个正则表达式，与 `skip` 结合识别文件中的字段。模式应包含一组括号以提取值。例如，为了从 `resolv.conf` 文件获取第一个 DNS 服务器，我们可以使用以下正则表达式：

```
^nameserver[\t]+([0-9]+)
```
