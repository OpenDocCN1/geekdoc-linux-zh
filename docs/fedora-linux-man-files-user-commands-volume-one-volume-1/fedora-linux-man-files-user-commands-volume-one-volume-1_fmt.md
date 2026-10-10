
# Fedora Linux 手册页：用户命令第一卷（卷 1）

![](img/9e4ee58043860d211449562b68ac7238_0_0.png)

用户命令

ab 退出

献辞：

本书献给 Michael Kerrisk 以及 Linux 文档项目团队成员。

编译与编辑：Gareth Morgan Thomas

![](img/9e4ee58043860d211449562b68ac7238_5_0.png)

## 名称

`ab` - Apache HTTP 服务器基准测试工具

### 概要

`ab [ -A auth-username:password ] [ -b windowsize ] [ -B local-address ] [ -c concurrency ] [ -C cookie-name=value ] [ -d csv-file ] [ -f protocol ] [ -g gnuplot-file ] [ -h ] [ -H custom-header ] [ -i ] [ -k ] [ -l ] [ -m HTTP-method ] [ -n requests ] [ -p POST-file ] [ -P proxy-auth-username:password ] [ -q ] [ -r ] [ -s timeout ] [ -S ] [ -t timelimit ] [ -T content-type ] [ -u PUT-file ] [ -v verbosity ] [ -w ] [ -x table-attributes ] [ -X proxy[:port] ] [ -y tr-attributes ] [ -z td-attributes ] [ -Z ciphersuite ] http[s]://hostname[:port]/path`

### 摘要

`ab` 是一个用于您的 Apache 超文本传输协议 (HTTP) 服务器基准测试的工具。它旨在让您了解当前 Apache 安装的性能。这特别展示了您的 Apache 安装每秒能够处理多少请求。

### 选项

- `-A authentication`: 向服务器提供身份验证凭据。用户名和密码由单个 `:` 分隔，并 base64 编码发送。该字符串取决于服务器是否需要（例如发送 401 身份验证）。
- `-b windowsize`: TCP 发送/接收缓冲区的大小，单位为字节。
- `-b local-address`: 发起外部连接时绑定的地址。
- `-c concurrency`: 同时执行的并发请求数。默认是一次一个请求。
- `-C cookie-name=value`: 在请求中添加 `Cookie:` 行。参数通常为名称=值对的形式。此字段可以重复。
- `-d`: 不显示“在 XX [ms] 内服务的百分比表”（旧版支持）。
- `-e csv-file`: 写入逗号分隔 (CSV) 文件，其中包含每个百分比（从 1% 到 100%）处理该百分比请求所需（毫秒）。这通常比 'gnuplot' 文件更有用；因为结果已经过分箱。
- `-f protocol`: 指定 SSL/TLS 协议 (`SSL2`, `SSL3`, `TLS1`, `TLS1.1`, `TLS1.2` 或 `ALL`)。2.4.4 及更高版本支持 `TLS1.1` 和 `TLS1.2`。
- `-g gnuplot-file`: 将所有测量值写入 'gnuplot' 或 TSV（制表符分隔值）文件。该文件可以轻松导入 Gnuplot、IDL、Mathematica、Igor 或 Excel 等软件包。标签位于文件的第一行。
- `-h`: 显示用法信息。
- `-H custom-header`: 为请求添加额外的标头。参数通常为有效的标头行格式，包含冒号分隔的字段值对（例如 "Accept-Encoding: zip/zip;8bit"）。
- `-i`: 使用 HEAD 请求代替 GET 请求。
- `-k`: 启用 HTTP KeepAlive 功能，即在一个 HTTP 会话中执行多次请求。默认禁用 KeepAlive。
- `-l`: 如果响应长度不固定，不报告错误。
- `-m HTTP-method`: HTTP 方法。
- `-n requests`: 请求数。
- `-p POST-file`: 包含数据的文件。
- `-P proxy-auth-username:password`: 提供身份验证凭据。
- `-q`: 禁止输出。
- `-r`: 不显示错误。
- `-s timeout`: 等待时间。
- `-S`: 不显示统计信息。
- `-t timelimit`: 测试的最大时间。
- `-T content-type`: 内容类型。
- `-u PUT-file`: 要上传的文件。
- `-v verbosity`: 详细程度。
- `-w`: 以 HTML 格式显示结果。
- `-x table-attributes`: 表格属性。
- `-X proxy[:port]`: 代理端口。
- `-y tr-attributes`: 传输属性。
- `-z td-attributes`: TD 属性。
- `-Z ciphersuite`: 密码套。

## 输出

以下列表描述了 `ab` 返回的值：

### Server Software: 第一次响应的服务器标头中返回的值（如果有的话）。

### Server Hostname: 命令行中指定的 DNS 或 IP 地址。

## Server Port: `ab` 连接的端口。如果命令行未给出端口，将使用默认值。

## SSL/TLS Protocol: 客户端和服务器之间协商的参数。

## Document Path: 从命令行解析出的请求 URI。

## Document Length: 第一个成功返回的文档的大小（字节）。

## Concurrency Level: 测试期间使用的并发客户端数量。

## Time taken for tests: 从创建第一个套接字到接收最后一个响应的时间。

## Complete requests: 接收到的成功响应数。

## Failed requests: 被视为失败的请求数。

## Write errors: 写入期间的错误数。

## Non-2xx responses: 非 200 系列状态码的响应数。

## Keep-Alive requests: 导致 Keep-Alive 请求的连接数。

## Total body sent: 测试期间发送的总字节数。

## Total transferred: 从服务器接收的总字节数。

通过网络传输的字节数。

## HTML 传输

从服务器接收到的文档总字节数。此数字不包含 HTTP 请求头中接收的字节。

### 每秒请求数

这是每秒请求数。该值是请求数除以总耗时得到的结果。

### 每个请求时间

每个请求消耗的平均时间。第一个值通过公式 `concurrency * timetaken * 1000 / done` 计算，第二个值通过公式 `timetaken * 1000 / done` 计算。

### 传输率

根据公式 `totalread / 1024 / timetaken` 计算的传输率。

## BUG

存在各种固定长度的静态声明缓冲区。结合对命令行参数、服务器响应头以及其他外部输入的惰性解析，这可能会给你带来麻烦。它没有完全实现 HTTP/1.x；仅接受某些“预期”形式的响应。对 `strerror(3)` 的大量使用在性能分析中排列前茅，这可能表明存在性能问题；即，你测量的是 `ab` 的性能而非服务器的性能。

### Abrt-action-analyze-backtrace

## 名称

`abrt-action-analyze-backtrace` - 分析 C/C++ 回溯，生成重复哈希、回溯评分，并识别问题目录 DIR 中的崩溃函数。

### 摘要

`abrt-action-analyze-backtrace [-v] [-d DIR]`

### 描述

该工具从问题目录读取名为 `backtrace` 的文件，生成重复哈希、回溯评分，并识别崩溃函数。然后，它将这些数据作为新元素 `duphash`、`rating` 和 `crash_function` 保存到该问题目录中。

### 与 libreport 事件的集成

`abrt-action-analyze-backtrace` 可可以在回溯生成后作为二级分析器使用。`abrt-action-analyze-backtrace` 生成的数据对于向 bug 数据库报告崩溃有用：`rating` 可以防止报告低质量（无信息）回溯的 bug，`duplication hash` 用于查找已提交的类似崩溃的 bug。

在 `report_event.conf` 中的用法示例：

```
EVENT=analyze analyzer=CCpp abrt-action-generate-backtrace || exit $?
abrt-action-analyze-backtrace
```

### 选项

`-d DIR`

问题目录的路径。

`-v`

更详细输出。可以多次给定。

### 作者

ABRT 团队

### 参见



# abrt-action-generate-backtrace

## Abrt-action-analyze-c

### 名称

`abrt-action-analyze-c` - 为带有核心转储的问题数据目录 `DIR` 计算并保存 `UUID`。

### 摘要

```
abrt-action-analyze-c [-v] [-d DIR]
```

### 描述

该工具从问题数据目录读取名为 `coredump` 的文件，对其进行处理并生成一个通用唯一标识符（`UUID`）。然后，它将此数据作为新元素 `uuid` 保存。

### 与 ABRT 事件的集成

`abrt-action-analyze-c` 可用于生成新保存的转转储的 `UUID`。

```
EVENT=post-create analyzer=CCpp abrt-action-analyze-c
```

### 选项

`-d DIR`

问题目录的路径。未提供此选项时，使用当前工作目录。

`-v`

更详细输出。可以多次给定。

### 作者

`ABRT` 团队

## Abrt-action-analyze-cppp-local

### 名称

`abrt-action-analyze-cpp-local` - 生成回溯并查找重复项

### 摘要

```
abrt-action-analyze-cpp-local [--without-di][--without-bz][--without-bodhi]
```

### 描述

此工具下载 `debuginfo` 并为问题目录中的核心转储生成回溯，同时检查 `bugzilla` 中已有的重复项以及与检测到的崩溃相关的可能的更新。

### 与 ABRT 事件的集成

`abrt-action-analyze-cpp-local` 用于在处理 `C/C++` 崩溃时的 `analyze` 步骤。

```
EVENT=analyze_LocalGDB analyzer=CCpp abrt-action-analyze-cpp-local
```

### 选项

`--without-di`

不安装 `debuginfo` 包

`--without-bz`

不在 `bugzilla` 中搜索已有的重复项

`--without-bodhi`

不在 `bodhi` 中搜索已有的更新

### 作者

`ABRT` 团队

## 名称

`abrt-action-analyze-core` - 从核心转储中提取构建信息

### 摘要

```
abrt-action-analyze-core [-v] [-o OUTFILE] -c COREFILE
```

### 描述

该工具读取核心转储并提取加载模块的构建 `id`，如果未配置 `OUTFILE` 文件，则将列表打印到标准输出。

### 选项

`-c COREFILE`

核心转储的路径。

`-v`

更详细输出。可以多次给定。

`-o OUTFILE`

输出文件

`-h`

打印帮助信息

### 作者

`ABRT` 团队

## Abrt-action-analyze-java

### 名称

`abrt-action-analyze-java` - 计算并保存 `UUID`

### 摘要

```
abrt-action-analyze-java [-v] [-d DIR] [-o FILE]
```

### 描述

该工具从问题数据目录读取名为 `backtrace` 的文件，对其进行处理并生成一个通用唯一标识符（`UUID`）。然后，它将此数据作为新元素 `duphash` 以及其堆栈帧是否有任何一个解释了为什么不应将堆栈跟踪报告到 `bug` 跟踪系统。

### 与 ABRT 事件的集成

`abrt-action-analyze-java` 可用于生成新保存的堆栈跟踪的 `UUID`。

```
EVENT=post-create analyzer=Java abrt-action-analyze-java
```

### 选项

`-d DIR`

问题目录的路径。

`-v`

更详细输出。可以多次给定。

`-f FILE`

堆栈跟踪的路径。

### 作者

`ABRT` 团队

## Abrt-action-analyze-oops

### 名称

`abrt-action-analyze-oops` - 为带有内核 `oops` 的问题目录计算并保存 `UUID`

### 摘要

```
abrt-action-analyze-oops [-v] [-d DIR]
```

### 描述

该工具从问题数据目录读取名为 `backtrace` 的文件，对其进行处理并生成一个通用唯一标识符（`UUID`）。然后，它将这些数据作为新元素 `duphash` 和 `uuid` 保存。

### 与 ABRT 事件的集成

`abrt-action-analyze-oops` 可用于生成新保存的内核 `oops` 的重复哈希。

```
EVENT=post-create analyzer=Kernelops abrt-action-analyze-oops
```

### 选项

`-d DIR`

问题目录的路径。未提供此选项时，使用当前工作目录。

`-v`

更详细输出。可以多次给定。

### 作者

`ABRT` 团队

## Abrt-action-analyze-python

### 名称

`abrt-action-analyze-python` - 为带有 `Python` 崩溃的问题目录计算并保存 `UUID`

### 摘要

```
abrt-action-analyze-python [-v] [-d DIR]
```

### 描述

该工具从问题数据目录读取名为 `backtrace` 的文件，对其进行处理并生成一个通用唯一标识符（`UUID`）。然后，它将这些数据作为新元素 `duphash` 和 `uuid` 保存。

### 与 ABRT 事件的集成

`abrt-action-analyze-python` 可用于生成新保存的 `Python` 崩溃的重复哈希。

```
EVENT=post-create analyzer=Python abrt-action-analyze-python
```

### 选项

`-d DIR`

问题目录的路径。未提供此选项时，使用当前工作目录。

`-v`

更详细输出。可以多次给定。

### 作者

`ABRT` 团队

## Abrt-action-analyze-vmcore

### 名称

`abrt-action-analyze-vmcore` - 从内核转储中提取 `oops` 信息，并在需要时安装内核 `debuginfo`

### 摘要

```
abrt-action-analyze-vmcore [-v] [-d PROBLEM_DIR] [--tmpdir=TMPDIR] [--cache=DIR1[:DIR2]]
```

### 说明

该工具从问题数据目录读取名为 `vmcore` 的文件，处理该文件并提取其中的 `oops` 消息。然后将这些数据保存为新元素 `backtrace`（回溯）。

### 与 ABRT 事件集成

`abrt-action-analyze-vmcore` 可用作转储核心的关键内核崩溃分析器。

在 `report_event.conf` 中的用法示例：

```
EVENT=analyze_VMcore analyzer=vmcore abrt-action-analyze-vmcore
```

### 选项

`-d DIR`

问题目录的路径。如果没有提供此选项，则使用当前工作目录。

`-v`

输出更详细的信息。可以多次指定。

`--core=VMCORE`

要分析的 `vmcore` 路径（默认值：`./vmcore`）

### 作者

`ABRT` 团队

## Abrt-action-analyze-vulnerability

### 名字

`abrt-action-analyze-vulnerability` - 为崩溃的潜在利用性提供评估

### 摘要

```
abrt-action-analyze-vulnerability
```

### 说明

该工具期望当前目录下存在一个名为 `coredump` 的文件，并在该文件上运行 `abrt-gdb-exploitable` `gdb` 插件。漏洞分析的结果将保存在当前目录下的 `exploitable` 文件中。

此工具要求 `PATH` 中同时存在 `gdb` 和 `eu-readelf` 可执行文件。如果缺少任何所需的程序，该工具将以退出代码 `0` 静默退出。

### 作者

`ABRT` 团队

## 名字

`abrt-action-analyze-xorg` -为带有 `Xorg` 回溯的问题数据目录 `DIR` 计算并保存 `UUID` 和重复哈希值

### 摘要

```
abrt-action-analyze-xorg [-v] [-d DIR]
```

### 说明

该工具读取名为 `Xorg.0.log` 的文件，并检查是否加载了任何黑名单中的模块。如果是，则会创建一个带有适当说明文本的 `not-reportable` 文件。如果没有加载黑名单中的模块，该工具将从问题数据记录中读取名为 `backtrace` 的文件，并生成重复哈希值和通用唯一标识符（`UUID`）。然后将这些数据保存为新元素 `duphash` 和 `uuid`。

### 与 ABRT 事件集成

`abrt-action-analyze-xorg` 可用于为新发现的 `Xorg` 回溯生成重复哈希。



```
EVENT=post-create analyzer=Xorg abrt-action-analyze-xorg
```

### 选项

- `-d DIR`

问题目录的路径。如果没有提供此选项，则使用当前工作目录。

- `-v`

输出更详细的信息。可以多次指定。

### 文件

`/etc/abrt/xorg.conf` 加载后应导致 Xorg 崩溃不可报告的模块列表。

### 作者

ABRT 团队

### Abrt-action-find-bodhi-update

## 名字

`abrt-action-find-bodhi-update` - 根据 ABRT 的问题目录查找 bodhi 更新

### 摘要

`abrt-action-notify [-v] [-d PROBLEM_DIR] [-b]`

### 说明

该工具读取问题目录中的 `duphash` 文件，并根据崩溃搜索新的更新。

### 选项

`-v`, `--verbose`

输出详细信息

`-b`, `--without-bodhi`

在不运行 `abrt-bodhi` 的情况下运行。如果存在重复 bug，仅打印 Bugzilla bug id。

`-d`, `--problem-dir PROBLEM_DIR`

问题目录 [默认值：当前目录]

## 环境变量

`Bugzilla_Product`

产品 bug 字段值。如果你需要与 `PROBLEM_DIR/os_info` 中指定的不同的产品，则此项有用。

### 参见

`abrt-bodhi(1)`, `reporter-bugzilla(1)`

### 作者

ABRT 团队

### Abrt-action-generate-backtrace

`abrt-action-generate-backtrace` - 分析 coredump，生成并保存回溯。

### 摘要

`abrt-action-generate-backtrace [-v] [-d DIR] [-i DIR1[:DIR2]...] [-t NUM]`

### 说明

该工具在问题目录 `DIR` 中名为 `coredump` 的文件上运行 `gdb(1)`。`gdb(1)` 会生成关于生成 coredump 刻应用程序状态的回溯（backtrace）和其他诊断信息。然后，该工具将其作为新元素 `backtrace` 保存到该问题目录。

### 与 libreport 事件集成

`abrt-action-generate-backtrace` 可用作转储核心的应用崩溃分析器。

在 `report_event.conf` 中的用法示例：

```
EVENT=analyze analyzer=CCpp abrt-action-generate-backtrace
```

### 选项

`-d DIR`

问题目录的路径。

`-v`

输出更详细的信息。可以多次指定。

`-i DIR1[:DIR2]`

额外的调试目录

`-t NUM`

如果 `gdb` 运行时间超过 `NUM` 则将其杀死。

### 作者

ABRT 团队

## 名字

`abrt-action-generate-core` - 生成核心级回溯

### 摘要

`abrt-action-generate-core [-v] [-r] -d DIR`

### 说明

该工具使用 coredump 和主要在崩溃时可用的二进制文件来生成核心级回溯。然而，它包含了栈上存在的调用指针。结果保存在问题目录中名为 `core_backtrace` 的文件中。

### 与 libreport 事件集成

`abrt-action-generate-core` 可用作转储核心的应用崩溃分析器。

在 `report_event.conf` 中的用法示例：

```
EVENT=analyze analyzer=CCpp abrt-action-generate-core
```

### 选项

`-d DIR`

问题目录的路径。

`-v`

输出更详细的信息。可以多次指定。

`-r`

不进行哈希处理。

### 作者

ABRT 团队

## 名字

`abrt-action-install-debuginfo` - 为 build-ids 安装 debuginfos

### 摘要

`abrt-action-install-debuginfo [-vy] [--ids=BUILD_IDS_FILE] [--tmpdir=TMPDIR] [--cache=CACHEDIR] [--size_mb=SIZE] [-e]`

### 说明

使用 `TMPDIR` 作为临时区域，为 `BUILD_IDS_FILE` 中列出的所有 ids 安装 debuginfos。`CACHEDIR` 中的旧文件将被删除，直到其大小小于 `SIZE`。

### 选项

`-v`

输出更详细的信息。可以多次指定。

`-y`

非交互模式，对所有问题均假设为 Yes。

`--ids`

包含 build ids 的文件路径。默认值：`build_ids`

`--tmpdir`

临时目录的路径。默认值：`/tmp/abrt-RANDOM_SUFFIX`

`--cache`

缓存目录的路径。默认值：`/var/cache/abrt-di`

`--size_mb`

默认值：`4096`

`-e,--exact`

仅下载指定的文件

### 作者

ABRT 团队

### Abrt-action-list-dsos - 打印映射内存区域的 DSO

## 摘要

```
abrt-action-list-dsos [-o OUTFILE] -m PROC_PID_MAP_FILE
```

### 说明

该工具读取包含映射内存区域的文件。输出打印到文件中。

输出格式：

```
%p %n %v %i
```

其中

- `%p` 映射到内存区域的库或二进制文件路径

- `%n` `%p` 所属包的名称、版本、发布版本、架构

- `%v` 包的供应商

- `%i` 安装时间

### 选项

`-o OUTFILE`

输出文件，如果没有指定，则打印到 `stdout`

`-m PROC_PID_MAP_FILE`

包含映射内存区域的文件

### 作者

ABRT 团队

### Abrt-action-notify - 通过所有可访问通道宣布问题的新发生

### 摘要

`abrt-action-notify [-h] -d PROBLEM_DIR [-v] [-a] [-e AUTOREPORTING_EVENT]`

### 说明

当前实现在系统总线的 `/org/freedesktop/problems` 路径下针对 `org.freedesktop.problems` 接口的 Crash 成员发布 D-Bus 信号。

### 与 ABRT 事件集成

`abrt-action-notify` 用于针对所有崩溃类型通知新问题以及单个问题的连续发生。

```
EVENT=notify package!= abrt-action-notify
```

### 参数

`-v`, `—verbose`

输出详细信息

`-d`, `—problem-dir PROBLEM_DIR`

问题目录 [默认：当前目录]

`-h`, `—help`

显示帮助信息

`-a`, `—autoreporting`

强制运行自动报告事件

`-e`, `—autoreporting-event AUTOREPORTING_EVENT`

覆盖自动报告事件名称

## 环境变量

`ABRT_VERBOSE`

ABRT 详细程度级别

### 文件

`/etc/abrt/abrt.conf`

`AutoreportingEnabled`

如果启用，`abrt-action-notify` 将运行 `AutoreportingEvent`

`AutoreportingEvent`

如果启用了自动报告，要运行的事件名称

`abrt.conf(5)`

### 作者

ABRT 团队

## 名称

`abrt-action-perform-ccpp-analysis` - 允许用户选择接受的核心转储（core dump）分析方式

### 摘要

`abrt-action-perform-ccpp-analysis [-h] [-d PROBLEM_DIR]`

### 描述

此工具允许用户在本地和远程转储分析之间进行选择。本地分析可能需要下载大量数据，但它是完全安全的。相反，远程分析只需要将核心转储上传到回溯服务器，但核心转储可能包含安全敏感数据。

### 与 ABRT 事件的集成

`abrt-action-perform-cpppp-analysis` 用于在处理 C/C++ 崩溃时的分析步骤（analyze）

```
EVENT=analyze_CCpp analyzer=CCpp abrt-action-perform-cpppp-analysis
```

### 参数

`-d`, `--problem-dir PROBLEM_DIR`

问题目录 [默认：当前目录]

`-h`, `--help`

显示帮助信息

### 作者

ABRT 团队

## 名称

`abrt-action-save-kernel-data` - 为内核错误（kernel oops）创建 uReport 强制文件。

### 摘要

`abrt-action-save-kernel-data`



### 描述

该工具读取问题目录 `DIR`。它分析内核元素的内容，检查已安装包数据库，并创建新元素 `pkg_name`, `pkg_arch`, `pkg_version`, `pkg_release`。

这些文件是 `reporter-ureporter` 需要的（uReport 中强制性的）。

### 与 ABRT 事件的集成

此工具可以作为 ABRT 报告器使用。`/etc/libreport/report_event.conf` 的示例片段：

```
### 确定崩溃发生在哪个包/组件中（如果尚未完成）：EVENT=post-create analyzer=Kerneloops abrt-action-save-kernel-data
```

### 作者

ABRT 团队

## 名称

`abrt-action-save-package-data` - 查询包数据库并保存包和组件名称。

### 摘要

`abrt-action-save-package-data` [-v] [-c CONFILE] -d DIR

### 描述

该工具读取问题目录 `DIR`。它分析 `analyzer`、`executable`、`cmdline` 和 `remote` 元素的内容，检查已安装包数据库，并创建新元素 `package` 和 `component`。

如果问题将要报告到错误跟踪数据库，则这些数据通常是必要的。

### 与 ABRT 事件的集成

此工具可以作为 ABRT 报告器使用。`/etc/libreport/report_event.conf` 的示例片段：

```
### 确定崩溃发生在哪个包/组件中（如果尚未完成）：EVENT=post-create component= abrt-action-save-package-data
```

### 参数

`-v`, `--verbose`

输出详细信息

`-c CONFILE`

配置文件的路径。

`-r CHROOT`

强制 RPM 使用 `CHROOT` 作为根目录

`-d DIR`

到问题目录的路径。

`abrt_event.conf(5)`, `abrt-action-save-package-data.conf(5)`

### 作者

ABRT 团队

## 名称

`abrt-action-trim-files` - 删除指定目录中的旧问题目录或文件，直到它们的大小小于指定大小。

### 摘要

`abrt-action-trim-files` [-v] [-d SIZE:DIR]... [-f SIZE:DIR]... [-p DIR] [FILE]...

### 参数

`-v`

输出更详细的信息。可以多次使用。

`-d SIZE:DIR`

删除 `DIR` 中的问题目录。`SIZE` 可以加 `k,m,g,t` 后缀以指定千字节、兆、吉、太字节。

`-f SIZE:DIR`

删除 `DIR` 中的文件

`-p DIR`

保留 `DIR`（从不考虑删除它）

`FILE`

保留 `FILE`（从不考虑删除它）

### 作者

ABRT 团队

## 名称

`abrt-action-applet` - 通知用户新问题的小部件程序

### 摘要

`abrt-action-applet` [-v]

### 描述

此工具监听 `org.frektop.dbus` 并等待信号。当它检测到任何 C/C++ 崩溃时，它会通过桌面弹出窗口通知用户。

### 参数

`-v`, `--verbose`

输出更详细的信息。可以多次使用。

### 参见

`dbus(8)`

### 作者

ABRT 团队

## ABRT-AUTO-REPORTING

`abrt-auto-reporting` - 获取或修改报告选项

### 摘要

`abrt-auto-reporting` [-v] [enabled | yes | disabled | no]

### 描述

从 `abrt.conf` 读取配置并保存更改。启用允许 ABRT 在检测后立即上传 uReport。禁用意味着你必须手动报告。

### 参数

`-v`, `--verbose`

输出详细信息。可以多次使用。

### 作者

(RT 相关)

## 名称

`abrt-bodhi` - ABRT bodhi 客户端。

### 摘要

`abrt-bodhi` [-v] [-r[RELEASE]] [-u URL] [-d DIR] (-b ID1[,ID2...] | PKG-NAME) [PKG-NAME]...

### 描述

`abrt-bodhi` 用于列出更新的命令行工具。Bodhi 可以通过版本、错误 ID 或包名查询。

### 参数

`-v`, `--verbose`

输出详细信息

`-r[RELEASE]`, `--release[RELEASE]`

指定版本（f16|rawhide）

`-b`, `--bugs ID1,ID2...` 指定任意数量的 Bug ID（--bugs=1234,5678）

`-d`, `--problem-dir DIR`

问题目录的路径

`-u`, `--url URL`

指定 bodhi 服务器 URL

## 名称

`abrt-cli` - 列出、删除、打印、分析、报告问题

### 摘要

`abrt-cli` [—authenticate] COMMAND [COMMAND OPTIONS]

`abrt-cli list [-vn] [—detailed] [—since NUM] [—until NUM] [DIR]...`

`abrt-cli remove [-v] DIR...`

`abrt-cli report [-v] [—delete] DIR...`

`abrt-cli info [-v] [—detailed] [-s SIZE] DIR...`

`abrt-cli status [-vb] [—since NUM]`

`abrt-cli process [-v] [—since NUM] DIR...`

### 全局参数

`-a`,—authenticate

启用 PolicyKit 验证以便处理系统问题

### 命令选项

- `-v,--verbose`

更详细的输出。可以多次使用。

- `-b,--bare`

仅打印问题计数，不打印任何消息。

- `--detailed`

显示详细报告。

- `--delete`

在报告后删除 `PROBLEM_DIR`。

- `-n,--not-reported`

仅列出未报告的问题。

- `--size SIZE`

大于 `SIZE` 字节的文本将以缩略形式显示。

- `--since NUM`

仅选择时间戳之后检测到的问题。

- `--until NUM`

仅选择早于指定时间戳的问题。

### 作者

ABRT 团队

## ABRT-DUMP-OOPS

`abrt-dump-oops` - 从 FILE（或标准输入）中提取 oops 信息

### 概要

```
abrt-dump-oops [-vusoxtm] [-d DIR]/[-D] [FILE]
```

### 描述

该工具从 `FILE` 或标准输入提取 oops 并创建问题目录，或者使用从 `FILE` 或标准输入提取的 oops 更新问题目录或打印出来。

### 文件

`/etc/abrt/plugins/oops.conf`

配置文件，用户可以在其中禁用对非致命 MCE 的检测。

### 选项

- `-v`, `--verbose`

更详细的输出。可以多次使用。

- `-s`

记录到 syslog。

- `-o`

在标准输出上打印找到的 oops。

- `-d DIR`

为每个 oops 在 `DIR` 中创建一个新的问题目录。

- `-D`

等同于 `-d DumpLocation`，`DumpLocation` 在 `abrt.conf` 中指定。

- `-u PROBLEM`

将提取的信息保存在 `PROBLEM` 目录中。

- `-x`

使问题目录对 world 可读。仅在配合 `-d`/`-D` 使用。

- `-t`

将问题目录的创建限制为 1 秒。

- `-m`

将 `abrt-watch-log` 的搜索字符串打印到 stdout 并退出。

### 参见

`abrt-watch-log(1)`, `abrt.conf(5)`

### 作者

ABRT 团队

## `abrt-dump-xorg` - 从 FILE（或标准输入）中提取 Xorg 崩溃信息

### 概要

```
abrt-dump-xorg [-vsoxm] [-d DIR]/[-D] [FILE]
```

### 描述

该工具从 `FILE` 或标准输入提取 Xorg 崩溃并创建问题目录或打印出来。

### 选项

- `-v`, `--verbose`

更详细的输出。可以多次使用。

- `-s`

记录到 syslog。

- `-o`

在标准输出上打印找到的崩溃数据。

- `-d DIR`

为找到的每个崩溃在 `DIR` 中创建一个新的问题目录。

- `-D`

等同于 `-d DumpLocation`，`DumpLocation` 在 `abrt.conf` 中指定。

- `-x`

使问题目录对 world 可读。仅在配合 `-d`/`-D` 使用。

- `-m`

将 `abrt-watch-log` 的搜索字符串打印到 stdout 并退出。

### 参见

`abrt-watch-log(1)`, `abrt.conf(5)`

### 作者

ABRT 团队



## ABRT-HANDLE-UPLOAD

## 名称

`abrt-handle-upload` - 解压并移动问题数据。

### 概要

```
abrt-handle-upload ABRT_DIR UPLOAD_DIR FILENAME
```

### 描述

该工具解压位于 `UPLOAD_DIR` 中的 `FILENAME`，并将找到的问题数据移动到 `ABRT_DIR`。它支持解压由 `gzip`、`bzip2` 或 `xz` 压缩的 `tar` 包。当 `abrtd` 在 `WatchCrashdumpArchiveDir` 选项配置的上传目录中发现新文件时会调用它。

### 作者

ABRT 团队

### 参见

`abrt.conf(5)`

## Abrt-harvest-pstoreops

## 名称

`abrt-harvest-pstoreoops` - 从 `/sys/fs/pstore/*` 文件中重建 oops，创建 ABRT 问题并删除文件

### 概要

`abrt-harvest-pstoreoops`

### 描述

此脚本旨在于系统启动且 `abrtd` 运行后执行一次。它扫描 `/sys/fs/pstore/*`，从这些文件中重建 oops 文本，根据它们创建 ABRT 问题目录，然后删除这些文件（pstore 存储是一项有限的资源）。

### 参见

`abrt-merge-pstoreoops(1)`

### 作者

ABRT 团队

## 名称

`abrt-harvest-vmcore` - 将 VMCores 转换为 ABRT 问题

### 概要

`abrt-harvest-vmcore`

### 描述

此脚本旨在于系统启动且 `abrtd` 运行后执行一次。它将 `/var/crash` 中所有的 vmcore 目录（假设是由 kdump 创建的）移动到 `abrtd` 目录。目标是让 `abrtd` 注意并将其作为新的问题数据进行处理。

### 文件

`/etc/abrt/plugins/vmcore.conf`

配置文件，用户可以在其中启用将 VMcore 复制或移动到 ABRT 问题目录

### 参见

`abrt-vmcore.conf(5)` `abrt.conf(5)`

### 作者

ABRT 团队

## Abrt-install-cpp-hook

## 名称

`abrt-install-cpp-hook` - 安装 coredump 处理器。

### 概要

`abrt-install-cpp-hook install | uninstall | is-installed`

### 描述

`abrt-install-cpp-hook` 将 ABRT coredump 处理器（保存段错误数据）注册到内核。

### 选项

- `install`

安装 coredump 处理器。

- `uninstall`

卸载 coredump 处理器。

- `is-installed`

如果安装则返回 0，否则返回 1。

### 作者

ABRT 团队

## Abrt-merge-pstoreoops

`abrt-merge-pstoreoops` - 扫描文件中的拆分消息。可以打印并删除它们。

### 概要

`abrt-merge-pstoreoops` 扫描文件中的拆分消息 `[-od]` `[-v]`

### 描述

该工具扫描文件中的拆分消息。将拆分部分合并到原始消息。

### 选项

- `-o`

打印找到的 oops。

- `-d`

删除找到的 oops。

- `-v`

更详细的输出。

### 作者

ABRT 团队

## ABRT-RETRACE-CLIENT

## 名称

`retrace-client` - 与 retrace server 通信。

### 概要

```
retrace-client <operation> [options]
```

### 描述

该工具能够与 retrace server 通信：创建一个新任务、查询状态、下载日志或回溯。

### 集成

`libreport` 用于崩溃的分析。

### 操作

- `create`

创建一个新任务。将 ID 和密码打印到 stdout。需要 `-d` 或 `-c`。

- `status`

在标准输出上打印任务状态。需要 `-t` 和 `-p`。

- `log`

在标准输出上打印任务日志。需要 `-t` 和 `-p`。

- `backtrace`

在标准输出上打印任务的回溯。需要 `-t` 和 `-p`。

- `batch`

在一个步骤中运行所有操作：创建一个新任务，定期查询状态（由 `--status-delay` 指定），并在完成后下载。如果任务成功则保存回溯文件，否则将日志打印到 stdout。需要 `-c` 或 `-d`。

### 选项

- `-v`, `--verbose`

详细。

- `-s`

记录到 syslog。

- `-k,--insecure`

允许不安全连接 retrace server。

- `-url`

retrace server 的 URL。

- `-headers`

调试显示收到的 HTTP 头。

- `-d`, `--dir`

从 ABRT 问题目录读取数据。

- `-c`, `--core`

从 core dump 读取数据。

- `-l`, `--status-delay`

轮询操作间隔（秒）。

- `-no-unlink`

调试不删除 `/tmp` 中的临时文件。

- `-t --task`

服务器上的任务 ID。

- `-p password`

服务器上的任务密码。

### 作者

ABRT 团队

## `abrt-server` - ABRT 的 Unix socket。

### 概要

```
abrt-server [-u UID] [-sp[v]...
```

### 描述

`abrtd-server` 由 `abrtd` 守护进程执行以处理 socket 连接。系统中的每个应用程序都可以按照协议（见下文协议部分）调用创建问题目录。

### 选项

- `-u UID`

使用客户端 uid

- `-s`

记录到日志。

- `-p`

在日志中添加程序名。

- `-v`

记录详细的调试信息。

### 协议

初始化 dump：连接到 UNIX 域 socket `/var/run/abrt.socket`

提供数据（写入 `"n\n"`）

```
- > POST / HTTP/1.1\r\n" -> "\r\n" -> "type=string\0" 字符串最大长度 100 字节 -> "reason=string\0" 字符串最大长度 512 字节
- >"pid=number\0" 数字， 0 - PID_MAX (/proc/sys/kernel/pid_max) -> -executable=string\0" 字符串最大长度 1 MB -> -backtrace=string\0" 字符串最大长度 -MAX_PATH -> (关闭写入的 socket) <- - "HTTP/1.1 201 \r\n" <- - "\r\n"
```

### 作者

ABRT 团队

## 名称

`abrt-watch-log` - 监控日志文件并在文件增长或被替换时运行命令

### 摘要

`abrt-watch-log [-vs] [-F STR] ... FILE PROG [ARGS]`

### 选项

- `-F STR`

如果未找到 `STR`，则不运行 `PROG`

- `-v`, `--verbose`

输出更详细的信息。可以多次使用。

- `-s`

记录到 syslog

### FILE

被监控的文件

### PROG

可执行文件的路径

### ARGS

`PROG` 的参数

### 作者

ABRT 团队

## 名称

`abs2rel` - 将绝对路径转换为相对路径

### 摘要

`abs2rel` 路径 基准

### 描述

`abs2rel` 命令恰好接受两个参数——目标路径和一个基路径。它会确定从基路径到目标路径的相对路径，并将其打印到标准输出。

## 示例

`abs2rel /1/2/3/a/b/c /1/2/3` 将在标准输出上打印 `a/b/c`。

`abs2rel foo/bar foo/baz` 将在标准输出上打印 `../bar`。

# 报告错误

错误应通过 Red Hat Bugzilla 报告：`http://bugzilla.redhat.com/`。

## 名称

`ac` - 打印关于用户连接时间的统计信息

### 摘要

```
[ -d |daily-totals ] [ -y |print-year ] [ -p |individual-totals ] [ people ] [ -f
--file filename ] [ -a |all-days ] [ --complain ] [ --reboots ] [ --supplants ] [ --
timawarps ] [ --compatibility ] [ --tw-leniency num ] [ --tw-suspicious num ] [ -z
|print-zeros ] [ --debug ] [ -V|version ] [ -h |--help ]
```

### 描述



`ac` 根据当前 `wtmp` 文件中的登录/注销情况打印连接时间（以小时为单位）报告。还会打印一个总计。

会计文件 `wtmp` 由 `init(8)` 和 `login(1)` 维护。`ac` 或 `login` 都不会在 `wtmp` 不存在时创建它，因此不会进行会计。要开始会计，请创建一个长度为零的文件。

注意：`wtmp` 文件增长得非常快。你可能需要经常修剪它。

GNU `ac` 的工作原理与 uix `ac` 几乎相同，尽管它在某些方面更智能。因此，你应该预期 GNU `ac` 的输出与其他系统上 `ac` 的输出存在差异。使用命令 `info accounting` 来获取更多信息。

### 选项

- `-d`, `--daily-totals`

  打印每天的总计，而不是在最后只打印一个大总计。输出如下：Jul 3 total 1.17 Jul 4 total 2.10 Jul 5 total 8.23 Jul 6 total 2.10 Jul 7 total 0.30

- `-p`, `--individual-totals`

  除了通常的合并值外，还打印每个用户的时间总计。看起来像：bob 8.06 goff 0.60 maley 7.37 root 0.12 16.15

- `people`

  打印 `people` 中包含的所有用户使用的连接时间总和。注意，`people` 是用空格分隔的有效用户名列表；不允许通配符。

- `-f`, `--file filename`

  从文件 `filename` 而不是系统的 `wtmp` 文件读取。

- `--complain`

  当 `wtmp` 文件出现问题时（时间回溯、记录丢失或任何情况），打印适当的错误。

- `--reboots`

  重启记录不是在重启时写入，而是在系统启动时写入；因此，无法确切知道重启发生的时刻。用户可能在重启时登录系统，`ac` 会自动将登录和重启记录之间的时间计入用户（尽管可能应该这样做，例如如果系统关机很久）。如果你想计算这段时间，请包含此标志。*对于原生 `ac`*

- `--supplants`

  有时

- `--timewraps`

  有时，`wtmp` 文件中的项会突然跳回过去，而没有发生时钟更改记录。无法在这种情况下用户登录了多久。如果你想将登录和时间回溯之间的时间计入用户，请包含此标志。*为了兼容原生 `ac`，请包含此标志。*

- `--compatibility`

  这是输入上述三个选项的简写。

- `-a`, `--all-days`

  如果我们打印每日总计，则打印每一天的记录，而不是跳过没有登录活动的中间日期。如果没有此标志，这些中间日期积累的时间将被列出。

- `--lenency num`

  将容忍度设置为 `num`。

- `--suspicious num`

  将可疑度设置为 `num`。

- `-z|print-zeros`

  打印零。

- `--debug`

  调试。

- `-V|version`

  打印版本。

- `-h|--help`

  打印帮助信息

- 文件

  `wtmp` 文件

- 作者

  会计工具由 Noel Cragg 编写。

- 另请

  `login(1)`, `wtmp(5)`

## 名称

`ac` - 打印关于用户连接时间的统计信息

### 摘要

`ac` - connect connect to

## 名称

`ac` - connect to-AC

### 摘要

```
[ -d |daily-totals ] [ -y |print-year ] [ -p |individual-totals ] [ people ] [ -f
--file filename ] [ -a |all-days ] [ --complain ] [ --reboots ] [ --supplants ] [ --
timawarps ] [ --compatibility ] [ --tw-leniency num ] [ --tw-suspicious num ] [ -z
|print-zeros ] [ --debug ] [ -V|version ] [ -h |--help ]
```

### 描述

`ac` 根据当前 `wtmp` 文件中的登录/注销情况打印连接时间（以小时为单位）报告。还会打印一个总计。

会计文件 `wtmp` 由 `init(8)` 和 `login(1)` 维护。`ac` 或 `login` 都不会在 `wtmp` 不存在时创建它，因此不会进行会计。要开始会计，请创建一个长度为零的文件。

注意：`wtmp` 文件增长得非常快。你可能需要经常修剪它。

GNU `ac` 的工作原理与 uix `ac` 几乎相同，尽管它在某些方面更智能。因此，你应该预期 GNU `ac` 的输出与其他系统上 `ac` 的输出存在差异。使用命令 `info` 来获取更多信息。

### 选项

- `-d`, `--daily-totals`

  打印每天的总计，而不是在最后只打印一个大总计。输出如下：Jul 3 total 1.17 Jul 4 total 2.10 Jul 5 total 8.23 Jul 6 total 2.10 Jul 7 total 0.30

- `-p`, `--individual-totals`

  除了通常的合并值外，还打印每个用户的时间总计。看起来像：bob 8.06 goff 0.60 maley 7.37 root 0.12 16.15

- `people`

  打印 `people` 中包含的所有用户使用的连接时间总和。注意，`people` 是用空格分隔的有效用户名列表；不允许通配符。

- `-f`, `--file filename`

  从文件 `filename` 而不是系统的 `wtmp` 文件读取。

- `--complain`

  当 `wtmp` 文件出现问题时（时间回溯、记录丢失或任何情况），打印适当的错误。

- `--reboots`

  重启记录不是在重启时写入，而是在系统启动时写入；因此，无法确切知道重启发生的时刻。用户可能在重启时登录系统，`ac` 会自动将登录和重启记录之间的时间计入用户（尽管可能应该这样做，例如如果系统关机很久）。如果你想计算这段时间，请包含此标志。*对于原生 `ac`*

- `--supplants`

  有时

- `--timewraps`

  有时，`wtmp` 文件中的项会突然跳回过去，而没有发生时钟更改记录。无法在这种情况下用户登录了多久。如果你想将登录和时间回溯之间的时间计入用户，请包含此标志。*为了兼容原生 `ac`，请包含此标志。*

- `--compatibility`

  这是输入上述三个选项的简写。

- `-a`, `--all-days`

  如果我们打印每日总计，则打印每一天的记录，而不是跳过没有登录活动的中间日期。如果没有此标志，这些中间日期积累的时间将被列出。

- `--lenency num`

  将容忍度设置为 `num`。

- `--suspicious num`

  将可疑度设置为 `num`。

- `-z|print-zeros`

  打印零。

- `--debug`

  调试。

- `-V|version`

  打印版本。

- `-h|--help`

  打印帮助信息

- 文件

  `wtmp` 文件

- 作者

  会计工具由 Noel Cragg 编写。

- 另请

  `login(1)`, `wtmp(5)`

## 名称

`ac` - 打印关于用户连接时间的统计信息

### 摘要

`ac` - connect connect to-AC

## 名称

`abs2rel` - 将绝对路径转换为相对路径

### 摘要

`**abs2rel**` 路径 基准

### 描述

`**abs2rel**` 命令恰好接受两个参数——目标路径和一个基路径。它会确定从基路径到目标路径的相对路径，并将其打印到标准输出。

## 示例

`abs2rel /1/2/3/a/b/c /1/2/3` 将在标准输出上打印 `a/b/c`。

`abs2rel foo/bar foo/baz` 将在标准输出上打印 `../bar`。

# 报告错误

错误应通过 Red Hat Bugzilla 报告：http://bugzilla.redhat.com/。

## 名称

`ac` - 打印关于用户连接时间的统计信息

### 摘要

```
[ -d |daily-totals ] [ -y |print-year ] [ -p |individual-totals ] [ people ] [ -f
--file filename ] [ -a |all-days ] [ --complain ] [ --reboots ] [ --supplants ] [ --
timawarps ] [ --compatibility ] [ --tw-leniency num ] [ --tw-suspicious num ] [ -z
|print-zeros ] [ --debug ] [ -V|version ] [ -h |--help ]
```

### 描述

`ac` 根据当前 `wtmp` 文件中的登录/注销情况打印连接时间（以小时为单位）报告。还会打印一个总计。

会计文件 `wtmp` 由 `init(8)` 和 `login(1)` 维护。`ac` 或 `login` 都不会在 `wtmp` 不存在时创建它，因此不会进行会计。要开始会计，请创建一个长度为零的文件。



注意：`wtmp` 文件增长得非常快。你可能需要经常修剪它。

GNU `ac` 的工作原理与 `uix ac` 几乎相同，尽管它在某些方面更智能。因此，你应该预期 GNU `ac` 的输出与其他系统上 `ac` 的输出存在差异。使用命令 `info accounting` 来获取更多信息。

### 选项

- `-d`, `--daily-totals`

  打印每天的总计，而不是在最后只打印一个大总计。输出如下：Jul 3 total 1.17 Jul 4 total 2.10 Jul 5 total 8.23 Jul 6 total 2.10 Jul 7 total 0.30

- `-p`, `--individual-totals`

  除了通常的合并值外，还打印每个用户的时间总计。看起来像：bob 8.06 goff 0.60 maley 7.37 root 0.12 16.15

- `people`

  打印 `people` 中包含的所有用户使用的连接时间总和。注意，`people` 是用空格分隔的有效用户名列表；不允许通配符。

- `-f`, `--file filename`

  从文件 `filename` 而不是系统的 `wtmp` 文件读取。

- `--complain`

  当 `wtmp` 文件出现问题时（时间回溯、记录丢失或任何情况），打印适当的错误。

- `--reboots`

  重启记录不是在重启时写入，而是在系统启动时写入；因此，无法确切知道重启发生的时刻。用户可能在重启时登录系统，`ac` 会自动将登录和重启记录之间的时间计入用户（尽管可能应该这样做，例如如果系统关机很久）。如果你想计算这段时间，请包含此标志。*对于原生 ac*

- `--supplants`

  有时

- `--timewraps`

  有时，`wtmp` 文件中的项会突然跳回过去，而没有发生时钟更改记录。无法在这种情况下用户登录了多久。如果你想将登录和时间回溯之间的时间计入用户，请包含此标志。*为了兼容原生 ac，请包含此标志。*

- `--compatibility`

  这是输入上述三个选项的简写。

- `-a`, `--all-days`

  如果我们打印每日总计，则打印每一天的记录，而不是跳过没有登录活动的中间日期。如果没有此标志，这些中间日期积累的时间将被列出。

- `--lenency num`

  将容忍度设置为 `num`。

- `--suspicious num`

  将可疑度设置为 `num`。

- `-z|print-zeros`

  打印零。

- `--debug`

  调试。

- `-V|version`

  打印版本。

- `-h|--help`

  打印帮助信息

- 文件

  `wtmp` 文件

- 作者

  会计工具由 Noel Cragg 编写。

- 另请

  `login(1)`, `wtmp(5)`

### 参见

`aseqnet(1)`, `aseqview(1)`

### 作者

Takashi Iwai <tiwai@suse.de>

## 名称

`afs5log` - AFS 令牌初始化器

### 概要

```
afs5log [[ -v] [-5] [-k] [-p path] [cell[=principal]] ] ] [...]
```

### 描述

`afs5log` 命令使用 Kerberos 为指定的单元获取 AFS 令牌。如果没有指定单元，则为本地单元获取令牌。如果已知 af 服务的主体名称（principal name），也可以以 `cell=principal_name` 的形式给出单元名称。程序会尝试先获取 Kerberos IV 凭据，如果失败，`afs5log` 将创建 Kerberos 5 (2b样式) 令牌。

### 参数

`-v`

开启详细输出模式。`afs5log` 在工作时将打印调试信息。多次使用该选项可获取更详细的信息。

- `-p path`

确定指定路径所在的单元，并为该单元获取令牌。

- `-s strategy`

用指定的策略覆盖默认的令牌设置策略（“2b”）。识别的策略名称包括：`rx5` `rxk5`（需要 OpenAFS 1.6 或更高版本），`2b` `rxkad` “2b”（需要 OpenAFS 1.2.8 或更高版本）。

- `-5`

跳过使用 Kerberos IV 的尝试，仅使用 2b 样式令牌，该令牌仅支持 OpenAFS 1.2.8 及更高版本。

- `-k`

跳过使用 Kerberos IV 的尝试并使用 `rxk5` 样式令牌，该令牌仅支持 OpenAFS 1.6 或更高版本。

- `-n`

假设如果单元名称和领域（realm）名称仅大小不同，则 AFS 服务的主体名称不包含实例。

### 参见

`pam_krb5(5)` `krb5.conf(5)`

## 缺陷

可能存在，但我们希望没有。如果你发现任何问题，请在 `http://bugzilla.redhat.com/` 针对“`pam_krb5`”组件提交 bug 报告。

### 作者

Nalin Dahyabhai <nalin@redhat.com>

## ALSACTL

## 名称

`alsactl` - ALSA 声卡驱动的高级控制

### 概要

```
alsactl [options] [store|restore|init] <card # or id or device>
```

```
alsactl monitor <card # or id>
```

### 描述

`alsactl` 用于控制 ALSA 声卡驱动的高级设置。它支持多个声卡。如果你的声卡具有某些似乎无法从混合器应用程序中控制的功能，那么你来对地方了。

### 命令

`store` 将所选声卡的当前驱动状态保存到配置文件中。

`restore` 从配置文件加载所选声卡的驱动状态。如果恢复失败（最终是部分失败），将调用 `init` 操作。

`nstore` 类似于 `restore`，但还会通知守护进程对可用声卡进行新的重新扫描。

`init` 尝试将所有设备初始化为默认状态。如果设备未知，则返回错误代码 99。

`daemon` 定期保存声音状态。

`rdaemon` 类似于 `daemon`，但会先恢复声音状态。

`kill` 通知守护进程执行指定操作（退出、重新扫描、保存并退出）。

`monitor` 用于监控从给定控制设备接收到的事件。

如果没有指定声卡，将对所有声卡的设置进行保存、加载或监控。

### 选项

`-h`, `--help`

帮助：显示可用标志和命令。

`-d`, `--debug`

使用调试模式：更详细。

`-v`, `--version`

打印 `alsactl` 版本号。

- `-f`, `--file`

选择使用的配置文件。默认是 `/var/lib/alsa/asound.state`。

- `-l`, `--lock`

使用文件锁来序列化对状态文件的并发访问（这是全局状态文件的默认设置）。

- `-L`, `--no-lock`

不使用文件锁序列化对状态文件的并发访问（包括全局状态文件）。

- `-O`, `--lock-state-file`

选择状态锁文件路径。

- `-F`, `--force`

配合 `restore` 命令。尽可能恢复匹配的控制元素。此选项现设置为默认值。

- `-g`, `--ignore`

配合 `store` 和 `restore` 命令。当未安装声卡时不显示“未找到声卡”且不设置错误退出状态码。

- `-P`, `--pedantic`

配合 `restore` 命令。不恢复不匹配的控制元素。这是是旧的默认行为。

- `-I`, `--no-init-fallback`

如果恢复失败，不初始化声卡。从 1.0.18 版本开始，`alsactl` 尝试将恢复操作作为默认来初始化卡。但这可能与旧版本不兼容。调用者可能期望在不存在状态文件时不触碰状态。此选项通过抑制初始化将恢复行为回退到旧版本。

- `-r`, `--runstate`

将恢复和初始化状态保存到此文件。该文件仅包含错误。错误会在文件末尾附加声卡 ID。

- `-R`, `--remove`

先删除 `runstate` 文件。

- `-E`, `--env=#`

设置环境变量（用于 `init` 操作，或你可以覆盖 `ALSA_CONFIG_PATH` 以读取不同的或优化的配置 - 可能对“启动”脚本有用）。

- `-i`, `--initfile`

`init` 的配置文件。默认使用 `PREFIX/share/alsa/00main`。

- `-p`, `--period`

`daemon` 命令的存储周期（秒）。

- `-e`, `--pid-file`

存储进程 ID 文件的路径，采用 UUCP 格式（ASCII）。

- `-b`, `--background`

在后台运行任务。

- `-s`, `--syslog`

使用 `syslog` 消息。

- `-c`, `--sched-idle`

将进程调度策略设置为空闲（`SCHED_IDLE`）。

### 文件

`/var/lib/alsa/asound.state`. 使用的配置文件。默认是 `/var/lib/alsa/asound.state`。

### 参见

`pam_krb5(5)` `krb5.conf(5)`

# 缺陷

可能存在，但我们希望没有。如果你发现任何问题，请在 `http://bugzilla.redhat.com/` 针对“`pam_krb5`”组件提交 bug 报告。

### 作者



Nalin Dahyabhai <nalin@redhat.com>

`device` - 控制 ID 设备
`subdevice` - 控制 ID 子设备

`iface` - 控制 ID 接口
`numid` - 控制 ID numid

`-O <ossmixid>` | `--ossmixer=<midid>`

将混音器控制从 OSS 混合器仿真层（捕获卡）重定向到 ALSA 层（捕获卡）。`ossmixid` 的格式为 `ALSA,[INDEX]@OSSID`：

“Master@VOLUME” “PCM,1@ALTPCM

已知的 OSS 属性：

`VOLUME`, `BASS`, `TREBLE`, `SYNTH`, `PCM`, `SPEAKER`, `LINE`, `MIC`, `CD`, `IMAX`, `A`

`RECLEV`, `IGAIN`, `OGAIN`, `LINE1`, `LINE2`, `LINE3`, `DIGITAL1`, `DIGITAL2`, `DIGIT`,

`PHONEIN`, `PHONEOUT`, `VIDEO`, `RADIO`, `MONITOR`

`-v` | `--verbose`

详细模式。多次使用可增加详细程度。

`-U` | `--xrun`

详细的 xrun（缓冲区溢出）性能分析。

`-W <timeout>` | `--wake=<timeout>`

设置进程唤醒超时时间。

## 示例

```
alsaloop -C hw:0,0 -P hw:1,0 -t 50000
```

## 缺陷

暂无已知。

### 作者

`alsaloop` 由 Jaroslav Kysela <perex@perex.cz> 编写。本文档由 Jaroslav Kysela <perex@perex.cz> 编写。

# `alsamixer` - 用于 ALSA 声卡驱动声卡混音器，带有 ncurses 界面

### 摘要

`alsamixer` 是一个用于 ALSA 声卡驱动的 ncurses 混音器程序。它支持带有多个设备的多个声卡。

### 选项

`-h,--help`

帮助：显示可用标志。

`-c,--card <声卡编号或标识>`

如果有多个声卡，选择要使用的声卡。声卡从 0（默认）开始编号。

`-D,--device <设备标识>`

选择要控制的混音器设备。

`-V,--view <mode>`

选择起始视图模式：播放、捕获或全部。

`-g,--no-color`

切换颜色使用。

## 混音器视图

`alsamixer` 的左上角显示了一些基本信息：声卡名称、混音器芯片名称、当前视图模式和当前选中的混音器项。当混音项被关闭时，名称中将显示 `[Off]`。

音量条位于基本信息区域下方。你可以向左/右滚动，所有的控制无法显示在一个屏幕内。每个控制的名称显示在音量条下方的。当前选中的项用红色绘制并/或突出。

每个具有音量能力的混音器控制都会显示一个框，并在框内填充当前音量。音量百分比显示在左、右通道的音量条下方。对于单声道控制，此处只显示一个值。

当一个混音器控制被关闭时，音量条下方会出现 M（静音）。当它开启时，取而代之的是绿色的 O。你可以通过 `m` 键切换开关。

当一个混音器控制具有捕获功能时，捕获标志也会出现在音量条下方。当捕获关闭时，将显示 —。当捕获开关打开时，会出现红色的 CAPTURE。此外，左右侧会显示 L 和 R 字母，表示左右声道已开启。

某些控制具有枚举列表，不显示框，而是仅显示指示当前活动项的文本。你可以通过上/下键更改项。

## 视图模式

`alsamixer` 有三种视图模式：播放、捕获和全部。在播放视图中，只显示与播放相关的控制。同样，在捕获视图中，只显示用于捕获（录制）的控制。全部视图显示所有控制。当前视图模式与混音器名称等一起显示在左上角。

默认视图模式是播放视图。你可以通过 `-V` 选项更改。

每个视图模式也可以通过键盘命令切换。见下一节。

## 键盘命令

`alsamixer` 识别以下键盘命令来控制声卡。此处显示的大写命令也可以用小写给出。按 `h` 键可以提示这些按键。

### 通用控制

左和右方向键用于选择通道（或设备，取决于你的偏好术语）。你也可以使用 `n`（下一个）和 `p`（上一个）。

向上和向下方向键控制当前选定设备的音量。你也可以使用 `+` 或 `-` 实现相同目的。左右信号都会受到影响。若需独立的左右控制，请参阅下文。`B` 或 `=` 键调整左右通道音量的平衡。

`M` 切换当前通道（左右都是）。如果硬件支持，你可以分别使用 `,` (`<`) (或 `()`) 和 `.` (或 `>`) 分别静音左右声道。

`SPACE`（空格）启用当前通道的录制。如果任何其他通道开启了录制，它们将首先禁用录制功能。当然，这只对有效的输入通道有效。

`L` 重绘屏幕。

## 视图模式控制

功能键用于切换视图模式。`F1` 和 `F2` 键分别显示帮助和进程信息。`F3`、`F4` 和 `F5` 键分别切换到播放、捕获和全部模式。`TAB` 切换当前视图。

## 音量更改

`PageUp` 增加音量 5。

`PageDown` 减少音量 5。

`End` 设置音量为0。

## 选择声卡

你可以按 `F6` 或 `S` 键选择另一块卡。这将显示可用声卡列表以便手动输入混音器名称。

## 退出

按 `ALT Q` 或 `ESC` 退出程序。请注意在某些终端上可能需要按两次 `ESC`。

## 音量映射

在 `alsamixer` 中，音量被映射到一个更符合人类直觉的值，即位置是线性因子的立方根。对于范围较小（24 dB以内）的控制，采用线性映射，每步大小相等。

对于没有 dB 信息的控制，使用硬件寄存值的线性映射。

## 缺陷

某些终端模拟器（例如 `nxterm`）可能与 `ncurses` 工作得不完美，但那是它们的问题。普通的 `xterm` 看起来正常。

### 作者

`alsamixer` 由 Tim Janik 编写，由 Jaroslav Kysela <perex@perex.cz> 和 Clemens Ladisch 进一步改进。

本文档由 Paul Winkler <zarmz@erols.com> 提供。

# `alsaunmute` - 用于初始化 ALSA 设备的简单脚本

### 描述

`alsaununmute` 是一个 脚本，运行带有 init 参数的 `alsactl(1)` 工具（详情见脚本）。

### 选项

无

### 示例

```
alsaununmute
```

### 参见

`alsactl(1)`, `alsamixer(1)`, `amixer(1)`

# `amidi`

### 选项

使用 `-h`, `-V`, `-l` 或 `-L` 选项显示信息；或至少使用 `-s`, `-r`, `-S`, 或 `-d` 选项之一来指定要发送或接收的数据。

`-h,--help`

帮助：打印选项列表。

`-V,--version`

打印当前版本。

`-l,--list-devices`

打印所有硬件 MIDI 端口列表。

`-L,--list-rawmidis`

打印所有 RawMIDI 定义。（用于调试配置文件时）。

`-p,--port=name`

设置要使用的 ALSA RawMIDI 端口名称。如果未指定，`*amidi*` 将使用配置文件中定义的默认端口（该端口的默认值为卡 0 上的 0，该端口可能不存在）。

`-s,--send=filename`

将指定文件的内容发送到 MIDI 端口。该文件必须包含原始 MIDI 命令（例如 `.syx` 文件）；对于标准 MIDI (`.mid`) 文件，请使用 `playmidi(1)`）。

`-r,--receive=filename`

将来自 MIDI 端口的数据写入指定的文件。该文件将包含原始 MIDI 命令（如 `.syx` 文件）；要录制标准 MIDI (`.mid`) 文件，请使用 `arecordmidi(1)`）。

`amidi` 将过滤掉任何活动感字节 (`FeH`)，除非提供了 `-a` 选项。

`-S,--send-hex=...`

将指定的十六进制数字指定的字节发送到 MIDI 端口。

`-d,--dump`

将从 MIDI 端口接收的数据作为十六进制字节打印。除非提供了 `-a` 选项，否则不会显示活动感字节 (`FeH`)。

此选项用于调试。

`-t,--timeout=seconds`

当在指定时间内没有接收到数据时，停止接收数据。

如果未提供此选项，你必须按下 `Ctrl+C`（或 `kill amidi`）来停止接收数据。

`-a,--active-sensing`

在保存或打印接收到的 MIDI 命令时，不忽略活动感字节 (`FeH`)。

## 示例

```
amidi -p hw:0 -s my_settings.syx
```

将 `my_settings.syx` 中的 MIDI 命令发送到端口 `hw:0`。

```
amidi -S ‘F0 43 10 4C 00 00 7E 00 74 F7’
```

向默认端口发送 XG 重置信号。

```
amidi -p hw:1,2 -S F041104211C00000000074F7 -r dump.syx -t 1
```

向 GS 设备发送“参数转储请求”，将接收到的参数数据保存到文件 `dump.syx`，并在设备完成数据发送后停止（当一秒内没有接收到数据时）。

```
amidi -p virtual -d
```



# 创建一个虚拟 RawMIDI 端口并打印所有发送到该端口的数据

### 文件

`/usr/share/alsa/alsa.conf` rawmidi 定义

`/etc/asound.conf` 系统级 rawmidi 定义

`~/.asoundrc` 用户特定的 rawmidi 定义

# 另请

`aplaymidi(1)`

`arecordmidi(1)`

### 作者

Clemens Ladisch <clemens@ladisch.de>

`amixer` - 用于 ALSA 声卡驱动的命令行混音器

### 摘要

`amixer [-option] [cmd]`

不带参数的 `amixer` 将显示默认声卡和设备的当前混音设置。这是查看你可以使用的简单混音控制列表的良好方法。

### 命令

`help`

显示语法。

`info`

显示关于混器设备的信息。

`scontrols`

显示简单混音控制的完整列表。

`scontents`

显示带有内容的简单混音控制完整列表。

`set` `sset <SCONTROL> <PARAMETER> ...`

设置简单混音控制的内容。参数可以是从 0% 到 100% 的百分比音量（带有 `%` 后缀）、带有 dB 后缀的 dB 增益（如 `-12.5dB`）或精确的硬件值。dB 增益仅用于具有可用 dB 信息的混音器元件。当音量值后附加加(+)或减(-) 字母时，音量将分别从当前值增加或减少。

参数 `cap`, `nocap`, `mute`, `unmute`, `toggle` 用于更改指定组的捕获（录制）和静音。

可选的修饰符可以作为额外参数，以指定应用的流方向或通道。修饰符 `playback` 和 `capture` 指定流，而修饰符 `front`, `rear`, `center`, `woofer` 用于指定要更改的通道。

必须指定一个简单混音控制。一次只能控制一个设备。

`get` 或 `sget <SCONTROL>`

显示简单混音控制的内容。

必须指定一个简单混音控制。一次只能控制一个设备。

`controls`

显示卡控制的完整列表。

`contents`

显示带有内容的卡控制完整列表。

`cset <SCONTROL> <PARAMETER> ...`

设置卡控制的内容。标识符包含组件：`iface`, `name`, `device`, `subdevice`, `numid`。下一个参数指定控制的值。

`cget <SCONTROL>`

显示卡控制的内容。标识符的语法与 `cset` 相同。

### 选项

`-c card`

选择卡号。由此参数创建的设备名称语法为 `hw:N`，其中 N 是指定的卡。

`-D device`

选择设备。由此参数创建的设备名称语法为 `hw:N`，其中 N 是指定的卡。

`-sstdin`

从标准输入读取。当给定此选项时，使用默认 格式。其他选项被忽略。

`-h`

显示语法。

`-q`

静默模式。

`-R`

使用 raw 格式。

`-M`

使用 ALSA 格式。

## 示例

`amixer -c1 sset Line 80%,40%`

将 Line 设置为 80% 捕获，40% 播放。

`amixer -c1 sset Master -20dB`

将 Master 设置为 -20dB。如果指定了多个，则应用于声卡。

`amixer -c1 sset Master 80%`

将 Master 设置为 80%。当存在多个通道时，应用此。

`amixer -c1 sset Line 80%`

将 Line 设置为 80%。

设备再次可用。

`-F,--period-time=#`

中断之间的间隔为 # 微秒。如果未给出周期时间（周期大小（period size），则设置为缓冲区时间的四分之一。

`-B,--buffer-time=#n`

缓冲区持续时间为 # 微秒。如果未给出缓冲区时间和缓冲区大小（buffer size），则设置为最大允许的缓冲区时间，但不超过 500ms。

`--period-size=#n`

中断之间的间隔为 # 帧。如果未给出周期大小和周期时间（period time），则设置为缓冲区大小的四分之一。

`--buffer-size=#n`

缓冲区持续时间为 # 帧。如果未给出缓冲区时间和缓冲区大小，则设置为最大允许的缓冲区时间，但不超过 500ms。

`-A,--avail-min=#n`

用于唤醒的最小可用空间为 # 微秒。

`-R,--start-delay=#n`

自动 PCM 启动的延迟为 # 微秒（如果 <= 0，则相对于缓冲区大小）。

`-T,--stop-delay=#`

从 xrun（上溢）发生后，自动 PCM 停止的延迟为 # 微秒。

`-v,--verbose`

显示 PCM 结构和设置。此选项可累加。当给出两次或三次时，将显示 VU 表。

`-V,--vmeter=TYPE`

指定 VU 表类型，立体声（stereo）或单声道（mono）。立体声 VU 表仅适用于交错格式的 2 通立体声。

`-I,--separate-channels`

每个通道一个文件。此选项将禁用 max-file-time 和 use-strptime，并忽略 SIGUSR1。使用独立通道时无法使用立体声 VU 表。

`-P`

播放。如果通过输入 aplay 调用程序，则为默认值。

`-C`

录制。如果通过输入 arecord 调用程序，则为默认值。

`-i,--interactive`

允许通过标准输入（stdin）进行交互。目前仅实现了通过空格键或回车键进行暂停/恢复。

`-m,--chmap=ch2,...`

提供通道映射以覆盖或遵循。传递诸如 FL、FR 等通道位置字符串。

如果设备支持覆盖通道映射，aplay 会尝试传递该通道映射。如果它不支持通道映射覆盖但仍提供了通道映射信息，aplay 会尝试重新排列缓冲区中的通道顺序，以匹配设备返回的通道映射。

`--disable-resample`

禁用自动重采样。

`--disable-channels`

禁用自动通道转换。

`--disable-format`

禁用自动格式转换。

`--disable-softvol`

禁用软件量控制（softvol）。

`--test-position`

测试环形缓冲区（ring buffer）位置。

`--test-coef=<coef>`

测试环形缓冲区位置的系数；默认值为 8。验证表达式为：`coef * (buffer_size / 2)`。最小值为1。

`--test-nowait`

不等待环形缓冲区——会消耗所有 CPU。

录制时，当输出文件积累声音达到足够长度时，关闭它并打开一个新的输出文件。默认值为文件格式支持的最大大小：WAV 文件为 2 GiB。如果指定了 `--separate-channels`，此选项无效。

`--process-id-file <id name>`

aplay 将其进程 ID 写入此处，其他程序可以向其发送信号。

`--use-strftime`

录制时，每当打开输出文件，使用 strftime 功能解释文件名参数中的 % 代码。重要的 strftime 代码有：`%Y` 年份，`%m` 月，`%d` 日，`%H` 小时，`%M` 分钟和 `%S` 秒。此外，`%v` 是文件编号，从 1 开始。指定此选项时，会自动创建输出文件的中间目录。如果指定了 `--separate-channels`，此选项无效。

`--dump-hw-params`

将设备预配置状态的 hw_params 导出到 stderr。导出列出了所选设备的能力，如支持的格式、采样率、通道数、周期和缓冲区字节/大小/时间。对于原始设备 hw:X，此选项列出声卡的硬件能力。

`--fatal-errors`

当遇到错误（例如 xrun）时禁用恢复尝试；aplay 进程将立即终止。

## 信号 (SIGNALS)

录制时，`SIGINT`、`SIGTERM` 和 `SIGABRT` 将关闭输出文件并退出。`SIGUSR1` 将关闭输出文件，打开新文件并继续录制。然而，`SIGUSR1` 配合 `--separate-channels`时不工作。

## 示例 (EXAMPLES)

```
aplay -c 1 -t raw -22050 -f mu_law foobar
```

将把原始文件“foobar”作为 22050-Hz、8 位、单声道、Mu-Law .au 文件播放。

```
record -d 10 -f cd -t wav -D copy foobar.wav
```

将 foobar.wav 录制为 10 秒的 CD 质量波形文件，使用 PCM “copy”（这可能在用户的 .asoundrc 文件中定义为：pcm.copy { type plug slave { pcm hw } route_policy copy }）。

```
record -t wav --max-file-time 30 mon.wav
```

从默认音频源录制单声道、每秒 8,000 采样、每采样 8 位的内容。每 30 秒创建一个新文件。文件名为 mon-nn.wav，其中 nn 从 01 开始增加。mon-99.wav 之后的文件是 mon-100.wav。

```
record -f cd -t wav --max-file-time 3600 --use-strftime %Y/%m/%d/listen-%H%M-%v.wav
```



从默认音频源以立体声录制。每小时创建一个新文件。文件根据其日期放置在目录中。

`unset`，在这种情况下，它将根据你的 `$PATH` 环境变量确定一个适当的 `manpath`。此选项将覆盖 `$MANPATH` 的内容。

### `-L locale`, `--locale=locale`

`apropos` 通常会通过调用 C 函数 `setlocale(3)` 来确定你当前的 `locale`，该函数会查询各种环境变量，可能包括 `$LC_MESSAGES` 和 `$LANG`。若要临时覆盖确定的值，可以使用此选项直接将 `locale` 字符串传递给 `apropos`。请注意，在实际开始搜索页面之前，它不会生效。帮助信息等输出将始终在最初确定的 `locale` 中显示。

### `-C file`, `--config-file=file`

使用此配置文件而不是默认的 `~/.manpath`。

### `-?`, `--help`

打印帮助信息并退出。

### `-usage`

打印简短的用法信息并退出。

### `-V`, `--version`

显示版本信息。

## 退出状态 (EXIT STATUS)

- `0` 程序执行成功。
- `1` 用法、语法或配置文件错误。
- `2` 运行错误。
- `16` 未找到匹配指定标准的项目。

## 环境 (ENVIRONMENT)

### 系统 (SYSTEM)

如果设置了 `$SYSTEM`，其效果与作为 `-m` 选项参数相同。

### MANPATH

如果设置了 `$MANPATH`，其值将被解释为用冒号分隔的帮助页层级搜索路径。

### MANWIDTH

如果设置了 `$MANWIDTH`，其值将作为终端宽度（参见 `—long` 选项）。如果未设置，终端宽度将使用 `$COLUMNS` 的值、可用的 `ioctl(2)` 计算，如果所有其他尝试都失败，则回退到 80 个字符。

### POSIXLY_CORRECT

如果设置了 `$POSIXLY_CORRECT`（即使是空值），默认的 `apropos` 搜索也将使用扩展正则表达式 (`-r`)。如今，这本身就是默认行为。

## 文件 (FILES)

`/usr/share/man/index.(bt|db|dir|pag)`

传统的全局索引数据库缓存。

`/var/cache/man/index.(bt|db|dir|pag)`

符合 FHS 标准的全局索引数据库缓存。

`/usr/share/man/../whatis`

传统的 `whatis` 文本数据库。

## 参见 (SEE ALSO)

`man(1)`, `whatis(1)`, `mandb(8)`

## 作者 (AUTHOR)

Wilf. (`G.Wilford@ee.surrey.ac.uk`). Fabrizio Polacco (`fpolacco@debian.org`).

Colin Watson (`cjwatson@debian.org`).

# 名称 (NAME)

`arch` - 打印机器硬件名称（与 `uname -m` 相同）

# Synopsis (SYNOPSIS)

`arch [OPTION]...`

# 描述 (DESCRIPTION)

打印机器架构。

- `-help`

显示此帮助并退出

- `-version`

输出版本信息并退出

# 作者 (AUTHOR)

由 David MacKenzie 和 Karel Zak 编写

# 报告错误 (REPORTING BUGS)

GNU coreutils 在线帮助: `<http://www.gnu.org/software/coreutils/>` 向 `<http://translationproject.org/team/>` 报告 `arch` 翻译错误。

# 版权 (COPYRIGHT)

Copyright © 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL 3 或更高 `<http://gnu.org/licenses/gpl.html>`。这是自由软件：你可以自由地更改和重新发布。在法律允许的范围内不提供任何保证。

# 参见 (SEE ALSO)

`uname(1)`, `uname(2)`

完整文档请访问：`<http://www.gnu.org/software/coreutils/arch>` 或通过本地信息查看：info ‘`(coreutils) arch invocation'`

# ARECORDMIDI

# 名称 (NAME)

`arecordmidi` - 记录标准 MIDI 文件 (Standard MIDI Files)

# Synopsis (SYNOPSIS)

```
arecordmidi -p client:port[...] [options] midfile
```

# 描述 (DESCRIPTION)

`arecordmidi` 是一个命令行工具，从一个或多个 ALSA 序列器端口记录标准 MIDI 文件。

停止录制请按 Ctrl+C。

# 选项 (OPTIONS)

- `-h`, `—help`

打印选项列表。

- `-V`, `—version`

打印当前版本。

- `-l`, `—list`

打印可能的输入端口列表。

- `-p`, `—port=client:port,...`

设置录制事件的序列器端口。

客户端可以通过其数字、名称或名称前缀指定。端口通过其数字指定；对于客户端的 0 端口，端口规范中的 `:0` 部分可以省略。

- `-b`, `—bpm=beats`

设置 MIDI 文件的音乐节奏，为每分钟拍数。默认值为 120 BPM。

- `-f`, `—fps=frames`

设置 SMPTE 分辨率，单位为每秒帧数。可能值为 24、25、29.97（针对 30 抽帧）和 30。

- `-t`, `—ticks=ticks`

设置 MIDI 文件中时间戳（ticks）的分辨率，单位为每拍刻（使用音乐节奏时）或每帧刻（使用 SMPTE 定时时）。

- `-s`, `—split-channels`

指定每个通道写入单独的轨道。

- `-m`, `--port=client:port`

设置客户端的序列器端口。

- `-i`, `—ticks=ticks`

设置 MIDI 文件的音乐节奏，单位为每分钟拍数。默认值为 120 BPM。

### 选项

- `--p port`

指定 TCP 端口号或 TCP 服务名称。

- `-s addr`

自动对给定的地址进行读取。

- `-d addr`

自动对给定的地址进行写入。

- `-v`

详细模式。

# 另请参

`aconnect(1)`, `pmidi(1)`

### 作者

Takashi Iwai `<tiwai@suse.de>`。

# ASN1PARSE

## 名称

`asn1parse` - ASN.1 解析工具

### 概要

`openssl asn1parse [-inform PEM|DER] [-in filename] [-out filename] [-noout] [-offset number] [-length number] [-i] [-oid filename] [-dump] [-dlimit num] [-strparse offset] [-genstr string] [-genconf file]`

### 描述

`asn1parse` 命令是一个诊断实用程序，可以解析 ASN.1 结构。它也可以用于从 ASN.1 格式的数据中提取数据。

### 选项

`-inform DERPEM`

输入格式。二进制格式和 DER（默认值）是 base64 编码的。

`-in filename`

输入文件，默认为标准输入。

`-out filename`

存放 DER 编码数据输出输出文件。如果不存在此选项，则不输出任何数据。这与 `-strparse` 选项结合使用最为有用。

`-noout`

不输出输入文件的解析版本。

`-offset number`

开始解析的起始偏移量，默认是文件开头。

`-length number`

要解析的字节数，默认持续到文件末尾。

`-i`

根据结构的“深度”对输出进行缩进。

`-oid filename`

一个包含额外对象标识符 (OID) 的文件。该文件的格式在下文的“注意”部分进行了描述。

`-dump`

以十六进制格式转储未知数据。

`-limit num`

类似于 `-dump`，但仅输出前 `num` 个字节。

`-strparse offset`

解析从偏移量开始的 ASN.1 对象的字节流（octets）。此选项可以多次使用，以“钻入”嵌套结构中。

`-genstr string`, `-genconf file`

根据字符串、文件或两者使用 `ASN_generate_nconf(3)` 格式生成编码后的数据。如果仅存在文件，则从默认节名 `asn1` 获取主体密钥（Subject Key）。编码后的数据将通过 ASN1 解析器并像来自文件一样打印出来，因此可以检查内容并使用 `out` 选项写入文件。

## 输出

输出通常包含如下所示行：

```
0:d=0 hl=4 l= 681 cons: SEQUENCE
```



```
229:d=3 hl=3 l= 141: BIT STRING 373:d=2 hl=3 l= 162 cons: cont [ 3 ]
376:d=3 hl=3 l= 159: SEQUENCE 379:d=4 hl=2 l= 29: SEQUENCE
381:d=5 hl=2 l= 3 prim: OBJECT :X509v3 Subject Key Identifier 386:d=5 hl=2
22: prime: OCTET STRING 410:d=4 hl=2 l= 112: SEQUENCE 412:d=5 hl=2 l=
3 prim: OBJECT :509v3 Authority Key Identifier 417:d=5 hl2=2 l= 15 prim:
OCTET STRING 524:d=4 hl2=2 l= 12 cons: SEQUENCE
```

此示例是自签名证书的一部分。每行以十进制表示的偏移量开头。`d=XX` 指定当前深度。在任何 `SET` 或 `SEQUENCE` 的作用范围内，深度会增加。`hl=XX` 给出当前类型的头部长度（标签和长度字节）。`l=XX` 给出内容字节的长度。

可以使用 `-i` 选项使输出更具可读性。

需要对 `ASN.1` 结构有一定的了解才能解释输出内容。内容：

在此示例中，偏移量 `229` 处的 `BIT STRING` 是证书公钥。其内容字节将包含公钥信息。可以使用 `-strparse 229` 选项进行检查，结果如下：

```
0:d=0 hl=3 l=137 cons: SEQUENCE 3:d=1 hl=3 l=129 prim: INTEGER
:E5D21EF1FC5D208EA7A2166C7AF6BDF 05969C6087DD70840F15AAAA5699FE
71F379F1D6A4B8E7D509AB68A4D94756 24B91D8CF55DB352015460C8EDE44EE8A41
89F7A8BE77D6CD3A9AF2696F48685CF58BF 0ED2FB24068058C7A947F52548DDF7E15E96B
385F86422BEA9064A35897135:d=1 l=3 prim: INTEGER:010081
```

# 注意

如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。

如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。如果 `OID` 不是 `OpenSSL` 内部表的一部分，它将以数字形式表示（例如 `1.2.3.4`）。传递给 `-oid` 选项的文件允许包含额外的 `OID`。该文件的格式在下文的“注意”部分进行了描述。

## 示例

解析 `PEM` 文件：

```
asn1parse -inform PEM
```

解析 `DER` 文件：

```
asn1parse -inform DER
```

将输出保存到文件：

```
asn1parse -in file -out output
```

解析特定偏移量：

```
asn1parse -in file -offset 100
```

解析特定长度：

```
asn1parse -in file -length 50
```

查看特定的 `OID`：

```
asn1parse -in file -oid oids.txt
```

### 选项

`-V`

将版本号打印到标准错误输出并成功退出。

`-q queue`

使用指定的队列。队列标识由单个字母组成；有效的标识范围从 `a` 到 `z` 以及 `A` 到 `Z`。`at` 的默认队列是 `q`，`batch` 的默认队列是 `b`。字母靠后的队列运行时的 `niceness`（优先级）越高。特殊队列 `=` 留给当前正在运行的作业。

如果将作业提交到由大写字母指定的队列，该作业将被处理为在提交时提交给了 `batch`。一旦时间到达，将适用关于平均负载的批处理规则。如果给 `atq` 指定了特定队列，它将只显示该队列中等待的作业。

`-m`

当作业完成后，即使没有输出，也会向用户发送邮件。

`-M`

永远不向用户发送邮件。

`-f file`

从文件而非标准输入读取作业。

`-t time`

在指定时间运行作业，格式为 `[[CC]YY]MMDDhhmm[.ss]`。

`-l`

是 `atq` 的别名。

`-r`

是 `atmrm` 的别名。

`-d`

是 `atmrm` 的别名。

`-b`

是 `batch` 的别名。

`-v`

在读取作业之前显示作业将执行的时间。

显示的时间格式为 `Thu Feb 20 14:50:00 1997`。

`-c`

将命令行上列出的作业 `cat` 打印到标准输出。

### 文件

```
/var/spool/at
/var/spool/at/spool
/proc/loadavg
/var/run/utmp
/etc/at.allow
/etc/at.deny
```

# 相关帮助



`at.allow(5)`, `at.deny(5)`, `atd(8)`, `cron(1)`, `nice(1)`, `sh(1)`, `umask(2)`。

## 缺陷

Linux 上 `batch` 的正确运行取决于 `/proc` 是否挂载了 `proc-type` 目录。

如果文件 `/var/run/utmp` 不可用或已损坏，或者在调用 `at` 时用户未登录，则邮件将发送到环境变量 `LOGNAME` 中找到的 `userid`。如果该变量未定义或为空，则假设为当前 `userid`。

目前实现的 `at` 和 `batch` 不适用于用户竞争资源的情况。如果你的站点存在这种情况，你可能需要考虑另一种批处理系统，如 `nqs`。

### 作者

`At` 大部分由 Thomas Koenig 编写，邮箱为 `ig25@rz.uni-karlsruhe.de`。

## 名称

`attr` - XFS 文件系统对象的扩展属性

# 语法

```
attr [ -LRSq ] -s attrname [ -V attrvalue ] pathname
attr [ -LRSq ] -g attrname pathname
attr [ -LRSq ] -r attrname pathname
attr [ -LRSq ] -l pathname
```

# 概述

扩展属性允许用户为 XFS 文件系统中的对象附加“名称:值”键值对。

本文描述了 `attr` 命令，该命令主要与同名的 IRIX 命令兼容。因此，它专门针对 XFS 文件系统的用户——对于与文件系统无关扩展属性操作，请参阅 `getfattr(1)` 和 `setfattr(1)` 文档。

扩展属性可存储有关文件的元数据。例如，`character-set=kanji` 可以告诉文档浏览器在显示该文档时使用日语字符集，而 `thumbnail=...` 可以为高分辨率图形图像提供低分辨率的预览。

在 XFS 文件系统中，属性名称长度可达 256 字节，以第一个 0 字节终止。其意图是使其成为可打印的 ASCII（或其他字符集）名称。值可以是最多 64KB 的任意二进制数据。

属性可以附加到所有类型的 XFS 节点上：普通文件、目录、符号链接、设备节点等。

XFS 为每个文件系统对象关联了两个不交叉的属性命名空间。它们是根空间（`root`）和用户空间（`user`）。根命名空间仅供超级用户访问，且仅通过向函数调用指定标记参数来实现。其他用户无法看到或修改根命名空间中的属性。用户命名空间受普通文件权限机制保护，因此文件所有者可以决定谁能够查看和/修改修改特定文件属性的值。

### 描述

`attr` 工具允许在 shell 脚本中操作与文件系统对象相关的扩展属性。

`attr` 可以执行四个主要操作：

## GET

`-g attrname` 选项告诉 `attr` 搜索指定的对象并打印（到 `stdout`）与属性名关联的值。使用 `-q` 标志时，`stdout` 将将恰好且仅包含该属性的值，适合直接存储到文件中或通过管道命令处理。

## LIST

`-l` 选项告诉 `attr` 列出与对象关联的所有属性名称，以及这些每个属性值的字节数。使用 `-q` 标志时，`stdout` 将是仅包含属性名的简单列表，每行一个，适合输入脚本。

## REMOVE

`-r attrname` 选项告诉 `attr` 如果属性存在，则从对象中删除指定名称的属性。成功完成后输出。

## SET/CREATE

`-s attrname` 选项告诉 `attr` 将对象的指定属性设置为从 `stdin` 读取的值。如果已存在该命名的属性，其值将被替换。使用 `-V attrvalue` 标志时，属性的值将被设置为 `attrvalue`。使用 `-q` 标志时，属性将被设置为 `attrvalue` 值，且 `stdin` 不会被读取。当 `-l` 选项给出且指定对象是符号链接时，操作其引用的对象。否则操作符号链接本身。当 `-R` 选项给出且进程具有相应权限时，在根命名空间操作而非用户命名空间。

`-S` 选项类似，它指定使用安全命名空间。在使用 `-q` 选项时，`attr` 将保持安静。它输出错误信息（到 `stderr`），但不会打印状态消息（到 `stdout`）。

## 注意事项

标准文件交换 `tar(1)` 和 `cpio(1)` 不存档扩展属性。

## 警告

IRIX 版本中的列表选项不支持。`getfattr` 提供了一种检索所有属性名的机制。

## 相关帮助

`getfattr(1)`, `setfattr(1)`, `attr_get(3)`, `attr_set(3)`, `attr_multi(3)`, `attr_remove(3)`, `attr(5)`, 以及 `xfsdump(8)`。

## 名称

`audit2allow` - 从拒绝的操作日志生成 SELinux 策略/audit规则

`audit2why` - 将 SELinux 审计消息翻译为拒绝访问的描述（`audit2allow -w`）

# 语法

```
audit2allow [options]
```

### 选项

+ `-a --all` 从审计和日志读取输入，冲突 `-i`
+ `-b --boot` 读取自启动以来的审计消息，冲突 `-i`
+ `-d --dmesg` 从 `/bin/dmesg` 的输出读取输入。注意审计运行时无法通过 `dmesg` 获取所有审计消息；请改用 `ausearch -m avc | audit2allow` 或 `-a`。
+ `-D --dontaudit` 生成 `audit` 规则（默认：`allow`）
+ `-h --help` 打印简短用法信息
+ `-i <inputfile> --input <inputfile>` 从 `<inputfile>` 读取输入
+ `-l --lastreload` 仅在策略加载后读取输入
+ `-m <modulename> --module <modulename>` 生成模块/需要输出 `<modulename>`
+ `-M --modulename` 生成可加载模块包，冲突 `-o`
+ `-p <policyfile> --policy <policyfile>` 用于分析的策略文件
+ `-o <outputfile> --output <outputfile>` 将输出附加到 `<outputfile>`
+ `-r --requires` 生成可加载模块的输出语法
+ `-N --noreference` 不生成引用策略，传统的允许规则。这是默认行为。
+ `-R --reference` 使用安装的宏生成引用策略。这尝试匹配接口拒绝。
+ `-w --why` 将 SELinux 审计消息翻译为拒绝访问的描述
+ `-v --verbose` 开启详细输出

### 描述

此工具扫描日志中在系统拒绝操作权限时记录的消息，并生成一段策略规则片段。如果这些规则被加载到策略中，可能会允许这些操作成功。然而，此工具仅生成类型强制（TE）允许规则。某些权限拒绝可能需要其他类型的策略更改，例如：为类型声明添加属性以满足现有约束条件、添加角色规则或修改约束条件。当原因不明确时，可以使用 `audit2why(8)` 工具来诊断原因。

在处理此工具的输出结果时必须小心，以确保被允许的操作不会构成安全威胁。通常，定义新的领域和/或类型，或者对结构进行更改以在狭窄范围内允许一组最优操作成功，要比盲目实施此工具推荐的更改要好。某些权限拒绝对应用程序并非致命的，在这种情况下，通过 `dont` 规则简单的抑制拒绝日志可能比使用 `allow` 规则更好。

## 示例

注意：这些示例适用于使用 `audit` 包的系统。如果你没有使用 `audit` 软件包，AVC 消息将位于 `/var/log/messages` 中。

### 作者

本手册页由 Manoj Srivastava <srivasta@debian.org> 为 Debian GNU/Linux 系统编写。由 Dan Walsh <dwalsh@redhat.com> 更新。

`audit2allow` 工具包含了多个人的贡献，包括 Justin R. Smith、Yuichi Nakamura 和 Dan Walsh。

## 名称

`gawk` - 模式扫描与处理语言

### 概要

```
gawk [ POSIX 或 GNU 风格选项 ] -f program-file [ — ] file ...
gawk [ POSIX 或 GNU 风格选项 ] [ — ] program-text file ...
```

### 描述

`Gawk` 是 GNU 项目对 `AWK` 语言的实现。它符合 POSIX 1003.1 标准中对语言的定义。该版本基于 Aho、Kernighan 和 Weinberg 所著的《The AWK Programming Language》中的描述。`Gawk` 提供了 Kernigh's `awk` 版本中的额外功能以及许多 GNU 特有的扩展。

命令行由用于 `awk` 自身的选项、AWK 程序正文（如果未通过 `-f` 或 `--file` 选项提供）以及要在 `ARGC` 和 `ARGV` 预定义 AWK 变量可用可用组成。

当使用 `--profile` 选项调用 `gawk` 时，它开始从程序的执行中收集性能统计数据。`Gawk` 在此模式下运行较慢，并在完成后自动在 `awkprof.out` 文件中生成执行分析。见下文 `--profile` 选项。



Gawk 还具有一个集成调试器。通过向命令行提供 `--debug` 选项可以启动交互式调试会。在这种执行模式下，`gawk` 加载 AWK 源代码并提示调试命令。`Gawk` 只能调试通过 `-f` 选项提供的 AWK 程序源。调试器的相关文档见 *GAWK: Effective AWK Programming*。

## 选项格式

`Gawk` 选项可以是传统的 POSIX 风格的单字母- 选项，也可以是 GNU 风格的长选项。POSIX 选项以单个 `-` 开头，而长选项以 `—` 开头。长选项既适用于 GNU 特有功能也适用于 POSIX 强制功能。

`Gawk` 特有的选项通常以长选项的形式使用。长选项的参数通过 `=` 号与选项连接（中间不留空格），或者可以在下一个命令行参数中提供。长选项可以缩写，只要缩写保持唯一即可。

此外，每个长选项都有一个对应的短选项，因此可以在 `#!` 可执行脚本中使用该选项的功能。

### 选项

`Gawk` 接受以下选项。标准选项列在前，随后是 `gawk` 扩展，按短选项的字母顺序排列。

- `-f program-file --file program-file` 从文件读取 AWK 程序源，而不是第一个命令行参数。可以使用多个 `-f`（或 `—file`）选项。
- `-F fs --field-separator fs` 使用 `fs` 作为输入字段分隔符（预定义变量 `FS` 的值）。
- `-v var=val --assign var=val` 在执行程序之前将 `val` 赋值给变量 `var`。此类变量在 AWK 的 `BEGIN` 规则可用。
- `-b --characters-as-bytes` 将所有输入视为单字节字符。换句话说，在尝试处理多字节字符时不要考虑任何区域信息。`--posix` 选项会覆盖此设置。
- `-c --traditional` 以兼容模式运行。在兼容模式下，`gawk` 的行为与 Brian Kernan's `awk` 完全相同；不识别任何 GNU 特有的扩展。更多信息请见 `EXTENSIONS`。
- `-C --copyright` 在标准输出上打印 GNU 版权信息的版本并成功退出。
- `-d[file] --dump-variables=[file]` 将全局变量的排序列表、类型和最终值打印到文件。如果没有提供文件，`gawk` 使用当前目录下名为 `awkvars.out` 的文件。拥有所有全局变量列表是查找程序中拼写错误的好方法。如果你有一个包含大量函数的大型程序，并且想确保你的函数没有无意中将本应局部的变量变为全局，你也会使用此选项（这在使用 `i`、`j` 等简单变量名时特别容易犯的错误）。
- `-D[file] --debug=[file]` 启用 awk 程序的调试。默认情况下，调试器从键盘（标准输入）交互式读取命令。可选的文件参数指定了一个包含命令列表的文件，供调试器非交互式地执行这些命令。
- `-e program-text --source program-text` 使用 `program-text` 作为 awk 程序源码。此选项允许库函数（通过 `-f` 和 `--file` 选项使用）与在命令行输入的源代码之间进行交叉混合。它主要用于中等到用于 shell 脚本的大型 AWK 程序。
- `-E file --exec` 与 `-f` 类似，但此选项是最后一个被处理的选项。这应该与 `#1` 脚本配合使用，特别是对于 CGI 应用，以避免从 URL 命令行出现选项或源代码 (!)。此选项会禁用命令行变量赋值。
- `-g --gen-pot` 扫描并解析 AWK 程序，并在标准输出上生成一个 GNU `.pot`（迁移对象模板）格式的文件，其中包含程序所有可本地字符串的条目。程序本身不会执行。有关 `.pot` 文件的更多信息，请参阅 GNU `gettext` 分发版。
- `-h --help` 在标准输出上打印可用选项的简短摘要。（根据 GNU 编码标准，这些选项会导致程序立即并成功退出。）
- `-i include-file --include-file` 加载 AWK 源代码库。这会使用 `AWPATH` 环境变量搜索该库。如果初始搜索失败，则在附加 `.awk` 后缀后进行再次尝试。该文件将仅加载一次（即消除重复项），且代码不构成主程序源码。
- `-lib --load` 加载共享库文件。这会使用 `AWKLIBPATH` 环境变量搜索该库。如果初始搜索失败，则在附加平台的默认共享库后进行再次尝试。预计库初始化程序命名为 `dl_load()`。
- `-L [value] --lint=value` 对于可疑或不可移植到其他 AWK 实现的结构提供警告。如果带有可选参数 `fatal`，lint 警告将变为致命错误。这可能非常极端，但它的使用将鼓励开发更整洁的 AWK 程序。带有可选参数 `invalid`，将发出关于实际无效内容的警告。（这尚未完全实现。）
- `-M --bignum` 强制对数字使用任意精度算术。如果 `gawk` 未被编译为使用 GNU MPFR 和 MP 库，则此选项无效。
- `-n --non-decimal-data` 识别输入数据中的八进制和十六进制值。请极其谨慎使用此选项！
- `-N --use-lc-numeric` 强制 `gawk` 在解析输入数据时使用区域的小数点字符。虽然 POSIX 标准要求此行为，且 `gawk` 在开启 `--posix` 时也会这样做，但默认是遵循传统行为并使用句号作为小数点，即使在这些区域中句号不是小数点字符。此选项覆盖了默认行为，但没有 `--posix` 选项那样完全严苛。
- `-o[file] --pretty-print=[file]` 将程序的格式化打印版本输出到文件。如果没有提供文件，`gawk` 将使用当前目录下的名为 `awkprof.out` 的文件。
- `--O --optimize` 在程序的内部表示上启用优化。目前，这包括简单的常量折叠和递归函数的尾调用消除。`gawk` 维护者希望随时间增加额外的优化。
- `-p[file] --profile=[prof=file]` 启动分析会话，并将分析数据发送到 `prof-file`。默认为 `awkprof.out`。分析文件在左边页包含程序中每个语句的执行计数以及每个用户定义函数的函数调用。
- `-P --posix` 开启兼容模式，带有以下额外限制：不识别 `\x` 转义序列。当 `FS` 设置为单个空格或换行时，只有空格和制表符作为字段分隔符。你不能在 `?` 和 `:` 之后延续行。关键字 `function` 的同义词 `func` 不被识别。运算符 `**` 和 `!=` 不能代替 `^` 和 `^=`。
- `-r --re-interval` 在正则表达式匹配中启用区间表达式（见下文“正则表达式”）。区间表达式在传统的 AWK 语言中并不可用。POSIX 标准增加了它们，使 `awk` 和 `egrep` 保持一致。它们默认启用，但此选项仍保留用于配合 `traditional`。
- `--S --sandbox` `Gawk` 以沙箱模式运行，禁用 `system()` 函数、使用 `getline` 的输入方向、`print` 和 `printf` 的输出方向以及动态扩展。命令执行（通过管道）也被禁用。这有效地阻止了脚本访问本地资源（命令行上指定的文件除外）。
- `--t --lint-old` 关于不可移植到原始版本 UNIX `awk` 的结构的警告。
- `--V --version` 打印此特定版本的信息，对于了解你系统当前的 `gawk` 版本是否与自由软件基金分发的版本保持更新有用。这在报告 bug 时也很有用。（根据 GNU 编码标准，这些选项会导致程序立即并成功退出。）
- `--` 标记选项的结束。这允许传递给 `awk` 程序本身的后续参数以 `--` 开头。这与大多数其他 POSIX 程序使用的参数解析保持一致性。

在兼容模式下，任何其他选项都被标记为无效，但在其他会被忽略。在正常操作下，只要提供了程序文本，未知选项将通过 `ARGV` 数组传递给 `awk` 程序进行处理。这对于通过 `#!` 可执行解释器机制运行 `awk` 程序特别有用。

为了 POSIX 兼容性，可以使用 `-W` 选项，后跟一个长选项名称。

## AWK 程序的执行

AWK 程序由一系列模式-动作语句和可选的函数定义组成。

```
@include "filename" @load "filename" { action statements }
function name(parameter list) { statements }
```

如果指定，`Gawk` 首先从程序文件(s)、`--source` 的参数或命令行上的第一个非参数项读取程序源码。`-f` 和 `--source` 选项可以在命令行上多次使用。`Gawk` 读取程序文本，就像所有的程序文件和命令行源代码已经连接在一起一样。这对于构建 `awk` 函数库非常有用，而无需将它们包含在每个使用这些函数的 `awk` 程序中。它还提供了将库函数与命令行程序混合的能力。

此外，以 `@include` 开头的行可以将其他源文件包含到你的程序中，使得库的使用更加简单。这等同于 `-i` 选项。

以 `@load` 开头的行可以将共享库加载到你的程序中。这等同于 `-l` 选项。



环境变量 `AWKPATH` 指定了查找源文件时使用的路径。`.:/usr/local/share/awk`。（实际目录取决于 gawk 的构建和安装方式。）如果此变量不存在，默认路径为空。如果传递给 `-f` 选项的文件名包含 `/` ，则不进行搜索。

环境变量 `AWKLIBPATH` 指定在使用 `-l` 选项查找源文件时使用的路径。如果此变量不存在，默认路径为 `/usr/local/lib/gawk`。（实际目录取决于 gawk 的构建和安装方式）。

Gawk 按以下顺序执行 awk 程序。首先，执行通过 `-v` 选项指定的所有变量赋值。接下来，gawk 将程序编译为内部形式。然后，gawk 执行 `BEGIN` 规则中的代码（如果有），并继续读取 `ARGV` 数组中命名的每个文件（直到 `ARGC`）。如果命令行没有命名文件，gawk 读取标准输入。

如果命令行上的文件名具有 `var=val` 形式，则被视为变量赋值。变量 `var` 将被赋值 `val`（这发生在任何 `BEGIN` 规则运行之后）。命令行变量赋值对于动态分配 awk 用于控制输入如何拆分为字段和记录的变量最有用。它对于控制是否需要对单个数据文件进行多次处理处理。

如果 `ARGV` 的特定元素为空，gawk 将跳过它。

对于每个输入文件，如果存在 `BEGINFILE` 规则，gawk 将执行关联代码。

在处理文件内容之前。同样，gawk 在处理文件后执行与 `ENFILE` 相关的代码。

对于输入中的每条记录，gawk 会测试其是否匹配 AWK 程序中的任何模式。对于记录匹配的每个模式，gawk 会执行相应的动作。模式是按照它们在程序中出现的顺序进行测试的。

最后，在所有输入完毕后，gawk 会执行 `END` 规则（如果有）中的代码。

## 命令行目录

根据 POSIX 标准，`awk` 命令行上命名的文件必须是文本文件。如果不是，则其行为是“未定义”的。大多数 awk 版本会将命令行上的目录视为致命错误。

从 gawk 4.0 版本开始，命令行上的目录会产生警告，但除此之外会被跳过。如果给出了 `--posix` 或 `--traditional` 选项之一，gawk 将恢复为将命令行上的目录视为致命错误。

## 变量、记录和字段

AWK 变量是动态的；它们在第一次被使用时创建。它们的值可以是浮点数、字符串，或者两者兼有，取决于如何使用它们。AWK 仅只有一维数组；多维数组可以通过模拟实现。gawk 提供了数组数组；见下文的 Arrays 部分。程序运行时会设置几个预定义变量；这些变量将在需要时进行描述并在下文中总结。

### 记录

通常情况下，记录由换行符分隔。你可以通过给内置变量 `RS` 赋值来控制记录的分隔方式。如果 `RS` 是任何单个字符，则用该字符分隔记录。否则，`RS` 是一个正则表达式。输入中匹配该正则表达式的部分将分隔记录。然而，在兼容模式下，仅使用其字符串值的第一个字符来分隔记录。如果将 `RS` 设置为空字符串，则由空行分隔记录。当 `RS` 设置为空字符串时，换行符始终作为字段分隔符，无论 `FS` 具有什么值。

### 字段

在读取输入时，gawk 使用 `FS` 变量的值作为字段分隔符将记录分为字段。如果 `FS` 是单个字符，则每个字符都成为一个独立的字段。否则，预期 `FS` 是一个完整的正则表达式。在 `FS` 为单个空格的特殊情况下，字段由连续的空格和/或制表符以及换行符分隔。（但请参见 POSIX COMPATIBILITY 部分，注意：`IGNORECASE` 的值（见下文）也会影响当 `FS` 为正则表达式时的字段分割方式，以及当 `RS` 为正则表达式时的记录分隔方式。

如果 `FIELDWIDTHS` 变量设置为由空格分隔的数字列表，则预期每个字段具有固定宽度，gawk 使用指定的宽度分割记录。此时 `FS` 的值被忽略。给 `FS` 或 `FPAT` 赋值新值将覆盖对 `FIELDWIDTHS` 的使用。

同样，`FPAT` 变量被设置为表示正则表达式的字符串，每个字段都由匹配该正则表达式的文本组成。在这种情况下，正则表达式描述的是字段，而不是分隔字段的文本。给 `FS` 或 `FIELDWIDTHS` 赋值新值将覆盖对 `FPAT` 的使用。

输入记录中的每个字段都可以通过其位置引用：`$1`、`$2` 等。`$0` 是整条记录。字段不需要通过常量引用：

```
n = 5
print $n
```

打印输入记录中的第五字段。

变量 `NF` 被设置为输入记录中的字段总数。

对不存在的字段（即 `$NF` 之后的字段）的引用会产生空字符串。然而，给不存在的字段赋值（例如 `$NF+2 = 5`）会增加 `NF` 的值，创建中间的字段并以空字符串作为其值，并导致 `$0` 的值重新计算，字段由 `OFS` 的值分隔。对负字段的引用会导致致命错误。递减 `NF` 会导致新值丢失，并重新计算 `$0` 的值，字段由 `OFS` 的值分隔。

给现有字段赋值会导致在引用 `$0` 时重新构建整条记录。同样，给 `$0` 赋值会导致记录被重新拆分，并为字段创建新值。

## 内置变量

gawk 的内置变量有：

### ARGC

命令行参数的数量（不包括给 gawk 的选项或程序源码）。

### ARGIND

当前正在处理的文件在 `ARGV` 中的索引。

### ARGV

命令行数组。该数组索引从 0 到 `ARGC - 1`。动态更改 `ARGV` 的内容可以控制用于数据的文件。

### BINMODE

在非 POSIX 系统上，指定文件 I/O 的“二进制”模式。数值 1、2 或 3 分别指定输入文件、输出文件或所有文件应使用二进制 I/O。字符串值 `r` 或 `w` 指定输入文件或输出文件应使用二进制 I/O。字符串值 `rw` 或 `wr` 指定所有文件应使用二进制 I/O。任何其他字符串被视为 `rw`，但会生成警告消息。

### CONVFMT

数字的转换格式，默认认为 `%.6g`。

### ENVIRON

一个包含当前环境值的数组。该数组由环境变量索引，每个元素是变量的值（例如 `ENVIRON["HOME"]` 可能是 `/home/arnold`）。更改此数组不会影响 gawk 通过重定向或 `function()` 产生的程序所看到的环境。

### ERRNO

如果在 `getline`、`read` 或 `close()` 期间发生错误，`ERRNO` 将包含该字符串。

### FIELDWIDTHS

由空格分隔的数字列表。设置时，gawk 解析输入为

### FILENAME

当前文件名。

### FNR

输入记录编号。

### FPAT

正则表达式。设置时，gawk 解析输入为

### FS

字段分隔符，默认值。

### FUNCTAB

以用户定义函数名为索引的数组。

### IGNORECASE

控制比较的大小敏感性。设置为 `false` 时区分大小写。

### LINT

提供有关运行程序的信息。

### NF

输入记录中的字段数。

### OFMT

数字的输出格式，默认认为 `%.6g`。

### OFS

输出分隔符，空格。

### ORS

输出分隔符，换行符。

### PREC

任意精度数的精度。

### PROFINFO

此数组的元素提供了运行程序的信息。在某些系统上，可能有：

### PROFINFO["egid"]

`getgid(2)` 系统调用的值。

### PROFINFO["strftime"]

`strftime()` 的格式字符串。

### PROFINFO["uid"]

`getuid(2)` 系统调用的值。

### PROFINFO["FS"]

`FS` 的值。

### PROFINFO["identifiers"]

一个以 gawk 知的所有标识符名称索引的子数组。元素的值是以下之一：

- array

  标识符是一个数组。

- builtin

  标识符是一个内置函数。

- extension

  标识符是一个通过 `@load` 或 `-l` 载的扩展。

- scalar

  标识符是一个标量。

- untyped

  标识符未类型（可以作为标量或数组，gawk 尚未知）。

- user

  标识符是一个用户函数。

### PROFINFO["gid"]

`getgid(2)` 系统调用的值。

### PROFINFO["pgrid"]

当前进程进程组 ID。

### PROFINFO["pid"]

当前进程的进程 ID。

### PROFINFO["ppid"]

当前进程的父进程 ID。

### PROFINFO["sorted_in"]

如果 `PROFINFO` 中存在此元素，其值控制在循环中遍历元素的顺序。支持的值有 `@ind_str_asc`、`@ind_num_asc`、`@val_type_asc`、`@val_str_asc`、`@val_num_asc`、`@ind_str_desc`、`@ind_num_desc`、`@val_type_desc`、`@val_str_desc`、`@val_num_desc` 和 `@unsorted`。该值也可以是



可以作为如下定义的比较函数的名称：

```
function cmp_func(i1, v1, v2)
```

其中 `i1` 和 `i2` 是索引，`v1` 和 `v2` 是两个比较元素对应的值。它应该返回一个小于、等于或大于 0 的数字，取决于数组元素如何进行排序。

`PROFINCI["input", "READ_TIMEOUT"]` 读取数据输入的最小时间（单位毫秒），其中 `input` 是重定向字符串或文件名。值为 0 或小于 0 表示不设置超时时间。`PROFINCI["mpfr_version"]` `gawk` 中用于任意精度数字的 GNU MPFR 库版本。如果 `gawk` 编译编译 MPFR 库，则该条目不存在。`PROFINCI["gmp_version"]` `gawk` 中支持任意精度数字的 GNU MPFR 库版本。如果 `gawk` 编译编译 MPFR 库，则该条目也不存在。

`PROFINCI["prec_max"]` GNU MPFR 库支持的任意精度浮点数的最大精度。如果 `gawk` 编译编译 MPFR 支持，则该条目不存在。`PROFINCI["prec_min"]` GNU MPFR 库允许的任意精度浮点数的最小精度。如果 `gawk` 编译编译 MPFR 支持，则该条目不存在。

`PROFINCI["api_major"]` 扩展 API 的版本。`PROFINCI["api_minor"]` 扩展 API 的次版本。如果没有加载动态扩展，则该条目不存在。`PROFINCI["version"]` `gawk` 的版本。

`ROUNDMODE` 用于任意精度算术的舍入模式，默认为 `N` (IEEE-754) 舍入偶数（`roundTiesToEven`）。接受的值为 `N` 或非舍入向零（`roundTiesTowardZero`），如果你的 GNU MPFR 库支持，可以是 `A` 或舍入向负（`roundTiesTowardNegative`），`Z` 或 `z` 表示舍入远离零（`roundTiesToAway`）。`RS` 输入记录分隔符，默认值。`RT` 终止符。`Gawk` 将 `RT` 设置为匹配 `RS` 指定字符或正则表达式的输入。`START` 是 `match()` 匹配到的第一个字符；如果没有匹配则为 0。（这意味着该字符从 1 开始）。`RLENGTH` 是 `match()` 匹配到的字符串长度；如果没有匹配则为 -1。用于分隔数组元素中多个下标的字符，默认为 `\034`。`SYMTAB` 是索引为程序中当前所有定义的变量和数组名称的数组。可以用于间接访问读取或写入变量的值：

```
foo = 5; SYMTAB["foo"] = 4; print foo # 输出 4
```

`isarray()` 函数可以用于测试 `SYMTAB` 中的元素是否为数组。你不能对 `SYMTAB` 数组使用 `delete` 语句。

`TEXTDOMAIN` 程序的领域域；用于查找程序字符串的本地化翻译。

# 数组

数组使用方括号（`[` 和 `]`）之间的表达式作为下标。如果该表达式是一个表达式列表（`expr, expr ...`），那么数组下标是每个表达式的（字符串）值的连接后的字符串，并用 `SUBSEP` 变量的值进行分隔。这种机制被用于模拟多维数组。例如：

```
i = "A"; j = "B"; k = "C"; x[i, j] = "hello, world"
```

将字符串 `hello, world` 分配给数组 `x` 的元素，该元素的索引为字符串 `A\034B\034C`。`awk` 中的所有数组都是关联数组，即通过字符串值进行索引。

当数组的索引由一个特定值组成时，需要使用特殊运算符：

```
if (val in array) print array[val]
```

如果数组有多个下标，请在 `array` 使用 `(i, j)`。

`in` 结构也可以用于 `for` 循环，以遍历数组的所有元素。然而，`(i, j) in array` 结构仅在测试中有效，而不适用于 `for` 循环。

可以使用 `delete` 语句从数组中删除元素。也可以通过指定不带下标的数组名来使用 `delete` 语句删除数组的整个内容。

`awk` 支持真正的多维数组。它并不要求数组像 C 或 C++ 那样是“矩形的”。例如：

```
a[1] = 5; a[2][1] = 6; a[2][2] = 7
```

注意：你可能需要告诉 `awk` 元素是一个子数组，以便在 `awk` 需要数组的地方（例如 `split()` 的第二个参数）使用它。你可以通过在子数组创建一个元素并使用 `delete` 语句将其删除来实现。

# 变量类型与转换

变量和字段可以是（浮点）数字、字符串或两者兼有。变量值的解释方式取决于其上下文。如果用于数值表达式，它将被视为数字；如果用作字符串，它将被视为字符串。

要强制将变量视为数字，请向其加 0；要强制将其视为字符串，请与空字符串连接。

未初始化的变量具有数值值 0 和字符串值 `""`（空字符串或零字符串）。

当必须将字符串转换为数字时，使用 `strtod(3)` 完成转换。使用 `CONVFMT` 的值作为 `sprintf(3)` 的格式字符串并将变量的数值作为参数可以将数字转换为字符串。然而，尽管 `awk` 中的所有数字都是浮点数，但整数值也会转换。

# 模式与动作

`AWK` 是一种面向行的语言。模式先在前面，然后是动作。动作语句包含在 `{ }` 中。模式可以缺失，动作也可以缺失，但当然，两者不能同时缺失。如果模式缺失，则对每条记录执行动作。缺失动作等同于

```
{ print }
```

这打印整个记录。注释以 `#` 字符开始，持续到行尾。空行可用于分隔语句。通常，语句以换行符结束，但以逗号结尾的行例外。以逗号结尾的语句会自动延续到下一行。在其他情况下，可以通过在行尾添加 `\` 来延续行。多条语句可以通过 `;` 分隔放在同一行内。这既适用于模式-动作对中的动作部分（通常情况），也适用于模式-动作语句本身。

## 模式

`AWK` 模式可以是以下之一：

```
BEGIN ENDFILE ENDFILE /regular expression/ relational expression pattern&& pattern || pattern ? pattern : pattern (pattern) ! pattern ! pattern2
```

`BEGIN` 和 `END` 是两种不测试输入的特殊模式。所有 `BEGIN` 模式的动作部分合并在一起就像写在一个 `BEGIN` 规则中。它们在读取任何输入之前执行。同样，所有的 `END` 规则合并并在耗尽输入（或执行 `exit` 语句）时执行。`BEGIN` 和 `END` 模式不能与其他模式与其他中结合。`BEGIN` 和 `END` 模式不能缺失动作部分。

`BEGINFILE` 和 `ENDFILE` 是额外的特殊模式，在读取每个命令行文件的第一个记录之前以及在读取每个文件的记录之后执行。在 `BEGINFILE` 中，如果文件打开成功，`ERRNO` 的值将为空字符串。否则，文件存在某些问题，代码应使用 `nextfile` 跳过它。如果没有这样做，`gawk` 对无法打开的文件产生通常的致命错误。

对于 `/regular expression/` 模式，关联语句将在每个匹配正则表达式的输入上执行。正则表达式与 `egrep(1)` 中的相同，并在下文中摘要。

关系表达式可以使用下面节中定义的任何运算符在 `actions`。它们通常测试某些字段是否匹配正则表达式。

`&&`、`|` 和 `!` 运算符分别是逻辑与（AND）、逻辑或（OR）和逻辑非（NOT），与 C 语言一样。它们像 C 语言一样支持短路求值，用于组合原始模式表达式。与大多数语言一样，可以使用括号来改变求值顺序。

`?` 运算符类似于 C 语言中的运算符。如果第一个模式为真，则用于测试的模式为第二个模式，否则为第三个模式。第二个和第三个模式中仅有一个会被求值。

表达式中的 `pattern1`, `pattern2` 被称为范围模式（range pattern）。它匹配所有从匹配 `pattern1` 的记录开始的输入记录，一直到匹配 `pattern2` 的记录结束（包含该记录本身）。它不会与任何其他类型的模式表达式结合。

### 正则表达式

正则表达式是在 `egrep` 中找到扩展类型。它们由以下字符组成：

- `+ c`: 匹配非元字符 `c`。
- `\c`: 匹配字面字符 `c`。
- `.`: 匹配包括换行符在内的任何字符。
- `^`: 匹配字符串的开头。
- `$`: 匹配字符串的结尾。
- `[abc...]`: 字符列表：匹配 `abc....` 中的任意一个字符。你可以通过连字符分隔它们来包含一个字符范围。
- `[^abc...]`: 否定字符列表：匹配 `abc....` 之外的任何字符。
- `r1|r2`: 择选择：匹配 `r1` 或 `r2`。
- `r1r2`: 拼接：先匹配 `r1`，再匹配 `r2`。
- `r+`: 匹配一个或多个 `r`。
- `*`: 匹配零或多个 `r`。
- `r?`: 匹配零或一个 `r`。
- `(r)`: 分组：匹配 `r`。



- `r{n}, r{n,}, r{n,m}`: 大括号内的一个或两个数字表示区间表达式。如果括号内有一个数字，则前面的正则表达式 `r` 重复 `n` 次。如果有两个用逗号分隔的数字，则 `r` 重复 `n` 到 `m` 次。如果数字后跟着逗号，则 `r` 至少重复 `n` 次。

- `+ \y`: 匹配单词开头或结尾的空字符串。

- `+ \B`: 匹配单词内部的空字符串。

- `+ \<`: 匹配单词开头的空字符串。

- `+ \>`: 匹配单词结尾的空字符串。

- `+ \s`: 匹配任何空白字符。

- `+ \S`: 匹配任何非空白字符。

- `+ \w`: 匹配任何单词字符（字母、数字或下划线）。

- `+ \W`: 匹配任何非单词字符。

- `^`: 匹配缓冲区（字符串）开头的空字符串。

- `$`: 匹配缓冲区（字符串）结尾的空字符串。

在字符串常量中有效的转义序列（见 `String Constants`）在正则表达式中同样有效。

字符类（Character classes）是 POSIX 标准引入的一种特性。字符类是描述具有特定属性的字符列表的特殊表示法，但实际字符本身随国家和/或字符集而异。关于什么是“字母”的概念在美国和法国是不同的。

字符类仅在正则表达式字符列表的大括号内有效。字符类由 `[:`、表示该类的关键字和 `:]` 组成。POSIX 标准定义的字符类有：

- `[:num:]`: 字母数字。

- `[:alpha:]`: 字母。

- `[:cntrl:]`: 控制字符。

- `[:digit:]`: 数字字符。

- `[:graph:]`: 既可打印又可见的字符。（空格是可打印的，但不可见，而 `a` 两者皆是。）

- `[:lower:]`: 小写字母。

- `[:print:]`: 可打印字符（不是控制字符的字符）。

- `[:punct:]`: 标点符号（不是字母、数字、控制字符或空格字符的字符）。

- `[:space:]`: 空白字符（例如空格、制表符和分页符等）。

- `[:upper:]`: 大写字母。

- `[:xdigit:]`: 十进制数字字符。

例如，在 POSIX 标准出现之前，要匹配字母数字，你必须写成 `[:A-Za-z0-9]`。如果你的字符集包含其他字母，它将无法匹配；如果你的字符排序方式与 ASCII 不同，它甚至可能无法匹配 ASCII 字母数字。使用 POSIX 字符类，你可以写成 `[:alnum:]`，无论你的字符集如何，它都能匹配其中的字母数字和数字字符。

字符列表中还可以出现两个额外的序列。这些适用于非 ASCII 字符集，这些字符集可能包含用多个字符表示的单个符号（称为排序元素 collating elements），以及多个在排序（或称排序）目的上等效的字符。（例如，在法语中，普通的“e”和带有重音符号的“è”）

## 排序符号

合并符号（Collapsing symbol）是位于 `[` 和 `]` 之间的多字符排序元素。例如，如果 `ch` 是一个排序元素，那么 `[[ch]]` 是匹配该合并元素的正表达式，而 `[ch]` 是匹配 `c` 或 `h` 的正则表达式。

## 等价类

等等价类（Equivalence class）是等效字符列表的特定区域名称。名称包含在 `[= =]` 中。例如，名称 `e` 可能表示所有的“e”、“é”和“è”。在这种情况下，`[[e =]]` 是匹配 e、é 或 è 中任意一个的正则表达式。

这些特性在非英语区域非常有价值。`gawk` 使用的库函数在正则表达式匹配方面目前仅识别 POSIX 字符类；不支持排序符号或等价类。

`\y`、`\b`、`\<`、`\>`、`\s`、`\w` 和 `\W` 是 `gawk` 特有的。

各种命令行选项控制 `gawk` 如何解释正则表达式中的字符。

### 选项

- 在默认情况下，`gawk` 提供所有 POSIX 正则表达式以及上述 GNU 运算符。

- `-posix`: 仅支持 POSIX 正则表达式，不支持 GNU 运算符（例如 `w`）。

- `-traditional`: 使用传统的 `awk` 正则表达式。不支持 GNU 运算符，由八进制和十六进制转义序列描述视为字面量，即使它们代表正则表达式元字符。

- `-re-interval`: 即使提供了 `-traditional`，也允许在正则表达式中使用区间表达式。

## 动作

动作语句包含在大括号 `{ }` 中。动作语句由大多数语言中的赋值、条件和循环语句组成。

## 运算符

`awk` 中的运算符按优先级降序排序如下：

- `(...)`: 分组

- `$n`: 字段引用。

- `++ --n`: 递增和减少，包括前缀和后缀。

- `^n`: 幂（也可以使用 `**`，`**=` 用于赋值运算符）。

- `+ - !`: 一元加、一元减和逻辑非。

- `* / %`: 乘法、除法和取模。

- `+ -`: 加和减。

- 空格: 字符串拼接。

- `&`: `getline`、`print` 和 `printf` 的管道输入输出。

- `< > == !=`: 关系运算符。

- `~ !`: 正则表达式匹配、否定匹配。注意：不要在 `~` 的左侧使用常量正则表达式 `/foo/`。仅在右侧使用一个。表达式 `(/foo/) ~ exp` 等同于 `(($0 ~ /foo/) exp)`。这通常你想要的。

- `in`: 数组成员关系。

- `&`: 逻辑与。

- `?:`: C 条件表达式。形式为 `expr1 ? expr2 : expr3`。如果 `expr1` 为真，表达式的值为 `expr2`，否则为 `expr3`。只有 `expr2` 和 `expr3` 其中之一会被求值。

- `= += - *= /= %= ^= \=: 赋值。绝对赋值（`var = value`）和运算符赋值（其他形式）均受支持。

输入/输出语句如下：

`close(file [, ,how])`

关闭文件、管道或协进程。可选的 `how` 参数仅应在关闭指向协进程的双向管道的某一端时使用。它必须是一个字符串值，可以是 `to` 或 `from`。

`getline`

将 `$0` 设置为下一个输入记录；设置 `NF`, `NR`, `FNR`, `RT`。

`getline <file`

将 `$0` 设置为文件的下一记录；设置 `NF`, `RT`。

`getline var`

将 `var` 设置为下一个输入记录；设置 `NR`, `FNR`, `RT`。

`getline var <file`

将 `var` 设置为文件的下一记录，设置 `RT`。

`command | getline [var]`

运行命令并将输出管道到 `$0` 或 `var` 中（如上所示），并设置 `RT`。`|` 是管道分隔符。

`command & getline [var]`

作为协进程运行命令，并将输出管道到 `$0` 或 `var` 中（如上所示），并设置 `RT`。协进程是 `gawk` 的扩展。（`command` 也可以是一个 socket。详见下文的“特殊文件名”小节。）

`next`

停止处理当前记录。读取下一个输入记录，并从 `awk` 程序中的第一个模式开始处理。到达输入数据的末尾时，`awk` 会执行任何 `END` 规则。

`nextfile`

停止处理当前文件。下一个输入记录来自下一个输入文件。`FILENAME` 和 `ARGIND` 会更新，`FNR` 重置为 `1`，并从 `awk` 程序中的第一个模式开始处理。到达输入数据的末尾时，`awk` 会执行任何 `END` 规则。

`print`

打印当前记录。输出以 `ORS` 的值结束。

`print expr-list`

打印表达式。每个表达式之间用 `OFS` 的值分隔。输出记录以 `ORS` 的值结束。

`print expr-list >file`

在文件中打印表达式。每个表达式之间用 `OFS` 的值分隔。输出记录以 `ORS` 的值结束。

`printf fmt, expr-list`

格式化并打印。详见下文的“printf 语句”。

`printf fmt, expr-list >file`

在文件中格式化并打印。

`system(cmd-line)`

执行命令 `cmd-line`，并返回退出状态。（这在非 POSIX 系统上可能不可。）

## flush{file}

刷新与打开的输出文件或管道文件相关的所有缓冲区。如果 `file` 缺失或为空字符串，则刷新所有打开的输出文件和管道。

`print` 和 `printf` 允许额外的输出重定向。

- `print ... >> file`

将输出追加到文件。

- `print ... | command`

写入管道。

- `print ... &command`

将数据发送到协进程或 socket。（另，请参见下文的“特殊文件名”小节。）

`getline` 在成功时返回 `1`，在文件末尾时返回 `0`，在错误时返回 `-1`。发生错误时，`ERRNO` 被设置为描述该问题的字符串。



> 注意：打开双向 socket 失败会导致返回给调用函数的非致命错误。如果在循环中使用管道、协进程或 socket 进行 `getline`，或通过 `print` 或 `printf` 操作，你必须使用 `close()` 创建命令或 socket 的新实例。`awk` 在它们返回 EOF 时不会自动关闭管道、socket 或协进程。

## printf 语句

`awk` 版本的 `printf` 语句和 `sprintf()` 函数（见下文）接受以下转换规范格式：

- `%c`

单个字符。如果用于 `%c` 的参数是数值，则将其视为字符并打印。否则，假设参数是字符串，并打印该字符串的第一个字符。

- `%d`, `%i`

十进制数字（整数部分）。

- `%e`, `%E`

格式为 `[-]d.ddddde[+-dd]` 的浮点数。`%E` 格式使用 E 代替 e。

- `%f`, `%F`

格式为 `[-]d.ddddddd` 的浮点数。如果系统支持，`%F` 也可用。这类似于 `%f`，但使用大写字母表示特殊的“非数字”和“无穷”值。如果 `%F` 不可用，`awk` 使用 `%f`。

- `%g`, `%G`

使用 `%e` 或 `%f` 转换，以较短者为主，并抑制不显著的零。`%G` 格式使用 E 代替 e。

- `%0`

无符号数字（也是整数）。

- `%u`

未指定的十进制数字（同样是整数）。

- `%s`

字符字符串。

- `%X`

未赋值的十六进制数（整数）。`%X` 格式使用 ABCDEF 代替 abcdef。

- `#`

单个字符；不转换任何参数。

- `count$`

在格式化点使用第 `count` 个参数。这被称为位置指定符，主要用于格式化字符串的翻译版本，而不是 `gawk` 扩展的原始文本。

- `space`

表达式应在其字段内左对齐。对于数值转换，在正值前加空格，在负值前加减号。

- `+`

符号，用在宽度修饰符（见下文）之前，表示始终为数值转换提供符号，即使格式化的数据为正数。这会覆盖符号设置。

- `n`

对某些控制字母使用“替代形式”。对于 `%o`，提供前导零。对于 `%x` 和 `%X`，为非零结果提供前导 0。对于 `%e`、`%f` 和 `%F`，结果始终包含小数点。对于 `%g` 和 `%G`，不会从结果中移除尾零。

- `0`

数字 0 充当标志，表示输出应该用零而不是而不是填充。这仅适用于数值格式。该标志仅在字段宽度大于值时起作用。

- `width`

字段应填充到此宽度。使用 0 标志时，将用零填充。

- `prec`

指定打印时使用的精度数字。对于 `%e`、`%E` 和 `%F` 格式，这指定了要在小数点右侧打印位数。支持 ISO printf 程的动态宽度和精度能力。用 `*` 代替宽度或精度会导致其值从 `printf` 或 `sprintf()` 的参数列表中取值。这需要正确的本地化支持。

## 特殊文件名

当通过 `print` 重定向到文件、通过 `sprintf` 输出到文件或通过 `getline` 读取文件时，`awk` 识别某些文件描述符。这些文件名允许在命令行中使用文件描述符来访问从 `awk` 的父进程继承的文件描述符。这些文件名是：

- `/dev/stdin`

标准输入。

- `/dev/stdout`

标准输出。

- `/dev/stderr`

错误输出。

- `/fd/n`

与文件描述符 `n` 关联的文件。这些特别用于错误消息。例如：

```
print "You it!" > "/dev/stderr"
```

而你本本可以使用：

```
print "You it!" | "cat 2"
```

使用 `|` 协进程运算符创建 TCP/IP 连接的特殊文件名：

- `/inet/tcp/port/rhost/port`

- `/inet4/tcp/port/rhost/port`

- `/inet6/tcp/port/rhost/port` 使用端口 0 让系统选择端口。使用 `/inet4` 强制使用 IPv4 连接，使用 `/inet6` 强制使用 IPv6 连接。普通的 `/inet` 使用系统默认值（通常是 IPv4）。

- `/inet/udp/port/rhost/port`

- `/inet4/udp/lport/rhost/port`

- `/inet6/udp/lport/rhost/port` ，但使用 UDP/IP 代替 TCP/IP。

## 数字函数

`awk` 有内置数学函数：

- `atan2(y, x)`

返回 `y/x` 的反正角，单位为弧度。

- `cos(expr)`

返回 `expr` 的余弦，单位为弧度。

- `exp(expr)`

指数函数。

- `int(expr)`

截取整数。

- `log(expr)`

自然对数函数。

- `rand()`

返回 0 到 1 之间的随机数 N，使得 0 <= N < 1。

- `sin(expr)`

返回 `expr` 的正弦，单位为弧度。

- `sqrt(expr)`

返回 `expr` 的平方根。

- `rand(expr)`

使用 `expr` 作为随机数生成器的新种子。如果没有提供 `expr`，则使用当天时间。返回随机数生成器的之前的种子。

## 字符串函数

`gawk` 有内置字符串函数：

- `asort(s [, d [, how ])`

使用 `gawk` 普通比较规则返回数组 `s` 中的元素数量，并将排序后的值的索引替换为从 1 开始的顺序索引。如果指定了最优目标数组 `d`，先将 `s` 复制到 `d`，然后排序 `d`，保持源数组的索引不变。可选的字符串 `how` 控制方向和比较模式。`how` 的有效值是 `PROCINFO["sorted_in"]` 中有效的任何字符串。它也可以是 `PROCINFO["sorted_in"]` 中描述的用户定义比较函数的名称。

- `asorti(s [, d [, how ])`

返回源数组 `s` 中的元素个数。其行为与 `asort()` 相同，不同之处在于使用数组索引排序，而不是数组值。完成后，数组将按数字索引，其值是原始索引的值。原始值将丢失；如果你想保留原始值，请提供第二个数组。可选字符串 `h` 的用途如 `asort()` 中描述的所示。

```
gensub(r, s, h, [t])
```

在目标字符串 `t` 中搜索正则表达式 `r` 的匹配项。如果 `h` 是以 `g` 或 `G` 开头的字符串，则将所有 `r` 的匹配项替换为 `s`。否则，`h` 是一个数字，表示要替换 `r` 的哪部分。如果未提供 `t`，则使用 `s0`。在替换字符串 `t` 中，序列 `vn`（其中 `n` 是 1 到 9 的数字）可用于指示哪个字符串匹配了第 n 个括号子表达式。序列 `v0` 代表原始匹配文本，`&` 也是如此。与 `sub()` 和 `gsub()` 不同，修改后的字符串作为函数的返回值返回，目标字符串不会被改变。

```
gensub(r, s, [t])
```

对于字符串 `t` 中每个匹配正则表达式 `r` 的项，替换为字符串 `s`，并返回替换次数。如果未提供 `t`，则使用 `s0`。替换文本中的 `&` 被替换为实际匹配的文本。使用 `\&` 获取字面量 `&`。（必须类型化为 `\&`；关于 `sub()`、`gsub()` 和 `gensub()` 替换文本中 `&` 和反斜杠规则的更详细讨论，请参考 GAWK: Effective AWK Programming）

```
index(s, t)
```

返回字符串 `t` 在字符串 `s` 中的索引，如果 `t` 不存在则返回 0（这意味着字符索引从 1 开始）。使用正则表达式常量作为 `t` 是致命错误。

```
length(s)
```

返回字符串 `s` 的长度，如果未提供 `s`，则返回 `s` 的长度。作为一种非标准扩展，当带有数组参数时，`length()` 返回数组中的元素个数。

```
match(s, r, [a])
```

返回正则表达式 `r` 在 `s` 中出现的位置，如果 `r` 不存在则返回 0，并设置 `RSTART` 和 `RLENGTH` 的值。注意，顺序参数与 `~` 运算符相同：`str ~ re`。如果提供了 `a`，则清空 `a` 并在元素 1 到 `n` 中填充 `s` 中与 `r` 对应括号子表达式匹配的部分。`a` 的第 0 个元素包含由整个正则表达式 `r` 匹配的 `s` 部分。下表 `a[n,"start"]` 和 `a[n,"length"]` 分别提供每个匹配子字符串在字符串中的起始索引和长度。

```
patsplit(s, a, [r, t seps])
```

根据正则表达式 `r` 将字符串 `s` 分分为数组 `a` 和分隔符 `seps`，并字段个数。元素值是 `s` 中匹配 `r` 的部分。`seps[i]` 的值是出现在 `a[i+1]` 之前的分隔符。如果省略 `r`，则使用 `FPAT`。数组 `a` 和 `seps` 会被清空。分割行为与上述描述的使用 `FPAT` 的分割完全一致。

```
split(s, a, r, seps )
```



根据正则表达式 `r` 将字符串 `s` 分分为数组 `a` 和分隔符数组 `seps`，并返回个数。如果省略 `r`，则使用 `FS`。首先清空数组 `a` 和 `seps`。`seps[i]` 是 `a[i]` 和 `a[i+1]` 之间由 `r` 分隔的字段。如果 `r` 是单个空格，则 `s` 中的引导空格进入元素 `seps[0]`，尾随空格进入元素 `seps[n]`，其中 `n` 是 `split(s, a, r, seps)` 的返回值。分割行为与上述描述的字段分割完全一致。

``` 
sprintf(fmt, expr-list)
```

根据 `fmt` 打印 `expr-list`，并返回生成的字符串。

```
strtonum(str)
```

检查 `str` 并返回其数值。如果 `str` 以 0 开头，则将其视为八进制数。以 0X 开头，则将其视为十六进制数。否则，假设它是十进制数。

```
sub(r, s, i)
```

类似于 `gsub()`，但仅替换第一个匹配的子字符串。

```
substr(s, i, n)
```

返回 `s` 中从 `i` 开始的 `n` 个字符的子字符串。如果省略 `n`，使用 `s` 的剩余部分。

```
tolower(str)
```

返回字符串 `str` 的拷贝，将 `str` 中所有大写字母转换为其对应的小写字母。非字母字符保持不变。

```
toupper(str)
```

返回字符串 `str` 的拷贝，将 `str` 中所有小写字母转换为其对应的大写字母。非字母字符保持不变。

Gawk 是感知多字节的。这意味着 `index()`、`length()`、`substr()` 和 `match()` 都是以字符为单位工作的，而不是字节。

# 时间函数

由于 awk 程序的主要用途之一是处理包含时间戳信息的日志文件，gawk 提供了以下函数来获取时间戳并对其进行格式化。

```
mktime(datespec)
```

将 `datespec` 转换为与 `system()` 返回相同的格式并返回结果。`datespec` 是格式为 `YYYY MM DD HH MM SS[DST]` 的字符串。字符串的内容是六或七个数字，分别代表完整年份、1 到 12 的月份、1 到 31 的日期、0 到 23 的小时、分钟。

```
strftime(format, timestamp, [utc])
```

根据 `format` 格式化 `timestamp`。如果 `utc` 存在且非零，则结果为 UTC，否则结果为本地时间。默认域是 `TEXTDOMAIN`。

```
system()
```

返回当前时间（秒数）。

# 位运算

Gawk 提供了以下位运算函数。它们通过将双精度值转换为无整数进行操作，然后将结果转换回浮点数。这些：

```
and(v1, v2, ...])
```

返回列表中提供的值的位与逻辑结果。至少有两个参数。

```
compl(val)
```

返回 `val` 的位取反。

```
lshift(val, count)
```

返回 `val` 左移位的值。

```
or(v1, v2, ...])
```

返回列表中提供的值的位或逻辑结果。至少有两个参数。

```
rshift(val, count)
```

返回 `val` 右移位的值。

```
xor(v1, v2, ...])
```

返回列表中提供的值的位异或逻辑结果。至少有两个参数。

# 类型函数

以下函数用于多维数组。

```
isArray(x)
```

如果 `x` 是数组则返回真，否则返回假。

# 国际化函数

以下函数可在 AWK 程序中运行时翻译字符串。更多细节请参见 GAWK: Effective AWK Programming。

```
match(s, r, [a])
```

返回正则表达式 `r` 在 `s` 中出现的位置，如果 `r` 不存在则返回 0，并设置 `RSTART` 和 `RLENGTH` 的值。注意，顺序参数与 `~` 运算符相同：`str ~ re`。如果提供了 `a`，则清空 `a` 并在元素 1 到 `n` 中填充 `s` 中与 `r` 对应括号子表达式匹配的部分。`a` 的第 0 个元素包含由整个正则表达式 `r` 匹配的 `s` 部分。下标 `a[n,"start"]` 和 `a[n,"length"]` 分别提供每个匹配子字符串在字符串中的起始索引和长度。

```
patsplit(s, a, [r, t seps])
```

根据正则表达式 `r` 将字符串 `s` 分分为数组 `a` 和分隔符 `seps`，并返回字段个数。元素值是 `s` 中匹配 `r` 的部分。`seps[i]` 的值是出现在 `a[i+1]` 之前的分隔符。如果省略 `r`，则使用 `FPAT`。数组 `a` 和 `seps` 会被清空。分割行为与上述描述的使用 `FPAT` 的分割完全一致。

```
split(s, a, r, seps )
```

根据正则表达式 `r` 将字符串 `s` 分分为数组 `a` 和分隔符数组 `seps`，并返回字段个数。如果省略 `r`，则使用 `FS`。首先清空数组 `a` 和 `seps`。`seps[i]` 是 `a[i]` 和 `a[i+1]` 之间由 `r` 分隔的字段。如果 `r` 是单个空格，则 `s` 中的引导空格进入元素 `seps[0]`，尾随空格进入元素 `seps[n]`，其中 `n` 是 `split(s, a, r, seps)` 的返回值。分割行为与上述描述的字段分割完全一致。

## 用户定义函数

AWK 中的函数定义如下：

```awk
function name(parameter list) { statements }
```

函数在从模式（patterns）或动作（actions）中的表达式内部被调用时执行。函数调用中提供的实际参数用于实例化函数中声明的形式参数。数组通过引用传递，而其他变量则通过值传递。

由于函数最初并不是 awk 语言的一部分，因此局部变量的提供机制相当拙劣；它们被声明为参数列表中的额外参数。惯俗做法是通过在参数列表中使用额外的空格将局部变量与实际参数隔开。例如：

```awk
function(p, q, a, b) # a 和 b 为局部 { ... } /abc/ { ... ; f(2) ; ... }
```

函数调用中的左括号必须紧跟在函数名后面，中间不能有任何空白符。这避免了与连接操作符的语法歧义。此限制不适用于上述列出的内置函数。

函数可以相互调用并进行递归。用作局部变量函数参数在函数调用时被初始化为空字符串（null）和数字 0。

使用 `return expr` 从函数返回一个值。如果没有提供值，或者函数通过“掉落”末尾返回，则返回值未定义。

作为 gawk 的扩展，函数可以被间接调用。要实现这一点，可以将要调用的函数名作为字符串赋值给变量。然后像使用函数名一样使用该变量，并加上 @ 前缀，如下所示：

```awk
function myfunc() { print "myfunc" ... } { ... the_func = "myfunc"@the_func() # 通过 the_func 调用 myfunc ... }
```

在版本 4.1.2 中，此功能适用于用户定义函数、内置函数和扩展函数。

如果提供了 `--lint` 参数，gawk 会在解析时对未定义的调用进行警告，而不是在运行时。在运行时调用未定义的函数是致命错误。

单词 `func` 可以代替 `function`，尽管它已弃用。

你可以使用 `@load` 语句向运行中的 gawk 解释器动态地添加新的内置函数。详细细节超出了本手册的范围；请参见《GAWK: Effective AWK Programming》。

## 信号

gawk 性能分析器接受两个信号。`SIGUSR1` 会导致它将分析概要和函数调用栈转储到概要文件（该文件可以是 awkprof.out 或通过 `--profile` 指定的任何文件）。然后它继续运行。`SIGHUP` 会导致 gawk 转储分析概要和函数调用栈然后退出。

## 国际化

字符串常量是包含在双引号中的字符序列。在非英语环境中，可以将 awk 程序中的字符串标记为需要翻译成本地自然语言。此类字符串在 awk 程序中用前导下划线（""）标记。例如，

```bash
gawk 'BEGIN { print "hello, world" }'
```

始终打印 hello, world。但是，

```bash
gawk 'BEGIN { print _"hello, world" }'
```

在法国可能会打印 bonjour, monde。

制作和运行可本地化的 awk 程序涉及几个步骤：

- 添加一个 BEGIN 动作为 `TEXTDOMAIN` 变量赋值，以将文本域设置为与你的程序相关的名称：

  `BEGIN { TEXTDOMAIN = "myprog" }`

  这允许 gawk 找到与你的程序相关的 `.gmo` 文件。没有这一步，gawk 将使用 messages 文本域，该域可能不包含你程序的翻译。



- 为所有应该翻译的字符串加上前导下划线。

- 如果必要，在程序中适当使用 `dcgettext()` 和/或 `bindtextdomain()` 函数。

- 运行 `gawk --gen-pot -f myprog.awk > myprog.pot` 为你的程序生成 `.pot` 文件。

- 提供相应的翻译，并编译并安装相应的 `.gmo` 文件。

国际化功能在《GAWK: Effective AWK Programming》中有详细描述。

## POSIX 兼容性

`gawk` 的主要目标之一是与 POSIX 标准以及 Brian Kernighan 的 `awk` 的最新版本兼容。为此，`gawk` 整合了以下用户可见的功能，这些功能在 `awk` 书中没有描述，但是 Brian Kernighan 版本 `awk` 的一部分，也是 POSIX 标准的一部分。

书中指出，当 `awk` 原本会将参数作为文件打开时会发生命令行变量赋值，这是在 `BEGIN` 规则执行之后。然而，在早期的实现中，当这种赋值出现在任何文件名之前，赋值会在 `BEGIN` 规则运行之前发生。当 `awk` 改变以匹配其文档时，增加了 `-v` 选项在程序执行前分配变量，以适应依赖旧行为的应用程序。（此功能已由贝尔实验室和 GNU 开发者达成共识。）

在处理参数时，`gawk` 使用特殊选项 `"--"` 来指示参数的结束。在兼容模式下，它会警告但忽略未定义的选项。在正常操作下，此类参数会被传递给 `awk` 程序进行处理。

`awk` 书没有定义 `rand()` 的返回值。POSIX 标准要求它返回所使用的种子，以便跟踪随机数序列。因此，`gawk` 中的 `rand()` 也会返回其当前种子。

其他新功能还有：使用多个 `-f` 选项（来自 MKS `awk`）；`ENV` 数组；`\a` 和 `\w` 转义序列（最初在 `gawk` 中完成并回馈给贝尔实验室版本）；`tolower()` 和 `toupper()` 内置函数（来自贝尔实验室版本）；以及 `printf` 中的 ISO 格式规范。

## 历史特性

`gawk` 支持一个 `awk` 特性：

```awk
a = length($0)
```

等同于

```awk
a = length()
```

这种做法并不符合习惯

## GNU 扩展

`gawk` 有许多对 POSIX 的扩展。它们在本节中描述：

- 包含文件的机制（`gawk` 的包含机制）。

- 动态添加用 C 编写的方法（`gawk` 的加载机制）。

- `\` 转义序列（使用 `--posix` 时）。

- `AWK` 中的进制和十六进制常量。

- `ARGIND`, `BINMODE`, `ERNO`, `LINT`, `RT` 和 `TEXTDOMAIN` 变量不是特殊的。

- `IGNORECASE` 变量及其副作用。

- `FIELDWIDTH` 变量和固定宽度字段分割。

- 基于字段值的 `FPAT` 变量。

- `PROCINFO` 数组。

- 将 `RS` 作为正则表达式。

- 不识别重定向的特殊文件名。

- 创建协进程的 `|` 运算符。

- `BEGINFILE` 和 `ENDFILE` 特殊模式可用。

- 使用空字符串作为 `FS` 的值来分割单个字符，以及 `split()` 的第三个参数。

- 用于接收分隔符文本的 `split()` 可选第四参数。

- `close()` 函数的可选第二个参数。

- `match()` 函数的可选第三个参数。

- `printf` 和 `sprintf()` 中使用位置标识符。

- 向 `length()` 传递任何参数。

- `psplit()`、`rshift()`、`strftime()`、`stratum()` 和 `xor()` 函数。

- 可本地化字符串。

`awk` 书没有返回 `close()` 函数的返回值。`gawk` 的 `close()` 在关闭输出管道或文件时，分别返回 `close(3)` 或 `pclose(3)` 的值。在关闭输入管道时，返回进程的退出状态。如果命名的文件、管道或协进程未通过重定向打开，则返回值为 `-1`。

当使用传统选项调用 `gawk` 时，如果 `fs` 参数是 `-F` 选项 `"t"`，则 `FS` 被设置为制表符。注意输入 `gawk -Ft` 只是导致 shell 引用了 `"t"`，并没有将 `"\t"` 传递给 `-F` 选项。由于这是一个

特殊情况

## 环境变量

`AWKPATH` 环境变量可以提供一个目录列表，`*gawk*` 会在这些目录下搜索通过 `-f`、`--file`、`-i` 和 `--include` 选项指定的文件。如果初始搜索失败，则会在文件名后添加 `.awk` 再次进行搜索。

`AWKLIBPATH` 环境变量可以提供一个目录列表，`*gawk*` 会在这些目录下搜索通过 `-l` 和 `--load` 选项指定的文件。

`GAWK_READ_TIMEOUT` 环境变量可以指定从终端、管道或包括 socket 在内的双向通信读取输入的超时时间（单位为毫秒）。

对于通过 socket 连接远程主机，`GAWK_SOCK_RETRIES` 控制重试次数，`GAWK_MSEC_SLEEP` 控制重试之间的间隔。在不支持 `usleep(3)` 的系统上，该值将向上取整为整数秒。

如果环境中存在 `POSIXLY_CORRECT`，则 `*gawk*` 的行为将与在命令行中指定了 `posix` 完全一样。如果指定了 `--lint`，`*gawk*` 会发出此类的警告信息。

## 退出状态

如果 `exit` 语句带有值使用，则 `gawk` 以其给定的数值退出。

否则，如果执行过程中没有出现问题，`gawk` 以 C 常量 `EXIT_SUCCESS` 的值退出。这通常是 `0`。

如果发生错误，`gawk` 以 C 常量 `EXIT_FAILURE` 的值退出。这通常是 `1`。

如果 `gawk` 因为致命错误退出，则退出状态为 `2`。在非 POSIX 系统上，该值可能被映射到 `EXIT_FAILURE`。

## 版本信息

本帮助页文档记录了 `gawk 4.1` 版本。

### 作者

`UNIX awk` 的原始版本由贝尔实验室的 Alfred Aho、Peter Weinberger 和 Brian Kernighan 设计并实现。Brian Kernighan 持续对其进行维护和增强。

来自自由软件基金会的 Paul Rubin 和 Jay Fenlason 编写了 `gawk`，使其与第七版 `UNIX` 中分发的 `awk` 原始版本兼容。John Woods 贡献了许多错误修复。David Trueman 在 Arnold Robbins 的贡献下，使 `gawk` 与新版本的 `UNIX awk` 兼容。Arnold Robbins 是目前的维护者。

请参阅《GAWK: Effective AWK Programming》以获取 `gawk` 及其文档贡献者的完整列表。

请参阅 `gawk` 分发包中的 `README` 文件，获取有关维护者以及当前支持哪些端口的最新信息。

## 错误报告

如果你在 `gawk` 中发现 bug，请发送电子邮件至 `bug-gawk@gnu.org`。请包含你的操作系统及其修订版本、`gawk` 的版本（通过 `gawk — version` 查看）、你用于编译它的哪个 C 编译器，以及一个尽可能小的用于重现问题的测试程序和数据。

在发送错误报告之前，请执行以下操作。首先，验证你是否拥有最新版本的 `gawk`。许多 bug（通常是细微的）在每个发布版本中被修复，如果你的版本过旧，问题可能已经得到解决。其次，查看将环境变量 `LC_ALL` 设置为 `LC_ALL=C` 是否会让行为符合你的预期。如果是，则这是一个区域（locale）问题，可能是 bug 也可能不是。最后，请仔细阅读本帮助页和参考手册，以确保你认为的 bug 确实是 bug，而不是仅仅是语言的特性。

无论你做什么，**不要**在 `comp.lang.awk` 中发布错误报告。虽然 `gawk` 开发者偶尔会阅读该新闻组，但在那里发布错误报告不是报告 bug 的可靠方法。相反，请使用上方提供的电子邮件地址。真的。

如果你正在使用 GNU/Linux 或基于 BSD 的系统，你可能希望向你发行版的供应商提交错误报告。这可以，但请同时也向官方电子邮件地址发送一份副本，因为无法保证错误报告会被转发给 `gawk` 维护者。

## bug

由于有了命令行变量赋值功能，`-F` 选项并不是必需的；它仅为了为了向后兼容而存在。

### 参见

`egrep(1)`, `sed(1)`, `getpid(2)`, `getppid(2)`, `getpgrp(2)`, `getuid(2)`, `getuuid(2)`, `getgid(2)`, `getegid(2)`, `getgroups(2)`, `usleep(3)`

《The AWK Programming Language》，Alfred V. Aho, Brian W. Kernighan, Peter J. Weinberger, Addison-Wesley, 1988. ISBN 0-201-07981-X.

GAWK: Effective AWK Programming, Edition 4.1, 随 `gawk` 源码发布。该文档的当前版本可以在网上获取：



http://www.gnu.org/software/gawk/manual.

## 示例

打印并排序所有用户的登录名：`BEGIN { FS = ":" } { print $1 | "sort" }`

统计文件行数：`{ nlines++ } END { print nlines }`

在文件的每行前加上行号：`{ print FNR, $0 }`

拼接并行号（一种变体）：`{ print NR, $0 }`

对特定数据行运行外部命令：`tail -f access | awk '/home.html/ {system("nmap")}'`

## 致谢

Brian Kernighan 在测试期间宝贵的帮助。

## 复制权限

Copyright © 1989, 1991, 1992, 1993, 1994, 1995

## BASH_BUILTINS

## 名称

`bash`, `:`, `;`, `[`, `alias`, `bg`, `break`, `builtin`, `caller`, `cd`, `command`, `compgen`, `complete`, `compopt`, `continue`, `declare`, `dirs`, `disown`, `echo`, `enable`, `eval`, `exec`, `export`, `false`, `fc`, `fg`, `getopts`, `hash`, `help`, `history`, `jobs`, `kill`, `let`, `local`, `logout`, `mapfile`, `popd`, `printf`, `pushd`, `pwd`, `read`, `readonly`, `return`, `set`, `shift`, `shopt`, `source`, `suspend`, `test`, `times`, `trap`, `true`, `type`, `typeset`, `ulimit`, `umask`, `unalias`, `unset`, `wait` - bash 内置命令，详参见 `bash`(1)

### BASH 内置命令

除非另有说明，本节中记录的每个内置命令都接受以 `-` 开头的选项——使用 `—` 表示选项的结束。`；`、`true`、`false` 和 `test` 内置命令不接受选项，也不对 `—` 进行特殊处理。`exit`, `logout`, `break`, `continue`, `let` 和 `shift` 内置命令接受并处理带有 `-` 句缀的参数，而无需 `—`。其他接受参数的内置命令未被指定为接受选项，它们会将以 `-` 开头的参数解释为无效选项，并需要 `—` 来防止这种解释。

无影响；该命令除了展开别名和执行指定的重定向外，不执行任何操作。返回零退出码。

+   * `filename[arguments]`

`source filename [arguments]`

在当前 shell 环境中读取并执行来自 `filename` 的命令，并返回从 `filename` 执行的最后一个命令的退出状态。如果 `filename` 不包含斜杠，则使用 `PATH` 中的文件名来查找目录文件名。`PATH` 中搜索的文件不需要是可执行的。当 bash 不在 posix 模式时，如果在 `PATH` 中没有找到文件，则搜索当前目录。如果关闭了 `shop` 命令的 `sourcepath` 选项，则不搜索 `PATH`。如果提供了任何参数，它们将成为位置参数并保持不变。脚本的返回状态是最后一个执行命令的状态（如果未执行任何命令，则为 0），如果未找到或无法读取 `filename`，则为 false。

+   * `[-p] [name=value]`

不带参数或带有 `-p` 选项的 `alias` 会以 `alias=value` 的形式在标准输出上打印别名列表。当提供参数时，将为每个给定的名称定义一个别名。值末尾的空格会导致在展开别名时检查下一个单词是否进行别名替换。对于参数列表中的每个未提供值的名称，将打印别名的名称和值。如果给出一个未定义别名的名称，则 `alias` 将返回。

+   * `bg [jobspec ...]`

在后台恢复每个挂起的 `jobspec`，就好像它在 `&` 之前启动的一样。如果未指定 `jobspec`，则使用 shell 对当前作业的概念。当禁用运行作业控制时，`bg jobspec` 返回 0；或者在启用运行作业控制时，未找到指定的 `jobspec` 或该 `jobspec` 在没有作业控制的情况下启动的。

+   * `bind [-m keymap] [-q function] [-u function] [-r keyseq]`

* `bind [-m keymap] -f filename`

* `bind [-m keymap] -x keyseq:shell-command`

* `bind [-m keymap] keyseq:function-name`

* `bind readline`

显示当前的 readline 和函数绑定，将键序列绑定到 readline 函数或宏，或设置 readline 变量。每个非选项参数都是其在 `.inputrc` 中所示的命令，但每个绑定或命令必须作为单独参数传递；例如，`"^C-X-C-r"`：重新读取初始化文件。如果提供了选项，它们具有以下含义：

+   `- keymap`

使用 `keymap` 作为受后续命令影响的键map。接受的 `keymap` 名称有 `emacs`, `emacs-standard`, `emacs-meta`, `emacs-ctlx`, `vi`, `vi-move`, `vi-command` 和 `vi-insert`。`vi` 等于 `vi-command`；`emacs` 等于 `emacs-standard`。

+   `- l`

列出所有 readline 函数的名称。

+   `- p`

以可以重新读取的形式显示 readline 函数名和绑定。

+   `- s`

以可以重新读取的形式显示绑定到宏的 readline 键序列及其输出的字符串。

+   `- S`

显示绑定到宏的 readline 键序列及其输出的字符串。

+   `- v`

以可以重新读取的形式显示 readline 变量名和值。

+   `- f filename`

列出当前的 readline 变量名和值。

+   `- q function`

从 `filename` 读取键位绑定（key bindings）。

+   `- u function`

查询哪些键调用了命名的函数。

+   `- r keyseq`

取消所有绑定到命名函数的键。

+   `- x keyseq:shell-command`

移除 `keyseq` 的任何绑定。每当输入 `keyseq` 时，执行 `shell-command`。当执行 `shell-command` 时，shell 将 `READLINE_LINE` 变量设置为 readline 行缓冲区的内容，并将 `READLINE_POINT` 变量设置为插入点的当前位置。如果执行的命令更改了 `READLINE_LINE` 或 `READLINE_POINT` 的值，这些新值将反映在编辑状态中。

+   `- X`

以可以重复输入的格式列出所有绑定到 shell 命令的键序列及关联命令。

除非给出未识别选项或发生错误，否则返回值为 0。

`break [n]` 从 `for`, `while`, `until` 或 `select` 循环内部退出。如果指定了 `n`，则退出 `n` 级。如果 `n` 大于循环次数，则退出所有循环。除非 `n` 不等于 1，否则返回值为 0。

`builtin [arguments]` 执行指定的内置命令，并返回其状态。这在定义函数名与内置相同时很有用。如果未找到内置，则返回状态为 false。

`caller [expr]` 返回任何活动帧的上下文。如果没有指定 `expr`，`caller` 显示当前子程序的行号和文件名。一个非负整数作为 `expr` 提供。

`cd [-L] [-e] [-@]]` 将目录切换到 `dir`。如果未提供 `dir`，则默认值为 `HOME`。`dir` 之后的附加参数将被忽略。如果 `dir` 以斜杠 (`/`) 开头，则不使用 `CPATH`.-P 选项导致 `cd` 通过解析链接到当前目录使用物理目录结构。如果 `dir` 中出现 `.`，则通过移除 `dir` 中之前的路径直到斜杠或开头来处理。如果在 `-P` 时提供了 `-e`，更改目录后无法成功确定工作目录，`cd` 将返回失败状态。在支持的系统中，`-@` 选项返回与文件或目录相关的扩展属性。在尝试目录之前，会将参数转换为 `PWD`。如果使用了 `CPATH` 中的非空目录名，或者它是第一个参数，且目录更改成功，则会将新目录的绝对路径写入标准输出。如果目录更改成功，返回值为 true；否则为 false。



`command [-pV] command [arg ...]` 以常规函数查找运行命令。只执行内置命令或在 `PATH` 中找到的命令。如果给了 `-p` 选项，将使用保证找到所有标准实用程序的默认 `PATH` 值对命令进行搜索。如果提供了 `-V` 或 `-v` 选项，则打印命令的描述。`-v` 选项导致显示指示调用命令或文件名的单个单词；`-V` 选项产生更详细的描述。如果提供了 `-V` 或 `-v` 选项，如果找到了命令则退出状态为 `0`，否则为 `1`。如果未提供任何选项且发生错误或找不到命令，则退出状态为 `127`。否则，`command` 内置命令的退出状态为 `command` 的退出状态。

`compgen [option] [word]` 根据选项生成 `word` 的可能匹配，选项可以是 `complete` 内置命令接受的任何选项（`-p` 和 `-r` 除外），并将匹配项写入标准输出。在使用 `-F` 或 `-C` 选项时，可编程补全功能设置的各种 shell 变量可用，但没有有效值。

匹配项的生成方式与可编程补全代码直接从带有标志的补全规范生成它们相同。如果指定了 `word`，则只显示与 `word` 匹配的补全项。

返回值为 `true`，除非指定了无效选项或没有生成任何匹配项。

`complete [-abcdefghijksv] [-c comp-option] [-DE] [-A action] [-G globpat] [-W wordlist] [-F function] [-C command] [-X filter] [-P prefix] [-S suffix] name [...]`

### `complete -pr [name ...]`
指定每个 `name` 的参数应如何补全。如果提供了 `-p` 选项，或者如果没有提供任何选项，则打印现有的补全规范，其方式允许它们为每个 `name` 重用；如果未提供任何 `name`，则打印所有补全规范。`-D` 选项表示剩余的选项和操作适用于“默认”补全命令；即对之前没有定义过补全的命令尝试补全。`-E` 选项表示剩余的选项和操作适用于“空”补全命令；即对空白行尝试补全。

在上述“可编程补全”（Programmable Completion）部分描述了应用这些补全规范的过程。

其他选项如果指定，将具有以下含义。`-G`、`-W` 和 `-X` 选项的参数（以及在需要时的 `-P` 和 `-S` 选项）应该用引号括起来，以防止它们在调用 `complete` 内置命令之前被展开。

## `-o comp-option`
`comp-option` 控制补全规范（compspec）除简单生成补全之外的多个方面。`comp-option` 可以是以下之一：

### `bashdefault`
- 如果 `compspec` 没有生成匹配项，则执行剩余的默认 `bash` 补全。

### `default`
- 如果 `compspec` 没有生成匹配项，使用 `readline` 的默认文件名补全。

### `dirnames`
- 如果 `compspec` 没有生成匹配项，则执行目录名补全。

### `filenames`
- 告诉 `readline` `compspec` 生成文件名，这样它就可以执行任何特定特定的处理（如为目录名添加斜杠、特殊字符或抑制末尾空格）。旨在与 shell 函数配合。

### `nquote`
- 告诉 `readline` 如果补全的单词是文件名，则不要对它们加引号（对文件名加引号是默认设置）。

### `nospace`
- 告诉 `readline` 不要在行尾补全的单词后添加空格（默认设置）。

### `plusdir`
- 在生成 `compspec` 定义的任何匹配项后，尝试目录名补全，并将任何匹配项添加到其他操作的结果中。

## `-A action`
`action` 可能是以下之一，用以生成可能的补全项列表：

- `alias`: 别名。。也可以指定为 `-a`。
- `arrayvar`: 数组变量名。
- `binding`: 键绑定名。
- `builtin`: shell 内置命令名。也可以指定为 `-b`。
- `command`: 命令名。也可以指定为 `-c`。
- `directory`: 目录名。也可以指定为 `-d`。
- `disabled`: 已禁用的 shell 内置命令名。
- `enabled`: 已启 shell 内置命令名。
- `export`: 导出 shell 变量名。也可以指定为 `-e`。
- `file`: 文件名。也可以指定为 `-f`。
- `function`: shell 函数名。
- `group`: 组名。也可以指定为 `-g`。
- `helptopic`: `help` 内置命令接受的帮助主题。
- `hostname`: 主机名，来自 `HOSTFILE` shell 变量指定的文件。
- `job`: 任务名，如果作业控制开启。也可以指定为 `-j`。
- `keyword`: shell 保留字。也可以指定为 `-k`。
- `running`: 正在运行的任务名，如果作业控制开启。
- `service`: 服务名。也可以指定为 `-s`。
- `setopt`: `set` 内置命令 `-o` 选项的有效参数。
- `shopt`: `shopt` 内置命令接受的 shell 选项。
- `signal`: 信号名。
- `stopped`: 停止的任务名，如果作业控制开启。
- `user`: 用户名。也可以指定为 `-u`。
- `variable`: 所有 shell 变量名。也可以指定为 `-v`。
- `-C command` `command` 在子 shell 环境中执行，其输出用作可能的补全项。
- `-F function` shell 函数在当前 shell 环境中执行。当执行函数时，第一个参数 `($1)` 是正在补全参数的命令名，第二个参数 `($2)` 是正在补全的单词，第三个参数 `($3)` 是当前行中被补全单词之前的单词。完成后，从 `REPLY` 数组的值中检索可能的补全项。
- `-G glob` 路径扩展 `glob` 被展开以生成可能的补全项。
- `-P prefix` 在应用所有其他选项后，在每个可能的补全项开头添加 `prefix`。
- `-S suffix` 在应用所有其他选项后，在每个可能的补全项末尾附加 `suffix`。
- `-W word` 将单词列表拆分为 `IFS` 特殊变量，并展开每个结果。可能的补全项是结果列表中与正在补全的单词匹配的成员。
- `-X filterpat` `filterpat` 是用于路径扩展的模式。它应用于由前面的选项和参数生成的补全项列表，并从列表中移除每个匹配 `filterpat` 的补全项。`filterpat` 开头的 `!` 反转该模式；在这种情况下，任何匹配 `filterpat` 的补全都会被移除。

返回值为 `true`，除非提供了无效选项、在没有 `name` 的情况下提供了 `-p` 或 `-r` 选项、尝试删除不存在的 `name` 或发生错误。

## `continue [n]`
恢复 `for`、`while` 或 `select` 循环的下次迭代。如果 `n` 大于循环数量，则恢复最后一个嵌套的（顶层）循环。返回值为 `0`，除非 `n` 不大于或等于 `1`。

## `typeset [-FFgnux [-p] [name=value] ...`
声明变量并为它们赋予属性。如果没有给出 `name`，则显示变量的值。`-p` 选项将显示每个 `name` 的属性和值。当 `-p` 与参数一起使用时，忽略除 `-f` 和 `-F` 之外的额外选项。如果没有 `name` 参数，将显示具有指定属性的所有变量的属性和值。`-f` 显示 shell 函数；只打印函数名和属性。如果启用了 `shellcheck`，还会显示定义的源文件名和行号。`-F` 选项意味着 `-f`。`-g` 选项即使在 shell 函数中执行 `declare` 也在全局范围内创建或定义变量。在所有其他情况下均忽略。可以使用以下选项限制输出具有指定属性的变量或赋予变量属性：

- `-a` 每个 `name` 是索引数组变量（见 Arrays）。
- `-A` 每个 `name` 是关联数组变量（见 Arrays）。
- `-f` 仅使用函数名。
- `-i` 变量被视为整数；在给变量赋值时执行算术评估（见 ARITHMETIC EVALUATION）。
- `-l` 给变量赋值时，将所有大写字符转换为小写。禁用大写属性。
- `-n` 给每个 `name` 赋予引用属性，使其成为另一个变量的名称引用。除了更改 `-n` 属性本身，对 `name` 的所有引用和赋值都在 `name` 值所引用的变量上执行。
- `-r` 使 `name` 只读。这些名称无法通过后续赋值语句赋值或取消。
- `-t` 给每个 `name` 赋予跟踪属性。跟踪函数从调用 shell 继承 `DEBUG` 和 `RETURN` 陷。跟踪属性对变量没有特殊含义。
- `-u` 当变量被赋值时，所有小写字母都将转换为大写字母。小写属性被禁用。
- `-x` 标记通过环境导出到后续命令的名称。



使用 `+` 代替 `-` 可以关闭属性插入，但例外是 `+a` 可能无法用于破坏数组变量，且 `+r` 不会移除属性。在函数中使用时，`declare` 和 `typeset` 会使每个名称变为局部的（与 `local` 命令相同），除非使用了 `-g` 选项。如果变量名后紧跟 `=value`，则变量的值设置为 `value`。当使用 `-a` 或 `-A` 并配合复合赋值语法创建数组变量时，额外的属性在后续赋值之前不会生效。返回值为 0，除非遇到无效选项、尝试使用 `-f foo=bar` 定义函数、尝试给只读变量赋值、在不使用复合赋值语法（`Arrays`）的情况下尝试给数组变量赋值、其中一个名称不是有效的变量名、尝试关闭数组变量的只读状态，或尝试使用 `-f` 显示不存在的函数。

## `dirs` [-clvp] [+n]
不带选项时，显示当前记住的目录列表。默认显示为单行，目录名用空格分隔。通过 `pushd` 命令将目录添加到列表中；`popd` 命令从列表中移除项。

### `-c`
通过删除所有条目来清除目录栈。

### `-l`
使用全路径生成列表；默认列表格式使用波浪号 `~` 表示目录。

### `-p`
每行打印一个目录栈项。

### `-v`
每行打印一个目录栈项，并在每个条目前加上其在栈中的索引。

### `+n`
在不带选项调用时，显示 `dirs` 输出的列表中从左侧数的第 `n` 个条目（从零开始）。

### `-n`
在不带选项调用时，显示 `dirs` 输出的列表中从右侧数的第 `n` 个条目（从零开始）。除非提供了无效选项或 `n` 索引超出目录栈范围，否则返回值为 0。

## `disown` [-ar] [-h] [jobspec ...]
不带选项时，从活动作业表中移除每个 `jobspec`。如果不存在 `jobspec` 且未提供 `-a` 或 `-r` 选项，则使用当前作业。如果给出了 `-h` 选项，每个 `jobspec` 不从表中移除，而是被标记为当 shell 接收到 `SIGHUP` 时向作业发送 `SIGHUP`。如果没有提供 `jobspec`，`-a` 选项意味着移除或标记所有作业；没有 `jobspec` 参数的 `-r` 选项将操作限制为运行中的作业。除非 `jobspec` 未指定有效作业，否则返回值为 0。

## `echo` [-n] [arg ...]
输出由分隔的参数，后接换行符。除非发生错误，返回状态为 0。如果指定了 `-n`，则抑制末尾换行符。如果给了 `-e` 选项，则解释这些转义字符（即使在默认解释这些的系统中也是如此）。可以使用 `xpg_echo` shell 选项来动态确定 `echo` 是否默认扩展这些转义字符。`echo` 不将 `--` 解释为选项的结束。`echo` 解析以下转义序列：

- `\a` 警报（铃声）
- `\b` 退格格
- `\c` 抑制后续输出
- `\e` 转义字符
- `\f` 换页
- `\n` 换行
- `\r` 回车
- `\t` 水平制表
- `\v` 垂直制表
- `\0nnnn` 值为八进制值 `nnn` 的八位字符（零到三位八进制数字）
- `\xHH` 值为十六进制值 `HH` 的八位字符（一或两位十六进制数字）
- `\uHHHH` 为 Unicode (ISO/IEC 10646) 字符，其值为十六进制值 `HHHH`（一到四位十六进制数字）
- `\uHHHHHHHH` 为 Unicode (ISO/IEC 10646) 字符，其值为十六进制值 `HHHHHHHH`（一到八位十六进制数字）

## `enable` [-a] [-dnps] [-f filename] [name ...]
启用和禁用内置 shell 命令。禁用内置命令允许执行与 shell 内置命令同名的磁盘命令，尽管 shell 通常在搜索磁盘命令之前先搜索内置命令。如果使用 `-n`，则禁用每个名称；否则，启用名称。例如，通过 shell 的 `PATH` 找到 `test` 二进制文件以使用 shell 内置版本的 "enable-test"。`-f` 选项意味着从共享对象文件名加载新的内置命令（在支持动态加载的系统中）。`-d` 选项将删除之前通过 `-f` 加载的内容。如果没有给出名称参数，或提供了 `-p` 选项，则打印 shell 内置列表。在没有其他选项参数的情况下，列表包含所有启用的内置命令。如果提供了 `-n`，则只打印禁用的内置命令。如果提供了 `-f`。如果提供了 `-s`，输出限制为 POSIX 特殊内置命令。除非名称不是 shell 内置命令或从共享对象加载新内置命令时出错，否则返回值为 0。

## `eval` [arg ...]
参数被读取并合并成单个命令。然后由 shell 读取并执行该命令，并将其状态作为 `eval` 的值返回。如果没有参数或空参数，`eval` 返回 0。

## `exec` [-l] [-name] [command [arguments]]
如果指定了命令，它将替换当前 shell。如果没有给出命令，shell 将退出。除非遇到无效选项，返回值为 0。如果使用 `-l`，则作为登录 shell 执行命令。如果使用 `-name`，则赋予指定的名称。如果提供了参数，则将其传递给命令。

## `exit` [status]
终止 shell 并返回退出状态。如果没有提供状态，默认为 0。

## `trap` [command] [signal ...]
定义当接收信号时执行的命令。如果命令为空，则移除 trap。

## `fg` [jobspec]
在前台恢复作业。如果没有设置 `jobspec`，则使用当前作业。

## `bg` [jobspec]
在后台恢复作业。如果没有设置 `jobspec`，则使用当前作业。

## `jobs` [jobspec]
列出活动作业。如果指定了 `jobspec`，则只列出匹配的作业。除非遇到无效选项，返回值为 0。

## `wait` [jobspec]
等待作业完成。如果没有指定 `jobspec`，则等待所有后台作业。除非遇到无效选项，返回值为 0。

## `history` [n]
显示命令历史。如果指定了 `n`，显示最后 `n` 条命令。除非遇到无效选项，返回值为 0。

## `type` [name]
描述命令（别名、函数、内置或文件）的类型。除非未找到。

## `which` [name]
显示可执行文件的路径。除非未找到，返回值为 0。

## `alias` [name=value]
定义别名。除非遇到无效选项，返回值为 0。

## `unalias` [name]
移除别名。除非遇到无效选项，返回值为 0。

## `readonly` [name=value]
设置变量为只读。除非遇到无效选项，返回值为 0。

## `unset` [name]
移除变量、函数或属性。除非遇到无效选项，返回值为 0。

## `export` [name=value]
将变量标记为导出。除非遇到无效选项，返回值为 0。

## `local` [name=value]
在函数中声明局部变量。除非遇到无效选项，返回值为 0。

## `let` [expression]
评估表达式。为真返回 0，为假返回 1。

## `((` [expression]`)`
评估术表达式。为真返回 0，为假返回 1。

## `[` [expression] `]`
评估条件。为真返回 0，为假返回 1。

## `test` [expression]
测试表达式。为真返回 0，为假返回 1。

## `source` [file]
源 shell 文件。除非文件无法读取，返回值为 0。

## `.` [file]
`source` 的别名。除非文件无法读取，返回值为 0。

## `read` [options] variable
从标准输入读取一行。除非发生错误，返回值为 0。

## `printf` [option] [...]
打印格式化字符串。除非发生错误，返回值为 0。

## `col` [options] [file]
将文本格式化为列。除非发生错误，返回值为 0。

## `tr` [options] [file]
翻译或删除字符。除非发生错误，返回值为 0。

## `cut` [options] [file]
从行中删除部分。除非发生错误，返回值为 0。

## `sed` [script] [file]
用于过滤文本流编辑器。除非发生错误，返回值为 0。

## `awk` [program] [file]
模式扫描处理语言。除非发生错误，返回值为 0。

## `sort` [options] [file]
排序文本文件。除非发生错误，返回值为 0。

## `uniq` [options] [file]
报告或跳过重复行。除非发生错误，返回值为 0。

## `grep` [options] [pattern]
搜索行中的模式。除非发生错误，返回值为 0。

## `diff` [options] file1 file2
按行比较文件。除非发生错误，返回值为 0。

## `join` [options] file1 file2
根据共同部分合并文件。除非发生错误，返回值为 0。

## `paste` [options] file1 file
拼接文件的行。除非发生错误，返回值为 0。

## `tsort` [options] [file]
对列进行排序。除非发生错误，返回值为 0。



# 命令参考

### `wc [options] [file]`
统计行、单词、字节。除非发生错误，返回值为 0。

### `cmp [options] [file]`
按字节比较文件。除非发生错误，返回值为 0。

### `compress [options] [file]`
为了存储压缩文件。除非发生错误，返回值为 0。

### `compress [options] [file]`
解压缩压缩文件。除非发生错误，返回值为 0。

### `gzip [options] [file]`
压缩或扩展文件。除非发生错误，返回值为 0。

### `compress [options] [file]`
压缩或扩展文件。除非发生错误，返回值为 0。

### `bzip2 [options] [file]`
使用 `bzip2` 压缩文件。除非发生任何错误，返回值为 0。

### `xz [options] [file]`
使用 `xz` 压缩或解压文件。除非发生错误，返回值为 0。

### `tar [options] [file]`
创建归档文件。除非发生错误，返回值为 0。

### `zip [options] [file]`
创建压缩包。除非发生错误，返回值为 0。

### `unzip [options] [file]`
提取压缩包。除非发生错误，返回值为 0。

### `lzma [options] [file]`
压缩或解压。除非发生错误，返回值为 0。

### `cz [options] [file]`
压缩或解压。除非发生错误，返回值为 0。

### `find [path] [expression]`
在目录中搜索文件。除非发生错误，返回值为 0。

### `locate [pattern]`
在数据库中搜索文件。除非发生错误，返回值为 0。

### `whichis [name]`
显示命令的位置。除非发生错误，返回值为 0。

### `command [name]`
显示如何执行命令。除非发生错误，返回值为 0。

### `file [options] [file]`
确定文件类型信息。除非发生错误，返回值为 0。

### `stat [options] [file]`
显示文件属性。除非发生错误，返回值为 0。

### `ls [options] [file]`
列出内容。除非发生错误，返回值为 0。

### `du [options] [file]`
估计磁盘用量。除非发生错误，返回值为 0。

### `df [options] [file]`
估计空间使用。除非发生错误，返回值为 0。

### `mount [options] [file]`
挂载文件系统。除非发生错误，返回值为 0。

### `umount [options] [file]`
卸载文件系统。除非发生错误，返回值为 0。

### `cd [directory]`
切换目录。除非发生错误，返回值为 0。

### `pwd [options]`
打印工作目录。除非发生错误，返回值为 0。

### `mkdir [options] [directory]`
创建目录。除非发生错误，返回值为 0。

### `rmdir [options] [directory]`
移除空目录。除非发生错误，返回值为 0。

### `rm [options] [file]`
删除文件。除非发生错误，返回值为 0。

### `cp [options] [file]`
复制文件。除非发生错误，返回值为 0。

### `mv [options] [file]`
移动或重命名文件。除非发生错误，返回值为 0。

### `touch [options] [file]`
创建文件或更新时间戳。除非发生错误，返回值为 0。

### `chmod [options] [file]`
更改权限。除非发生错误，返回值为 0。

### `chown [options] [file]`
更改所有者。除非发生错误，返回值为 0。

### `chgrp [options] [file]`
更改用户组。除非发生错误，返回值为 0。

### `facet [options] [file]`
列出属性。除非发生错误，返回值为 0。

### `chattr [options] [file]`
更改文件属性。除非发生错误，返回值为 0。

### `fdisk [options]`
操作或处理 Linux 分区表。除非发生错误，返回值为 0。

### `fsck [options] [file]`
检查并修复文件系统。除非发生错误，返回值为 0。

### `mkfs [typetype] [file]`
格式化文件系统。除非发生错误，返回值为 0。

### `blklist [options] [file]`
列出块设备。除非发生错误，返回值为 0。

### `lsblk [options] [file]`
列出块设备信息。除非发生错误，返回值为 0。

### `fdisk [options] [file]`
打印分区表。除非发生错误，返回值为 0。

### `parted [options] [file]`
分区并操作磁盘。除非发生错误，返回值为 0。

### `gdisk [options] [file]`
GPT 分区表。除非发生错误，返回值为 0。

### `wipefs [options] [file]`
擦除系统签名。除非发生错误，返回值为 0。

### `mkswap [options] [file]`
创建交换区。除非发生错误，返回值为 0。

### `swapon [options] [file]`
启用交换区。除非发生错误，返回值为 0。

### `swapoff [options] [file]`
禁用交换区。除非发生错误，返回值为 0。

### `pv [options] [file]`
监控数据流。除非发生错误，返回值为 0。

### `dd [options] [file]`
转换并复制文件。除非发生错误，返回值为 0。

### `smartctl [options] [file]`
控制 SMART 信息。除非发生错误，返回值为 0。

### `iostat [options] [file]`
报告 CPU 使用统计。除非发生错误，返回值为 0。

### `vmstat [options] [file]`
报告虚拟内存。除非发生错误，返回值为 0。

### `top [options] [file]`
显示 Linux 任务进程。除非发生错误，返回值为 0。

### `htop [options] [file]`
交互式进程查看器。除非发生错误，返回值为 0。

### `iotop [options] [file]`
监控磁盘使用。除非发生错误，返回值为 0。

### `sar [options] [file]`
报告系统活动。除非发生错误，返回值为 0。

### `nload [options] [file]`
监控网络流量使用。除非发生错误，返回值为 0。

### `netstat [options] [file]`
报告网络统计。除非发生错误，返回值为 0。

### `ip [options] [file]`
显示或配置 IP。除非发生错误，返回值为 0。

### `route [options] [file]`
显示或修改 IP。除非发生错误，返回值为 0。

### `nmcli [options] [file]`
配置网络连接。除非发生错误，返回值为 0。

### `dig [options] [file]`
DNS 查询工具。除非发生错误，返回值为 0。

### `nslookup [options] [file]`
查询名称。除非发生错误，返回值为 0。

### `ping [options] [file]`
发送 ICMP。除非发生错误，返回值为 0。

### `traceroute [options] [file]`
跟踪路由。除非发生错误，返回值为 0。

### `mtr [options] [file]`
网络诊断。除非发生错误，返回值为 0。

### `nmap [options] [file]`
网络扫描器。除非发生错误，返回值为 0。

### `tcpdump [options] [file]`
捕获数据包。除非发生错误，返回值为 0。

### `wireshark [options] [file]`
网络协议分析器。除非发生错误，返回值为 0。

### `curl [options] [file]`
传输数据。除非发生错误，返回值为 0。

### `wget [options] [file]`
获取文件。除非发生错误，返回值为 0。

### `scp [options] [file]`
安全复制文件。除非发生错误，返回值为 0。

### `sftp [options] [file]`
安全文件传输。除非发生错误，返回值为 0。

### `ssh [options] [file]`
OpenSSH 客户端。除非发生错误，返回值为 0。

### `rsh [options] [file]`
远程 shell。除非发生错误，返回值为 0。

### `telnet [options] [file]`
远程终端。除非发生错误，返回值为 0。

### `opens-keygen [options] [file]`
生成 SSH 密钥。除非发生错误，返回值为 0。

### `ssh-agent [options] [file]`
管理 SSH 密钥。除非发生错误，返回值为 0。

### `ssh-add [options] [file]`
添加 SSH 密钥。除非发生错误，返回值为 0。



在名称中放置冒号（`:`）并将 `OPTARG` 设置为找到的选项字符。

如果找到选项（或未指定的选项），`getopts` 返回 true。如果遇到选项末尾或发生错误，则返回 false。

### `hash`
`hash [-lr] [-p filename] [-dt] [name]`

每次调用 `hash` 时，都会通过搜索 `$PATH` 中的目录来确定命令的完整路径，并将其记住。任何之前记录的路径都将被丢弃。如果提供了 `-p` 选项，则不进行路径搜索，并使用 `filename` 作为命令的完整路径。`-r` 选项导致 shell 忘记所有已记录的位置。如果提供了 `-t` 选项，则会打印每个名称对应的完整路径。使用 `-t` 提供了多个名称参数时，名称将打印在哈希后的路径之前。`-l` 选项导致以一种可以重用为输入的格式显示输出。如果如果没有提供任何参数，或者仅提供了 `-l`，则会打印有关已记录命令的信息。除非未找到名称或提供了无效选项，否则返回状态为 true。

### `Help`
`Help [-dms] [pattern]`

显示关于内置命令的帮助信息。如果指定了 `pattern`，帮助将提供所有匹配 `pattern` 的命令的帮助；否则将打印所有内置命令和 shell 结构的帮助。

- `-d`

显示每个模式的简短描述

- `-m`

以类似 man 页的格式显示每个模式的描述

- `-s`

仅显示每个模式的简短用法提要

除非没有命令匹配模式，否则返回状态为 0。

### `history`
`history [-n]`
`history -c`
`history -d offset`
`history -anrw [filename]`
`history -p arg [arg ...]`
`history -s arg [arg ...]`

在不带任何选项的情况下，显示带行号的命令历史列表。带有 `*` 的行表示已执行。参数 `n` 仅列出最后 `n` 行。如果 shell 变量 `HISTTIMEFORMAT` 被设置且不为空，则它被用作格式字符串，在格式化时间戳和历史行之间打印一个空行。使用 `strftime(3)` 显示与每个显示的历史条目相关的时间戳。如果提供了 `filename`，则将其用作历史文件的名称；否则，使用 `HISTFILE` 的值。如果提供了选项，其具有以下含义：

- `-c`

通过删除所有条目来清除历史列表。

- `-d offset`

删除位置在 `offset` 处的历史条目。

- `-a`

将“新”历史行（自当前 bash 会话开始以来输入的历史行）追加到历史文件中。

- `-n`

从历史文件中读取尚未读取过的历史行到当前历史列表中。这些行是自当前 bash 会话开始以来追加到历史文件的行。

- `-r`

读取历史文件的内容并将其追加到当前历史列表中。

- `-w`

将当前历史列表写入历史文件，覆盖历史文件的内容。

- `-p`

对随后的 `args` 执行历史替换，并在标准输出上显示结果。不将结果存储在历史列表中。每个 `arg` 必须用引号引起以禁用正常的历史扩展。

- `-s`

将 `args` 作为单条目存储在历史列表中。在添加 `args` 之前会移除历史列表中的最后一个命令。

如果设置了 `HISTTIMEFORMAT` 变量，则与每个历史条目相关的时间戳将被写入历史文件，用历史注释字符标记，紧随其后的数字被解释解释为上一行的时间戳。除非遇到无效偏移、在读取或写入历史文件时发生错误、作为 `-d` 的参数提供了无效偏移，或作为 `-p` 的参数启用的历史扩展失败，否则返回值为 0。

### `jobs`
`jobs [-inprs] [ jobspec ... ]`
`-command [ args ... ]`

第一个列表列出活动作业。这些选项具有以下含义：

- `-l`

列出进程 ID，并添加到普通信息中。

- `-n`

仅显示自用户上次通知其状态以来状态发生变化的作业信息。

- `-p`

仅列出作业进程组首的进程 ID。

- `-r`

仅显示运行中的作业。

- `-s`

仅显示停止的作业。

如果给了 `jobspec`，输出将限制为该作业的信息。除非遇到无效选项或提供了无效的 `jobspec`，否则返回状态为 0。

如果使用了 `-x` 选项，`jobs` 会将命令或参数中找到任何 `jobspec` 替换为相应的进程组 ID，并传递它来执行命令，返回其退出状态。

### `kill`
`kill [-s sigspec | -n signal] [pid | jobspec] ...`
`kill -l [sigspec | exit_status]`

向由 `sigspec` 指定的信号或通过 `pid` 或 `jobspec` 向进程发送信号。`sigspec` 既可以是不区分大小写的信号名称（如 `SIGKILL`，带或不带 `SIG` 前缀），可以是信号号；`signum` 是信号号。如果不存在 `jobspec`，则假设为 `SIGTERM`。参数 `-l` 列出信号名称。如果在给出 `-l` 的时候提供了任何参数，则将列出与参数对应的信号名称，且返回状态为 0。`-l` 的 `exit_status` 参数是一个数字，指定信号号或由信号终止的进程的退出状态。如果成功发送了至少一个信号，则 `kill` 返回 true；如果发生错误或遇到无效选项，则返回 false。

### `let`
`let arg [arg ...]`

每个 `arg` 都是一个要评估的算术表达式（见上文 `ARITHMETIC EVALUATION`）。

### `local`
`local [option][name=value]`

对于每个参数，都会创建一个本地变量名并赋值。该选项可以是 `declare` 接受的任何选项之一。在函数内部使用 `local` 时，它会导致变量名的可见性范围限制在该函数及其子函数中。当带有操作数时，`local` 将变量列表写入标准输出。在不在函数内部使用 `local` 是错误。返回状态为 0，除非不在函数内部、提供了无效名称或提供了无效选项。

### `Help`
`Help [-dms] [pattern]`

显示关于内置命令的帮助信息。如果指定了 `pattern`，帮助将提供所有匹配 `pattern` 的命令的帮助；否则将打印所有内置命令和 shell 结构的帮助。

- `-d`

显示每个模式的简短描述

- `-m`

以类似 man 页的格式显示每个模式的描述

- `-s`

仅显示每个模式的简短用法提要

除非没有命令匹配模式，否则返回状态为 0。

### `history`
`history [-n]`
`history -c`
`history -d offset`
`history -anrw [filename]`
`history -p arg [arg ...]`
`history -s arg [arg ...]`

在不带任何选项的情况下，显示带行号的历史列表。带有 `*` 的行表示已执行。参数 `n` 仅列出最后 `n` 行。如果 shell 变量 `HISTTIMEFORMAT` 被设置且不为空，则它被用作格式字符串，在格式化时间戳和历史行之间打印一个空行。使用 `strftime(3)` 显示与每个显示的历史条目相关的时间戳。如果提供了 `filename`，则将其用作历史文件的名称；否则，使用 `HISTFILE` 的值。如果提供了选项，其具有以下含义：

- `-c`

通过删除所有条目来清除历史列表。

- `-d offset`

删除位置在 `offset` 处的历史条目。

- `-a`

将“新”历史行（自当前 bash 会话开始以来输入的历史行）追加到历史文件中。

- `-n`

从历史文件中读取尚未读取过的历史行到当前历史列表中。这些行是自当前 bash 会话开始以来追加到历史文件的行。

- `-r`

读取历史文件的内容并将其追加到当前历史列表中。

- `-w`

将当前历史列表写入历史文件，覆盖历史文件的内容。

- `-p`

对随后的 `args` 执行历史替换，并在标准输出上显示结果。不将结果存储在历史列表中。每个 `arg` 必须用引号引起以禁用正常的历史扩展。

- `-s`

将 `args` 作为单条目存储在历史列表中。在添加 `args` 之前会移除历史列表中的最后一个命令。

如果设置了 `HISTTIMEFORMAT` 变量，则与每个历史条目相关的时间戳将被写入历史文件，用历史注释字符标记，紧随其后的数字被解释解释为上一行的时间戳。除非遇到无效偏移、在读取或写入历史文件时发生错误、作为 `-d` 的参数提供了无效偏移、或作为 `-p` 的参数启用的历史扩展失败，否则返回值为 0。

### `jobs`
`jobs [-inprs] [ jobspec ... ]`
`-command [ args ... ]`

第一个列表列出活动作业。这些选项具有以下含义：

- `-l`

列出进程 ID，并添加到普通信息中。

- `-n`

仅显示自用户上次通知其状态以来状态发生变化的作业信息。

- `-p`

仅列出作业进程组首的进程 ID。

- `-r`

仅显示运行中的作业。

- `-s`

仅显示停止的作业。

如果给了 `jobspec`，输出将限制为该作业的信息。除非遇到无效选项或提供了无效的 `jobspec`，否则返回状态为 0。

如果使用了 `-x` 选项，`jobs` 会将命令或参数中找到任何 `jobspec` 替换为相应的进程组 ID，并传递它来执行命令，返回其退出状态。



## `kill`

`kill [-s sigspec | -n signal] [pid | jobspec] ...`
`kill -l [sigspec | exit_status]`

向由 `sigspec` 指定的信号或通过 `pid` 或 `jobspec` 向进程发送信号。`sigspec` 既可以是不区分大小写的信号名称（如 `SIGKILL`，带或不带 `SIG` 前缀），可以是信号号；`signum` 是信号号。如果不存在 `jobspec`，则假设为 `SIGTERM`。参数 `-l` 列出信号名称。如果在给出 `-l` 的时候提供了任何参数，则将列出与参数对应的信号名称，且返回状态为 0。`-l` 的 `exit_status` 参数是一个数字，指定信号号或由信号终止的进程的退出状态。如果成功发送了至少一个信号，则 `kill` 返回 true；如果发生错误或遇到无效选项，则返回 false。

## `let`

`let arg [arg ...]`

每个 `arg` 都是一个要评估的算术表达式（见上文 `ARITHMETIC EVALUATION`）。

## `local`

`local [option][name=value]`

对于每个参数，都会创建一个本地变量名并赋值。该选项可以是 `declare` 接受的任何选项之一。在函数内部使用 `local` 时，它会导致变量名的可见性范围限制在该函数及其子函数中。当带有操作数时，`local` 将变量列表写入标准输出。在不在函数内部使用 `local` 是错误。返回状态为 0，除非不在函数内部、提供了无效名称或提供了无效选项。

## `Help`

`Help [-dms] [pattern]`

显示关于内置命令的帮助信息。如果指定了 `pattern`，帮助将提供所有匹配 `pattern` 的命令的帮助；否则将打印所有内置命令和 shell 结构的帮助。

## `mapfile`

`mapfile` 格式格式。格式是一个字符字符串，包含三种类型的对象：普通字符，直接复制到标准输出；字符转义序列，转换并复制到标准输出；以及格式规范，每个导致下一个参数的打印。除了标准的 `printf(1)` 格式规范，`printf` 解释以下扩展：

+ 展开相应参数中的反斜杠转义（除了单引号中的反斜杠不会被移除，且以 `\0` 开头的进制转义最多包含四位数字）。
+ 将 `datefmt` 作为 `strftime(3)` 的格式字符串输出日期时间字符串。相应的参数是一个表示自纪元以来秒数的整数。两个特殊参数值可以使用：`-1` 代表当前时间，`-2` 代表 shell 调用的时间。如果没有指定参数，转换行为就像给定了 `-1` 一样。这是对通常 `printf` 行为的例外。

根据需要重复格式以消耗所有参数。如果需要的参数比提供的多，额外的格式规范将表现像提供了零值或空字符串一样。非字符串格式规范的参数被视为 C 常量，但允许前导加负号，并且如果领先字符是单引号或双引号，则值为后续字符的 ASCII 值。成功时返回零，失败时返回非零。

## `pushd`

`pushd [+n] [-n]`
`pushd [-n] [dir]`

将目录添加到目录栈的顶端，或旋转堆栈，使栈的新顶端成为当前工作目录。如果不提供参数，则交换栈顶部的两个目录并返回 0，除非目录栈为空。如果提供了参数，其含义如下：

- `-n`

  在向栈中添加目录时，抑制正常的目录切换，因此只对堆栈进行操作。
- `+n`

  旋转堆栈，使第 `n` 个目录（从 `dirs` 显示的列表左侧开始计数，从 0 开始）位于栈顶。
- `-n`

  旋转堆栈，使第 `n` 个目录（从 `dirs` 显示的列表右侧开始计数，从 0 开始）位于栈顶。
- `+dir`

  将 `dir` 添加到目录栈的顶端，使其成为新的工作目录，就像它被作为 `cd` 内置命令的参数提供了一样。

如果 `pushd` 命令执行成功，也会执行 `dirs`。如果使用第一种形式，除非 `cd to dir` 失败，否则 `pushd` 返回 0。使用第二种形式时，除非目录栈为空、指定了不存在的目录栈元素或切换到指定的新当前目录时失败，否则 `pushd` 返回 0。

## `pwd`

`pwd [-LP]`

打印当前工作目录的绝对名称。如果提供了 `-P` 选项或启用了 `set` 内置命令的 `-o physical` 选项，路径不包含符号链接。如果使用 `-L` 选项，路径可能包含符号链接。返回状态为 0，或者在读取当前目录名称时发生错误，或提供了无效选项。

## `read`

`read [-ers] [-a name] [-d delim] [-i text] [-n nchars] [-p prompt] [-t timeout] [name ...]`

从标准输入或作为 `-u` 选项的参数从文件描述符 `fd` 读取一行，并将第一个单词分配给第一个 `name`，将第二个单词分配给第二个 `name`，依此类推，剩余的单词及其之间的的分隔符分配给最后一个 `name`。如果输入流中的单词少于 `name` 的数量，则剩余的 `name` 被赋值为空值。`nfs` 中的字符用于使用 shell 用于扩展的相同规则（见上文“单词拆分”）将行拆分为单词。反斜杠字符 (`\`) 用于移除读取的下一个字符的任何特殊含义并用于行持续符。如果提供了选项，其含义如下：

- `-a name`

  将单词分配给数组变量 `aname` 的连续索引，从 0 开始。在分配任何新值之前 `aname` 会被清除。其他 `name` 参数被忽略。
- `-d delim`

  `delim` 的第一个字符用于终止输入行，而不是换行符。
- `-e`

  如果标准输入来自终端，则使用 `readline`（见上文 `READLINE`）来获取该行。`readline` 使用当前的（如果之前没有活动行编辑则使用默认的）编辑设置。
- `-i text`

  如果使用 `readline` 读取行，在编辑开始之前将 `text` 放入编辑缓冲区。
- `-n nchars`

  `read` 在读取 `nchars` 个字符后返回，而不是等待完整的行输入，但在遇到分隔符之前读取的字符少于 `nchars` 个。
- `-N nchars`

  `read` 在恰好读取 `nchars` 个字符后返回，而不是等待完整的行输入，除非遇到 `EOF` 或 `read` 超时。在输入中遇到的分隔符不被特殊处理，且在读取 `nchars` 个字符之前不会导致 `read` 返回。
- `-p prompt`

  在尝试读取任何输入之前，在标准错误上显示提示且不带尾随换行。只有当输入来自终端时才会显示提示。
- `-r`

  反斜杠不作为转义字符。反斜杠被视为行的一部分。特别是，反斜杠-换行的组合不用作行持续。
- `-s`

  静默模式。如果输入来自终端，字符不回显。
- `-t timeout`

  如果在 `timeout` 秒内没有读取完整的行输入（或指定数量的字符），导致 `read` 超时并返回失败。`timeout` 可以是带有小数点后小数部分的小数。此选项仅在 `read` 从终端、管道或其他特殊文件读取输入时有效；从普通文件读取时没有影响。如果 `read` 超时，将任何输入保存到指定的变量名中。如果 `timeout` 为 0，`read` 立即返回，而不尝试读取任何数据。如果指定的描述符上有可用输入，则退出状态为 0，否则为非零。如果超时，则退出状态大于 128。
- `-u fd`

  从文件描述符 `fd` 读取输入。

如果不提供 `name`，则将行分配给变量 `REPLY`。除非遇到文件结束、`read` 超时（在这种情况下返回码大于 128）、变量赋值错误（如赋值给只读变量）或提供的文件描述符无效，否则返回码为 0。

## `readonly`

`readonly [-af] [-p] [name=word]=`

给定的名称标记为只读；这些名称的值不能通过后续赋值更改。提供 `-f` 选项时，与名称对应的函数会被标记。`-a` 选项将变量限制为索引数组；`-A` 选项将变量限制为关联数组。如果两个选项都提供，则 `-A` 优先。如果没有给出 `name` 参数，或者提供了 `-p` 选项，则打印所有只读名称的列表。其他选项可将输出限制为只读名称子集。`-p` 选项导致输出以可以重用为设置当前变量的格式显示。当指定选项时，它们设置或取消属性。选项处理后的任何剩余参数被视为值并分配给 `$1`, `$2`, ... `$Sn`。

- `-a`

  自动将修改或创建的变量和函数标记为导出到后续命令的环境中。
- `-b`

  立即报告已终止作业的状态，而不是在下次提示符出现之前。这仅在作业控制启用时有效。
- `-e`

  如果管道（可能由单个命令组成）、列表或复合命令以非零状态退出，则立即退出。如果失败的命令是 `while` 或 `until` 关键字后面的命令列表部分、`if` 或 `elif` 保留字后面的测试部分、任何 `&&` 或 `||` 列表中执行中最后一个 `&&` 之后的命令，或命令返回值被 `!` 反转，如果非子 shell 的复合命令由于命令失败被忽略而返回非零状态，shell 不退出。如果设置了 `ERR` 陷，将在 shell 退出之前执行。此选项适用于 shell 环境和每个子 shell（见上文命令执行环境），并可能导致子 shell 在执行子 shell 中的所有命令之前退出。
- `-f`

  在 `posix` 模式下，仅列出 shell 变量。输出根据 `locale` 排序。只读变量无法重置。

## `return`

`return [n]`



导致函数停止执行并将 `n` 指定的值返回给调用者。如果省略 `n`，则返回状态是函数中执行的最后一个命令的状态。如果在函数外部使用 `return`，它将调用 `shell` 并返回脚本内部最后一个命令的退出状态。如果为 `return` 提供非数字参数，或在通过或 `source` 执行期间及之后使用，则返回状态为非零。与 `RETURN` 陷阱关联的命令（如果已设置）将在函数执行之后执行。

主体将受 `-e` 设置的影响，即使设置了 `-e` 且命令返回了失败状态也是如此。如果复合命令或 `shell` 函数在忽略 `-e` 的环境中执行时设置了 `-e`，则在命令或包含该函数的命令完成之前，该设置不会产生任何影响。

### `-f`

禁用路径名扩展。

### `-h`

在查找命令以执行时记住它们的位置。此选项默认启用。

### `-k`

所有以赋值语句形式出现的参数都将放在命令的环境中，而不只是位于命令名之前的参数。

### `-m`

监控模式。启用作业控制。对于支持的系统的交互式 `shell`，此选项默认开启（参见上文的“**作业控制**”部分）。所有进程都运行在一个独立的进程组中。当后台作业完成时，`shell` 会打印出包含其状态的行。

### `-n`

读取命令但不执行它们。这可以用于检查 `shell` 脚本的语法错误。交互式 `shell` 会忽略此选项。

### `-o option-name`

`option-name` 可以是以下之一：

- `a`

与 `-a` 相同。

- `braceexpand`

与 `-B` 相同。

- `emacs`

使用 `emacs` 风格的命令行编辑界面。如果 `shell` 是交互式的，则默认启用，除非启动 `shell` 时带有 `--noediting` 选项。这也会影响 `read -e` 使用的编辑界面。

- `errxit`

与 `-e` 相同。

- `errtrace`

与 `-E` 相同。

- `functrace`

与 `-T` 相同。

- `hashall`

与 `-h` 相同。

- `histexpand`

与 `-H` 相同。

- `history`

启用命令历史，如上文 **HISTORY** 部分所述。此选项在交互式 `shell` 中默认开启。

- `ignoreeof`

其效果等于执行了 `shell` 命令 `IGNOREEOF=10`（参见上文“**Shell 变量**”）。

- `keyword`

与 `-k` 相同。

- `monitor`

与 `-m` 相同。

- `noclobber`

与 `-C` 相同。

- `noexec`

与 `-n` 相同。

- `noglob`

与 `-f` 相同。

- `nolog`

目前被忽略。

- `notify`

与 `-b` 相同。

- `nounset`

与 `-u` 相同。

- `onecmd`

与 `-t` 相同。

- `physical`

与 `-P` 相同。

- `pipefail`

如果设置，管道的返回值是最后一个以非零状态退出的命令的值；如果管道中的所有命令都成功退出，则为零。此选项默认禁用。

- `posix`

更改 `bash` 的行为，使默认操作与 POSIX 标准一致以匹配该标准（`posix` 模式）。参见下文的“**另另**”部分，以获取详细说明 `posix` 模式如何影响 `bash` 行为的文档。

- `privileged`

与 `-p` 相同。

- `verbose`

与 `-v` 相同。

- `vi`

使用 `vi` 风格的命令行编辑界面。这也会影响 `read -e` 使用的编辑界面。

- `xtrace`

与 `-x` 相同。

如果提供了 `-o` 但没有提供 `option-name`，则打印当前选项的值。如果提供了 `+o` 但没有提供 `option-name`，会在标准输出上显示一系列用于重建当前选项设置的 `set` 命令。

### `-p`

开启特权模式。在此模式下，不会处理 `SENV` 和 `SBASH_ENV` 文件，`shell` 函数不会从环境中继承，如果环境变量中出现了 `SHELLOPTS`、`BASHOPTS`、`CDPATH`、`GLOBIGNORE` 变量，它们将被忽略。如果启动 `shell` 时有效用户（组）ID 不等于真实用户（组）ID，且未提供 `-p` 选项，将执行这些操作并将有效用户 ID 设置为真实用户 ID。如果在启动时提供了 `-p` 选项，有效用户 ID 将不会重置。开启此选项会导致有效用户和组 ID 设置为真实用户和组 ID。

### `-t`

执行一个命令后退出。

### `-u`

在执行参数扩展时，将特殊参数“`@`”和 `*` 以外的变量和参数视为错误。如果尝试对变量或参数进行扩展，`shell` 会打印错误信息，如果不是交互式的，则以非零状态退出。

### `-v`

在读取输入时打印输入行。

### `-x`

在执行每个简单命令、`for` 命令、`case` 命令、`select` 命令或算术 `for` 命令后，通过命令及其扩展后的参数或关联列表，显示 `PS4` 扩展后的值。

### `-B`

如果 `shell` 执行大括号扩展（参见上文“**大括号扩展**”）。这是默认的。

### `-C`

如果 `bash` 在使用 `>` 或 `&` 重定向操作符创建输出文件时，不覆盖现有文件。可以使用重定向 `>` 来覆盖此设置。

### `-E`

如果设置，任何 `on ERR` 都会被 `shell` 函数、命令替换以及在 `shell` 环境中执行的命令继承。在这种情况下，`ERR` 陷阱通常会被。

### `-H`

启用样式历史。此选项在 `shell` 是交互式时默认开启。

### `-P`

如果设置，`shell` 在执行更改当前工作目录的 命令时不会解析符号链接。它使用物理目录结构。默认情况下，`bash` 在命令更改当前目录时遵循逻辑目录链。

### `-T`

如果设置，`DEBUG` 和 `RETURN` 陷阱会被 `shell` 函数、命令替换以及在 `shell` 环境中执行的命令继承。在这种情况下，`DEBUG` 和 `RETURN` 陷阱通常会被。

### `--`

如果此选项后没有参数，则位置参数将被取消。否则，位置参数将设置为这些参数，即使它们以 `-` 开头。

### `-`

标记选项结束，导致所有剩余参数被分配给位置参数。关闭 `-x` 和 `-v` 选项。如果没有参数，位置参数保持不变。

### `-s`

启用（设置）`eachname`。

### `-u`

禁用（取消设置）`eachname`。

如果在使用 `-s` 或 `-u` 时没有提供 `optname` 参数，`shop` 只显示相应设置或取消设置的选项。

### `-q`

抑制正常输出（静默模式）；返回状态指示 `optname` 是否已设置。如果在使用 `-q` 时给出多个 `optname` 参数，如果所有 `optnames` 都启用，则返回状态为零，否则非零。

### `-0`

为 `set` 命令的 `-0` 限制 `optname` 的值。

在设置或取消选项时，除非 `optname` 有效，否则返回状态为零。

### `autcd`

如果设置，与目录同名的命令将作为 `cd` 命令执行。此选项仅用于交互式 `shell`。

### `cdable_vars`

如果设置，`cd` 内置命令中不是目录的参数将被假设为变量名，其值为目标目录。

### `cdspell`

如果设置，`cd` 命令中目录组件拼写的小错误将被修正。检查的错误包括字符易换、缺失字符和一个多余字符。如果发现修正，将打印修正后的文件名并继续执行。此选项仅用于交互式 `shell`。

### `checkhash`

如果设置，`bash` 在尝试执行哈希表中的命令之前会检查该命令是否存在。如果哈希命令不再存在，将执行正常的路径搜索。

### `checkjobs`

如果设置，`bash` 在退出交互式 `shell` 前会列出任何停止和运行作业的状态。如果有任何作业正在运行，这将导致延迟退出，直到在没有后续命令的情况下再次尝试退出（参见上文“**作业控制**”）。如果有作业已停止，`shell` 总是延迟退出。

### `checkwins`

如果设置，`bash` 在每个命令执行后都会检查窗口大小，并在时更新 `LINES` 和 `COLUMNS` 的值。

### `cmdhist`

如果设置，`bash` 尝试将多行命令的所有行保存到同一个历史记录条目中。这允许对多行命令进行重新编辑。

### `compat31`

如果设置，`bash` 在处理针对 `[[` 条件命令的 `=~` 运算符的引号参数，以及在使用 `[[` 条件命令的 `<` 和 `>` 运算符进行特定区域的比较时，其行为将变为类似于 3.1 版本。`bash-4.1` 之前的 `bash` 版本使用 ASCII 排序和 `strcmp(3)`；`bash-4.1` 及更高版本使用当前区域设置的排序序列和 `strcoll(3)`。

### `compat32`

如果设置，`bash` 在使用 `[[` 条件命令的 `<` 和 `>` 运算符进行特定区域设置的字符串比较时，其行为将变为类似于 3.2 版本（参见上述项目）。

### `compat40`

如果设置，`bash` 在使用 `[[` 条件命令的 `<` 和 `>` 运算符进行特定区域设置的字符串比较时（参见 `compat31` 的描述）以及中断命令列表的影响时，其行为将变为类似于 4.0 版本。`bash 4.0` 及更高版本会在 `shell` 接收到中断信号时中断列表；之前的版本则继续执行列表中的下一个命令。

### `compat41`



如果设置，`bash` 在 `posix` 模式下，将双引号内参数扩展中的单引号视为特殊字符。单引号必须匹配（偶数个），且单引号之间的字符被视为已引号的。这是通过版本 4.1 为止 `posix` 模式的行为。之前的版本保持默认的 `bash` 行为。

## compat42

如果设置，`bash` 在使用模式替换扩展时，不会使用移除引号的方法处理替换字符串。

## complete_fullquote

如果设置，`bash` 在执行补全时，会对文件名和目录名中的所有元字符加上引号。如果未设置，当这些元字符出现在待补全的 shell 变量引用中，`bash` 将将美元符号等元字符从补全文件名的加引号字符集中移除。这意味着展开到目录的变量名中的美元符号将不会加引号；然而，文件名中出现的任何美元符号也不会被加引号。这仅在 `bash` 使用反斜杠对补全的文件名加引号时生效。该变量默认开启，这是 4.2 版本中 `bash` 的默认行为。

## direxpand

如果设置，`bash` 在执行补全时，会将目录名替换为单词扩展的结果。这会改变 `readline` 编辑缓冲区的内容。如果未设置，`bash` 将尝试保留用户输入的内容。

## dirspell

如果设置，如果最初提供的目录名不存在，`bash` 在单词补全期间尝试对目录名进行拼写检查。

## dotglob

如果设置，`bash` 在路径名扩展的结果中包含以 `.` 开头的文件。

## execfail

如果设置，非交互式 shell 如果无法执行作为 `exec` 内置命令参数的文件，则将不会退出。交互式 shell 在 `exec` 失败时不会退出。

## expand_aliases

如果设置，将按照 ALIASES 节下的的描述展开别名。此选项在交互式 shell 中默认启用。

## extdebug

如果设置，将启用旨在供调试器使用的行为：

- 1. `declare` 内置命令的 `F` 选项将显示与作为参数提供的每个函数名对应的源文件名和行号。
- 2. 如果由 `DEBUG` 陷阱运行的命令返回非零值，则将跳过不执行下一个命令。
- 3. 如果由 `DEBUG` 陷阱运行的命令返回值为 2，且 shell 正在执行子程序（shell 函数或通过 `.` `source` 内置命令执行的 shell 脚本），则模拟一次 `return` 调用。
- 4. `BASH_ARGC` 和 `BASH_ARGV` 将按照上述描述进行更新。
- 5. 启用函数跟踪：通过 (`command`) 调用的命令替换、shell 函数和子 shell 将继承 `DEBUG` 和 `RETURN` 陷阱。
- 6. 启用错误跟踪：通过 (`command`) 调用的命令替换、shell 函数和子 shell 将继承 `ERR` 陷阱。

`extglob` 如果设置，将启用上述在 `Pathname Expansion`（路径名扩展）下描述的扩展模式匹配功能。`extquote` 如果设置，在由双引号包围的 `${parameter}` 扩展中将执行 `'$string'` 和 `"$string"` 引号处理。此选项默认启用。`failglob` 如果设置，路径名扩展期间模式无法匹配文件名时将导致错误。`force_ignore` 如果设置，`FIGNORE` shell 变量指定的后缀会导致在执行补全时忽略某些单词，即使这些忽略的单词是唯一可能的补全。参见上文 SHELLVARIABLES 中 `IGNORE` 的描述。`globasciranges` 如果设置，在模式匹配括号表达式（参见 Pattern Matching）中，当不考虑排序序列时，范围表达式的行为类似于传统的 C 区域，`b` 将不会与 `A` 和 `B` 冲突，且大小写 ASCII 字符将聚集。`globstar` 如果设置，路径名扩展上下文中的模式 ` *` 将匹配所有文件以及零或多个目录和子目录。如果模式后跟着一个 `/`，则只匹配目录和子目录。`gnu_errfmt` 如果设置，shell 错误消息将以标准 GNU 错误消息写入：`histappend` 如果设置，shell 退出时历史列表将被追加到 `HISTFILE` 变量值命的文件，而不是覆盖文件。`histreet` 如果设置且使用了 `readline`，用户将有机会编辑失败的历史替换。`histverify` 如果设置且使用了 `readline`，历史替换的结果不会立即传递给 shell 解析器。相反，结果生成的行被加载到 `readline` 缓冲区中，允许进一步修改。`hostcomplete` 如果设置且使用了 `readline`，当命令 `@` 被补全时，`bash` 将尝试执行主机名补全（参见 READING）。`hupexit` 如果设置，交互式 shell 退出时向所有作业发送 `SIGHUP`。`interactive_comments` 如果设置，允许以 `#` 开头导致交互式 shell 中的剩余字符被忽略（参见 COMMENTS）。此选项默认启用。`lastpipe` 如果设置，且作业控制未激活，shell 将运行管道的最后一个命令。`lithist` 如果设置且启用了 `cmdhist` 选项，多行命令将以换行符而非分号分隔保存到历史中。`login_shell` 在作为登录 shell 时设置此选项（参见 INVOCATION）。该值不可更改。`mailwarn` 如果设置，且 `bash` 自从上次检查以来有邮件访问，则显示“Mail in mailbox”消息。`no_empty_completion` 如果设置且使用了 `readline`，当空行尝试补全时 `bash` 将不会搜索。`nocaseglob` 如果设置，`bash` 在执行路径名扩展时以不区分大小的方式匹配文件名（参见 Pathname Expansion）。`nocatch` 如果设置，在执行 `[[ conditional]]` 时 `bash` 以大小敏感的方式匹配模式。`nullglob` 如果设置，`bash` 允许匹配无文件的模式扩展为空字符串，`progcomp` 如果设置，将启用可编程补全（参见 Programmable Completion）。此选项默认启用。`promptvars` 如果设置，提示字符串在按照 PROMPTING 中的描述展开后，将进行参数扩展、命令替换、算术扩展和引号移除。此选项默认启用。`restricted_shell` shell 在受限模式启动时设置此选项（参见下文 RESTRICTED SHELL）。该值不可更改。在执行启动文件时不会重置，允许启动文件发现 shell 是否受限。`shift_verbose` 如果设置，`bash` 会打印参数数量。`sourcepath` 如果设置，`source` (`.`) builtin 可以找到作为参数提供的文件所在的目录。此选项默认启用。`xpg_echo` 如果设置，`echo` 默认展开反斜线转义序列。`suspend [-f]` 挂起此 shell 的执行直到接收 `SIGCONT` 信号。登录 shell 不能挂起；可以使用 `-f` 选项覆盖此设置，如果未挂起或作业控制未启用。`test [ expr ]` 除非是登录 shell，否则返回状态 0。根据条件表达式 `expr` 的评估结果返回状态 0（真）或 1（假）。每个运算符必须是独立的参数。表达式由上述 CONDITIONALEXPRESSIONS 下描述的原始项组成。`test` 不接受任何选项，它也不接受并忽略将 `—` 视为选项结束标志的参数。

表达式可以使用以下操作符组合，按优先级从高到低列出。求值取决于参数的数量；见下文。当参数有五个或更多时，会使用操作符优先级。

- `+ * expr`: 如果 `expr` 为假，则结果为真。
- `+ * ( expr )`: 取 `expr` 的值。这可以用于覆盖操作符的正常优先级。
- `+ * expr1 - expr2`: 如果 `expr1` 和 `expr2` 都为真，则结果为真。
- `+ * expr1 -o expr2`: 如果 `expr1` 或 `expr2` 其中一个为真，则结果为真。

# 根据参数数量的一组规则来测试和评估条件表达式。

- `+ * 0 个参数`: 表达式为假。
- `+ * 1 个参数`: 当且仅当参数不为空时，表达式为真。
- `+ * 2 个参数`: 如果第一个参数是 `I`，则当且仅当第二个参数为空时，表达式为真。如果第一个参数是上述 CONDITIONALEXPRESSIONS 下列出的一元条件操作符之一，则当一元测试为真时表达式为真。如果第一个参数不是有效的条件操作符，则表达式为假。
- `+ * 3 个参数`: 按照顺序应用以下条件。如果第二个参数是上述 CONDITIONALEXPRESSIONS 下列出的二元条件操作符之一，表达式的结果是用第一个和第三参数作为操作数的二元测试的结果。当有三个参数时，`-a` 和 `-o` 操作符被视为二元操作符。如果第一个参数是 `!`, 则该值为使用第二个和第三参数进行二参数测试的反反。如果第一个参数恰好是 `I`，则结果是第二个参数的一元测试。否则，表达式为假。
- `+ * 4 个参数`: 如果第一个参数是 `I`，则结果是由剩余参数组成的三参数表达式。否则，表达式将根据上述规则按照优先级进行解析和评估。



- `+ * 5 个或更多参数`: 表达式将根据上述规则按照优先级进行解析和评估。

当 `test` 或 `[` 使用时，`<` 和 `>` 操作符使用 ASCII 排序进行字典序排序。

`times`: 打印 shell 以及从 shell 运行的进程的累计用户时间和系统时间。返回状态为 `0`。

`trap [-lp] [[arg] sigspec ...]`: 当 shell 接收到信号 `sigspec` 时，命令 `arg` 将读取并执行。如果 `arg` 缺失（且仅有一个 `sigspec`）或为 `-`，则指定的信号将重置为其原始分配（进入 shell 时的值）。如果 `arg` 是每个 `sigspec` 指定的空字符串，则 shell 和被调用的命令将忽略它。如果 `arg` 不存在且提供了 `-p`，则显示与每个 `sigspec` 关联的 `trap` 命令。如果没有提供任何参数或给出了 `-p`，`trap` 将打印与每个信号名称关联的命令列表。每个 `sigspec` 或是 `<signal.h>` 中定义的名称，或是信号数字。信号对大小写敏感，`sigspec` 前缀是可选的。

如果 `sigspec` 是 `EXIT` (`0`)，则在退出 shell 时执行命令 `arg`。如果 `sigspec` 是 `DEBUG`，则在每个简单命令之前、`case` 命令之前、`select` 命令之前、每个算术命令之前，以及 shell 函数中的第一个命令之前（见上文 `SHE GRAMMAR`）执行命令 `arg`。参阅 `extdebug` 选项的描述以了解其对 `DEBUG` trap 影响的影响。如果 `sigspec` 是 `RETURN`，则每当 shell 或使用 `或` `source` 内置命令执行的脚本结束时，执行命令 `arg`。

如果 `sigspec` 是 `ERR`，每当管道（可能由简单命令组成）、列表或复合命令返回非零退出状态时，都会执行命令 `arg`，但须满足以下条件。如果失败的命令是 `while` 或 `until` 关键字后后续命令列表的一部分、`if` 语句中 `test` 的一部分、`&&` 或 `||` 列表中执行的命令的一部分（排除执行最后的 `&&` 或 `||` 的命令，或管道中除最后一个以外的任何命令），或者命令的返回值被取反 `!`，则不执行 `ERR` trap。`erexit` (`-e`) 选项遵循相同的条件。

在进入 shell 时被忽略的信号无法被捕获、重置或列出。被捕获但未被忽略的信号在创建子壳或子进程环境时，将重置为为的原始值。如果任何 `sigspec` 无效，则返回状态为假；否则 `trap` 返回真。

`type [-aft name [name ...]]`: 在没有选项的情况下，指示每个名称如何被解释为命令名。如果使用了 `-t` 选项，`trap` 将打印一个字符串，如果 `name` 是别名（`aliases`）、关键字（`keyword`）、函数（`function`）、内置命令（`builtin`）或文件（`file`）之一；如果未找到 `name`，则不打印任何内容并返回错误的退出状态。如果使用了 `-p` 选项，`trap` 将返回如果 `name` 指定为命令名将执行的磁盘文件的值，或者如果 `type -t name` 不返回文件则返回空。如果使用了 `-P` 选项，当 `type -t name` 不返回文件时，强制对每个名称进行搜索。如果命名了命令，`-p` 和 `-P` 将返回其哈希值，该哈希值不一定是出现在 `PATH` 中的第一个文件。如果使用了 `-a` 选项，`trap` 将打印所有包含名为 `name` 的可执行文件的位置。这包括别名和函数，且当仅未使用使用 `-p` 选项时。在使用 `-a` 时不会咨询已哈希的命令。`-f` 选项抑制 shell 函数查找，与命令内置命令一样。如果所有参数都为假（即未找到），或其中任何一个未被找到，则 `type` 返回真。

`ulimit [-Hastabcdeff [name ...]]`: 对 shell 及其启动的进程可用的资源提供控制。限制。如果提供了 `-p` 或 `-S`，则显示软限制。如果未提供模式，则设置硬限制。如果模式以数字开头，则解释为八进制数；否则解释为符号模式。如果省略模式，则打印当前软限制。`-S` 选项导致以符号形式打印；默认输出为八进制数。如果提供了 `-p` 选项且省略模式，则输出可能使用的格式。如果指定了资源，则设置硬限制或软限制。如果未指定资源，其解释如下：

- `a`: 所有当前限制
- `b`: 最大缓冲区大小
- `c`: 最大核心文件大小
- `d`: 最大数据段大小
- `e`: 最大调度优先级（nice）
- `f`: 由 shell 启动的核心文件大小
- `i`: 最大打开数量
- `l`: 最大大小
- `m`: 最大驻留集大小
- `n`: 最大数量
- `p`: 管道大小
- `q`: 最大数量
- `r`: 最大实时优先级
- `s`: 最大大小
- `t`: 最大 CPU 时钟时间
- `v`: 最大虚拟内存
- `x`: 最大数量
- `T`: 最大数量

`umask [-p] [-S] [mode]`: 用户创建掩码设置为模式。如果模式是数字，则解释为八进制数；否则解释为符号掩码。如果省略模式，则打印当前掩码值。`-S` 选项导致掩码以符号形式输出；默认输出为八进制。如果提供了 `-p` 选项且省略模式，则输出可能使用的格式。如果模式成功更改或未提供参数，返回状态为 `0`。

`alias [-a] [name ...]`: 从定义的列表中删除每个名称。如果提供了 `-a`，则删除所有别名。除非名称不是定义的别名，否则返回状态为真。

`unset [-fv] [-n] [name ...]`: 删除每个名称对应的变量或函数。如果给了 `-v` 选项，名称指向 shell 变量，并删除该变量。只有变量无法取消。如果指定了 `-f`，每个名称指向 shell 函数，并删除函数定义。如果提供了 `-n` 选项且 `name` 是名称引用（nameref）属性的变量，则将取消其引用的变量。如果提供了 `-f` 选项，`-n` 无效。如果没有提供任何选项，每个名称指向变量；如果没有没有该变量，则取消该名称。每个被取消的变量或函数将从传递给后续命令的环境中移除。如果取消了 `COMP_WORDBREAKS`、`RANDOM`、`SENS`、`LINENO`、`HISTCD`、`FUNGROUP`、`GROUPS` 或 `DIRSTACK` 中的任何一个，它们将丢失符号属性，除非它们随后被重置。除非名称是只读的，否则退出状态为真。

`wait [-n] [n ...]`: 等待每个指定的子进程并返回。每个 `n` 可以是进程 ID 或作业规范；如果给出了作业，则等待该作业管道中的所有进程。如果没有给出 `n`，则等待所有当前活跃的进程，返回状态为零。如果提供了 `-n` 选项，则等待任何作业终止并返回其状态。如果 `n` 指定了不存在的进程或作业，返回状态为 `127`。否则，返回最后一个等待的进程或作业的退出状态。

### 参见

`bash(1)`, `sh(1)`

# BASH

## 名字

`bash` - GNU Bourne-Again SHell

## 语法

```
bash [options] [command_string | file]
```

## 版权所有

Bash 的版权所有 (C) 1989-2013 由 Free Software Foundation, Inc.。

### 描述

**Bash** 是一个兼容 **sh** 的命令行语言解释器，用于执行从标准输入或文件中读取的命令。**Bash** 还整合了来自 Korn shell 和 C shell (**ksh** 和 **csh**) 的有用功能。

**Bash** 旨在实现 IEEE POSIX 规范（IEEE 标准 1003.1）中 Shell 和实用程序部分的合规版本。**Bash** 可以配置为默认符合 POSIX 标准。

### 选项

在 **set** 内置命令描述中记录的所有单字符 shell 选项都可以在调用 shell 时作为选项使用。此外，**bash** 在调用时还会解释以下选项：

- `-c`

如果存在 `-c` 选项，则从第一个非选项参数 `command_string` 中读取命令。如果 `command_string` 之后还有参数，它们将被分配给位置参数，从 `$0` 开始。

- `-i`

如果存在 `-i` 选项，shell 是**交互式**的。

- `-l`

使 **bash** 如同作为登录 shell（login shell）被调用一样运行（参见下文 **INVOCATION**）。

- `-r`

如果存在 `-r` 选项，shell 将变为**受限制的**（参见下文 **RESTRICTED SHELL**）。

- `-s`

如果存在 `-s` 选项，或者在选项处理后没有剩余参数，则从标准输入读取命令。此选项允许在调用交互式 shell 时设置位置参数。

- `-D`

在标准输出上打印出以 `$` 开头的双引号字符串列表。当当前区域（locale）不是 **C** 或 **POSIX** 时，这些字符串将进行语言翻译。这意味着带有 **-n** 选项；不会执行任何命令。

- `[-+]O [shop_option]`



*shop_option* 是 **shopt** 内置命令接受的 shell 选项之一（参见下文 **SHELL BUILTIN COMMANDS**）。如果存在 *shop_option*，**-O** 设置选项的值；**+O** 重置它。如果未提供 *shop_option*，则在标准输出上打印 **shopt** 接受的 shell 选项名称和值。如果调用选项为 **+O**，输出将以可重用的格式显示。

-- 标记选项的结束并禁用后续的选项处理。-- 之后的任何参数都将被视为文件名和参数。参数 - 等同于 --。

Bash 还会解释许多多字符选项。这些选项必须在命令行中出现在单字符选项之前才能被识别。

- --debugger

安排在 shell 启动之前执行调试器配置文件。开启扩展调试模式（参见下文对 **bash** 内置命令中 **extdebug** 选项的描述）。

- --dump-po-strings

等同于 **D**，但输出为 GNU **gettext po**（可移植对象）文件格式。

- --dump-strings

等同于 -D。

- -help

在标准输出上显示帮助并成功退出。

- -init-file file

- -rcfile file

如果 shell 是交互式的，则从文件而非标准的个人初始化文件 ~/.bashrc 执行命令（参见下文 **INVOCATION**）。

- -login

等同于 -l。

- -noediting

当 shell 是交互式的时，不使用 GNU readline 库读取命令行。

- -nprofile

不读取系统级启动文件 /etc/profile 或任何个人初始化文件 ~/.bash_profile, ~/.bash_login 或 ~/.profile。默认情况下，bash 在作为登录 shell 调用时会读取这些文件（参见下文 **INVOCATION**）。

- -norc

如果 shell 是交互式的，则不读取并执行初始化文件 ~/.bashrc。当 shell 作为 sh 调用时，此选项默认开启。

- -posix

更改 bash 的行为，使默认操作与 POSIX 标准不同的之处符合该标准（posix 模式）。参见下文 **SEE ALSO** 以获取详细说明 posix 模式如何影响 bash 行为的文档。

- -restricted

shell 将变为受限制的（参见下文 **RESTRICTED SHELL**）。

- -rpm-requires

生成运行 shell 脚本所需的文件列表。这意味着包含了 '-n' 并且受到编译时错误检查相同的限制；命令替换、条件表达式和 eval 内置命令不会被解析，因此可能会漏掉某些依赖。

- -verbose

等同于 -v。

- -version

在标准输出上显示此 bash实例的版本信息并成功退出。

### 参数

如果在选项处理后仍有参数，且未提供 -c 或 -s 选项，则第一个参数被假设为包含 shell 命令的文件名。如果以这种方式调用 **bash**，$0 被设置为文件名，位置参数被设置为剩余参数。**Bash** 从该文件中读取并执行命令，然后退出。**Bash 的退出状态是脚本中执行的最后一个命令的退出状态。如果没有执行任何命令，则退出状态为 0。**

# 调用

使用 -login 选项启动登录 shell。不带非选项参数或使用 -i 选项启动交互式 shell。以下段落描述了 bash 如何执行其启动文件。文件名中的波浪号如下文“波浪号展开”（Tilde Expansion）所示进行展开。

当 bash 作为交互式登录 shell 或带有 -login 选项的非交互式 shell 调用时，它首先从 /etc/profile 读取并执行命令（如果文件存在）。读取之后，它会按顺序查找 ~/.bash_profile、 ~/.bash_login 和 ~/.profile，并读取和执行第一个存在且可读的文件。在启动 shell 时可以使用 —profile 选项来抑制这种行为。

当登录 shell 退出时，bash 会从 ~/.bash_logout 和 /etc/bash_logout 读取并执行命令（如果文件存在）。

当启动一个非登录 shell 的交互式 shell 时，bash 会从 ~/.bashrc 读取并执行命令（如果文件存在）。这可以通过 -norc 选项抑制。—rcfile 选项将强制 bash 从文件而非 ~/.bashrc 读取并执行命令。

当 bash 以非交互方式启动（例如运行 shell 脚本）时，它会查找环境中的 BASH_ENV 变量，如果其中存在，则使用展开后的值作为读取和执行的文件名。Bash 的行为如同执行了以下命令：

```
if [ -n "$BASH_ENV" ]; then "$BASH_ENV"; fi
```

但不会使用 PATH 变量的值来搜索文件名。

如果以 sh 的名称调用 bash，它将尝试尽可能模拟历史版本 sh 的启动行为，同时符合 POSIX 标准。当作为交互式登录 shell 或带有 -login 选项的非交互式 shell 调用时，它将按顺序从 /etc/profile 和 ~/.profile 读取并执行命令。可以使用 —profile 选项来抑制这种行为。当以 sh 的名称作为交互式 shell 调用时，bash 会查找 ENV 变量，如果已定义，则使用展开后的值作为读取和执行的文件名。由于作为 sh 调用的 shell 不尝试读取和执行任何其他启动文件，因此 —rcfile 选项无效。以 sh 名称调用的非交互式 shell 不尝试读取任何其他启动文件。当作为 sh 调用时，bash 在读取启动文件后进入 posix 模式。

当 bash 以 posix 模式启动时（例如使用 `--posix` 命令行选项），它将遵循 POSIX 标准来处理启动文件。在此模式下，交互式 shell 会扩展 `ENV` 变量，并从展开后的值命名的文件中读取并执行命令。不会读取其他启动文件。

Bash 会尝试判断其是否是由于远程 shell 守护进程（通常是 rsh 或 ssh）在标准输入连接到网络连接的情况下运行的。如果 bash 确定自己是以这种方式运行的，那么只要 `~/.bashrc` 文件存在并可读，它将从该文件读取并执行命令。当作为 `sh` 被调用时，它不会执行此操作。可以使用 `--norc` 选项来抑制这种行为；虽然可以使用 `rsh` 或 `ssh --rcfile` 选项来强制读取另一个文件，但 rsh 或 ssh 通常不会带上这些选项启动 shell，也不允许指定这些选项。

如果启动 shell 时有效用户（组）ID 不等于实际用户（组）ID，且未提供 `-p` 选项，则不会读取任何启动文件，shell 函数不会从环境中继承，如果环境中出现了 `SHELLOPTS`、`BASHOPTS`、`CDPATH` 和 `GLOBIGNORE` 变量将被忽略，且有效用户 ID 将设置为实际用户 ID。如果在调用时提供了 `-p` 选项，则启动行为相同，但有效用户 ID 不会被重置。

# 定义

以下定义在本文的其余部分中使用。

- 空格 (blank)

空格或制表符。

- 字 (word)

被 shell 视为单个单元的字符序列。也称为标记 (token)。

- 名称 (name)

由字母、数字和下划线组成，并以字母或下划线开单词。也称为**标识符**(identifier)。

- 元字符 (metacharacter)

在未加引号时分隔单词的字符。属于以下之一：

+ | & ; ( ) < space tab

- 控制操作符 (control operator)

执行控制函数的标记。它是以下符号之一：

```
|| && &&; ; ( )||<&<
```

# 保留字

保留字是对 shell 具有特殊含义的单词。当以下单词在未加引号，且是简单命令的第一个单词（见下文 SHELL GRAMMAR）或 `case` 或 `for` 命令的第三个单词时，会被识别为保留字：

```
! case coproc do done elif else esac fi for function if in select then until while { } time [ ]
```

# Shell 语法

## 简单命令

命令是一系列可选的变量赋值，后跟由空格分隔的单词和重定向，并由控制操作符终止。第一个单词指定要执行的命令，并作为参数 0 传递。其余单词作为参数传递给调用的命令。

简单命令的返回值是它的退出状态；如果命令被信号 `n` 终止，则返回 `128+n`。

## 管道

管道是由控制操作符 `|` 或 `|&` 分隔的一个或多个命令序列。管道的格式为：

```
[time [-p]] [!] command [|||] command2 ...
```



`command`的标准输出通过管道连接到`command2`的标准输入。此连接在命令指定的任何重定向之前完成（见下文`REDIRECTION`）。如果使用`|&`，`command`的标准错误及其标准输出将通过管道连接到`command2`的标准输入；它是`2>&1`的简写。这种标准错误到标准输出的隐式重定向是在命令指定的任何重定向之后执行的。

管道的返回状态是最后一个命令的退出状态，除非启用了`pipefail`选项。如果启用了`pipefail`，管道的返回状态是最后一个非零状态退出的命令的值，如果所有命令都执行成功。如果保留字`!`位于管道之前，则管道的退出状态是上述退出状态的逻辑取反。shell会在管道中的所有命令终止之前等待一个值。

如果保留字位于管道之前，则报告其执行时消耗的经过时间以及用户时间和系统时间。`-p`选项会将输出格式更改为`POSIX`指定格式。当shell处于`posix`模式时，如果下一个标记以`-`开头，它不会将`time`识别为保留字。`TIMEFORMAT`变量可以设置为指定显示计时信息的格式字符串；见下文`TIMEFORMAT`变量的描述。

当shell处于`posix`模式时，`time`可能会跟一个换行符。在这种情况下，shell显示shell及其子进程消耗的总用户时间和系统时间。`TIMEFORMAT`变量可用于指定时间信息的格式。

管道中的每个命令都作为一个单独进程执行（即在子shell中执行）。

## 列表

在这些列表操作符中，`&&`和`||`优先级相等，随后是`;`和`&&`，它们的优先级相等。

列表中可以用一个或多个换行符代替分号来分隔命令。

如果命令由控制操作符`&&`终止，shell在后台执行该命令且不等待其完成，且返回状态为0。由`;`分隔的命令顺序执行；shell会等待每个命令终止。返回状态是最后一个执行的命令的退出状态。

`AND`列表和`OR`列表分别是由`&&`和`||`控制操作符分隔的一个或多个管道序列。`AND`和`OR`列表按左结合律执行。`OR`列表的形式为：

```
command1 && command2
```

`AND`列表的形式为：

```
command1 || command2
```

列表的返回状态是最后一个执行命令的退出状态。

## 复合命令

复合命令是包含`{}`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`()`中的命令序列。命令在子shell中执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`[]`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含反引号``的命令序列。命令在子shell中执行，命令的标准输出作为命令的替换。

复合命令是包含`$()`中的命令序列。命令在子shell中执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`if-then-else`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`while-do-done`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`for-do-done`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`case-esac`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`function-definition`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`test`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`[[`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`((`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

## 条件表达式

以下定义在本文的其余部分中使用。

- 空格 `blank`

空格或制表符。

- 字 `word`

被shell视为单个单元的字符序列。也称为标记 `token`。

- 名称 `name`

由字母、数字和下划线组成，并以字母或下划线开头的单词。也称为标识符 `identifier`。

- 元字符 `metacharacter`

在未加引号时分隔单词的字符。属于以下之一：

```
+ | & ; ( ) < space tab
```

- 控制操作符 `control operator`

执行控制函数的标记。它是以下符号之一：

```
|| && &&; ; ( )||<&<
```

复合命令是包含`{ [[`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`{ ((`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`[[`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

复合命令是包含`((`中的命令序列。命令按顺序执行，复合命令的返回状态是最后一个命令的退出状态。

返回表达式的值。这可以用于覆盖运算符的正常优先级。

`! expression`

如果表达式为假，则返回真。

`expression1 && expression2`

如果`expression1`和`expression2`都为真，则返回真。

`expression1 || expression2`

如果`expression1`或`expression2`中任一个为真，则返回真。

如果`expression1`的值足以确定整个条件表达式的值，则`&&`和`||`运算符不会计算`expression2`。



`for name [ [ in word ... ] ] ; do list ;` `in` 之后的单词列表将被展开，生成一个项列表。变量 `name` 将依次赋值为该列表的每个元素，并且每次执行 `list`。如果省略了 `in`，则 `for` 命令将为每个执行的位置参数执行一次（见下文 PARAMETERS 部分）。返回状态是最后一个执行的命令的退出状态。如果 `in` 之后的项展开结果为空列表，则不执行任何命令，返回状态为 0。

`for (( expr1 ; expr3 )) ; do list ;` 首先，根据下方“算术评估”（ARITHMETIC EVALUATION）部分描述的规则对算术表达式 `expr1` 进行评估。然后反复评估算术表达式 `expr2` 直到其值为零。每当 `expr2` 评估为非零值时，都会执行 `list`。如果省略，其行为表现于评估为 1。返回值为最后一个执行的命令的退出状态，或者如果任何表达式无效，则返回非零。

`select name [ in word ] ; do list ;` `in` 之后的单词列表将被展开，生成一个项列表。设置的单词将打印在标准错误上，每个单词前都有一个数字。如果省略了 `in`，则打印位置参数（见下文 PARAMETERS 部分）。然后显示 `Ps3` 提示符，并从标准输入读取一行。如果该行包含与显示的单词之一对应的数字，则 `name` 的值将设置为该单词。如果该行为空，则再次显示单词和提示符。如果达到 EOF（文件结束符），则将命令行读入 `REPLY` 中。读取到的任何其他值都无法设置为空。在每次选择后执行 `list`，直到执行 `break` 命令为止。`select` 的退出状态是 `list` 中最后一个执行的命令的退出状态，如果没有执行任何命令，则为 0。

`case word in [ pattern | ]` 尝试匹配每个模式，使用相同的路径名扩展规则（见下文路径名扩展/Pathname Expansion 部分）。`word` 使用波浪号替换、参数和变量扩展、算术替换、命令替换和进程替换进行展开。每个检查的模式都使用波浪号扩展、参数和变量扩展、算术替换、命令替换和进程替换进行展开。如果启用了 `nocematch` 选项，则匹配将不考虑字母字符的大小写。当找到匹配时，执行相应的 `list`。如果使用了 `;;` 运算符，则在第一个模式匹配后将不再尝试后续的匹配。使用 `&` 代替 `;;` 会导致执行到下一组模式的 `list`。使用 `&` 代替 `;` 会导致 shell 跳到语句中的下一个模式列表（如果有的话），并在匹配成功时执行任何相关的 `list`。如果没有模式匹配，则退出状态为 0。否则，它是 `list` 中最后一个执行的命令的退出状态。

`if list; then list; [ else list; then list]; ... [ else list; fi` 如果执行了 `list`。如果其退出状态为 0，则执行 `list`。否则，依次执行每个 `list`，如果其退出状态为 0，则执行对应的 `list` 并完成命令。如果存在 `else list`，则执行 `else list`。退出状态是最后一个执行的命令的状态，如果没有命令测试为真，则为 0。

`while list-1; do list-2; do until list-1; do list-2; done` 只要 `list-1` 中的命令返回退出状态为 0，命令就会持续执行 `list-2`。该单元与 `while` 命令相同，区别是测试取反了；只要 `list-1` 中的命令返回非零退出状态，就会执行 `list-2`。`while` 和 `until` 命令的退出状态是最后一个执行的命令的退出状态。

Coprocess 只要 `list-1` 中的命令返回退出状态为 0，命令就会持续执行 `list-2`。该单元与 `while` 命令相同，区别是测试取反了；只要 `list-1` 中的命令返回非零退出状态，就会执行 `list-2`。`while` 和 `until` 命令的退出状态是最后一个执行的命令的退出状态。

`coproc [name] command`

# Shell Function Definitions

函数是一个可以通过以下方式调用的对象，`coproc` 命令是异步执行的。函数使用以下语法定义：

```bash
name ()
```

或者

```bash
function name
```

函数的体包含在大括号 `{ }` 中。函数通过其名称后接任意参数进行调用。传递给参数赋值为 `$1,$2` 等。函数可以使用 `local` 关键字定义局部变量。函数的退出状态是最后一个执行的命令的状态。

# Comments

在非交互式 shell 中，或启用了 `interactive_comments` 选项的交互式 shell 中，以 `#` 开头的单词会导致该行之后的所有字符被忽略。`interactive_comments` 选项在交互式 shell 中默认开启。

# Quoting

引用用于移除字符或单词的特殊含义。引用可以禁用字符的特殊处理，防止保留字被识别，并防止参数扩展。

DEFINITIONS 下列出的每个元字符对 shell 有特殊含义。在使用历史扩展功能时（见 HISTORY EXPANSION 部分），历史扩展字符 `!` 必须引用。

有三种引用机制：转义字符、单引号和双引号。

非引号的反斜杠是转义字符。它保留后续字符的字面值，`<newline>` 除外。如果出现 `<newline>` 对且反斜杠未引号，`\<newline>` 被视为行延续（即它从输入流中移除并实际上被忽略）。

单引号保留内部每个字符的字面值。单引号内不允许出现单引号，即使前面有反斜杠。

双引号保留内部所有字符的字面值，但 `$`, `\` 以及在启用历史扩展时的 `!` 外。`$` 和 `\` 在双引号内保留其特殊含义。反斜杠仅在跟随 `$`, `\` 或 `<newline>` 时才保留其特殊含义。双引号可以通过前面的反斜杠进行引用。

特殊参数 `*` 和 `@` 在双引号中具有特殊含义（见下文 PARAMETERS 部分）。

形式为 `'$string'` 的单词被特殊处理。单词展开为 string，并按照 ANSI C 标准替换反斜杠转义字符。反斜杠序列（如果存在）的解码如下：

```
\a alert (bell)
\b backspace
\e escape
\E an escape character
\f form feed
```

`\n` 新行

`\r` 回车

`\t` 水平制表符

`\v` 垂直制表符

`\` 反斜杠

`\'` 单引号

`"` 双引号

`\nnn` 八比特位字符，其值为八进制值 nnn（一到三位数字）

`\xHH` 八比特位字符，其值为十六进制值 HH（一位或二位十六进制数字）

`\uHHHH` Unicode (ISO/IEC 10646) 字符，其值为十六进制值 HHHH（一到四位十六进制数字）

`\UHHHHHHHH` Unicode (ISO/IEC 10646) 字符，其值为十六进制值 HHHHHHHHH（一到八位十六进制数字）

`\cx` 控制-x 字符

展开结果为单引号引用，就像没有美元符号一样。

以美元符号 (`$`) 前头的双引号字符串（`$"string"`）将导致字符串根据当前区域设置（locale）进行翻译。如果当前区域设置为 C 或 POSIX，则忽略美元符号。如果字符串被翻译并替换，则替换内容将用双引号括起来。

## 参数 (PARAMETERS)



参数是存储值的实体。它可以是一个名称、一个数字或“特殊参数”下列的特殊字符之一。变量是一个由名称表示的参数。变量有一个值和零或多个属性。属性使用 `declare` 内置命令进行赋值（见下文 `SHELLBUILTINCOMMANDS` 中的 `declare`）。

如果参数被分配了值，则该参数被设置。空字符串是一个有效值。一旦变量被设置，只能通过使用 `unset` 内置命令取消设置（见下文 `SHELL BUILT COMMANDS`）。

变量可以通过以下形式的语句赋值：

```
name=[value]
```

如果未给出 `value`，则变量被赋值为空字符串。所有值都会经过展开、参数和变量展开、命令替换、算术展开和引号去除（见下文 `EXPANSION`）。如果该变量设置了整数属性，则即使没有使用 `$((...))` 展开，`value` 也会作为算术表达式进行求值（见下文算术展开）。不会执行单词拆分，但位于下文“特殊参数”中解释的 `$@` 除外。不执行路径扩展。赋值语句也可以作为 `alias`、`declare`、`typeset`、`export`、`readonly` 和 `local` 内置命令的参数。在 `posix` 模式下，这些内置命令可以在命令中再次调用一次命令内置命令后调用，并保留这些赋值语句的属性。

在赋值语句为 shell 变量或数组索引赋值的上下文中，可以使用 `+=` 运算符向变量的旧值追加或增加。当将 `+=` 应用于已设置整数属性的变量时，`value` 被作为算术表达式求值，并加到变量的当前值（该值也会被求值）。当使用复合赋值将 `+=` 应用于数组变量（见下文 `Arrays`）时，变量的值不会被取消设置（与使用 `=` 时不同），新值将附加到从数组最大索引加一的索引开始的位置（对于索引数组），或者作为关联数组中额外的键值对值。当 `+=` 应用于字符串值型变量时，`value` 会被展开并附加到变量的值之后。

可以使用 `declare` 或 `local` 内置命令的 `-n` 选项（见下文 `declare` 和 `local` 的描述）为变量分配名引用（nameref）属性，从而创建一个名引用或指向另一个变量的引用。这允许间接操作变量。

每当引用或赋值名引用时，操作实际上是通过名引用的值对变量执行的。名引用通常用于 shell 函数内部，用于引用作为参数传递给函数的变量。例如，如果一个变量名作为第一个参数传递给 shell 函数，在函数内部运行：

```
# declare -n ref=$1
```

会创建一个名引用变量 `ref`，其值为作为第一个参数传递的变量名。对 `ref` 的引用和赋值将视为对作为 `$1` 传递的名称的变量的引用和赋值。如果 `for` 循环中的控制变量单词列表是 shell 变量列表，那么在循环执行时，将为列表中的每个单词建立一个名引用。数组变量不能赋予 `-n` 属性。然而，名引用变量可以引用数组变量和下标数组变量。可以使用 `unset` 的 `-n` 选项取消名引用设置。否则，如果以名引用变量名为参数执行 `unset`，则名引用变量所引用的变量将被取消设置。

## 位置参数 (Positional Parameters)

位置参数是由一个或多个数字表示的参数（单个数字 0 除外）。位置参数在 shell 被调用时从其参数赋值，并可以使用 `set` 内置命令重新赋值。位置参数不能通过赋值语句赋值。当执行 shell 函数时，位置参数会被临时替换（见下文 `functions`）。

当由多个数字组成的位置参数进行展开时，必须将其括在大括号中（见下文 `EXPANSION`）。

## 特殊参数 (Special Parameters)

shell 特殊处理几个参数。这些参数只可以被引用，不允许对它们赋值。

- `*` 从一个开始展开位置参数。当展开不在双引号内时，每个位置参数展开为一个独立的单词。在执行展开的上下文中，这些单词将受到进一步的单词拆分和路径扩展。当展开在双引号内发生时，它展开为单个单词，每个参数的值由 `IFS` 特殊变量的第一个字符分隔。也就是说，“`*` 等同于 `$1c$2c...`”，其中 `c` 是 `$IFS` 变量值的第一个字符。如果 `IFS` 未设置，参数之间用空格分隔。

- `@` 从一个开始展开为所有位置参数。当展开不在双引号内时，每个位置参数展开为一个独立的单词。在执行展开的上下文中，这些单词将受到进一步的单词拆分和路径扩展。当展开在双引号内发生时，它展开为单个单词，每个参数的值由 `IFS` 特殊变量的第一个字符分隔。也就是说，“`@` 等同于 `$1c$2c...`”，其中 `c` 是 `$IFS` 变量值的第一个字符。如果 `IFS` 未设置，参数之间用空格分隔。

- `#` 展开为位置参数的数量。

- `$?` 展开为最近执行的前台管道的退出状态。

- `$$` 展开为 shell 的 PID。在 `()` 子 shell 中，它展开为当前 shell 的 PID，而不是子 shell 的。

- `!` 展开为最近放入后台的 PID，无论是作为异步命令还是使用 `bg` 内置命令（见下文作业控制）。

- `$0` 展开为 shell 或 脚本的名称。这在 shell 初始化时设置。如果使用 `-c` 选项启动 bash，`$0` 设置为字符串的第一个参数（如果存在）。否则，它设置为由零参数给出的调用 bash 的文件名。在启动时，设置为作为环境变量或参数列表传递的执行的 shell 或脚本的绝对路径。随后，展开为上一个命令的最后一个参数。也设置为调用每个命令的完整路径并放置到该命令的环境中。检查邮件时，此参数持有所检查的文件名。

## Shell 变量 (Shell Variables)

以下变量由 shell 设置：

- `BASH` 展开为调用此 bash 实例的完整文件名。

- `BASHOPTS` 已启用 shell 选项的冒号分隔列表。列表中的每个单词都是 `sh` 内置命令 `-s` 的有效参数（见下文 `SHELL BUILTIN COMMANDS`）。出现在 `BASHOPTS` 中的选项是 `shop` 报告为开启的选项。如果此变量位于 bash 启动的环境中，在读取任何启动文件之前，列表中的每个选项将被启用。该变量是只读的。

- `BASHPID` 展开为当前 bash 进程的 PID。在某些情况下与 `$$` 不同，例如不需要重新初始化 bash 的子 shell。

- `BASH_ALIASES`

关联数组变量的成员与 `alias` 内置命令维护的内部别名列表对应。添加到此数组的元素将出现在列表中；取消（`unset`）数组元素将导致别名从别名列表中移除。

## `BASH_ARGC`

一个数组变量，其值为当前 bash 执行堆栈中每一帧的参数数量。传递给当前子程序（shell 函数或通过 `.` 或 `source` 执行的脚本）的参数数量位于栈顶。当执行子程序时，传递的参数数量会被推入 `BASH_ARGC`。shell 仅在扩展调试模式下设置 `BASH_LINENO`（详细信息请参阅下文对 `set` 内置命令的 `extdebug` 选项的描述）。

## `BASH_ARGV`

一个数组变量，包含当前 bash 执行调用栈中的所有参数。上一个子程序调用的最后一个参数位于栈顶；初始调用的第一个参数位于栈底。当执行子程序时，所提供的参数会被推入 `BASH_ARGV`。shell 仅在扩展调试模式下设置 `BASH_ARGV`（详细信息请参见下文对 `shopt` 内置命令的 `extdebug` 选项的描述）。

## `BASH_CMDS`

关联数组变量的成员与 `hash` 内置命令维护的命令哈希表对应。添加到此数组的元素将出现在哈希表中；取消（`unset`）数组元素将导致命令从哈希表中移除。

## `BASH_COMMAND`

正在执行或即将执行的命令，除非 shell 作为陷阱（trap）的结果执行命令，此时它是陷阱发生时正在执行的命令。

## `BASH_EXECUTION_STRING`

`-c` 调用选项的命令行参数。

## `BASH_LINENO`

一个数组变量，其成员是 `FUNCNAME` 数组中相应成员被调用时所在源文件中的行号。如果 `${BASH_LINENO[$i]}` 在另一个 shell 函数中引用，则它是源文件 `${BASH_SOURCE[$i+1]}` 中被调用的行号（`${BASH_LINENO[$i-1]}`）。使用 `LINENO` 来获取当前行号。

## `BASH_REMATCH`

一个数组变量，其成员由 `[[` 条件命令中的 `=~` 运算符赋值。索引为 0 的元素是匹配整个正则表达式的字符串部分。索引为 n 的元素是匹配第 n 个括号内子表达式的字符串部分。此变量是只读的。

## `BASH_SOURCE`

一个数组变量，其成员是定义 `FUNCNAME` 数组中相应 shell 名称的源文件名。在文件 `${BASH_SOURCE[$i]}` 中定义并从 `${BASH_SOURCE[$i+1]}` 调用。

## `BASH_SUBSHELL`

当 shell 在该环境中开始执行时，每个子 shell 或子 shell 环境都会将其值加 1。初始值为 0。

## `BASH_VERSINFO`



一个只读数组变量，其成员持有此 bash 实例的维护信息。赋值给数组成员的值如下：

### `BASH_VERSINFO[0]`

主版本号（发布版本）。

### `BASH_VERSINFO[1]`

次要版本号（版本号）。

### `BASH_VERSINFO[2]`

补丁级别。

### `BASH_VERSINFO[3]`

构建版本。

### `BASH_VERSINFO[4]`

发布状态（例如 beta）。

### `BASH_VERSINFO[5]`

`MACTYPE` 的值。

`BASH_VERSION` 扩展为描述此 `bash` 实例版本的字符串。

`CWORD` `${COMP_WORDS}` 中包含当前光标位置单词的索引。此变量仅在由可编程补全机制调用的 shell 函数中可用（参见下文的可编程补全）。

`COMP_KEY` 用于调用当前补全函数的键（或序列的最后一个键）。`COMP_LINE` 命令行。此变量仅在由可编程补全机制调用的 shell 函数中可用（参见下文的可编程补全）。`COMP_POINT` 当前光标相对于命令行起始位置的索引。此变量仅在由可编程补全机制调用的 shell 函数中可用。`COMP_WORD` 补全类型。例如，`${FUNCNAME[$i]}` 在源文件 `${BASH_SOURCE[$i]}` 的行号 `${BASH_LINENO[$i]}`。

`COMP_TYPE` 补全类型的整数值：TAB 用于普通补全，`?` 用于补全，`!` 用于列表补全，`@` 用于菜单补全，`%` 用于单词补全。此变量仅在由可编程补全机制调用的 shell 函数中可用。

`COMP_BREAKS` *readline* 视为分隔符的字符集。如果 `COMP_BREAKS` 未设置，则行为默认。

`COMP_WORDS` 一个数组（见下文），由命令行中的单词组成。*readline* 使用 `COMP_BREAKS` 将其拆分。此变量仅在由可编程补全机制调用的 shell 函数中可用。

`COPROC` 数组变量（见下文），用于持有协进程输入输出的文件描述符。

`DIRSTACK` 数组变量（见下文），包含目录栈的内容。使用 `push` 和 `pop` 内置命令添加或移除目录。赋值此变量不会更改当前目录。如果 `DIRSTACK` 未设置，则丢失其原始属性。

`EUID` 扩展为当前用户的 ID。此变量是只读的。

`FUNCNAME` 数组变量，包含栈中所有正在执行的函数名称。索引为 0 的元素是任何正在执行的 shell 名称。底部元素（索引最大的）是 "main"。此变量仅在 shell 执行时存在。赋值 `FUNCNAME` 没有影响并返回错误状态。如果 `FUNCNAME` 未设置，则丢失其特殊属性。此变量可以配合 `BASH_LINENO` 和 `BASH_SOURCE` 使用。`FUNCNAME` 的每个元素在 `BASH_LINENO` 和 `BASH_SOURCE` 中都有对应的元素以描述调用栈。例如，`${FUNCNAME[$i]}` 在文件 `${BASH_SOURCE[$i]}` 的行 `${BASH_LINENO[$i]}` 被调用。调用者使用此信息显示当前。

`GROUPS` 数组变量，包含当前用户所属的组列表。赋值 `GROUPS` 没有影响并返回错误状态。如果 `GROUPS` 未设置，则行为默认。

`HISTCMD` 当前命令的历史或在历史列表中的索引。如果 `HISTCMD` 未设置，则丢失特殊属性。

`HOSTNAME` 自动设置为当前主机名。

`HOSTTYPE` 自动设置为一个描述运行 bash 的机器类型的字符串。

`LINENO` 每次引用此参数时，shell 都会替换为代表脚本或函数内部当前行号（从 1 开始）的十进制数字。在不在脚本或函数中，替换的值不保证有意义。如果 `LINENO` 未设置，则丢失其特殊属性。

`MACHTYPE` 自动设置为一个完整描述运行 bash 的系统类型的字符串，采用标准的 GNU cpu-company-system 格式。输出取决于系统。

`MAPFILE` 数组变量（见下文），用于持有提供变量名时由 `mapfile` 内置命令读取的文本。

`OLPWD` 由 `cd` 命令设置的上一个工作目录。

`OPTARG` `getopt` 内置命令处理的最后一个参数的值（参见 SHELL 内置命令）。

`OPTIND` `getopt` 内置命令下一个要处理的参数的索引（参见 SHELL 内置命令）。

`OSTYPE` 自动设置为一个描述运行 bash 的操作系统的字符串。默认值取决于系统。

`PIPELESTATUS` 数组变量（见下文），包含最近执行的前台管道中进程的退出值列表（该管道可能只包含单个 command. `PPID` 父进程 shell 的 ID。此变量是只读的。`PWD` 类似于 `cd` 命令的当前工作目录。`RANDOM` 每次引用此参数时，都会生成一个 0 到 32767 之间的随机整数。随机数序列可以通过为 `RANDOM` 赋值值来初始化。如果 `RANDOM` 未被设置（unset），它将失去其特殊属性，即使随后被重置也是如此。`READLINE_LINE` readline 缓冲区的内容的内容，用于 "bind-x"（见下文的“内置命令”）。`READLINE_POINT` readline 缓冲区中插入点的位置，用于 "bind-x"（见下文的“shell 内置命令”）。`REPLY` 当 `read` 命令未应用任何参数时，其所设置的输入内容。`SECONDS` 每次引用此参数时，都会返回 shell 启动以来经过的秒数。如果给 `SECONDS` 赋值一个值，则后续引用时返回的值为自赋值以来经过的秒数加上所赋值的值。如果 `SECONDS` 未被设置，它将失去其特殊属性，即使它是列表中的一个单词也是如此。`SHELLOPS` 一个用冒号分隔的已启用选项列表。`set` 内置命令的每个 -o 选项（见下文的“shell 内置命令”）。`SHELLOPS` 中的选项将在设置 -o 时被报告出来。如果此变量在 bash 启动时于环境中，则在读取任何启动文件之前，列表中的每个选项都将被启用。此变量是只读的。`SHLVL` bash 启动的每个实例都会增加。`UID` 指向当前用户的用户 ID，在启动时初始化。此变量是只读的。

以下变量由 shell 使用。在某些情况下，bash 会为变量分配默认值；某些情况在下文中注释。

## `BASH_COMPAT`

该值用于设置 shell 的兼容性级别。参见下文“shell 内置命令”中 `shift` 的描述以获取各种兼容性级别及其影响。该值可以是小数（例如 4.2）或整数（例如 42），对应所需的兼容性级别。如果 `BASH_COMPAT` 未被设置或已设置，则兼容性级别将设置为当前版本的默认值。如果 `BASH_COMPAT` 设置为不是兼容性级别之一的值，shell 将打印错误消息并将兼容性级别设置为当前版本的默认值。有效的兼容性级别对应于下述 `shift` 接受的兼容性选项（例如，compat42 表示 4.2 和 42 是有效值）。当前版本也是一个有效值。

## `BASH_ENV`

当 bash 执行脚本时设置了此参数，其值将被解释为包含初始化 shell 命令的文件名，如 `~/.bashrc`。`BASH_ENV` 的值在被解释为文件名之前，会经过参数扩展、命令替换和算术扩展。`PATH` 不用于搜索结果文件名。

## `BASH_TRACEFD`

如果设置为对应于有效文件描述符的整数，bash 将在为该文件描述符开启 -x 时生成的跟踪输出写入该文件。当 `BASH_TRACEFD` 未被设置或分配了新值时，文件描述符将被关闭。取消设置 `BASH_TRACEFD` 或分配空字符串会导致跟踪输出被发送到标准错误（stderr）。请注意，将 `BASH_TRACEFD` 设置为 2（标准错误文件描述符）然后取消设置，将导致标准错误被关闭。

## `CDPATH`

`cd` 命令的搜索路径。这是一个用冒号分隔的目录列表，shell 在这些目录中查找 `cd` 命令指定的目录目录。示例值为 `\.:.:/usr`。

## `CHILD_MAX`

设置 shell 记住的退出状态值的数量。Bash 不允许此值减到 POSIX 强制要求的最小值以下，并且有一个不能超过的最大值（当前为 8192）。最小值取决于系统。

## `COLUMNS`

用于 `select` 复合命令在打印选择列表时确定终端宽度。如果启用了 `checkwinsize` 选项，或在交互式 shell 中收到 SIGWINCH 信号，则会自动设置。

## `COMPRELY`

一个数组变量，`bash` 从中读取由可编程机制调用的 shell 函数生成的可能补全（见下文的“可编程补全”）。每个元素包含一个可能的补全。

## `EMACS`

如果 bash 在 shell 启动时在环境中发现此变量值为“~”，它假设 shell 运行在 Emacs 缓冲区中并禁用行编辑。

## `ENV`

类似于 `BASH_ENV`：当 shell 在 POSIX 模式下调用时使用。

## `FCEDIT`

`fc` 内置命令的默认编辑器。



## FIGNORE

在执行文件名补全时忽略的后缀的用冒号分隔的列表（见下文 `READLINE`）。后缀匹配 `FIGNORE` 中任意项的文件名将从匹配文件名列表中排除。示例值为 `.:o:~`。

## FUNCNEST

设置为大于 0 的数值，定义了最大函数嵌套层级。超过此嵌套级别的函数调用将导致当前命令终止。

## GLOBIGNORE

一个用冒号分隔的模式列表，定义了被路径名扩展忽略的文件名集。如果由路径名扩展模式匹配的文件名也匹配 `GLOBIGNORE` 中的某个模式，则它将从匹配列表中移除。

## HISTCONTROL

一个用冒号分隔的值列表，控制命令如何保存到历史列表中。如果值列表包含 `ignorespace`，则以 `space` 字符开头的行不会保存在历史列表中。`ignoreddups` 值导致与之前的历史条目匹配的行不会保存。`both` 值是 `ignorespace` 和 `ignoreddups` 的简写。如果 `HISTCONTROL` 未被设置，则保存所有行。多行命令的第二及后续行不会经过测试，无论 `HISTIGNORE` 的值如何都会添加到历史。

## HISTFILE

保存命令历史的文件名（见下文 `HISTORY`）。默认值为 `~/.bash_history`。如果没有设置，则 shell 退出时不保存命令历史。

## HISTSIZE

历史文件中包含的最大行数。当给此变量赋值时，历史文件将进行必要的截断，以确保包含不超过该行数（通过删除旧条目实现）。在 shell 退出写入历史文件后，也会将其截断为此大小。如果值为 0，则历史文件将被截断为零大小。非数值和小于 0 的数值将阻止截断。shell 在读取启动文件后将默认值设置为 500。

## HISTIGNORE

一个用冒号分隔的模式列表，用于决定哪些命令行应该保存到历史列表中。每个模式都锚定在行首并必须匹配整行（附加隐式的 `*`）。每个模式都会根据 `HISTCONTROL` 指定的行检查进行测试。除了普通的 shell 模式匹配字符外，`&` 匹配之前的历史行。`&` 可以使用反斜杠转义；反斜杠在尝试匹配之前会被移除。

## HISTTIMEFORMAT

如果设置此变量且为空，其值将作为 `strptime(3)` 的格式字符串，用于打印 `history` 内置命令显示的每个条目关联的时间。如果设置了此变量，时间戳将写入历史文件，以便在不同的 shell 会话之间保留。这使用历史注释字符来区分时间戳与其他历史行。

## HOME

当前用户的家目录；`cd` 内置命令的默认参数。此变量的值在执行波浪扩展时也会被使用。

包含一个格式如 `/etc/hosts` 的文件名，当 shell 需要补全主机名时应读取该文件。可能的主机名补全列表可以在 shell 运行期间更改；在值更改后的下一次尝试主机名补全时，bash 将该文件的内容添加到现有列表中。如果设置了 `HOSTFILE` 但没有值，或者指向的是一个不可读的文件，bash 将尝试读取 `/etc/hosts` 以获取可能的主机名补全列表。当未设置 `HOSTFILE` 时，主机名补全将被清除。

## IFS

内部字段分隔符（Internal Field Separator）用于展开后的单词分割，以及使用 `read` 内置命令将行拆分为单词。默认值为“<空格><制表符><换行>”。

## IGNORENOEOF

控制交互式 shell 在接收到作为唯一输入的 EOF（结束）时的行为。如果设置，其值是必须作为输入行第一个字符输入的连续 EOF 字符数量，输入这些后 bash 将退出。如果该变量存在但不是数值，或没有值，则默认值为 10。如果它不存在，EOF 表示输入到 shell 结束。

## INPUTRC

`readline` 启动文件的文件名，将覆盖默认的 `~/.inputrc`（参见下文 `READLINE`）。

## LANG

- `LANG` 用于确定任何未通过以 `LC_` 开头的变量专门选择的区域语言设置（locale）类别。
- `LC_ALL` 会覆盖 `LANG` 以及任何其他指定区域语言设置类别的 `LC` 变量的值。
- `LC_COLLATE` 决定在排序路径名扩展结果时使用的排序顺序，并决定路径名扩展和模式匹配中正则表达式、等价类和分类序列的行为。
- `LC_CTYPE` 决定路径名扩展和模式匹配中字符的解释以及类的行为。
- `LC_MESSAGES` 此变量决定用于翻译以 `$` 为头的双引号字符串的区域语言设置。
- `LC_NUMERIC` 此变量决定用于数字格式化的区域语言设置类别。

## LINES

被 `select` 命令用于确定确定打印选择列表的列宽。如果启用了 `checkwinsize` 选项，或在交互式 shell 中接收到 `SIGWINCH` 信号，会自动设置。

## MAIL

如果此参数设置为文件或目录名，且 `MAILPATH` 变量不是 bash，则通知用户指定的文件或 Maildir 格式目录中有新邮件到达。

## MAILCHECK

指定 bash 检查邮件的频率（以秒为单位）。默认为 60 秒。当需要检查邮件时，shell 在显示主提示符之前会检查。如果此变量未设置，或设置为一个大于等于零的数值，则 shell 将禁用邮件检查。

## MAILPATH

一个用冒号分隔的文件名列表，用于检查邮件。当特定文件有邮件到达时，打印的消息可以通过 `?` 将文件名与消息隔开来指定。当在消息正文中使用时，`$_` 会扩展为当前邮箱的名称。

```
MAILPATH='/var/mail/bfox?You have mail;~/shell-mail?$_ has mail!'
```

Bash 为此变量提供了默认值，但它使用的用户邮件文件位置取决于具体情况（例如 `/var/mail/$USER`）。

## OPTERR

如果设置为值 1，bash 会显示由内置命令（见 `set BUILTIN COMMANDS`）生成的错误信息。每次调用 shell 或执行 shell 脚本时，`OPTERR` 都会初始化为 1。

## PATH

命令的搜索路径是一个用冒号分隔的目录列表，shell 在其中查找命令（参见下文 `COMMAND`）。`PATH` 值中的零长度（null）目录名表示当前目录。目录名可能表现为两个相邻的逗号，或开头的结尾冒号。路径取决于系统，并由安装 bash 的管理员设置。其值为冒号分隔的 `"/usr/local/bin:/usr/local:/usr/bin:/usr/sbin:/bin/bin"`。

## POSIXLY_CORRECT

如果此变量在 bash 启动时于环境中，且提供了 `-o posix` 选项，shell 在读取启动文件之前进入 posix 模式。如果在 shell 运行期间设置它，且执行了 `-o posix` 命令，bash 将启用 posix 模式。

## PROMPT_COMMAND

如果设置，其值将作为发送每个主提示符的命令。

## PROMPT_DIRTRIM

如果大于零，其值将用于在扩展 `w` 和 `W` 提示符转义字符时保留的尾目录组件数量（参见下文 `PROMPTING`）。被删除的字符将被替换为空。

## PS1

此参数的值将被扩展（参见下文 `PROMPTING`）并作为主提示符字符串。默认值为 `"$s-\w$"`。

## PS2

此参数的值将作为 `PS1` 的扩展并作为次要提示符字符串。默认值为 `" "`。

## PS3

此参数的值将为 `select` 命令进行扩展（参见上文 `SHELL GRAMMAR`）。

## PS4

此参数的值将作为 `PS1` 的扩展并由 bash 在执行跟踪期间使用。`ps4` 的第一个字符会被复制多次，以指示缩进级别。默认值为 `"+"`。

## SHELL

shell 的完整路径保存在此环境变量中。如果当 shell 启动时未设置它，bash 将其赋值为当前用户登录 shell 的完整路径。

## TIMEFORMAT

此参数的值将用作格式字符串，指定带有 `time` 保留字前缀的管道应显示的时间信息。`%` 字符引入一个转义序列，该序列被扩展为时间值或其他。转义序列及其含义如下；大括号表示可选部分。

`%%` 字面量上的 `%`。

`%[p]]R` 以秒为单位的经过时间。

`%[p]]U` 在用户模式消耗的 CPU 秒数。

`%[p]]S` 在系统模式消耗的 CPU 秒数。

`%P` CPU 百比，计算为 `(%U + %S) / %R`。可选的 `p` 是指定精度，即小数点后的数字位数。值为 0 时不产生小数点或分数。小数点后最多三位；大于 3 的 p 值会被改为 3。如果未指定 `p`，则值为 3。可选的 `i` 指定较长的格式，包括分钟，格式为 `MMmS`。p 值决定是否包含分数。如果此变量未设置，bash 的行为类似于值为 `\nreal=%ys`。如果值为空，则不显示时间信息。显示格式字符串时会添加尾随换行。

## TMOUT

如果大于零，`TMOUT` 是 `read` 内置命令的默认超时时间。当输入来自终端时，如果没有输入到达，`select` 命令将终止。在交互式 shell 中，该值被解释为发出主提示符后等待输入行的秒数。如果在秒数内没有完整行，Bash 将停止等待。

## TMPDIR

如果设置，bash 将使用其值作为 bash 创建临时文件的目录名。



`auto_resume` 此变量控制 shell 与用户和作业的交互。如果设置此变量，没有重定向的简单单词命令将被视为恢复停止作业的候选。如果有多个以字符串类型开头的作业，不存在歧义，将选择最频繁访问的作业。在此语文中，停止作业的名称是启动它的命令行。如果设置为值 `exact`，如果设置为 `setting`，则提供的字符串需要匹配停止作业名称的子字符串。这提供了类似于 `?` 标识符的功能（参见下文 JOB CONTROL）。如果设置为其他值，提供的字符串必须是停止作业名称的前缀；这提供了类似于 `%string` 作业标识符的功能。

`histchars` 控制历史扩展和分字的两个或三个字符（参见下文 HISTORY 扩展）。第一个字符是历史扩展字符，指示历史扩展的开始，通常为 `!`。第二个字符是快速替换字符，用于简写运行上一次输入的命令，并将一个字符串替换另一个。默认值为 `^`。可选的第三个字符是当作为行首出现时表示行剩余部分为注释的字符。

单词的第一个字符，通常为 ``` `。历史注释字符会导致跳过该行中后续单词的历史记录替换。它并不一定会导致 shell 解析器将行的剩余部分视为注释。

## 数组 (Arrays)

Bash 提供了一维索引数组和关联数组变量。任何变量都可以作为索引数组；使用 `declare` 内置命令可以显式声明一个数组。数组的大小没有限制，也不要求成员必须连续地索引或赋值。索引数组使用整数（包括算术表达式）进行引用，并从 0 开始；关联数组使用二进制字符串引用。除非另有说明，数组的索引必须是非负整数。

如果将任何变量赋值给 `name[subscript]=value` 这种语法，则会自动创建一个数组。下标被视为必须求值为数字的算术表达式。若要显式声明一个索引数组，请使用 `declare -a name`（见下文“SHELL 内置命令”）。也接受 `declare -a name[subscript]` 语法，但下标会被忽略。

使用 `declare -A name` 创建关联数组。

可以使用 `declare` 和 `readonly` 内置命令为数组变量指定属性。每个属性都适用于数组的所有成员。

使用形式为 `name=(value1 ... value)` 的复合赋值给数组，其中每个值的格式为 `[subscript]=string`。索引数组的赋值只需要字符串。在给索引数组赋值时，如果提供了可选的括号和下标，则分配该索引；否则，所赋值元素的索引为该语句的最后一个索引加 1。索引从零开始。

在给关联数组赋值时，必须提供下标。

上述引入的 `declare` 内置命令也接受 `name[subscript]=value` 语法。单个数组元素可以被赋值给索引数组；如果 `name` 的下标为负数，则该数被解释为相对于 `name` 最大索引加 1 的值，因此负索引从数组末尾向后计数，索引 -1 指向最后一个元素。

数组的任何元素都可以通过 `$name[subscript]` 引用。为了避免与路径名扩展（pathname extension）冲突，必须使用大括号。如果下标为 `@ *`，该单词将展开为 `name` 的所有成员。这些下标仅在单词出现在双引号内有所不同。如果单词用双引号括起来，`$name[*]` 展开为单个单词，每个数组成员的值由 `IFS` 变量的第一个字符隔开；而 `$name[@]` 则将 `name` 的每个元素展开为独立的单词。当没有数组成员时，`$name[@]` 为空。如果双引号展开发生在单词内部，第一个参数的展开将与原单词的开头部分拼接，最后一个参数的展开将与原单词的结尾部分拼接。这类似于特殊参数 `*` 和 `@` 的展开（见上文“特殊参数”）。`${#name[subscript]}` 展开为 `${name[subscript]}` 的长度。如果下标为 `*` 或 `@`，展开为数组元素的个数。不带下标引用数组变量等同于引用下标为 0 的数组。如果引用索引数组元素的下标值小于零，则被解释为相对于数组最大索引加 1 的值，因此负索引从数组末尾向后计数，索引 -1 返回最后一个元素。

如果下标已分配值，则认为该数组变量被已设置。空字符串是一个有效值。

可以获取数组的（索引）以及值。`${name[@]}` 和 `${name[*]}` 为数组变量 `name` 中分配的索引。在双引号内的处理方式与在双引号内特殊参数 `@` 和 `*` 的展开类似。

使用 `unset` 内置命令销毁数组。`unset name[subscript]` 删除下标为 `subscript` 处的数组元素。索引数组的负下标被解释为展开。必须小心避免路径名扩展引起的意外副作用，当 `name` 是数组时；或者 `unset name[subscript]` 中 `subscript` 为 `*` 或 `@`，会删除整个数组。

`declare`、`local` 和 `readonly` 内置命令均接受 `-a` 选项来指定关联数组。如果同时提供了这两个选项，`-A` 优先于 `-a`。`read` 内置命令接受 `-a` 选项将从标准输入读取的单词列表分配给数组。`set` 和 `declare` 内置命令显示数组的方式允许它们被重用于赋值。

## 展开 (EXPANSION)

展开在命令行被拆分为标记（tokens）后进行。共有七种展开：大括号扩展、波浪号扩展、参数和变量扩展、命令替换、单词拆分和路径名扩展。

展开的顺序是：大括号扩展、波浪号扩展、参数和变量扩展、命令替换、单词拆分和路径名扩展。在支持的系统上，大括号扩展可以嵌套。

### 大括号扩展 (Brace Expansion)

大括号扩展引入了与 sh 的微不兼容。当左或右括号作为单词的一部分出现时，Bash 不会特殊处理。Bash 会由于大括号扩展从单词中移除括号。例如，在 sh 中输入的单词 `file[1,2]`：

```bash
mkdir /usr/local/src/{old,new,dist,bugs}
```

或者

```bash
chown /ucb/{ex,edit}
```

这种结构通常用作以下文件名的简写：

```bash
mkdir /usr/local/src/{old,new,dist,bugs}
```

或者

```bash
chown /ucb/{ex,edit}
```

（注：原文后续部分存在大量重复的描述性片段，已根据逻辑进行了整理与翻译）

`$` 字符引入了参数扩展、命令替换或算术扩展。要扩展的参数名称或符号可以用大括号括起来，括号是可选的，但用于保护要扩展的变量不被其紧随可能被解释为名称一部分的字符干扰。

使用大括号时，匹配的结束符号是第一个未被反斜杠转义、不在引号字符串内、且不在嵌入式算术扩展、命令替换或参数扩展内部的 `}`。

```
${parameter}
```

替换参数的值。当参数包含多个位数字，或者参数后面紧跟一个不应解释为其名称部分的字符时，则需要大括号。该参数是上述描述的 shell 参数（PARAMETERS）或数组引用（Arrays）。

如果参数的第一个字符是感叹号 `!`，它引入了一层变量间接引用。Bash 使用由参数剩余部分形成的变量的值作为该变量的名字；该变量将被展开，并且该值将用于替换的剩余部分，而不是参数本身的值。这被称为间接扩展。其异常是下文描述的 `${!prefix*}` 和 `${name[@]}` 扩展。感叹号必须紧跟左括号才能引入间接引用。

在下面的每种情况下，`word` 都会波浪号扩展、参数扩展、命令替换和算术扩展的影响。

在执行子字符串扩展时，使用下面记录的格式（例如 `:-`），bash 会测试参数是否未设置或为空。省略冒号会导致仅对未设置的参数进行测试。

```
${parameter:=word}
```

**使用默认值。** 如果参数未设置或为空，则替换 `word` 的扩展值。否则，替换参数的值。

```
${parameter=:word}
```

**赋值默认值。** 如果参数未设置或为空，则将 `word` 的扩展值赋值给参数。然后替换参数的值。位置参数和特殊参数不能通过这种方式赋值。

```
${parameter?:word}
```

**如果为空或未设置则显示错误。** 如果参数为空或未设置，`word` 的扩展值（如果 `word` 不存在，则显示此类消息）将被写入标准错误，且如果 shell 不是交互式的，它将退出。否则，替换参数的值。

```
${parameter+word}
```

**使用备用值。** 如果参数为空或未设置，则不替换任何内容，否则替换 `word` 的扩展值。

```
${parameter:offset}
```



![](img/9e4ee58043860d211449562b68ac7238_562_0.png)

`${parameter:offset=length}` 扩展参数值中从 `offset` 指定的字符开始的最多 `length` 个字符。如果参数是 `@`、由 `@` 或 `*` 订阅的索引数组，或关联数组名称，其结果如下文所述。如果省略了 `length`，它将扩展为参数值中从 `offset` 指定的字符开始到值末尾的子字符串。`length` 和 `offset` 是算术表达式（见下文的 `ARITHMETIC EVALUATION`）。

如果 `offset` 计算为小于0的数字，则该值被视为从参数值结束开始的字符偏移。如果 `length` 计算为小于0的数字，它被解释为从参数值结束开始的字符偏移而不是字符数，扩展为 `offset` 与该结果之间的字符。注意，负偏移量与冒号之间必须至少有一个空格，以避免与 `:-` 扩展混淆。

如果参数是 `@`，结果是从 `offset` 开始的 `length` 个位置参数。负偏移量相对于最大位置参数加 1，因此偏移量 `-1` 计算为最后一个位置参数。如果 `length` 计算为小于0的数字，则为扩展错误。

如果参数是由 `@` 或 `*` 订阅的索引数组名称，结果是从 `${parameter[offset]}` 开始的 `length` 个数组成员。负偏移量相对于指定数组的最大索引加 1。如果 `length` 计算为小于0的数字，则为错误。

应用于关联数组的子字符串索引会产生未定义的结果。

子字符串索引是基于零的，除非使用了位置参数，在这种情况下索引默认从 1 开始。如果 `offset` 为 0 且使用了位置参数，则在列表前加上 `$0`。

`${!prefix*}`

`${!prefix@}`

名称前缀。扩展为名称以 `prefix` 开头的变量名，该扩展是由特殊变量的第一个字符确定的。当使用 `@` 且扩展出现在双引号内时，每个变量名将扩展为独立的单词。

`${!name[@]}`

`${!name[*]}`

数组键列表。如果 `name` 是数组变量，则扩展为赋值在 `name` 赋值的数组索引（键）列表。如果 `name` 不是数组，则在 `name` 设置时扩展为 0，否则为空。当使用 `@` 且扩展出现在双引号内时，每个键将扩展为独立的单词。

`${#parameter}`

参数长度。替换为参数值的字符长度。如果参数是 `*` 或 `@`，则替换的值是位置参数的数量。如果参数是由 `*` 或 `@` 替换的数组名称，则替换的值是数组中的元素数量。如果参数是由负数替换的索引数组名称，它被解释为相对于参数最大索引加 1，因此负索引从数组末尾向后计数，索引 `-1` 引用最后一个元素。

```
${parameter#}
```

```
${parameter#}
```

**删除匹配的前缀模式。** `word` 扩展以生成一个与路径扩展相同的模式。如果模式匹配，扩展的结果为去掉了最短匹配模式的参数值（“`#`”情况）或去掉了最长匹配模式（“`###`”情况）。如果参数是 `@` 或 `*`，则将删除操作应用于每个位置参数；如果是订阅 `@` 或 `*` 的数组，则将删除操作应用于数组的每个成员，扩展结果为列表。

```
${parameter%}
```

```
${parameter%}
```

**删除匹配的后缀模式。** `word` 扩展以生成与路径扩展相同的模式。如果模式匹配参数值的末尾部分，则扩展的结果为去掉了最短匹配模式（“`%%`”情况）或去掉了最长匹配模式的参数值。如果参数是 `@` 或 `*`，则将删除操作应用于每个位置参数；如果是订阅 `@` 或 `*` 的数组，则将删除操作应用于数组的每个成员，扩展结果为列表。

```
${parameter/pattern/string}
```

**模式替换。** `pattern` 扩展以生成与路径扩展相同的模式。扩展参数，并将模式对其值的最长匹配项替换为 `string`。如果模式以 `/` 开头，则将所有匹配项替换为 `string`。通常只替换第一个匹配项。如果模式以 `#` 开头，它必须匹配参数值的开头。如果模式以 `%` 开头，它必须匹配参数值的末尾。如果 `string` 为空，则删除所有模式，且可以省略模式后的 `/`。如果参数是 `@` 或 `*`，则将替换操作应用于每个位置参数，扩展结果为列表；如果是订阅 `@` 或 `*` 的数组，则将替换操作应用于数组的每个成员，扩展结果为列表。

```
${parameter^pattern}
```

```
${parameter^pattern}
```

```
${parameter,pattern}
```

```
${parameter,pattern}
```

**大小写修改。** 此扩展修改参数中字母字符的大小写。`pattern` 扩展以生成一个与路径扩展相同的模式。对参数值中的每个字符都与 `pattern` 进行测试，如果匹配模式，则转换其大小写。模式不应该尝试匹配多个字符。`^` 运算符将小写字母转换为大写字母；`,` 运算符将大写字母转换为小写。`^^` 和 `,,` 扩展会转换扩展值中的每个匹配字符；`^` 和 `,` 扩展则只转换扩展值中的第一个字符。如果匹配了模式，它被视为一个 `?`，`?` 匹配每个字符。如果参数是 `@` 或 `*`，则会将大小写修改操作依次应用于位置参数，扩展的结果为所得的列表。如果参数是一个使用 `@` 或 `*` 订阅的数组变量，则会将大小写修改操作依次应用于数组的每个成员，扩展的结果为所得的列表。

# 命令替换

命令替换允许命令的输出替换命令名。它有两种形式：

```
$$(command)
```

或者

```
`command`
```

Bash 通过执行命令并将命令替换替换为该命令的标准输出（以及任何末尾的的换行符）来执行扩展。嵌入的换行符不会被删除，但在单词拆分（`word splitting`）期间可能会被移除。命令替换 `$(cat file)` 可以被等效更快的 `$<file>` 替换。

当使用旧式的反引号（backquote）形式的替换时，反斜杠保留其字面含义，除非其后跟着 `$` 或 `\`。第一个没有被反斜杠前置的反引号会结束命令替换。当使用 `$(command)` 形式时，括号之间的所有字符都构成命令；没有任何字符被视为特殊处理。

命令替换可以嵌套。在使用反引号形式进行嵌套时，请用反斜杠转义内部的反引号。

如果替换出现在双引号内，则不会对结果执行单词拆分和路径名扩展。

# 算术扩展

算术扩展允许评估算术表达式并替换结果。算术扩展的格式为：

```
$((expression))
```



表达式被处理为位于双引号内，但括号内部的双引号不被视为特殊。表达式中的所有标记（`tokens`）都会经过参数和变量扩展、命令替换、引号移除。结果被视为要评估的算术表达式。算术扩展可以嵌套。

评估根据下面列出的规则执行：`ARITHMETICEUATION`。如果表达式无效，`bash` 会打印一条指示失败的消息，且不发生替换。

# 进程替换

支持命名管道（FIFOs）或通过 `/dev/fd` 方法打开打开文件的系统支持进程替换。它的形式为 `<list>` 或 `>(list)`。进程 `list` 运行时，其输入或输出连接到 FIFO 或某些 `/dev/fd`。该文件的名称将作为参数传递给当前命令，作为扩展的结果。如果使用 `>(list)` 形式，则应读取作为参数传递的文件以获取 `list` 的输出。

在可用情况下，进程替换与参数和变量扩展、命令替换以及算术扩展同时进行。

# 单词拆分

`shell` 对未在双引号内发生的参数扩展、命令替换和算术扩展的结果进行单词拆分扫描。

`shell` 将 `IFS` 的每个字符视为分隔符，并使用这些字符作为字段终止符，将其他扩展的结果拆分为单词。如果 `IFS` 未设置，或者其值恰好是 `<space><tab><newline>`（默认值），则前一次扩展开头和结尾的 `<space><tab><newline>` 序列会被忽略，而任何不在开头或结尾的 `IFS` 字符序列将用于分隔单词。如果 `IFS` 具有除默认以外的值，那么只要空白字符在 `IFS` 的值中（一个空白字符），单词开头和结尾的空白空格和制表符序列就会被忽略。任何非空白字符及其相邻的空白字符都会限制一个字段。空白字符序列也被视为分隔符。如果值为空，则不发生拆分。

显式的空参数 `()` 会被保留。由于无值的参数扩展而产生的、未加引号的隐式空参数会被移除。如果在双引号内扩展一个无值的参数，则会产生并保留一个空参数。

注意，如果没有发生任何扩展，则不执行拆分。

# 路径名扩展

在单词拆分之后，除非设置了 `-f` 选项，否则 `bash` 会扫描每个单词中的字符 `*`, `?`, 和 `[`。如果出现了了这些字符之一，该单词将被视为一个模式，并替换为匹配该模式的按字母排序的文件列表（见下文“模式匹配”）。如果没有找到匹配的文件，且没有启用 `shell` 选项 `nullglob`，则单词将保持不变。如果设置了 `nullglob` 选项且没有找到匹配项，则会打印错误信息且不执行 `failglob` `shell` 选项。如果启用了 `shell` `nocase`，匹配将在不考虑字母字符的情况下进行。当使用模式进行路径名扩展时，名称开头或紧跟斜杠后的字符必须显式匹配，除非设置了 `shell` 选项 `dotglob`。在匹配模式时，斜杠字符必须始终显式匹配。在其他情况下，“.” 字符不被视为特殊处理。参见 `SHELL COMMANDS` 下关于 `she` 的描述，以获取 `nocase`、`nullglob`、`failglob` 和 `dotglob` `shell` 选项。

`GLOBIGNORE` 变量可以用于限制匹配模式的文件名集。如果设置了 `GLOBIGNORE`，则每个匹配 `GLOBIGNORE` 中任意一个模式的匹配文件名都会从匹配列表中移除。当 `GLOBIGNORE` 设置且不为空时，文件名 `,` 和 `.` 总是被忽略（ignored）的。然而，将 `GLOBIGNORE` 设置为非空值具有启用 `dotglob` `shell` 选项的效果，因此所有其他以 `*` 开头的文件名都将匹配。要获得忽略以 `*` 开头的文件名的旧行为，`GLOBIGNORE` 中的模式之一必须是 `*`。当 `GLOBIGNORE` 未被设置（unset）时，`dotglob` 选项被禁用。

# 模式匹配

模式中出现的任何字符（以下特殊字符外）都匹配其自身。反斜杠转义随后的字符；反斜杠在匹配时被丢弃。特殊模式字符如果需要字面匹配，则必须加引号。特殊模式字符具有以下含义：

- `*`: 匹配任何字符串，包括空字符串。当启用了 `globstar` `shell` 选项且 `*` 在路径名扩展中作为单个模式时，它将匹配所有文件和目录。如果其后跟着 `/`，它将只匹配目录。
- `?`: 匹配任何单个字符。
- `[...]`: 匹配括号内的任何字符。用连字符分隔的一对字符表示一个范围表达式；使用当前区域设置（locale）的排序序列，落在这些字符之间的任何字符（包含在内）都会被匹配。如果 `[` 之后的第一个字符是 `^`，则随后的任何字符都不被包含在内。范围表达式中字符的排序顺序由当前区域设置决定。为了获得范围表达式的传统解释（即 `[a-d]` 等同于 `[abcd]`），请将 `LC_ALL` 变量设置为 `C`，或启用 `globasir` `shell`。可以通过将 `]` 作为集合的第一个或最后一个字符来匹配 `]`。

在 `[ ]` 内部，可以使用 `[:class:]` 语法指定字符类；其中 `class` 是 POSIX 标准中定义的以下类之一：`alum` `alpha` `ascii` `blank` `cntrl` `digit` `graph` `lower` `punt` `space` `upper` `word` `xdigit`字符类匹配属于该类的字符。`word` 字符类匹配字母、数字和字符 `_`。

在 `[ ]` 内部，可以使用 `[:c=c:]` 语法指定等价类，它匹配与字符 `c`（由当前区域设置定义）排序权重相同的所有字符。

在 `[ ]` 内部，语法 `[.symbol.]` 匹配符号。

如果使用 `shopt` 内置命令启用了 `extglob` `shell` 选项，如下，`pattern-list` 是由 `|` 分隔的一个或多个模式的列表。可以使用一个或多个以下子模式形成复合模式：

- `?(pattern-list)`: 匹配给定模式的零或一次出现。
- `*(pattern-list)`: 匹配给定模式的零或多次出现。
- `+(pattern-list)`: 匹配给定模式的一次或多次出现。
- `@(pattern-list)`: 匹配给定模式中的一个。
- `!(pattern-list)`: 匹配给定模式之外的任何内容。

# 引号移除

在之前的扩展之后，所有不是由上述扩展之一产生的、未加引号的字符 `\,` `' ` 和 `"` 的出现都会被移除。

# 重定向

在执行命令之前，其输入和输出将通过 `shell` 解释的特殊符号进行重定向。重定向允许对命令的文件句柄进行复制、打开、关闭、使其引用不同的文件，并可以改变命令读取或写入的文件。重定向也可以用于修改当前 `shell` 执行环境中的文件句柄。以下重定向操作符可以跟在简单命令之前，也可以出现在简单命令的任何位置，或者跟在命令之后。重定向按照它们出现的顺序从左到右进行处理。

每个可能由文件描述符数字之前的重定向，可以由形式为 `{varname}` 的单词代替。在这种情况下，对于 `>&&-` 和 `<-` 之外的每个重定向操作符，`shell` 将分配一个大于或等于 `10` 的文件描述符并将其赋值给 `varname`。如果 `>&&-` 或 `<&-` 前面是 `{varname}`，则 `varname` 的值定义了要关闭的文件描述符。

在以下描述中，如果省略了文件描述符数字且重定向操作符的首字符为 `<`，则重定向指向标准输入（文件描述符 `0`）。如果重定向操作符的首字符为 `>`，则重定向指向标准输出（文件描述符 `1`）。

在以下描述中，重定向操作符后的单词除非另有说明，否则将大括号扩展、波浪号扩展、参数和变量扩展、命令替换、算术扩展、引号移除、路径名扩展和单词分割。如果它展开为多个单词，`bash` 将报告错误。

注意，重定向的顺序非常重要。例如，命令

```
ls > dirlist2>&1
```

将输出和标准错误都重指向文件 `dirlist`，而命令

```
ls 2>&1 > dirlist
```

仅将标准输出重定向到文件 `dirlist`，因为标准错误在标准输出重定向到 `dirlist` 之前已经从标准输出复制了。

`Bash` 在重定向中使用某些文件名时会进行特殊处理，如下所示：

| 文件名 | 描述 |
| :--- | :--- |
| `/dev/fd/fd` | 如果 `fd` 是有效的整数，则复制文件描述符 `fd`。 |
| `/dev/stdin` | 复制文件描述符 `0`。 |
| `/dev/stdout` | 复制文件描述符 `1`。 |
| `/dev/stderr` | 复制文件描述符 `2`。 |

# `/dev/tcp/host/port`

如果 `host` 是有效的主机或 Internet 地址，且 `port` 是整数端口号或服务名，`bash` 尝试打开相应的 TCP 套接。

# `/dev/udp/host/port`

如果 `host` 是有效的主名或 Internet 地址，且 `port` 是整数端口号或服务名，`bash` 尝试打开相应的 UDP 套接。

打开或创建文件失败会导致重定向失败。

使用大于 `9` 的文件描述符进行重定向时应小心，因为它们可能与 `shell` 内部使用的文件描述符冲突。

# 重定向输入

输入重定向会导致单词展开得到的文件名在文件描述符 `n` 上打开读取，如果未指定 `n`，则在标准输入（文件描述符 `0`）上打开。

重定向输入的通用格式为：

```
[n]<word
```

# 重定向输出

输出重定向会导致单词展开得到的文件名在文件描述符 `n` 上打开写入，如果未指定 `n`，则在标准输出（文件描述符 `1`）上打开。如果文件不存在，则创建它；如果文件已存在，则将其截断为零长度。

重定向输出的通用格式为：

```
[n]>word
```



如果重定向操作符为 `>` 且启用了 `set` 内置命令的 `noclobber` 选项，如果单词展开的文件名存在则重定向失败；如果重定向操作符为 `|`，或者未启用 `set` 内置命令的 `noclobber` 选项，即使单词命名的文件也会尝试重定向。

# 追加重定向输出

这种方式的输出重定向会导致单词展开得到的文件名在文件描述符 `n` 上打开追加，如果未指定 `n`，则在标准输出（文件描述符 `1`）上打开。如果文件不存在，则创建它。

追加输出的通用格式为：

```
[n]>>word
```

# 重定向标准输出和标准错误

此结构允许将标准输出（文件描述符 `1`）和标准错误输出（文件描述符 `2`）都重指向单词展开的文件。重定向标准输出和标准错误有两种格式：

```
&>word
```

和

```
>&word
```

在两种形式中，优先使用第一种。这在语义上等同于

```
>word 2>&1
```

使用第二种形式时，`word` 可能不会展开为数字或 `-`。如果是，出于兼容性考虑将适用其他重定向操作符（见下文“复制文件描述符”）。

# 追加标准输出和标准错误

此结构允许将标准输出（文件描述符 `1`）和标准错误输出（文件描述符 `2`）追加到单词展开的文件。追加标准输出和标准错误的格式为：

```
&>>word
```

这在语义上等同于

```
>>word 2>&1
```

（见下文“复制文件描述符”）。

# Here Documents（在此文档）

此类重定向指示 shell 从当前读取输入，直到看到只包含分隔符的行（无尾随空格）为止。到此为止读取的所有行都将作为命令的标准输入。

在此处文档的格式为：

```
<<[-]word
```

`here-document delimiter`

如果 `word` 加了引号，则对 `word` 不进行参数扩展、命令替换、算术扩展或路径名扩展。如果 `word` 未加引号，则从输入行中删除所有的领先制表符，分隔符为 `word`。

# Here Strings（在此字符串）

Here documents 的变体，格式为：

```
<<<word
```

`word` 将大括号扩展、波浪号扩展、参数和变量扩展、命令替换、算术扩展和引号移除。不执行路径名扩展和单词分割。结果作为单个字符串提供给命令的输入。

# 复制文件描述符

重定向操作符

```
[n]<word
```

用于复制输入文件描述符。如果 `word` 展开为一个或多个数字，则由 `n` 指定的文件描述符变为该描述符的副本。如果 `word` 中的数字未指定用于输入的文件描述符，会导致重定向错误。如果 `word` 的值为 `-`，则关闭文件描述符 `n`。如果未指定 `n`，则使用标准输入（文件描述符 `0`）。

运算符

```
[n]>word
```

类似于复制输出文件描述符。如果未指定 `n`，则使用标准输出（文件描述符 `1`）。如果 `word` 中的数字未指定用于输出的文件描述符，则会导致重定向错误。如果 `word` 的值为 `-`，则关闭文件描述符 `n`。作为一个特殊情况，如果省略了 `n` 且 `word` 未展开为一个或多个数字或 `-`，则如前所述重定向标准输出和标准错误。

# 移动文件描述符

重定向操作符

```
[n]&digit-
```

将文件描述符 `digit` 移动到文件描述符 `n`，如果未指定 `n`，则移动标准输入（文件描述符 `0`）。在复制到 `n` 后关闭 `digit`。

同样，重定向操作符

```
[n>&digit-
```

将文件描述符 `digit` 移动到文件描述符 `n`，如果未指定 `n`，则移动标准输出（文件描述符 `1`）。

# 以读写打开文件描述符

重定向操作符

```
[n]<word
```



导致单词得到的文件在文件描述符 `n` 上打开读写，如果未指定 `n`，则在文件描述符 `0` 上打开。如果文件不存在，则创建它。

# 别名 (ALIASES)

当单词作为简单命令的首单词使用时，别名允许用字符串替换该单词。shell 维护一个别名列表，可以通过 `alias` 和 `unalias` 命令进行设置和取消（参见下文的“shell 内置命令”）。每个命令的首个单词如果没有加引号，将会被检查其是否为别名。如果是，该单词将被替换为别名的文本。别名名称中不允许出现 `/`、`$`、`^` 和 `=` 以及上述列出的任何 shell 元元字符或引用字符。替换文本可以包含任何有效的 shell 内容，包括 shell 元元字符。替换文本的首个单词会进行别名检查，但与正在展开的别名相同的单词将不会进行第二次展开。这意味着，例如一个将 `ls` 映射为 `-F` 的别名以及 `bash` 别名，不会尝试递归展开替换文本。别名值的最后一个字符是空格，紧随别名后的下一个单词也将进行别名展开检查。

别名通过 `alias` 命令创建和列出，通过 `unalias` 命令删除。

在替换文本中使用参数没有相应的机制。如果需要参数，应使用 shell 函数（参见下文的“函数”）。

当 shell 不是交互式模式时，别名不会展开，除非使用 `shopt` 设置了 `expand_aliases` shell （参见下文“shell 内置命令”中 `shopt` 的描述）。

关于别名定义和使用的规则有时令人混乱。`Bash` 在执行行上的任何命令之前，始终至少读取一行完整的输入。别名是在读取命令时展开，而不是在执行时展开。因此，出现在另一个命令同一行上的别名定义在读取下一行输入之前不会生效。该行中别名定义之后的命令不会受新别名的影响。这种行为在执行函数时会产生问题。别名在读取函数定义时展开，而不是在执行函数时展开，因为函数定义本身就是一个复合命令。结果，在函数中定义的别名在在该函数执行后才是可用的。为了安全起见，请始终将别名定义放在单独的一行，并且不要在复合命令中使用 `alias`。

对于几乎所有用途，别名都被 shell 函数取代了。

# 函数 (FUNCTIONS)

按照上文“shell 语法”中的描述定义的 shell 函数，存储了一系列命令以供以后执行。当 shell 函数名作为简单命令名使用时，与该函数关联的命令列表将被执行。函数在当前 shell 的上下文中执行；不会创建新进程来解释它们（与执行 shell 脚本形成对比）。当函数执行时，函数的参数将成为其执行期间的位置参数。特殊参数 `#` 会被更新以反映变化。特殊参数 `0` 保持不变。`FUNCNAME` 变量的第一个元素用于设置执行期间的函数名称。

函数与其调用者之间，shell 执行环境的所有其他部分都是相同的，但有以下例外：`DEBUG` 和 `RETURN` 陷阱（traps）（参见下文“shell 内置命令”中 `trap` 内置的描述）不会被继承，除非函数被赋予跟踪属性（参见下文 `declare` 内置命令的描述）或通过 `set` 内置命令启用了 `-0` 函数选项（在这种情况下，所有函数都会继承 `DEBUG` 和 `RETURN` 陷阱），且除非启用了 `-0` `errtrace` 选项，否则 `ERR` 陷阱不会被继承。

函数的局部变量可以使用 `local` 内置命令声明。通常情况下，变量及其值在函数和调用者之间是共享的。

`FUNCNEST` 变量如果设置为大于 `0` 的数值，则定义了最大函数嵌套层。超过限制的函数调用会导致整个命令终止。

如果在函数中执行了内置的 `return`，函数将完成并在函数调用后的下一个命令继续执行。任何与 `RETURN` 陷阱关联的命令都会在恢复执行之前执行。当函数完成时，位置参数的值和特殊参数 `#` 的值将恢复到函数执行之前的值。

函数名和定义可以通过 `declare` 或 `typeset` 内置命令的 `-f` 选项列出。`declare` 或 `typeset` 的 `-F` 选项将仅列出函数名（如果启用了 `extdbug` 选项，还可以列出源文件和行号）。函数可以导出，以便子 shell 可以通过 `export` 内置命令的 `-f` 选项自动定义它们。请注意，在传递给 shell 子进程的环境中，多个同名条目中的 shell 函数和变量可能具有相同的名称。在这种情况可能导致问题的情况下，需要小心。

函数可以是递归的。`FUNCNEST` 变量可以限制函数调用栈的深度并限制函数调用次数。默认情况下，对递归调用次数不限制。

# 算术求值 (ARITHMETIC EVALUATION)

shell 在某些情况下允许求值算术表达式（参见 `let` 和 `declare` 内置命令以及算术扩展）。求值在固定宽度的整数中进行，不进行溢出检查，但除以 `0` 会被捕获并标记为错误。运算符及其优先级、结合性和值与 C 语言相同。下面的运算符列表被分为具有相同优先级的运算符级别。这些级别按优先级递减的顺序列出。

- `+` `-` `id++` `id--` 变量后自增和后自减
- `-` `-` `+` 变量前自增和前自减
- `-` 一元负和加
- `!` `~` 逻辑取反和位运算取反
- `**` 幂
- `*` `/` `%` 乘法、除法、余数
- `-` 加法、减法
- `<<` `>>` 左移和右位移
- `<=` `>=` `<` 比较
- `==` `!=` 等于和不相等
- `&` 位运算与
- `^` 位运算异或
- `|` 位运算或
- `&&` 逻辑与
- `||` 逻辑或
- `expr?expr` 条件三元运算符
- `*= /= % += &= |= ^= ` 赋值
- `expr1, expr2`

- 以 `0` 开头的常量解释为八进制数。否则，数字以 `0x` 或 `0X` 表示十六进制。

运算符按优先级求值。括号中的子表达式首先求值并可能覆盖优先级。

# 条件表达式 (CONDITIONAL EXPRESSIONS)

条件表达式用于 `[[` 复合命令以及 `test` 和 `[` 命令来测试文件属性并进行字符串和比较。表达式由以下一元或二元操作数组成。如果操作之一的文件参数格式为 `/dev/fd/n`，则检查文件描述符 `n`。如果操作之一的文件参数格式为 `/dev/stdin`、`dev/stdout` 或 `/dev/stderr`，则分别检查文件描述符 `0`、`1` 或 `2`。

除非另有指定，操作操作跟随符号链接并操作链接的目标，而不是链接本身。

在配合 `[[` 时，`<` 和 `>` 运算符使用当前区域进行字典排序。`test` 命令使用 ASCII 排序。

- `-a` 文件如果存在。
- `-b` 文件如果存在且是块设备文件。
- `-c` 文件如果存在且是字符设备文件。
- `-d` 文件如果存在且是目录。
- `-e` 文件如果存在。
- `-f` 文件如果存在且是普通文件。
- `-g` 文件如果存在且设置了组 ID。
- `-h` 文件如果存在且是符号链接。
- `-k` 文件如果存在且设置了粘性位。
- `-p` 文件如果存在且是命名管道（FIFO）。
- `-r` 文件如果存在且可读。
- `-s` 文件如果存在且大小大于0。
- `-t` 文件描述符 `fd` 已打开并指向终端。
- `-u` 文件如果存在且设置了用户 ID。
- `-w` 文件如果存在且可写。
- `-x` 文件如果存在且可执行。

如果文件存在且具有执行权限，则为真。

- `-G file`
如果文件存在且由有效组 ID 所有，则为真。

- `-L file`
如果文件存在且是一个符号链接，则为真。

- `-N file`
如果文件存在且自上次读取以来被修改过，则为真。

- `-O file`
如果文件存在且由有效用户 ID 所有，则为真。

- `-S file`
如果文件存在且是一个套接字，则为真。

- `file1 -ef file2`
如果 `file1` 和 `file2` 指向同一个设备和节点号，则为真。

- `file1 -nt file2`
如果 `file1` 比 `file2` 新（根据修改日期），或者 `file1` 存在而 `file2` 不存在，则为真。

- `file1 -ot file2`
如果 `file1` 比 `file2` 旧，或者 `file2` 存在而 `file1` 不存在，则为真。

- `-o optname`
如果 shell `optname` 已启用，则为真。参见下方 `set` 内置命令 `-o` 选项描述下的选项列表。

- `-v varname`
如果 shell 变量 `varname` 已设置（已赋值值），则为真。

- `-R varname`
如果 shell 变量 `varname` 已设置且是一个名称引用，则为真。

- `-z string`
如果字符串长度为 `0`，则为真。

- `string -n string`
如果字符串长度不为 `0`，则为真。

- `string1 == string2`
如果字符串相等，则为真。为了符合 POSIX 标准，应在 `[ ]` 命令中使用 `=`。在使用此时，它将执行上述描述的模式匹配（复合命令）。

- `string1 != string2`
如果字符串不相等，则为真。

- `string1 < string2`
如果 `string1` 在字典排序上于 `string2` 之前，则为真。

- `string1 > string2`
如果 `string1` 在字典排序上于 `string2` 之后，则为真。

- `arg1 OP arg2`
`OP` 是 `-eq, -ne, -lt, -le, -gt, -ge` 之一。这些算术二元运算符分别在 `arg1` 等于、不等于、小于、小于等于、大于或大于等于 `$arg2$` 时返回。`$Arg1$` 和 `$arg2$` 可以是正整数或负整数。

# 简单命令扩展

当执行一个简单命令时，shell 会从左到右执行以下扩展、赋值和重定向。

1. 解析器标记为变量赋值的单词（位于命令名之前的单词）和重定向将被保存，以供稍后处理。
2. 不是变量赋值或重定向的单词将进行扩展。如果扩展后仍有单词，则第一个单词被视为命令名，其余单词为参数。
3. 重定向将按照上述“重定向（REIRECTION）”部分的描述进行执行。
4. 每个变量赋值中 `=` 之后的文本在赋值给变量之前，将经过波浪号扩展、参数扩展、命令替换、算术扩展和引号删除。

如果没有产生命令名，变量赋值将影响当前的 shell 环境。否则，变量将添加到所执行命令的环境中，且不影响当前的 shell 环境。如果任何赋值尝试给只读变量赋值，则会发生错误，命令以非零状态退出。

如果没有产生命令名，则将执行重定向，但不会影响当前的 shell 环境。如果扩展后仍留有命令名，则按照下文描述继续执行。否则，命令退出。如果其中一个扩展包含命令替换，则命令的退出状态为最后一次执行的命令替换的退出状态。如果没有命令替换，命令以状态零退出。

# 命令执行

在命令被拆分为单词后，如果它结果为一个简单命令和一个可选的参数列表，将采取以下操作。

如果命令名不包含斜杠，shell 将尝试定位它。如果存在同名的 shell 函数，则按照上文“函数（FUNCTIONS）”中的描述调用该函数。如果名称不匹配这些，shell 将在 shell 内置命令（builtins）列表中搜索它。如果找到匹配项，则调用该内置命令。

如果该名称既不是 shell 函数也不是内置命令，且不包含斜杠，bash 将搜索 `PATH` 中的每个元素，寻找包含同名可执行文件的目录。Bash 使用哈希表记录可执行文件的完整路径名（参见内置命令（BUILTIN COMMANDS）中的 `hash` shell）。只有在哈希表中未找到命令时，才会对 `PATH` 中的目录进行完整搜索。如果搜索失败，shell 将搜索名为 `command_not_found_handle` 的定义 shell 函数。如果该函数存在，则以原始名称和原始命令的参数作为参数调用它，该函数的退出状态将成为 shell 的退出状态。如果未定义函数，shell 将打印错误消息并返回退出状态 `127`。

如果搜索成功，或者命令名包含一个或多个斜杠，shell 将在一个独立的执行环境中执行指定的程序。参数 `0` 设置为给定的名称，命令的其余参数设置为给定的参数（如果有）。

如果此执行失败是因为文件不是可执行格式且该文件不是目录，则假设它是一个 shell 脚本（一个包含 shell 命令的文件）。将产生一个子 shell 来执行它。该子 shell 会重新初始化自己，其效果相当于调用了一个新的 shell，但父级 shell 记住的命令位置会被保留。

如果程序是以 `#` 开头的文件，则第一行的剩余部分指定了该程序的解释器。在处理该可执行文件的操作系统上，shell 将执行指定的解释器。解释器的参数由第一行中解释器名称后的可选参数、随后的程序名称以及任何命令参数组成。

# 命令执行环境

 shell 有一个执行环境，由以下内容组成：

- * 调用时继承的打开文件，加上通过重定向指定的修改和添加
- * 由 `cd`、`pushd`、`popd` 设置的当前工作目录
- * 文件创建掩码
- * 标记导出的 shell 变量和函数，以及传递给命令的环境
- * shell 当前捕获的陷阱
- * 调用时启用的选项（通过默认或命令行参数）
- * 通过 `shopt` 启用的选项
- * 使用 `alias` 定义的 shell 别名
- * 各种进程 ID，包括后台作业、`$$` 和 `PPID`

执行非内置命令或 shell 函数的简单命令，它将在独立的执行环境中调用。除非另有说明，否则值继承自 shell：

- * shell 的打开文件
- * 当前工作目录
- * 文件创建掩码
- * 导出的 shell 变量，以及传递给命令的环境
- * shell 捕获的陷阱将重置为 shell 从父 继承的值

对子 shell 环境的修改不会影响 shell 的执行环境。

命令替换、用括号分组的命令以及异步命令将在子 shell 环境中调用，该环境是 shell 环境的副本，但 shell 捕获的陷阱将重置为 shell 在调用时从父 继承的值。作为管道一部分的内置命令同样在子 shell 环境中执行。对子 shell 环境的修改不会影响 shell 的执行环境。

用于执行命令替换的子 shell 会继承父 shell 的 `-e` 选项值。在非 posix 模式下，bash 会此类子 shell 中清除 `-e` 选项。

如果命令后跟着一个 `&` 且未激活作业控制，则该命令的默认标准输入为空文件 `/dev/null`。否则，被调用的命令将继承调用 shell 通过重定向所修改的文件描述符。

## 环境

当程序被调用时，它会获得一个名为环境的字符串数组。这是一个名称-值对的列表，格式为 `name=value`。

shell 提供了多种操作环境的方法。在调用时，shell 会扫描其自身的环境，并为找到每个名称创建一个参数，自动将其标记为导出到子进程。执行的命令继承该环境。`export` 和 `declare -x` 允许向环境中添加和删除参数及函数。如果环境中的某个参数值被修改，新值将成为环境的一部分并替换旧值。任何执行命令所继承的环境由 shell 的初始环境组成（其值可以在 shell 中被修改），减去由 `unset` 命令删除的键对，加上通过 `export` 和 `declare -x` 命令添加的任何项。

任何简单命令或函数的环境可以通过在前面前面加上参数赋值来临时增强，如上文“参数”部分所述。这些赋值语句仅影响该命令所看到的环境。

如果设置了 `-k` （见下文 `set` 内置命令），则所有参数赋值都会放入命令的环境中，而不仅仅是命令名称之前的赋值。

当 bash 调用外部命令时，变量 `_` 被设置为命令的完整文件名，并通过其环境传递给该命令。

## 退出状态

执行命令的退出状态是 `waitpid` 系统调用或等效函数返回的值。退出状态处于 `0` 到 `255` 之间，但下文所述，shell 可能会特殊地使用 `125` 以上的值。shell 内置命令和复合命令的退出状态也限制在此范围之内。在某些情况下，shell 将使用特殊值来指示特定的失败模式。

对于 shell 而言，以零退出状态退出的命令表示成功。退出状态为零表示成功。非零退出状态表示失败。当命令因致命信号 `N` 终止时，bash 使用 `128+N` 的值作为退出状态。

如果未找到命令，创建以执行它的子进程将返回状态 `127`。如果找到了命令但不可执行，则返回状态为 `126`。

如果命令因为扩展或重定向期间的错误而失败，则退出状态大于零。

shell 内置命令在成功时返回状态 `0`（true），在执行期间发生错误时返回非零（false）。所有内置命令均返回退出状态 `2` 以表示用法错误。

Bash 本身返回最后执行命令的退出状态，除非发生语法错误，在这种情况下，它将以非零值退出。另见下文 `exit` 内置命令。

## 信号

`bash` 是交互式的，在没有任何陷阱（traps）的情况下，它忽略 `SIGTERM`（这样 kill 就不会杀掉交互式 shell），并且捕获并处理 `SIGINT`（这样 `wait` 内置命令就可以被中断）。在所有情况下，`bash` 忽略 `SIGQUIT`。如果启用了作业控制，`bash` 忽略 `SIGTIN`、`SIGTTOU` 和 `SIGSTP`。

由 `bash` 运行的非内置命令信号处理器设置为从 shell 继承的值。在未启用作业控制时，异步命令除了这些继承的处理器外，还会忽略 `SIGINT` 和 `SIGQUIT`。作为命令替换结果运行的命令忽略键盘生成的作业控制信号 `SIGTIN`、`SIGTTOU` 和 `SIGSTP`。

shell 默认在接收到 `SIGHUP` 后退出。退出之前，交互式 shell 会向所有运行中或停止的作业重新发送 `SIGHUP`。停止的作业会被发送 `SIGCONT` 以确保它们接收到 `SIGHUP`。为了防止 shell 向特定作业发送信号，应使用 `disown` 内置命令（见下文“shell 内置命令”）从作业表中移除，或使用 `disown -h` 标记为不接收 SIGHUP。

如果使用 `shopt` 设置了 `huponexit` ，当交互式登录 shell 退出时，`bash` 会向所有作业发送 `SIGHUP`。

当 `bash` 正在等待命令并接收到一个已设置陷阱的信号时，陷阱在命令完成之前不会执行。当 `bash` 通过 `wait` 内置命令等待异步命令时，接收到一个已设置陷阱的信号将导致 `wait` 内置命令在陷阱执行后后立即返回一个大于 `128` 的退出状态。

## 作业控制

作业控制指的是选择性停止（挂起）进程执行并在稍后继续（恢复）其执行的能力。用户通常通过操作系统内核终端驱动程序和 bash 共同提供的交互界面使用此功能。

shell 将每个作业与每个管道相关联。它维护一个当前正在执行作业的表格，可以通过键盘命令输入列出这些作业。当 bash 异步（在后台）启动作业时，它会打印一行如下所示的内容：

```
+   [1] 25647
```

表示该作业是作业号 `1`，且与此作业相关的管道中最后一个进程的进程 ID 为 `25647`。单个管道中的所有进程都是同一个作业的成员。Bash 使用作业抽象作为作业控制的基础。

为了便于作业控制用户界面的实现，操作系统维护了当前终端进程组 ID 的概念。该组的成员（其组 ID 等于终端）接收键盘生成的信号，如 `SIGINT`。后台进程对信号免疫。只有前台进程允许从终端读取或向终端写入。挂起字符（通常为 Ctrl+Z）会导致停止。在支持作业控制的操作系统上，挂起字符（通常为 Ctrl+Z）在进程运行时会导致进程停止并将控制权交给 bash。用户可以使用 `bg` 命令将其在后台继续运行，或使用 `fg` 命令将其带到前台。Ctrl+Z 会立即生效，并具有导致输出降级的额外副作用。

shell 将每个作业与每个管道相关联。它维护一个当前正在执行作业的表格，可以通过键盘命令输入列出这些作业。`jobs` 命令。

在 shell 中有多种方法可以引用作业。字符 `%` 引入了作业规范（jobspec）。作业号可以作为 `%n` 被引用。可以使用作业名称的前缀或出现在其命令行中的子字符串来引用一个作业。例如，`%ce` 指向 ce 作业。如果前缀匹配多个作业，bash 会报错。另一方面，使用 `%ce` 则指向任何命令行中包含字符串 ce 的作业。如果该子字符串匹配多个作业，bash 会报错。符号 `%` 和 `%+` 指向当前作业，即上一个在前台被停止或在后台启动的作业。上一个作业可以通过 `%-` 引用。如果只有一个作业，`++` 和 `%-` 可用于引用该作业。在与作业相关的输出（例如 `jobs` 命令的输出）中，当前作业总是标记为 `+`，前一个作业标记为 `-`。单个 `%`（不带任何作业规范）也指向当前作业。

简单命名作业即可将其带到前台：`%1` 是...的同义词。

每当作业状态发生时，shell 都会立即获。。通常，`bash` 会在打印提示符之前报告作业状态的变化，启用 `set` 内置命令的 `-b` 选项，`bash` 会报告任何其他输出。每个进程退出时，任何对 `SIGCHLD` 的陷阱都会执行。

如果在作业停止时尝试退出 `bash`（如果使用 `shopt` 内置命令启用了 `checkjobs` shell 选项并在运行时），shell 会打印警告消息，并且如果启用了 `checkjobs` 选项，会列出作业及其状态。随后可以使用 `jobs` 命令检查其状态。如果在在没有后续命令的情况下再次尝试退出，shell 将不再再次打印警告，并且任何停止的作业都将被终止。

# 提示符 (PROMPTING)

在交互式执行时，bash 在准备好读取命令时显示主提示符 `ps1`，在需要更多输入来完成命令时显示次级提示符 `ps2`。Bash 允许通过插入反斜杠转义特殊字符来自定义这些提示符字符串，这些字符会被解码为：

- `\a` 一个 ASCII 响铃字符 (07)
- `\d` “星期 月 日” 格式的日期（例如，“周二5月26日”）
- `\f` 传递给 `strftime(3)` 的格式，结果被插入提示符字符串中；空格式将产生特定于区域的时间表示。大括号为
- `\e` 一个 ASCII 转义字符 (033)
- `\h` 到第一个 `.` 之前的主机名
- `\H` 主机名
- `\j` 当前由 shell 管理的任务数
- `\l` shell 终端设备名的基名
- `\n` 换行
- `\r` 回车
- `\s` shell 的名称，`$0` 的基名（最后一个斜杠后的部分）
- `\t` 24 小时制 HH:MM:SS 格式的当前时间
- `\T` 12 小时制 HH:MM:SS 格式的当前时间
- `\@` 12 小时 am/pm 格式的当前时间
- `\A` 24 小时制 HH:MM 格式的当前时间
- `\u` 当前用户的用户名
- `\v` bash 的版本（例如，2.00）
- `\V` bash 的发布版本，版本号 + 补丁级别（例如，2.00.0）
- `\w` 当前工作目录，其中 `$HOME` 用波浪号 缩写（使用 `PROMPT_DIRTRIM` 变量的值）
- `\W` 当前工作目录的基名，其中 `$HOME` 用波浪号 缩写
- `\#` 此命令的历史编号
- `\C` 此命令的编号
- `\$` 如果有效 UID 为 0，则显示 #，否则显示 $
- `\Q` 与八进制数 nnn 对应的字符
- `\\` 一个反斜杠
- `\E` 开始一个非打印字符序列，可将终端控制序列嵌入提示符中
- `\E` 一个非打印字符序列

命令编号和历史编号通常不同：命令的历史编号是其在历史列表中的位置，可能包括从历史文件恢复的命令（见下文 HISTORY），而命令编号是当前 shell 会话期间执行的命令序列中的位置。字符串被解码后，将通过参数扩展、命令替换、算术扩展和引号去除进行扩展，这取决于 `promptvars` shell 选项的值（见下文 SHELL BUILTIN COMMANDS 下的 `shopt` 命令描述）。

# READLINE

这是一个在使用用交互式 shell 时处理读取输入的库，除非在调用 shell 时给出了 `noediting`（不编辑）选项。在使用 `read`（读取）`read` 内置命令并带有 `-e` 选项时，也会使用行编辑。默认情况下，行编辑命令与 Emacs 类似。也提供 vi 样式的行编辑界面。可以使用 `set` 内置命令（属于 SHELL BUILT COMMANDS）的 `-o emacs` 或 `-o vi` 选项随时启用行编辑。若要在 shell 运行时关闭行编辑，请使用 `set` 内置命令的 `+0 emacs` 或 `+0` 选项。

# Readline 符号 (Readline Notation)

在本节中，使用 Emacs 风格的符号表示按键。控制键用 `C-key` 表示，例如，`C-n` 表示 Control-N。*元键（Meta keys）*用 `M-key` 表示，因此 M-x 表示 Meta-X。（在带有*元键*的键盘上，M-x 表示 ESC X，即先按 Escape 键再按 x 键）。这使得 ESC 成为*元前缀*。组合 M-C-x 表示 ESC-Control-x，或者按下 Escape 键后按住 Control 键再按 x 键。

Readline 命令可以接受数字参数，这些通常作为重复命令。然而，有时参数的符号具有重要意义。向命令传递一个负参数以向正方向操作（例如，`kill-line`）会导致命令向反方向操作。行为偏离此的命令未在下文中列出。

当一个命令被描述为*杀死（killing）*文本时，被删除的文本会被保存以备将来可能的检索（*产出（yielding）*）。被杀的文本保存在存在*剪切环（kill ring）*中。连续的杀死会导致文本累积为一个单元，可以一次性提取（yank）。不杀死文本的命令会分割剪切环中的块。

# Readline 初始化 (Readline Initialization)

通过将命令放入初始化文件（`inputrc` 文件）对 Readline 进行自定义。该文件的文件名来自 `INPUTRC` 变量的值。如果该变量未设置，默认为 `~/.inputrc`。当程序使用 readline 库并启动时，会读取初始化文件并设置按键绑定和变量。readline 初始化文件中只允许极少数结构。空行被忽略。以 `#` 开头的行是注释。以 `$` 开头的行表示条件结构。其他行表示按键绑定和变量设置。

默认按键绑定可以通过 `inputrc` 文件更改。其他使用此库的程序可能有它们自己的命令和绑定。

例如，

- `- M-Control-u: 通参数（通用参数）`
- `# C-Meta-u: 通参数（通用参数）`

将这些输入 inputrc 将使 M-C-u 执行 readline 的通用参数。

识别以下字符名称：`RUBOUT, DEL, ESC, LFD, NEWLINE, RET, SPACE, TAB`。

# Readline 绑定 (Readline Bindings)

在 `inputrc` 文件中控制按键绑定的语法非常简单。只需要命令名称或宏文本，以及它应该绑定的按键序列。名称可以通过两种方式之一指定：作为符号按键名（可能带有 Meta- 或 Control 前缀），或者作为序列。当使用 keyname:function-name 或 macro 格式时，keyname 是用英文拼读的按键名称。例如：

- `Control-u: universal-argument（通用参数）`
- `Meta-Rubout: backward-kill-word（向后杀死单词）`
- `Control-o: "> output"`

在上面的示例中，C-u 绑定到函数 `universal-argument`，M-DEL 绑定到函数 `backward-kill-word`，而 C-o 绑定运行右侧表示的宏（即插入文本 "> output"）。

在第二种形式 keyseq:function-name 或 macro 中，keyseq 与上述的 keyname 不同之处在于，通过将序列放在双引号内可以指定整个序列。可以使用 GNU Emacs 风格的按键转义，如下例所示，但无法识别符号字符名称。

- `>"C-u": universal-argument（通用参数）`
- `"\xC-r": re-readfile（重新读取文件）`
- `"e[11~": "Function 1"（功能1）`

在此示例中，C-u 再次绑定到函数 `universal-argument`。C-x C-r 绑定到函数 `re-readfile`，而 ESC [ 1 1 ~ 绑定到插入文本 "Function 1"。

完整的 GNU Emacs 风格序列集为

-C- 控制前缀
-M- 元前缀
-\e 转义字符
-\ 斜杠
文字 "
文字 ‘

除了 GNU Emacs 风格转义序列外，还有第二组反斜杠转义可用：

- `\a` 警报（响铃）
- `\b` 退格
- `\d` 删除
- `\f` 页
- `\n` 换行
- `\r` 回车
- `\t` 水平制表
- `\v` 垂直制表
- `\nnn` 值为八进制数 nnn 的八位字符（一到三位）
- `\HH` 值为十六进制数 HH 的八位字符（一到两位十六进制）

在输入宏文本时，必须使用不带引号或双引号表示宏定义。在宏正文中，上述反斜杠转义会被展开。反斜杠会对宏文本中的任何其他字符。

Bash 允许使用 `bind` 内置命令显示或修改当前的 readline 按键绑定。在交互式使用期间可以使用 `set` 内置命令的 `-o` 选项切换编辑模式（见下文 SHELL BUILT COMMANDS）。

# Readline 变量 (Readline Variables)

Readline 拥有用于进一步自定义其行为的变量。可以在 `inputrc` 文件中使用以下语句设置变量



`set variable-name value`

除非另有说明，`readline` 变量可以取值为 `On` 或 `Off`（不区分大小写）。无法识别的变量名将被忽略。当读取变量时，空值或空值、`"on"`（不区分大小写）和 `"1"` 等同于 `On`。所有其他值均等同于 `Off`。这些变量及其默认值如下：

### `bell-style` (audible)

控制当 `readline` 想要响终端铃声时发生的情况。如果设置为 `none`，`readline` 永远不会响铃声。如果设置为 `visible`，如果可用可见响铃，`readline` 将使用可见响铃。如果设置为 `audible`，`readline` 将尝试鸣响终端的铃铛。

### `bind-tty-special-chars` (On)

如果设置为 `On`，`readline` 将尝试将内核终端驱动程序特殊处理的控制字符绑定到相应的 `readline` 等效字符上。

### `colored-stats` (Off)

如果设置为 `On`，`readline` 将使用不同的颜色显示补全内容，以指示其文件类型。颜色定义取自 `LS_COLORS` 环境变量的值。

### `comment-begin` ("#")

在执行 `readline` `insert-comment` 命令时插入的字符串。该命令在 emacs 模式下绑定到 `M-#`，在 vi 模式下绑定到 `#`。

### `completion-ignore-case` (Off)

如果设置为 `On`，`readline` 将以不区分大小写进行文件名匹配和补全。

### `completion-prefix-display-length` (0)

补全列表中公共前缀的字符长度，该长度将不做修改显示。当设置为大于零的值时，在显示补全时，长于该值的公共前缀将被省略号替换。

### `completion-query-items` (100)

这决定了何时询问用户是否查看由 `possible-completions` 命令生成的可能补全数量。它可以设置为任何大于或等于 0 的整数值。如果补全数量大于或等于此变量的值，将询问用户是否想要查看它们；否则，它们将直接列在终端上。

### `convert-meta` (On)

如果设置为 `On`，`readline` 将通过剥离第八位并加上转义字符（实际上是使用 escape 作为 meta 前缀），将设置了第八位的字符转换为 ASCII 键位序列。

### `disable-completion` (Off)

如果设置为 `On`，`readline` 将抑制单词补全。补全字符将插入到行中，就像它们被映射为自插入一样。

### `editing-mode` (emacs)

控制 `readline` 是否以一组类似于 Emacs 或 vi 的键绑定开始。`editing-mode` 可以设置为 `emacs` 或 `vi`。

### `echo-control-characters` (On)

设置为 `On` 时，在指示支持的操作系统上，`readline` 会回显对应键盘生成的信号对应的字符。

### `enable-keypad` (Off)

设置为 `On` 时，`readline` 在调用时尝试启用应用程序小键盘。某些系统需要此来启用方向键。

### `enable-meta-key` (On)

如果设置为 `On`，`readline` 在调用时尝试启用终端声支持的任何 meta 修饰键。在许多终端上，meta 键用于发送八位字符。

### `expand-tilde` (Off)

如果设置为 `On`，当 `readline` 尝试单词补全时将执行波号扩展。

### `history-preserve-point` (Off)

如果设置为 `On`，历史代码尝试在 `previous-history` 或 `next-history` 获取的每条历史行上将光标（point）放置在相同位置。

### `history-size` (0)

设置历史列表中保存的历史条目的最大数量。如果设置为 0，将删除所有现有的历史条目并保存新条目。如果设置为小于 0 的值，历史条目的数量不受限制。默认情况下，历史条目的数量不受限制。

### `horizontal-scroll-mode` (Off)

设置为 `On` 时，`readline` 使用单行显示，当输入超过屏幕宽度时，在单屏上水平滚动输入，而不是换到新行。

### `input-meta` (Off)

如果设置为 `On`，`readline` 将启用八位输入（即它将不会从读取的字符中删除高位），无论终端声称支持与。`meta-flag` 是该变量的别名。

### `isearch-terminators` ("[C-J]")

用于终止增量搜索且随后不将该字符作为命令执行的字符串。如果未给此变量赋值，字符 `ESC` 和 `C-J` 将终止增量搜索。

### `keymap` (emacs)

设置当前的 `readline`。有效键映射集有 `emacs`、`emacs-standard`、`emacs-meta`、`emacs-ctlx`、`vi-command` 和 `vi-insert`。`vi` 等同于 `vi-command`；`emacs` 等同于 `emacs-standard`。默认值为 `emacs`；`editing-mode` 的值也会影响默认小键盘。

### `keyup-timeout` (500)

指定 `readline` 在读取歧义键位序列时等待字符的持续时间（可以使用目前的输入形成完整的键位序列，也可以通过额外输入来完成更长的键位序列）。如果在超时时间内未接收到输入，`readline` 将使用较短但完整的键位序列。该值以毫秒为单位，因此 `1000` 表示 `readline` 将等待一秒的额外输入。如果设置为小于等于 0 的值或非数值值，`readline` 将等待按下另一个按键以决定补全哪个键位序列。

### `mark-directories` (On)

如果设置为 `On`，补全的目录名称将附带一个斜杠。

### `mark-modified-lines` (On)

如果设置为 `On`，已修改的历史行将进行标记。

### `mark-symlinked-directories` (On)

如果设置为 `On`，补全的目录将附带斜杠。

### `match-hidden` (On)

如果设置为 `On`，`readline` 匹配以隐藏开头的文件。

### `menu-display-prefix` (Off)

如果设置为 `On`，`readline` 显示正在补全的单词的前缀。

### `output-meta` (On)

如果设置为 `On`，`readline` 将设置了第八位的字符转换为 ASCII 键位序列。

### `page-completions` (On)

如果设置为 `On`，`readline` 使用类似于分页器的机制进行补全。

### `print-completions-horizontally` (Off)

如果设置为 `On`，水平显示补全。

### `revert-all-at-newline` (Off)

如果设置为 `On`，`readline` 将撤销对历史行的更改。

### `show-all-if-ambiguous` (Off)

如果设置为 `On`，具有多个补全项会导致列表。

### `show-all-if-unmodified` (Off)

如果设置为 `On`，未修改的具有多个补全。

### `show-mode-in-prompt` (Off)

如果设置为 `On`，在提示符开头添加字符。

### `skip-completed-text` (Off)

如果设置为 `On`，`readline` 不在单词中插入字符。

### `visible-stats` (Off)

如果设置为 `On`，文件名后将附带一个由 `stat(2)` 报告的文件类型字符。

## 条件结构

`Readme` 实现了一种类似于预处理器条件编译特性的机制，允许根据测试结果执行键绑定和变量设置。

### `if`

`$if` 结构允许根据编辑模式、使用的终端或使用 `readline` 的应用程序进行绑定。测试文本延伸到行尾；不需要字符来隔离它。

`$if` 指令的 `mode` 用于测试 `readline` 是否处于 emacs 或 vi 模式。这可以与 `set keymap` 命令结合使用，例如仅当 `readline` 以 emacs 模式启动时为 `emacs-standard` 和 `emacs-ctlx` 键映射设置绑定。

### `term`

`term=` 形式可以包含特定的终端键绑定，允许绑定终端功能键输出的键位序列。等侧的单词将与终端的全名以及第一个 `-` 之前的部分进行测试。这允许 `sun` 匹配 `sun` 和 `sun-cmd`，例如。

### `application`

`application` 结构用于包含特定应用程序的设置。每个使用 `readline` 库的程序都会设置应用程序名称，初始化文件可以针对特定值进行测试。这可以用于绑定对特定程序有用的序列。例如，以下内容为 `bash` 添加了一个可以引用当前或之前单词的序列：

```
$if Bash # 当前或之前的单词 "C-Q": "\b"\f\"

$endif
```



`$endif` 该命令如上一个示例所示，终止 `$if` 命令。`$Else` 命令在 `$if` 指令的分支中测试失败时执行。`$Include` 接受单个文件名作为参数并从该文件中读取命令和绑定。例如，以下指令将读取 `/etc/inputrc`：

```
$include /etc/inputrc
```



# 搜索

Readline 提供了用于在命令历史（见下文 HISTORY 部分）中搜索包含指定字符串的行的命令。有两种搜索模式：增量式和非增量式。

增量搜索在用户完成输入搜索字符串之前就开始了。随着搜索字符串每个字符的输入，readline 都会显示历史中与目前字符串匹配的下一个条目。增量搜索只需要找到所需的历史条目所需的字符数量。`search-terminators` 变量值中的字符被用于终止增量搜索。如果该变量未赋值，则 `Escape` 和 `Control-J` 字符将终止增量搜索。`Control-G` 将中止增量搜索并恢复原始行。当搜索结束时，包含该搜索内容的历史条目将成为当前行。

要查找历史列表中的其他匹配项，请根据情况输入 `Control-S` 或 `Control-R`。这将在历史中向后或向前搜索与目前字符串匹配的下一个条目。任何其他绑定到 readline 的键序列都将终止搜索并执行该命令。例如，换行将终止搜索并接受该行，从而执行历史列表中的命令。

Readline 会记住上一次的增量搜索字符串。如果在输入两个 `Control-R` 之间没有定义新搜索字符串的中间字符，则使用任何记忆的搜索字符串。

非增量搜索在开始搜索匹配的历史行之前，会读取整个搜索字符串。搜索字符串可以是用户输入的，也可以是当前行内容的一部分。

# Readline 命令名称

以下是命令名称及其默认未绑定的键序列列表。没有附带键序列的命令名称默认均未绑定。在以下描述中，`point` 指代当前光标位置，`mark` 指代由 `set-mark` 命令保存的光标位置。`point` 和 `mark` 之间的文本被称为 `region`（区域）。

# 移动命令

- `beginning-of-line` (`C-a`)
移动到当前行的开头。

- `end-of-line` (`C-e`)
移动到行的末尾。

- `forward-char` (`C-f`)
向前移动一个字符。

- `backward-char` (`C-b`)
向后移动一个字符。

- `forward-word` (`M-f`)
移动到下一个单词的末尾。单词由字母数字字符（字母和数字）组成。

- `backward-word` (`M-b`)
移动到当前或上一个单词的开头。单词由字母数字字符（字母和数字）组成。

- `shell-forward-word`
移动到下一个单词的末尾。单词由未加引号的元字符界定。

- `shell-backward-word`
移动到当前或上一个单词的开头。单词由未加引号的元字符界定。

- `clear-screen` (`C-l`)
清除屏幕，并将当前行留在屏幕顶部。带有参数时，则刷新当前行而不清除屏幕。

- `redraw-current-line`
刷新当前行。

# 历史操作命令

- `accept-line` (`Newline`, `Return`)
无论光标所在何处，均接受该行。如果该行非空，则根据 `HISTCONTROL` 变量的状态添加到历史列表中。如果该行是修改过的历史行，则将历史行恢复到其原始状态。

- `previous-history` (`C-p`)
从历史列表中获取上一个命令，在列表中向后移动。

- `next-history` (`C-n`)
从历史列表中获取下一个命令，在列表中向前移动。

- `beginning-of-history` (`M-<`)
移动到历史中的第一行。

- `end-of-history` (`M->`)
移动到输入历史的末尾，即当前输入的行。

- `reverse-search-history` (`C-r`)
从当前行开始向后搜索，并在历史中必要时向上 `up` 。这是一个增量搜索。

- `forward-search-history` (`C-s`)
从当前行开始向前搜索，并在历史中必要时向下 `down`移动。这是一个增量搜索。

- `non-incremental-reverse-search-history` (`M-p`)
从当前行开始，使用非增量搜索对用户提供的字符串进行历史向后搜索。

- `non-incremental-forward-search-history` (`M-n`)
使用非增量搜索对用户提供的字符串进行历史向前搜索。

- `history-search-forward`
在历史中向前搜索当前行开头与 `point` 之间的字符字符串。这是一个非增量搜索。

- `history-search-backward`
在历史中向后搜索当前行开头与 `point` 之间的字符字符串。这是一个非增量搜索。

- `yank-nth-arg` (`M-y`)
在 `point` 处插入上一个命令的第一个参数（通常是上一行的第二个单词）。带有数字参数 *n* 时，则插入上一个命令的第 *n* 个单词（上一个命令从 0 开始）。负参数插入上一个命令末尾的第 *n* 个单词。一旦参数 *n* 计算完成，由于指定了 `“in”` 历史扩展，该参数将被提取。

- `yank-last-arg` (`M-,` `M_-`)
插入上一个命令的最后一个参数（上一个历史条目的最后一个单词）。带有数字参数时，其行为与 `yank-nth-arg` 完全相同。在历史列表中向后移动，依次插入每行的最后一个单词（或第一次调用时参数指定的单词）。提供给这些连续调用的任何数字参数决定了在历史中移动的方向（向后或向前）。

- `insert-last-arg` (`M-,` `M_-`)
`yank-last-arg` 的别名。

- `operate-and-get-next` (`C-o`)
接受当前行并从历史中相对于当前行获取下一行。任何参数都会被忽略。

- `edit-and-execute-command` (`C-e`)
在当前行上调用编辑器，并执行结果。Bash 尝试按顺序调用 `VISUAL`、`EDITOR` 和 `emacs` 作为编辑器。

# 修改文本命令

- `end-of-file` (usually `C-d`)
指示文件结束的字符，例如通过 “stty” 设置。当行没有字符且 `point` 在行开头时，readline 将其解释为输入结束并返回 EOF。

- `delete-char` (`C-d`)
删除 `point` 处的字符。如果该函数绑定到与 tty 相同的字符（`C-d` 通常如此），请参见上文产生的影响。

- `backward-delete-char` (`Rubout`)
删除光标后的字符。当给定数字参数时，将删除的文本保存到 `kill ring` 中。

- `forward-backward-delete-char`
删除标下的字符，除非光标在行末尾，此时光标后的字符将执行删除。

- `quoted-insert` (`C-v`)
将输入的下一个字符原样添加到行。这是输入字符 `C-q` 的方式。

- `tab-insert` (`C-v TAB`)
插入制表符字符。

- `self-insert` (`a`, `b`, `A`, `1`, ...)
插入输入的字符。

- `transpose-chars` (`C-t`)
将 `point` 之前的字符向前移动到 `point` 处的字符，同时也让 `point` 向前。如果 `point` 在行末尾，将交换 `point` 之前的两个字符。

- `transpose-words` (`M-t`)
将 `point` 之前的单词越过 `point` 之后的单词，同时也让 `point` 越过该单词。如果 `point` 在行末尾，将交换行的最后两个单词。

# `upcase-word` (`M-u`)

将当前（或后续）单词转换为大写。带有负参数时，会将上一个单词转换为大写，但不移动光标。

# `downcase-word` (`M-I`)

将当前（或后续）单词转换为小写。带有负参数时，会将上一个单词转换为小写，但不移动光标。

# `capitalize-word` (`M-c`)

将当前（或后续）单词的首字母大写。带有负参数时，会将上一个单词的首字母大写，但不移动光标。

# `overwrite-mode`

切换覆盖模式。带有显式正数字参数时切换到覆盖模式。带有显式非正数字参数时切换到插入模式。此命令影响 emacs模式；vi 模式的覆盖方式不同。每次调用 `readline()` 都会启动插入模式。在覆盖模式下，绑定到 `self-insert` 的字符将替换光标处的文本而不是向右推文本。绑定到 `backward-delete-char` 的字符将光标前的字符替换为空格。默认情况下，此命令未绑定。

# 剪切与粘贴 (Killing and Yanking)

## `kill-line` (`C-k`)

剪切从光标位置到行尾的文本。

## `backward-kill-line` (`C-x Rubout`)

向后剪切到行首。

## `unix-line-discard` (`C-u`)

从光标位置向后剪切到行首。剪切的文本保存在剪切环（kill-ring）中。

## `kill-whole-line`

剪切当前行的所有字符，无论光标在哪里。

## `kill-word` (`M-d`)

剪切从光标到当前单词结束，或者从单词间隙到下一个单词结束。单词边界与 `forward-word` 使用的相同。

## `backward-kill-word` (`M-Rubout`)

剪切光标之前的单词。单词边界与 `backward-word` 使用的相同。

## `shell-kill-word` (`M-d`)

剪切从光标到当前单词结束，或者从单词间隙到下一个单词结束。单词边界与 `shell-forward-word` 使用的相同。

## `shell-backward-kill-word` (`M-Rubout`)

剪切光标之前的单词。单词边界与 `shell-backward-word` 使用的相同。

## `unix-word-rubout` (`C-w`)

使用空格作为单词边界，剪切光标之前的单词。剪切的文本保存在剪切环中。

## `unix-filename-rubout`

使用空格和斜杠字符作为单词边界，剪切光标之前的单词。剪切的文本保存在剪切环中。

## `delete-horizontal-space` (`M-\`)

删除光标周围所有的空格和制表符。

## `kill-region`

剪切当前区域内的文本。

## `copy-region-as-kill`

将区域内的文本复制到剪切缓冲区中。

## `copy-backward-word`

将光标之前的单词复制到剪切缓冲区。单词边界与 `backward-word` 相同。

## `copy-forward-word`

将光标后的单词复制到剪切缓冲区。单词边界与 `forward-word` 相同。

## `yank` (`C-y`)

将剪切环顶部的内容粘贴到光标所在的缓冲区。

## `yank-pop` (`M-y`)

旋转剪切环并粘贴新的顶端内容。仅在执行 yank 或 yank-pop 后有效。

# 数字参数 (Numeric Arguments)

## `digit-argument` (`M-0`, `M-1`, ..., `M—`)

将此数字添加到已累积的参数中，或开始一个新参数。M— 开始负参数。

## `universal-argument`

这是指定参数的另一种方式。如果此命令后跟着一个或多个数字（可选带有前负号），则这些数字将重新定义参数。如果命令后直接跟着数字，执行 `universal-argument` 会结束数字参数，否则会被忽略。一种特殊情况是：如果此命令后紧跟着一个既不是数字也不是负号的字符，则下一个命令的参数计数将乘以四。参数计数初始为一，因此第一次执行此函数将使参数计数变为 4，第二次变为 16，依此类推。

# 补全 (Completing)

## `complete` (`TAB`)

尝试对光标前的文本进行补全。Bash 会依次尝试将文本视为变量（如果以 $ 开头）、用户名（如果以 ~ 开头）、主机名（如果以 @ 开头）或命令（包括别名和函数）进行补全。如果这些都不产生匹配项，则尝试文件名补全。## `possible-completions` (`M-?`)

列出光标前文本可能的补全。

## `insert-completions` (`M-*`)

插入所有由 `possible-completions` 生成的光标前文本补全。

## `menu-complete`

与 `complete` 类似，但会将待补全的单词替换为补全列表中的单个匹配项。通过补全列表重复执行 `menu-complete` 步骤，依次插入每个匹配项。在列表末尾，会响铃（取决于 bell-style 的设置）并恢复原始文本。参数 m 会在匹配列表中向前移动 n 个位置；可以使用负参数向后移动。此命令本应绑定到 TAB，但默认未绑定。

## `menu-complete-backward`

与 `menu-complete` 相同，但如果给 `menu-complete` 给了负参数，则在可能的补全列表中向后移动。此命令默认未绑定。

## `delete-char-or-list`

如果不在行首或行尾，则删除光标下的字符（类似于 delete-char）。如果在行尾，行为与 `possible-completions` 相同。

## `complete-filename` (`M-`)

对光标前的文本执行文件名补全。

## `possible-filename-completions` (`C-x /`)

列出光标前可能的文件名补全。

## `complete-username` (`M~`)

对光标前的文本执行用户名补全。

## `possible-username-completions` (`C-x ~`)

列出光标前可能的用户名补全。

## `complete-variable` (`M-`)

对光标前的文本执行变量补全。

## `possible-variable-completions` (`C-x $`)

列出光标前可能的变量补全。

## `complete-hostname` (`M@`)

对光标前的文本执行主机名补全。

## `possible-hostname-completions` (`C-x @`)

列出光标前可能的主机名补全。

## `complete-command` (`M-!`)

对光标前的文本执行命令补全。按别名、保留字、shell 函数、shell 内内置以及可执行文件的顺序进行匹配。

## `possible-command-completions` (`C-x !`)

列出光标前可能的命令补全。

## `dynamic-complete-history` (`M-TAB`)

对光标前的文本进行动态补全，与历史列表进行匹配。

## `dabbrev-expand`

对光标前的文本进行菜单补全，与历史列表进行匹配。

## `complete-into-braces` (`M{}`)

执行文件名补全并将补全列表在大括号内，以便 shell 可以使用该列表（见上文的大括号展开）。

# 键盘宏 (Keyboard Macros)

## `start-kbd-macro` (`C-x (`)

开始记录输入的字符到当前键盘宏。

## `end-kbd-macro` (`C-x)`)

停止记录输入的字符并存储定义。

## `call-last-kbd-macro` (`C-x e`)

重新执行最后定义的键盘宏，宏中的字符就像在键盘上输入的一样。

## `print-last-kbd-macro`

以 inputrc 文件的格式打印最后定义的键盘宏。

# 其他 (Miscellaneous)

## `re-read-init-file` (`C-x C-r`)

读取 inputrc 文件的内容，并纳入其中的任何变量赋值。

## `abort` (`C-g`)

取消当前的编辑命令并响终端铃（取决于 bell-style 的设置）。

## `do-uppercase-version` (`M-a`, `M-b`, `M-x`, ...)

如果元字符 x 是小写的，则运行绑定到相应大写字符的命令。

## `prefix-meta` (`ESC`)

将下一个字符元化。ESC f 等同于 Meta-f。

## `undo` (`C-_, C-x C-u`)

增量撤销，每行单独记忆。

## `revert-line` (`M-r`)

撤销对此行进行的所有更改。这相当于反复执行撤销命令，直到该行恢复到初始波浪展开状态 (M-&)。

对当前单词执行波浪展开。

`set-mark` (`C-@`, `M-<csp>`) 将标记（mark）设置在当前光标处。如果提供了数值参数，则将标记设置在相应位置。

`exchange-point-and-mark` (`C-x C-x`) 交换光标和标记。当前的光标位置被设置为之前保存的位置，而旧的光标位置被保存为标记。

`character-search` (`C-J`) 读取一个字符并移动到该字符的下一次出现处。负数计数将搜索之前的出现处。

`character-search-backward` (`M-C-J`) 读取一个字符并移动到该字符的上一次出现处。负数计数将搜索后续的出现处。

`skip-csi-sequence` 读取字符以消耗多键序列，例如为 Home 和 End 等键定义的序列。此类序列以控制序列指示符（CSI）开头，通常为 ESC[-。如果此序列没有显式绑定到某个按键，则产生的序列将产生产生影响（除了执行 readline 命令外），而不是将字符插入到编辑缓冲区。它默认未绑定的，通常绑定到 ESC[-。

`insert-comment` (`M-#`) 在不提供数值参数的情况下，将 readline comment-begin 变量的值插入到当前行的开头。如果提供了数值参数，此命令将作为切换开关：如果行开头的字符与 comment-begin 的值不匹配，则插入该值；否则，从行开头删除 comment-begin 中的字符。无论何种情况，如果之前输入过，该行都被视为换行符。comment-begin 的默认值使此命令将当前行变为注释。如果数值参数导致注释字符被移除，该行将由 shell 执行。

`glob-complete-word` (`M-g`) 将光标前的单词视为路径名扩展的模式，并隐式地添加星号 **。该模式用于生成匹配的文件名列表以供可能的补全。

`glob-expand-word` (`C-x *`) 将之前的单词视为路径名扩展的模式，并插入匹配的文件名列表以替换该单词。如果提供了数值参数，则在路径扩展之前添加星号 **。

`glob-list-expansions` (`C-x g`) 显示 glob-expand-word 将会生成的扩展列表，并重绘行。如果提供了数值参数，则在路径扩展之前添加星号 **。

## `dump-functions`

将所有函数及其按键绑定打印到 readline 输出流。如果提供了数值参数，输出的格式将处理为可以作为 inputrc 文件的一部分。

## `dump-variables`

将所有可设置的 readline 变量及其值打印到 readline 输出流。如果提供了数值参数，输出的格式将处理为可以作为 inputrc 文件的一部分。

## `dump-macros`

打印所有绑定到宏的 readline 键序列及其输出的字符串。如果提供了数值参数，输出的格式将处理为可以作为 inputrc 文件的一部分。

## `display-shell-version` (`C-x C-v`)

显示关于当前 bash 实例的内部版本信息。

## 可编程补全 (Programmable Completion)

当尝试对命令的参数进行补全，且该命令已通过下文定义的“完整的 SHELL 内置命令”定义了补全规范（compspec）时，将调用可编程补全。

首先，识别命令名称。如果空行开头是命令单词，则将使用带有 -E 选项定义的补全 compspec。如果为该命令定义了 compspec，则使用该 compspec 生成该单词的可能补全列表。如果命令单词是全名（fullname），则会首先搜索全名的 compspec。如果没有为全名找到 compspec，将尝试寻找斜杠后部分的 compspec。如果这些搜索都没有找到 compspec，则将使用带有 -D 选项定义的任何补全 compspec 作为默认值。

一旦找到 compspec，将使用它来生成匹配单词列表。如果未找到 compspec，则执行上述上文“补全（Completing）”部分描述的默认 bash 补全。

首先，使用 compspec 指定的操作。只返回以正在补全的单词为前缀的匹配项。当使用 -f 或 -d 选项进行文件名或目录名补全时，将使用 shell 变量 IGNORE 来过滤匹配项。

接下来生成由 -G 选项指定的路径名模式的补全。模式生成的单词可能与正在补全的单词不匹配。不使用 shell 变量 GLOBIGNORE 来过滤匹配项，但会使用 IGNORE 变量。

接下来，考虑作为 -W 选项参数的字符串。该字符串使用 IFS 特殊变量中的字符作为分隔符进行分割。遵循 shell 引用。每个单词随后将使用括号扩展、波浪展开、参数和变量扩展、命令替换和算术扩展进行扩展，如“扩展（EXPANSION）”部分所述。扩展的结果将与正在补全的单词进行前缀匹配，匹配的单词将成为可能的补全。

在生成这些匹配项后，将调用使用 -F 和 -C 选项指定的任何函数或命令。当调用命令或函数时，将为 COMP_LINE、COMP_POINT、COMP_KEY 和 COMP_TYPE 变量赋值，正如“shell 变量”部分所示。如果调用了 shell 函数，还会设置 COMP_WORDS 和 COMP_CWORD 变量。当调用命令或函数时，第一个参数 ($S1) 是正在补全参数的命令名称，第二个参数 ($S2) 是正在补全的单词，第三个参数 ($S3) 是当前行上正在补全的单词。不会对生成的补全进行过滤；函数或命令可以自由生成匹配项。

调用使用 -F 指定的任何函数。第一个函数可以使用 shell 功能（包括下文描述的 compgen 内置命令）来生成匹配项。它必须将可能的补全放入 COMPREPLY 数组中，每个元素一个。

接下来，在使用 -C 指定的任何命令，等同于命令替换的环境调用。它应该向标准输出打印补全列表，每行一个。必要时，可以使用反斜杠转义换行符。

在生成所有可能的补全后，对列表应用由 -X 选项指定的过滤器。过滤器是路径名扩展的模式；模式中的 & 将替换为正在补全单词的文本。字面量 & 可以用反斜杠转义；在尝试匹配之前删除反斜杠。任何匹配模式的补全将从列表中移除。领先的符号取反模式；在这种情况下，不匹配模式的补全将被移除。

最后，将 -P 和 -S 选项指定的任何前缀和后缀添加到补全列表的每个成员中，并将结果返回 readline 补全代码作为可能的补全列表。

如果之前应用的操作没有生成任何匹配项，且在定义 compspec 时提供了 -o dirnames 选项，则尝试进行目录名补全。

如果在定义 compspec 时提供了 -plus dirs 选项，则尝试进行目录名补全，并将任何匹配项添加到其他操作的结果中。

默认情况下，如果指定了 compspec，其生成的任何内容将作为完整的补全集返回给补全代码。不会尝试默认的 bash 补全；如果在定义 compspec 时提供了 -bashdefault 选项，则当 compspec 未生成匹配项时将尝试 bash 默认补全。如果在定义 compspec 时提供了 - default 选项，则使用 readline 的默认

补全将由 compspec（以及如果尝试，则由默认的 bash 补全）执行，未生成任何匹配项。

当 compspec 指明需要进行目录名补全时，可编程补全函数会调用 readline 在完成的指向目录的符号链接名称后添加斜杠，这取决于 readline `mark-directories` 变量的值，而不受 readline `mark-synlinked-directories` 变量设置的限制。

对动态修改补全提供了某些支持。这在与 `complete -D`指定的默认补全结合使用时最为有用。作为补全处理程序执行的 shell 函数可以通过返回退出状态 124 来指示应该重试补全。如果 shell 函数返回 124，并更改了与正在尝试补全的命令关联的 compspec（该命令在函数执行时作为第一个参数提供），则可编程补全将从头开始重启，尝试为该命令寻找新的 compspec。这允许在尝试补全时动态构建一组补全，而不是一次性加载所有。

例如，假设有一个 compspec 库，每个 compspec 都存储在一个与命令名相对应的文件中，以下默认补全函数将动态加载补全：

```
```



```
_completion_loader() { "/etc/bash_completion.d/$1.sh" >/dev/null 2>&1 && { return 124 } complete -D -F _completion_loader -o bashdefault -o default
```



# 历史 (HISTORY)

当启用 `set` 内置命令的 `-o history` 选项时，shell 提供对之前输入的命令列表的访问。变量 `HISTSIZE` 的值用于历史列表中保存的命令数量。最后 `HISTSIZE` 条命令（默认值为 0）的文本将被保存。shell 在变量和变量扩展（上文 EXPANSIONS）之前、但在执行历史扩展之后将每个命令存储在历史列表中，但受 shell 变量 `HISTIGNORE` 和 `HISTCONTROL` 值的影响。

启动时，历史由变量 `HISTFILE` 指定的文件名（默认为 `~/.bash_history`）初始化。文件名通过 `HISTFILE` 的值进行验证，必要时会被截断，使其包含不超过 `HISTFILESIZE` 值指定的行数。如果 `HISTFILESIZE` 未设置，或设置为 null、非数值值或小于零的数值，则历史不被截断。读取历史时，以历史注释字符开头紧跟数字的行将被解释为时间戳，取决于 `HISTTIMEFORMAT` 变量的值。当启用的 shell 退出时，最后 `HISTSIZE` 行将从历史列表复制到 `HISTFILE`。如果启用了 `histappend` 选项（见下文 SHELL BUILT COMMANDS 中 `shopt` 的描述），这些行将追加到历史文件中，否则历史文件将被覆盖。如果 `HISTFILE` 未设置或历史文件不可写，则历史不会被保存。如果设置了 `HISTTIMEFORMAT` 变量，时间戳将写入历史文件并用历史注释字符标记，以便在跨 shell 会话时保留。这使用历史注释字符来区分时间戳和其他历史行。保存历史后，历史文件将被截断，使其包含不超过 `HISTFILESIZE` 行。如果 `HISTFILESIZE` 未设置，或设置为 null、非数值值或小于零的数值，则历史文件不被截断。

可以使用内置命令 `fc`（见下文 SHELL BUILT COMMANDS）列出或编辑并重新执行历史列表的一部分。`history` 内置命令可用于显示或修改历史列表并操作历史文件。当使用命令行编辑时，每个编辑模式下都提供了搜索命令，以访问历史列表。

shell 允许控制哪些命令可能导致 shell 仅保存输入命令的子集。如果启用了 `HISTCONTROL` 和 `cmdhist` shell 选项，shell 将尝试将多行命令的每一行保存在历史条目中，并在必要处添加分号以保持语法正确性。`lithist` shell 选项导致 shell 使用嵌入换行符而非分号来保存命令。见下文 SHELL BUILT COMMANDS 中 `shopt` 内置命令的描述以获取有关设置和取消 shell 选项的信息。

# 历史扩展 (HISTORY EXPANSION)

shell 支持类似于 csh 中历史扩展的功能。本节描述了可用的语法特征。此功能在交互式 shell 中默认启用，可以使用下文 SHELL BUILT COMMANDS 中 `set` 命令的 `+H` 选项禁用。非交互式 shell 默认不执行历史扩展。

历史扩展将历史列表中的单词引入输入流，便于重复命令、将上一个命令的参数插入到当前输入行，或快速修复之前命令中的错误。

历史扩展在读取完完整行后立即执行，在 shell 将其拆分为单词之前。首先是确定在替换时使用历史列表中的哪一行。其次是选择行的部分包含在当前行中。从历史中选择的行称为“事件”（event），被操作的行部分被称为对象。多种修饰符可以操作所选单词。行拆分为单词的方式与视为单个单词时相同。历史扩展通过历史扩展字符（默认为 `!`）的出现引入。只有反斜杠（`\`）和单引号可以引用历史扩展字符。

如果在紧随历史扩展字符之后发现以下几个字符，即使它们未被引号引用，也会抑制历史扩展：空格、制表符、换行符、回车符和 `=`。如果启用了 `extglob` shell 选项，`(` 将抑制扩展。

可以使用 `shopt` 内置命令设置的若干选项来定制历史扩展的行为。如果启用了 `histverify` 选项（见下文 `shopt` 描述）并正在使用 `readline`，则历史替换不会立即传递给 shell。`history` 内置命令的 `-p` 选项可以在执行前查看历史扩展将做什么。`history` 内置命令的 `-s` 选项用于将命令添加到列表末尾而不实际执行。shell 允许控制历史扩展使用的各种字符（见上文 Shell Variables）。shell 在写入历史文件时使用历史注释标记时间戳。

# 事件标识符 (Event Designators)

事件标识符是对历史列表中命令条目的引用。除非引用是绝对的，否则事件相对于历史列表的位置。

`!` 历史替换的开始，除非后面跟着空格、换行符、回车符或 `=`（当启用 `extglob` 选项时）。

`!n` 引用第 n 行命令。

`!-n` 引用当前命令减 n。

`!!` 引用上一条命令。这是 `!-1` 的同义词。

`$string` 引用当前位置之前以 `string` 开头的最近命令。

`?string[?]` 引用当前位置之前包含 `string` 的最近命令。如果 `string` 紧跟换行符，可以省略结尾的 `?`。

`^string1^string2` 快速替换。重复上一条命令，将 `string1` 替换为 `string2`。等同于 `!:s/string1/string2`（见下文修饰符）。

`!#` 目前为止输入的整个命令行。

# 单词标识符 (Word Designators)

单词标识符用于从事件中选择所需的单词。`:` 分隔事件规范和单词标识符。如果单词标识符以 `^`、`$`、`*` 或 `%` 开头，可以省略 `:`。单词从行开始编号，第一个单词用 `0 (zero)` 表示。单词以单空格分隔插入当前行。

`0 (zero)` 第零单词。对于 shell 而言，这就是命令单词。

`n` 第 n 个单词。

`^` 第一个参数。即单词 1。

`$` 最后一个单词。这通常是最后一个参数，但如果行只有一个单词，它将扩展为零单词。

`%` 由最近 `?string?` 搜索匹配的单词。

`x-y` 单词范围；`-y'` 缩写为 `0-y*`。

* 除第零词以外的所有单词。这是 `1-$` 的同义词。如果事件中只有一个单词，使用 `**` 并不是错误；在这种情况下将返回空字符串。
* `x*` 是 `x-$` 的缩写。
* `x-` 像 `x*` 一样缩写 `x-$`，但省略了最后一个单词。

如果在未提供事件指定的情况下提供了单词标识符，则使用上一个使用的命令作为事件。

# 修饰符

在可选的单词标识符之后，可能会出现一个或多个以下修饰符序列，每个修饰符前面都有一个 `:`。

- `-h`: 删除结尾的文件名部分，只保留头部（head）。
- `-t`: 移除所有前面的文件名部分，保留尾部（tail）。
- `-r`: 删除 `.xxx` 格式的结尾后缀，保留基文件名（basename）。
- `-e`: 删除末尾后缀以外的所有内容。
- `-p`: 打印新命令但不执行它。
- `-q`: 对替换的单词加引号，转义后续的替换。
- `-x`: 如 `q` 一样对替换的单词加引号，但在空格和换行符处拆分单词。
- `s/old/new/` 替换事件行中第一次出现的 `old`。可以使用任何分隔符代替 `/`。如果该分隔符是事件行的最后一个字符，则该分隔符是可选的（可以省略）。可以使用单个反斜杠在 `old` 和 `new` 中对分隔符进行引号处理。如果 `new` 中出现 `&`，则它被替换为 `old`。单个反斜杠会对 `&` 进行引号处理。如果 `old` 为空，则将被设置为上一次替换的 `old`，或者如果没有发生历史替换，则设置为 `?:string[?]` 搜索中的最后一个字符串。
- `&`: 重复该替换。
- `g`: 应用于整个事件行的更改。这与 `s': :gs/old/new/` 以及 `&:` 配合使用。如果与 `:s` 使用，可以使用任何分隔符代替 `/`，如果该分隔符是事件行的最后一个字符，则该分隔符是可选的。可以使用 `a` 作为 `g` 的同义词。

对事件行中的每个单词应用一次以下 `s'` 修饰符。

# Shell 内置命令

除非另有说明，本节中记录为接受以 `-` 开头的选项的每个内置命令都接受 `—` 来表示选项的结束。`true`、`false` 和 `test` 内置不接受选项，也不特殊处理 `—`。`exit`、`logout`、`break`、`continue`、`let` 和 `shift` 内置接受并处理以 `-` 开头的参数，无需 `—`。其他接受参数的内置命令未指定接受选项，它们会将以 `-` 开头的参数解释为无效选项，并需要 `—` 来防止这种解释。

- `:` [arguments]
无影响；除了展开参数和执行任何指定的重定向外，命令什么都不做。返回零退出状态码。

- `.` `filename` [arguments]
- `.` `source` `filename` [arguments]
在当前 shell 环境中从 `filename` 读取并执行命令，并返回从 `filename` 执行的最后一个命令的退出状态。如果 `filename` 不包含斜杠，则使用 `PATH` 中的文件名来查找 `filename` 所在的目录。在 `PATH` 中搜索的文件可能没有执行权限。当 bash 不处于 posix 模式时，如果在 `PATH` 中未找到文件，则搜索当前目录。如果 `shopt` 内置的 `sourcepath` 选项关闭，则不搜索 `PATH`。提供了任何参数，它们在执行 `filename` 时变为位置参数。返回脚本内执行的最后一个命令的状态（如果没有执行任何命令则为 0），以及如果未找到或无法读取 `filename`。

- `alias` [-p] [name=value] ...
无参数或带有 `-p` 选项的 `alias` 以 `alias name=value` 的形式在标准输出上打印别名列表。提供参数时，为每个给定的名称定义别名。值末尾的空格会导致在展开别名时检查下一个单词是否进行别名替换。对于参数列表中未提供值的每个名称，将打印该别名的名称和值。如果给出的名称没有定义别名，则返回别名状态。

- `bg` [jobspec ...]
在后台恢复每个挂起的 `jobspec`，就像它通过 `&` 启动的一样。如果 `jobspec` 不存在，则使用 shell 对当前作业的概念。当禁用作业控制时，`bg jobspec` 返回 0；或者在启用作业控制时，未找到指定的 `jobspec` 或其在没有作业控制的情况下启动，则返回 0。

- `bind` [-m keymap] [-lpsPSVK]
- `bind` [-m keymap] [-q function] [-u function] [-r keyseq]
- `bind` [-m keymap] -f filename
- `bind` [-m keymap] -x keyseq:shell-command
- `bind` [-m keymap] keyseq:function-name
- `bind` readline
显示当前的 `readline` 和函数绑定，将 `bind` 键序列绑定到 `readline` 函数或宏，或设置 `readline` 变量。每个非选项参数都是其在 `.inputrc` 中的形式的命令，但每个绑定或命令必须作为单独参数传递；例如 `"C-x\C-r"`: re-read-init-file。如果提供了选项，则具有以下作用：

- `-n keymap` 使用指定的 `keymap` 作为受后续命令影响的键map。可接受的 `keymap` 名称有 `emacs`, `emacs-standard`, `emacs-meta`, `emacs-ctlx`, `vi`, `vi-move`, `vi-command` 和 `vi-insert`。`vi` 等同于 `vi-command`；`emacs` 等同于 `emacs-standard`。
- `-l` 列出所有 `readline` 函数的名称。
- `-p` 显示并移除 `readline` 函数名称和绑定，以便它们被重新读取。

- `command` [-pV] command [arg ... ]
运行命令，参数替换正常的 shell 函数查找。只执行内置命令或在 `PATH` 中找到的命令。如果给出 `-p` 选项，则使用保证找到所有标准实用程序的默认 `PATH` 值进行命令搜索。如果提供了 `-V` 或 `-v` 选项，则打印命令的描述。`-v` 选项导致显示一个指示调用命令的单词或文件名；`-V` 选项产生更详细的描述。如果提供了 `-V` 或 `-v` 选项，找到则返回状态，未找到返回 1。如果未提供任何选项且发生错误或找不到命令，则退出状态为 127。否则，返回命令的退出状态。

- `compgen` [option] [word]
生成可能的选项匹配项，选项可以是 `complete` 内置命令接受的除 `-p` 和 `-r` 以外的任何选项并将匹配项写入标准输出。

# 受限制的 shell (RESTRICTED SHELL)

如果使用 `rbash` 名称启动 `bash`，或者在调用时提供了 `-r` 选项，shell 将变为受限制。受限制 shell 用于设置比标准 shell 更控制的环境。它的行为与 `bash` 相同，但以下操作是不允许或不会执行的：

- 使用 `cd` 切换目录
- 设置或取消 `SHELL`、`PATH`、`ENV` 或 `BASH_ENV` 的值
- 指定包含 `/` 的命令名
- 向内置命令 `.` 指定包含 `/` 的文件名作为参数
- 向内置命令 `hash` 的 `-p` 选项指定包含斜杠的文件名作为参数
- 启动时从 shell 环境导入函数定义
- 启动时从 shell 环境解析 `SHELLOPTS` 的值
- 使用 `>`、`|`、`&` 和 `>>` 重定向操作重输出
- 使用内置命令 `exec` 将 shell 替换为另一个命令
- 使用内置命令 `enable` 的 `-f` 和 `-d` 选项添加或删除内置命令
- 为内置命令 `command` 指定 `-p` 选项
- 使用 `set +r` 或 `set +o restricted` 退出受限制模式

这些限制在读取任何启动文件后强制执行。

当执行发现是 shell 脚本的命令时（见上述“命令执行”），`rbash` 将关闭执行脚本时派生的 shell 中的任何限制。

# 另请参考

- Bash 参考手册，Brian Fox 和 Chet Ramey
- Gnu Readline 库，Brian Fox 和 Chet Ramey
- Gnu History 库，Brian Fox 和 Chet Ramey
- 可移植操作系统系统接口 (POSIX) 第 2 部分：Shell 和工具，IEEE —
- http://pubs.opengroup.org/onlinepubs/9699919799/
- http://tiswww.case.edu/~chet/bash/POSIX — posix 模式的描述
- `sh(1)`, `ksh(1)`, `csh(1)`
- `emacs(1)`, `vi(1)`
- `readline(3)`

### 文件

- `/bin/bash`: `bash` 可执行文件
- `/etc/profile`: 系统级初始化文件，为登录 shell 执行
- `/etc/bash.bash_logout`: 系统级登录 shell 清理文件，登录 shell 退出时执行
- `~/.bash_profile`: 个人初始化文件，为登录 shell 执行
- `~/.bashrc`: 个人交互式 shell 启动文件
- `~/.bash_logout`: 个人登录 shell 清理文件，登录 shell 退出时执行
- `~/.inputrc`: 个人 *readline* 初始化文件

### 作者

- Brian Fox, 自由软件基金 bfox@gnu.org
- Chet Ramey, 凯斯西储储大学 chet.ramey@case.edu

## bug 报告

如果你在 `bash` 中发现了 bug，应该报告它。但首先，你应该确保它在最新版本的 `bash` 中确实是一个 bug。最新版本始终可以通过 `ftp://ftp.gnu.org/pub/gnu/bash/` 获取。

一旦你确定 bug 确实存在，请使用 `bashbug` 命令（来自源码包）提交 bug 报告。如果你有修复方案，鼓励你也通过邮件发送！建议和“哲学性”bug 报告可以发送至 `bug-bash@gnu.org` 或发布在 Usenet 新闻组 `gnu.bash.bug` 上。

所有 bug 报告都应包含：

- `bash` 的版本号
- 硬件和操作系统
- 用于编译的编译器
- bug 行为描述
- 触发该 bug 的短脚本或 `recipe`

关于本手册页的注释和 bug 报告应指向 `chet.ramey@case.edu`。

## BUGS

它太大且太慢了。

`bash` 与传统的 `sh` 版本之间存在细微差异，主要是因为 POSIX 规范。

别名在某些用法下令人困惑。

shell 内置命令和函数无法停止/重启。

尝试挂起进程时，形式如 `a ; b ; c` 的复合命令和命令序列处理并不优雅。当进程被停止时，shell 会立即执行序列中的下一个命令。只需将命令序列放在括号之间即可强制其进入子 shell，子 shell 可以作为一个单元被停止。

数组变量可能（尚未）导出。

此时可能同时只有一个活跃的协进程。

## 名称

`bashbug` - 报告 `bash` 中的 bug

### 概要

```



`bashbug` [--version] [--help] [email-address]

### 描述

`bashbug` 是一个 shell 脚本，帮助用户以标准格式编写并邮寄关于 bash 的 bug 报告。`bashbug` 在环境变量 `EDITOR` 指定的 bug 报告大纲的临时副本上调用其指定的编辑器。用户必须填写适当字段并退出编辑器。然后，`bashbug` 将完成的报告邮寄到 `bug-bash@gnu.org` 或 `email-address`。如果无法邮寄报告，它将保存在调用用户目录下的 `dead.bashbug` 文件中。

bug 报告格式大纲由几个部分组成。第一部分提供机器、操作系统、bash 版本和编译环境的信息。第二部分应填写 bug 描述。第三部分是重现 bug 的描述。可选的第四部分用于建议的修复。鼓励提供修复。

## 环境

`bashbug` 将利用以下环境：

- `EDITOR`: 指定首选编辑器。如果未设置，`bashbug` 默认使用 `emacs`。
- `HOME`: 存储 bug 报告的目录。
- `TMPDIR`: 创建的目录

### 作者

Brian Fox, 自由软件基金 `bfox@gnu.org`
Chet Ramey, 凯斯西储储大学 `chet.ramey@case.edu`

## 名称

`bc` - 计算器

## 语法

`bc` 是一种允许任意精度的语言。此版本按行输入。所有计算均在进制下进行。

## 数字

四个特殊变量：`scale`、`ibase`、`obase` 和 `last`。`scale` 定义了某些操作如何使用小数点后的数字。`scale` 的默认值为 0。`ibase` 和 `obase` 定义了输入和输出的转换进制。`last`（扩展）是一个具有最后一个数字值的变量。这将在适当的地方详细讨论。所有这些都可以赋值，也可以在表达式中使用。

## 变量

数字存储在两种变量中：简单变量和数组。简单变量和数组都有名称。名称字母字母开头后跟任意数字。所有字母必须小写。

## 注释

`bc` 中的注释以 `/*` 开始，以 `*/` 结束。注释出现在任何地方，并在输入中显示为单个空格。（会导致注释分隔其他项目。）为了支持脚本，增加了单行注释。单行注释从 `#` 字符开始，持续到下一行。行尾字符不是注释的一部分，会被正常处理。

## 表达式

数字通过表达式和语句进行处理。由于该语言设计为交互式，语句和表达式会尽快执行。没有“主”程序。相反，代码在遇到时就会执行。（函数将在稍后详细讨论，并在遇到时定义。）

简单表达式只是常量。`bc` 使用当前的输入进制（由变量 `ibase` 指定）将常量转换为内部数字。（函数中有一个例外）此版本的十进制。例如：

```
.00001 的长度为 6。
```

`1935.000` 的长度为 7，`scale` 为 3。

完全表达式与许多其他高级语言相似。由于只有一种数字类型，因此没有混合规则的规则。相反，存在关于表达式标度（`scale`）的规则。每个表达式都有一个标度。它源于原始数字的标度、所执行的操作以及在许多情况下，变量标度的值。变量标度的合法取值范围为 0 到 C 整数能表示的最大数字。

在以下对合法表达式的描述中，“`expr`”指一个完整的表达式，“`var`”指简单变量或数组变量。简单变量只是一个名称，而数组变量指定为

`name[expr]`

除非特别说明，否则结果的标度是涉及的表达式的最大标度。

- `+- expr`

  结果是表达式的取反。
- `++ var`

  变量加 1，新值为表达式的结果。
- `- var`

  变量减 1，新值为表达式的结果。
- `var ++`

  表达式的结果为变量的值，然后变量加 1。
- `var -`

  表达式的结果为变量的值，然后变量减 1。
- `expr + expr`

  表达式的结果为两个表达式之和。
- `expr - expr`

  表达式的结果为两个表达式之差。
- `expr * expr`

  表达式的结果为两个表达式之积。如果 `a` 和 `b` 是两个表达式的标度，那么结果的标度为：`min(a+b,max(scale,a))`
- `expr / expr`

  表达式的结果为两个表达式的商。结果的标度为变量标度的值。
- `expr % expr`

  表达式的结果为“余数”，按以下方式计算。计算 `%b` 时，首先计算到标度数字的 `a/b`。该结果用于计算 `a-(a/b)*b`，其标度为最大标度+`scale(b)` 和 `scale(a)`。如果 `scale` 为 0 且两个表达式均为整数，则为整数取模函数。
- `expr ^ expr`

  表达式的结果为第一个表达式升到第二个表达式的幂。第二个表达式必须是整数。（如果第二个表达式不是整数，则会产生警告并将表达式截断以获得整数值。）如果指数为负，结果的标度为 `scale`。如果指数为正，结果的标度是第一个表达式标度乘以指数值与 `scale` 和第一个表达式标度的最大值之间的最小值（例如 `scale(a^b) = min(scale(a)*b, max(scale, scale(a)))`）。需要注意的是，`expr^0` 将始终返回值 1。
- `( expr )`

  这改变了标准优先级以强制评估表达式。
- `var = expr`

  将表达式的值赋予变量。
- `var <> = expr`

  这等同于“`var = var <> expr`”，例外是“`var`”部分只求值一次。如果“`var`”是数组，这可能会产生差异。

关系表达式是一种特殊的表达式，如果关系为假，结果始终为 0；如果关系为真，结果为 1。这些可以出现在任何合法表达式中。（POSIX `bc` 要求关系表达式只能用于 `if`、`while` 和 `for` 语句，且语句中只能进行一次关系测试。）关系运算符有：

- `expr1 < expr2`

  如果 `expr1` 严格小于 `expr2`，结果为 1。
- `expr1 <= expr2`

  如果 `expr1` 小于或等于 `expr2`，结果为 1。
- `expr1 > expr2`

  如果 `expr1` 严格大于 `expr2`，结果为 1。
- `expr1 >= expr2`

  如果 `expr1` 大于或等于 `expr2`，结果为 1。
- `expr1 == expr2`

  如果 `expr1` 等于 `expr2`，结果为 1。
- `expr1 != expr2`

  如果 `expr1` 不等于 `expr2`，结果为 1。

布尔操作也是合法的。（POSIX `bc` 没有布尔操作）。所有布尔操作的结果均为 0 和 1（分别代表假和真），与关系表达式相同。布尔运算符有：

- `!expr`

  如果 `expr` 为 0，结果为 1。
- `expr && expr`

  如果两个表达式都非零，结果为 1。
- `expr || expr`

  如果表达式非零，结果为 1。

表达式的优先级如下（从低到高）：

```
|| 运算符，左结合性 | && 运算符，左结合性 | |
非结合性 | 关系运算符，左结合性 | 赋值
运算符，右结合性 | + 和 - 运算符，左结合性 | *, /
以及和 % 运算符，左结合性 | ^ 运算符，右结合性 | 一元
运算符，非结合性 | ++ 和 - 运算符，非结合性
```

选择这种优先级是为了确保 POSIX `bc` 程序能够正确运行。这实际上会导致在与赋值表达式配合关系和逻辑运算符时产生某些异常行为。考虑以下表达式：

```
a = 3 < 5
```

大多数 C 程序员会假设这会将 "3 < 5" 的结果（值 1）赋值给变量 "a"。但在 `bc` 中这是将值 3 赋值给变量 "a"，然后将 3 与 5 进行比较。在使用赋值运算符配合关系和逻辑运算符时，最好使用括号。

`bc` 中提供了一些特殊的表达式。这些与用户定义函数有关。这些与标准函数有关。以下是：

- `length ( expression )`

  `length` 的值是小数点后的数字位数。
- `scale ( expression )`

  `scale` 的值是小数点前的数字位数。
- `sqrt ( expression )`

  `sqrt` 的值是表达式的平方根。

# 语句

语句（在大多数语言中）提供了……（在大多数语言中）提供了……（在大多数语言中）提供了。

表达式

该语句执行两件事之一。如果表达式以 `=` 开头，则被视为赋值语句。如果表达式不是赋值语句，则求值表达式并输出到输出中。输出后一个换行。表达式被求值并赋值给变量 `last`。语句中的字符串输出到输出中，并可能包含特殊字符。所有数字都根据 `obase` 指定的基数输出。`abase` 的合法取值范围为 2 到 `BC_BASE_MAX`。（见 `LIMITS` 部分）。对于 2 到 16 的基数，使用通常的数字方法。对于大于 16 的基数，`bc` 使用多字符数字方法打印数字，每个数字作为一个十进制数字。数字之间用空格分隔。由于任意精度，某些数字可能无法在单行输出中打印。这些长数字将使用作为行的最后一个字符进行跨行显示。由于 `bc` 的交互性质，打印数字会产生将值赋值给特殊变量 `last` 的副作用。这允许用户无需重试打印数字的表达式即可恢复最后的值。赋值 `last` 是合法的，并将赋值值覆盖最后打印的值。新赋值的值将保留，直到打印下一个数字或向另一个值赋值 `last`。（某些安装版本允许使用单个句号 `(.)`，它不是表达式的一部分）

`string`



字符串输出到输出中。以双引号开始并包含到下一个双引号之前的所有字符。所有字符均字面取出，包括任何换行符。字符串后不打印换行符。

`print list`

`print`语句（扩展）提供了另一种输出方法。`list`是一个由逗号分隔的字符串和表达式的列表。每个字符串或表达式按照列表顺序打印。不打印终止换行符。表达式被求值，其值被打印并赋值给变量`last`。`print`语句中的字符串输出到输出中，并可能包含特殊字符。

以反斜杠字符（`\`）开头字符。`bc`识别的特殊字符有`"a"`（警报或铃声）、`"b"`（退格）、`"f"`（分页）、`"n"`（换行）、`"r"`（回车）、`"q"`（双引号）、`"t"`（制表符）和`"\"`（反斜杠）。反斜杠后的任何其他字符都将被忽略。

`statement_list`

这是复合语句。它允许将多个语句分组在一起执行。

`if ( expression ) statement1 [else statement2]`

`if`语句根据表达式的值评估表达式并执行`statement1`。如果表达式为非零，则执行`statement1`。如果存在`statement2`且表达式的值为0，则执行`statement2`。（`else`子句是一个扩展。）

`while ( expression ) statement`

`while`语句会在表达式为非零时持续执行`statement`。它在每次执行`statement`之前都会评估表达式。循环的终止是由表达式值为0或执行`break`语句导致的。

`for [expression1] ; [expression2] ; [expression3] ) statement`

`for`语句控制`statement`的重复执行。`expression1`在循环开始前被求值。`expression2`在每次执行`statement`之前被求值。如果非零，则执行`statement`。如果为0，则终止循环。在每次执行`statement`后，在重新求值`expression2`之前评估`expression3`。如果`expression1`或`expression3`缺失，则在相应的求值点不进行任何评估。如果`expression2`缺失，等同于将`expression2`替换为值1。（可选表达式是扩展。POSIX `bc`要求所有三个表达式）。该语句的等效代码如下

```
expression1; while (expression2) { statement; expression3; }
```

`break`此语句强制退出最近的包含它的`while`语句或语句。`continue`语句（一种扩展）导致最近的包含它的`for`语句开始下一次迭代。`halt`语句（一种扩展）是一个可执行语句，只有在执行执行时才会导致`bc`处理器退出。例如，`if (0 == 1) halt`不会导致`bc`终止，因为`halt`未被执行。

`return`从函数返回值0。`return ( expression )`从函数返回表达式的值。（参见函数章节。）作为一种扩展，括号不是必须的。

# 伪语句 (PSEUDO STATEMENTS)

这些语句在传统意义上并不是语句。它们不是可执行的语句。它们的功能在“编译”时完成。

`limits`

打印本地`bc`版本强制执行的本地限制。这是一种扩展。

`quit`

当读取到`quit`语句时，`bc`处理器终止，无论`quit`语句位于何处。例如，`if (0 == 1) quit`会导致`bc`终止。

打印保修说明。这是一种扩展。

# 函数 (FUNCTIONS)

函数提供了一种定义稍后执行的计算的方法。

`bc`中的函数始终计算一个值并将其返回给调用者。函数定义在意义上是“动态”的，因为在输入中遇到定义之前，函数是未定义的。该定义会被一直使用，直到遇到同名的另一个函数定义。新定义将替换旧定义。函数的定义如下：

```
define name ( parameters ) { newline auto_list statement_list }
```

函数调用只是形式为`name(parameters)`的表达式。

参数是数字或数组（扩展）。在函数定义中，通过逗号分隔的列表来定义零或多个参数。所有参数都通过值传递。数组在参数定义中通过符号`name[]`进行指定。在函数调用中，实际参数是数字的完整表达式。传递数组与定义数组参数使用相同的符号。命名数组按值传递给函数。由于函数定义是动态的，在调用函数时会检查参数名称和类型。参数数量或类型上的任何不匹配都会导致运行时错误。调用未定义的函数也会发生运行时错误。

`auto_list`是可选的变量列表，这些变量是“局部的”。`auto`列表的语法（如果存在）为`auto_name, ...;`（分号是可选的）。每个名称都是自动变量的名称。可以使用与参数中相同的符号来指定数组。这些变量的值被初始化为0，并在函数的整个执行过程中被使用。在退出时，这些变量会被弹出，从而恢复原始值（调用该刻的值）。参数实际上是自动变量，它们的值被初始化为函数调用中提供的值。自动变量与传统的局部变量不同，因为如果函数A调用B，B可以使用相同的名称访问A的自动变量，除非函数B已将它们推入堆栈。由于自动变量和参数被推入堆栈中，`bc`支持递归函数。

函数体是`bc`语句的列表。同样，语句之间用分号或换行符分隔。`return`语句导致函数的终止并返回值。`return`语句有两种形式。第一形式`return`向调用表达式返回值0。第二种形式`return ( expression )`计算表达式的值并将该值返回给调用表达式。每个函数的末尾都有一个隐含的`return (0)`。这允许函数在没有显式`return`语句的情况下终止并返回0。

函数还会改变变量`ibase`的用法。函数体中的所有常量都将使用函数调用时`ibase`的值进行转换。在函数执行期间，`ibase`的更改将被忽略，但标准函数`read`除外，`read`始终将使用`ibase`的当前值进行数字转换。

函数方面还增加了一些扩展。首先，定义的格式略有放宽。标准要求大括号与`define`关键字在同一行，而其他部分位于随后的行。此版本的`bc`允许在函数大括号前后任意数量的换行符。例如，以下定义是合法的：

```
define d (n) { return (2*n); } define d (n) { return (2*n); };
```

通过`void`定义。`void`函数不返回值，因此不能在任何需要值的地方单独使用。在输入行上调用`void`函数不会产生任何输出。`void`关键字放在`define`和函数名之间。例如，考虑以下方案：

```
define py (y) { print "-",", y, "-", "; define void px (x) { print "-",", x, "-", "; } py(1)--21<-- 0 px(1) --->1<--
```

由于`py`不是`void`函数，调用`py(1)`会打印所需的输出，然后打印函数的值。没有给出显式`return`语句的函数值为0。对于`px(1)`，不会打印0，因为它是`void`函数。

此外，增加了数组的按值传递。要声明按值传递数组，函数定义中的数组参数看起来像`*name[]`。对函数的调用与按值传递数组相同。

# 数学库 (MATH LIBRARY)

如果使用`-l`选项启动`bc`，将预加载数学库并将默认`scale`设置为20。数学函数将根据调用时设置的`scale`来计算其结果。数学库定义了以下函数：

- `s (x)`

  `x`的正弦，`x`为弧度。

- `c (x)`

  `x`的余弦，`x`为弧度。

- `a (x)`

  `x`的反正切，反正切返回弧度。

- `l (x)`

  `x`的自然对数。

# 以 e 为值为底的指数函数。

`(n,x)`

`x`的整数阶数`n`贝塞尔函数。

## 示例

在`/bin/sh`中，以下命令将"`pi`"的值赋值给shell变量`pi`。

```sh
pi=$(echo "scale=10; 4*a(1)" | bc)
```

以下是数学库中指数函数的定义。该函数用POSIX `bc`编写。

```bc
scale = 20 /* Use the fact that e^x = (e^(x/2))^2 when x is small
enough, we use the series: e^x = 1 + x + x^2/2! + x^3/3! + ... */
define(e(x) { if (f > 0) { f += 1; x /= 2; } /* Initialize the variables.
if (x < 0) { m = 1; x = -x; } /* Precondition. */ scale /= z; scale = 4 + z +
44*x; while (x > 1) { f = a = x = d = 1 for (i=2; i++); } { e = (a *= x) / (d *= i) if (e == 0) { if (f < 0) { v = -v; } scale = z if (m) return (1/v);
return (v/j); v += e }
```



以下代码使用 `bc` 的偏移功能实现了一个计算支票的程序。该程序最好保存在文件中，这样就可以多次使用而无需每次重新输入。

```bc
scale=2 print "\ncheck program!\n" print "Remember, deposits are
negative transactions.\n" print "Exit by a 0 transaction.\n\n" print
"Initial balance"; bal = read(1) bal /= 1 print "\n" while (1) {
"current balance = "; bal = "transaction"; trans = read(1) if (trans ==
0) break; bal -= trans bal /= 1 quit
```

以下是递归阶乘函数的定义。

```bc
def f (x) { if (x <= 1) return (1); return (f(x-1) * x); }
```

## READLINE 与编辑选项

GNU `bc` 可以编译（通过配置选项）以使用 GNU `readline` 编辑器库或 BSD 库。这允许用户在将行发送到 `bc` 之前对其进行编辑。它还允许保留之前输入行的历史。当选择此选项时，`bc` 有一个特殊变量。这个特殊变量 `history` 是保留的历史行数。对于 `readline`，值 `-1` 表示保留无限数量的历史行。将 `history` 的值设置为正数会将历史行数限制为给定的数量。设置为值为 `0` 则禁用历史功能。默认值为 `100`。有关更多信息，请参阅 GNU `deadline`、`history` 和 BSD `libedit` 库的用户手册。不能同时启用 `readline` 和 `libedit`。

## 差异

此版本的 `bc` 是根据 POSIX P1003.2/D11 草稿实现的，相对于草稿和传统实现，包含若干差异和扩展。它不是使用传统的 `dc(1)` 方式实现的。此版本是一个单进程，负责解析并运行程序的字节码翻译。有一个“未文档的选项 (-c)”，它会导致程序将字节码输出到标准输出而不是运行它。它主要用于调试解析器和准备数学库。

差异的主要来源是扩展（extensions），即对功能进行扩展以添加更多功能；以及新增（additions），即添加新功能。以下是差异和扩展的列表。

## LANG 环境

此版本在处理 `LANG` 环境变量以及所有以 `LC_` 开头的环境变量时不符合 POSIX 标准。

- `names`: 传统的 POSIX `bc` 对函数、变量和数组使用字母命名。它们现在被扩展为多字符名称，以字母开头并可以包含字母、数字和下划线字符。

- `Strings`: 字符串不允许包含 NUL 字符。POSIX 规定所有字符都必须包含在字符串中。

- `last`: POSIX `bc` 没有 `last` 变量。某些 `bc` 的实现以类似的方式使用 `.(.)`。

- `comparisons`: POSIX `bc` 仅在 `if` 语句、`while` 语句和语句的第二个表达式中允许比较。此外，在这些语句中，每个只允许一个关系操作。

- `if` 语句，`else` 子句: POSIX `bc` 没有 `else` 子句。

- `for` 语句: POSIX `bc` 要求 `for` 语句中必须存在所有表达式 `&&`、`||`、`!`

- `read` 函数: POSIX `bc` 没有逻辑运算符。

- `print` 语句: POSIX `bc` 没有 `read` 函数。POSIX `bc` 没有 `print` 语句。

- `continue` 语句: POSIX `bc` 没有 `continue` 语句。

- `return` 语句: POSIX `bc` 要求在表达式周围有括号。

- `array parameters`: POSIX `bc`（目前）未完全支持数组参数。POSIX 语法允许在函数定义中使用数组，但没有提供一种将数组指定为实际参数的方法（这很可能是语法中的疏忽）。传统的 `bc` 实现仅通过值传递调用数组参数。

- `function format`: POSIX `bc` 要求左大括号与关键字在同一行，`auto` 语句在下一行。

- `=`, `-=`, `*=`, `/=`, `%,^`: POSIX `bc` 不要求定义这些“旧式”赋值运算符。此版本可能允许这些“旧式”赋值。

# 诊断

如果命令行上的任何文件无法打开，`bc` 将报告该文件不可用并终止。此外，还有编译和运行诊断信息，其含义通常是不言自明的。

## 缺陷

目前的错误恢复机制尚不完善。

请将错误报告发送至 `bug-bc@gnu.org`。请确保在“主题（Subject:）”字段某处包含“`bc`”字样。

### 作者

Philip A. Nelson `philnelson@acm.org`

# 感谢

作者感谢 Steve Sommars (`Steve.Sommars@att.com`) 在测试实现方面提供的巨大帮助。他给出了许多棒的建议。由于他的参与，这个产品变得好得多。

`bccmd` - 用于 CSR BCCMD 接口的实用程序

### 概要

```
bccmd bccmd [-t <transport>] [-d <device>] <command> [<args>] bccmd [-h--help]
```

### 描述

`bccmd` 向 Cambridge Silicon Radio 设备发送 BlueCore 命令。如果在未提供 `<command>` 参数的情况下运行，将显示简短的帮助页面。

### 选项

`-t <transport>`

指定通信传输层。有效的选项有：

- `HCI`

带有主机控制器接口（Host Controller Interface）的本地设备（默认）。

- `USB`

直接 USB 连接。

- `BCSP`

蓝牙核心串口协议（Blue Core Serial Protocol）。

- `H4`

H4 串口协议。

- `3WIRE`

3WIRE 协议（未实现）。

# -D <DEV>

指定要操作的特定设备。如果没有指定，默认为第一个可用的 HCI 设备，或串口传输的 `/dev/ttyS0`。

### 命令

`builddef`

获取构建定义

`keylen <handle>`

获取当前加密密钥长度

`clock`

获取本地蓝牙时钟

`rand`

获取随机数

`chiprev`

获取芯片版本号

`buildname`

获取完整构建名称

`panicarg`

获取崩溃代码参数

`faultarg`

获取故障代码参数

`coldreset`

执行冷启动

`warmreset`

执行热启动

`disablex`

禁用设备上的 TX（发送）

`enablex`

启用设备上的 TX（发送）

`singlechan <channel>`

在特定通道上锁定无线电

`hopping`

恢复通道跳频模式

`rttdata1 <decimal freq MHz> <level>`

TXDadio 无电测试

`radiotest <decimal freq MHz> <level> <id>`

运行无线电测试，4, 6 和 7 是发送测试

`memtypes`

获取内存类型

`psget [-r] [-s <stores>] <key>`

获取 PS 键值。`-r` 在之后发送一次热启动。

`psset [-r] [-s <stores>] <key> <value>`

设置 PS 键值。`-r` 在之后发送一次热启动。

`psclr [-r] [-s <stores>] <key>`

清除 PS 键值。`-r` 在之后发送一次热启动。

`plist [-r] [-s <stores>]`

列出所有 PS 键。`-r` 在之后发送一次热启动。

```
psread [-r] [-s <stores>]
```

读取所有 PS 键。`-r` 在之后发送一次热启动。

```
psload [-r] [-s <stores>] <file>
```

从 PSR 文件加载所有 PS 键。`-r` 在之后发送一次热启动。

```
pscheck [-r] [-s <stores>] <file>
```

检查 PSR 文件的语法。`-r` 在之后发送一次热启动。

# 键

`bdaddr` `country` `devclass` `keymin` `keymax` `features` `commands` `version` `remver` `hciextn` `mapsco` `baudrate` `hostintf` `anafreq` `anaftrim` `usbvid` `usbpid` `dfupid` `bootmode`

### 作者

Marcel Holtmann `<marcel@holtmann.org>` 编写，帮助页由 Adam Laurie `<adam@algroup.co.uk>` 编写

## 名称

`bdftopcf` f - 将 X 字体从位图分布格式（BDF）转换为可移植编译格式（PCF）

### 概要

`bdftopcf [ -pn ] [ -un ] [ -m ] [ -l ] [ -M ] [ -L ] [ -t ] [ -i ] [ -outputfile ] fontfile.bdf`



### 描述

`Bdftopcf` 是用于 X 服务器和字体服务器的字体编译器。任何架构都可以读取可移植编译格式的字体，尽管文件结构允许特定架构无需重新格式读取。这允许在相应的机器上进行快速读取，但在其他机器上文件仍然具有移植性（尽管读取速度较慢）。

### 选项

`-pn`

设置字体字符填充。字体中的每个字符的扫描行将填充为 n 字节的倍数，其中 n 为 1, 2，4 或 8。

`-u`

设置字体扫描行单位。当字体顺序与字体顺序不同时，扫描行单位描述了要交换的数据单元（字节）；单位 i 可以是 1, 2 或 4 字节。

`-m`

将字体顺序设置为最高有效位（MSB）优先。每个字符的位将按此顺序排列；即屏幕上最左边的位将是每个单元中的最高位。

`-l`

将字体顺序设置为最低位（LSB）优先。

`-M`

将字体顺序设置为最高有效位（MSB）优先。

`-L`

将字体顺序设置为最低位（LSB）优先。

`-t`

将字体顺序设置为最低位（LSB）优先。

`-i`

将字体顺序设置为最高有效位（MSB）优先。

`-outputfile`

设置输出文件的名称。

`-v`

打印版本信息并退出。

### 作者

Keith Packard, MIT 联盟

# 另参

`X(7)`

# bdftuncate

从 BDF 生成截断的 BDF

### 概要

```
bdftuncate threshold source.bdf > destination.bdf
```

### 描述

`bdftuncate` 允许生成一个对于阈值以上的字符未编码的 BDF 字体。这通常是必要的，因为 Xlib API 和 X11 协议结构在处理稀疏字体时效率极低。

## 示例

命令

```
bdftuncate 0x3200 < 6x13t.bdf > 6x13t.bdf
```

将生成 6x13t.bdf，其中字符未编码。

# 另参

`ucs2any(1)`

### 作者

`bdftuncate` 由 Markus Kuhn 编写。Brandon Robinson 为 Debian 项目编写了此手册页。

## 名称

`bond2team` – 将绑定配置（bonding configuration）转换为团队（team）

### 概要

```
bond2team [options]
```

### 描述

`bond2team` 是一个用于将绑定选项转换为 team 尝试的工具，尽可能保留原始功能。

生成的文件默认使用 ifcfg 样式并保存在临时目录中。在转换 ifcfg 文件时，它会将绑定选项转换为 team 选项，并保留所有其他选项。在这种情况下，它会将相应的从机（slave）ifcfg 文件转换为 team 端口，同样保留它们的所有其他选项。如果从命令行给定的绑定选项进行转换，工具可以使用指定的端口作为 team 端口。

### 选项

- `--master <interface>`

指定要转换的接口名称或 ifcfg 文件。如果指定了接口名称，工具将在 `/etc/sysconfig/network-scripts/` 中查找对应的 ifcfg 文件。

- `--rename <interface>`

这是一个方便的选项，用于将原始接口名称替换为指定的名称。例如，如果 `--rename` 指定了 `bond0`，则可以使用 `--rename team0` 将最终接口名称更改为 `team0`。

- `--ifcfg`

将输出格式设置为 ifcfg 配置样式。[默认]

- `--json`

将输出格式设置为 JSON 样式。更多细节请参见 `teamd.conf(5)`。

指定要转换的绑定选项，而不是从 ifcfg 文件中读取。

- `--port <interface>`

将指定的接口设置为 team 端口。

- `--configdir <directory>`

将 ifcfg 配置路径从 `/etc/sysconfig/network-scripts` 为指定的 `<directory>`。

- `--stdout <directory>`

将输出目录设置为 `<directory>`。

- `--stdout`

将结果打印到屏幕而不是写入文件。

- `--debug`

增加调试级别。

- `--quiet`

禁止向控制台打印任何消息。

- `--version`

将工具版本信息打印到控制台并退出。

- `--help`

将帮助文本打印到控制台并退出。

- `--examples`

将常用示例打印到控制台并退出。

## 示例

将当前的 'bond0' ifcfg 配置转换为 team ifcfg：

```
# bond2team --master bond0
```

将当前的 'bond0' ifcfg 配置转换为 team ifcfg，并将接口名称重命名为 'team0'。**注意：** 可能绑定到原始接口名称的防火墙规则、别名接口等在重命名后可能会损坏，因为工具只会更改 ifcfg 文件，不会更改其他内容。

```
# bond2team --master bond0 --rename team0
```

在没有 ifcfg 的情况下转换带有端口的给定绑定参数：

```
# bond2team --bonding_opts 'mode=1 miimon=500 primary=eth1 primary_reselect=0' --port eth1 --port eth2 --port eth3 --port eth4
```

更多示例请参见选项 `--examples`。

## 注意事项

该工具不会转换任何可能绑定到当前设置的配置。例如，防火墙规则、别名接口、桥接等。

### 作者

Flavio Leitner 是该工具的原始作者。Jiri Pirko 是 libteam 的原始作者和当前维护者。

### 参见

`teamd(8)`, `teamdctl(8)`, `teamd.conf(5)`, `teamnl(8)`

## BOOTCTL

## 名称

`bootctl` - 控制固件和启动管理程序设置

### 概要

```
bootctl [OPTIONS... ]status
bootctl [OPTIONS...]update
bootctl [OPTIONS...]install
bootctl [OPTIONS...]remove
```

### 描述

`bootctl`

检查、更新、安装或删除当前系统中的引导程序。

`bootctl status` 检查并打印当前安装的引导程序二进制文件以及所有当前的 EFI 启动变量。

`bootctl update` 更新所有已安装的 systemd-boot 版本，如果版本比 EFI 系统分区中安装的版本新。这包括 `/EFI/Boot\*.efi` 中的 EFI 默认/备用 loader。如果 EFI 启动变量中没有条目，则创建一个 systemd-boot 条目。创建的条目将被添加到启动列表的末尾。

`bootctl install` 将 systemd-boot 安装到 EFI 系统分区。systemd-boot 的副本将作为 EFI 默认/备用 存储在 `/EFI/Boot\*.efi`。在 EFI 启动变量中创建一个 systemd-boot 条目并将其添加到启动列表的最顶部。

`bootctl remove` 从 EFI 系统分区中删除所有已安装的 systemd-boot 版本并从 EFI 启动变量中删除 systemd-boot。

如果没有传递命令，则隐含为 status。

### 选项

支持以下选项：

- `-h`, `--help`

打印简短的帮助文本并退出。

- `--version`

打印简短的版本字符串并退出。

- `--path`

指向 EFI 系统分区的路径。默认是 `/boot`。

- `--no-variables`

不要碰 EFI 启动变量。

## 退出状态

成功时返回 0，否则返回非零失败代码。

### 参见

引导程序规范

Systemd 引导程序接口

## 备注

1. 引导程序规范

`http://www.freedesktop.org/wiki/BootSpec`

2. Systemd 引导程序接口

`http://www.freedesktop.org/wiki/Software/Loader`

## 名称

`brtty` - Linux (Unix-like) 可刷新盲文显示器

### 概要

```
brtty [options]
```

### 描述

`brtty` 是一个后台进程（守护进程），为文本转盲文提供盲文显示器访问。它还为文本转语音提供驱动程序。

### 选项

选项可以通过以下数字方式传递给 `brtty`。从高到低为：

1. 命令行

2. 参数

3. 环境变量

4. 配置文件

5. 默认值

## 命令行

选项按顺序处理。如果指定了多次，则最后一次具有优先级。支持以下选项：

- `-a`, `--attributes=`

指向属性表的路径。相对路径相对于 `/etc/brtty`。atb 扩展为可选。

- `-b`, `--driver=`

驱动程序。默认为 auto。

- `-c`, `--contraction=`

指向收缩表的路径。相对路径相对于 `/etc/brtty`。ktb 扩展为可选。

- `-d`, `--device=`

目标设备。默认为 auto。



## 选项

`-e`, `--standard-error`

将日志写入标准错误而不是系统日志（用于调试）。

`-f`, `--configuration-file=`

指向配置文件的路径。相对路径相对于工作目录。默认为 `/etc/brtty.conf`。

`-h`, `--help`

打印命令行摘要（常用选项）并退出。

`-n`, `--speech-input=`

文件对象（FIFO、命名管道、命名套接字），允许应用程序访问 `brtty` 的文本转语音驱动程序。它在启动时创建，在终止时移除。相对路径相对于 `/etc/brtty`。默认不创建文件对象。

`-k`, `--keyboard-table=`

指向键盘表的路径。`ktb` 扩展为可选。

`-l`, `--log-level=`

写入日志的最小严重级别。可以指定以下数字或其对应名称的缩写：

`0` `alert`

`2` `critical`

`3` `error`

`4` `warning`

`5` `notice`

`6` `information`

`7` `debug`

`-v`, `--version`

打印版本信息并退出。

`-w`, `--address=`

对于蓝牙设备，指定地址。地址必须是冒号分隔的十六进制数字，例如 `01:23:45:67:89`。

## 蓝牙

对于蓝牙设备，指定地址。地址必须是冒号分隔的十六进制数字，例如 `01:23:45:67:89`。

## 串口

对于串口设备（Unix 类系统中定义设备的位置）。以下设备规范指向主串口：`serial:/dev/ttyS0`, `ttyS0`。

## USB

对于 USB 设备，指定 `brtty` 将搜索匹配驱动程序的第一个 USB 设备。如果多个 USB 设备需要相同的驱动程序，则可以通过附加显示器的序列号来精确定位，例如 `usb:12345`。注意：“通过序列号识别”功能对某些模型不起作用，因为某些制造商未设置 USB 序列号描述符，或将其设置为唯一值。

可以指定逗号分隔的盲文设备列表。如果是这样，将按顺序对列表中的每个设备执行自动检测。这对于具有多个接口的盲文显示器（例如同时具有串口和 USB 端口）特别有用。

默认值为 `notice`。

`-m device` (`--midi-device=`) 用于 MIDI（乐器数字接口）的设备。对于 ALSA，它的的格式为 `client:port`，其中每个可以是数字或区分大小写的名称子字符串。对于其他接口，它是指向适当系统设备的完整路径。内置默认值为：

- Linux/ALSA: 第一个可用 MIDI 输出端口
- Linux/OSS: `/dev/sequencer`

`-n` (`--no-daemon`) 保持在控制台运行（用于调试）。

`-p device` (`--pcm-device=`) 用于数字音频的设备。对于 ALSA，格式为 `name[:argument,...]`。对于其他接口，它是指向适当系统设备的完整路径。内置默认值为：

- FreeBSD: `/dev/dsp`
- Linux/ALSA: `hw:0,0`
- Linux/OSS: `/dev/dsp`
- NetBSD: `/dev/audio`
- OpenBSD: `/dev/audio`
- Qnx: 优选 PCM 输出设备
- Solaris: `/dev/audio`

`-q` (`--quiet`) 抑制启动消息。这是通过将默认日志级别降低来实现，参见 `-l` (`--log-level=`) 选项设置为 `warning`（如果也指定了 `-v` (`--verify`) 或 `-V` (version)，则显示为 `information`）。

`-r` (`--release-device`) 当当前屏幕或窗口无法被读取时，释放盲点显示器连接的设备。

`-s driver,...auto` (`--speech-driver=`) 语音合成器的驱动程序（参见表格=`）。指向规范的路径。相对路径以 `/etc/brtty` 为锚点。`.tb` 扩展名是可选的。内置设备是 `ennabc.tb`（北美盲点计算机代码）。

`-v` (`--verify`) 打印启动消息并退出。这始终包含 `brtty` 的版本、其应用程序接口的服务端，以及每个选定的盲点驱动程序和语音驱动程序。如果没有同时指定 `-q` (`--quiet`) 选项，则将包含找到所有源后各个选项的值。如果指定了多个盲点驱动程序和或多个盲点设备，则将执行盲点显示自动检测。如果指定了多个语音驱动程序，则将执行语音合成器自动检测。

`-x driver` (`--screen-driver=`) 屏幕驱动程序。内置默认值为相应的操作系统合适的。

`-A name=value,...` (`--parameters=`) 应用程序接口的参数。如果多次指定同一个参数，则使用最右侧的规范。参数名称可以缩写。

`-B [driver]:name=value,...` (`--braille-parameters=`) 盲点显示器驱动程序的参数。如果多次指定同一个参数，则使用最右侧的规范。参数名称可以缩写。如果参数赋值带有驱动程序识别码，则仅在使用该盲点显示驱动程序时才会被处理。

`-D directory` (`--drivers-directory=`) 包含动态加载驱动对象的目录路径。内置默认值为 `/usr/lib/brtty`。

`-E` (environment-variables) 识别环境变量。

`-F file` (`--preferences-file=`) 内置默认值为 `brbrty`。相对路径以 `/var/lib/brtty` 为锚点。

`-H` (`--full-help`) 打印命令行用法摘要（所有选项），然后退出。

`-I` (install-server) (仅限 Windows) 将 `brbrty` 安装为 BRLAPI 服务，使其在系统启动时自动启动，并且应用程序可以获知 BRLAPI 服务器正在运行。

`-K arg` (`--keyboard-properties=`) 键盘的属性。

`-L file` (`--log-file=`) 归档日志消息的文件。相对路径以工作目录为锚点。默认将日志消息发送到系统。

`-M mcs` (`--message-delay=`) 消息保持时间，单位为百分之一秒。内置默认值为 `400`（秒秒）。

`-N` (no-api) 不启动应用程序接口。

`-P file` (`--pid-file=`) 进程标识符的路径。如果提供了此选项，`brbrty` 会在启动时将其进程标识符 (`pid`) 写入指定的文件。在使用 `brbrty` 时会删除该文件。

`-R` (`--remove-service`) (仅限 Windows) 移除 BRLAPI 服务，以便 `brbrty` 不会在系统启动时自动启动，并且应用程序知道 BRLAPI 服务器正在运行。

`-S [driver:name=value,...` (`--parameters=`) 语音合成器的参数。如果多次指定同一个参数，则使用最右侧的规范。参数名称可以缩写。如果参数赋值带有驱动程序识别码，则仅在使用该合成器时才会被处理。

`-T directory` (`--tables-directory=`) 包含属性、键盘和输入的目录路径。内置默认值为 `/etc/brtty`。

`-V` (version) 打印 `brtty` 本身、所有应用程序接口的服务端以及在构建时配置的驱动程序的版本，然后退出。如果没有同时指定 `-q` (`--quiet`) 选项，则打印信息。

`-W directory` (`--writable-directory=`) 可写入的目录路径。内置默认值为 `/var/run/brtty`。

`-X name=value,...` (`--screen-parameters=`) 屏幕驱动程序的参数。如果多次指定该参数，则使用最右侧的规范。

## 环境变量

以下环境变量由 `-E` (environment-variables) 识别：

`brtty_API_PARAMETERS=name=value,...` 应用程序接口的参数。

`brtty_ATTRIBUTES_TABLE=table` 属性表。

`brtty_BRAILLE_DEVICE=device` 盲点显示器设备。

`brtty_BRAILLE_DRIVER=driver,...auto` 盲点驱动程序。

`brtty_BRAILLE_PARAMETERS=[driver:]name=value,...` 盲点显示器驱动程序的参数。

`brtty_CONFIGURATION_FILE=file` 配置文件。

`brtty_CONTRACTION_TABLE=table` 缩写表。

`brtty_MIDI_DEVICE=device` MIDI（乐器数字接口）设备。

`brtty_PCM_DEVICE=device` 数字音频设备。

`brtty_PREFERENCES_FILE=file` 偏好文件。

`brtty_RELEASE_DEVICE=onoff` 当当前屏幕或窗口无法被读取时的盲点显示器设备。

`brtty_SCREEN_DRIVER=driver` 屏幕驱动程序。

`brtty_SCREEN_PARAMETERS=name=value,...` 屏幕驱动程序的参数。



`brtty_SPEECH_DRIVER=driver,...auto` 语音驱动程序。

`brtty_SPEECH_INPUT=name` 语音输入对象。

`brtty_TEXT_TABLE=table` 文本表。

# 配置文件

空行将被忽略。如果某行出现 `#` 字符，该字符之后到行尾的所有字符都被视为注释。

支持以下配置指令：

- `api-parameters` `name=value,...` 应用程序接口的参数。
- `attributes-table` `table` 属性表。
- `braille-device` `device,...` 盲点显示器设备。
- `braille-driver` `driver,...auto` 盲点驱动程序。
- `braille-parameters` `[driver:]name=value,...` 盲点显示器驱动程序的参数。
- `contraction-table` `table` 缩写表。
- `midi-device` `device` MIDI（乐器数字接口）设备。
- `pcm-device` `device` 数字音频设备。
- `preferences-file` `file` 偏好文件。
- `release-device` `onoff` 当当前屏幕或窗口无法被读取时的盲点显示器设备。
- `screen-driver` `driver` 屏幕驱动程序。
- `screen-parameters` `name=value,...` 屏幕驱动程序的参数。
- `speech-driver` `driver,...auto` 语音驱动程序。
- `speech-input` `name` 语音输入对象。
- `text-table` `table` 文本表。

详情选项。

`text-table` 表 文本表格。详情请参见 `-t (--text-table=)` 选项。

# 驱动程序规范

必须通过识别码指定盲文器或语音合成器驱动：

- Alva
- Android
- Albatross
- BrlAPI
- BrailComm
- Braudi
- B2G
- BrailleLite
- Baum
- BrailleNote
- CombiBraille
- EcoBraille
- eSpeak
- EuroBraille
- FestivalLite
- FreedomScientific
- Festival-GenericSay
- hd Hedo
- hm HIMS
- ht HandyTech
- hw HumanWare
- ir Iris
- lb Libbraille
- lt LogText
- mb MultiBraille
- md MDV
- mm BrailleMemo
- mn MiniBraille
- mp Mikropuhe
- mt Metec
- no driver
- np NinePoint
- pg Pegasus
- pm Papenmeier
- sd SpeechDispatcher
- sk Seika
- sw Swift
- th Theta
- tn
- TechniBraille Systems Inc.
- ts
- Telesensory Systems Inc.
- tt
- TTY
- vd
- VideoBraille
- vo
- Voyager, Part232 (serial adapter), BraillePen/EasyLink
- vr
- Virtual
- vs
- VisioBraille
- vv
- ViaVoice
- xs
- ExternalSpeech
- xw
- XWindow

可以指定逗号分隔的驱动程序列表。这将按顺序使用列出的每个驱动程序进行自动检测。由于某些驱动程序的自动检测效果更好，你可能需要通过来确定最可靠的顺序。

如果指定单个单词 `auto`，则将仅使用已知对该目的可靠的驱动程序进行自动检测。

# 另请

完整文档请参阅 `brltty` 的在线手册 [`http://mielke.cc/brltty/documentation.html`]

# BUILD-CLASSPATH

# 节点

`build-classpath` - 构建 Java CLASSPATH

### 概要

```
build-classpath JAR|artifact-coordinates [JAR|artifact-coordinates ...]
```

### 描述

用于使用指定的 JAR 或 Maven 构件坐标构建 Java CLASSPATH 的小型实用工具。构件坐标指定 Maven 构件，格式为 `groupId:artifactId[:extension[:classifier]]:version`。如果省略扩展，则使用“jar”。如果省略分类器，则使用空分类器。更多信息请参阅 XMvn 配置参考。CLASSPATH 返回到标准输出。

# 依赖关系

使用带有构件坐标的 `build-classpath` 需要系统可用用 `xmvn-resolve` 命令。`build-classpath` 的用户负责在系统中提供该命令。

## 示例

`build-classpath junit xerces-j2 wsdl4j` - 这将向标准输出返回一个字符串，它是包含 junit、xerces-j2 和 wsdl4j 压缩包（JARS）的有效 CLASSPATH。

`build-classpath log4j:log4j org.apache.commons:commons-io` - 这将向标准输出返回一个字符串，包含 log4j 和 commons-io JAR 的有效 CLASSPATH。

`build-classpath com.google.inject:guice::no_aop:` 这将向标准输出返回一个字符串，包含分类器 no_aop 的 google-guice JAR 的有效 CLASSPATH。

### 作者

最初由 David Walluck 编写。

# 报告错误

错误应通过 Red Hat Bugzilla 报告：`http://bugzilla.redhat.com/`。

# 另请

`build-jar-repository(1)`, `rebuild-jar-repository(1)`,

# BUILD-JAR-REPOSITORY

# 节点

`build-jar-repository` - 创建 JAR 的符号链接

### 概要

```
build-jar-repository [OPTION]... DIRECTORY JAR|artifact-coordinates
```

### 描述

在指定的目录中通过复制文件或创建符号链接构建 JAR 仓库。可以通过其名称或 Maven 构件坐标识别 JAR。构件坐标指定 Maven 构件，格式为 `groupId:artifactId[:extension[:classifier]]:version`。如果省略扩展，则使用“jar”。如果省略分类器，则使用空分类器。更多信息请参阅 XMvn 配置参考。

### 选项

如果未指定选项，默认操作将是创建符号链接

`-c, --copy`

复制文件。

`-h, --hard`

创建硬链接。

`-p, --preserve-naming` 尝试保留原始 JAR 文件的名称（如果发生嵌套，路径中的斜杠仍将被下划线替换）。使用此选项将导致无法进行任何后续的自动仓库重建，除非另有指定，否则将隐含 `-c`。

`-s, --soft, --symbolic`

创建符号链接（默认）。

`--help`

显示帮助文本

# 依赖关系

使用带有构件坐标的 `build-jar-repository` 需要系统可用 `mvn-resolve` 命令。`build-jar-repository` 的用户负责在系统中提供该命令。

## 示例

`build-jar-repository .jndi` - 这将在当前工作目录下创建一个指向 jndi JAR 的符号链接。

`build-jar-repository -h /tmp log4j` - 这将在 `/tmp` 目录下创建一个指向 log4j JAR 的硬链接。

`build-jar-repository -c org.apache.commons:commons-io` - 这将 commons-io JAR 复制到当前工作目录。

### 作者

最初由 Nicholas Mailhot 和 David Walluck 编写。

# 报告错误

错误应通过 Red Hat Bugzilla 报告：`http://bugzilla.redhat.com/`。

# 另请

`build-classpath(1)`, `rebuild-jar-repository(1)`,

# 节点

`busctl` - 检查总线

### 概要

```
busctl [OPTIONS...] [COMMAND] [NAME...]
```

### 描述



`busctl`可用于检查和监控 D-Bus 总线。

### 选项

以下选项有效：

`--address=ADDRESS`

连接到指定的`ADDRESS`总线，而不是使用系统或用户的默认值（见`--system`和`--user`）。

`--show-machine`

在显示列表时，显示所属容器名称的列。参见`systemd-machine(8)`。

`--unique`

在显示列表时，仅显示唯一名称（格式为`":number"`）。

`--acquired`

`--unique`的反反，将显示“已知”名称。

`--activatable`

在显示列表时，仅显示尚未激活但可以自动启动的对端。

`--match=MATCH`

在显示交换的消息时，仅显示匹配`MATCH`的子集。

`--size=`

配合`capture`命令使用时，指定捕捉的最大 own（snaplen）。默认为 4096 字节。

`--list`

配合`tree`命令使用时显示对象路径列表而不是树。

`--quiet`

配合`call`命令使用时抑制响应负载的显示。注意即使指定了此选项，返回的错误仍会被打印，工具将通过退出码指示成功。

`--verbose`

配合`call`或`get-property`命令使用时以更详细的格式显示输出。

`--expect-reply=BOOL`

配合`call`命令使用，指定`busctl`是否等待方法完成、输出返回的数据并通过退出码返回成功或失败。如果设置为`"no"`，则将调用方法但不期望响应，工具立即终止，因此无法显示响应，也不会通过退出码返回成功或失败。要抑制响应消息输出，请使用`--quiet`。默认`"yes"`。

`--auto-start=BOOL`

配合`call`命令使用，指定如果调用的服务未运行但配置为自动启动，则方法调用是否应隐式激活它。默认`"yes"`。

`--timeout=SECS`

配合`call`命令使用，指定等待方法完成的最大时间。如果未指定时间单位，假设为秒。也理解常用的单位（`ms`, `min`, `s`, `h`, `d`, `w`, `month`, `y`）。注意，如果使用了`--expect-reply=no`，则超时不适用，因为工具不再等待任何响应消息。当未指定或设置为 0 时，默认为`"25s"`。

`--augment-creds=BOOL`

控制是否对列表或状态报告的数据使用来自`/proc`的数据进行增强。开启此选项时，显示的数据可能不一致，因为从`/proc`读取的数据可能比其他凭据信息更新。默认`"yes"`。

`--user`

与调用用户的服务管理器通信，而不是系统的服务管理器通信。

`--system`

与系统的服务管理器通信。这是隐含的默认设置。

### `-H`, `--host=`

在远程执行操作。指定主机名，或用`@`分隔的用户名和主机名进行连接。主机名可选地以容器名作为后缀，并用`:`分隔，这将直接连接到指定主机上的特定容器。这将使用 SSH 与远程机器管理器实例通信。可以使用``machinectl -H HOST``列出容器名称。

### `-M`, `--machine=`

在本地容器上执行操作。指定要连接的容器名称。

### `-no-pager`

不将输出通过管道到分页器（pager）中。

### `-no-legend`

不打印图例，即列标题和带有提示的页脚。

### `-h`, `--help`

打印短的帮助文本并退出。

### `-version`

打印简短的版本字符串并退出。

## COMMANDS

支持以下命令：

- `list`

按服务名显示总线上的所有对端（peers）。默认显示唯一名称（unique names）和已知名称（well-known names），但可以通过`--unique`和`--acquired`选项进行更改。如果没有指定命令，则这是默认操作。

- `status [SERVICE]`

显示总线服务的进程信息和凭据（如果通过唯一名称或已知名称指定）、进程信息（如果通过数字 PID 指定），或总线的所有者（如果未指定参数）。

- `monitor [SERVICE...]`

转储正在交换的消息。如果指定了`SERVICE`，则显示由已知名称或唯一名称标识的对端收发的消息。否则，显示总线上的所有消息。使用 Ctrl-C 终止转储。

- `capture [SERVICE...]`

与`monitor`类似，将输出以 pcap 格式写入（详情请参见 Libpcap File Format-1 描述）。确保将输出重定向到 STDOUT 或文件。可以使用如`wireshark(1)`等工具来解析和查看生成的文件。

- `tree [SERVICE...]`

显示一个或多个服务的对象树。如果指定了`SERVICE`，则仅显示指定服务的对象树。否则，显示总线上所有获取了至少一个已知名称的服务的对象树。

- `introspect SERVICE OBJECT [INTERFACE]`

显示指定服务上指定对象（通过路径识别）的接口、方法、属性和信号。如果传递了接口参数，则输出将限制为指定接口的成员。

- `call SERVICE OBJECT INTERFACE METHOD [SIGNATURE [ARGUMENT...]]`

调用方法并响应。接收服务名、对象路径、接口名和方法名。如果需要向方法调用传递参数，则需要一个签名字符串，随后是单独格式化为字符串的参数。有关所用格式的详情见下文。使用`--quiet`选项来抑制返回数据的输出。

## `get-property SERVICE OBJECT INTERFACE PROPERTY...`

检索一个或多个对象属性的当前值。接收服务名、对象路径、接口名和属性名。可以同时指定多个属性，在这种情况下，它们的值将依次显示并用换行符分隔。输出默认为简写格式。使用`--verbose`获取更详细的输出。

## `set-property SERVICE OBJECT INTERFACE PROPERTY SIGNATURE ARGUMENT...`

设置对象属性的当前值。接收服务名、对象路径、接口名、属性名、签名，以及一个格式化为字符串的参数列表。

## `help`

显示命令语法。

## PARAMETER FORMATTING

`call`和`set-property`命令接收一个签名字符串以及格式化为字符串的参数列表（详情请参见 D-Bus 规范中的 Type 章节）。对于简单类型，签名后的每个参数应仅为格式化为字符串的参数值。正布尔值可以格式化为“true”、“yes”、“on”；负布尔值可以指定为“false”、“no”、“0”。对于数组，应指定一个表示条数的数字参数。对于变体（variants），应指定内容的签名。对于字典（dictionaries），应直接指定内容。例如：

- `s all`是单个字符串“all”的格式化。

- `s 3 hello foobar`是包含三个条目的字符串数组的格式化，分别为“hello”、“world”和“foobar”。

- `a{sv} 3 One Two 2 true`是一个映射字符串到变体的字典数组的格式化，包含三个条目。字符串“One”被分配字符串“Two”。被分配无符号整数 2。字符串“Yes”被分配正布尔值。

注意，`call`、`get-property`和`introspect`命令也会以这种格式生成返回数据的输出。由于这种格式有时过于简练而难以理解，当传递`--verbose`选项时，`call`和`get-property`命令可能会生成更详细的多行输出。

## EXAMPLES

### 示例 1. 写入和读取属性

这两个命令首先写入一个属性，然后将其读回。该属性位于`"org.freedesktop.systemd1"`服务的`"org.freedesktop.systemd1"`对象上。属性名称为`"org.freedesktop.systemd1.Manager"`接口上的`"LogLevel"`。属性包含单个字符串：

```
# busctl set-property org.freedesktop.systemd1 /org/freedesktop/systemd1/Manager LogLevel s debug
# busctl get-property org.freedesktop.systemd1 /org/freedesktop/systemd1/Manager LogLevel s "debug"
```

这两个命令读取一个包含字符串数组的属性，首先以简写格式显示，然后以详细格式显示：

```
# busctl get-property org.freedesktop.systemd1 /org/freedesktop/systemd1/Manager Environment as 2 "LANG=en_UTF-8" "PATH=/usr/local/sbin:/usr/sbin"
$ busctl get-property --verbose org.freedesktop.systemd1 /org/freedesktop/systemd1/Manager Environment ARRAY "s" { "LANG=en_UTF-8"; "PATH=/usr/local/sbin:/usr/sbin"; };
```

### 示例 3. 调用方法



该命令调用 `"org.freedesktop.systemd1"` 服务 `"org.freedesktop.systemd1.Manager"` 接口上的 `"StartUnit"` 方法，并传递两个字符串 `"cups.service"` 和 `"replace"`。方法返回并显示了一个对象路径参数：

```
# busctl call org.freedesktop.systemd1 /org/freedesktop/systemd1 .freedesktop.systemd1.Manager StartUnit ss "cups.service" "replace" o "/org/freedesktop/systemd1/job/42684"
```

## SEE ALSO

`dbus-daemon(1)`, `dbus-monitor(1)`, `sd-bus(3)`, `systemd(1)`, `systemd-bus-proxyd(8)`, `machinectl(1)`, `wireshark(1)`

## NOTES

- 1. Libpcap File Format

`http://wiki.wireshark.org/Development/LibpcapFileFormat`

- 2. D-Bus 规范中的 Type 章节

`http://dbus.freedesktop.org/doc/dbus-specification.html#type-system`

- 3. D-Bus

`http://freedesktop.org/wiki/Software/dbus`

### 概要

`bzgrep [ grep_options ] [ -e ] pattern filename...`

`bzegrep [ egrep_options ] [ -e ] pattern filename...`

`bzfgrep [ fgrep_options ] [ -e ] pattern filename...`

### 描述

`Bgrep` 用于对已用 `bzip2` 压缩的文件调用 `grep`。所有指定的选项将直接传递给 `grep`。如果没有指定文件，则将对标准输入进行解压并输入给 `grep`。否则，将在必要对给文件进行解压并输入给 `grep`。

如果以 `bzgrep` 或 `bzfgrep` 的形式调用 `Bgrep`，将使用 `egrep` 或 `fgrep` 代替 `grep`。如果设置了 `GREP` 环境变量，`bzgrep` 将使用其作为要调用的 `grep` 程序。例如：

```sh
for sh: GREP=fgrep bzgrep string files
for csh: setenv GREP fgrep bzgrep string files
```

# l属性

Charles Levert (`charles@comm.polymtl.ca`)。由 Philippe Troin `<phil@fifi.org>` 针对 Debian GNU/Linux 适配到 `bzip2`。

### 参见

`grep(1)`, `egrep(1)`, `fgrep(1)`, `bzdiff(1)`, `bzmore(1)`, `bzless(1)`, `bzip2(1)`

# bzip2

`bzip2`, `bunzip2` - 一个块排序文件压缩器，v1.0.6

`bzcat` - 将文件解压到 stdout

`bzip2recover` - 从损坏的 `bzip2` 文件中恢复数据

### 概要

`bzip2 [ -cdfkqstvzVL1234567892 ] [ filenames ... ]`

`bunzip2 [ -fkvsVL ] [ filenames ... ]`

`bzcat [ -s ] [ filenames ... ]`

`bzip2recover filename`

### 描述

`bzip2` 使用 Burrows-Wheeler 块排序文本压缩算法和霍曼编码来压缩文件。压缩效果通常比基于传统的 LZ77/LZ78 的压缩器好得多，并接近 PPM 族统计压缩器的性能。

命令行选项刻意设计得与 GNU `gzip` 非常相似，但并不完全相同。

`bzip2` 期望一个文件名列表来配合命令行标记。每个文件都将被替换为自身的压缩版本，文件名为 "`original_name.bz2`"。每个压缩文件具有与原始文件相同的修改日期、权限，并且在可能的情况下相同的所有者，以便在解压时能够正确恢复这些属性。文件名的处理是原始的，因为在缺乏这些概念或有文件名长度限制（如 MS-DOS）的文件系统中，没有机制可以保留文件中的原始文件名、权限、所有者或日期。

`bzip2` 和 `bunzip2` 默认不会覆盖现有文件。如果你希望执行此操作，请指定 `-f` 标记。

如果没有指定名称，`bzip2` 将从标准输入压缩到标准输出。在这种情况下，`bzip2` 将拒绝将压缩输出写入终端，因为这将是完全不可读且毫无意义的。

`bunzip2`（或 `bzip2 -d`）解压所有指定的文件。不是由 `bzip2` 创建的文件将被检测并忽略，同时发出警告。`bzip2` 尝试根据压缩文件的文件名推断解压文件的文件名，如下：

- `filename.bz2` 变为 `filename`
- `filename.bz` 变为 `filename`
- `filename.tbz` 变为 `filename.tbz`
- `filename.tbz` 变为 `filename.tar`
- 其他任何变为 `anyname.out`

如果文件不是以识别的扩展名 `.bz2`, `.bz`, `.tb2` 或 `.tar` 结尾，`bzip2` 会抱怨它无法猜测原始文件的文件名，并使用带有 `.out` 后缀的文件名。

与压缩一样，不提供文件名会导致从标准输出进行解压。

`bzip2` 可以正确解压由两个或多个压缩文件连接的文件。结果是相应的解压文件的连接。还支持对连接的压缩文件进行完整性测试 (`-t`)。

你还可以通过提供 `-c` 标记将文件压缩或解压到标准输出。可以这样压缩和解压多个文件。产生的输出按顺序输入到 stdout。这种方式压缩多个文件会生成一个包含多个压缩文件表示的流。这种流只有 `bzip2` 0.9.0 或更高版本才能正确解压。早版本的 `bzip2` 将停止解压流中的第一个文件。

`bzcat`（或 `bzip2 -dc`）将所有指定的文件解压到标准输出。

`bzip2` 会顺序从环境变量 `BZIP2` 和 `BZIP` 读取参数，并在从命令行读取的任何参数之前处理它们。这提供了一种提供默认参数的方便方法。

始终执行压缩，即使压缩文件比原始文件稍大一点。小于一百字节的文件往往会变大，因为压缩机制在 50 字节左右有恒定的开销。随机数据（包括大多数文件压缩器的输出）每字节按约 8.05 位编码，导致约 0.5% 的膨。

作为一种保护自检，`bzip2` 使用 32 位 CRC 来确保文件的解压版本与原始文件相同。这可以防止压缩数据损坏，并防止 `bzip2` 中未被检测到的错误（希望非常不利）。数据损坏未被检测到的概率微乎其微，每个处理的文件大约为四十亿分之一。但请注意，检查是在解压时发生的，因此它只能告诉你出了问题。它无法帮助你恢复原始未解压数据。你可以使用 `bzip2recover` 尝试恢复数据。

返回值：`0` 表示正常退出，`1` 表示环境问题（找不到文件、I/O 错误），`2` 表示压缩文件损坏，`3` 表示内部一致性错误（导致 `bzip2` 崩溃）。

### 选项

`-c`—stdout

压缩或解压到标准输出。

`-d`—解压

强制解压。`bzip2`, `bunzip2` 和 `bzcat` 实际上是同一个程序，根据调用名称决定采取何种操作。

`-z`—压缩

`-d` 的补充：无论使用哪个名称都强制压缩。

`-t`—测试

检查指定文件的完整性，但不解压。

`-f`—强制

强制覆盖输出文件。通常 `bzip2` 不覆盖现有文件。还会强制 `bzip2` 断开链接。这是 GNU `gzip` 的行为。

`-k`—保留

在压缩或解压时保留（不删除）输入文件。

`-s`—小

减少内存使用。压缩时使用每字节 2.5 字节的修改算法。这意味着任何文件都可以在 30k 内存中解压，尽管速度只有一半。在压缩期间，`-s` 选择 200k 的块大小，限制了内存使用，但以牺牲压缩率为代价。简而言之，如果你的机器内存不足（8MB 或更少），一切使用 `-s`。见内存管理。

`-q`—安静

抑制必要的警告消息。有关 I/O 错误和其他关键事件的消息将不会抑制。

`-v`—详细

详细模式 —显示每个处理文件的压缩率。更多的 `-v` 会增加详细程度，输出大量主要用于诊断的信息。

`-L`—许可—版本

显示软件版本、许可条款和条件。

`-1`（或`—fast`）到 `-9`（或`—best`）

压缩时将块大小设置为 100k 到 900k。解压时无效。见内存管理。`—fast` 和 `—best` 别名主要是为了与 `gzip` 兼容。特别是，`—fast` 并不会显著变快。而 `—best` 只是选择了默认行为。

`--`

将所有后续参数视为文件名，即使它们以破折号开头。这样就可以处理以破折号开头的文件，例如：`bzip2 -- myfilename`。

`repetitive-fast repetitive-best`

这些标记在 0.9.5 及以上版本中是冗的。它们在早期版本中对排序算法的行为提供了一些粗略的控制，有时有用。0.9.5 及以上版本使用了改进的算法，使得这些标记变得无关紧要。

# 内存管理



# bzip2 块压缩与内存使用

bzip2 以块压缩大文件。块大小会影响所实现的压缩率，以及压缩和解压所需的内存量。标记 `-1` 到 `-9` 分别将块大小指定为 100,000 字节到 900,000 字节（默认值）。在解压时，压缩时使用的块大小将从压缩文件的头部读取，`bzip2` 仅分配足够的内存来解压该文件。由于块大小存储在压缩文件中，因此 `-1` 到 `-9` 标记在解压过程中是无关的，会被忽略。

压缩和解压所需的内存（以字节计）可以估计为：

- 压缩：`400k + ( 8 * 块大小 )`
- 解压：`100k + ( 4 * 块大小 )` 或 `1000k + ( 2.5 * 块大小 )`

较大的块大小边际收益迅速递减。大部分压缩效果来自于前两个或三百 k 的块大小，这在小型机器上使用 `bzip2` 时需要注意。此外，重要的是，解压内存需求是通过块大小的选择在解压时设定的。

对于使用默认 900k 块大小压缩的文件，`bzip2` 需要约 3700 kbytes 内存进行解压。为了支持在 4MB 内存上解压任何文件，`bzip2` 有一个选项可以使用大约一半的内存（约 2300 字节）。但解压速度也会减半，因此仅在必要时使用此选项。相关的标记是 `-s`。

通常情况下，请使用内存允许的最大块大小，因为这可以实现最大的压缩。压缩和解压速度几乎不受块大小的影响。

另一个重要点适用于适合单个块的文件——这意味着当你使用大块大时会遇到的文件。如果文件小于一个块，实际接触的内存量与文件大小成比例。例如，使用标记 `-9` 压缩一个 20,000 字节的文件将导致压缩分配约 7600k 内存，但其中只有 `400k + 20000 * 8 = 560 kbytes`。同样，解压器将分配 3700k，但仅使用 `100k + 20000 * 4 = 180 kbytes`。

以下表显示了 Calgary 文本压缩语库中 14 个文件（总计 3,141,622 字节）的最大内存使用。这一列让你大致了解压缩是如何随块大小变化的。这些数字倾向于低估大块大小对大文件的优势，因为该语库主要以小文件为主。

| 压缩 | 解压 | 语库标记 | 使用量 | 大小 |
|---|---|---|---|---|
| -1 | 1200k | 500k | 350k | 914704 |
| -2 | 2000k | 900k | 600k | 877003 |
| -3 | 2800k | 1300k | 850k | 860338 |
| -4 | 3600k | 1700k | 1100k | 846899 |
| -5 | 4400k | 2100k | 1350k | 845160 |
| -6 | 5200k | 2500k | 1600k | 838626 |
| -7 | 6100k | 2900k | 1850k | 834096 |
| -8 | 6800k | 3300k | 2100k | 828642 |
| -9 | 7600k | 3700k | 2350k | 828642 |

## 从损坏文件中恢复数据

`bzip2` 以块压缩文件，通常每块 900kbytes。每个块都被独立处理。如果介质或传输错误导致多块 `.bz2` 文件损坏，则可能从文件中未损坏的块中恢复数据。

每个块的压缩表示由一个 48 位模式界定，这使得能够相当有把握地找到块边界。每个块还带有自己的 32 位 CRC，因此可以将损坏块与未损坏块区分开。

`bzip2recover` 是一个简单的程序，其目的是搜索 `.bz2` 文件中的块，并将每个块写入单独的 `.bz2` 文件中。你可以使用 `bzip2 -t` 测试生成文件的完整性，并解压那些未损坏的文件。

`bzip2recover` 接收单个参数，即损坏文件的名称，并将每个块写入单独的 `.bz2` 文件中。你可以使用 `bzip2 -t` 测试生成文件的完整性，并解压那些未损坏的文件。

### 描述

`Bzmore` 是一个过滤器，允许在软拷贝终端上一次显示一屏压缩文件或纯文本文件进行检查。`bzmore` 既可以处理用 `bzip2` 压缩的文件，也可以处理未压缩的文件。如果文件不存在，`bzmore` 将查找文件名带有 `.bz2` 后缀的同名文件。

`Bzmore` 通常在每屏显示后暂停，并在屏幕底部打印—More—。如果用户使用回车键，将显示额外一行。如果用户按下空格键，则将显示另一个屏的内容。其他可能性将在后文中列出。

`Bzmore` 通过查找 `/etc/termcap` 文件来确定终端特性以及默认窗口大小。在能够显示 24 行的终端上，默认窗口大小为 22 行。当 `bzmore` 暂停时可以输入的其他序列及其影响如下（`i` 是一个可选的整数参数，默认为 1）：

- `- - i<space>`
  显示 `i` 行内容（如果未提供参数，则显示另一个屏的内容）
- `- - ^D`
  显示 11 行（一次“滚动”）。如果给出了 `i`，则滚动大小设置为 `i`。
- `- - d`
  同 `^D` (control-D)
- `- - iz`
  与输入空格键相同，但如果存在 `i`，它将成为新的窗口大小。注意窗口大小在当前文件结束时会恢复到默认值。
- `- - is`
  跳过 `i` 行并打印一屏内容
- `- - if`
  跳过 `i` 屏并打印一屏内容
- `- - q` 或 `Q`
  退出读取当前文件；进入下一个文件（如果有）。
- `- - e` 或 `q`
  当打印提示符—More-(Next file: file) 时，此命令导致 `bzmore` 退出。
- `-` 当打印提示符—More-(Next file: file) 时，此命令导致 `bzmore` 跳过下一个文件并继续。

## 显示当前行号。

### iepr

搜索正则表达式 `expr` 的第 `i` 次出现位置。如果没有找到该模式，`bzmore` 将继续处理下一个文件（如果有）。否则，将显示一屏内容，从找到表达式的位置的前两行开始。用户可以使用删除（erase）字符和杀掉（kill）字符来编辑正则表达式。向后删除到第一列之前将取消搜索命令。

### in

搜索上次输入的正则表达式的第 `i` 次出现位置。

### !command

调用带有 `command` 的 shell。`command` 中的字符 `!` 将被替换为上一次的 shell 命令。序列 `\!` 被替换为 `i`。

### :q 或 :Q

退出读取当前文件；进入下一个文件（如果有）（同 `q` 或 `Q`）。

### (点) 重复上一个命令。

命令会立即生效，即不需要输入回车键。在输入命令本身之前，用户可以按下行杀掉字符（line kill character）来取消正在形成的数字参数。此外，用户可以按下删除字符（erase character）重新显示 —More— 信息。

在向终端发送输出的任何时候，用户都可以按下退出键（通常为 control-\）。`Bzmore` 将停止发送输出并显示通常的 —More — 提示符。用户随后可以正常输入命令之一。遗憾的是，这样做会丢失一些输出，因为退出信号发生时，终端输出队列中等待的所有字符都会刷新。

此程序将终端设置为无回显（noecho）模式，以便输出是连续的。你输入的内容不会显示在终端上，`/ ` 和 `!` 命令除外。

如果标准输出不是电字机（teletype），`bzmore` 的行为就像 `bcat` 一样，但在每个文件之前会打印页头。

### 文件

`/etc/termcap`

终端数据库

## 另参

`more(1)`, `less(1)`, `bzip2(1)`, `bzdiff(1)`, `bgrep(1)`

## 名称

`c2ph`, `pstruct` - 将“cc -g -S”生成的 stabs 导出 C 结构

### 概要

```
c2ph [-dpnP] [var=val] [files...]
```

### 选项

选项：`-w`宽；缩写为：`type_width=45 member_width=35 offset_width=8`

- `x` 十进制；缩写为：`offset_fmt=x size_width=08 size_fmt=x size_width=04`
- `-n` 不生成 perl 代码（作为 `pstruct` 调用时为默认值）
- `-p` 生成 perl 代码（作为 `c2ph` 调用时为默认值）
- `-v` 生成 perl 代码，并将 C 声明作为注释
- `-i` 不重新计算内置数据类型的大小
- `-a` 同时也转储内置数据类型的信息
- `-t` 跟踪执行
- `-d` 产生大量的调试输出
- `-s-list` 给出逗号分隔的结构列表进行转储

### 描述

以下是 Tom Christiansen 的旧版 `c2ph.doc` 文档

`<christ@perl.com>` 日期：91年7月25日 08:10:21 GMT

很久以前，我写了一个名为 `pstruct` 的程序。这是一个 perl 程序，尝试解析 C 结构并显示它们的成员偏移量。这对于查看二进制转储或研究内核的人来说特别有用。

`pstruct` 并不是一个漂亮的程序。它也不特别健壮。你知道的，问题在于，编译器解析 C 的能力远比我所希望的要强。

所以我变得聪明：我决定偷懒，让 C 编译器来解析 C，它会为我输出调试器 stabs。这些要容易解析得多。它仍然不是一个漂亮的程序，但至少是健壮的。`pstruct` 接受任何 `.c` 或 `.h` 文件，因为它将把它们转换为这种格式并输出如下列表：



```
struct tty { int tty.tty_locker 000 4 int tty.tty_mutex 004 4 struct tty.tp_virt 008 4 struct tty.tty_rawq 02c 10 int tty.tty_rawq.cmax 010 4 tty.tty_rawq.cxf 014 4 int tty.tty_rawq.clix 038 4 struct tty *tty.tty_rawq.c_001 4 struct tty *tty.tty_c_iop 020 8 unsigned char * tty.tty_rawq.c_buf 024 4 unsigned char * tty.tty_cq.buf_iop 008 4 struct tty.tty_cq.cmax 02c 20 intty.tty_cq.cc 022 4 int tty.tty_cq.cmax 030 4 tty.tty_cq.cxf 034 4 int tty.tty_cq.clix 038 4 struct tty *tty.tty_cq.tp_cpu 03c 4 struct *tty.tty_cq.tp_iop 004 8 unsigned char * tty.tty_cq.buf_cpu 044 8 unsigned char * tty.tty_cq.buf_iop 048 4 struct tty.tty_outq 04c 20 int 000 4 int tty.tty_outq.cc 064 050 4 int tty.tty_outq.clix 054 4 struct tty *tty.tty_outq.c_iop 060 4 unsigned char * tty.tty_outq.c_buf 064 4 unsigned char * tty.tty_outq.buf_iop 068 4 (*int()) tty.tty_oproc 006 6 (*int()) tty.tty_oproc_iop 070 4 (*int())tty.tty.stopproc_cpu 074 4 (*int()) tty.tty.stopproc_iop 078 4 struct thread tty.resel 07c 4
```

实际上，这由特定的选项生成。你可以控制每列的格式，无论你喜欢宽的还是窄的、十六进制还是十进制、前导零或其他。

你只需要一个生成 BSD/GCC 风格 stubs 的 C 编译器。（此处后续大量重复的段落已根据要求未重复翻译）

程序的各个部分相互进行通信等。如果我不需要现场推断这些位符（stabs）的组成，并对我的编译器与 gcc 之间的微小差异进行处理，可能也会有所帮助。

总之，它在这里了。应该可以在 perl v4 或更高版本上运行。也许低版本也可以。

- tom

# C_REHASH

## 名称

`c_rehash` - 为哈希值命的文件创建符号链接

### 概要

```
c_rehash [-old] [-h] [-n] [-v] [directory...]
```

### 描述

`c_rehash` 扫描目录并为指定目录列表中的每个 `.pem`、`.crt`、`.cer` 或 `.crl` 文件计算哈希，并为每个文件创建符号链接，其中链接的名称为哈希值。该实用程序非常有用，因为许多使用 OpenSSL 目录的程序首先按照此顺序设置以查找证书。（如果平台不支持符号链接，则会创建副本。）

如果命令行上指定了任何目录，将按顺序处理。如果没有，将查询环境变量 `SSL_DIRPATH`；它应该是一个由冒号分隔的目录列表。如果未设置该变量，则处理默认目录（特定于安装，但通常为 `/usr/local/ssl/certs`）。

为了处理目录，用户必须拥有该目录的权限，否则将被跳过。创建的链接格式为 `HHHHHNNNN.D`，其中每个 `H` 是十六进制字符，`D` 是一个十进制数字。在处理目录时，`c_rehash` 将首先删除该目录下所有具有此类名称的链接。如果你有其他用途的此类格式链接，它们将被删除。要跳过删除步骤，请使用 `-n` 标志。CRL 的哈希看起来相似，只是字母 `r` 出现在点之后，如下：`HHHHHNNNN.r`。

多个对象可能具有相同的哈希；它们将通过增加 `D` 值来。通过比较完整的 `SHA-1` 指纹可以发现重复项。如果发现重复，将显示警告。

如果存在无法解析为证书或 CRL 的文件，也将显示警告。

该程序使用 `openssl` 程序来计算哈希和指纹。如果在此用户的 PATH 中未找到，则将 `OPENSSL` 环境变量设置为完整路径。可以使用任何程序，它对于证书或 CRL 都将以如下方式调用：

```
$OPENSSL x509 -hash -fingerprint -noout -in FILENAME $OPENSSL crl -hash fingerprint -noout -in FILENAME
```

其中是文件名。它必须在第一行输出文件的哈希，在第二行输出指纹，可选地带有某些文本和等号的前缀。

`FILENAME`

### 选项

- `-old`

为 1.0.0 之前的版本使用旧式哈希（`MD5`，而非 `SHA-1`）来生成链接。请注意，当前版本将不再使用旧式样式。

- `-h`

显示简短的使用信息。

- `-n`

不删除现有的链接。当在同一目录中保留新旧样式链接时，需要此项。

- `-v`

打印关于删除的旧链接和创建的新链接的消息。默认情况下，`c_rehash` 只在处理每个目录时列出它。

## 环境

`OPENSSL`

用于生成哈希和指纹的可执行文件路径（见上文）。

`SSL_CERT_DIR`

要操作的目录分隔列表。如果命令行上列出了目录，则忽略。

### 参见

`openssl(1)`, `crl(1)`. `x509(1)`.

## 名称

`ca` - 示例最小 CA 应用程序

### 概要

```
openssl ca [-verbose] [-config filename] [-name section] [-gencrl] [-revoke file] [-nstatus serial] [-updatedb] [-crl_reason reason] [-crl_hold instruction] [-crl_compromise time] [-crl_CA_compromise time] [-crldays days] [-crlhours hours] [-crelets section] [-startdate date] [-enddate date] [-days arg] [-md arg] [-policy arg] [-keyfile arg] [-keyform PEM|DER] [-key arg] [-passin arg] [-cert file] [-selfsign] [-infile] [-out file] [-notext] [-outdir dir] [-infiles] [-spkac file] [-ss_cert file] [-preserveDN] [-noemailDN] [-batch] [-msie_hack] [-extensions section] [-extfile section] [-engine id] [-subj arg] [-utf8] [-multivalue-rdn]
```

### 描述

`ca` 命令是一个最小的 CA 应用程序。它可以用于签名各种形式的证书请求并生成 CRL，它还维护一个已发布证书及其状态的文本数据库。

选项描述将按每个用途划分。

# CA 选项

- `-config filename`

指定使用的配置文件。

- `-name section`

指定使用的配置部分节（覆盖 `ca` 部分中的默认 `ca`）。

- `-in filename`

输入文件名，包含一个要由 CA 签名的单个证书请求。

- `-ss_cert filename`

一个要由 CA 签名的自签名证书。

- `-spac filename`

一个包含已签名的 Netscape 公钥和要由 CA 签名的额外字段的文件。有关所需的输入和输出格式的信息，请参见 SPKAC FORMAT 部分。

- `-infiles`

如果这应该是最后一个选项，则所有后续参数都被假设为包含证书请求的文件名。

- `-out filename`

输出证书的输出文件。默认是标准输出。证书详情也将输出。

- `-outdir directory`

输出证书的目录。证书将以 `.pem` 格式写入。

- `-cert`

CA 证书文件。

- `-keyfile filename`

用于签名请求的私钥。

- `-keyform PEM|DER`

密钥的格式。默认是 `PEM`。

- `-key password`

用于加密私钥的密码。由于某些系统的限制，应谨慎使用。

- `-selfsign`

指示要签名的已发布证书。如果给了 `-spac`、`-ss_cert` 或 `-gencrl`，则忽略 `-selfsign`。`-selfsign` 的结果是自签名证书出现在证书数据库中。

- `-passin arg`

关键字来源。有关格式的更多信息请参见 `openssl(1)`。

- `-verbose`

这会打印有关正在执行的操作的额外细节。

- `-notext`



# 不输出证书的文本

进入目录，找到证书相关文件。

- `-startdate date`

允许设置起始日期。日期格式为 `YYYYMMDDHHSS`（与 ASN1 结构相同）。

- `-enddate date`

允许设置过期日期。日期格式为 `YYYYMMDDHHSS`（与 ASN1 结构相同）。

- `-days arg`

证书有效的天数。

- `-md arg`

使用的消息哈希算法。可能的值包括 `md5`、`sha1` 和 `mdc2`。哈希的完整列表请查看 `openssl -h`。此选项也适用于 CRL。

- `-policy arg`

定义使用的 CA “策略”。这是配置文件中的一个部分，决定了哪些字段是强制性的或与 CA 证书匹配。更多信息参见 `POLICY FORMAT` 部分。

- `-msie_hack`

这是一个为了与非常旧版本的 IE 证书注册控制兼容的遗留选项。它几乎使用 UniversalStrings。由于旧控制存在各种安全漏洞，强烈建议不要使用。新的控制 `Xenroll` 不需要此选项。

- `-preservedDN`

通常证书的 DN 顺序与相关策略部分中字段的顺序相同。设置此选项时，顺序与请求相同。这在很大程度上是为了兼容旧的 IE 注册控制，该控制只接受 DN 顺序与请求匹配的证书。`Xenroll` 不需要此选项。

- `-noemailDN`

如果在 DN 中存在，证书的 DN 可以包含 EMAIL 字段，但良好的策略是将电子邮件设置在证书的 altName 扩展中。当设置此选项时，EMAIL 将从证书主题中删除，并仅设置在最终出现的扩展中。可以在配置文件中使用 `email_in_dn` 关键字来启用此行为。

- `-batch`

设置批模式。在此模式下，不会询问任何问题，所有证书将自动签名。

- `-extensions section`

配置文件中包含在发布证书时添加的扩展部分（除非使用了 `-extfile` 选项，否则默认是 `x509_extensions`）。

已使用。如果没有扩展部分（extension section），则创建一个 V1 证书。如果存在扩展部分（即使它是空的），则创建一个 V3 证书。详情请参见 `x509v3_config(5)` 手页中关于扩展部分格式的说明。

- `-extfile file`

一个额外的配置文件，用于从其中读取证书扩展信息（除非同时使用了 `-extensions` 选项，否则使用默认节）。

- `-engine id`

指定一个引擎（通过其唯一 ID 字符串）将使 `ca` 尝试获取指定引擎的功能引用，并在需要时对其进行初始化。该引擎将设置为所有可用算法的默认引擎。

- `-subj arg`

覆盖请求中给出的主题名称（subject name）。参数的格式必须为 `/type0=value0=type1=value1=type2=...`，字符可以通过 `\`（反斜杠）进行转义。

- `-utf8`

此选项导致字段值被解释为 UTF8 字符串，默认情况下它们被解释为 ASCII。这意味着字段值（无论是从终端提示还是从配置文件获取）都必须是有效的 UTF8 字符串。

- `-multvalue-rdn`

此选项导致 `-subj` 参数在解析时完全支持多值 RDN（相对区分名称）。示例：

```
/DC=org/DC=OpenSSL/users/UID=123456+CN=John Doe
```

如果不使用 `-multi-rdn`，则 UID 值为 `123456+CN=John Doe`。

## CRL 选项

- `-gencrl`

此选项根据索引文件中的信息生成 CRL（吊销列表）。

- `-crldays num`

下一次 CRL 到期前的天数。即从现在起放入 CRL `nextUpdate` 字段的天数。

- `-crhours num`

下一次 CRL 到期前的小时数。

- `-revoke filename`

包含要撤销证书的文件名。

- `-status serial`

显示指定序列号证书的撤销状态并退出。

- `-updateddb`

更新数据库索引以清除过期的证书。

- `-crl_reason reason`

原因，其中 `reason` 是以下值之一：`unspecified`（未指定）、`keyCompromise`（密钥泄露）、`CACompromise`（CA 泄露）、`affiliationChanged`（关系变更）、`cessationOfOperation`（停止运营）、`certificateHold`（证书吊起）或 `removeFromCRL`（从 CRL 中移除）。原因的匹配区分大小。设置撤销原因将使 CRL 变为 v2。

在实践中，`removeFromCRL` 并不特别有用，因为它只用于目前尚未实现的增量 CRL（delta CRLs）。

- `-crl_hold instruction`

将 CRL 撤销代码设置为 `certificateHold`，并将吊起指令设置为 `instruction`，该指令必须是一个 OID。可以使用任何其他 OID，但只能用于 `holdInstructionNone`（RFC2459 建议不使用）、`holdInstructionIssuer` 或 `holdInstructionReject`，通常会使用这些。

- `-crl_compromise time`

将撤销原因设置为 `keyCompromise`，并将泄露时间设置为 `time`。时间应采用 `GeneralizedTime` 格式，即 `YYYYMMDDHMMSSZ`。

- `-crl_CAcompromise time`

此项与 `crl_compromise` 相同，不同之处在于撤销原因被设置为 `CACompromise`。

- `-clexts section`

配置文件中包含包含的 CRL 扩展的节。如果没有 CRL 扩展节，则创建一个 V1 CRL；如果存在 CRL 扩展节（即使是空的），则创建一个 V2 CRL。指定的 CRL 扩展是 CRL 扩展而非 CRL 条目扩展。需要注意的是，软件（例如 Netscape）无法处理 V2 CRL。详情请参见 `x509v3_config(5)` 手页中关于扩展部分格式的说明。

## 配置文件选项

配置文件中包含 `ca` 选项的节查找如下：如果使用了 `name` 命令行选项，则将命名要使用的节。否则，要使用的节必须在配置文件 `ca` 节的 `default_ca` 选项中（或在配置文件的默认节中）命名。除了 `default_ca` 外，以下选项直接从 `ca` 节读取：`RANDFILE`、`preserve`、`preserve_`。除 `RANDFILE` 之外，这可能是一个错误，并在未来的发布中发生变化。

许多配置文件选项与命令行选项相同。当文件中存在该选项且使用了命令行值时，以命令行值为准。如果选项被描述为强制性的，则它必须在配置文件或使用的对应的命令行（如果有）中存在。

- `oid_file`

指定一个包含额外 `.objects` 的文件。文件的每行应由对象标识符的数字形式组成，随后是空格、短名、再是空格，最后是长名。OBJECT IDENTIFIERS

- `oid_section`

指定配置文件中一个包含额外对象标识符的节。每行应由对象标识符的短名、等号 `=` 和其数字形式组成。使用此选项时，短名和长名是相同的。

- `new_certs_dir`

与 `-outdir` 命令行选项相同。它指定新证书存放的目录。强制性。

- `certificate`

与 `-cert` 相同。提供包含 CA 证书的文件。强制性。

- `private_key`

与 `-keyfile` 选项相同。包含 CA 私钥的文件。强制性。

- `RANDFILE`

一个用于读取和写入随机数种子信息的文件，或一个 EGD 套接字（参见 `RAND_egd(3)`）。

- `default_days`

与 `-days` 选项相同。证书有效期的天数。

- `default_startdate`

与 `-startdate` 选项相同。证书的起始日期。如果没有设置，则使用当前时间。

- `default_enddate`

与 `-enddate` 选项相同。必须存在此选项或 `default_days`（或对应的命令行）。

- `default_crl_hours` `default_crl_days`

与 `-crrlhours` 和 `-crldays` 相同。只有当这些选项都不存在时，才会使用这些来生成 CRL。

- `default_md`

与 `-md` 选项相同。要使用的消息摘要算法。强制性。

- `database`

要使用的数据库文件。强制性。

- `unique_subject`

如果给值为 `yes`，数据库中的证书条目必须是唯一的。如果给值为 `no`，证书条目可以具有相同的相同。默认值为 `yes`，特别是当配合 `-selfsign` 选项使用时，建议使用 `no`。

- `serial`

包含要使用的序列号的文件。强制性。此文件必须存在并包含有效的序列号。

- `crnl`

包含要使用的 CRL 号的文件。只有当此文件存在时，才会插入 CRL 中。如果此文件存在，必须包含有效的 CRL 号。

- `x509_extensions`

与 `-extensions` 相同。

- `rl_extensions`

与 `-crlects` 相同。

- `preserve`

与 `-preserveDN` 相同。



`email_in_dn`

与 `-noemailDN` 相同。如果你想从证书的 DN 中删除 EMAIL 字段，只需将其设置为 `no`。如果不是，默认允许 DN 中有 email 字段。

`msie_hack`

与 `-msie_hack` 相同。

`policy`

与 `-policy` 相同。强制性。更多信息请参见 `POLICY FORMAT` 节。

`name_opt`,`cert_opt`

这些选项允许在请求用户签名时显示证书详情。`x509` 工具支持的所有 `-nameopt` 和 `-certopt` 切换开关均可在此处使用。`no_signame` 和 `no_sigdump` 被永久设置且无法禁用（这是因为此时证书尚未签名，无法显示签名）。

为了方便起见，两者接受 `ca_default` 以产生合理的输出。

如果这两个选项都不存在，则使用早期版本 OpenSSL 的格式。强烈建议不要使用旧格式，因为它只显示策略节中提到的字段，错误地处理多字符字符串类型且不显示扩展。

`copy_extensions`

决定如何处理证书请求中的扩展。如果设置为 `none`（或未出现此选项），则忽略扩展且不复制到证书中。如果设置为 `copy`，则将请求中任何尚未存在的扩展复制到证书中。如果设置为 `copyall`，则将请求中的所有扩展复制到证书中：如果扩展已存在于证书中，则先将其删除。在使用此选项之前请参见 `WARNINGS` 节。

此选项的主要用途是允许证书请求提供扩展（如 `subjectAltName`）的值。

# 策略格式

策略部分由一组与证书 DN 字段对应的变量组成。如果值为“match”，则该字段值必须与 CA 证书中的相同字段匹配。如果值为“supplied”，则该字段必须存在。如果值为“optional”，则该字段可能存在。策略部分中未提到的任何字段都将被静默删除，除非设置了 `-preserveDN` 选项，但这可以更多地看作是一个异常行为而非刻意的设计。

# SPKAC 格式

`-spkac` 命令行选项的输入是一个 Netscape 签名的公钥和挑战。这通常来自 HTML 表单中的 KEYGEN 标签，用于创建新的私钥。然而，也可以使用 `spkac` 工具创建 SPKAC。

该文件应包含设置为 SPKAC 值的变量 `SPKAC`，以及作为键值对（name value pairs）的所需的 DN 组件。如果你需要包含两个相同的组件，可以在其前面加上数字和一个“\”。

在处理 SPKAC 格式时，如果使用了 `-out` 标志，输出为 DER 格式；如果发送到 stdout 或使用 `-outdir` 标志，则输出为 PEM 格式。

## 示例

这些示例假设 ca 目录结构已经建立，且相关文件已经存在。这通常涉及使用 req 创建 CA 证书和私钥、一个序列号文件和一个空索引文件，并将它们放置在相关的目录中。

在使用示例配置文件之前，将创建 `demoCA`、`demoCA/private` 和 `demoCA/newcerts` 目录。CA 证书将复制到 `demoCA/cacert.pem`，其私钥将复制到 `demoCA/private/cakey.pem`。将创建一个文件 `demoCA/serial`，其中包含“01”，以及一个空索引文件 `demoCA/index.txt`。

签名证书请求：

```
openssl ca -in req.pem -out newcert.pem
```

使用 CA 扩展程序签名证书请求：

```
openssl ca -in req.pem -extensions v3_ca -out newcert.pem
```

生成 CRL：

```
openssl ca -gencrl -out crl.pem
```

签名多个请求：

```
openssl ca -infiles req1.pem req2.pem req3.pem
```

认证一个 Netscape SPKAC：

```
openssl ca -spkac.txt
```

一个示例 SPKAC 文件（为了清晰起见，SPKAC 行已截断）：

```
SPKAC:MIG0MGawXANBqJhkkiIGw0BAQEFAANLADBIAKEAnPDhCeV/xIXUg8V70YRXK2A5
CN=Test emailaddress=openssl.org 0.0=OpenSSL Group
1.OU=Another Group
```

包含 CA 相关部分的示例配置文件：

```
[ ] default_ca = CA_default 默认部分 [ CA_default ]
./demoCA # 顶部索引数据库 = $dir/index.txt # 索引文件。new_certs_dir
=$dir/newcerts # 新证书目录 = $dir/cacert.pem # CA证书
s=$dir/serial # 序列号文件 private key = $dir/private/cakey.pem #
CA私钥 RANDFILE = $dir/private/ # 随机数
default_days = 365 # 默认认证有效期
crl_days = 30 # CRL 之前的有效期
next before CRL default = md5 # 使用策略
_policy = any = 默认策略
email_in = no # 不将电子邮件添加到 DN 中
name_opt ca_default # 主体名称显示
copy opt_cert = ca_default # 证书显示
copy extensions = none # 不从请求复制扩展
from request [ _policy_any ] countryName = supplied stateProvinceName =
optional organizationName = optional organizationalUnitName = optional
CommonName = supplied emailAddress = optional
```

### 文件

注意：所有文件的位置都可以通过编译时选项、配置文件条目、环境变量或命令行选项发生变化。下方的值反映了默认值。

```
/usr/local/ssl/lib/openssl.cnf - 主配置文件
./demoCA - 主 CA 目录
./demoCA/cacert.pem - CA 证书
./demoCA/private/cakey.pem - CA 密钥
./demoCA/serial - CA 序列号
./number file ./demoCA/serial.old - CA 私钥 ./demoCA/serial - CA 序列号备份文件
./demoCA/index.txt - CA 文本数据库文件 ./demoCA/index.old - CA 文本
数据库备份文件 ./demoCA/certs - 证书输出文件 ./demoCA/.rnd
- CA 随机种子信息
```

## 环境变量

`OPENSSL_CONF` 反映主配置文件的位置，它可以通过 `-config` 命令行选项覆盖。

# 限制

文本数据库索引文件是过程中的关键部分，如果损坏，则很难修复。理论上，可以从所有已颁发的证书和当前 CRL 重建索引文件：但没有选项可以执行此操作。

目前不支持增量 CRL 等 V2 CRL 特性。

虽然可以一次性输入并处理多个请求，但只能包含一个 SPKAC 或自签名证书。

# Bug

当存在大量证书时，使用内存文本数据库可能会导致问题，因为如所示，数据库必须保持在内存中。

## 示例

取消当前打印作业：`cancel` 取消作业“myprinter-42”：`cancel myprinter-42` 取消所有作业：`cancel -a`

# 注意

希望通过 `-u` 选项防止未经授权取消作业的管理员，应该在 `cupsd.conf(5)` 中对 Cancel-Jobs 操作要求身份验证。

# 另另

`cupsd.conf(5)`, `lp(1)`, `lpmove(8)`, `lpstat(1)`, CUPS 在线帮助 (`http://localhost:631/help`)

# 版权

Copyright © 2007-2014 Apple Inc.

## 名称

`capsh` - 能力 shell 包装器

### 概要

```
capsh [OPTION]...
```

### 描述

可以使用此工具探索和限制 Linux 能力的支持和使用。该工具为某些类型的能力测试和环境创建提供了方便的包装器。它还提供了一些有助于总结能力状态的调试功能。

### 选项

该工具接受多个可选参数，并按照提供的顺序对其进行操作。它们如下：

- `--print`

  显示当前的能力和相关状态。

- `--args`

  带有尾随参数执行 `/bin/bash`。注意，你可以使用 `-c ‘要执行的命令’`执行特定命令。

- `-- ===`

  使用剩余参数再次执行 `capsh`。对于测试 `exec()` 行为很有用。

- `--caps-set`



将当前进程能力设置为 `cap-set` 指定的能力。其中 `cap-set` 是根据 `cap_from_text(3)` 定义的能力状态的文本表示。

- `--drop=cap-list`

  从当前边界集（bounding set）中移除列出的能力。这些能力是 `cap_from_name(3)` 识别的逗号分隔能力列表。使用此功能要求 `capsh` 程序在 fact有效能力集中具有 `CAP_SEPCAP` 权限运行。

- `--inh=cap-list`

  将当前进程的可继承能力设置为与逗号分隔列表相同的项。为了使此操作成功，当前进程应该已经在当前可继承能力集和允许能力集的并集中拥有这些能力中的每一个，或者 `capsh` 程序在其有效能力集中具有 `CAP_SEPCAP` 权限。

- `--user=username`

  假设指定用户的身份。即，通过 `getpwuid(3)` 查找用户的 `uid` 和 `gid`，通过 `getgrouplist(3)` 查找其组组成并设置它们所有。

- `--uid=id`

  使用 `setuid(2)` 系统调用强制所有 `uid` 值等于 `id`。

- `--gid=id`

  使用 `setgid(2)` 系统调用强制所有 `gid` 值等于 `id`。

- `--groups=<id-list>`

  将补充组设置为提供的数值列表。组通过 `setgroups(2)` 系统调用设置。

- `--keep=<0|1>`

  在非纯能力模式下，内核为超级用户提供宽松的权限。然而，超级用户将 `uid` 更改某些较低的用户是正常的，然后能力会丢失。对于这些情况，内核允许进程在执行 `setuid(2)` 系统调用后保留其能力。此功能被称为 keep-caps 支持。使用此脚本激活它的方法是使用参数。将值设置为 1 将导致 keep-caps 激活。设置为 0 将导致 keep-caps 对当前进程失效。在所有情况下，当执行 `exec()` 时，keep-caps 都会失效。参见 `--secbits` 禁用此功能的方法。

- `--secbits=N`

XXX - 需要记录此功能。

- `--chroot=path`

  执行 `chroot(2)` 系统调用，新的根目录 (`/`) 等于 `path`。此操作需要 `CAP_SYS_CHROOT` 效力。

- `--forkfor=sec`

- `--killit=sig`

- `--decode=N`

这是一个方便功能。如果你查看 `/proc/1/status`，会有一些如下形式的相关字段：

| CapInh: 0000000000000000 | CapPrm: fffffffffffffff |

| CapEff: fffffffffffffff | CapBnd: fffffffffffffff |

此选项提供了一种快速解码以此形式表示的能力向量的方法。例如，有效能力集中缺失的能力是 `0x0100`。通过运行：

```
capsh --decode=0x0100
```

我们观察到缺失的能力是：`cap_set`。

- `--supports=XXX`

  随着内核的演进，增加了更多的能力。此选项可以用于验证系统上是否存在能力。例如，在内核 2.6.27 上运行时，`--supports=cap_syslog` 会导致 `capsh` 以状态 1 退出。然而，在内核 2.6.38 上运行时，它将成功退出。

# 退出状态

执行成功后，工具以状态 0 退出。发生错误后，工具以状态 1 退出。

### 作者

由 Andrew G. Morgan <morgan@kernel.org> 编写。

# 报告错误

请向作者报告错误。

# 另另

`libcap(3)`, `getcap(8)`, `setcap(8)`。

## 名称

`capsh` - 能力 shell 包装器

### 概要

`capsh [OPTION]...`

### 描述

可以使用此工具探索和限制 Linux 能力的支持和使用。该工具为某些类型的能力测试和环境创建提供了方便的包装器。它提供了一些有助于总结能力状态的调试功能。

### 选项

该工具接受多个可选参数，并按照提供的顺序对其进行操作。它们如下：

- `--print`

  显示当前能力和相关状态。

- `--args`

  带有尾随参数执行 `/bin/bash`。注意，你可以使用 `-c` ‘要执行的命令’执行特定命令。

- `-- ===`

  使用剩余参数再次执行 `capsh`。对于测试 `exec()` 行为很有用。

- `--caps-set`

  将当前进程能力设置为 `cap-set` 指定的能力。其中 `cap-set` 是根据 `cap_from_text(3)` 定义的能力状态的文本表示。

- `--drop=cap-list`

  从当前边界集中移除列出的能力。这些能力是 `cap_from_name(3)` 识别的逗号分隔能力列表。使用此功能要求 `capsh` 程序在有效能力集中具有 `CAP_SEPCAP` 权限运行。

- `--inh=cap-list`

  将当前进程的可继承能力设置为与逗号分隔列表相同的项。为了使此操作成功，当前进程应该已经在当前可继承能力集和允许能力集的并集中拥有这些能力中的每一个，或者 `capsh` 程序在其有效能力集中具有 `CAP_SEPCAP` 权限。

- `--user=username`

  假设指定用户的身份。即，通过 `getpwuid(3)` 查找用户的 `uid` 和 `gid`，通过 `getgrouplist(3)` 查找其组组成并设置它们所有。

- `--uid=id`

  使用 `setuid(2)` 系统调用强制所有 `uid` 值等于 `id`。

- `--gid=id`

  使用 `setgid(2)` 系统调用强制所有 `gid` 值等于 `id`。

- `--groups=<id-list>`

  将补充组设置为提供的数值列表。组通过 `setgroups(2)` 系统调用设置。

- `--keep=<0|1>`

  在非纯能力模式下，内核为超级用户提供宽松的权限。然而，超级用户将 `uid` 更改某些较低的用户是正常的，然后能力会丢失。对于这些情况，内核允许进程在执行 `setuid(2)` 系统调用后保留其能力。此功能被称为 keep-caps 支持。使用此脚本激活它的方法是使用参数。将值设置为 1 将导致 keep-caps 激活。设置为 0 将导致 keep-caps 对当前进程失效。在所有情况下，当执行 `exec()` 时，keep-caps 都会失效。参见 `--secbits` 禁用此功能的方法。

- `--secbits=N`

XXX - 需要记录此功能。

- `--chroot=path`

  执行 `chroot(2)` 系统调用，新的根目录 (`/`) 等于 `path`。此操作需要 `CAP_SYS_CHROOT` 效力。

- `--forkfor=sec`

- `--killit=sig`

- `--decode=N`

这是一个方便功能。如果你查看 `/proc/1/status`，会有一些如下形式的相关字段：

| CapInh: 0000000000000000 | CapPrm: fffffffffffffff |

| CapEff: fffffffffffffff | CapBnd: fffffffffffffff |

此选项提供了一种快速解码以此形式表示的能力向量的方法。例如，有效能力集中缺失的能力是 `0x0100`。通过运行：

```
capsh --decode=0x0100
```

我们观察到缺失的能力是：`cap_setpcap`。

- `--supports=XXX`

  随着内核的演进，增加了更多的能力。此选项可以用于验证系统上是否存在能力。例如，在内核 2.6.27 上运行时，`--supports=cap_syslog` 会导致 `capsh` 以状态 1 退出。然而，在内核 2.6.38 上运行时，它将成功退出。

# 退出状态

执行成功后，工具以状态 0 退出。发生错误后，工具以状态 1 退出。

### 作者

由 Andrew G. Morgan <morgan@kernel.org> 编写。

# 报告错误

请向作者报告错误。

# 另另

`libcap(3)`, `getcap(8)`, `setcap(8)`。

## 名称

`captoinfo` - 将 termcap 转换为 terminfo

### 概要

`captoinfo [-v] [-w] file`

### 描述

`captoinfo` 在文件中查找 termcap 能力。对于找到的每项，等效的 terminfo写入标准输出。如果环境变量 `TERM` 未设置，则：

- `-v`

  打印版本。

- `-w`

  将输出更改为字符。

### 文件

`/usr/share/terminfo`

# 非标准能力的翻译

某些非标准能力将被 `captoinfo` 转换为标准的 (Svr4/XSI) terminfo。每当条目中出现单行能力时，它们将自动组成 `acsc` 字符串。双行能力和 `GG` 将被警告丢弃。

| Nonstd | Terminfo |

| :--- | :--- |

| BO | 反转模式 (reverse_mode) |

| CI | 光标隐藏 (cursor_invisible) |



| `CV` | 光标正常 (`cursor_normal`) |
| `DS` | 变暗模式 (`dim_mode`) |
| `EE` | 退出属性模式 (`exit_attribute_mode`) |
| `FL` | 标签开启 (`label_on`) |
| `LO` | 标签关闭 (`label_off`) |
| `XS` | 安全模式 (`secure_mode`) |
| `GE` | 字符集模式 (`exit_charset_mode`) |
| `GS` | 替代字符集模式 (`alt_charset_mode`) |
| `HM` | 首页 (`home`) |
| `LD` | 下载 (`dl`) |
| `PD` | 页面 (`page`) |
| `PN` | 打印机关闭 (`prtr_off`) |
| `PS` | 页面 (`page`) |
| `RT` | `kent` |
| `UP` | `kuu1` |
| `KA` | `f10` |
| `KB` | `f11` |
| `KC` | `f12` |
| `KD` | `f13` |
| `KE` | `f14` |
| `KF` | `f15` |
| `BC` | 背景 (`background`) |
| `FC` | 前景 (`foreground`) |
| `HS` | 变暗模式 (`dim_mode`) |

`termcap` 也曾用于一组表单绘制的扩展能力，旨在利用 IBM PC 高图形。它们如下：

# 图形

- `G2` 左上
- `G3` 左下
- `G1` 右上
- `G4` 右下
- `GR` 向右
- `GL` 向左
- `GU` 向上
- `GD` 向下
- `GH` 水平线
- `GV` 垂直线
- `GC` 交叉
- `G6` 左上
- `G7` 左下
- `G5` 右上
- `G8` 右下
- `Gr` tee 向右
- `Gr` tee 向左
- `Gu` tee 向上
- `Gd` tee 向下
- `Gh` 水平线
- `Gv` 垂直线
`Gc` 交叉
`GG` 魔术 Cookie 计数

IBM 的 AIX 有一个自自 SVr1 `terminfo` 的设施，但与 SVr4 格式不兼容。以下 AIX 扩展被自动翻译：

`IBM XSI`

```
ksel kslt
ktab kbct
font0 s0ds
font1 s1ds
font2 s2ds
font3 s3ds
```

此外，AIX `box1` 能力将自动转换为 `acsc` 字符串。

Hewlett-Packard 的 `terminfo` 库支持两个非标准的 `terminfo` 功能：`meml`（内存锁定）和 `memu`（内存解锁）。这些功能将在带有警告消息的情况下被丢弃。

# 注意事项

此实用程序实际上是 `tic(1M)` 的链接，在 `-I` 模式下运行。你可以使用其他的 `tic` 选项，例如 `-f` 和 `-x`。

`trace` 与 SVr4 的不同。在 SVr4 下，不是在 `-v` 后面跟随跟踪级别 `n`，而是重复它 `n` 次。

### 参见

`infocmp(1M)`, `curses(3X)`, `terminfo(5)`

本说明档描述了 `ncurses` 5.9 版本（补丁 20150214）。

### 作者

Eric S. Raymond <esr@snark.thyrsus.com> 和 Thomas E. Dickey <dickey@invisible-island.net>

# card_eventmgr

## 名称

`card_eventmgr` - PCSC-Lite 事件管理器

# 语法

```
card_eventmgr [debug] [[no]daemon] [timeout=<msecs>] [config_file=<filename>] [kill] [pidfile=<pidfile> ]
```

### 描述

`card_eventmgr` 是一个智能卡监控工具，用于监听读卡器状态并在多个事件上触发操作。`card_eventmgr` 可用于多种操作，例如在移除卡片时锁定屏幕。

支持三种事件：插卡、拔卡以及移除卡片后的超时。具体操作均在配置文件中指定。

### 选项

`debug`

启用调试输出。

`[no]daemon`

如果指定 `daemon` 则在后台运行，如果指定 `nodaemon` 则在前台运行（默认）。如果未设置 `debug`，程序将从 tty 分离。

`timeout=<msecs>`

设置毫秒级轮询超时时间。默认值为 1000（1 秒）。

`config_file=<configuration file>`

设置配置文件。默认值为 `/etc/pam_pkcs11/card_eventmgr.conf`。

`pidfile=<pidfile>`

将 `card_eventmgr` 的 ID (`pid`) 存储在文件 `pidfile` 中。

`kill`

从 `pidfile` 读取进程 ID 并杀死该进程。必须使用参数 `pidfile=<pidfile>` 来使用 `kill`。

### 文件

```
/etc/pam_pkcs11/card_eventmgr.conf
```

## 示例

以标准方式运行此程序：

`card_eventmgr`

或者，你可以指定选项：

```
card_eventmgr debug nodaemon timeout=500
config_file=$HOME/.card_eventmgr.conf
```

如果你想在 X11 会话中自动启动和停止 `card_eventmgr`，可以创建一个包含以下内容的 `~/.xsession` 文件：# 启动卡片自动锁定

```
card_eventmgr pidfile=$HOME/.card_eventmgr.pid
```

```
# 启动 Gnome 或其他 /usr/bin/x-session-manager
```

```
# 杀死自动自动锁定 card_eventmgr kill pidfile=$HOME/.card_eventmgr.pid
```

# Bug

某些应用程序（如 `xscreensaver-command`）可能会由于外部事件失败（例如：尝试解锁一个未锁会话）。在这种情况下，命令会错误地返回错误代码。

### 作者

Juan Antonio Martinez <jonsito@teleleline.es> Ludovic Rousseau

<ludovic.rousseauau@free.fr>

### 参见

`pam_pkcs11(8)`, `pkcs11_eventmgr(1)`, `README.eventmgr`, `PAM-PKCS11` 用户手册

`cat` - 合并文件并打印到标准输出

# 概览

`cat [OPTION]... [FILE]...`

### 描述

将 `FILE(s)` 合并到标准输出。

在没有 `FILE` 或当 `FILE` 为 `-` 时，从标准输入读取。

- `-A,--show-all`

等同于 `-vET`

- `-b,--number-nonblank`

对非空输出行编号，覆盖 `-n`

- `-e`

等同于 `-VE`

- `-E,--show-ends`

在每行末尾显示 `$`

- `-n,--number`

所有输出行编号

- `-s,--squeeze-blank`

抑制重复的空输出行

- `-t`

等同于 `-vT`

- `-T,--show-tabs`

将 TAB 字符显示为 `^I`

- `-u`

（忽略）

- `-v,--show-nonprinting`

使用 `^` 和 `M-` 表示，LFD 和 TAB 除外

`--help`

显示此帮助信息并退出

`--version`

输出版本信息并退出

## 示例

`cat f -g`

输出 `f` 的内容，然后标准输入，然后 `g` 的内容。

`cat`

将标准输入复制到标准输出。

### 作者

由 Torbjorn Granlund 和 Richard M. Stallman 编写。

# 报告 Bug

GNU `coreutils` 在线帮助：<http://www.gnu.org/software/coreutils/> 向 <http://translationproject.org/team/> 报告 `cat` 翻译 bug

# 版权

Copyright © 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL 版本 3 或更高版本 <http://gnu.org/licenses/gpl.html>。这是免费软件：你可以自由地更改和分发它。在法律允许的范围内不提供任何保证。

### 参见

`tac(1)`

完整文档见：<http://www.gnu.org/software/coreutils/cat> 或通过本地信息可用：info ‘(coreutils) cat invocation'

## 名称

`cd-it8` - 颜色管理器测试工具

# 概览

```
cd-it8 [ --verbose ]
```

### 描述

本说明档简要描述了 `cd-it8` 命令。

`cd-it8` 允许管理员创建 IT8 文件，如 `*.ti3, .ccmx*`。

### 选项

此程序带有以双连字符 ('') 开头的长选项。下所示。

`-help`

显示帮助。

### 作者

本说明档由 Richard Hughes <richard@ghsie.com> 编写。



## 名称

`cd-profile` - 颜色配置文件创建

## 概览

```
cd-profile [profile ]
```

### 描述

本说明档简要描述了 `cd-it8` 命令。

`cd-it8` 允许管理员创建 IT8 文件，如 `*.ti3`, `.ccmx`。

### 选项

此程序带有以双连字符 (`--`) 开头的长选项。下所示。

+   `-help`

显示总结。

`-description`

设置描述。

`-copyright`

设置版权。

`-model`

设置型号。

`-manufacturer`

设置制造商。

`-output`

指定输出文件名。

`-nc-prefix`（可选）

指定命名前缀。

`-nc-suffix`（可选）

指定命名颜色后缀。

### 作者

本说明档由 Richard Hughes <richard@ghsie.com> 编写。

## 名称

`cd-drive` - 显示 CD-ROM 驱动器

## 概览

```
cd-drive [OPTION...]
```

### 描述

- `-d,--debug=INT`

设置调试级别

- `-i,--cdrom-device=[DEVICE]`

仅显示关于 CD-ROM 设备的信息

- `-q,--quiet`

不产生警告输出

- `-V,--version`

显示版本信息并退出

帮助选项：

- `?,--help`

显示帮助信息

`-usage`

显示用法

### 作者

Rocky Bernstein@gnu.org

## 版权

Copyright © 2003-2005, 2007-2008, 2011-2013 R. Bernstein 这是免费软件；请查看源代码条件。没有任何保证，甚至包括商品性或特定用途的适用性。驱动程序：GNU/Linux ioctl 和 MMC 驱动；cdrdao (TOC) 磁盘镜像驱动程序；bin/cuesheet 磁盘镜像驱动程序；Nero NRG 磁盘镜像驱动程序默认 CD-ROM 设备：`/dev/cdrom`

### 参见

`cd-info(1)` 用于获取 CD-ROM 内部 CD 的信息

## 名称

`cd-fix-profile` - 颜色管理器测试工具

## 概览

```
cd-fix-profile [ --verbose ]
```

### 描述

本说明档简要描述了 `cd-fix-profile` 命令。

`cd-fix-profile` 允许管理员修改并修复系统上的 ICC 配置文件。

程序还会修复配置文件中常见的错误。

### 作者

本手册页由 Richard Hughes <richard@hughsie.com> 编写。

`cd-info` - 显示 CD 或 CD 镜像的信息

### 摘要

```
cd-info [OPTION...]
```

### 描述

`-a, --access-mode=STRING`

设置 CD 访问模式

`-d, --debug=INT`

设置调试级别为 LEVEL

`-T, --no-tracks`

不显示轨道信息

`-A, --no-analyze`

不显示文件大小分析

`--no-cddb`

此选项无效，因为此程序是

`-P, --cddb-port=INT`

启用 CDDB 并设置端口号

`-H, --cddb-http`

`--cddb-server=STRING`

`--cddb-cache=STRING`

`--cddb-email=STRING`

`--no-cddb-cache`

`--no-cddb-timeout=INT`

`--no-device-info`

不显示设备信息，只显示 CD 信息

`--no-disc-mode`

不显示盘模式信息

`--dvd`

如果发现 DVD，则尝试提供 DVD 信息。

`-v, --no-vcd`

不查找视频 CD 信息 - 对于此版本，该选项始终被开启

`-I, --no-ioctl`

不显示 ioctl() 镜像

`-b, --bin-file=[FILE]`

将 "bin" CD-ROM 磁盘镜像文件设置为源

`-c, --cue-file=[FILE]`

将 "cue" CD-ROM 磁盘镜像文件设置为源

`-N, --nrg-file=[FILE]`

将 Nero CD-ROM 磁盘镜像文件设置为源

`-t, --toc-file=[FILE]`

将 cdrdao CD-ROM 磁盘镜像文件作为源

`-i, --input=[FILE]`

设置源并判断是“bin”镜像还是设备

`-iso9660`

打印任何 ISO-9660 文件系统的目录内容

`-C, --cdrom-device=[DEVICE]`

将 CD-ROM 设备设置为源

- `-i, --list-drives`

列出 CD 驱动器列表

- `-no-header`

不显示页眉和版权信息（用于回归测试）

- `-no-joliet`

不使用 Joliet 扩展

- `-no-rock-ridge`

不使用 Rock-Ridge 扩展信息

- `-no-xa`

不使用 XA 扩展信息

- `-q, --quiet`

不产生警告输出

- `-V, --version`

显示版本和版权信息并退出

# 选项：

- `-?,--help`

显示此帮助消息

- `--usage`

显示简要用法消息

### 作者

Rocky Bernstein rocky@gnu.org，基于 Gerd Knorr <kraxel@bytesex.org> 和 Heiko Eissfeldt <heiko@hexco.de> 的 cdinfo 程序编写。

## 版权所有

Copyright © 2003-2005, 2007-2008, 2011-2013 R. Bernstein 这是一个免费软件；复制条件请参见源代码。不提供任何保证；即使对于适用性或特定用途的适用性保证。拥有驱动：GNU/Linux ioctl 和 MMC 驱动；拥有驱动：cdrdao (TOC) 磁盘镜像驱动；拥有驱动：bin/cuesheet 磁盘镜像驱动；拥有驱动：Nero NRG 磁盘镜像驱动。默认 CD-ROM 设备：`/dev/cdrom`

### 参见

`cd-drive(1)` 查看 CD-ROM 特性；`iso-info(1)` 查看关于 ISO-9660 镜像的信息。

# `cd-paranoia`

## 名称

`cd-paranoia` - 9.8 (通过 libcdio 发布 Paranoia 版本 III) - 一个音频 CD 读取工具，包含额外的数据验证功能。

### 摘要

```
cd-paranoia [options] span [outfile]
```

### 描述

`cd-paranoia` 从支持 CDDA 的 CD-ROM 驱动器中检索音频轨道。数据可以保存到文件，或以 WAV、AIFF、AIFF-C 或原始格式定向到标准输出。支持大多数 ATAPI、SCSI 以及多种专用 CD-ROM 驱动；`cd-paranoia` 可以判断目标驱动器是否支持 CDDA。

除了简单的读取，`cd-paranoia` 还增加了额外的强化数据验证、同步、错误处理和划痕重建能力。

此版本使用 `libcdio` 库与 CD-ROM 驱动器交互。然而，抖动（jitter）和纠错与 Xiph 的 cdparanoia 使用的相同。

### 选项

`-A--analyze-drive`

对驱动器缓存、定时和读取行为进行完整分析；验证 `cd-paranoia` 是否正确对特定驱动器的缓存和读取行为进行建模。

`-v--verbose`

在自动感和读取过程中输出极其详尽的信息。适用于设置和调试。

`-q--quiet`

在读取过程中不打印任何进度或错误信息。

`-e--stderr-progress`

强制将进度信息输出到 stderr（用于封装脚本）。

`-V--version`

打印程序版本并退出。

`-Q--query`

执行 CD-ROM 驱动器自动感、查询并打印 CD-ROM 目录表，然后退出。

`-h--help`

打印 `cd-paranoia` 用法和选项的简要摘要。

`-l--log-summary-file`

将结果摘要保存到文件。

`-L--log-debug file`

将详细的设备自动感和调试输出保存到文件。

`-p--output-raw`

以无头数据的原始 16 位 PCM 格式输出，并按字节顺序交错采样。如需强制使用小端或大端序，请使用下文的 `-r` 或 `-R`。

`-r--output-raw-little-endian`

以无头数据的原始 16 位 PCM 格式输出，按小端序交错采样。

`-R--output-raw-big-endian`

以无头数据的原始 16 位 PCM 格式输出，按大端序交错采样。

`-w--output-wav`

以 MicroSoft RIFF WAV 格式输出（注意 WAV 数据始终为小端序）。

`-f--output-aiff`

以 Apple AIFF 格式输出（注意 AIFC 数据始终为大端序）。

`-f--output-aiff`

以 Apple AIFF 格式输出（注意 AIFC 数据始终为大端序）。

- `-B--batch`

某些 CDDA 驱动器报告轨道起始，但输出轨道边界。



# 选项

- `-c --force-cdrom-little-endian`

某些 CDDA 驱动器报告轨道起始，`cd-paranoia` 将对小端风格设备进行偏移。

- `-C --force-cdrom-big-endian`

使用此选项强制驱动器偏移采样位置指定的量。

- `-O --sample-offset`

某些 CD-ROM/CD-R 在读取时会向位置一个偏移。这通常在读取时约为 500-700 个采样（约 1/75 秒）。因此当 `cd-paranoia` 查询特定扇区时，接收到的可能不是精确，而是偏移了某些。

使用此选项强制驱动器偏移采样位置指定的量。这可以手动偏移整个光片的轨道边界。

- `-d --force-device`

某些 ATAPI, SCSI 会向位置一个偏移（取决于支持情况）。

- `-g --force-generic-device`

某些 ATAPI, SCSI 会向位置一个偏移。

- `-n --force-cdrom-n`

使用此选项强制偏移。

- `-S --force-read-speed`

使用此选项设置读取速率（取决于支持情况）。

- `-T --toc-bias`

某些 CDDA 驱动器报告轨道起始，但输出轨道边界。

- `-x --test-flags-mask`

模拟 CD 读取错误。这用于回归测试，但其他用途可能是观察 CD-ROM 在（模拟的）光盘劣化下的性能。

`0x10` - 模拟欠道读取

# 输出表情

`:-)` 正常运行，低抖动/无抖动

`:-|` 正常运行，有显著抖动

`-/-` 读取漂移

`:-P` 原子读取操作中未报告的流媒体丢失

`8-|` 在重读时在相同点发现读取问题；难以修复

`:-0` SCSI/ATAPI 传输错误

`:-( `检测到划痕

`:-( `放弃尝试修复

`8-X` 由于已知的不可修复错误，读取已中止

`:^D` 完成提取

# 进度条符号

`<space>`

`+`   - 无需修复

`+`   - 需要纠正抖动

`+`   + 读取中存在未报告的流媒体丢失/其他错误

`+`   ! 在第 1 阶段修复后发现错误；驱动器在多次重读中产生相同的错误，`cd-paranoia` 难以检测到这些错误。

`+`   e SCSI/ATAPI 传输错误（已修复）

`+`   V 未修复错误/跳过

# 跨度参数 (SPAN ARGUMENT)

`span` 参数指定要读取的轨道、多个轨道或轨道子部分。该 `span` 参数是必须的。注意：除非 `span` 是简单的数字，否则通常建议对 `span` 参数加引号以防止其受 shell 影响。

`span` 偏移量（`offset`）可以是简单的轨道编号，也可以是偏移/跨度指定。偏移/span 的语法遵循大致形式：

```
1[[ww:xx:yy-zz]-2[aa:bb:cc:dd]]
```

在这里，`1` 和 `2` 是轨道编号；括号中的数字提供了特定轨道内更细粒度的偏移量。`[aa:bb:cc:dd]` 采用小时/分钟/秒/扇区的格式。零字段不需要指定：`[::20]`, `[-20]`, `[20]`, `[20.]` 等将被被解释为二十秒，`[10:1]` 将被解释为十分，`[..30]` 将被解释为三十秒（每秒 75 个轨道）。

当仅提供单个偏移量时，它被解释为起始偏移量，提取将持续到轨道末尾。如果单个偏移量前后有连字符，则隐含的缺失偏移量分别被取为光片的开始或结束。因此：

+   `1:[20.35]`

- 指定从轨道 1 的第 20 秒第 35 扇提取到轨道 1 的末尾。

+   `1:[20.35]-`

- 指定从 `1[20.35]` 提取到光片的结束

+   `-2`

- 指定从光片的开始（并包含）轨道 2 开始

+   `-2:[30.35]`

- 指定从光片的开始提取到 `2:[30.35]`

+   `2-4`

- 指定从轨道 2 的开始提取到轨道 4 的结束。

再次，不要忘记在 shell 中保护方括号和连字符。

## 示例

一些受 shell 保护的示例：

仅对驱动器进行穷尽搜索并对自动感应进行完整报告：

```
cd-paranoia -VSQ
```

提取整张光片，并将每个轨道放在单独的文件中：

```
cd-paranoia -B
```

从轨道 1、时间 0:30.12 提取到 1:10.00：

```
cd-paranoia "1[:30.12]-1[1:10]"
```

从光片的开始提取到轨道 3：

```
cd-paranoia — "3"
```

上面的“—”是为了区分“-3”和选项标记。

## 输出

输出文件参数是可选的；如果未指定，`cd-paranoia` 将将样本输出到 `cdda.wav`、`cdda.aifc` 或 `cdda.raw` 之一，取决于是否使用了 `-w`、`-a`、`-r` 或 `-R`（`-w` 是隐含默认值）。`-` 的输出文件参数指定标准输出。

## 致谢

`cd-paranoia` 提供了大量的贡献。Heikofeldt 贡献了 SCSI 传输方面的知识。

Rocky 贡献。

# 版权

Copyright © 2003-2005, 2007, 2011-2013 R。这是免费软件，请参源代码中的条件。不提供任何商业性担保。

# 另请

`monty@xiph.org` 贡献了大量的代码。Rocky `<rocky@gnu.org>`

`cd-paranoia` 的主页可以访问：`http://www.xiph.org`

### 作者

Rocky `<rocky@gnu.org>`

# 版权

Copyright © 2003-2005, 2007, 2011-2013 R。这是免费软件，请参源代码中的条件。不提供任何商业性担保。

# 另请

`cd-info(1)` 关于 CD 的信息；`cd-drive(1)` 关于 CD-ROM；`iso-read(1)` 关于 ISO。

## 名称

`certutil` - 管理 NSS 数据库中的密钥和证书

# 状态

此文档仍在完善中

# 命令选项和参数

运行 `certutil` 总是需要且仅需要命令选项来指定证书操作。每个命令选项可以接受零或多个参数。命令选项 `-H` 将列出所有命令选项及其相关参数。

### 命令选项

`-A` 将现有证书添加到证书数据库。证书数据库应该已经存在；如果没有，此命令选项将默认初始化。

`-B` 从指定的批文件运行一系列命令。这需要 `-i` 参数。

`-C` 从二进制证书请求文件创建新的二进制证书文件。使用 `-i` 参数指定证书请求文件。如果未使用此参数，`certutil` 会提示文件名。

`-D` 从证书数据库中删除证书。

`-E` 向证书数据库添加电子邮件证书。

`-F` 从密钥数据库中删除私钥。使用 `-d` 参数指定要删除的密钥。使用 `-k` 参数显式指定从哪个数据库删除密钥。

当删除密钥时，请确保也通过 `-D` 从证书数据库中删除与这些密钥相关的证书。在某些情况下，智能卡中仅从密钥对中删除了私钥。你可以使用命令 `certutil - K -h tokenname` 显示公钥。

`-G`

在密钥数据库中生成一组新的公钥和私钥对。密钥数据库应该已经存在；如果不存在，此命令选项将默认初始化一个。智能卡只能存储一个密钥对。如果你为此类设备创建了新的密钥对，之前的密钥对将被覆盖。

## `-H`

显示命令选项和参数的列表。

## `-K`

列出密钥数据库中密钥的 ID。密钥 ID 是 RSA 密钥的模或 DSA 密钥的 `publicValue`。ID 以十六进制形式显示（不显示“0x”）。

## `-L`

列出证书数据库中的所有证书，或显示指定命名证书的信息。使用 `-h tokenname` 参数指定特定硬件或软件令牌上的证书数据库。

## `-M`

使用 `-t` 参数的值修改证书的信任属性。

## `-N`

创建新的证书数据库和密钥数据库。

## `-O`

打印证书链。

## `-R`

创建一个证书请求文件，该文件可以提交给证书颁发机构 (`CA`) 处理成最终证书。除非指定了 `-o output-file` 参数，否则输出默认到标准输出。使用 `-a` 参数指定 ASCII 输出。

## `-S`

创建一个单个证书并将其添加到证书数据库中。

## `-T`

重置密钥数据库或令牌。

## `-U`

列出所有可用模块或打印单个命名模块。

## `-V`

检查证书及其属性的有效性。

## `-W`

更改密钥数据库的密码。

## `-merge`

将两个数据库合并为一个。

## `-upgrade`

升级旧数据库并合并到新数据库。这用于将旧的 NSS 数据库（`cert8.db` 和 `key3.db`）迁移到新的 SQLite 数据库（`cert9.db` 和 `key4.db`）。

## Arguments

参数修改命令选项，通常为小写字母、数字或符号。

### `-a`

使用 ASCII 格式或允许在输入或输出中使用 ASCII 格式。此格式遵循 RFC 1113。对于证书请求，除非被重定向，否则 ASCII 输出默认到标准输出。

### `-b validity-time`



指定证书必须有效的时间。当使用 `-V` 选项检查证书有效性时，`validity-time` 参数的格式为 `YYYYMMDDHHMMSS[+HHMM][-Z]`，允许相对于有效结束时间设置偏移量。指定秒 `SS` 是可选的。当指定明确时间时，在术语末尾附近使用 `Z`，即 `YYYYMMDDHHMMSSZ`。当指定偏移时间时，使用 `YYYYMMDDHHMMSS+HHMM` 或 `YYYYMMDDHHMMSS-HHMM` 分别加或减时间。

如果不使用此项，有效性检查默认使用当前系统。

### `-c` issuer

识别新证书派生真实性的 CA 证书。使用 CA 证书的准确名称或别名，或使用 CA 的电子邮件地址。如果发行者字符串包含空格，请用引号将其括起来。

### `-d` [prefix]directory

指定包含证书和密钥数据库文件的目录。`certutil` 支持两种数据库：旧版安全数据库（`cert8.db`、`key3.db` 和 `secmod.db`）和新的 SQLite 数据库（`cert9.db`、`key4.db` 和 `pkcs11.txt`）。

NSS 识别以下前缀：

- `sql:` 请求较新的数据库
- `dbm:` 请求旧数据库

如果未指定前缀，默认类型从 `NSS_DEFAULT_DB_TYPE` 获取。如果未设置 `NSS_DEFAULT_DB_TYPE`，则默认为 `dbm:`。

### `-dump-ext-val` OID

对于单个证书，打印扩展 `OID` 的二进制 DER 编码。

### `-e`

在验证证书的过程中检查证书的签名。

### `-email` email-address

指定要列出的证书的电子邮件地址。配合 `-L` 命令选项使用。

### `-extGenericOID:critical-flag:filename,[OID:critical-flag:filename]...`

通过从外部文件加载编码，添加 `certutil` 尚无法编码的一个或多个扩展。

`OID`（示例）：`1.2.3.4`

`critical-flag`: 关键或非关键

`filename`: 包含编码扩展的文件完整路径

### `-f` password-file

指定一个自动提供密码以包含在证书或访问证书数据库的文件。这是一个包含一个密码的纯文本文件。请确保防止对该文件的未经访问。

### `-g` keysize

设置生成新的公私钥对时使用的密钥大小。最小为 512 位，最大为 16384 位。默认为 2048 位。允许最小和最大之间的任何大小。

### `-h` tokenname

指定要使用或操作的令牌名称。如果未指定，默认令牌是内部数据库插槽。

### `-i` input_file

将输入文件传递给命令。根据命令选项，输入文件可以是特定的证书、证书请求文件或命令批处理文件。

### `-k` key-type-or-id

指定密钥的类型或特定 ID。有效的密钥类型选项有 `rsa`、`dsa`、`ec` 或 `all`。默认值为 `rsa`。指定密钥类型可以避免由重复名称引起的错误。给出密钥类型将生成新的密钥对；给出现有密钥的 ID 则将重用该密钥对（这是强制要求的）。

### `-l`

列出证书的名称（nickname）。

### `-m`

重置密钥数据库或令牌。

### `-n`

指定序列号。

### `-o`

输出证书链。

### `-p`

指定前缀。

### `-q`

指定 PQG 值。

### `-r`

显示证书的二进制 DER 编码。

### `-s`

识别主体所有者。

### `-t`

指定信任属性。

- `c` - 有效的 CA
- `T` - 受信的 CA（包含 `c`）
- `C` - 用于客户端认证的受信 CA（ssl 服务器）
- `u` - 用户

类别的属性代码之间用逗号分隔，整个属性集包含在引号内。例如：

`"TCu,Cu,Tu"`

使用 `-L` 选项查看证书数据库中当前的证书和信任属性列表。

### `-u` certusage

在使用 `-V` 选项验证证书时，指定要应用的用途上下文。

上下文如下：

- `C`（作为 SSL 客户端）
- `V`（作为 SSL 服务器）
- `L`（作为 SSL CA）
- `A`（作为任意 CA）
- `Y`（验证 CA）
- `S`（作为邮件签名者）
- `R`（作为邮件接收者）
- `O`（作为 OCSP 状态应答器）
- `J`（作为对象签名者）

### `-v` valid-months

设置新证书的有效期月数。有效期从当前系统时间开始，除非使用 `-w` 选项添加或减去了偏移量。如果未使用此参数，默认有效期为三个月。

### `-w` offset-months

设置证书有效期开始时间相对于当前系统时间的偏移量（单位为月）。适用于创建证书或将其添加到数据库时。使用整数表示偏移量，使用负号 `-` 表示负偏移量。如果未使用此参数，有效期从当前系统时间开始。有效期的长度通过 `-v` 参数设置。

### `-X`

强制以读写模式打开密钥和证书数据库。此选项通常与 `-U` 和 `-L` 命令选项配合使用。

### `-x`

使用 `certutil` 为正在创建或添加到数据库的证书生成签名，而不是从单独的 CA 获取签名。

### `-y` exp

设置为数据库生成新的 RSA 公钥时使用的备用指数值，该值代替默认值 `65537`。可选的备用值为 `3` 和 `17`。

### `-z` noise-file

从指定文件中读取种子值以生成新的私钥和公钥对。此参数可以使用硬件生成的种子值或通过键盘手动创建一个值。最小文件大小为 20 字节。

### `-Z` hashAlg

指定在使用 `-C`、`-S` 或 `-R` 命令选项时的哈希算法。可能的关键字：

`MD2`

`MD4`

`MD5`

`SHA1`

`SHA224`

`SHA256`

`SHA384`

`SHA512`

### `-0` SSO_password

在令牌上设置站点安全管理员密码。

### `-1` |keyUsage keyword,

在证书中设置 X.509 V3 证书类型扩展。有几个可用关键字：

- `digitalSignature`（数字签名）
- `nonRepudiation`（不可否认性）
- `keyEncipherment`（密钥加密）
- `dataEncipherment`（数据加密）
- `keyAgreement`（密钥协商）
- `certSigning`（证书签名）
- `crlSigning`（CRL 签名）
- `critical`（关键性）

### `-2`

为正在创建或添加到数据库的证书添加基本约束扩展。该扩展支持证书链验证过程。`certutil` 会提示选择要的证书约束扩展。

X.509 证书扩展在 RFC 5280 中有描述。

### `-3`

为正在创建或添加到数据库的证书添加机构密钥 ID 扩展。该扩展支持从与同一主题名称关联的多个证书中识别特定证书作为证书的正确颁发者。证书数据库工具将提示您选择机构密钥 ID 扩展。

X.509 证书扩展在 RFC 5280 中有描述。

### `-4`

为正在创建或添加到数据库的证书添加 CRL 分布点扩展。该扩展标识证书相关的证书撤销列表 `CRL` 的 URL。`certutil` 会提示输入 URL。

X.509 证书扩展在 RFC 5280 中有描述。

### `-5` |nsCertType keyword,keyword

为正在创建或添加到数据库的证书添加 X.509 V3 证书类型扩展。有多个可用关键字：

- `sslClient`
- `sslServer`
- `smime`
- `objectSigning`
- `sslICA`
- `smimeCA`
- `objectSigningCA`
- `critical`

X.509 证书扩展在 RFC 5280 中有描述。

### `-6` |extKeyUsage keyword,keyword

为正在创建或添加到数据库的证书添加扩展密钥用法。可选关键字包括：

- `serverAuth`（服务器认证）
- `clientAuth`（客户端认证）
- `codeSigning`（代码签名）
- `emailProtection`（邮件保护）
- `timeStamp`（时间戳）
- `ocResponder`（OCSP 应答器）
- `stepUp`（升级）
- `msTrustSign`（微软信任签名）
- `critical`（关键性）

X.509 证书扩展在 RFC 5280 中有描述。

### `-7` emailAddrs

为正在创建或添加到数据库的证书备用名称扩展添加用逗号分隔的电子邮件地址。备用名称扩展见 RFC 3280 的第 4.2.1 节。

### `-8` dns-names

为正在创建或添加到数据库的证书备用名称扩展添加用逗号分隔的 DNS 名称。备用名称扩展见 RFC 3280 的第 4.2.1 节。

### `-extAIA`

为证书添加机构信息访问扩展。X.509 证书扩展在 RFC 5280 中有描述。

### `-extSIA`

为证书添加主体信息访问扩展。X.509 证书扩展在 RFC 5280 中有描述。

### `-extCP`

为证书添加证书策略扩展。X.509 证书扩展在 RFC 5280 中有描述。

### `-extPM`

为证书添加策略映射扩展。X.509 证书扩展在 RFC 5280 中有描述。

### `-extPC`

为证书添加策略约束扩展。X.509 证书扩展在 RFC 5280 中有描述。

### `-extIA`

为证书添加禁止任何扩展。X.509 证书扩展在 RFC 5280 中有描述。



`-extSKID` 为证书添加主体密钥 ID 扩展。X.09 证书扩展在 RFC 5280 中有描述。

`-extNC` 为证书添加名称扩展。X.509 证书扩展在 RFC 5280 中有描述。

`-extSAN` 为证书添加主体备用名称扩展。X.509 证书扩展在 RFC 5280 中有描述。

`Corp,L=Mountain View,ST=California,C=US -d sql:$HOME/nssdb -p 650-555-0123 -a -o cert` Generating key. 正在生成密钥。这可能需要一些时间...

# 创建证书

有效的证书必须由受信任的 CA 发。这可以通过指定存储在证书数据库中的 CA 证书 (`-ce`) 来完成。如果没有 CA 密钥对，可以使用 `-S` 命令选项配合 `-x` 参数来创建自签名证书。

```
$ certutil -S -k rsa|||ec -cn certname -s subject [-c issuer [-x] -w
trustards -d sql:]directory [-m serial-number] [-v valid-months] [-w offset-months] [-p phone] [-1] [-2] [-3] [-4] [-5 keyword] [-6 keyword]
[-7 emailAddress] [-8 dns-names] [--extAIA] [--extSIA] [--extCP] ---
extextM] [--extPC] [--extIA]
```

一系列数字和 `--ext` 选项设置了证书扩展，当证书由 CA 生成时可以将这些扩展添加到证书中。将产生交互式提示。

在此示例中，创建一个自签名证书：

```
$ certutil -S -s "Example CA" -n my-ca-cert -x -t "C,C,C" -1 -2 -5 -
m 3650
```

为了简洁起见，省略了关于用法以及任何扩展是否关键的交互式提示和响应。

从这里开始，你可以引用自签名证书：

```
$ certutil -S -s "CN=My Server Cert" -n my-server-cert -c "my-ca-cert"
-t "u,u,u" -1 -5 -6 -8 -m 730
```

# 从证书请求生成证书

当创建证书请求时，可以使用该请求生成证书，然后引用证书颁发签名证书（`-c` 中指定的颁发者）。颁发证书必须在指定的目录下。

```
$ certutil -c issuer -i request-file -o output-file -m serial-number [-v valid-months] [-w offset-months] [-d sql:]directory [-1] [-2] [-3] [-4] [-5 keyword] [-7 emailAddress] [-8 dns-names]
```

例如：

```
$ certutil -c "my-ca-cert" -i /home/certs/cert.req -o cert.cer -m 730 -v 1 -d sql:$HOME/nssdb -5 nonRepudiation -6 clientAuth -7 client.com
```

# 列出证书

`-l` 命令列出数据库中的所有证书。需要目录路径 (`-d`)。与 `-l` 用时，返回单个证书的信息。`-n` 参数传递证书，而 `-a` 参数以 ASCII 格式打印证书：

```
$ certutil -d sql:/home/my/sharedndb -a my-ca
BEGIN CERTIFICATE...
END CERTIFICATE
```

为了人类可读的格式：

```
$ certutil -d sql:$HOME/nssdb -n my-ca Certificate: Data:
Version: 3 (0x2) Signature Algorithm: PKCS# Signature Algorithm: PKCS#1 SHA-1 With RSA Encryption Issuer: "CN=CA" Validity:
Before: Mar 13 19:10:29 2013 Not After: Jun 13 19:10:29 2013
Subject: "CN=CA" Subject Public Key Info: Public Key:
PKCS#1 RSA Public Key: Modulus:
9e:0a:ce:bf:37:22:50:85:54:b8:
```

证书；当 CA 颁发证书时，它本质上是在该证书上盖了它自己的指纹。`-O` 参数会打印证书的完整链，从初始 CA（根 CA）开始通过每一个中间 CA 直到实际的证书。例如，对于一个在链中包含两个 CA 的电子邮件证书：

```bash
$ certutil -sql:home/sharednssdb -0 -n "jsmith@example.com"
Built Object Token: Thawte Personal Freemail CA [E=personal-freemail@thaw.com,CN=Thawte Personal Freemail CA,OU=Certification
Services Division,O=Thawte Consulting,Cape Town,ST=Western Cape,C=ZA]
"Thawte Personal Freemail Issuing CA - Thawte Consulting" [CN=Thawte
Personal Freemail Issuing CA,O=Thawte Consulting (Pty) Ltd.,C=ZA] "
(null)[[E=jsmith@example.com,CN=Thawte Member
```

## 重置令牌

存储证书的设备——包括外部硬件设备和内部软件数据库——可以被清空并重复使用。此操作是在存储数据的设备上执行的，而不是直接在安全数据库上执行，因此可以通过令牌名称 (`-h`) 作为任何目录路径来引用位置。如果没有使用外部令牌，则默认值为内部令牌。

```bash
certutil -T -d [sql:]directory -h token-name -0 security-officer-password
```

许多网络有专门的人员处理安全令牌的变化（安全专员）。此人必须提供访问指定令牌的密码。例如：

```bash
$ certutil -T -d sql:home/my/sharednssdb -h netsm -0 secret
```

## 升级或合并安全数据库

许多网络或应用程序可能正在使用旧的 BerkeleyDB 版本的证书数据库 (`cert8.db`)。可以使用 `-upgrade-merge` 命令将数据库升级到新的 SQLite 版本数据库 (`cert9.db`)，或者使用 `-merge` 命令将现有数据库与新的 `cert9.db` 数据库合并。

`-upgrade-merge` 命令必须提供有关原始数据库的信息，并使用标准参数 (`-d`) 提供有关新数据库的信息。该命令还需要工具在升级过程和覆盖原始数据库时将用用的信息。

```bash
certutil --upgrade-merge -d [sql:]directory [-P dbprefix] --source-dir directory --source-prefix dbprefix serverapp --upgrade-id id --upgrade-token-name [-@ password-file]
```

例如：

```bash
$ certutil --upgrade-merge -d sql:home/my/sharednssdb --source-dir /opt/my-app/alias/ --source-prefix serverapp --upgrade-id 1 --upgrade-token-name internal
```

`-merge` 命令仅需要有关原始数据库位置的信息；由于它不改变数据库格式，因此可以在不执行中间步骤的情况下覆盖信息。

```bash
certutil --merge -d [sql]directory -P dbprefix --source-dir directory --source-prefix dbprefix [-@ password-file]
```

例如：

```bash
$ certutil --merge -d sql:/home/my/sharedndb --source-dir /opt/my-app/alias/ --source-prefix serverapp
```

## 从批文件运行 certutil 命令

可以使用 `-B` 命令选项从文本文件中顺序运行一系列命令。该选项的唯一参数是指定输入文件。

```bash
$ certutil -B -i /path/to/batch-file
```

## NSS 数据库类型



NSS 最初使用 BerkeleyDB 数据库存储安全信息。这些遗留数据库的最后版本为：

- `cert8.db` 用于证书
- `key3.db` 用于密钥
- `secmod.db` 用于 PKCS #11 模块信息

然而，BerkeleyDB 有性能限制，导致它无法被多个应用程序同时使用。NSS 具有灵活性，允许应用程序使用自己的独立数据库引擎，同时保持共享数据库并绕过访问问题。尽管如此，NSS 需要更多的灵活性来提供真正的共享安全数据库。

2009 年，NSS 引入了一组新的数据库，它们是 SQLite 数据库而不是 BerkeleyDB。这些新数据库提供了更高的可访问性和性能：

- `cert9.db` 用于证书
- `key4.db` 用于密钥

`pkcs11.txt` 是所有 PKCS #11 模块的列表，包含在安全数据库目录下的新子目录中

由于 SQLite 数据库设计为共享类型，因此它们是共享数据库类型。应首选共享数据库类型；给定的格式是为了向后兼容。

默认情况下，工具 (`certutil`, `pk12util`, `modutil`) 假设给定的安全数据库遵循常见的遗留类型。使用 SQLite 数据库必须通过对给定的安全目录使用前缀手动指定。例如：

```bash
$ certutil -L -d sql:/home/my/sharednssdb
```

要将共享数据库类型设置为工具的默认值，请将环境变量 `NSS_DEFAULT_DB_TYPE` 设置为：

```bash
export NSS_DEFAULT_DB_TYPE="sql"
```

可以将此行添加到 `~/.bashrc` 文件中以使更改永久生效。

大多数应用程序默认不共享数据库，但可以配置为使用共享数据库。例如，本文介绍了如何配置 Firefox 和 Thunderbird 使用新的共享数据库：

https://wiki.mozilla.org/NSS_Shared_DB_Howto

[注：提供的用于第 969-978 页的 OCR 文本是另一个关于 'chacl' 的手册页，已被追加或扫描错误。我将 'chacl' 内容作为文档流的一部分处理。]

# chacl

## 名称

`chacl` - 修改文件或目录的访问列表

## 概要

`chacl acl pathname...`
`chacl -b dacl pathname...`
`chacl -d dacl pathname...`
`chacl -R pathname...`
`chacl -D pathname...`
`chacl -B pathname...`
`chacl -l pathname...`
`chacl -r pathname...`

## 描述

`chacl` 是 IRIX 兼容命令，为那些在 XFS 或 IRIX 中熟悉其用法的用户维护。请参见下方的另另部分了解更符合（已撤回的）POSIX 1003.1 标准的工具，该标准描述了访问控制列表 (ACL)。

`chacl` 修改文件或目录的 ACL。指定的 ACL 应用于路径参数中的每个文件。

每个 ACL 是一个使用 `acl_from_text(3)` 例程解释的字符串。这些字符串由逗号分隔的句组成，每个句的形式为 `tag:name:perm`。其中 `tag` 可以是：

- `user` (or "`u`")

  表示该条目是用户 ACL 条目
- `group` (or "`g`")

  表示该条目是组 ACL 条目
- `other` (or "`o`")

  表示该条目是其他 ACL 条目
- `mask` (or "`m`")

  表示该条目是掩码 ACL 条目

`name` 是 ACL 条条目的用户或组名称字符串。用户或组 ACL 条目中的空名称表示文件的所有者或文件组。`perm` 是字符串 "`rwx`"，其中每个条目都可以被替换为 "`-`"，表示没有该类型的权限，例如 "`r-x`"`、`"-x"`、`"---"`。

## 选项

- `-b` 表示有两个 ACL 需要更改，第一个是文件访问 ACL，第二个是目录默认 ACL。
- `-d` 用于仅设置目录的默认 ACL。
- `-R` 仅移除文件访问 ACL。
- `-D` 仅移除目录默认 ACL。
- `-B` 移除所有 ACL。
- `-l` 列出与指定文件或目录关联的访问 ACL 以及可能存在的默认 ACL。此选项是在 XFS 移植到 Linux 期间的，不与 IRIX 兼容。
- `-r` 递归地为以路径(s) 为根的每个子树设置访问 ACL。此选项也是在 XFS 移植到 Linux 期间的，不与 IRIX 兼容。

## 示例

最少 ACL：

```
chacl u::rwx,g::r-x,o::r-- file
```

设置文件 ACL，使得文件所有者具有“rwx”权限，文件组具有读取和执行权限，而其他人对文件只有读取权限。

如果 ACL 不是所有者组的，则必须包含一个掩码项（mask），该项指定除文件所有者或所有者组以外的用户或组：

```
chacl u::rwx,g::r-x,o::r--,u:bob:r--,m::-x file1 file2
```

要将 `newdir` 的默认 ACL 和访问 ACL 设置为与 `olddir` 相同，你可以输入：

```
chacl -b `chacl -l olddir | sed -e 's/.[//' -e 's##/ #' -e 's/$]//'` newdir
```

## 注意

`chacl` 可以替换现有 ACL。要添加或删除条目，必须先执行 `chacl -1` 获取现有的 ACL，并使用输出结果构建 `chacl` 的参数。

更改文件的权限位将更改文件访问 ACL 设置（参见 `chmod(1)`）。然而，文件创建模式掩码（参见 `umask(1)`）不会影响使用目录默认 ACL 创建的文件的 ACL 设置。

ACL 是文件系统的扩展属性，因此因此通常不使用传统的归档工具进行归档或恢复。有关扩展属性的更多信息，请参见 `attr(5)`，关于 XFS 下备份这些属性的方法，请参见 `xfsdump(8)`。

## 参见

`getfacl(1)`, `setfacl(1)`, `chmod(1)`, `umask(1)`, `acl_from_text(3)`, `acl(5)`, `xfsdump(8)`

# chage

## 名称

`chage` - 修改用户密码过期信息

## 语法

```
chage [options] LOGIN
```

## 描述

`chage` 命令用于更改密码更改之间的天数以及最后一次更改密码的日期。系统使用此信息来确定用户何时必须更改其密码。

## 选项

适用于 `chage` 命令的选项有：

- `-d`, `—lastday LAST_DAY`

  设置自 1970 年 1 月 1 日以来最后一次更改密码的天数。日期也可以以 `YYYY-MM-DD` 格式（或你所在地区更常用的格式）表示。
- `-E`, `—expired EXPIRE_DATE`

  设置用户账户不再可以访问的日期，或自 1970 年 1 月 1 日以来的天数。日期也可以以 `YYYY-MM-DD` 格式（或你所在地区更常用的格式）表示。账户被锁的用户在重新使用系统之前必须联系系统管理员。

  将数字 `-1` 传递给 `EXPIRE_DATE` 将移除账户过期设置。
- `-h`, `—help`

  显示帮助信息并退出。
- `-I`, `—inactive INACTIVE`

  设置密码过期后账户锁定之前的非活动天数。`INACTIVE` 选项表示非活动状态的天数。账户被锁的用户在重新使用系统之前必须联系系统管理员。

  将数字 `-1` 传递给 `INACTIVE` 将移除账户的非活动限制。
- `-l`, `—list`

  显示账户老化信息。
- `-m`, `—mindays MIN_DAYS`

  设置密码更改之间的最小天数为 `MIN_DAYS`。此字段的值为零，表示用户可以随时更改其密码。
- `-M`, `—maxdays MAX_DAYS`

  设置密码有效的最大天数。当 `MAX_DAYS` 加上 `LAST_DAY` 小于当前日期时，用户将被要求在使用账户之前更改密码。可以使用 `-W` 选项提前计划此发生情况，为用户提供提前警告。

  将数字 `-1` 传递给 `MAX_DAYS` 将移除对密码有效性的检查。
- `-R`, `--root CHROOT_DIR`

  在 `CHROOT_DIR` 目录中应用更改并使用来自 `CHROOT_DIR` 目录的配置文件。
- `-W`, `--warndays WAR_DAYS`

  设置需要更改密码前的警告天数。`WAR_DAYS` 选项是在密码过期前多少天用户将收到密码即将过期的警告。

如果没有选择任何选项，`chage` 将以交互方式运行，提示用户所有字段的当前值。输入新值以更改该字段，或留空以使用当前值。当前值显示在两个标记之间。

## 注意

`chage` 程序需要一个可用 shadow 文件。`chage` 命令限制为 root 用户，但 `-l` 选项外，无权限用户可以使用该选项来确定其密码何时过期。

## 配置

`/etc/defs` 中的以下变量影响 shadow 文件：

### 文件

`/passwd`

用户信息。

`/shadow`

账户信息。

## 退出

`chage` 命令退出时的值如下：

- `0` 成功
- `1` 权限拒绝
- `2` 命令无效

## 参见

`passwd(5)`, `shadow(5)`

## 语法



```
chattr [options] file
```

### 描述

`chattr` 更改 Linux 系统下的文件属性。使用 `+` 添加属性，`-` 移除属性，使用 `=` 设置属性。

### 选项

- `-R` 递归地更改目录及其内容。
- `-V` 详细输出并打印版本。
- `-f` 抑制大多数错误信息。
- `-v` 设置版本号。

## 属性

具有 `'a'` 属性的文件只能以追加模式打开。只有 root 用户或拥有 `CAP_LINUX_IMMUTABLE` 能力的用户才能设置或清除此属性。当具有 `'A'` 属性的文件被访问时，其访问时间（atime）不会被修改。具有 `'c'` 属性的文件由内核在磁盘上压缩。从该文件读取的是未压缩的数据。写入该文件会将数据进行压缩。具有 `'C'` 属性的文件将进行写复制（注意：对于 btrfs，`'C'` 标记应设置在空文件。如果设置在已有数据的文件上，它是未定义的）。注意：请确保阅读本文末尾的错误和限制部分。具有 `'D'` 属性的文件在运行 `dump(8)` 程序运行时不会被备份。当具有 `'D'` 属性的目录被修改时，更改将同步写入磁盘；这等同于对部分文件应用 `'sync'` 挂载选项。

`'e'` 属性表示文件使用 extent 映射块。无法通过 `chattr(1)` 移除。

`'E'` 属性用于实验性压缩补丁，指示压缩文件存在压缩错误。无法通过 `chattr(1)` 设置或重置，尽管可以通过 `lsattr(1)` 显示。

`'h'` 属性表示文件以文件系统大小而非扇区为单位存储，意味着文件（或曾经）大于 2TB。无法通过 `chattr(1)` 设置或重置，尽管可以通过 `lsattr(1)` 显示。

`'i'` 属性的文件不可修改：不能删除或重命名，不能为该文件创建链接。只有 root 用户或拥有 `CAP_LINUX_IMMUTABLE` 能力的用户才能设置或清除此属性。

`'I'` 属性用于 htree 代码，指示目录使用哈希树索引。无法通过 `chattr(1)` 设置或重置，尽管可以通过 `lsattr(1)` 显示。

`'j'` 属性的文件在文件系统以 `'data=ordered'` 或 `'data=writeback'` 挂载时，其所有数据在写入文件之前都会写入 ext3 或 ext4 日志中。当文件系统以 `'data=journal'` 挂载时。并非所有文件系统都支持这些标志（参见 btrfs, ext4, xfs）。

所有文件数据已通过日志记录（journalled），因此此属性无效。只有超级用户或拥有 `CAP_SYS_RESOURCE` 能力的进程才能设置或清除此属性。

设置了 `'N'` 属性的文件表示该文件将数据存储在内联的 inode 中。无法使用 `chattr(1)` 设置或重置此属性，但可以通过 `lsattr(1)` 显示。

当删除带有 `'s'` 属性的文件时，其包含的块将将被清零并写回磁盘。请务必阅读本文档末尾的“错误与局限性”部分。

当修改带有 `'S'` 属性的文件时，更改将同步写入磁盘；这等同于对部分文件应用了 `'sync'` 挂载选项。

带有 `'t'` 属性的文件在文件末尾的部分块碎片（block fragment）不会与其他文件合并（对于支持尾部合并 tail-merging 文件系统）。这对于像 LILO 等直接读取文件系统且不支持尾部合并文件的应用程序来说是必要的。注意：截至本文编写时，ext2 或 ext3 文件系统尚未（除非在极少数实验性补丁中）支持尾部合并。

带有 `'T'` 属性的目录在 Orlov 块分配器中被视为目录层次结构的顶端。这是对 ext3 和 ext4 使用的块分配器的一个提示，表示该目录下的子目录是不相关的，在分配时应将它们分开。例如，为 `/home` 目录设置 `'T'` 属性是非常好的主意，这样 `/home/john` 和 `/home/mary` 将被放在不同的块组中。对于未设置此属性的目录，Orlov 分配器将尝试让子目录靠得近。

当删除带有 `'u'` 属性的文件时，其内容会被保存。这允许用户请求恢复（undeletion）。注意：请务必阅读本文档末尾的“错误与局限性”部分。

`'X'` 属性用于实验性压缩补丁，表示可以直接访问压缩文件的内容。目前无法通过 `chattr(1)` 设置或重置此属性，但可以通过 `lsattr(1)` 显示。

`'Z'` 属性用于实验性压缩补丁，表示压缩文件为脏数据（dirty）。无法通过 `chattr(1)` 设置或重置此属性，但可以通过 `lsattr(1)` 显示。

### 作者

`chattr` 由 Remy Card <Remy.Card@linux.org> 编写。目前由 Theodore Ts’o <tytso@alum.mit.edu> 维护。

## 错误与局限性

`'c'`、`'s'`和`'u'`属性在当前主线 Linux 内核实现的 ext2、ext3 和 ext4 文件系统中不被支持。

`'j'`选项仅在文件系统挂载为 ext3 或 ext4 时才有用。

`'D'`选项仅在 Linux 内核 2.5.19 及更高版本上有用。

## 可用性

`chattr` 是 e2fsprogs 包的一部分，可以通过 http://e2fsprogs.sourceforge.net 获取。

### 参见

`lsattr(1)`, `btrfs(5)`, `ext4(5)`, `xfs(5)`。

`chcon` - 更改文件的 SELinux 安全上下文

## 语法概要

`chcon [OPTION]... CONTEXT FILE...`
`chcon [OPTION]... [-u USER] [-r ROLE] [-l RANGE] [-t TYPE... FILE...`
`chcon [OPTION]... --reference=RFILE FILE...`

### 描述

将每个 `FILE` 的 SELinux 安全上下文更改为 `CONTEXT`。使用 `--reference`，将每个 `FILE` 的安全上下文更改为 `RFILE` 的安全上下文。

长选项的强制参数对于短选项也是强制的。

- `-dereference`
  影响每个符号链接的引用对象（默认值），而不是符号链接本身
- `-h`, `--no-dereference`
  影响符号链接而不是任何被引用的文件
- `-u`, `--user=USER`
  在目标安全上下文中设置用户 `USER`
- `-r`, `--role=ROLE`
  在目标安全上下文中设置角色 `ROLE`
- `-t`, `--type=TYPE`
  在目标安全上下文中设置类型 `TYPE`
- `-l`, `--range=RANGE`
  在目标安全上下文中设置范围 `RANGE`
- `--no-preserve-root`
  不特殊处理 `'/'`（默认值）
- `--preserve-root`
  防止在 `'/'` 上进行递归操作
- `--reference=RFILE`
  使用 `RFILE` 的安全上下文，而不是指定 `CONTEXT` 值
- `-R`, `--recursive`
  递归地对文件和目录进行操作
- `-v`, `--verbose`
  为处理的每个文件输出诊断信息

当指定了 `-R` 选项时，以下选项将修改层次结构遍历的方式。如果指定了多个，则只有最后一个生效。

- `-H`
  如果命令行参数是目录目录的符号链接，则遍历它
- `-L`
  遍历遇到的每一个指向目录的符号链接
- `-P`
  不遍历任何符号链接（默认值）
- `--help`
  显示此帮助信息并退出
- `--version`
  输出版本信息并退出

### 作者

由 Russell Coker 和 Jim Meyering 编写。

## 错误报告

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 向 <http://translationproject.org/team/> 报告 chchon 翻译错误

## 版权

Copyright © 2015 Free Software Foundation, Inc. 许可 GPLv3+: GNU GPL 3 或更后版本 <http://gnu.org/licenses/gpl.html>。这是一个自由软件：你可以自由地更改和分发它。在法律允许范围内不提供任何保证。

### 参见

完整文档位于：<http://www.gnu.org/software/coreutils/chcon> 或本地通过：info ‘(coreutils)

## 名称

`chfn` - 修改你的指纹信息

### 概要

`chfn [-f full-name] [-o office] [-p office-phone] [-h home-phone] [-u] [-v] [username]`

### 描述

`chfn` 用于更改指纹信息。这些信息存储在 `/etc/passwd` 文件中，并由 `finger` 程序显示。可以被 `chfn` 修改的内容：你的姓名、办公室电话和家庭电话。

这四项信息中的任何一项都可以在命令行指定。如果没有提供信息，`chfn` 将进入交互模式。

在交互模式下，`chfn` 会对每个字段进行提示。在提示处，你可以输入新信息，或者直接按回车键保持字段不变。输入关键字“none”可使字段为空。

如果链接了 libuser，`chfn` 支持非本地条目（kerberos, LDAP 等），否则使用 `ypwchfn`、`lchfn` 或其他实现。

### 选项



`-f`, `--full-name` `full-name`

指定你的姓名。

`-o`, `--office`

指定房间号。

`-p`, `--office-phone` `office-phone`

指定办公室电话。

`-h`, `--home-phone` `home-phone`

指定你的家庭电话。

`-u`, `--help`

显示帮助文本并退出。

`-v`, `--version`

输出版本信息并退出。

# 配置项

`chfn` 读取 `/etc/login.defs`(5) 配置文件。注意该配置文件可能与其他软件包一起（例如 `shadow-utils`）。以下配置项与 `chfn`(1) 相关：

`CHFN_RESTRICT` (string)

指示哪些字段可以被 `chfn` 修改。

布尔值“yes”意味着办公室、办公室电话和家庭电话可以更改；布尔值“no”意味着姓名、办公室、办公室电话和家庭电话可以更改。

另一种方法是通过缩写指定可更改字段：`f` = 姓名，`r` = 办公室，`w` = 工作电话，`h` = 家庭电话。例如 `CHFN_RESTRICT` “`wh`”允许更改工作和家庭电话。

如果未定义 `CHFN_RESTRICT`，则所有指纹信息只读。这是默认值。

# 退出状态

操作成功返回 `0`，如果操作失败或命令语法无效返回 `1`。

### 参见

`finger`(1), `passwd`(5)

### 作者

Salvatore Valente <svalente@mit.edu>

# 可用性

`chfn` 命令是 `util-linux` 包的一部分，可以通过 `ftp://ftp.kernel.org/pub/linux/utils/util-linux/` 获取。

## chgrp - 更改组所有权

### 语法概要

```
chgrp [OPTION]... GROUP FILE... chgrp [OPTION]... --reference=RFILE FILE...
```

### 描述

将每个 `FILE` 的组更改为 `GROUP`。使用 `--reference` 参数，则将每个 `FILE` 的组更改为 `RFILE` 的所属组。

`-c`, `--changes`

类似 `verbose`（详细模式），但仅在发生更改时报告

`-f`, `--quiet`

抑制大多数错误信息

`-v`, `--verbose`

对处理的每个文件输出诊断信息

`--dereference`

影响每个符号链接指向的目标（这是默认值），而不是符号链接本身

`-h`, `--no-dereference`

影响符号链接而不是任何引用的文件（仅适用于更改符号链接所有权的系统）

`--no-preserve-root`

不特殊对待 `/`（默认值）

`--preserve-root`

禁止在 `/` 上执行递归操作

`--reference=RFILE`

使用 `RFILE` 的组而不是指定一个 `GROUP` 值

`-R`, `--recursive`

递归地对文件和目录进行操作

当指定 `-R` 选项时，以下选项将修改遍历层级结构的方式。如果指定了多个选项，则仅以最后一个为准。

`-H`

如果命令行参数是符号目录的符号链接，则遍历它

`-L`

遍历遇到的每一个指向目录的符号链接

`-P`

不遍历任何符号链接（默认值）

`--help`

显示此帮助信息并退出

`--version`

输出版本信息并退出

## 示例

```
chgrp staff /u
```

将 `/u` 的组改为“staff”。

```
chgrp -hR staff /u
```

将 `/u` 及其子文件的组更改为“staff”。

### 作者

由 David MacKenzie 和 Jim Meyering 编写。

## 报告 Bug

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 将 `chgrp` 的翻译错误报告至 <http://translationproject.org/team/>

## 版权

Copyright © 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 3 版或更高版本 <http://gnu.org/licenses/gpl.html>。这是免费软件：你可以自由地更改和重新发布。在法律允许的范围内不提供任何保证。

### 参见

`chown`(1), `chown`(2)

完整文档见：<http://www.gnu.org/software/coreutils/chgrp> 或通过本地：info ‘(coreutils) chgrp invocation’

## 名称

`chmod` - 更改文件模式位

### 语法概要

```
chmod [OPTION]... MODE[,MODE]... FILE... chmod [OPTION]... OCTAL-MODE FILE... chmod [OPTION]... --reference=RFILE FILE...
```

### 描述

本手册页文档了 GNU 版本的 `chmod`。`chmod` 根据 `mode` 更改每个给定文件的模式位，`mode` 既可以是要执行更改的符号表示，也可以代表新模式模式的八进制数字。

符号模式的格式为 `[ugo][][-+][perms...]`，其中 `perms` 是 `rwxXst` 集合中的零或多个字母，或者 `ugo` 集合中的单个字母。可以提供多个符号模式，并用逗号隔开。

字母 `ugo` 的组合控制哪些用户的文件访问权限将发生更改：该文件的所有者 (`u`)、文件所在组的其他用户 (`g`)、不在文件组的其他用户 (`o`) 或所有用户 (`a`)。如果未提供其中任何一个，则效果等同于给出了 (`a`)，但 `um` 中设置的位不受影响。

运算符 `+` 会导致所选的文件模式位被添加到每个文件的现有文件模式位中；`-` 会导致它们被移除；`=` 则导致它们被添加，并移除未提及的位，但目录未设置的用户 ID 和组 ID 不受影响。

字母 `rwxXst` 控制所选的文件模式位：对于目录，执行的权限包括读取 (`r`)、写入 (`w`)、执行 (`x`)、执行 (`X`)、特殊位 (`s`) 或删除标记位 (`t`)。

## SETUID 和 SETGID 位

`MODE` 格式为 '[ugoa]*([-+=][rwxXst]*([ugo]))+|[-=]=[0-7]+'。

## 限制删除标志或粘性位

限制删除标志（粘位）在目录上，除非是目录所有者、组成员或具有写权限的用户，否则无法删除或重命名文件。这常见于 `/tmp`。

### 选项

将每个 `FILE` 的组更改为 `GROUP`。使用 `--reference`，则将每个 `FILE` 的组更改为 `RFILE` 的所属组。

### 描述

本手册文档了 GNU 版本的 `chown`。`chown` 更改每个给定文件的用户和/或组所有权。如果只给出所有者（用户名或数字用户 ID），则该用户将成为每个给定文件的所有者，且文件的组保持不变。如果所有者后面紧跟一个冒号和组名（或数字组 ID），且用户名和组名之间没有空格，则该用户将成为文件的所有者，并且文件的组将更改为该用户的登录组。如果用户名后仅有冒号而没有组名，则文件的组所有权也会发生更改。如果给出了冒号和组，但省略了所有者，则仅更改文件的组；在这种情况下，`chown` 执行的功能与 `chgrp` 相同。如果只给出一个冒号，或者整个操作数为空，则所有者和组都不会发生更改。

### 选项

将每个 `FILE` 的所有者和/或组更改为 `OWNER` 和/或 `GROUP`。使用 `--reference`，将每个 `FILE` 的所有者和组更改为 `RFILE` 的。

`-c`, `--changes`

类似于 `verbose`（详细），但仅在发生更改时报告

`-f`, `--silent`, `--quiet`

抑制大多数错误消息

`-v`, `--verbose`

对每个处理的文件输出一条诊断信息

`--dereference`

影响每个符号链接的引用目标（默认值），而不是符号链接本身

`-h`, `--no-dereference`

影响符号链接而不是任何引用的文件（仅在可以更改符号链接所有权的系统上有用）

`--from=CURRENT_OWNER:CURRENT_GROUP`

仅当文件的当前所有者和组与此处指定的项匹配时，才更改每个文件的所有者和/或组。其中任何一项都可以被省略，在这种情况下，被省略的属性不需要匹配

`--no-preserve-root`

不对 `/` 视为特殊处理（默认值）

`--preserve-root`

在对 `/` 进行递归操作时失败

`--reference=RFILE`

使用 `RFILE` 的所有者和组，而不是指定 `OWNER:GROUP` 值

`-R`, `--recursive`

递归地对文件和目录进行操作

以下选项在指定了 `-R` 选项时，修改遍历层级结构的方式。如果指定了多个选项，则仅最后一个生效。

`-H`

如果命令行参数是符号目录的符号链接，则遍历它

`-L`

遍历遇到的每一个指向目录的符号链接

`-P`



不遍历任何符号链接（默认值）

- `--help`

显示此帮助信息并退出

- `--version`

输出版本信息并退出

如果缺失所有者，则保持不变。如果缺失组，则保持不变，但如果由符号 OWNER后的冒号暗示，则将其更改为登录组。OWNER 和 GROUP 可以是数字的也可以是符号的。

## 示例

`chown root /u`

将 `/u` 的所有者改为“root”。

`chown root:staff /u`

同样，但将其组更改为“staff”。

`chown -hR root /u`

将 `/u` 及其子文件的所有者改为“root”。

### 作者

由 David Mackenzie 和 Jim Meyering 编写。

# 报告错误

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 向 <http://translationproject.org/team/> 报告 chown 翻译错误

# 版权

Copyright © 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL 版本3 或更高版本 <http://gnu.org/licenses/gpl.html>。这是免费软件：你可以自由地更改和分发它。在法律允许的范围内不提供任何保证。

# 另请

`chown(2)`

完整文档位于：<http://www.gnu.org/software/coreutils/chown> 或通过本地可用：info ‘(coreutils) chown invocation'

## 名称

`chronyc` - 用于 `chronyd` 的命令行界面

# 语法摘要

```
chronyc [OPTIONS]
```

### 描述

`chrony` 是一对用于维护计算机时钟准确性的程序。

`chronyc` 是一个命令行界面程序，可用于监控 `chronyd` 的性能并在运行时更改各种运行参数。

# 使用方法

`chronyc` 支持的所有命令的详细说明可以通过发行版随附的文档（`chrony.txt` 和 `chrony.texi`）获取。

### 选项

下方包含了 `chronyc` 支持的选项摘要。

- `-h hostname`

指定主机名（默认 `127.0.0.1`）

- `-p port-number`

指定端口号

- `-n`

显示原始 IP 地址（不尝试查找主机名）

- `-4`

仅将主机名解析为 IPv4 地址

- `-6`

仅将主机名解析为 IPv6 地址

- `-m`

允许在命令行上指定多个命令。每个参数将被整体解释为一条完整的命令。

- `-f conf-file`

此选项可指定配置文件的替代位置（默认 `/etc/chrony.conf`）。`-a` 选项需要配置文件。

- `-a`

使用此选项后，`chronyc` 将在启动时尝试自动身份验证。它将读取配置文件，从密钥文件中读取命令键并运行 `authhash` 和 `password` 命令。

- `command`

指定命令。如果没有给出命令，`chronyc` 将以交互方式读取命令。

# 错误

如需报告错误，请访问 http://chrony.tuxfamily.org

# 另请

`chronyd(8)`

http://chrony.tuxfamily.org/

### 作者

Richard Curnow <rc@rc0.org.uk>

此手册页由 Jan Schaumann <jsuma@netmeister.org> 作为“缺失手册页项目”的一部分编写。请参 http://www.netmeister.org/misc/m2p/index.html 详情。

完整的 `chronyd` 文档以 texinfo 格式提供。

## 名称

`chroot` - 更改根

# 语法摘要

```
chroot [OPTIONS]
```

### 描述

`chroot` 更改命令及其子进程的根目录。

根目录更改指定的目录。如果没有指定，则使用当前根目录。

目录必须是一个目录，且进程对其拥有读取和执行权限。新目录必须是当前根目录的子目录，或者进程拥有 root 权限。

`chroot` 命令更改命令及其子进程的根目录。

## 名称

`chroot` - 更改根

# 语法摘要

```
chroot [OPTIONS] [DIRECTORY]
```

### 描述

`chroot` 更改命令及其子进程的根目录。

根目录更改指定的目录。如果没有指定，则使用当前根目录。

目录必须是一个目录，且进程对其拥有读取和执行权限。新目录必须是当前根目录的子目录，或者进程拥有 root 权限。

### 作者

由 Free Software Foundation 编写。

本手册页文档了 GNU 版本的 `chroot`。`chroot` 更改命令及其子进程的根目录。

# 报告错误

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 向 <http://translationproject.org/team/> 报告 `chroot` 翻译错误

# 版权

Copyright ... omitted ...

### 选项

- `--help`

显示此帮助信息并退出

- `--version`

输出版本信息并退出

# 另请

`chroot(2)`

# 用法

默认行为是运行一个新命令：

```
chrt priority command [arguments]
```

你也可以获取现有任务的实时属性：

```
chrt -p pid
```

或者设置这些属性：

```
chrt -r -p priority pid
```

# 权限

用户必须拥有 `CAP_SYS_NICE` 权限才能更改进程的调度属性。任何用户都可以获取调度信息。

# 注意事项

只有 `SCHED_FIFO`、`SCHED_OTHER` 和 `SCHED_RR` 属于 POSIX 1003.1b 进程调度标准。其他调度属性在某些系统上可能会被忽略。

Linux 默认调度策略是 `SCHED_OTHER`。

### 参见

`taskset(1)`, `nice(1)`, `renice(1)`

Linux 调度方案的描述请参见 `sched_setscheduler(2)`。

### 作者

由 Robert M. Love 编写。

# 版版权

Copyright © 2004 Robert M. Love. 本软件为免费软件；请参源代码复制条件。不提供任何保证；即使对于商品性或特定用途的适用性也是如此。

# 可用性

`chrt` 命令是 `util-linux` 软件包的一部分，可以通过 `ftp://ftp.kernel.org/pub/linux/utils/util-linux/` 获取。

`chsh` - 更改你的登录 shell

### 概要

```
chsh [-s shell] [-l] [-u] [-v] [username]
```

### 描述

`chsh` 用于更改你的登录 shell。如果命令行上没有提供 shell，`chsh` 会提示输入一个。

如果与 `libuser` 链接，`chsh` 支持非本地条目（kerberos、LDAP 等），否则请使用 `ypchsh, lchsh` 或任何其他用于非本地条目的实现。

### 选项

- `-s`, `--shell shell`

指定你的登录 shell。

- `-l`, `--list-shells`

打印 `/etc/shells` 中列出的 shell 列表并退出。

- `-u`, `--help`

显示帮助文本并退出。

- `-v`, `--version`

显示版本信息并退出。

# 有效 shell

`chsh` 会接受系统上任何可执行文件的完整路径。然而，如果 shell 未在 `/etc/shells` 文件列表中，它将发出警告。另一方面，它也可以配置为仅接受该文件中列出的 shell，除非你是 root 用户。

# 退出状态

操作成功返回 0，如果操作失败或命令语法无效则返回 1。

### 参见

`login(1)`, `passwd(5)`, `shells(5)`

### 作者

Salvatore Valente <svalente@mit.edu>

# 可用性

`chsh` 命令是 `util-linux` 软件包的一部分，可以通过 `ftp://ftp.kernel.org/pub/linux/utils/util-linux/` 获取。

## 名称

`chvt` - 切换前虚拟终端

### 概要

`chvt N`

### 描述

命令 `chvt N` 将 `/dev/ttyN` 设置为前台终端。（如果相应的屏幕不存在，则会创建它。要移除未使用的 VT，请使用 `deallocvt(1)`。组合键 (Ctrl)-左Alt-FN（N 范围为 1-12）通常具有类似的效果。）

`cifscreds` - 在内核密钥环中管理 NTLM 凭据

### 概要



`cifscreds add|clear|clearall|update [-u username] [-d] host|domain`

### 描述

`cifscreds` 程序是一个用于管理多用户挂载建立会话所需的凭据（用户名和密码）的工具。

当 `cifs` 文件系统使用 `multiuser` 选项挂载且不使用 `krb5` 认证时，它需要能够从某个地方获取每个用户的凭据。`cifscreds` 程序即是用于向内核提供这些凭据的工具。

`cifscreds` 的第一个非选项参数是命令（参见下文章节）。第二个非选项参数是主机名、地址或一个 `DOMAINNT` 名称。

### 命令

`add`

将凭据添加到内核中，用于连接到指定的服务器或指定网域内的服务器。

`clear`

从内核中清除特定主机或网域的凭据。

`clearall`

从内核中清除所有 `cifs` 凭据。

`update`

使用新的用户名和密码更新内核中存储的凭据。

### 选项

- `-d`, `--domain` 提供的 `host/domain` 参数是一个 NT 域名。

  通常情况下，提供给 `cifcreds` 的第二个参数被视为主机名或 IP 地址。此选项使 `cifscreds` 程序将该参数视为 NT 域名。

  如果挂载的服务器没有特定主机的凭据，则内核将随后查找与挂载时提供的 `domain=` 选项相同的网域凭据。

- `-u`, `--username`

  通常情况下，用户名派自添加凭据的用户的 unix 用户名。此选项允许用户替换不同的用户名。

# 注意事项

`cifreds` 工具需要构建了支持 `login` 密钥类型的内核。该密钥类型在 Linux 主线内核的 v3.3 版本中添加。

由于 `cifsreds` 会向会话密钥环添加密钥，强烈建议使用 `pam_keyinit` 以确保在登录时建立会话密钥环。

### 参见

`pam_keyinit(8)`

### 作者

`cifsreds` 程序最初由 Igor Druzhinin <jax@gmail.com> 开发。此帮助页和代码重设计由 Jeff Layton <layton@samba.org> 完成。

`ciphers` - 列出密钥环中的 NTLM 凭据（注意：此行似乎根据上下文重复的）

### 概要

```
openssl ciphers [-v] [-V] [-ssl2] [-ssl3] [-tls1] [cipherlist]
```

### 描述

`ciphers` 命令将文本加密列表转换为 SSL 优先级列表。

### 选项

- `-v` 详细模式。列出加密。
- `-V` 类似于 `-v`，但以十六进制格式包含加密套。
- `-ssl3` 仅包含 SSL3 加密。
- `-ssl2` 仅包含 SSL2 加密。
- `-tls1` 仅包含 TLS1 加密。
- `-h`, `-?` 显示简单的用法信息。
- `cipherlist` 要转换为优先级列表的加密列表。如果不包含，将使用默认加密列表。格式见下文。

# 加密列表格式

加密列表格式

加密列表由多个由冒号分隔的加密字符串组成。逗号或空格也可以接受，但通常使用冒号。

实际的加密字符串可以有多种形式。

它可以由单个加密套组成，如 `RC-SHA`

它可以表示包含特定算法或某种类型的加密套列表。例如，`SHA` 表示使用摘要算法 SHA 的加密套，`SSL3` 表示所有 SSL3 算法。

加密套列表可以使用 `+` 字符在单个加密字符串中组合。这用于逻辑与。例如，`SHA1+DES` 表示包含 SHA1 和 DES 算法的所有加密套。

每个加密字符串都可以可选地带有 `!`, `-` 或 `+` 前缀。

如果使用了 `!`，则加密将从列表中永久删除。即使显式说明，已删除的加密也不会再次出现在列表中。

如果使用了 `-`，则加密将从列表中删除，但可以通过后续选项重新添加部分或全部加密。

如果使用了 `+`，则加密将移动到列表末尾。此选项不会添加任何新加密，只是移动匹配的现有项。

如果没有这些字符，则字符串仅被解释为附加到当前优先级列表的加密列表。如果列表中已包含任何加密，则将忽略它们：即它们不会被移动到列表末尾。

此外，加密字符串 `@STRENGTH` 可以任何位置使用，按加密算法密钥长度对当前加密列表进行排序。

# 加密字符串 (CIPHER STRINGS)

以下是所有允许的加密字符串及其含义的列表。

## DEFAULT

默认加密列表。这在编译时确定，通常为 `ALL:!aNULL:!eNULL:!SSLv2`。这必须是指定的第一个加密。

## COMPLEMENTOFDEFAULT

包含在 `ALL` 中但默认未启用的加密算法。目前为 `ALLADH ECDH`。注意，此规则不涵盖 `eNULL`，它不包含在 `ALL` 中（如有必要，请使用 `COMPLEMENTALL`）。

## ALL

除必须显式启用的 `eNULL` 加密算法以外的所有加密套件；根据 OpenSSL，`ALL` 加密套件默认按合理顺序排序的。

## COMPLEMENTALL

当前 `ALL` 中未启用的加密套件。

## HIGH

“高强度”加密套件。目前指密钥长度大于 128 位的套件，以及某些具有 128 位密钥的套件。

## MEDIUM

“中强度”加密套件，目前指某些使用 128 位加密的套件。

## LOW

“低强度”加密套件，目前指使用 64 或 56 位加密算法的排除出口加密套件。

## EXPORT

出口加密算法。包括 40 位和 56 位算法。

## EXPORT40

40 位出口加密算法。

## EXPORT56

56 位出口加密算法。在 OpenSSL 0.9.8c 及更高版本中，除非 OpenSSL 明确配置为支持实验性（experimental），否则 56 位出口加密算法集为空。

## eNULL, NULL

不提供加密的“NULL”加密算法。由于这些提供了加密且存在安全风险，除非显式包含，否则它们将被禁用。

## aNULL

不提供身份验证的加密套件。目前为匿名 DH 算法和匿名 ECDH 算法。这些加密套件容易受到“中间人”攻击，因此通常不建议使用。

## kRSA, RSA

使用 RSA 密钥交换的加密套件。

## kDHr, kDHd

使用 DH 密钥协商以及分别由带有 RSA 和 DSS 密钥的 CA 名的 DH 证书的加密套件。

## kDEH, kEDH

使用临时 DH 密钥协商的加密套件，包括匿名加密套件、使用身份验证临时 DH 密钥协商的加密套件。

## ADH

匿名 DH 加密套件，注意这不包括匿名椭圆曲线 DH (ECDH) 套件。

## DH

使用 DH 的加密套件，包括匿名 DH、临时 DH 和固定 DH。

## kECDRH, kECDHe, kECDH

使用带有 RSA 和 ECDSA 密钥的 CA 名的固定 ECDH 密钥协商的加密套件。

## kECDHE, kECDH

使用临时 ECDH 密钥协商的加密套件，包括匿名加密套件。

## ECDHE, EECDH

使用身份验证临时 ECDH 密钥协商的加密套件。

## AECDH

匿名椭圆曲线 Diffie Hellman 加密套件。

## ECDH

使用 ECDH 密钥交换的加密套件，包括匿名、临时和固定 ECDH。

## aRSA

使用 RSA 身份验证的加密套件，即证书带有 RSA 密钥。

## aDSS, DSS

使用 DSS 身份验证的加密套件，即证书带有 DSS 密钥。

## aDH

有效使用 DH 身份验证的加密套件，即证书带有 DH 密钥。

## aECDH

有效使用 ECDH 身份验证的加密套件，即证书带有 ECDH 密钥。

## aECDSA, ECDSA

使用 ECDSA 身份验证的加密套件，即证书带有 ECDSA 密钥。

## kFZA, aFZA, eFZA, FZA

使用 FORTEZA 密钥交换、加密或所有 FORTEZA 算法的加密套件。尚未实现。

## TLS1.2, TLSv1, SSLv3, SSLv2

分别对应 TLS v1.2、TLS v1.0、ssl v3.0 和 ssl v2.0 加密套件。注意：没有特定于 tls 1.1 套件。

## AES128, AES256, AES

使用 128 位 AES、256 位 AES 或 128 或 256 位 AES 的加密套件。

## AESGCM

伽罗斯计数器模式 (GCM) 下的 AES：这些套件仅在 TLS v1.2 中支持。

## CAMELLIA128, CAMELLIA256, CAMELLIA

使用 128 位 CAMELLIA、256 位 CAMELLIA 或 128 或 256 位 CAMELLIA 的加密套件。

## 3DES

使用三重 DES 的加密套件。

## DES

使用 DES (非三重 DES) 的加密套件。

## RC4

使用 RC4 的加密套件。

## RC2

使用 RC2 的加密套件。

## IDEA

使用 IDEA 的加密套件。

## SEED

使用 SEED 的加密套件。

## MD5

使用 MD5 的加密套件。

## SHA1

使用 SHA1 的加密套件。

## SHA256, SHA384

使用 SHA256 或 SHA384 的加密。



## aGOST

使用 GOST R 34.10 (2001 或 94) 进行身份验证的加密套件（需要运行 GOST 算法的引擎）。

## aGOST01

使用 GOST R 34.10-2001 身份验证的加密套件。

## aGOST94

使用 GOST R 34.10-94 身份验证的加密套件（注意 R 34.10-94 标准已过期，请使用 GOST R 34.10-2001）。

## kGOST

使用 GOST R 34.10 密钥交换的加密套件，符合 RFC 4357。

## GOST94

使用 GOST R 34.10-94 HMAC 的加密套件。

## GOST89

使用 GOST R 34.10 的 HMAC 的加密套件。

## PSK

使用预共享密钥 (PSK) 的加密套件。

## SUITE128, SUITE19

启用 128 位套件模式。如果这些加密字符串出现在列表中，其后的任何内容将被忽略。符合 RFC 6460，特别是加密算法被限制为仅支持 ECDSA 和 SHA256 或 SHA384（ECDHE-AES-GCM-256 等允许）。

## CIPHER SUITE NAMES

以下加密字符串提供了 SSL 或 TLS 的名称。在这些情况下，使用了 SSL v3 身份验证。

### SSL v3.0 加密套件

`SSL_RSA_WITH_NULL_MD5`
`SSL_RSA_WITH_NULL_SHA`
`SSL_RSA_EXPORT_WITH_RC4_40_MD5`
`SSL_RSA_WITH_RC4_128_MD5`
`SSL_RSA_WITH_RC4_128_SHA`
`SSL_RSA_EXPORT_WITH_RC2_CBC_40_MD5`
`SSL_RSA_WITH_DES_CBC_SHA`
`SSL_RSA_EXPORT_WITH_DES_CBC_40_SHA`
`SSL_RSA_WITH_DES_CBC_SHA`
`SSL_RSA_WITH_3DES_EDE_CBC_SHA`
`SSL_DH_WITH_DES_CBC_SHA`
`SSL_DH_WITH_3DES_EDE_CBC_SHA`
`SSL_DH_WITH_RC4_128_SHA`
`SSL_DH_WITH_3DES_EDE_CBC_SHA`
`SSL_DHE_EXPORT_WITH_DES_CBC_40_SHA`
`SSL_DHE_WITH_DES_CBC_SHA`
`SSL_DHE_WITH_3DES_EDE_CBC_SHA`
`SSL_RSA_EXPORT_WITH_DES_CBC_40_SHA`
`SSL_RSA_WITH_DES_CBC_SHA`

### TLS v1.0 加密套件

`TLS_RSA_WITH_NULL_MD5`
`TLS_RSA_WITH_NULL_SHA`
`TLS_RSA_EXPORT_WITH_RC4_40_MD5`
`TLS_RSA_WITH_RC4_128_MD5`
`TLS_RSA_WITH_RC4_128_SHA`
`TLS_RSA_EXPORT_WITH_RC2_CBC_40_MD5`
`TLS_RSA_WITH_DES_CBC_SHA`
`TLS_RSA_EXPORT_WITH_DES_CBC_40_SHA`
`TLS_RSA_WITH_DES_CBC_SHA`
`TLS_RSA_WITH_3DES_EDE_CBC_SHA`
`TLS_DH_WITH_DES_CBC_SHA`
`TLS_DH_WITH_3DES_EDE_CBC_SHA`
`TLS_DH_WITH_RC4_128_SHA`
`TLS_DH_WITH_3DES_EDE_CBC_SHA`
`TLS_DHE_EXPORT_WITH_DES_CBC_40_SHA`
`TLS_DHE_WITH_DES_CBC_SHA`
`TLS_DHE_WITH_3DES_EDE_CBC_SHA`
`TLS_RSA_EXPORT_WITH_DES_CBC_40_SHA`
`TLS_RSA_WITH_DES_CBC_SHA`
`TLS_RSA_WITH_3DES_EDE_CBC_SHA_EDH-RSA-DES-CBC3-SHA`
`TLS_DH_anon_WITH_RC4_40_MD5 EXP-ADH-RC4-MD5`
`TLS_DH_anon_WITH_RC4_128_MD5 ADH-RC4-MD5`
`TLS_DH_anon_WITH_DES40_CBC_SHA EXP-ADH-DES-CBC-SHA`
`TLS_DH_anon_WITH_DES_CBC_SHA ADH-DES-CBC-SHA`
`TLS_DH_anon_WITH_3DES_EDE_CBC_SHA ADH-DES-CBC3-SHA`

### 扩展 TLS v1.0 的 AES 算法

`TLS_RSA_WITH_AES_128_CBC_SHA` `AES128-SHA` `TLS_RSA_WITH_AES_256_CBC_SHA` `AES256-SHA` `TLS_DH_DSS_WITH_AES_128_CBC_SHA` `DH-DSS-AES128-SHA` `TLS_DH_DSS_WITH_AES_256_CBC_SHA` `DH-DSS-AES256-SHA` `TLS_RSA_WITH_AES_128_CBC_SHA` `DH-RSA-AES128-SHA` `TLS_RSA_WITH_AES_256_CBC_SHA` `DH-RSA-AES256-SHA` `TLS_DH_DSS_WITH_AES_128_CBC_SHA` `DHE-DSS-AES128-SHA` `TLS_DH_DSS_WITH_AES_256_CBC_SHA` `DHE-DSS-AES256-SHA` `TLS_RSA_WITH_AES_128_CBC_SHA` `DHE-RSA-AES128-SHA` `TLS_RSA_WITH_AES_256_CBC_SHA` `DHE-RSA-AES256-SHA` `TLS_DH_anon_WITH_AES_128_CBC_SHA` `ADH-AES128-SHA` `TLS_DH_anon_WITH_AES_256_CBC_SHA` `ADH-AES256-SHA`

### 扩展 TLS v1.0 的 RFC4132 卡米亚（Camellia）算法

`TLS_RSA_WITH_CAMELLIA_128_CBC_SHA` `CAMELLIA-128-SHA` `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA` `CAMELLIA-256-SHA` `TLS_DH_DSS_WITH_CAMELLIA_128_CBC_SHA` `DH-DSS-CAMELLIA-128-SHA` `TLS_DH_DSS_WITH_CAMELLIA_256_CBC_SHA` `DH-DSS-CAMELLIA-256-SHA` `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA` `DH-RSA-CAMELLIA-128-SHA` `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA` `DH-RSA-CAMELLIA-256-SHA` `TLS_DH_DSS_WITH_CAMELLIA_128_CBC_SHA` `DHE-DSS-CAMELLIA-128-SHA` `TLS_DH_DSS_WITH_CAMELLIA_256_CBC_SHA` `DHE-DSS-CAMELLIA-256-SHA` `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA` `DHE-RSA-CAMELLIA-128-SHA` `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA` `DHE-RSA-CAMELLIA-256-SHA` `TLS_DH_anon_WITH_CAMELLIA_128_CBC_SHA` `ADH-CAMELLIA-128-SHA` `TLS_DH_anon_WITH_CAMELLIA_256_CBC_SHA` `ADH-CAMELLIA-256-SHA`

### 扩展 TLS v1.0 的 RFC4162 种子（Seed）算法

`TLS_RSA_WITH_SEED_CBC_SHA` `SEED-SHA` `TLS_DH_anon_WITH_SEED_CBC_SHA` `DH-DSS-` `TLS_DH_anon_WITH_SEED_CBC_SHA` `DH-RSA-SEED-SHA` `TLS_DH_DSS_WITH_SEED_CBC_SHA` `DHE-DSS-SEED-SHA` `TLS_RSA_WITH_SEED_CBC_SHA` `DHE-RSA-SEED-SHA` `TLS_DH_anon_WITH_SEED_CBC_SHA` `ADH-SEED-SHA`

### 扩展 TLS v1.0 的 draft-chudov-crypto-cptls GOST 算法

注意：这些算法需要一个包含 gost 加密算法的引擎，例如 OpenSSL 分发中的 cogst 引擎。

```
TLS_GOSTR341094_WITH_28147_CNT_IMIT GOST94-GOST89-GOST89
TLS_GOSTR341001_WITH_28147_CNT_IMIT GOST2001-GOST89-GOST89
TLS_GOSTR341094_WITH_NULL_GOSTR3411 GOST94-NULL-GOST94
TLS_GOSTR341001_WITH_NULL_GOSTR3411 GOST2001-NULL-GOST94
```

## 额外的 Export1024 和其他密码套件



注意：这些算法可以在 `ssl3` 中中使用。

`TLS_RSA_EXPORT1024_WITH_DES_CBC_SHA` `EXP-RSA-DES-CBC-SHA` `TLS_RSA_EXPORT1024_WITH_RC4_40` `EXP-RSA-RC4-40` `TLS_DHE_EXPORT1024_WITH_DES_CBC_SHA` `EXP-DHE-DES-CBC-SHA` `TLS_DHE_EXPORT1024_WITH_RC4_40` `EXP-DHE-RC4-40` `TLS_DHE_DSS_WITH_RC4_40` `ADH-RC4-40`

# 椭圆曲线（Elliptic curve）套件

`ECDH_RSA_WITH_NULL` `ECDH-RSA-NULL` `ECDH_RSA_WITH_RC4_128` `ECDH-RSA-RC4-128` `ECDH_RSA_WITH_3DES_EDE_CBC` `ECDH-RSA-DES-CBC3` `ECDH_RSA_WITH_AES_128_CBC_SHA` `ECDH-RSA-AES128` `ECDH_RSA_WITH_AES_256_CBC_SHA` `ECDH-RSA-AES256` `ECDH_RSA_WITH_NULL` `ECDH-RSA-NULL` `ECDH_DSS_WITH_RC4_128` `ECDH-DSS-RC4-128` `ECDH_DSS_WITH_3DES_EDE_CBC` `ECDH-DSS-DES-CBC3` `ECDH_DSS_WITH_AES_128_CBC_SHA` `ECDH-DSS-AES128` `ECDH_DSS_WITH_AES_256_CBC_SHA` `ECDH-DSS-AES256` `ECDH_anon_WITH_NULL` `ECDH-anon-NULL` `ECDH_anon_WITH_RC4_128` `ECDH-anon-RC4-128` `ECDH_anon_WITH_3DES_EDE_CBC` `ECDH-anon-DES-CBC3` `ECDH_anon_WITH_AES_128_CBC_SHA` `ECDH-anon-AES128` `ECDH_anon_WITH_AES_256_CBC_SHA` `ECDH-anon-AES256`

# TLS v1.2 密码套件

`TLS_RSA_WITH_NULL_SHA256` `TLS-NULL-SHA256` `TLS_RSA_WITH_AES_128_CBC_SHA256` `AES128-SHA256` `TLS_RSA_WITH_AES_256_CBC_SHA256` `AES256-SHA256` `TLS_RSA_WITH_AES_128_GCM_SHA256` `AES128-GCM-SHA256` `TLS_DHE_WITH_AES_128_CBC_SHA256` `DH-RSA-AES128-SHA256` `TLS_DHE_WITH_AES_256_CBC_SHA256` `DH-RSA-AES256-SHA256` `TLS_DHE_WITH_AES_128_GCM_SHA256` `DH-RSA-AES128-GCM-SHA256` `TLS_DHE_WITH_AES_256_GCM_SHA384` `DH-RSA-AES256-GCM-SHA384` `TLS_DHE_DSS_WITH_AES_128_CBC_SHA256` `DHE-DSS-AES128-SHA256` `TLS_DHE_DSS_WITH_AES_128_GCM_SHA256` `DHE-DSS-AES128-GCM-SHA256` `TLS_DHE_DSS_WITH_AES_256_GCM_SHA384` `DHE-DSS-AES256-GCM-SHA384` `TLS_DHE_RSA_WITH_AES_128_CBC_SHA256` `DHE-RSA-AES128-SHA256` `TLS_DHE_RSA_WITH_AES_256_CBC_SHA256` `DHE-RSA-AES256-SHA256` `TLS_DHE_RSA_WITH_AES_128_GCM_SHA256` `DHE-RSA-AES128-GCM-SHA256` `TLS_DHE_RSA_WITH_AES_256_GCM_SHA384` `DHE-RSA-AES256-GCM-SHA384` `TLS_DHE_DSS_WITH_NULL` `DHE-DSS-NULL` `TLS_DHE_DSS_WITH_RC4_128` `DHE-DSS-RC4-128` `TLS_DHE_DSS_WITH_3DES_EDE_CBC` `DHE-DSS-DES-CBC3` `TLS_DHE_DSS_WITH_AES_128_CBC_SHA` `DHE-DSS-AES128` `TLS_DHE_DSS_WITH_AES_256_CBC_SHA` `DHE-DSS-AES256` `TLS_DHE_anon_WITH_NULL` `DHE-anon-NULL` `TLS_DHE_anon_WITH_RC4_128` `DHE-anon-RC4-128` `TLS_DHE_anon_WITH_3DES_EDE_CBC` `DHE-anon-DES-CBC3` `TLS_DHE_anon_WITH_AES_128_CBC_SHA` `DHE-anon-AES128` `TLS_DHE_anon_WITH_AES_256_CBC_SHA` `DHE-anon-AES256`

# 预共享密钥（psk）套件

`TLS_PSK_WITH_NULL_SHA256` `PSK-NULL-SHA256` `TLS_PSK_WITH_AES_128_CBC_SHA256` `PSK-AES128-SHA256` `TLS_PSK_WITH_AES_256_CBC_SHA256` `PSK-AES256-SHA256` `TLS_PSK_WITH_AES_128_GCM_SHA256` `PSK-AES128-GCM-SHA256` `TLS_PSK_WITH_AES_256_GCM_SHA384` `PSK-AES256-GCM-SHA384` `TLS_PSK_WITH_NULL` `PSK-NULL` `TLS_PSK_WITH_RC4_128` `PSK-RC4-128` `TLS_PSK_WITH_3DES_EDE_CBC` `PSK-DES-CBC3` `TLS_PSK_WITH_AES_128_CBC_SHA` `PSK-AES128` `TLS_PSK_WITH_AES_256_CBC_SHA` `PSK-AES256`

# 预共享密钥（psk）与DHE结合

`TLS_DHE_PSK_WITH_NULL_SHA256` `DHE-PSK-NULL-SHA256` `TLS_DHE_PSK_WITH_AES_128_CBC_SHA256` `DHE-PSK-AES128-SHA256` `TLS_DHE_PSK_WITH_AES_256_CBC_SHA256` `DHE-PSK-AES256-SHA256` `TLS_DHE_PSK_WITH_AES_128_GCM_SHA256` `DHE-PSK-AES128-GCM-SHA256` `TLS_DHE_PSK_WITH_AES_256_GCM_SHA384` `DHE-PSK-AES256-GCM-SHA384` `TLS_DHE_PSK_WITH_NULL` `DHE-PSK-NULL` `TLS_DHE_PSK_WITH_RC4_128` `DHE-PSK-RC4-128` `TLS_DHE_PSK_WITH_3DES_EDE_CBC` `DHE-PSK-DES-CBC3` `TLS_DHE_PSK_WITH_AES_128_CBC_SHA` `DHE-PSK-AES128` `TLS_DHE_PSK_WITH_AES_256_CBC_SHA` `DHE-PSK-AES256`

# 预共享密钥（psk）与ECDH结合

`TLS_ECDH_PSK_WITH_NULL_SHA256` `ECDH-PSK-NULL-SHA256` `TLS_ECDH_PSK_WITH_AES_128_CBC_SHA256` `ECDH-PSK-AES128-SHA256` `TLS_ECDH_PSK_WITH_AES_256_CBC_SHA256` `ECDH-PSK-AES256-SHA256` `TLS_ECDH_PSK_WITH_AES_128_GCM_SHA256` `ECDH-PSK-AES128-GCM-SHA256` `TLS_ECDH_PSK_WITH_AES_256_GCM_SHA384` `ECDH-PSK-AES256-GCM-SHA384` `TLS_ECDH_PSK_WITH_NULL` `ECDH-PSK-NULL` `TLS_ECDH_PSK_WITH_RC4_128` `ECDH-PSK-RC4-128` `TLS_ECDH_PSK_WITH_3DES_EDE_CBC` `ECDH-PSK-DES-CBC3` `TLS_ECDH_PSK_WITH_AES_128_CBC_SHA` `ECDH-PSK-AES128` `TLS_ECDH_PSK_WITH_AES_256_CBC_SHA` `ECDH-PSK-AES256`

### 命令

`show`

显示已连接设备的信息。

`search`

搜索蓝牙设备并连接到第一个支持 CIP 的设备。

`connect <bdaddr> [psm]`

将本地设备连接到指定 PSM 上的远程蓝牙设备。如果未指定 PSM，它将使用 SDP 从远程设备检索。

`release [bdaddr]`

释放对特定设备的连接。如果没有给出地址且仅连接了一个设备，则将释放该连接。

`loopback <bdaddr> [psm]`



创建一个到远程设备的连接以用于蓝牙测试。此命令不会提供 CAPI 控制器，因为它体仅用于测试 CAPI 消息传输协议。

### 作者

由 Marcel Holtmann <marcel@holtmann.org> 编写。

## 名称

`cisco-decrypt` - 解密混淆的 Cisco VPN 客户端预共享密钥

### 概要

`cisco-decrypt <obfuscated pre-shared key>`

### 描述

此命令配合 `vpnc` 使用。它可以密混淆的 `*.pcf-configuration` 文件，这些文件必须在命令行中指定。

结果将打印到 STDOUT。

### 作者

`cisco-decrypt` 最初由 Maurice Massar 编写。此帮助页根据 Wolfram Sang `ninja(at)the-dreams.de` 编写的 `pcf2vpnpc` 帮助页由 Jürgen Mayer 编写。

根据 GNU 通用许可许可证第 2 版或自由软件基金发布的任何后续版本，允许复制、分发和/或修改本文档。

在 Debian 系统上，GNU 通用许可许可证的全文可以在 `/usr/share/common-licenses/GPL` 找到。

### 参见

`vpnc(8)` `pcf2vpnc(1)`

## 名称

`cksum` - 计算文件的校验和并统计字节数

### 概要

```
cksum [FILE]... cksum [OPTION]
```

### 描述

打印每个 `FILE` 的 CRC 校验和和字节数。

- `-help`

  显示此帮助并退出

- `-version`

  输出版本信息并退出

### 作者

由 Q. Frank Xia 编写。

# 报告错误

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 请向 <http://translationproject.org/team/> 报告 `cksum` 翻译错误。

# 版权所有

Copyright © 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL 3 或更高版本 <http://gnu.org/licenses/gpl.html>。这是免费软件：你可以自由地更改和重新发布它。在法律允许范围内不提供任何保证。

### 参见

完整文档位于：<http://www.gnu.org/software/coreutils/cksum> 或通过本地可用：info ‘coreutils’ `cksum` invocation’

`clear` - 清除终端屏幕

### 概要

`clear`

### 描述

`clear` 如果可能，它会清除你的屏幕，包括其回滚缓冲区（如果定义了扩展“E3”功能）。`clear` 在环境变量中查找终端类型，然后在 `terminfo` 数据库中确定如何清除屏幕。

`clear` 会忽略任何可能存在的命令行参数。

### 参见

`tput(1)`, `terminfo(5)`

本文描述的是 ncurses 版本 5.9（补丁 20150214）。

## 名称

`cmp` - 逐字节比较两个文件

### 概要

```
cmp [OPTION]... FILE1 [FILE2 [SKIP1 [SKIP2]]]
```

### 描述

逐字节比较两个文件。

可选的 `SKIP1` 和 `SKIP2` 指定了每个文件开头跳过的字节数（默认 零）。

长选项的强制性参数对于短选项也是强制的。

- `-b`, `--print-bytes`

  打印不同的字节

- `-i`, `--ignore-initial=SKIP`

  跳过两个输入的前的前 `SKIP` 个字节

- `-i`, `--ignore-initial=SKIP1:SKIP2`

  跳过 `FILE1` 的前 `SKIP1` 个字节和 `FILE2` 的前 `SKIP2` 个字节

- `-l`, `--verbose`

  输出字节数和不同的字节值

- `-n`, `--bytes=LIMIT`

  最多比较 `LIMIT` 个

- `-s`, `--quiet`, `--silent`

  抑制所有正常输出

- `--help`

  显示此帮助并退出

- `-v`, `--version`

  输出版本信息并退出

`SKIP` 值可以跟随以下乘法后缀：`kB 1000`, `K 1024`, `MB 1,000`。

### 作者

由 Bjorn Granlund 和 David MacKenzie 编写。

# 报告错误

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 请向 <http://translationproject.org/team/> 报告 `cksum` 翻译错误。

# 版权所有

Copyright © 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL 3 或更高版本 <http://gnu.org/licenses/gpl.html>。这是免费软件：你可以自由地更改和重新发布它。

### 参见

`diff(1)`, `diffutils(1)`

为提供的消息生成并输出一个签名收据。输入消息必须包含签名收据请求。在其他功能上与 `-sign` 操作相似。

## `-verify_receipt receipt`

验证文件名为 `receipt` 的签名收据。输入消息必须包含原始收据请求。在其他功能上与 `-verify` 操作类似。

## `-in filename`

要进行加密或签名的输入消息，或者要进行解密或验证的消息。

## `-inform SMIME|PEM|DER`

这指定了 CMS 结构的输入格式。默认为 SMIME，即读取 S/MIME 格式的消息。PEM 和 DER 格式会更改为期望内部包含 PEM 和 DER 格式结构。这目前仅影响 CMS 结构的输入格式，如果没有处理 CMS 结构（例如使用 `-encrypt` 或 `-sign`），则此选项将不起作用。

## `-rctform SMIME|PEM|DER`

指定与 `-receipt_verify` 操作配合使用的签名收据格式。

## `-out filename`

已解密或经过验证的消息正文，或者已签名或经过验证的输出 MIME 格式消息。

## `-outform SMIME|PEM|DER`

这指定了 CMS 结构的输出格式。默认为 SMIME，即写入 S/MIME 格式的消息。PEM 和 DER 格式会更改为写入 PEM 和 DER 结构。这目前仅影响 CMS 结构的输出格式，如果没有输出 CMS 结构（例如使用 `-verify` 或 `-decrypt`），则此选项将不起作用。

## `-stream -indef -noindef`

`-stream` 和 `indef` 选项等效，用于开启编码操作流式 I/O。这允许流式处理数据而无需将整个内容保存在内存中，可能支持非常大的文件。对于分离数据的 S/MIME 签名，如果输出格式为 SMIME，目前会自动设置流式；所有其他操作默认都是关闭的。

## `-noindef`

禁用产生无限长度构造编码的流式 I/O。此选项不起作用。未来所有相关选项都将启用流式传输，而此选项将禁用它。

## `-content filename`

这指定一个包含分离内容的文件，这仅对 verify 命令有用。只有当 CMS 结构使用不包含内容的分离签名形式时才可用。如果输入格式是 S/MIME 且使用了 multipart/signed MIME 内容类型，此选项将覆盖任何内容。

## `-text`

在加密或签名时，此选项为提供的消息添加纯文本（text/plain）MIME 头。在解密或验证时剥离文本头：如果解密或验证的消息 MIME 类型不是 text/plain，则会发生错误。

- `-nout`

对于 `-cmsout` 操作，不输出解析后的 CMS 结构。这在与 `-print` 选项结合使用或检查 CMS 结构的语法时非常有用。

- `-print`

对于 `-cmsout` 操作，打印 CMS 结构的所有字段。这主要用于测试目的。

- `-CAfile`

包含受信任的 CA 证书的文件，仅用于 `-verify`。

- `-CApath dir`

包含受信任的 CA 证书的目录，仅用于 `-verify`。该目录必须是标准的证书目录：即每个主题名的哈希值（使用 `x509-hash` 计算）应链接到每个证书上。

- `-trusted_first`

在验证证书的信任链时，先使用 CA 文件或 CA 目录中的证书，后使用消息中不受信任的证书。这在具有桥接 CA 或交叉认证 CA 的环境中主要有用。

- `-md digest`

签名或重新签名时使用的摘要算法。如果不存在，将使用签名密钥的默认摘要算法（通常为 `sha1`）。

- `-cipher`



使用的加密算法。例如，三重 DES（168 位）`-des3` 或 256 位 AES `-aes256`。任何标准算法名称（如 `EVP_get_ciphername()` 函数使用的名称）前面也可以加一个连字符，例如 `-aes_128_chc`。查看 `enc` 以获取你版本 `OpenSSL` 支持的加密算法列表。如果未指定，则使用三重 DES。仅用于 `-encrypt` 和 `-EncryptedData_create` 命令。

- `-nointern`

在验证消息时，通常会搜索消息中包含的（如果有）证书以寻找签名证书。使用此选项时，仅使用 `-cert` 选项中指定的证书。然而，提供的证书仍可以作为不受信任的 CA 使用。

- `-no_signer_cert_verify`

不验证签名消息的签名者证书。

- `-noattr`

通常在消息签名时，会包含一组属性，包括签名时间和支持的对称算法。使用此选项时将不包含这些属性。

- `-nosmimecap`

从签名属性中排除支持的算法列表，签名时间和内容类型等其他选项仍会被包含。

`-binary`

通常输入消息会被转换为“规范”格式，实际上是使用 CR 和 LF 作为行尾：符合 S/MIME 规范的要求。当此选项存在时，不发生转换。这在处理可能不是 MIME 格式的二进制数据时有用。

- `-notach`

签名消息时使用不透明签名：这种形式更能抵抗邮件中继的翻译，但无法不支持 S/MIME 的邮件代理读取。如果没有此选项，将使用 MIME 类型为 `multipart/signed` 的明文签名。

- `-certfile`

允许指定额外的证书。签名时这些证书将包含在消息中。验证时将搜索这些证书作为签名者证书。证书应该是 PEM 格式。

- `-certsfile`

消息中包含的任何证书。

- `-inkey file`

签名或解密时使用的私钥。它必须与相应的证书匹配。如果未指定此选项，私钥必须包含在用 `-rec` 或 `-signer` 指定证书文件中。签名时可以多次使用此选项来指定连续的密钥。

# 注意事项

MIME 消息在头部（headers）和输出之间不能有任何空行。某些邮件程序会自动添加空行。直接将邮件管道传输到 `sendmail` 是实现正确格式的方法之一。

提供的待签名或待加密消息必须包含必要的 MIME 头部，否则许多 S/MIME 客户端将无法正常显示它（或者根本不显示）。你可以使用 `-text` 选项自动添加文本头部。

“签名并加密”的消息是指先对消息进行签名然后进行加密的消息。这可以通过对已签名的消息进行加密来实现：请参见示例部分。

此版本的程序每条消息允许一个签名者，但它可以验证多个签名者。如果消息包含多个签名者，某些 S/MIME 客户端可能会崩溃。通过对已签名的消息再次签名，可以“并行”签名消息。

`-encrypt` 和 `-decrypt` 选项反映了 S/MIME 客户端中的常用用法。严格来说，这些选项处理的是 CMS 封装数据：CMS 加密数据用于其他用途。

`-sign` 选项在添加新签名者时会使用现有的消息摘要。这意味着至少有一个使用相同消息摘要的签名者必须包含属性，否则该操作将失败。

`-stream` 和 `-indef` 选项启用了实验性的流式 I/O 支持。结果编码是无限长度构造编码的 BER，而不再是 DER。如果内容不是分离的，则 `-encrypt` 操作和 `-sign` 操作支持流式传输。

对于带有分离数据的 `-sign` 操作始终使用流式传输，但由于内容不再是 CMS 结构的一部分，编码保持为 DER。

如果在没有接收者证书的情况下使用 `-decrypt` 选项，程序将尝试通过提供的私钥逐个尝试接收者来定位接收者。为了防止 MMA 攻击（Bleichenbacher 对 PKCS #1 v1.5 RSA 填充的攻击），无论成功与否都会尝试所有接收者，如果没有匹配的接收者，则使用随机密钥对消息进行“解密”，这通常会输出垃圾数据。

可以使用 `-debug_decrypt` 选项禁用 MMA 攻击保护，并在找不到接收者时返回错误：此选项应谨慎使用。更详细的描述请参见 `CMS_decrypt(3)`。

# 退出状态

```
0 操作完全成功。
1 解析命令选项时发生错误。
2 无法读取其中一个输入文件。
3 创建 CMS 文件或读取 MIME 消息时发生错误。
4 解密或验证消息时发生错误。
5 消息验证正确，但在输出签名者证书时发生错误。
```

# 与 PKCS#7 格式的兼容性

`smime` 工具只能处理旧的 PKCS#7 格式。`cms` 工具支持加密消息语法（CMS）格式。使用某些功能将导致消息无法被仅支持旧格式的应用程序处理。细节下所示：

- 在 `-sign` 或 `-encrypt` 中使用 `-keyid` 选项。

- `-outform PEM` 选项使用了不同的头部。

- `-compress` 选项。

- 与 `-encrypt` 使用 `-secretkey` 选项。

- 在 `-sign` 中使用 PSS。

- 在 `-encrypt` 中使用 OAEP 或非 RSA 密钥。

此外，旧的 `smime` 命令无法处理 `-EncryptedData_create` 和 `-data_create` 类型。

## 示例

创建一个明文签名消息：

`openssl cms -sign -in message.txt -text -out mail.msg -signer mycert.pem`

创建一个不透明签名消息：

`openssl cms -sign -in message.txt -text -out mail.msg -nodetach -signer mycert.pem`

创建一个签名消息，包含一些额外的证书并从另一个文件读取私钥：

`openssl cms -sign -in in.txt -text -out mail.msg -signer mycert.pem -inkey mykey.pem -certfile mycerts.pem`

创建一个具有两个签名者的签名消息，使用密钥标识符：

`openssl cms -sign -in message.txt -text -out mail.msg -signer mycert.pem -signer othercert.pem -keyid`

在 Unix 下直接将签名消息发送到 sendmail，包含头部：

`openssl cms -sign -in in.txt -text -signer mycert.pem -from steve@openssl.org -to someone@somewhere -subject "Signed message" sendmail@somewhere`

成功验证并提取签名者证书：

`openssl cms -verify -in mail.msg -signer user.pem -out signedtext.txt`

使用三 DES 发送加密邮件：

`openssl cms -encrypt -in in.txt -from steve@openssl.org -to someone@somewhere -subject "Encrypted message" -des3 user.pem mail.msg`

签名并加密邮件：

`openssl cms -sign -in ml.txt -signer mycert.pem -text | openssl cms -encrypt out mail.msg -from steve@openssl.org -to someone@somewhere -subject "Signed and Encrypted message"`

注意：加密命令不包含 `-text` 选项，因为被加密的消息已经有了 MIME 头部。

解密邮件：

`openssl cms -decrypt -in mail.msg -recip mycert.pem -inkey key.pem`

Netscape 生成的是带有分离签名格式的 PKCS#7 结构。你可以通过对 base64 编码结构进行换行并包含以下内容来使用此程序验证签名：

```
-----BEGIN PKCS7-----
-----END PKCS7-----
```

# 选项与参数

选项

选项指定操作。参数修改操作。`cmsutl` 命令的选项和参数定义如下：

- `-C`

加密消息。

- `-D`

解码消息。

- `-E`

封装消息。

- `-O`

创建一个仅包含证书的消息。

- `-S`

对消息签名。

### 参数

选项参数修改操作。

- `-b`

解码 `infile` 中命名的批处理文件。

- `-c content`

使用此离线内容（仅解码）。

- `-d dbdir`

指定密钥/证书数据库目录（默认为 `.`）。

- `-e envfile`

指定一个包含封装消息的文件，该消息对应一组您想要发送加密消息的接收者。如果这是发给该组接收者的第一条加密消息，则会创建一个新的封装消息，随后您可以将其用于后续的（（仅加密）。

- `-f pwfile`

使用密码文件为所有 PKCS#11 令牌设置密码。

- `-G`



包含签名时间属性（仅签名）。

- `-H` `hash`

  使用指定的哈希算法（默认：`SHA1`）。

- `-h` `num`

  生成带有 CMS 消息信息的邮件头信息（仅解码）。

- `-i` `infile`

  使用 `infile` 作为数据源（默认是 `stdin`）。

- `-k`

  将解码后的加密证书保留在永久证书数据库中。

- `-N` `nickname`

  指定用于签名证书别名（仅签名）。

- `-n`

  抑制内容输出（仅解码）。

- `-o` `outfile`

  使用 `outfile` 作为数据目标（默认是 `stdout`）。

- `-P`

  包含 S/MIME 能力属性。

- `-p` `password`

  使用密码作为密钥数据库密码。

- `-r` `recipient1,recipient2, ...`

  指定加密或封装消息的接收者列表（电子邮件地址）。对于仅证书的消息，列出要发送的证书列表。

- `-T`

  抑制 CMS 消息中的内容（仅签名）。

- `-u` `certusage`

  设置证书用途类型（默认是 `certUsageEmailSigner`）。

- `-v`

  打印调试信息。

- `-Y` `ekprefnick`

  通过别名指定加密密钥偏好。

# 使用方法

## 加密示例

```
cmsutil -C [-i infile] [-o outfile] [-d dbdir] [-p password] -r "recipient1, recipient2, . ." -e envfile
```

## 解码示例

```
cmsutil -D [-i infile] [-o outfile] [-d dbdir] [-p password] [-c content] [-n] [-h num]
```

## 封装示例

```
cmsutil -E [-i infile] [-o outfile] [-d dbdir] [-p password] -r "recipient1, recipient2,..."
```

## 仅证书示例

```
cmsutil -o [-i infile] [-o outfile] [-d dbdir] [-p password] -r "cert1, cert2, . ."
```

## 签名消息示例

```
cmsutil -S [-i infile] [-o outfile] [-d dbdir] [-p password] -N nickname[-TGP] [-Y ekprefnick]
```

# 相关阅

`certutil(1)`

# 更多资源

有关 NSS 和其他与 NSS 相关工具（如 JSS）的信息，请查看 NSS 项目的 wiki：`http://www.mozilla.org/projects/security/pki/nss/`。NSS 站点与 NSS 代码更改和发布直接相关。

邮件列表：`https://lists.mozilla.org/listinfo/dev-tech-crypto`

IRC：Freenode `#dogtag-pki`

NSS 工具由来自 Netscape、Red Hat、Sun、Oracle、Mozilla 和 Google 的开发者编写并维护。

作者：Elio Maldonado `<emaldona@redhat.com>`, Deon Lackey `<dlackey@redhat.com>`。

# 许可证

根据 Mozilla Public License v. 2.0 授权。如果此文件未分发 MPL 副本，您可以在 `http://mozilla.org/MPL/2.0` 获取。

# 注意事项

1. Mozilla NSS bug 836477

`https://bugzilla.mozilla.org/show_bug.cgi?id=836477`

# col - 从输入中过滤反向换行符

### 概要

```
col [options]
```

### 描述

`col` 过滤掉反向（以及半反向）换行符，使输出顺序正确，仅保留正向和半正向换行符。它还可能将任何空白字符替换为制表符。这在处理 `nroff(1)` 和 `tbl(1)` 的输出时非常。

`col` 从标准输入读取并写入到标准输出。

### 选项

- `-b`, `--no-backspaces`

  不输出任何退格符，仅打印每个列位置写入的最后一个字符。

- `-f`, `--fine`

  允许半正向换行符。通常情况下，用于半行边界的字符将打印在下一行。

- `-h`, `--tabs`

  输出制表符代替多个空格。

- `-l`, `--lines` `number`

  在内存中缓冲至少 `number` 行。

- `-p`, `--pass`

  透传未知的控制序列。

- `-x`, `--spaces`

  输出多个空格而非制表符。

- `-V`, `--version`

  显示版本信息并退出。

- `-h`, `--help`

  显示帮助文本并退出。

# 注意事项

`col` 识别的控制序列如下所示：

| 序列 | 描述 |
| :--- | :--- |
| ESC 7 | 反向换行符 |
| ESC 8 | 半换行符 |
| ESC 9 | 正向换行符 |
| ESC 10 | 新行符 |
| ESC 11 | 移入 |
| ESC 12 | 移出 |
| ESC 13 | 回车符 |
| ESC 14 | 移出 |
| ESC 15 | 制表符 |
| ESC 16 | 退格 |
| ESC 32 | 空格 |
| ESC 33 | 垂直制表符 |

`col` 在处理未知控制序列时将其丢弃。它在读取字符时跟踪字符集，并在输出时确保是正确的。

# 相关阅览

`col(1)`

# 标准

`col` 符合单 Unix 规范（Single UNIX Specification）第2版。`-l` 选项是一个扩展。

# 历史

`col` 命令出现于 AT&T 版本 6。

# 可用性

`col` 是 `util-linux` 的一部分，可在 Linux Archive 获取。

## 名称

`colcrt` - 用于 预览的 nroff 输出

### 概要

```
colcrt [options] [file...]
```

### 描述

`colcrt` 为不支持此类功能的终端提供虚拟半行和反向传输序列，并且对于这些终端覆盖操作是破坏性的。半行字符和下划线（更改为 ~）被放置在正常行之间的。

### 选项

- `--no-underlining`

  抑制所有下划线。此选项对于预览 `tbl(1)` 的表格特别有用。

- `-2,--half-lines`

  强制打印所有半行，实际上使输出双倍行距。通常使用的最小空间输出会抑制空行。然而，程序永远不会抑制两个空行。当输出包含否则将不可见的上标和下标时，`-2` 选项非常有用。

- `-V,--version`

  显示版本信息并退出。

- `-h,--help`

  显示帮助文本并退出。

## 示例

```
tbl exum2.n | nroff -ms | colcrt - | more
```

# 相关阅览

`nroff(1)`, `troff(1)`, `col(1)`, `more(1)`, `ul(1)`

# Bug

即使开启选项，也应将下划线折叠到空白处，以便显示真实的下划线。无法备份超过 102 行。通用覆盖丢失；作为特殊情况，'|' 被 '-' 或下划线覆盖后变为'+'。行被裁剪为 132 个字符。对于已经是双倍行距的文档，处理上标和下标应采取某些措施。

# 历史

`colcrt` 命令出现于 3.0BSD。

# 可用性

`colcrt` 命令是 `util-linux` 软件包的一部分，可在 Linux Archive 获取。

## 名称

`colormgr` - 颜色管理器测试工具

# SYNOPSIS

```
colormgr [ --verbose ] [ --version ]
```

# DESCRIPTION

本手册页简要介绍了 `colormgr` 命令。

`colormgr` 允许管理员查看和更改颜色配置文件到设备的映射。

# OPTIONS

此程序遵循标准的 GNU 命令行语法，长选项以两个短横线 (`--`) 开头。下方列出了选项摘要。

`--help`

- 显示选项摘要。

# COMMANDS

此程序接受带有数量参数的命令。

- `create-device`

  创建设备

- `create-profile`

  创建配置文件

- `delete-device`

  删除设备

- `delete-profile`

  删除配置文件

- `device-add-profile`

  向已存在的设备添加配置文件

- `device-get-default-profile`

  获取设备的默认配置文件

- `device-get-profile-for-qualifier`

  返回所有匹配限定符的配置文件

- `device-inhibit`

  抑制此设备的颜色配置文件

- `device-make-profile-default`

  将配置文件设置为设备的默认配置

- `device-set-enabled`

  启用或禁用设备

- `device-set-kind`

  设置设备类型

- `device-set-model`

  设置设备型号



# device-set-serial
设置设备序列号

# device-set-vendor
设置设备供应商

# find-device
根据设备 ID 查找设备

# find-device-by-property
根据给属性值查找设备

# find-profile
根据配置文件 ID 查找配置文件

# find-profile-by-filename
通过文件名查找配置文件

# get-devices
获取所有颜色管理的设备

# get-devices-by-kind
获取所有特定类型的颜色管理设备

# get-profiles
获取所有可用的颜色配置文件

# get-sensor-reading
获取传感器的读数

# get-sensors
获取所有可用的颜色传感器

# get-standard-space
获取标准色彩空间

# import-profile
将 `.icc` 文件复制到正确的用户目录中，并显示有关导入的配置文件的信息。

# profile-set-property
在配置文件上设置额外属性

# sensor-lock
锁定颜色传感器

# sensor-set-options
设置一个或多个传感器选项

# AUTHOR
本手册页由 Richard Hughes `<richard@hughsie.com>` 编写。

# NAME
`colrm` - 从文件中删除列

# SYNOPSIS
```
colrm [first [last]]
```

# DESCRIPTION
`colrm` 从文件中删除选定的列。输入来自标准输入。输出发送到标准输出。

如果调用时带有一个参数，将从指定的第一个列开始删除每行的列。如果带有两个参数调用，将删除从第一列到最后一列的列。

列编号从第 1 列开始。

# OPTIONS
+ `-V`, `--version`
显示版本信息并退出。

+ `-H`, `--help`
显示帮助文本并退出。

# SEE ALSO
`awk(1)`, `column(1)`, `expand(1)`, `paste(1)`

# HISTORY
`colrm` 命令出现于 3.0BSD。

# AVAILABILITY
`colrm` 命令是 util-linux 软件包的一部分，可在 Linux 内核存档获取。

# NAME
`column` - 将列表列化

# SYNOPSIS
```
column [options] [file...]
```

# DESCRIPTION
`column` 工具将其输入格式化为多列。默认情况下，先填充行再填充列。输入来自文件，或来自标准输入。忽略空行。

# OPTIONS
`-c`, `--columns width`
输出格式化为指定字符数量的宽度。

`-o`, `--output-separator string`
指定表格输出的列分隔符（默认为两个空格）。

`-S`, `--separator separators`
指定可能的输入项分隔符（默认为空白符）。

`-t`, `--table`
确定输入包含的列数并创建表格。列由空白符分隔，或使用 `--output-separator` 选项提供的字符分隔。表格输出对于美化打印非常有用。

`-x`, `--fillrows`
在填充行之前先填充列。

`-V`, `--version`
显示版本信息并退出。

`-h`, `--help`
显示帮助文本并退出。

# ENVIRONMENT
在没有其他可用信息时，使用环境变量 `COLUMNS` 来确定屏幕尺寸。

# EXAMPLES
```
sed 's/##.*//' /etc/fstab | column -t
```

# BUGS
版本 2.23 将 `-s` 选项更改为非贪婪模式，例如：
```
printf "a:b:c" | column -s ':'
```

# SEE ALSO
`awk(1)`, `column(1)`, `expand(1)`

# HISTORY
`colrm` 命令出现于 3.0BSD。

# AVAILABILITY
`column` 命令是 util-linux 软件包的一部分，可在 Linux 内核存档获取。

# NAME
`column` - 将列表列化

# SYNOPSIS
```
colormgr [ --verbose ] [ --version ]
```

# DESCRIPTION
本手册页简要介绍了 `colormgr` 命令。

`colormgr` 允许管理员查看和更改颜色配置文件到设备的映射。

# OPTIONS
此程序遵循标准的 GNU 命令行语法，长选项以两个短横线 (`--`) 开头。下方列出了选项摘要。

`--help`
+ 显示选项摘要。

# COMMANDS
此程序接受带有数量参数的命令。

- `create-device`
创建设备

- `create-profile`
创建配置文件

- `delete-device`
删除设备

- `delete-profile`
删除配置文件

- `device-add-profile`
向已存在的设备添加配置文件

- `device-get-default-profile`
获取设备的默认配置文件

- `device-get-profile-for-qualifier`
返回所有匹配限定符的配置文件

- `device-inhibit`
抑制此设备的颜色配置文件

- `device-make-profile-default`
将配置文件设置为设备的默认配置

- `device-set-enabled`
启用或禁用设备

- `device-set-kind`
设置设备类型

- `device-set-model`
设置设备型号

- `device-set-serial`
设置设备序列号

- `device-set-vendor`
设置设备供应商

- `find-device`
根据设备 ID 查找设备

- `find-device-by-property`
根据给属性值查找设备

- `find-profile`
根据配置文件 ID 查找配置文件

- `find-profile-by-filename`
通过文件名查找配置文件

- `get-devices`
获取所有颜色管理的设备

- `get-devices-by-kind`
获取所有特定类型的颜色管理设备

# get-profiles
获取所有可用的颜色配置文件

# get-sensor-reading
获取传感器的读数

# get-sensors
获取所有可用的颜色传感器

# get-standard-space
获取标准色彩空间

# import-profile
将 `.icc` 文件复制到正确的用户目录中，并显示有关导入的配置文件的信息。

# profile-set-property
在配置文件上设置额外属性

# sensor-lock
锁定颜色传感器

# sensor-set-options
设置一个或多个传感器选项

# AUTHOR
本手册页由 Richard Hughes `<richard@hughsie.com>` 编写。

# NAME
`colrm` - 从文件中删除列

# SYNOPSIS
```
colrm [first [last]]
```

# DESCRIPTION
`colrm` 从文件中删除选定的列。输入来自标准输入。输出发送到标准输出。

如果调用时带有一个参数，将从指定的第一个列开始删除每行的列。如果带有两个参数调用，将删除从第一列到最后一列的列。

列编号从第 1 列开始。

# OPTIONS
+ `-V`, `--version`
显示版本信息并退出。

+ `-H`, `--help`
显示帮助文本并退出。

# SEE ALSO
`awk(1)`, `column(1)`, `expand(1)`, `paste(1)`

# HISTORY
`colrm` 命令出现于 3.0BSD。

# AVAILABILITY
`colrm` 命令是 util-linux 软件包的一部分，可在 Linux 内核存档获取。

# NAME
`column` - 将列表列化

# SYNOPSIS
```
column [options] [file...]
```

# DESCRIPTION
`column` 工具将其输入格式化为多列。默认情况下，先填充行再填充列。输入来自文件，或来自标准输入。忽略空行。

# OPTIONS
`-c`, `--columns width`
输出格式化为指定字符数量的宽度。

`-o`, `--output-separator string`
指定表格输出的列分隔符（默认为两个空格）。

`-S`, `--separator separators`
指定可能的输入项分隔符（默认为空白符）。

`-t`, `--table`



确定输入包含的列数并创建表格。列由空白符分隔，或使用 `--output-separator` 选项提供的字符分隔。表格输出对于美化打印非常有用。

`-x`, `--fillrows`

在填充行之前先填充列。

`-V`, `--version`

显示版本信息并退出。

`-h`, `--help`

显示帮助文本并退出。

# ENVIRONMENT

在没有其他可用信息时，使用环境变量 `COLUMNS` 来确定屏幕尺寸。

# EXAMPLES

```
sed 's/##.*//' /etc/fstab | column -t
```

# BUGS

版本 2.23 将 `-s` 选项更改为非贪婪模式，例如：

```
printf "a:b:c" | column -s ':'
```

# SEE ALSO

`awk(1)`, `column(1)`, `expand(1)`

# HISTORY

`colrm` 命令出现于 3.0BSD。

# AVAILABILITY

`column` 命令是 `util-linux` 软件包的一部分，可在 Linux 内核存档获取。

# NAME

`column` - 将列表列化

# SYNOPSIS

```
consoletype [stdout] [fg]
```

# DESCRIPTION

`consoletype` 打印连接到标准输入的控制台类型，并检查连接到标准输入的控制台是否为前台虚拟控制台。无参数时，如果控制台是虚拟终端 (`/dev/tty*` 或非串口控制台下的 `/dev/console` 设备)，则打印 `vt`；如果标准输入是串口控制台 (`/dev/console` 或 `/dev/ttyS*`)，则打印 `serial`；如果标准输入是伪终端，则打印 `pty`。

# RETURN VALUE

`consoletype` 在未传递参数时返回：

```
0
  在虚拟终端上
1
  在串口控制台上
2
  在伪终端上
```

当传递 `stdout` 参数时，`consoletype` 返回：

```
0
  所有情况下，并将控制台类型打印到 stdout。
```

当传递 `-fg` 参数时，`consoletype` 返回：

```
0
  如果连接到标准输入的控制台是当前虚拟终端
1
  否则。
```

# EXAMPLES

```
sed 's/##.*//' /etc/fstab | column -t
```

# OPTIONS

支持以下选项：

`--no-legend`
不打印列标题。

`-l`
仅显示单个核心转储（coredump），而不是列出所有已知转储。

`-F`, `--field=`
打印日志中匹配的 coredump 条目中指定字段所取的所有可能数据值。

`-o`, `--output=FILE`
将 core 写入 `FILE.`。

`-h`, `--help`
打印简短的帮助文本并退出。

`--version`
打印简短的版本字符串并退出。

`--no-pager`
不将输出通过管道传输到分页器（pager）。

支持以下命令：

`list`
列出日志中捕获的匹配指定特征的 coredump。如果没有指定命令，则这是默认值。

`info`
显示日志中捕获的 coredump 的详细信息。

`dump`
提取匹配指定特征的最后一个 coredump。除非使用 `-o`/`--output` 指定了输出文件，否则 coredump 将写入标准输出。

`gdb`
在匹配指定特征的最后一个 coredump 上调用 GNU 调试器（gdb）。

# MATCHING

匹配可以是：
`PID`
转储 core 的进程 ID。一个整数。

`COMM`
可执行文件的名称（匹配 `COREDUMP_COMM=`）。不能包含斜杠。

`EXE`
可执行文件的路径（匹配 `COREDUMP_EXE=`）。必须包含至少一个斜杠。

`MATCH`
通用的 `journalctl` 谓词（参见 `journalctl(1)`）。必须包含一个等号。

# EXIT STATUS

成功时返回 `0`；否则返回非零失败代码。未找到任何匹配的 coredump 被视为失败。

# EXAMPLES

示例 1. 列出所有名为 `foo` 的程序的所有 coredump

```
# coredumpctl list foo
```

示例 2. 在最后一个 coredump 上调用 gdb

```
# coredumpctl gdb
```

示例 3. 根据 PID 6654 匹配显示转储 core 的进程信息

```
# coredumpctl info 6654
```

示例 4. 将 `/usr/bin/bar` 的最后一个 coredump 提取到名为 `bar.coredump` 的文件中

```
# coredumpctl -o bar.coredump dump /usr/bin/bar
```

# SEE ALSO

`systemd-coredump(8)`, `coredump.conf(5)`, `systemd-journald.service(8)`, `gdb(1)`

# NAME

`cp` - 复制文件和目录

# SYNOPSIS

```
cp [OPTION]... [-T] SOURCE DEST
cp [OPTION]... SOURCE... DIRECTORY
cp [OPTION]... -t DIRECTORY SOURCE...
```



# DESCRIPTION

将 `SOURCE` 到 `DEST`，或将多个 `SOURCE(s)` 复制到 `DIRECTORY`。
长选项的强制参数对于短选项也是强制的。

- `-a`, `--archive`
  同于 `-dR --preserve=all`
- `--attributes-only`
  不复制文件数据，仅复制属性
- `--backup=[CONTROL]`
  为每个存在的目标文件创建备份
- `-b`
  类似于 `--backup` 但不接受参数
- `--copy-contents`
  递归时复制特殊文件的内容
- `-d`
  同于 `--no-dereference --preserve=links`
- `-f`, `--force`
  如果无法打开已的目标文件，则将其删除并重试（当同时使用 `-n` 选项时忽略此选项）
- `-i`, `--interactive`
  在覆盖之前提示（覆盖之前的 `-n` 选项）
- `-H`
  遵循 `SOURCE` 中的命令行符号链接
- `-l`, `--link`
  创建硬链接而非复制
- `-L`, `--dereference`
  始终遵循 `SOURCE` 中的符号链接
- `-n`, `--no-clobber`
  不覆盖现有文件（覆盖之前的 `-i` 选项）
- `-P`, `--no-dereference`
  从不遵循 `SOURCE` 中的符号链接
- `-p`
  同于 `--preserve=mode,ownership,timestamps`
- `--preserve=[ATTR_LIST]`
  保留指定的属性（默认：模式、所有者、时间戳），如果指定了额外属性：内容、链接、扩展属性(xattr)、全部 `all`
- `-c`
  已废用，同于 `--preserve=context`
- `--no-preserve=ATTR_LIST`
  不保留指定的属性
- `--parents`
  在 `DIRECTORY` 下使用完整的源文件名
- `-R`, `-r`, `--recursive`
  递归复制目录
- `--relink=[WHEN]`
  控制 clone/CoW 复制。见下文
- `--remove-destination`
  在尝试打开现有目标文件之前将其删除（与 `--force` 相对比）
- `--sparse=WHEN`
  控制稀疏文件的创建。见下文
- `--strip-trailing-slashes`
  从每个 `SOURCE` 参数中删除任何尾部斜杠
- `-s`, `symbolic-link`
  创建符号链接而非复制
- `--S`, `suffix=SUFFIX`
  覆盖通常的备份后缀
- `--t`, `--target-directory=DIRECTORY`
  将所有 `SOURCE` 参数复制到 `DIRECTORY`
- `--T`, `--no-target-directory`
  将 `DEST` 视为普通文件
- `--u`, `--update`
  仅当 `SOURCE` 文件新于目标文件或目标文件缺失时才复制
- `--v`, `--verbose`
  解释正在执行的操作
- `--x`, `--one-file-system`
  留在你的文件系统上
- `--Z`
  将目标文件的 SELinux 安全上下文设置为默认类型
- `--context=[CTX]`
  类似于 `-Z`，或者如果指定了 `CTX` 则将 SELinux 上下文设置为 `CTX`
- `--help`
  显示此帮助
- `--version`
  输出版本信息

默认情况下，通过简单的启发式方法检测稀疏文件，相应的 `DEST` 文件也被制为稀疏。此行为由 `--sparse=auto` 选择。指定 `--sparse=always` 以在 `SOURCE` 文件包含长序列零字节时始终创建稀疏文件。使用 `--sparse=never` 抑制稀疏文件的创建。当 `--relink=[always]` 时...

稀疏文件通过一种粗略的启发式方法检测，相应的 `DEST` 文件也被制为稀疏。此行为由 `--sparse=auto` 选择。指定 `--sparse=always` 以在 `SOURCE` 文件包含长序列零字节时始终创建稀疏文件。使用 `--sparse=never` 抑制稀疏文件的创建。当 `--relink=[always]` 时...（注：此处原文似乎存在部分逻辑截断或重复，已按字面尽可能翻译）

# AUTHOR

由 `Torbjorn Granlund`, `David MacKenzie`, `Jim Meyer` 编写。

# REPORTING

向 `bug-report.gnu.org` (`http://bug-report.gnu.org`) 报告 错误。

# COPYRIGHT

`Copyright © 2015 GNU Foundation.` 许可证 `GPL3+`: `http://www.gnu.org/licenses/`

# SEE ALSO

`systemd-coredump(8)`, `coredump.conf(5)`, `systemd-journald.service(8)`, `gdb(1)`

# WARNING

稀疏文件通过一种粗略的启发式方法检测，相应的 `DEST` 文件也被制为稀疏。此行为由 `--sparse=auto` 选择。指定 `--sparse=always` 以在 `SOURCE` 文件包含长序列零字节时始终创建稀疏文件。使用 `--sparse=never` 抑制稀疏文件的创建。当 `--relink=[always]` 时...（注：此处原文似乎存在部分逻辑截断或重复，已按字面尽可能翻译）

### 描述

`GNU cpio` 是一个创建和提取归档，或将文件从一个地方复制到另一个地方工具。它可以处理多种 `cpio` 格式，以及读写 `tar` 文件。

支持以下归档格式：`binary`、`old ASCII`、`new ASCII`、`crc`、`HPUX binary`、`HPUX old ASCII`、`old tar` 和 `POSIX.1 tar`。提供 `tar` 格式是为了与 `tar` 程序兼容。默认情况下，`cpio` 创建 `binary` 格式归档，以兼容旧版本的 `cpio` 程序。从归档中提取时，`cpio` 会自动识别正在读取哪种归档，并可以读取在不同字节序机器上创建的归档。

### 选项

- `-0`, `--null`
  读取以空字符终止的文件列表，而不是换行符，这样包含换行符的文件名就可以被归档。`GNU find` 是产生空字符终止文件名列表的一种方法。此选项可以在拷贝输出（copy-out）和拷贝透传（copy-pass）模式下使用。

- `-a`, `--reset-access-time`
  在读取文件后重置其访问时间，使其看起来不像刚刚被读取过。

- `-A`, `--append`
  附加到现有归档中。仅在拷贝输出模式下有效。归档必须是使用 `-O` 或 `-F` (`-file`) 选项指定的磁盘文件。

- `-b`, `--swap`
  交换数据中半部分的单词和半部分的字节。等同于 `-s`。此选项可以在拷贝输入（copy-in）模式下使用。使用此选项在大端和小端端机器之间转换 32 位整数。

- `-B`, `--block-size=BLOCK-SIZE`
  将 I/O 块大小设置为 5120 字节。初始块大小为 512 字节。

- `-c`, `--IO-size=IO-SIZE`
  相当于 `"-H newc"`，使用新的 (svr4) 可移植格式。如果你想要旧的可移植 (ASCII) 归档格式，请使用 `"-H doc"`。

- `-d`, `--make-directories`
  在需要的地方创建领先目录。

- `-E FILE`, `--pattern-file`
  从 `FILE` 读取额外的参数，指定要提取或列出的文件名。`FILE` 的每一行被视为作为 `cpio` 的非选项参数。此选项用于拷贝输入模式。

- `-f`, `--nonmatching`
  只拷贝不匹配任何给定模式的文件。

- `-F`, `--file-archive`
  使用归档文件名代替标准输入或输出。若要使用另一台机器上的磁带作为归档，请使用以 `.` 开头的文件名。`hostname` 前可以加上用户名和 `hostname@` 以该用户身份访问远程磁带，前提是你有相应权限（通常是用户 `~/.hosts` 文件中的条目）。

- `-force-local`
  配合 `-F`、`-I` 或 `-O` 使用时，即使归档文件名包含冒号（这通常表示远程主机名），也将该归档文件名视为本地文件。

- `-H FORMAT`, `--format=FORMAT`
  使用归档格式 `FORMAT`。有效格式列在下方；全大写名称也被识别。拷贝输入模式下默认自动检测归档格式，拷贝输出模式下默认默认为 `bin`。

  - `bin`
    过时的二进制 格式。
  - `odc`
    旧的 (POSIX.1) 可移植格式。
  - `newc`
    新的 (svr4) 可移植格式，支持具有超过 65536 个 i 节点的节点系统。
  - `crc`
    带有校验和 (Sum32) 的新的 (svr4) 可移植格式。
  - `tar`
    旧的 tar 格式。
  - `ustar`
    POSIX.1 tar 格式。也识别与 GNU tar 相似但不完全相同的归档。
  - `hpbin`
    HPUX cpio 使用的二进制二进制格式。
  - `hpodc`
    HPUX cpio 使用的可移植格式（存储文件的方式不同）。

- `-i`, `--extract`
  以拷贝输入模式运行。

- `-I archive`
  使用归档文件名代替标准输入。若要使用另一台机器上的磁带作为归档，使用以 `@` 开头的文件名。`hostname` 前可以加上用户名和 `:` 以该用户身份访问远程磁带，前提是你有相应权限（通常是用户 `~/.hosts` 文件中的条目）。

- `-k`
  忽略；用于兼容其他版本的 `cpio`。

- `-l`, `--link`
  可能时链接文件而不是拷贝它们。

- `-L`, `--dereference`
  拷贝符号链接指向的文件，而不是符号链接本身。

- `-m`, `--preserve-modification-time`
  创建文件时保留之前的修改时间。

- `-M MESSAGE`, `--message=MESSAGE`
  当备份介质（如磁带或软磁盘）卷结束时打印 `MESSAGE`，提示用户插入新卷。如果 `MESSAGE` 包含字符串 `"%d"`，会被当前卷号（从 1 开始）替换。

- `-n`, `--numeric-uid-gid`
  使用时显示数字的 UID 和 GID，而不是将其转换为名称。

- `no-absolute-filenames`
  在拷贝模式下相对于当前目录创建所有文件，即使归档中有绝对文件名。

- `absolute-filenames`（默认）
  在拷贝输入模式下，删除文件名中包含 `".."` 和领先斜杠的部分。

- `no-preserve-owner`
  不更改文件的所有权；由用户所有。这是非 root 用户的默认设置，防止 System V 用户意外泄露文件。

- `-o`, `--create`
  以拷贝输出模式运行。参见“拷贝输出模式”。

- `-O archive`
  使用归档文件名代替标准输出。若要使用另一台机器上的磁带作为归档，使用以 `'` 开头的文件名。`hostname` 前可以加上用户名和 `hostname@` 以该用户身份访问远程磁带，前提是你有相应权限（通常是用户 `~/.hosts` 文件中的条目）。

- `-only-verify-crc`
  读取 `crc` 格式时，验证归档中每个文件的 Sum32 校验和。不提取文件。

- `-p`, `--pass-through`
  以拷贝透传模式运行。参见“拷贝透传模式”。

- `-quiet`
  不打印拷贝的块数。

- `-r`, `--rename`
  交互式重命名文件。

- `-R [user][group]`, `--owner [user][group]`
  在拷贝输出和拷贝透传模式下，将创建的所有文件的所有设置为指定的用户或组。如果省略组，超级用户可以更改。

- `-rsync-command=COMMAND`
  通知 `cpio` 应使用 `rsync` 与远程设备通信。

- `-s`, `--swap-bytes`
  交换文件中每个半部分（字节对）的字节。此选项可以在拷贝输入模式下使用。

- `-S`, `--swap-halfwords`
  交换文件中每个字（4字节）的半字。此选项可以在拷贝输入模式下使用。

- `-sparse`
  将带有大块零的文件写入稀疏文件。此选项用于拷贝输入和拷贝透传模式。

- `-t`, `--list`
  打印输入的内容的目录列表。

- `--stdout`
  将文件提取到标准输出。此选项可以在拷贝输入模式下使用。

- `-u`, `--conditional`
  替换所有文件，在不询问的情况下用旧文件替换现有文件。

- `-v`, `--verbose`
  列出进程，或配合 `-t` 提供 `ls -l` 风格的目录列表。在 `ustar` 归档的详细目录列表中，归档中本地系统不存在的用户和组名将被替换为本地对应于存储的数字 UID 和 GID 的名称。

- `-V`, `--dot`
  为每个处理的文件打印一个 `"."`。

- `-W`, `--warning`
  控制警告显示。目前 `FLAG` 为 `''`、`'truncate'`、`'all'` 之一。多个选项可累积。

- `--license`
  打印许可协议并退出。

- `--help`
  提供与此帮助页相似的帮助页面。

- `--usage`
  提供短的用法信息。

- `--version`
  打印 `cpio` 程序版本号并退出。

## 示例

创建归档时，`cpio` 从标准输入获取要处理的文件列表，然后将归档发送到标准输出或由 `F` 选项指定的设备。通常使用 `find` 或 `ls` 向标准输入提供此列表。在下面的示例中，你可以看到归档单个目录内容的可能性。

```



`% ls | cpio -ov > directory.cpio`

`-o` 选项创建归档，`-v` 选项在归档时打印文件名。注意选项可以组合为 `-ov`，也可以分开放在命令行中。`>` 将 `cpio` 的输出重定向到文件 `directory.cpio`。

如果你想归档整个目录，可以使用 `find` 命令为 `cpio` 提供文件列表：

```
% find . -depth | cpio -ov > tree.cpio
```

这将把当前目录中的所有文件放入归档 `tree.cpio` 中。再次 `-o` 创建归档，`-v` 选项显示归档时的文件名。参见“拷贝输出模式”。

提取归档需要更多的思考，因为 `cpio` 默认不创建目录。另一个特性是，除非你指示，否则它不会覆盖现有文件。

```
% cpio -iv < directory.cpio
```

这将检索 `directory.cpio` 中的归档文件并将其放在当前目录。`-i` 选项提取归档，`-v` 显示提取时的文件名。如果你处理的是归档树，你需要使用 `-d` 选项在需要时创建目录，如下：

```
% cpio -idv < tree.cpio
```

这将提取 `tree.cpio` 的内容提取到当前目录。

# `% find . -depth -print0 | cpio -null -pvd new-dir`

该示例展示了将当前目录及其子目录拷贝到名为 `new-dir` 的新目录。某些选项包括 GNU `find` 提供的 `-print0`，与 `cpio` 的 `-null` 选项结合使用。这两个选项共同作用，用于在 `find` 和 `cpio` 之间传递文件名，即使文件名中包含特殊字符。另一个是 `-p`，它告诉 `cpio` 将找到的文件传递到目录 `new-dir`。

# 故障

GNU 的人们通常非常厌恶 man页（man pages），转而创建 info 文档。`cpio` 的维护者也属于这一类。因此，此 man 页可能是不完整的，也不是最新的，它被包含在 Red Hat 的 CVS 树中是因为 man 是一个非常强大的工具 :);

# 报告错误

请通过 https://bugzilla.redhat.com 报告错误。

# 另请

`cpio` 的完整文档作为 Texinfo 手册维护。如果你的站点上正确安装了 `info` 和 `cpio` 程序，执行命令

```
info cpio
```

应该可以让你访问完整的手册。文档的在线副本可在以下地址：

http://www.gnu.org/software/cpio/manual

## 名称

`crl` - CRL 实用

### 摘要

`openssl crl [-inform PEM|DER] [-outform PEM|DER] [-text] [-in filename] [-out filename] [-nameopt option] [-noout] [-hash] [-issuer] [-lastupdate] [-nextupdate] [-CAfile file] [-CApath dir ]`

### 描述

`crl` 命令处理 DER 或 PEM 格式的 CRL 文件。

### 命令选项

`-inform DER|PEM`

指定输入格式。`format` 为 DER 编码的 CRL 结构。PEM（默认）是 DER 形式的 base64 编码版本，带有页眉和页脚行。

`-output DER|PEM`

指定输出格式，与 `-inform` 选项含义相同。

`-in filename`

指定要读取的输入文件名，如果指定了此选项则从标准输入读取。

`-out filename`

指定写入的输出文件名，默认写入到标准输出。

`-text`

以文本形式打印 CRL。

`-nameopt option`

决定显示主体（subject）或颁发者（issuer）名称的选项。参见 `x509(1)` 中 `-nameopt` 的描述。

`-noout`

不输出 CRL 的编码版本。

`-hash`

输出颁发者名称的哈希。用于根据颁发者名称在目录中查找 CRL。

`-hash_old`

使用 OpenSSL 1.0.0 之前的旧算法输出 CRL 颁发者名称的“hash”。

`-issuer`

输出颁发者名称。

`-lastupdate`

输出 `lastUpdate` 字段。

`-nextupdate`

输出 `nextUpdate` 字段。

`-CAfile file`

通过查找文件中颁发的证书来验证 CRL 上的签名。

`-CApath dir_`

通过查找目录中的颁发证书来验证 CRL 上的签名。该目录必须是标准的证书目录：每个主体目录的哈希（使用 `x509 -hash` 计算）应链接到每个证书。

# 注意

PEM CRL 格式使用页眉和页脚行：

```
-----BEGIN X509 CRL----------END X509 CRL-----
```

## 示例

将 CRL 文件从 PEM 转换为 DER：

```
openssl crl -in crl.pem -outform DER -out crl.der
```

输出 DER 编码证书的文本形式：

```
openssl crl -in crl.der -text -noout
```

# 故障

理想情况下，也可以使用适当选项和文件创建 CRL。

# 另请

`crl2pkcs7(1)`, `ca(1)`, `x509(1)`

# CRL2PKCS7

## 名称

`crl2pkcs7` - 从 CRL 和证书创建 PKCS#7 结构。

### 摘要

```
openssl crl2pkcs7 [-inform PEM|DER] [-outform PEM|DER] [-in filename] [-out filename] [-certfile filename] [-nocrl]
```

### 描述

`crl2pkcs7` 命令接收可选的 CRL 和一个多个证书，并将它们转换为 PKCS#7 退化的“仅证书”结构。

### 命令选项

`-inform DER|PEM`
指定 CRL 输入格式。DER `format` 为 DER 编码的 CRL 结构。PEM（默认）是 DER 形式的 base64 编码版本，带有页眉和页脚行。
`-outform DER|PEM`
指定 PKCS#7 结构输出格式。`format` 为 DER 编码的 PKCS#7 结构。PEM（默认）是 DER 形式的 base64 编码版本，带有页眉和页脚行。

`-in filename`
指定读取 CRL 的输入文件名，如果指定了此选项则从标准输入读取。
`-out filename`
指定写入的输出文件名，默认写入到标准输出。
`-certfile filename`
指定读取证书的输入文件名，如果指定了此选项则从标准输入读取。
`-nocrl`
不输出 CRL 的编码版本。

## 示例

从 CRL 创建 PKCS#7 结构：

```
openssl crl2pkcs7 -in crl.pem -certfile cert.pem -out out.pk7
```

以 DER 格式创建 PKCS#7 结构：

```
openssl crl2pkcs7 -in crl.pem -certfile cert.pem -out out.pk7 -outform DER
```

# 注意

PEM CRL 格式使用页眉和页脚行：

```
-----BEGIN X509 CRL----------END X509 CRL-----
```

PEM CRL 格式使用页眉和页脚行：

```
-----BEGIN X509 CRL----------END X509 CRL-----
```

# 另请

`pkcs7(1)`

## 名称

`crl` - CRL 实用

### 摘要

`openssl crl [-inform PEM|DER] [-outform PEM|DER] [-text] [-in filename] [-out filename] [-nameopt option] [-noout] [-hash] [-issuer] [-lastupdate] [-nextupdate] [-CAfile file] [-CApath dir ]`

### 描述

`crl` 命令处理 DER 或 PEM 格式的 CRL 文件。

### 命令选项

`-inform DER|PEM`

指定输入格式。`format` 为 DER 编码的 CRL 结构。PEM（默认）是 DER 形式的 base64 编码版本，带有页眉和页脚行。

### 描述

`crl2pkcs7` 命令接收可选的 CRL 和一个多个证书，并将它们转换为 PKCS#7 退化的“仅证书”结构。

### 命令选项

`-inform DER|PEM`
指定 CRL 输入格式。DER `format` 为 DER 编码的 CRL 结构。PEM（默认）是 DER 形式的 base64 编码版本，带有页眉和页脚行。

# 注意

PEM CRL 格式使用页眉和页脚行：

```
-----BEGIN X509 CRL-----
```



# 故障

理想情况下，也可以使用适当选项和文件创建 CRL。

# 注意

PEM CRL 格式使用页眉和页脚行：

```
-----BEGIN X509 CRL-----
-----END X509 CRL-----
```

# 格式使用

和页50

9

```
BEGIN X509 CRL-----
```

#9 -----



# CRL 实用

## 名称
`crl` - CRL 实用

### 摘要
`openssl crl [-inform PEM|DER] [-outform PEM|DER] [-text] [-in filename] [-out filename] [-nameopt option] [-noout] [-hash] [-issuer] [-lastupdate] [-nextupdate] [-CAfile file] [-CApath dir]`

### 描述
`crl` 命令处理 DER 或 PEM 格式的 CRL 文件。

### 命令选项
`-inform DER|PEM`
指定输入格式。format 为 DER 编码的 CRL 结构。PEM（默认）是 DER 形式的 base64 编码版本，带有页眉和页脚行。

## `crl2pkcs7` 命令

`crl2pkcs7` 命令接收可选的 CRL 和一个多个证书，并将它们转换为 PKCS#7 退化的“仅证书”结构。

### 命令选项
`-inform DER|PEM`
指定 CRL 输入格式。DER format 为 DER 编码的 CRL 结构。PEM（默认）是 DER 形式的 base64 编码版本，带有页眉和页脚行。

# 格式使用

## 名称
`crl` - CRL 实用

## 摘要
`openssl crl [-inform PEM|DER] [-outform PEM|DER] [-text] [-in filename] [-out filename] [-nameopt option] [-noout] [-hash] [-issuer] [-lastupdate] [-nextupdate] [-CAfile file] [-CApath dir]`

## 描述
`crl` 命令处理 DER 或 PEM 格式的 CRL 文件。

## 描述
证书吊销列表（CRL）管理工具，`rlutil`，是一个命令行工具，可以对安全数据库文件(s)进行列表、生成或删除 CRL，并对特定 CRL 进行列表、创建或删除操作。密钥和证书管理过程通常从在密钥数据库中创建密钥开始，然后在证书数据库中生成和管理证书（参见 `certutil`），最后处理吊销。本文讨论证书吊销列表。有关安全模块数据库管理的信息，请参见使用安全数据库工具。有关证书和密钥数据库管理的信息，请参见使用证书数据库工具。要运行证书吊销列表管理工具，输入命令 `crutil option [arguments]`，其中选项和参数是下节列出的选项和参数的组合。

## 选项和参数
选项指定操作。选项参数修改操作。`crutil` 命令的选项和参数定义如下：

`-D` 从证书数据库中删除吊销列表。
`-E` 从证书数据库中删除所有类型的 CRL。
`-G` 创建新的证书吊销列表（CRL）。
`-I` 将 CRL 导入证书数据库。
`-L` 列出证书数据库文件中存在的 CRL。
`-M` 修改位于证书数据库或任意文件中的现有 CRL。如果是文件，则应为 ASN.1 编码格式。
`-S` 显示未存储在数据库中的 CRL 文件内容。

### 参数
选项参数修改操作。

`-a` 使用 ASCII 格式，或允许在输入和输出中使用 ASCII 格式。此格式遵循 RFC #1133。
`-B` 跳过 CA 签名检查。
`-c crl-gen-file`
指定用于控制 CRL（吊销列表）生成/修改的脚本文件。参见下文的 crl 文件格式。如果使用了选项 `-M|-G` 且未指定 `-c crl-script-file`，`crutil` 将从标准输入读取脚本数据。
`-d directory`
指定包含证书和密钥数据库文件的数据库目录。在 Unix 上，证书数据库工具的默认位于 `$HOME/.netscape`（即 `~/.netscape`）。在 Windows NT 上，默认是当前目录。
NSS 数据库文件必须存在于同一目录下。
`-f password-file`
指定一个将自动提供密码以包含在证书中或访问证书数据库的文件。这是一个包含一个密码的明文文件。请确保防止对该文件的未经授权的访问。
`-i crl-file`
指定包含要导入或显示的 CRL 的文件。
`-l algorithm-name`
指定特定的签名算法。可能的算法列表：`MD2 | MD4 | MD5 | SHA1 | SHA256 | SHA384 | SHA512`
`-n nickname`
指定要列出、创建、添加到数据库、修改或验证的证书或密钥的别名。如果别名字符串包含空格，请用引号将其括起来。
`-o output-file`
指定新 CRL 的输出文件名。如果输出文件字符串包含空格，请用引号将其括起来。如果未使用此参数，则输出目标默认为标准输出。
`-P dbprefix`
指定用于 NSS 安全数据库文件的前缀（例如，`my_cert8.db` 和 `my_key3.db`）。此选项作为特殊情况提供。不建议更改证书和密钥数据库的名称。
`-t crl-type`
指定 CRL 类型。可能的类型有：`0 - SEC_KRL_TYPE, 1 - SEC_CRL_TYPE`。此选项已废弃。
`-u url`
指定 url。
`-w pwd-string`
在命令行中提供数据库密码。
`-Z algorithm`
指定用于签署 CRL 的哈希算法。

## CRL 生成脚本语法
CRL 生成脚本文件具有以下语法：

- 注释行应以 `#` 作为行的第一个符号
- 设置 "this update" 或 "next update" CRL 字段：
`update=YYYYMMDDhhmmS`
`nextupdate=YYYYMMDDhhmmS`
"next update" 字段是可选的。时间应采用 GeneralizedTime 格式 (`YYYYMMDDhhmmS`)。例如：`20050204153000Z`
- 为 CRL 或 crl 证书条目添加扩展：
`extension-name critical/non-critical [arg1][arg2 ...]`
其中：
`extension-name`: 已知扩展名称的字符串值。`critical/non-critical`: 当扩展是关键的时为 1，否则为 0。`arg1, arg2`: 特定于扩展类型的参数。
`adext` 之前通过 `addcert` 设置的范围，并将向该范围内的每个条目安装扩展。
- 向 CRL 添加证书条目：
`addcert range date`
`range`: 两个由破折号分隔的整数：由此命令添加的证书范围。破折号用作分隔符。如果没有分隔符，则只添加一个证书。
`date`: 证书的吊销日期。日期应以 GeneralizedTime 格式表示 (`YYYYMMDDhhmmS`)。
- 从 CRL 删除证书条目
`rmcert range date`
其中：
`range`: 两个由破折号分隔的整数：由此命令添加的证书范围。如果没有分隔符，则只添加一个证书。
- 修改 CRL 中的证书条目范围
`range new-range`
其中：
`new-range`: 两个由破折号分隔的整数：由此命令添加的证书范围。破折号用作分隔符。如果没有分隔符，则只添加一个证书。

### Im 扩展
为 CRL 定义的扩展提供了将附加属性与其 CRL 条目关联的方法。更多信息请参阅 RFC #3280

- 添加权威密钥标识符（Authority Key Identifier）扩展：
权威密钥标识符扩展提供了一种识别用于签署 CRL 的私钥相对应的公钥的方法。
`authKeyId critical [key-id | dn cert-serial]`
其中：
`authKeyId`: 标识扩展名称。`critical`: 值为 1 或 0。如果这是关键的，则应设置为 1，否则设置为 0。`key-id`: 以字节表示的密钥标识符。`dn.`: 是 CA 区分名。`cert-serial`: 权威证书序列号。
- 添加发布者备名称（Issuer Alternative Name）扩展：
发布者备用名称扩展允许将额外的身份与 CRL 的发布者关联。定义的选项包括 rfc822 名称（电子邮箱地址）、DNS 名称、IP 地址和 URI。
`issuerAltNames non-critical name-list`
其中：
`subjAltNames`: 标识扩展名称，由于这是一个非关键扩展，应设置为 0。`name-list`: 逗号分隔的名称列表。
- 添加 CRL 编号（CRL Number）扩展：
CRL 编号是一个非关键的 CRL 扩展，为给定的 CRL 范围和 CRL 发布者提供一个单调递增的数字。此扩展允许用户轻松判断特定 CRL 何时取代另一个 CRL。
`crlNumber non-critical number`
其中：
`crlNumber`: 标识扩展名称。`critical`: 由于是非关键扩展，应设置为 0。`number`: long 类型的值，用于识别 CRL 的序列号。
- 添加 吊销原因代码（Revocation Reason Code）扩展：
`reasonCode` 是一个非关键的 CRL 条目扩展，用于识别证书吊销的原因。
`reasonCode non-critical code`
其中：
`reasonCode`: 标识扩展名称。`critical`: 由于是非关键扩展，应设置为 0。`code`: 可用代码如下：
`unspecified` (未指定), `keyCompise` (密钥泄露), `affiliationChanged` (关联变更), `superseded` (已取代), `cessationOfOperation` (停止操作), `certificateHold` (证书保留), `removeFromCRL` (从CRL移除), `privilegeWithdrawn` (权限取消), `aCompromise` (授权泄露)
- 添加失效日期（Invalidity Date）扩展：
失效日期是一个非关键的 CRL 条目扩展，提供了已知私密钥泄露或证书或其他失效的日期。
`invalidationDate non-critical date`
其中：
`crlNumber`: 标识扩展名称。`critical`: 由于是非关键扩展，应设置为 0。`date`: 证书的失效日期。日期应以 GeneralizedTime 格式表示 (`YYYYMMDDhhmmss`)。

## 用法
证书 CRL 管理工具的功能如下，使用这些选项和参数的组合。括号中的选项是可选的，没有括号的是必需的。

有关扩展及其参数的更多信息请参见“实现的扩展”。

- 创建或修改 CRL：
`crutil -G|-M -c crl-script-file -n nickname [-i crl] [-u url] [-d keydir] [-P dbprefix] [-l alg] [-a] [-B]`
- 列出所有 CRL 或命名的 CRL：
`crutil -L [-n crl-name] [-d keydir]`
- 从数据库删除 CRL：
`crutil -D -n nickname [-d keydir] [-P dbprefix]`
- 从数据库擦 CRL：
`crutil -E [-d keydir] [-P dbprefix]`

### 参见
`certutil(1)`

## 其他资源
有关 NSS 以及与 NSS 相关工具（如 JSS）的信息，请查看 NSS 项目 wiki：`http://www.mozilla.org/projects/security/pki/nss/`。NSS 站点直接涉及 NSS 代码更改和发布。

邮件列表：`https://lists.mozilla.org/listinfo/dev-tech-crypto`

IRC：Freenode 的 `#dogtag-pki`

### 作者
NSS 工具由 Netscape、Red Hat、Sun、Oracle、Mozilla 和 Google 的人员编写和维护。

作者：`Elio Maldonado <emaldona@redhat.com>`, `Deon Lackey <dlackey@redhat.com>`

## 许可证
根据 Mozilla 公共许可证 v2.0 许可。如果此文件未附带 MPL 副本，您可以从 `http://mozilla.org/MPL/2.0` 获取。

# Notes

- 1. Mozilla NSS bug 836477
`https://bugzilla.mozilla.org/show_bug.cgi?id=836477`

# CRONTAB

`crontab` - 为单个用户维护 crontab 文件

# 概览
```



`crontab [-u user] file`
`crontab [-u user] [-l | -r | -e] [-i] [-s]`
`crontab -n [ hostname ]`
`crontab -c`

### 描述

Cronab 是用于安装、删除或列出用于 `cron(8)` 守护进程的表的程序。每个用户都可以有自己的 crontab，虽然这些文件位于 `/var/spool/` 中，但并不打算被直接编辑。对于处于 MLS 模式的 SELinux，你可以为每个范围定义更多的 crontabs。更多信息，请参阅 `selinux(8)`。

在版本的版本的 Cron 中，可以在跨主机集群使用网络挂载的共享 `/var/spool/cron`，并指定任何时候只有集群中的一台主机运行特定目录下的 cron 任务。你也可以从这些主机中的任何一台使用 `crontab(1)` 来编辑同一组共享 crontab 文件，并设置和查询哪个主机应该运行 cron 任务。

可以允许或禁止不同用户运行 cron 任务。为了此目的，请使用 `cron.allow` 和 `cron.deny` 文件。如果 `cron.allow` 文件存在，则用户必须列在其中，且用户不能列在 `cron.deny` 文件中才能使用 cron。如果 `cron.allow` 文件不存在，且这两个文件都不存在，则只有超级用户允许使用 cron。另一种限制 cron 访问的方法是使用 `/etc/security/access.conf` 中的 PAM 认证来设置允许或禁止用户使用 crontab 或修改 `/etc/cron.d/` 目录下的系统 cron 任务。

可以通过环境变量设置临时目录。如果用户没有设置，则使用 `/tmp` 目录。

### 选项

`-u`
附加要修改的 crontab 用户的用户名。如果不使用此选项，`crontab` 将检查“你”的 crontab，即执行命令的人的 crontab。注意 `su(8)` 可能会混淆 `crontab`，因此在 `su(8)` 下执行命令时，你应该始终使用 `-u` 选项。如果特定用户没有 crontab，则在该用户用户名下第一次使用 `crontab -u` 命令时会为他创建一个。

`-l`
在标准输出上显示当前 crontab。

`-r`
删除当前 crontab。

`-e`
使用 `VISUAL` 或 `EDITOR` 环境变量指定的编辑器编辑当前 crontab。在你退出编辑器后，修改后的 crontab 将自动安装。

`-i`
此选项将修改 `-r` 选项，以便在实际删除 crontab 后提示用户输入 'y/Y' 响应。

`-s`
在编辑/替换之前，将当前的 SELinux 安全上下文字符串作为 `MLS_LEVEL` 设置附加到 crontab 文件中 - 请参阅 `crontab(5)` 中 `MLS_LEVEL` 的文档。

`-n`
此选项仅当 `cron(8)` 使用 `-c` 选项启动时有效，该选项用于启用集群支持。它被用于设置集群中应运行位于 `/var/spool/cron.d` 目录下 crontab 文件中指定任务的主机。如果提供了主机名，则 `gethostname(2)` 返回的主机与该主机名匹配，该主机将被选中后续运行选定的 cron 任务。如果集群中没有匹配该主机名的主机，或者你显式指定了一个空主机名，则选定的任务将不会运行。如果省略主机名，则使用 `gethostname(2)` 返回的本地主机名。使用此选项对 `/etc/crontab` 文件和 `/etc/cron.d` 目录下的文件没有影响，这些文件始终运行并被视为特定主机的。有关集群支持的更多信息，请参阅 `cron(8)`。

`-c`
此选项仅当 `cron(8)` 使用 `-c` 选项启动时有效，该选项用于启用集群支持。它用于查询集群中当前设置哪个主机运行 `/var/spool/cron` 目录下 crontab 文件中的指定任务（如使用 `-n` 选项设置）。

### 参见

`crontab(5)`, `cron(8)`

### 文件
`/etc/cron.allow` `/etc/cron.deny`

# 标准

`*crontab*` 命令符合 IEEE Std1003.2-1992 (“POSIX”）。这种新的命令语法与之前的 Vixie Cron 版本不同，也与经典的 SVR3 语法不同。

# 诊断

如果你运行包含错误命令的 crontab，将出现一条信息丰富的用法消息。

### 作者

Paul Vixie Colin Dean

# cups

## 名称

`cups` - 一个基于标准的开源打印系统

### 描述

CUPS 是你用于从文字处理器、电子邮件阅读器和照片编辑器等应用程序进行打印的软件。CUPS 将你产生的页面（过滤器、打印机监控器和后端）转换为可打印格式，然后运行它们以实际执行打印作业。每当打印机制造商的做法有所不同时，打印可能会变得复杂。CUPS 会尽力向你和你的应用程序隐藏这些复杂性。

# 它是如何工作的？

当你第一次打印时，CUPS 会创建一个任务，其中包含你正在发送的队列、你正在打印的文档名称以及任何页面（queue-1、queue-2 等），这样你就可以监控正在打印或取消的任务。每当任务完全完成时，CUPS 都会从队列中移除该任务并处理其他任务。你还可以通过几种不同的方式在任务完成或打印期间错误时收到通知。

# 我应该从哪里开始？

最简单的方法是使用 界面配置你的打印机。访问 `http://localhost:631` 并选择页面顶部的管理（Administration）选项卡。点击添加打印机（Add Printer）按钮并按照提示操作。当要求用户名和密码时，输入你的登录用户名和密码或“root”用户名和密码。打印机添加后，你将被要求为打印机设置默认选项（纸张大小、输出模式等）。根据需要进行任何更改，然后点击设置选项（Set Options）按钮保存它们。某些打印机还支持自动配置 - 点击查询打印机默认选项（Query Printer for Default Options）按钮自动更新选项。一旦添加了打印机，你就可以从任何应用程序对其打印。你还可以从维护菜单选择打印测试页（Print Test Page）来打印一个简单的测试页并验证一切运行正常。你还可以使用 `lpadmin(8)` 和 `lpinfo(8)` 命令将打印机添加到 CUPS 中。此外，你的操作系统可能包含图形用户界面，或在打印机连接到计算机时自动创建打印队列。

## 如何获取帮助？

CUPS 网站 (`http://www.CUPS.org`) 提供访问 `cups` 和 `cups-devel` 邮件列表、附加文档和资源以及错误报告数据库。大多数供应商还提供在线文档论坛来回答你所在操作系统的打印问题。

# 环境

CUPS 命令使用以下环境变量来覆盖文件等的默认位置。出于安全考虑，这些环境变量在 setuid 程序中会被忽略：

## `CUPS_ANYROOT`

是否允许任何 X.509 证书根根证书（Y 或 N）。

## `CUPS_CACHEDIR`

存储半持久化缓存文件的目录。

## `CUPS_DATADIR`

存储数据文件的目录。

## `CUPS_ENCRYPTION`

默认加密级别（Always Always, IfRequested 请求, Never, 需要）。

## `CUPS_EXPIREDCERTS`

是否允许过期的 X.509 证书（Y 或 N）。

## `CUPS_GSSERVICENAME`

用于认证的 Kerberos 服务名称。

## `CUPS_SERVER`

CUPS 调度器的主机/IP 地址和端口号（hostname:port 或 ipaddress:port）。

## `CUPS_SERVERSBIN`

存储服务器辅助程序、过滤器（filters）、后端等的目录。

## `CUPS_SERVERROOT`

服务器的根目录。

## `CUPS_STATEDIR`

存储状态文件的目录。

## `CUPS_USER`

指定打印请求的用户名。

## `HOME`

指定当前用户的家目录。

## `IPP_PORT`

指定 IPP 请求的默认端口号。

## `LOCALDIR`

指定本地化文件的位置。

## `LPDEST`

指定默认打印队列（System V 标准）。

## `PRINTER`

指定默认打印队列（Berkeley 标准）。

## `TMPDIR`

指定临时文件的位置。

### 文件

```
~/.cups/client.conf ~/.cups/lpoptions
```



# 符合性

`CUPS` 符合互联网打印协议第 2.1 版本，并实现了 Berkeley 和 System V UNIX 打印命令。

### 参见

`cancel(1)`, `client.conf(7)`, `cupsctl(8)`, `cupsd(8)`, `lp(1)`, `lpadmin(8)`, `lpinfo(8)`, `lpoptions(1)`, `lpr(1)`, `lprm(1)`, `lpq(1)`, `lpstat(1)`, CUPS 在线帮助 (`http://localhost:631/help`), CUPS 网站 (`http://www.CUPS.org`), PWG 打印协议工作组 (`http://www.pwg.org/ipp`)

# 版权

Copyright ©2007-2014 by Apple Inc.

## 名称

`cupstestdsc` - 测试 postscript 文件的符合性（已弃用）

### 摘要

```
cupstestdsc [ -h ] filename.ps [ ... filenameN.ps ]
cupstestdsc [ -h ] -
```

### 描述

`cupstestdsc` 测试 PostScript 文件是否符合 Adobe PostScript 语言文档结构化规范规范第 3.0 版本。测试结果和任何其他输出都将发送到标准输出。命令的第二种形式从标准输入读取 PostScript。

# 注意事项

此程序已弃用，将在未来的 CUPS 版本中被移除。

`cupstestdsc` 仅验证 PostScript 文件中的 DSC 注释，而不尝试验证 PostScript 本身。开发者应确保其生成的 PostScript 遵循 Adobe 定义的规则。具体而言，所有页面必须相互独立，页面描述之外的代码不能影响图形状态（当前字体、颜色、变换矩阵等），且不应使用如 `setpagedevice` 等设备特定命令。

### 参见

CUPS 在线帮助 (`http://localhost:631/help`), Adobe PostScript 语言文档结构化规范, 第 3.0 版。

# 版权

Copyright ©2007-2014 by Apple Inc.

# cupstestppd

## 名称

`cupstestppd` - 测试 ppd 文件的符合性

### 摘要

```
cupstestppd [ -I category ] [ -R rootdir ] [ -W category ] [ -q ] [ -r ] [ -v[v] ] filename.ppd[.gz] [ ... filename.ppd[.gz] ]
cupstestppd [ -R rootdir ] [ -W category ] [ -q ] [ -r ] [ -v[v] ] -
```

### 描述

`cupstestppd` 测试 PPD 文件是否符合 Adobe PostScript 打印机描述文件格式规范第 4.3 版本。它还可以列出 PPD 文件中支持的选项和可用字体。测试结果和任何其他输出都将发送到标准输出。

`cupstestppd` 的第一形式在命令行测试一个或多个 PPD 文件。第二种形式测试标准输入提供的 PPD 文件。

### 选项

`cupstestppd` 支持以下选项：

- `-I filename`
忽略所有 PCFileName 警告。
- `-I filters`
忽略所有过滤器错误。
- `-I profiles`
忽略所有配置文件错误。
- `-R rootdir`
指定过滤器、预过滤器和其他支持检查的备根目录。
- `-W constraints`
将所有约束作为警告报告。
- `-W defaults`
除尺寸相关的选项外，将所有默认错误作为警告报告。
- `-W filters`
将所有过滤器错误作为警告。
- `-W profiles`
将所有配置错误作为警告。
- `-W sizes`
将所有媒体错误作为警告。
- `-W translations`
将所有翻译错误作为警告。
- `-W all`
将上述所有错误作为警告。
- `-W none`
将上述错误作为错误报告。
- `-q`
指定不显示任何信息。
- `-r`
放宽 PPD 符合性，使得常见的空格、控制字符和格式问题不被视为强制错误。
- `-v`
指定显示详细测试结果而非 PASS/FAIL/ERROR。
- `-vv`
指定在详细测试结果之外额外显示 PPD 文件中的所有信息。`-q`、`v` 和 `-vv` 选项互斥。

# 退出状态

`cupstestppd` 成功时返回零，出错时返回非零。错误代码为：

- `1` 命令行参数错误或缺少 PPD 文件名。
- `2` 无法打开或读取 PPD 文件。
- `3` PPD 文件包含无法跳过的格式错误。
- `4` PPD 文件不符合 Adobe 规范。

## 示例

以下命令将测试当前目录下的所有 PPD 文件，并打印每个不符合的文件名：`find -name *.ppd -exec cupstestppd -q {} \;` 下一个命令测试当前目录下的所有 PPD 文件，并为不符合的文件打印详细测试结果：`find -name *.ppd -exec cupstestppd -q {} \; -exec cupstestppd -v {} \;`

### 参见

`lpadmin(8)`, CUPS 在线帮助 (`http://localhost:631/help`), Adobe PostScript 打印机描述规范。

# 版权

Copyright ©2007-2014 by Apple Inc.

# curl

`curl` - 一个 URL

### 摘要

```
curl [options] [URL]
```

### 描述

`curl` 是一个从或向服务器传输数据的工具，使用多种协议（DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS, IMAP, LDAP, LDAPS, POP, RTMP, RTSP, SCP, SFTP, SMTP, SMTPS, TELNET 和 TFTP）。它设计为无需交互即可工作。

`curl` 提供了许多技巧，如代理支持、用户认证、FTP 上传、SSL 连接、Cookie、文件传输恢复等。如下所示，它的功能会让你大目口界！

# URL

URL 语法取决于协议。你可以在 RFC 3986 中找到详细描述。

你可以在大括号内编写来指定多个 URL 或部分：
`http://site.{one,two,three}.com`

或者你可以使用 [] 获取字母序列，如：

```
ftp://numericals.com/file[1-100].txt
```

```
ftp://numericals.com/file[001-100].txt
```
带前零

```
ftp://letters.com/file[a-z].txt
```

不支持嵌套序列，但你可以并排使用多个：
```
http://any.org/archive/1996-1999/vol[1-4]/part{a,b,c}.html
```

你可以在命令行指定任意数量的 URL。它们将按照指定的顺序顺序获取。

你可以指定范围计数器来获取每 N 个数字或字母：
```
http://www.numericals.com/file[1-100:10].txt
```
```
http://www.letters.com/file[a-z:2].txt
```



当从命令行调用使用 `[]` 或 `{}` 序列时，你可能需要将整个 URL 放在双引号内，以避免 shell 干扰。这也适用于其他特殊字符，例如 `&`、`?` 和 `*`。

通过转义百分号和接口在 URL 中提供 IPv6 区域索引。例如 `[fe80::3%25eth0]`/在没有 `protocol://` 前缀的情况下指定 URL，`curl` 会尝试猜测你可能需要的协议。它默认使用 HTTP，但根据常用的主机名前缀尝试其他协议。例如，对于以“ftp.”开头的主机名，`curl` 会假设你想使用 FTP。

`curl` 会尽可能使用你传递给它的 URL。它并没有试图验证其是否为语法上正确的 URL，而是对接受的内容非常宽松。

# 进度表

`curl` 在操作期间通常会显示一个进度表，指示传输的数据量、传输速度和预计剩余时间等。

`curl` 默认将这些数据显示在终端，因此，如果你调用 `curl` 执行操作且它正准备向终端写入数据，它将禁用进度表，否则会造成进度表和响应数据混合导致的混乱。

如果你想为 HTTP POST 或 PUT 请求获取进度表，你需要将响应输出重定向到文件，使用 shell 重定向 (`>`)、`-o [file]` 或类似方法。

对于 FTP 上传的情况则不同，因为该操作不会向终端吐出任何响应数据。

如果你更倾向于使用进度“条”而不是普通的仪表，`-#` 是你的好伙伴。

## 选项

选项以一个或两个横线开头。许多选项需要在后面紧跟一个额外的值。

选项的短格式（“单横线”），例如 `-d`，可以在它与值之间使用空格，也可以不使用空格，尽管推荐使用空格作为分隔符。长格式（“双横线”），例如 `--data`，则要求在它与值之间必须有空格。

不需要任何额外值的短版本选项可以紧挨着使用，例如你可以一次指定所有选项 `-O`、`-L` 和 `-v`，即 `-Oliv`。

通常情况下，所有布尔选项都通过 `--option` 启用，通过 `--no-option` 禁用。此时，你使用 `no-` 前缀加上精确的选项名称。然而，在列表中我们主要列出并显示它们的 `--option` 版本。（这种带有 `--no` 选项的概念是在 7.19.0 中引入的。之前，大多数选项通过重复使用相同的命令行选项来切换开启/关闭。）

- `-#`,`--progress-bar`
  让 `curl` 以简单的进度条显示进度，而不是标准的、包含更多信息的仪表。

- `-`,`--next`
  告诉 `curl` 对后续的 URL 及其关联选项使用一个独立的操作。这允许你发送多个 URL 请求，每个请求都有其特定的选项，例如为每个请求设置不同的用户名或自定义请求。（在 7.36.0 中引入）

- `-0`,`--http1.0`
  (HTTP) 告诉 `curl` 使用 HTTP 版本 1.0，而不是使用其内部首选的：HTTP 1.1。

- `--http1.1`
  (HTTP) 告诉 `curl` 使用 HTTP 版本 1.1。这是内部的默认版本。（在 7.33.0 中引入）

- `--http2`
  (HTTP) 告诉 `curl` 使用 HTTP 2 发起请求。这要求底层的 libcurl 在编译时已支持它。（在 7.33.0 中引入）

- `--no-npn`
  禁用 NPN TLS 扩展。如果 libcurl 是使用支持 NPN 的 SSL 库编译的，则默认会启用 NPN。支持 HTTP 2 的 libcurl 在 https 会话中使用 NPN 与服务器协商 HTTP 2 支持。（在 7.36.0 中引入）

- `--no-alpn`
  禁用 ALPN TLS 扩展。如果 libcurl 是使用支持 ALPN 的 SSL 库编译的，则默认会启用 ALPN。支持 HTTP 2 的 libcurl 在 https 会话中使用 ALPN 与服务器协商 HTTP 2 支持。（在 7.36.0 中引入）

- `-1`,`--tlsv`
  (SSL) 强制 `curl` 在与远程 TLS 服务器协商时使用 TLS 版本 1.x。你可以使用选项 `--tlsv1.0`、`--tlsv1.1` 和 `--tlsv1.2` 来更精确地控制 TLS 版本（如果 SSL 后端支持这种级别的控制）。

- `-2`,`--sslv2`
  (SSL) 强制 `curl` 在与远程 SSL 服务器协商时使用 SSL 版本 2。有时 `curl` 编译时没有包含 SSLv2 支持。SSLv2 被广泛认为是不安全的。

- `-3`,`--sslv3`
  (SSL) 强制 `curl` 在与远程 SSL 服务器协商时使用 SSL 版本 3。有时 `curl` 编译时没有包含 SSLv3 支持。

- `-4`,`--ipv4`
  此选项告诉 `curl` 仅将名称解析为 IPv4 地址，而不要尝试 IPv6。

- `-6`,`--ipv6`
  此选项告诉 `curl` 仅将名称解析为 IPv6 地址，而不要尝试 IPv4。

- `-a`,`--append`
  (FTP/SFTP) 用于上传，这会让 `curl` 附加目标文件而不是覆盖。如果远程文件不存在，则将创建它。注意，此标志会被某些 SFTP 服务器（包括 OpenSSH）忽略。

- `-A`,`--user-agent <string>`
  (HTTP) 指定发送到 HTTP 服务器的 User-Agent 字符串。某些编写得糟糕的 CGI 如果该字段未设置为 "Mozilla/4.0" 就会失败。为了编码字符串中的空格，请用单引号包裹字符串。当然，也可以通过 `-H` 头部选项进行设置。如果多次使用此选项，将以最后一个为准。

- `--anyauth`
  (HTTP) 告诉 `curl` 自动确定身份验证方法，并使用远程站点支持的最安全的方法。这是通过先发送请求并检查响应头来实现的，可能会导致额外的网络往返。这用于替代设置特定的身份验证方法（你可以通过 `--basic`、`--digest`、`--ntlm` 和 `--negotiate` 来实现）。注意，如果上传到 stdin，则不建议使用 `--anyauth`，因为它可能需要发送两次数据，且客户端必须能够回溯。如果从 stdin 上传，由于可能需要发送两次数据，可能会失败。

- `-b`,`--cookie<data>`
  (HTTP) 传递从服务器接收的 cookie，格式为 NAME=VALUE。如果多次使用此选项，将以最后一个为准。如果使用 `-`，则写入 stdout。如果使用文件名，则写入文件。如果不存在该 cookie，则会创建它。使用 `-L` 选项时可以读取这些 cookie。如果多次使用此选项，将以最后一个为准。

- `-c`,`--cookie-jar <file>`
  (HTTP) 指定 `curl` 写入 cookie 的文件。如果多次使用此选项，将以最后一个为准。

- `-B`,`--use-ascii`
  (FTP) 告诉 `curl` 使用 ASCII 认证。这与 `-user` 选项配合使用。

- `-ciphers <list of ciphers>`
  (SSL) 指定连接中使用的加密套件。有关套件列表详情请参见 https://www.openssl.org/docs/apps/ciphers.html。NSS 套件与 OpenSSL 和 GnuTLS 有不同。NSS 的完整套件列表位于 https://git.fedorahost.org/cgit/mod_nss.git/plain/docs/。

- `--compressed`
  请求使用 `curl` 支持的算法压缩响应并保存。如果使用了此选项但服务器发送不支持的编码，`curl` 将报告错误。

- `--connect-timeout`
  允许 `curl` 连接的最大时间（秒）。这仅限制连接阶段；如果 `curl` 在规定时间内连接成功则继续，否则退出。从 7.32 版本开始，此选项接受小数。另见 `-m`,`--max-time` 选项。如果多次使用此选项，将以最后一个为准。

- `--create-dirs`
  与 `-o` 选项配合使用时，`curl` 将创建必要的目录层次。此选项仅创建 `-o` 提到的目录。如果 `-o` 文件名未使用目录或目录已存在，则不会创建。如需使用 FTP 或 SFTP 创建远程目录，请尝试 `--ftp-create-dirs`。

- `--crlf`
  上传时将 LF 转换为 CRLF。适用于 MVS (OS/390)。

- `-rlfile <file>`
  (HTTPS/FTPS) 提供一个 PEM 格式的证书吊销列表，可以指定被吊销的证书。如果多次使用此选项，将以最后一个为准。（SMTP 在 7.40.0 中添加）（在 7.19.7 中引入）

- `-d`,`--data <data>`
  (HTTP) 向 HTTP 服务器通过 POST 请求发送数据，就像浏览器在用户填写 HTML 表单并点击提交按钮一样。这将导致 `curl` 使用 content-type application/x-www-form-urlencoded 将数据传递给服务器。对比 `-F`,`--form`。

`-d`,`—data` 与 `--data-ascii` 相同。`--data-raw` 几乎相同，但对 `@` 字符没有特殊解释。要发布纯二进制数据，你应当改用 `--data-binary` 选项。要对表单字段的值进行 URL 编码，可以使用 `--data-urlencoded`。

如果在同一条命令行上多次使用这些选项中的任何一个，指定的数据片段将通过 `&` 分隔符合并在一起。因此，使用‘`-d name=daniel -d skill=lousy`’ 将生成一个看起来类似于‘`name=daniel&skill=lousy`’的请求。

如果你用字母 `@` 开头数据，剩余部分应为从其中读取数据的文件名，或者如果你想从标准输入（stdin）读取数据。也可以指定多个文件。从名为‘foobar’的文件发布数据可以使用 `--data@foobar` 完成。当 `--data` 被要求从类似这样的文件读取数据时，回车符和换行符将被剥除。如果你不想让 `@` 字符具有特殊含义，请使用 `--data-raw`。



## `-D,--dump-header <file>`

将标头写入指定的文件中。

当你想要存储 HTTP 站点发送给你的标头时，此选项非常方便。标头中的 Cookie 可以在第二次 `curl` 调用中通过 `-b, --cookie` 选项进行读取！`-c, --cookie-jar` 选项是存储 Cookie 的更好方法。

在 FTP 中使用时，FTP 服务器响应行被视为“标头”，因此保存在那里。

如果此选项被使用多次，将使用最后一次。

## `-data-ascii <data>`

参见 `-d,--data`。

## `-data-binary <data>`

`HTTP` 完全按照指定的格式进行发布，不经过任何额外处理。

如果你用字母 `@` 开头数据，剩余部分应为文件名。数据的发布方式与 `--data-ascii` 类似，不同之处在于保留了换行符和回车符且永远不会进行转换。

如果此选项被使用多次，第一个将按照 `-d,--data` 描述的方式追加数据。

## `-data-raw <data>`

`HTTP` 发布方式与 `--data` 类似，但没有对 `@` 字符的特殊解释。参见 `-d,--data`。（在 `7.43.0` 中引入）

## `-data-urlencode <data>`



## (HTTP) 发布方式与其他 `--data` 选项类似，不同之处在于它会执行 URL 编码。（在 7.18.0 中引入）

为了符合 CGI 标准，`<data>` 部分应以名称开头，后跟一个分隔符和内容规范。`<data>` 部分可以使用以下语法之一传递给 `curl`：

### `content`

这将对内容进行 URL 编码并传递。请务必内容不要包含任何 `=` 或 `@` 符号，因为这将导致语法匹配到下面的其他情况之一！

### `=content`

这将对内容进行 URL 编码并传递。此前的 `=` 符号不包含在数据中。

### `name=content`

这将对内容部分进行 URL 编码并传递。注意，名称部分预计已经是 URL 编码的了。

### `@filename`

这将让 `curl` 从给定文件加载数据（包括任何换行符），对该数据进行 URL 编码并在 POST 请求中传递。

### `name=@filename`

这将让 `curl` 从给定文件加载数据（包括任何换行符），对该数据进行编码并在 POST 请求中传递。`name` 部分在后会附加一个等号，结果为 `name=urlencoded-file-content`。注意，名称已经是 URL 编码的了。

## `--delegation Level`

设置级别以告知服务器在涉及用户凭据时它被允许代理的内容。配合 GSS/kerberos 使用。

### `none`

不允许任何代理。

### `policy`

仅当 Kerberos 服务票据中设置了 OK-AS-DELEGATE 标志时才进行代理，这是一个策略问题。

### `always`

无条件允许服务器进行代理。

## `--digest` (HTTP)

启用 HTTP 摘要认证。这是一种防止密码以明文通过网络传输的认证方案。请结合正常的 `-u,--user` 选项来设置名称和密码。另见相关选项 `--ntlm`、`--negotiate` 和 `--anyauth`。

如果此选项被使用多次，则仅使用第一个。

## `--disable-eprt` (FTP)

让 `curl` 在执行主动 FTP 传输时禁用 `EPRT` 和 `LPRT` 命令。`Curl` 通常总是先尝试使用 `EPRT`，然后在使用 `PORT` 前使用 `LPRT`，但使用此选项后，它将直接使用 `PORT`。`EPR` 和 `LPRT` 是 FTP 协议的扩展，可能在所有服务器上都无法工作，但它们比传统的 `PORT` 命令能更好地实现更多功能。

`-eprt` 可以显式再次启用 `EPRT`，`--no-eprt` 是 `--disable-eprt` 的别名。

禁用 `EPRT` 仅改变主动行为。如果你想切换到被动模式，无需使用 `-P, --ftp-port` 或通过 `--ftp-pasv` 强制执行。

## `--disable-epsv` (FTP)

告诉 `curl` 在执行被动 FTP 传输时禁用 `EPSV` 命令。`Curl` 通常会先尝试使用 `EPSV` 使用 `PASV`，但使用此选项后，它不会尝试 `EPSV`。

`-epsv` 可用于显式再次 `EPSV`，`--no-epsv` 是 `--disable-epsv` 的别名。

禁用 `EPSV` 仅改变被动行为。如果你想切换到主动模式，需要使用 `-P, --ftp-port`。

## `--dns-interface <interface>`

告诉 `curl` 通过 `<interface>` 发送 DNS 请求。此选项是 `--interface` 的计数（后者不影响 DNS）。提供的字符串必须是接口名称（而不是地址）。

此选项要求 `libcurl` 构建时使用了支持此操作的解析器后端。`c-ares` 后端是唯一支持的。（在 7.33.0 中引入）

## `--dns-ipv4-add <ip-address>`

告诉 `curl` 在进行 IPv4 DNS 请求时绑定到 `<ip-address>`，以便 DNS 请求源自此地址。参数应该是单个 IPv4 地址。

此选项要求 `libcurl` 构建时使用了支持此操作的解析器后端。`c-ares` 后端是唯一支持的。（在 7.33.0 中引入）

## `--dns-ipv6-add <ip-address>`

告诉 `curl` 在进行 IPv6 DNS 请求时绑定到 `<ip-address>`，以便 DNS 请求源自此地址。参数应该是单个 IPv6 地址。

此选项要求 `libcurl` 构建时使用了支持此操作的解析器后端。`c-ares` 后端是唯一支持的。（在 7.33.0 中引入）

## `--dns-servers <ip-address,ip-address>`

设置用于替代 DNS 服务器列表。列表应用逗号分隔。此选项要求 `libcurl` 构建时使用了支持此操作的解析器后端。`c-ares` 后端是唯一支持的。（在 7.33.0 中引入）

## `-e,--referer <URL>`

向 HTTP 头部发送“引用页”信息。也可以通过 `-L` 设置。如果此选项被使用多次，将使用最后一次。

## `-E,--cert[password]` (SSL)

告诉 `curl` 使用指定的客户端证书。如果使用 Secure Transport，证书必须是 PKCS#12 格式；如果使用其他库则为 PEM 格式。如果未指定密码，将在系统或用户密钥串中查询证书名称。

## `--cert-type <type>` (SSL)

告诉 `curl` 提供的证书类型。`PEM`、`DER` 和 `ENG` 是识别类型。如果没有指定，假设为 `PEM`。如果此选项被使用多次，将使用最后一次。

## `--engine <name>`

选择用于加密操作的 OpenSSL 引擎。使用 `--engine list` 输出编译时的引擎列表。注意并非所有引擎在运行时都可用。

## `--environment` (仅限 RISC OS)

使用 `-w` 选项设置环境变量，以便在运行时更容易提取有用信息。

## `--egd-file <file>` (SSL)

指定熵收集守护进程套接字的路径。该套接字用于为 SSL 连接种子。另见 `--random-file` 选项。

## `--cac <CA>` (SSL)

告诉 `curl` 使用指定的证书文件验证对方。该文件可以包含多个 CA 证书。证书必须是 PEM 格式。通常 `curl` 构建时使用默认文件，因此此选项通常用于更改默认文件。`curl` 识别环境变量 `CURL_CA_BUNDLE` 并使用给定的路径作为 CA 证书包路径。此选项会覆盖其他选项。Windows 版本的 `curl` 将自动查找名为 `curl-bundle.crt` 的 CA 证书，位于与 `curl.exe` 相同的目录、当前工作目录或 PATH 中的任何文件夹。如果 `curl` 基于 NSS SSL 库构建，则需要 NSS PEM PKCS#11 模块（`libnsspem.so`）可用才能生效。如果此选项被使用多次，将使用最后一次。

## `--capath <certificate directory>` (SSL)

告诉 `curl` 使用指定的证书验证对方。可以通过冒号分隔提供多个路径（例如 `"path1:path2:path3"`）。证书必须是 PEM 格式，且如果 `curl` 基于 OpenSSL 构建，则目录必须经过 `c_rehash` 工具的处理。

（仅限 iOS 和 Mac X）如果 `curl` 基于 Secure Transport 构建，则证书字符串应为系统或用户密钥串中的证书名称，或者是 PKCS#12 编码证书的路径。

由 OpenSSL 提供。使用 `--capath` 可以让由 OpenSSL 的 `curl` 的 SSL 连接比使用 `--cacert` 高得多，特别是当 `--cacert` 文件包含许多 CA 证书时。

如果设置了此选项，将忽略默认的 `capath` 值；如果使用了多次，则将以最后一次为准。

## `--pinnedpublickey <pinned public key>` (SSL)

告诉 `curl` 使用指定的公钥文件来验证对方。该文件必须包含一个 PEM 或 DER 格式的单个公钥。

在协商 TLS 或 SSL 连接时，服务器会发送一个指示其身份的证书。从该证书中提取出公钥，如果它与提供此选项的公钥不完全匹配，`curl` 将在发送或接收任何数据之前终止连接。

在 7.39.0 版本中为 OpenSSL、GnuTLS 和 GSkit 添加。在 7.43.0 版本中为 NSS 和 wolfSSL/CyaSSL 添加。不支持其他后端。

如果多次使用此选项，将使用最后一次。

## `--cert-status` (SSL)

告诉 `curl` 通过证书状态请求（OCSP 封装）TLS 扩展验证服务器证书的状态。

如果启用了此选项且服务器发送了无效（例如已过期）响应，如果响应表明服务器证书已被撤销，或者没有收到任何响应，则验证将失败。

目前仅在 OpenSSL、GnuTLS 和 NSS 后端实现。（在 7.41.0 中添加）

## `--false-start` (SSL)

告诉 `curl` 在 TLS 握手期间使用伪启动（false start）。伪启动是一种模式，TLS 客户端在验证服务器的 Finished 消息之前就开始发送应用数据，在执行完整握手时可以节省一次往返。

目前仅在 NSS 和 Secure Transport（在 iOS 7.0 或更高版本上，或 OS X 10.9 或更高版本上）后端实现。（在 7.42.0 中添加）

## `-f, fail` (HTTP)

在服务器错误时静默失败（无任何输出）。这主要是为了让脚本等更好地处理失败的尝试。当 HTTP 服务器无法交付文档时，它会返回一个说明情况的 HTML 文档（通常会描述原因以及为什么）。此标志将防止 `curl` 输出并返回错误代码 22。

此方法不是安全的，在某些情况下非成功的响应码会漏掉，特别是在涉及认证时（响应码 401 和 407）。

## `-F, --form <name=content>` (HTTP)

这允许模拟用户已按下提交按钮的已填充表单。这会导致 `curl` 使用根据 RFC 2388 的 `Content-Type multipartform-data` 来 POST 数据。这允许上传二进制文件等。要强制将‘content’部分视为文件，请在文件名前加 `@` 符号。要从文件获取内容部分，请在文件名前加符号 `<`。`@` 和 `<` 的区别在于 `@` 将作为文件上传附加到 post 中，而 `<` 创建文本字段并从文件中获取该文本字段的内容。

例如，将密码发送到服务器，其中‘password’ 是表单字段名，而 `/etc/passwd` 是输入内容：

```
curl -F 'password=@/etc/passwd' https://example.com/upload
```



`curl -F password=@/etc/passwd www.mypasswords.com`

要从 stdin 而不是文件读取内容，请使用 `-` 作为文件名。这适用于 `@` 和 `<`。

你可以通过使用 `type` 告诉 `curl` 使用哪种 `Content-Type`，方式类似于：

```
curl -F "web=@index.html;type=text/html" url.com
```

或者

```
curl -F "name=daniel;type=text/foo" url.com
```

你也可以通过设置 `filename=` 来显式更改文件上传部分的名称字段，例如：

```
curl -F "file=@localfile;filename=nameinpost" url.com
```

如果 `filename/path` 包含 `,` 或 `'`，则必须用双引号引用，如：

```
curl -F "file=@localfile;filename=nameinpost" url.com
```

或者

```
curl -F 'file=@localfile;filename=nameinpost' url.com
```

注意，如果文件名/路径被双引号引用，文件名中的任何双引号或反斜杠必须用反斜杠进行转义。

在 `MANUAL` 中查看更多示例和细节。

此选项可以使用多次。

### `--ftp-count [data]` (FTP)
当 FTP 服务器在提供用户名和密码后请求“账户数据”时，该数据将使用 `ACCT` 命令发送出去。（在 7.13.0 中添加）

如果多次使用此选项，将以最后一次为准。

### `--ftp-alternative-to-user <command>` (FTP)
如果使用 `USER` 和 `PASS` 命令身份验证失败，则发送此命令。在使用客户端证书连接到 Tumbleweed 的 Secure Transport 服务器时，`SITE AUTH` 将告诉服务器从证书中检索用户名。（在 7.15.5 中添加）

### `--ftp-create-dirs` (FTP/SFTP)
当 FTP 或 SFTP URL/操作使用了服务器上当前不存在的路径时，`curl` 的默认行为是失败。使用此选项，`curl` 将仍尝试创建目录。

### `--ftp-method [method]` (FTP)
控制 `curl` 应该使用何种方法访问文件，可选以下替代方案之一：

- `multcwd`: `curl` 为给定 URL 中的每个部分执行一次 `CWD` 操作。对于深层层次结构，这意味着许多命令。这是 RFC 1738 建议的做法。这是默认行为，也是最慢的。
- `nocwd`: `curl` 完全不执行 `CWD`。`curl` 执行 `SIZE`、`RETR`、`STOR` 等命令并为服务器提供完整路径。这是最快的行为。
- `singlecwd`: `curl` 对目标目录执行一次 `CWD` 并“正常地”操作文件（类似于 `multcwd` 的情况）。这比 `nocwd` 更有兼容性，但没有 `multcwd` 的副作用。（在 7.15.1 中添加）

### `--ftpas` (FTP)
使用被动模式连接数据。被动是内部默认，但使用此选项可以覆盖之前的 `--ftp-port` 选项。（在 7.0 中添加）如果多次使用此选项，仅使用第一个。除非使用 `EPSV`，否则被动模式将触发 `PASV` 命令然后跳过。

### `--skip-pasv-ip` (FTP)
告诉 `curl` 在连接数据时不要在响应 `PASV` 命令中使用 IP 地址。`Curl` 将重用它已使用的 IP 地址。（在 7.14.2 中添加）如果使用 `EPSV` 代替 `PASV`，则此选项无效。

### `--ftp-pret` (FTP)
在 `PASV` 之前发送 `PRET` 命令。某些 FTP 服务器需要此非标准命令用于目录列表以及下载。（在 7.20 中添加）

### `--ftp-ssl-ccc` (FTP)
使用 `CCC`（清晰命令通道）。身份验证后关闭 SSL/TLS 层。剩余的通信将是不加密的。这允许 NAT 路由器跟踪事务。更多信息请参阅 `--ftp-ssl-ccc-mode`。（在 7.1 中添加）

### `--ftp-ssl-ccc-mode [active/passive]`
使用 `CCC`（清晰命令通道）。被动模式不会启动关闭，而是等待服务器执行；活动模式将启动关闭并等待服务器的回复。（在 7.1.2 中添加）

### `--ftp-ssl` (FTP)
要求 FTP 登录使用 SSL/TLS。允许安全认证，但如果服务器不支持 SSL/TLS，非加密数据传输将失败。（在 7.16.0 中添加）仍可以使用，但在未来的版本中将被移除。

### `--form-string <name><string>` (HTTP)
与 `--form` 类似，但值字符串是字面使用的。开头的 `@` 和 `<` 字符以及值中的 `type=` 字符串没有特殊含义。使用此项的字符串可能会意外触发 `--form` 的 `@` 或 `<` 功能。

### `-g`, `--globoff`
关闭 URL 通配符解析。设置此选项时，可以指定包含 `{}` 字母的 URL 而不会被 `curl` 解释。注意这些字母不是合法的 URL 内容，但应根据 URI 标准进行编码。

### `-G`
当使用此选项时，它将使所有 `-d`、`--data`、`--data-binary` 指定的数据变为 GET 请求，而不是通常使用的 POST 请求。数据将通过 `?` 分隔附加到 URL。如果结合 `-I` 使用，POST 数据将通过 HEAD 请求附加到 URL。如果多次使用此选项，仅使用第一个。因为 GET 没有意义，但你应该强制执行你首选的替代方法。

### `-H`, `--header <header>` (HTTP)
向服务器发送 HTTP 时包含的额外头部。你可以指定任意数量的额外头部。注意，如果你添加与 `curl` 内部使用的头部同名的自定义头部，你设置的头部将代替内部头部。这允许你执行比 `curl` 通常情况下更复杂的操作。在不清楚自己在做什么的情况下不要替换内部设置的头部。通过在冒号右侧提供替换内容来移除内部头部，如 `-H "Host"`：如果你使用无值的自定义头部，则它必须以分号结束，如 `-H "X-Custom-Header"`；发送 "X-Custom-Header"。`curl` 将确保每个添加/替换的头部都带有正确的行尾标记，你不应该将其作为头部内容的一部分：不要添加换行符或回车符，它们只会搞乱你的设置。参见 `-A,--user-agent` 和 `-e,--referer` 选项。从 7.37.0 开始，你需要用于代理的自定义头部。示例：

```
# curl -H "X-First-Name: Joe" http://192.168.0.1/
```



警告：在使用 `-L`, `--location` 时，带有此选项的头部将在所有请求中设置——即使跟随重定向。这可能导致头部被发送到原始主机以外的主机，因此敏感头部在结合重定向时应谨慎使用。此选项可以使用多次来添加/替换/删除多个头部。

### `--hostpubmd5 <md5>` (SCP/SFTP)
传递包含 32 个十六进制数字的字符串。该字符串是远程主机公钥的 128 位 MD5 校验和，除非 `md5` 匹配，否则 `curl` 将拒绝连接。（在 7.17.1 中添加）

### `--ignore-content-length` (HTTP)
忽略 `Content-Length` 头部。这对于运行 Apache 1.x 的服务器特别有用，该服务器会在大于 2GB 的输出中包含正确的 `Content-Length`。

### `-i,--include` (HTTP)
在输出中包含 HTTP 头部。HTTP 头部包括服务器名称、内容日期、HTTP 版本等内容……

### `-I,--head` (HTTP/FTP/FILE)
仅获取 HTTP 头部！HTTP 服务器功能

`HEAD` 命令仅用于获取文档的标头。当用于 FTP 或 FILE 文件时，`curl` 会显示文件大小和最后修改时间。

### `-interface <name>`
使用指定的接口执行操作。你可以输入接口名称、IP 地址或主机名。例如：

```
curl --interface eth0:1 http://www.netscape.com/
```

如果多次使用此选项，将以最后一次为准。

### `-j,--junk-session-cookies` (HTTP)
当告诉 `curl` 从给定文件读取 cookie 时，此选项将忽略所有“会话 cookie (session cookies)”。这在基本上等同于启动了一个新会话。典型的浏览器在关闭时总是丢弃会话 cookie。

### `-J,--remote-header-name` (HTTP)
此选项将告诉 `-O,--remote-option` 使用服务器的 `Content-Disposition` 字段中的文件名来从文件中提取。

目前尚未尝试对提供的文件名进行 `%sequences` 序列解码，因此此选项可能会为你提供意料之外的文件名。

### `-k,--insecure` (SSL)
此选项显式允许 `curl` 执行“不安全”的 SSL 连接和传输。所有的 SSL 连接都会尝试通过使用默认安装的 CA 证书包来确保安全。这使得除非使用了 `-k,--insecure`，否则所有连接都会被视为“不安全”并失败。

请查看此在线资源以获取更多详情：http://curl.haxx.se/docs/sslcerts.html

### `-K,--config <config file>`
指定从哪个配置文件读取 `curl` 参数。配置文件是一个文本文件，可以在其中编写命令行参数，然后它们将像直接在实际命令行中编写的一样被使用。

选项及其参数必须在同一个配置文件指定，并用空格、冒号或等号分隔。在配置文件中可以可选提供长选项名称，而无需加开头的双横杠，如果是这样，可以使用冒号或等号字符作为分隔符。如果使用一个或两个横杠指定选项，则选项与参数之间不能有冒号。

如果参数包含空格，则参数必须包含在引号内。在双引号内，以下转义序列有效：`\"`、`\\`、`\t`、`\n` 和 `\`。在任何其他字母之前的反斜杠将被忽略。如果配置文件的第一列是 `#`，则该行的其余部分将被视为字符。配置文件中的每个物理行只能包含一个选项。

为 `-K,--config` 指定文件名可以让 `curl` 从标准输入 `stdin` 读取配置文件。

注意，要在配置文件中指定 URL，你需要使用 `--url` 选项进行指定，而不是简单地单独写一行 URL。因此，它看起来可能类似于：

```
url = "http://curl.haxx.se/docs/"
```

当调用 `curl` 时，它总是（除非使用 `-q`）检查默认配置文件，如果找到则使用它。按照以下顺序检查默认配置文件的位置：

1) `curl` 尝试寻找“主目录”：它首先检查 `CURL_HOME` 然后是 `HOME` 环境变量。如果失败，在 Unix 类系统上将使用 `getpwuid()`（返回系统中当前用户的主目录）。在 Windows 上，它会检查 `APPDATA` 变量，最后的手段是 `"%USERPROFILE%\Application Data"`。

2) 在 Windows 上，如果主目录下没有 `~curl` 文件，它会检查 `curl` 执行目录下的文件。在 Unix 类系统上，它仅尝试在确定的主目录下加载 `curl`。

# -- Example file -- # 这是一个注释

```
url = "curl.haxx.se"

output = "curlhere.html"

user-agent = "useragent/1.0"

and fetch another URL to url = "curl.haxx.se/docs/manage.html" -0 referred "http://nowhereall.com/"
```

-- End of example file --



此选项可以多次使用来加载配置文件。

- `--keepalive-time <seconds>` 此选项设置连接在发送心跳探针之前保持空闲的时间，以及单个心跳探针之间的时间。它目前在提供 `TCP_KEEPIDLE` 和 `TCP_KEEPINTVL` 套接选项的操作系统上（如 Linux、AIX、HP-UX 等）有效。如果使用了 `--no-keepalive`，则此选项无效。（7.18.0 版本引入）。

如果多次使用此选项，将以最后一次为准。如果未指定，该选项默认为 60 秒。

- `--<key>` (SSL/SSH) 私钥名称。允许你在此单独的文件中提供私钥。对于 SSH，如果指定了，curl 将按顺序查找以下候选路径：`/.ssh/id_rsa`、`~/.ssh/id_dsa`、`.id_rsa`、`/id_dsa`。

如果多次使用此选项，将以最后一次为准。

- `--<key> <type>` (SSL) 私钥类型。指定 `--key` 提供的私钥是什么类型，支持 DER、PEM 和 ENG。如果未指定，则假设为 PEM。

如果多次使用此选项，将以最后一次为准。

- `--krb<level>` (FTP) 启用 Kerberos 认证和使用。必须输入级别，且应该是 `clear`、`safe`、`confidential` 或 `private` 之一。你应该使用一个不在这些中的级别，将使用 `private`。

如果多次使用此选项，将以最后一次为准。

- `-l,--list` (FTP) 列出 FTP 目录时，此开关强制列出。这对于用户想要查看内容特别有用。

- `-L,--location` (HTTP/HTTPS) 如果服务器报告请求页面已移动到其他位置（由 3xx 响应码指示），此选项将跟随重定向。如果与 `-i,--include` 或 `-I` 配合使用，将显示所有请求页的头部。当 curl 跟重定向且请求不是纯 GET（例如 POST 或 PUT）时，如果响应码为 301、302 或 303，它将使用 GET 执行后续请求。如果响应码是任何其他 3xx，curl 将使用原始方法重发后续请求。你可以通过专门的选项 `--post301`、`--post302` 和 `--post303` 让 curl 在 3xx 后将非 GET 方法改为 GET。

- `-libcurl<file>` 将此附加到任何 curl 命令行，将在文件中获得相当于命令行操作的 libcurl-c 源码！

如果多次使用此选项，将使用最后给出的文件名。（7.16.1 版本引入）

- `-limit-rate<speed>` 指定 curl 下载和上传的最大传输速率。如果你有带宽限制并希望让传输比通常情况下慢，则此功能非常有用。

速率以字节/秒测量，除非附加了后缀。附加 `k` 或 `K` 将将数字视为千字节，`m` 或 `M` 代表兆字节，而 `g` 或 `G` 代表吉字节。示例：`200K`、`3m` 和 `1G`。

速率是整个传输过程中计算的平均速度。这意味着 curl 可能会在短时间内使用更高的速度，但从长远来看它不会超过给定的速率。如果你还使用了 `-Y,--speed-limit` 选项，该选项将优先并可能会略微影响速率限制。

如果多次使用此选项，将以最后一次为准。

- `-local-port<num>[-num]` 设置用于连接的首选本地端口号或端口号范围。注意，端口号本质上是稀缺资源，将

在将此范围设置为某些值时，可能会导致不必要的连接建立失败。（在 7.15.2 中添加）

- `--location-trusted` (HTTP/HTTPS) 类似于 `-L,--location`，但允许将用户名+密码发送到网站可能重定向到的所有主机。如果网站将您重定向到一个你会发送身份信息的站点（在 HTTP Basic 认证的情况下，该信息是明文的），这可能会也可能不会引入安全漏洞。

- `-m,--seconds<数字>` 允许整个操作消耗的最大时间（秒）。这有助于防止您的批处理作业因网络缓慢或链接中断而挂起数小时。从 7.32.0 开始，此选项接受小数值，但随着指定的超时时间小数精度的增加，实际超时时的准确性将会降低。另请参见 `--connect-timeout` 选项。

如果多次使用此选项，将使用最后一次指定的。

- `--login-options <options>` 指定在服务器身份验证期间使用的登录选项。你可以使用登录选项来指定身份验证期间可能使用的协议选项。目前 IMAP、POP3 和 SMTP 支持登录选项。有关登录选项的更多信息，请参阅 RFC 2384、RFC 5092 和 IETF draft-earhart-smtp-00.txt。（在 7.34.0 中添加）。

如果多次使用此选项，将使用最后一次指定的。

- `--mail-auth <address>` (SMTP) 指定单个地址。这将用于指定提交并中继到另一个服务器的邮件的验证地址（身份）。

（在 7.25.0 中添加）

- `--mail-from <address>` (SMTP) 指定指定邮件发送的单个地址。

（在 7.20.0 中添加）

- `--max-size <bytes>` 指定下载文件的最大大小（字节）。如果请求的文件大于此值，传输将不会开始，并返回退出代码 63。

注意：在下载之前并不总是知道文件大小的，对于此类文件，如果文件最终超过了此限制，则此选项将不起作用。这涉及 FTP 和 HTTP 传输。

- `--mail-rcpt <address>` (SMTP) 指定单个地址、用户名或邮件列表名称。

在执行邮件传输时，接收者应验证一个有效的电子邮件地址以发送邮件。（在 7.20.0 中添加）

在执行地址验证（VFRFY 命令）时，接收者应指定为用户名或域名（如 RFC5321 第 3.5 节所示。（在 7.34.0 中添加）。

在执行邮件列表展开（EXPN 命令）时，接收者应使用邮件列表名称，例如“Friends”或“London-Office”。（在 7.40.0 中添加）。

- `--max-redirs <num>` 设置允许的最大重定向跟随次数。如果使用了 `-L, --location`，可以使用此选项防止 curl “荒谬地”无限跟随重定向。默认情况下，限制设置为 50 次重定向。将此选项设置为 -1 可使其无限制。

如果多次使用此选项，将使用最后一次指定的。

- `--metalink` 此选项可以告诉 curl 将给定的 URI 解析并处理为 Metalink 文件（支持版本 3 和 4 (RFC 5854)），并在发生错误（例如服务器故障或不可用）时利用其中列出的镜像。它还会在下载完成后验证文件的哈希值。Metalink 文件本身在内存中下载和处理，不会存储在本地系统文件中。

使用远程 Metalink 文件的示例：

```
curl --metalink http://www.example.com/example.metalink
```

在本地文件系统中使用 Metalink 文件，使用 FILE 协议（file://）：

```
curl --metalink file://example.metalink
```

请注意，如果禁用了 FILE 协议，在本文编写无法使用本地 Metalink 文件。另注意，当 `--metalink` 和 `--include` 一起使用时，include 将忽略。这是因为在响应中包含头部会破坏 Metalink 解析器，如果头部包含在 Metalink 文件中描述的文件中，哈希检查将失败。

（在 7.27.0 中添加，前提是已针对 libmetalink 库构建。）

- `-netrc` 让 curl 在用户主目录下搜索 `.netrc`（Windows 上为 `.netrc`）文件以查找用户名和密码。这通常用于 Unix 上的 FTP。对于 HTTP，curl 将启用用户身份验证。有关文件格式的详情，请参阅 netrc(5) [ftp(1)]。如果文件权限不对，curl 不会报错（它应该是全局或用户组可读的）。使用环境变量 `HOME` 来查找主目录。

一个如何设置 `.netrc` 以允许 curl 使用用户名 ‘myself’ 和密码 ‘secret’ FTP 到 machine.domain.com 的快速且简单的示例如下所示：

```
machine host.domain.com login myself password secret
```



进入`/path/to/xxx`目录，找到`xxx.json`。

`-N, --no-buffer` 禁用输出流的缓冲。在正常情况下，`curl` 将使用标准的缓冲输出流，其效果是分块输出数据，而不一定恰好在数据到达时输出。使用此选项将禁用缓冲。

注意，这是被记录的反向选项。随后你可以使用 `--buffer` 来强制缓冲。

`--netrc-file` 此选项与 `--netrc` 类似，区别在于你提供了 Curl 应该使用的 netrc 文件的路径（绝对路径或相对于 netrc 文件的相对路径）。每次调用只能指定一个 netrc 文件。如果提供了多个 `--netrc-files` 选项，将使用最后一个。
（在 7.21.5 中添加）

此选项会覆盖任何对 `--netrc` 使用，因为它们是互斥的。如果指定，它还将遵循 `--netrc-optional`。

`--netrc-optional` 与 `--netrc` 非常相似，但此选项使 `.netrc` 的使用变为可选，而不是像 `--netrc` 选项那样是强制性的。

`--negotiate` (HTTP) 启用 Negotiate (SPNEGO) 认证。

如果你想为代理认证启用 Negotiate (SPNEGO)，请使用 `--proxy-negotiate`。

此选项需要构建了 GSS-API 或 SSPI 的库。使用 `-V, --version` 查看你的 curl 是否支持 GSS-API/SSPI 和 SPNEGO。

在使用此选项时，你也可以提供 `-u, --user` 选项以正确激活身份验证代码。发送 `'--u '` 即可，因为 `--u` 选项的用户名和密码实际上并未被使用。

如果多次使用此选项，将使用最后一次指定的。

`--keepalive` 禁用长连接的使用。

`--sessionid` (SSL) sessionid 的使用。

`--ntlm` (HTTP) 启用 NTLM 认证。

(新增于 7.37.0)

`-p,--proxtunnel` 当使用 HTTP 代理 (`-x,--proxy`) 时，此选项将导致非 HTTP 协议尝试通过代理进行隧道传输，而不仅仅是用于执行类似 HTTP 的操作。通过 HTTP 代理的 CONNECT 请求实现的隧道方法要求代理允许直接连接到 curl 想要隧道传输的远程端口。

`-P,--ftp-port <address>` (FTP) 在与 FTP 连接时，反转默认的启动者/监听者模式。此切换开关使 curl 处于主动模式。在实践中，curl 告诉服务器连接回客户端指定的地址和端口，而被动模式则要求服务器设置一个 IP 地址和端口供其连接。`<address>` 可以是以下之一：

`eth0`，用于指定你想要使用的接口的 IP 地址（仅限 Unix）
IP 地址，例如 `192.168.10.1`，用于指定确切的 IP 地址
主机名，例如 `my.host.domain`，用于指定机器

让 curl 选择已用于控制连接的 IP 地址。如果多次使用此选项，将使用最后一个。使用 `--ftp-pasv` 禁用 PORT 命令的使用。使用 `--disable-eprt` 禁用尝试使用 EPRT 命令代替 PORT。EPRT 实际上是 PORT 的增强版。

从 7.19.5 开始，你可以在地址右侧附加 `--[start]-[end]`，以告诉要使用哪个 TCP 端口范围。这意味着当你指定端口范围时，是从较小的数字到较大的数字。单个数字效果良好，但不要忘记这会增加失败风险，因为该端口可能不可用。

`--pass <phrase>` (SSL/SSH) 私钥的密码 phrase

如果多次使用此选项，将使用最后一个。

`--pass-as-is` 告诉 curl 不要处理给定的 URL 路径中的 `../` 或 `//` 序列。通常 curl 会根据标准压缩或合并它们，但使用此选项后你设置 curl 不要这样做。

(新增于 7.42.0)

`--post301` (HTTP) 告诉 curl 遵循 RFC 2616/10.3.2，在跟随 301 重定向时不将 POST 请求转换为 GET 请求。

`--post302` (HTTP) 告诉 curl 遵循 RFC 2616/10.3.2，在跟随 302 重定向时不转换 POST 请求。

`--post303` (HTTP) 告诉 curl 遵循 RFC 2616/10.3.2，在跟随 303 重定向时不将 POST 请求转换为 GET 请求。

`--proto <protocols>` 告诉 curl 使用列出的协议进行初始检索。协议从左到右评估，用逗号分隔，每个都是一个协议名称或 `all`，可选地带有零或多个修饰符前缀。

例如：
`--proto -ftps` 使用默认协议，但禁用 ftps
`--proto -all,https,+http` 仅启用 https 和 http
`--proto =http,https` 同时也启用 https 和 http

未知的协议会产生警告。

此选项可以使用多次，在这种情况下效果等同于将协议合并到一个选项实例中。

(新增于 7.20.2)

`--proxy-anyauth` 告诉 curl 在与给定代理通信时选择合适的身份验证方法。这可能会导致额外的请求/响应往返。（新增于 7.13.2)

`--proxy-basic` 告诉 curl 在与给定代理通信时使用 HTTP Basic 身份验证。

`--proxy-digest` 告诉 curl 在与给定代理通信时使用 HTTP Digest 认证。

`--proxy-negotiate` 告诉 curl 在与给定代理通信时使用 HTTP Negotiate (SPNEGO) 认证。

`--proxy-ntlm` 告诉 curl 在与给定代理通信时使用 HTTP NTLM。

`--proxy-ntlm-service-name <service>` 告诉 curl 在与给定代理通信时使用 NTLM 服务名称。

`--proxy-ntlm-domain <domain>` 告诉 curl 在与给定代理通信时使用 NTLM 域。

`--proxy-ntlm-username <username>` 告诉 curl 在与给定代理通信时使用 NTLM 用户名。

`--proxy-ntlm-password <password>` 告诉 curl 在与给定代理通信时使用 NTLM 密码。

`--proxy-ntlm-host <host>` 告诉 curl 在与给定代理通信时使用 NTLM 主机。

`--proxy-ntlm-workstation <workstation>` 告诉 curl 在与给定代理通信时使用 NTLM 工作站。

`source_file target_file`
`ln` 和 `symlink` 命令创建指向 `target_file` 位置的符号链接
`mdir directory_name`

`mkdir` 命令创建名为 `directory_name` 的目录。
`pwd`
`pwd` 命令返回当前目录的绝对路径。

`rename` 命令重命名由源操作数命名的文件或目录到目标路径指定的路径。
`rm`
`rm` 删除操作数指定的文件。`mdir` 删除目录操作数指定的目录项，前提是它是空的。
`symlink source_file target_file`

查看 `ln`。
`-r,--range <range>` (HTTP/FTP/SFTP/FILE) 从 HTTP/1.1、FTP 或 SFTP 服务器或本地 FILE 获取字节范围。

`0-499` 指定前 500 个字节
`500-999` 指定第二个 500 个字节
`-500` 指定最后 500 个字节
`9500-` 指定从偏移量 9500 开始的字节

`+chgrp group`
`chgrp` 命令将操作数命名的文件组 ID 设置为指定的组。组操作数是十进制数字。

`+chmod mode`
`chmod` 命令修改指定文件的模式位。模式是一个八进制数。

`+chown user`
`chown` 命令将操作数命名的文件所有者设置为指定的用户。用户操作数是十进制数字。

`-R,--remote` 当使用时，它将使 curl 尝试获取远程文件的时间戳，如果该时间戳可用，则让本地文件获取该时间戳。

`--random-file <file>` (SSL) 指定包含被视为随机数据的文件路径。

`---raw` (HTTP) 使用时，它将禁用对所有内容或传输编码的内部 HTTP 解码，转而对未修改的原始数据进行这些操作。

`---remote-all` 此选项更改了所有给定 URL 的默认操作，即如果对每个 URL 都使用了 `-O,--remote-name`。

`---resolve <host:port:address>` 为特定的主机和端口对提供自定义地址。

`---retry <num>` 如果 curl 在尝试执行传输时返回瞬态错误，它将在放弃之前重试该数字的次数。

`---retry-delay <seconds>` 当传输因瞬态错误失败时，Curl 在每次重试前睡眠该长度的时间。

`---retry-max-time <seconds>` 重试计时器在第一次传输尝试之前重置。

`-s, —silent` 静默或安静模式。不显示进度表或错误信息。

`---sasl-ir` 启用带有 SASL 认证的初始。

`---service-name` 此选项允许你更改 SPNEGO 的服务名称

示例：`—negotiate —service sockd` 将使用 sockd/server-name。

`-S, —error` 与 `-s` 一起使用，如果 curl 失败，它会输出错误消息。

`---ssl` (FTP, POP3, IMAP, SMTP) 使用 SSL/TLS 进行连接。

`---sslsqd` (FTP, POP3, IMAP, SMTP) 连接需要 SSL/TLS。

`---allow-beast` (SSL) 此选项告诉 curl 不要绕过使用 BEAST 的 SSL3 和 TLS1.0 协议的安全漏洞。

`---socks4 <host[:port]>` 使用指定的 SOCKS4 代理。

`socks5-hostname <host[:port]>` 使用指定的 S5 代理并在本地解析主机。

`socks5 [host[:port]]` 使用指定的 SOCKS5 代理。

`---stderr <file>` 将所有写入 stderr 的内容重定向到指定的文件。

`—-,telnet-option <OPT=val>` 向 telnet 协议传递选项。

`-T,--upload-file <file>` 这将指定的文件传输到远程 URL。

`--tcp-nodelay` 开启 TCP_NODELAY 方法。

`--ftp-blksize <value>` (TFTP) 设置 TFTP BLKSIZE 选项。

`--lsautype <type>` 设置 TLS 认证类型。

`--tlpassword<password>` 设置密码。

`--tluser<user>` 设置用户名。

`--tlsv1.0` (SSL) 强制 curl 在与远程 TLS 服务器协商时使用 TLS 1.0 版本。
`--tlsv1.1` (SSL) 强制 curl 在与远程 TLS 服务器协商时使用 TLS 1.1 版本。
`--tlsv1.2` (SSL) 强制 curl 在与远程 TLS 服务器协商时使用 TLS 1.2 版本。

`--trace-encoding` (HTTP) 请求使用 curl 支持的算法之一的压缩 Transfer-Encoding 响应，并在接收时进行解压。

`--trace <file>` 启用所有输入和输出数据的完整跟踪转储到输出文件。

`--trace-ascii <file>` 启用所有输入和输出数据的完整跟踪转储到输出文件。

`--trace-time` 在 curl 显示的每行跟踪或详细信息前添加时间戳。

`--unix-socket <path>` (HTTP) 通过此 Unix 域套接字连接，而不是使用网络。

`-u,--user <user:password>` 指定用于服务器认证的用户名和密码。

`-U,--proxy-server <user:password>` 指定用于代理认证的用户名和密码。

`--url <URL>` 指定要获取的 URL。

| 变量 | 描述 |
| :--- | :--- |
| `size_download` | 下载的总字节数。 |
| `size_header` | 下载头部的总字节数。 |
| `size_request` | 在 HTTP 请求中发送的总字节数。 |
| `size_upload` | 上传的总字节数。 |
| `speed_download` | curl 测量的完成下载平均速度（字节/秒）。 |
| `speed_upload` | curl 测量的完成上传平均速度（字节/秒）。 |
| `time_appconnect` | 从开始到完成 SSL/SSH/等 连接/握手所需的时间（秒）。 |
| `time_connect` | 从开始到与远程主机（或代理）TCP 连接完成的时间（秒）。 |
| `time_namelookup` | 从开始到域名解析完成的时间（秒）。 |
| `time_pretransfer` | 从开始到文件传输即将开始所需的时间（秒）。 |
| `time_redirect` | 完成所有重定向步骤所需的时间（秒）。 |
| `time_starttransfer` | 从开始到第一个字节即将传输所需的时间（秒）。 |

`time_total`

整个操作持续的总时间，单位为秒。时间将以毫秒级显示。

`url_effective`

获取的 URL。

`- -x, --proxy <protocol://[user:password@]proxyhost[:port]>`
使用指定的代理。

`- -X, --request<command>` (HTTP)
指定在与 HTTP 服务器通信时使用的自定义请求方法。

`- --xattr`
在将输出保存到文件时，此选项告诉 curl 将某些文件元数据存储在扩展文件属性（xattr）中。

`- -y, --speed-limit <time>`
如果下载在速度-时间段内的速度低于 `speed-limit` 字节/秒，则下载将中止。

`- -Y, --speed-limit <speed>`
如果下载在 `speed-time` 时间内速度低于给定的速度（字节/秒），则将中止。

`- -z, --time-cond <expression>|<file>` (HTTP/FTP)
请求修改时间晚于给定日期/时间的文件。

`- -h, --help`
用法帮助。

`- -M, --manual`
手册。显示帮助文本。

`- -V, --version`
显示关于 curl 及其使用的 libcurl 的信息。

### IPv6
你可以配合此使用 IPv6。

### krb4
自 7.21.7 起

### SSL
自 7.21.7 起

### Async
自 7.21.7 起

### NTLM
自 7.21.7 起

### Debug
自 7.21.7 起

### GSSAPI
自 7.21.7 起

### IDN
自 7.21.7 起

### GSS
自 7.21.7 起

### SSPI
自 7.21.7 起

### SRP
自 7.21.7 起

### HTTP2
自 7.21.7 起

### Metalink
自 7.21.7 起

## EXIT CODES
在不良情况下可能出现的各种错误代码及其相应的错误消息。

`- 1` 不支持协议。
`- 2` 初始化失败。
`- 3` URL 格式错误。
`- 4` 需要的功能或选项未启用或在编译时被禁用。
`- 5` 无法解析代理。
`- 6` 无法解析主机。
`- 7` 连接主机失败。
`- 8` FTP 服务器回复。
`- 9` FTP 拒绝访问。
`- 11` FTP 异常 PASS 回复。
`- 13` FTP 异常 PASV 回复。
`- 14` FTP 异常 227 格式。
`- 15` FTP 无法获取主机。
`- 17` FTP 无法设置二进制。
`- 18` 部分文件。
`- 19` FTP 无法下载/访问给定文件，RETR 命令失败。
`- 21` FTP 引用错误。

HTTP 页面未检索。未找到指定的 URL 或返回了 HTTP 错误码 400 或以上的其他错误。

写入错误。Curl 无法将数据写入本地文件系统或类似位置。

FTP 无法 STOR 文件。服务器拒绝了 STOR 操作。

读取错误。各种读取方面出现的问题。

内存不足。内存分配请求失败。

操作超时。根据指定条件达到了指定的超时时间。

FTP PORT 失败。PORT 命令失败。

FTP 无法使用 REST。REST 命令失败。

HTTP 范围（range）错误。

HTTP post 错误。内部 post 请求生成错误。

SSL 连接错误。SSL 握手失败。

FTP 下载点续传错误。无法继续之前已中断的下载。

FILE 无法读取文件。打开文件失败。

LDAP 无法绑定。LDAP 绑定操作失败。

LDAP 搜索失败。

未找到函数。未找到所需的 LDAP 函数。

被回调中止。应用程序告诉 curl 取消操作。

内部错误。调用函数时使用了错误的参数。

接口错误。无法使用指定的输出接口。

重定向过多。在跟随重定向时，curl 达到了最大数量。

`48` 为 libcurl 指定了未知选项。

`49` 格式错误的 telnet 选项。

`51` 对方的 SSL 证书或 SSH MD5 指纹不正确。

`52` 服务器没有返回任何内容，在这里被视为错误。

`53` 未找到 SSL 加密引擎。

`54` 无法将 SSL 加密引擎设置为默认。

`55` 发送网络数据失败。

`56` 接收网络数据失败。

`58` 本地证书问题。

`59` 无法使用指定的 SSL 密码算法。

`60` 无法通过已知 CA 证书验证对方证书。

`61` 不的传输编码。

`62` 无效的 LDAP URL。

`63` 超过最大文件大小。

`64` 请求的 FTP SSL 级别失败。

`66` 发送数据需要回溯但失败了。

`67` 初始化 SSL 引擎失败。

`68` 用户名、密码或类似信息未通过，curl 登录失败。

`69` TFTP 服务器上文件文件。

`70` TFTP 服务器权限问题。

# 作者 / 贡献者

Daniel Stenberg 是主要作者，贡献者列表可以在单独的 THANKS 文件找到。

# FTP

`ftp://ftp.sunet.se/pub/www/utilities/curl/`

### 参见

`ftp(1)`, `wget(1)`

## 名称

`cut` - 从文件的每行中删除部分

### 摘要

`cut OPTION... [FILE]...`

### 描述

从每个 FILE 中将选定的部分打印到标准输出。

`- -b, --bytes=LIST` 仅选择这些字节
`- -c, --characters=LIST` 仅选择这些字符
`- -d, --delimiter=DELIM` 使用 DELIM 代替 TAB 作为字段分隔符
`- -f, --fields=LIST` 仅选择这些字段
`- -n` 配合 `-b`：不拆分多字节字符
`-- --complement` 补全所选字节、字符或字段的集
`- -s, --only-delimited` 不打印包含分隔符的行
`-- --output-delimiter=STRING` 使用 STRING 作为输出分隔符
`-- --help` 显示此帮助并退出
`-- --version` 输出版本信息并退出

### 作者

由 David Stenberg, MacKenzie 编写。

# 报告 bug

向此处报告 bug：`http://www.gnu.org/bugs`

# 版权

Copyright © 2015 Free Foundation, Inc. 根据 GPL3 许可。

## 名称

`da` - 设置环境并创建语言

### 描述

`da` 是 DevAssistant 的主命令。

`- -debug` 让 DevAssistant 记录大量的调试信息
`- -no-cache` 让 DevAssistant 读取所有独立的助手并完全忽略缓存

**create** 创建新项目、安装依赖并设置环境
**modify** 修改之前创建的项目
**prepare** 为上游项目准备开发环境
**task** 执行与特定项目无关的自定义任务

# 描述 - 操作

DevAssistant 的设计旨在通过所谓的“操作”（actions）提供自定义功能。

**help** - 显示详细的帮助信息。
**version** - 显示 devassistant 版本。

# 通用选项

`- -h—help` 为所选的助手打印帮助信息。
`- -n—name` 项目名称。
`- -e—eclipse` 将项目导入到 eclipse 环境。
`- -g—github<username>` 创建一个 GitHub 仓库并将初始源码推送到那里。
`- -b—build` 生成 SPEC 文件、SRP 并模拟构建 RPM。
`- -v—vim` 安装针对此语言的 vim 设置

# 环境

# DEVASSISTANT_PATH

一个用冒号分隔的目录列表，在其中搜索助手。

# 另请参考

`da-gui(1)`

# 概要览

```



# date

```
date [OPTION]... [+FORMAT] date [-u|--utc|--universal] [MMDDhhmm[[CC]][YY]..ss]
```

### 描述

以给定的 `FORMAT` 显示当前时间，或设置系统日期。
长选项的强制参数对于短选项也是强制的。

- `-d`, `--date=STRING`
  显示 `STRING` 描述的时间，而不是‘now’

- `-f`, `--file=DATEFILE`
  类似于 `--date`；对于 `DATEFILE` 的每一行

- `-[FMT]`, `--iso-8601=[FMT]`
  以 ISO 8601 格式输出日期/时间。`FMT='date'` 表示仅日期（默认值），‘hours’‘minutes’‘seconds’或‘ns’表示到指定精度的日期和时间。示例：
  `2006-08-14T02:34:56-0600`

- `-R`, `--rfc-2822`
  以 RFC 2822 格式输出日期和时间。示例：`Mon, 14 Aug 2006 02:34:56-0600`

- `--rfc-3339=FMT`
  以 RFC 3339 格式输出日期和时间。`FMT='date' 'seconds' 或 'ns'` 表示到指定精度的日期和时间。示例：`2006-08-14 02:34:56-0600`

- `-r`, `--reference=FILE`
  显示 `FILE` 的最后修改时间

- `-s`, `--set=STRING`
  设置 `STRING` 描述的时间

- `-u`, `--utc`, `--universal`
  打印或设置协调世界时 (UTC)

- `--help`
  显示此帮助并退出

- `--version`
  输出版本信息并退出

`FORMAT` 控制输出。被解释的序列为：

- `%%`
  字面量 `%`

- `%a`
  本地化的简短的星期几名称（例如 Sun）

- `%A`
  本地化的全星期几名称（例如 Sunday）

- `%b`
  本地化的简短的月份名称（例如 Jan）

- `%B`
  本地化的全月份名称（例如 January）

- `%c`
  本地化的日期和时间（例如 Thu Mar 3 23:05:25 2005）

世纪；类似于 `%Y`，但省略最后两位数字（例如 20）

月份中的第几天（例如 01）

日期；相当于 `%m/%d/%y`

月份中的第几天，空格填充；相当于 `%_d`

全日期；相当于 `%Y-%m-%d`

ISO 周数的年份的最后两位数字（参见 `%G`）

ISO 周数的年份（参见 `%V`）；通常只与 `%V` 配合使用

与 `%b` 相同

小时（00..23）

小时（01..12）

一年中的第几天（001..366）

小时，空格填充（ 0..12）；相当于 `%_H`

小时，空格填充（ 1..12）；相当于 `%_I`

月份（01..12）

分钟（00..59）

换行符

纳秒（000000000.999999999）

本地化的 AM 或 PM 的等效值；未知则为空

类似于 `%p`，但全小写

本地化的 12 小时制时间（例如 11:11:04 PM）

24 小时时分；相当于 `%H:%M`

自 1970-01-01 00:00:00 以来的秒

```
%S
```

秒（00..60）

```
%t
```

一个制表符

```
%T
```

时间；相当于 `%H:%M`

```
%u
```

星期（1..7）；1 是周一

```
%U
```

年的周数，以周日为一周的第一天（00..53）

```
%V
```

ISO 周数，以周一为一周的第一天（01..53）

```
%w
```

星期（0..6）；0 是周日

```
%W
```

ISO 周数，以周一为一周的第一天（01..53）

```
%X
```

日期；相当于 `%m/%d/%y`

```
%Y
```

年份

```
%y
```

年份的最后两位数字

```
%Z
```

时区名称

```
%z
```

时区偏移（+HHMM或-HHMM）

# DBUS-DAEMON

# NAME

`dbus-daemon` - 消息总线进程

# SYNOPSIS

```
dbus-daemon [--version] [--session] [--system] [--config-file=FILE] [--print-address [=DESCRIPTOR]] [--print-pid [=DESCRIPTOR]] [--fork]
```

# DESCRIPTION

`dbus-daemon` 是 D-Bus 消息总线进程。关于整体架构的更多信息，请参见 `m[](http://www.freedesktop.org/software/dbus/m/)`。D-Bus 首先是一个提供任意两个应用程序之间一对一通信的库；而 `dbus-daemon` 是使用该库来实现消息总线进程的应用程序。多个程序连接到该消息总线进程并可以相互交换消息。

有两个标准的消息总线实例：系统级消息总线（在许多系统中作为“messagebus”服务安装）和用户级登录消息总线（每次用户登录时启动）。`dbus-daemon` 同时用于这两个实例，但使用不同的配置文件。

`--session` 选项等同于 `config-file=/usr/share/dbus-1/session.conf`，而 `--system` 选项等同于 `config-file=/usr/share/dbus-1/system.conf`。通过创建额外的配置文件并使用 `--config-file` 选项，可以创建额外的特殊用途消息总线进程。

系统级进程通常由 `init` 脚本启动，通常简单称为“messagebus”。

系统级进程主要用于广播系统事件，例如发送到打印队列的事件，或添加/移除设备。

会话级进程用于桌面应用程序之间的各种进程间通信（然而，它与 X 或 GUI 没有任何某种关联）。

`SIGHUP` 会导致 D-Bus 进程**部分**重新加载其配置文件并刷新其用户/组信息缓存。某些配置更改需要将所有应用从总线中踢出；因此这些更改只有在重启进程时才会生效。策略更改应通过 `SIGHUP` 生效。

# OPTIONS

支持以下选项：

- `-config-file=FILE`
  使用指定的配置文件。

- `-fork`
  强制消息总线进行派叉（fork）并成为守护进程，即使配置文件没有指定这样做。不过，在大多数情况下，配置文件已经正确处理了这一点。此选项在 Windows 上不支持。

- `-nofork`
  强制消息总线不要进行派叉并成为守护进程，即使配置文件指定要这样做。在 Windows 上，`dbus-daemon` 永远不会派叉，因此允许此选项但没有任何作用。

- `-print-address=[DESCRIPTOR]`
  将消息总线的地址打印到标准输出或给定的文件描述符。这由启动消息总线的程序使用。

- `-print-pid=[DESCRIPTOR]`
  将消息总线的进程 ID（PID）打印到标准输出或给定的文件描述符。这由启动消息总线的程序使用。

- `-session`
  用于登录会话消息总线的的标准配置文件。

- `-system`
  用于系统级消息总线的标准配置文件。

- `-version`
  打印进程的版本。

- `-introspect`
  打印所有 D-Bus 内部接口的内省信息。

- `-address=[ADDRESS]`
  设置要监听的地址。此选项将覆盖配置文件中配置的地址。

# --systemd-activation

启用 systemd 风格的服务激活。仅在 Linux 上与 systemd 系统和会话管理器配合使用时有用。

- `--nopidfile`
  即使配置文件中配置了 PID 文件，也不写入 PID 文件。

# CONFIGURATION FILE

消息总线进程有一个配置文件，用于针对特定应用程序进行专门化。例如，一个配置文件可能会将消息总线设置为系统级消息总线，而另一个可能将其设置为用户会话级总线。配置文件还建立了资源限制、安全参数等。配置文件不属于任何互操作规范，且不保证其向后兼容性；本文档是文档，而非规范。

标准的系统级和会话级消息总线设置在 `/usr/share/dbus-1/system.conf` 和 `/usr/share/dbus-1/session.conf` 文件中配置。这些文件通常 `<include>` `/etc/dbus-1` 中的 `system-local.conf` 或 `session-local.conf`；你可以在这些文件中放置本地覆盖内容，以避免修改主配置文件。

配置文件是一个 XML 文档。它必须具有以下 doctype 声明：

```
<!DOCTYPE busconfig PUBLIC "-//freedesktop//DTD D-Bus Bus Configuration//EN" "http://www.freedesktop.org/standards/dbus/1.0/busconfig.dtd">
```

配置文件中包含以下元素：

```
<busconfig>
```
根元素。

```
<type>
```



# 消息总线的已知类型

目前已知值为“`system`”和“`session`”；如果设置了其他值，应将它们添加到 D-Bus 规范中或进行命名空间处理。最后一个 `<type>` 元素有效（之前的值被忽略）。此元素控制在激活的客户端中设置哪些消息总线环境变量。区分会话总线和系统总线的多数策略由配置中的其他元素控制。

如果消息总线的已知类型为“`session`”，则 `DBUS_SESSION_ADDRESS` 环境变量被设置为提供的地址。如果类型为“`system`”，则 `DBUS_SYSTEM_ADDRESS` 环境变量被设置为提供的地址。

## `<include>`

配置文件可以包含其他文件。路径可以是相对于配置文件目录的，也可以是绝对路径。

## `<policy>`

策略定义了谁可以在消息总线上发送什么消息。策略可以根据用户、组或其他标准定义。

## `<interface>`

接口定义了总线上可用的 D-Bus 接口。

## `<method>`

方法定义了在接口上可以调用的函数。

## `<signal>`

信号定义了接口可以发射的事件。

## `<error>`

错误定义了方法可以返回的错误。

## `<property>`

属性定义了与接口关联的值。

## `<service>`

服务定义了总线上可用的名称。

## `</busconfig>`

## `<servicedir>`

添加一个用于扫描 `.service` 文件的目录。目录按照配置文件中出现的顺序进行扫描（找到第一个提供特定服务的 `.service` 文件将将被使用）。

服务文件告诉总线如何自动启动程序。它们主要用于用户会话总线（per-user-session bus），而不是系统级总线（systemwide bus）。

### `<standard_session_servicedirs/>`

`<standard_session_servicedirs/>` 等同于为 `<XDG Base Directory Specification>` 中的每个数据目录指定子目录 "`dbus-1/services`"，因此，指定了一系列 `<servicedir/>` 元素。例如，“`usr/share/dbus-1/services`” 将是搜索的目录之一。

如果 `<XDG Base Directory Specification>` 尚未变动，可以在 [https://freedesktop.org/wiki/Standards/based-spec] 找到它，否则请尝试使用搜索引擎搜索。

`<standard_session_servicedirs/>` 选项仅适用于在 `/etc/dbus-1/session.conf` 中定义的用户会话总线守护进程。将其放在任何其他配置文件中可能是没有意义的。

### `<standard_system_servicedirs/>`

`<standard_system_servicedirs/>` 指定了应该搜索服务文件的标准系统级激活目录。该选项默认为 `/usr/share/dbus-1/system-services`。

`<standard_system_servicedirs/>` 选项仅适用于在 `/usr/share/dbus-1/system.conf` 中定义的系统级总线守护进程。将其放在任何其他配置文件中可能是没有意义的。

### `<servicehelper/>`

`<servicehelper/>` 指定了用于以替代用户启动系统守护进程的 setuid 辅助程序。通常，这应该是位于 libexecd 中的 `dbus-daemon-launch-helper` 可执行文件。

`<servicehelper/>` 选项仅适用于在 `/usr/share/dbus-1/system.conf` 中定义的系统级总线守护进程。将其放在任何其他配置文件中可能是没有意义的。

## `<limit>`

`<limit>` 建立了一个资源限制。例如：

```xml
<limit name="max_message_size">64</limit>
<limit name="max_completed_connections">512</limit>
```

`name` 属性是强制性的。可用的限制名称：

- "`max_incoming_bytes`" : 来自单个连接的消息的总字节数
- "`max_incoming_unix_fds`" : 来自单个连接的消息消息的 unix 文件描述符总数
- "`max_outgoing_bytes`" : 为单个连接队列的消息的总字节数
- "`max_outgoing_unix_fds`" : 为单个连接队列的 unix 文件描述符总数
- "`max_message_size`" : 单条消息的最大大小（字节）
- "`max_incoming_unix_fds`" : 单条消息的最大文件描述符数量
- "`service_start_timeout`" : 启动的服务建立连接之前的等待时间（毫秒/千分之一秒）
- "`auth_timeout`" : 毫秒（千分之一秒）
- "`pending_fd_timeout`" : 在断开连接之前，将文件描述符传递给 `dbus-daemon` 之前的等待时间（毫秒/千分之一秒）
- "`max_connections`" : 已认证连接的最大数量
- "`max_incomplete_connections`" : 未认证连接的最大数量
- "`max_connections_per_user`" : 来自同一用户的完成连接的最大数量
- "`max_pending_service_starts`" : 正在进行的并行服务启动的最大数量
- "`max_names_per_connection`" : 单个连接可以拥有的名称数量
- "`max_match_rules_per_connection`" : 每个连接针对单个方法回复的最大匹配规则数量（正在进行的调用次数）
- "`reply_timeout`" : 方法调用超时之前的等待时间（毫秒/千分之一秒）

最大入/出站队列大小允许在当前数量低于最大值时将新消息放入队列。因此，你实际上可以超过 `max_message_size` 超过最大值。

`max_completed_connections` 除以 `max_connections_per_user` 是可以协作通过系统级总线上的连接对所有其他用户进行拒绝服务攻击的用户数量。

限制通常只适用于系统级总线，而不适用于用户会话总线。

```xml
<policy>
```



# 策略

`<policy>` 元素定义了应用到一组总线连接的安全策略。策略由 `<allow>` 和 `<deny>` 元素组成。策略通常用于系统级总线，它们类似于防火墙，允许预期的流量并防止意外的流量。

目前，系统对于发送方法调用和拥有总线名称有一个默认策略。其他所有内容，特别是回复消息、接收检查和信号，都有默认策略。

通常情况下，最好将系统服务保持为小型、目标程序，它们在自己的进程中运行并提供单一总线名称。这样，只需要一个“own”权限的 `<allow>` 规则允许进程声明总线名称，以及一个“send_destination”规则允许来自某些或所有 uid 的流量流向你的服务。

`<policy>` 元素具有四个属性之一：
`context="default [mandatory]"` `at_console="(true|false)"` `user="username or userid"` `group="group name or gid"`

策略应用到连接的方式如下：

- 应用所有 `context="default"` 策略
- 以未定义的顺序应用所有 `group="连接用户所属组"` 的策略
- 以未定义的顺序应用所有 `user="连接认证用户"` 的策略
- 应用所有 `at_console="true"` 策略
- 应用所有 `at_console="false"` 策略
- 应用所有 `context="mandatory"` 策略

最大入/出站队列大小允许在当前数量低于最大值时将新消息放入队列。因此，你实际上可以超过 `max` 最大值。

可能的属性有：

- `send_interface="name"`
- `member="or_name"`
- `receive_interface="name"`
- `type="method_call"`
- `method_return`
- `signal`
- `error`
- `path="path/"`
- `requested_reply`
- `context="default"`
- `user="username"`
- `group="group"`

`<policy>` 元素具有四个属性之一：
`context="default [mandatory]"` `at_console="(true|false)"` `user="username or userid"` `group="group name or gid"`

`send_destination="fooblah"/>` 将拒绝带有给定接口和给定总线名称的消息。要实现或（OR）效果，请指定多个 `<deny>` 规则。

你不能在同一规则中同时包含 `send_` 和 `receive_` 属性，因为“消息是否可以发送”和“消息是否可以被接收”是分开评估的。

在使用 `send_interface`/`receive_interface` 时要小心，因为消息中的接口字段是可选的。特别地，**不要**指定 `<deny send_interface="org.foo.Bar"/>`！这将导致所有服务的无接口消息被拦截，这几乎不是你想要的结果。请始终使用如下格式的规则：`<deny send_interface="org.foo.Bar" send_destination="org.foo.Service"/>`

## SELinux

`<selinux>` 元素包含与安全增强型 Linux（Security Enhanced Linux）相关的设置。更多细节请见下文。

## Associate

`<associate>` 元素出现在 `<selinux>` 元素下方并创建一个映射。目前只支持一种类型的 associate：

```
<associate own="org.freedesktop.Foobar" context="foo_t"/>
```

这意味着如果一个连接请求拥有名称 `org.freedesktop.Foobar`，那么源上下文将是该连接的上下文，目标上下文将是 `foo_t` —— 请下文关于 SELinux 的简短讨论。

注意，这里的上下文是请求名称时的目标上下文，而不是拥有该名称的连接的上下文。

目前没有办法为拥有任何名称设置默认值，如果我们添加了这种语法，它看起来会是：

```
<associate own="*" context="foo_t"/>
```

如果你发现这有用的理由，请告知开发者。目前默认值将是总线本身的安全上下文。

如果两个 `<associate>` 元素指定相同的名称，将使用配置文件中后出现的那个元素。

## AppArmor

`<apparmor>` 元素用于配置总线上的 AppArmor 调停。它可以包含一个指定调停模式的属性：

```
<apparmor mode="enabled|disabled|required"/>
```



默认模式为 `"enabled"`。在 `"enabled"` 模式下，如果内核支持 AppArmor，则将执行 AppArmor 调停。如果不支持，`dbus-daemon` 将启动但不会发生 AppArmor 调停。在 `"disabled"` 模式下，禁用了 AppArmor 调停。在 `"required"` 模式下，如果支持 AppArmor，则启用 AppArmor 调停，否则 `dbus-daemon` 将拒绝启动。

总线的 AppArmor 调停模式在总线启动后无法更改。在配置文件中修改模式并向守护发送 `SIGHUP` 信号对调停模式无效。

# SELINUX

详阅 [http://www.nsa.gov/selinux/m/] 获取 SELinux。以下是一些有用的摘要：

系统中的每个主体（进程）和对象（例如文件、socket、IPC 对象等）都分配了一组安全属性，称为安全上下文（`security context`）。安全上下文包含了与特定主体或对象相关且属于安全策略的所有安全属性。

为了更好地封装安全上下文并提高效率，SELinux 的策略执行代码处理的是安全标识符 (`SID`) 而不是安全上下文。`SID` 是一个整数，由安全服务器在运行时映射到安全上下文。

当需要安全决策时，策略执行代码会将一对 `SID`（通常是主体的 `SID` 和对象的 `SID`，但有时是一对主体 `SID` 或一对对象 `SID`）以及一个对象安全类传递给安全服务器。对象安全类指示对象的类型，例如普通文件、目录或 TCP socket。

访问决策指定了是否授予给定的 `SID` 对和类的权限。每个对象类都定义了一组关联权限，用于控制对该类对象的操作。

D-Bus 在两个地方执行 SELinux 安全检查。

首先，每当消息从一个连接路由到另一个连接时，总线守护进程将将以第一个连接的安全上下文为源，第二个连接的安全上下文为目标，对象类 "`dbus`" 以及请求的权限 "`send_msg`" 来检查权限。

如果连接没有安全上下文（在 UNIX 域套接字运行时是不可能的），则使用的目标上下文是总线守护进程自身的上下文。目前没有更改此默认值的方法，因为我们假设仅使用域套接字连接到系统总线。如果情况发生变化，我们可能会添加设置默认连接上下文的方法。

其次，每当连接请求拥有一个名称时，总线守护进程将以连接的安全上下文为源，配置文件中为该名称指定的上下文为目标，对象类 "`dbus`" 以及请求的权限 "`acquire_svc`" 来检查权限。

总线名称的安全上下文通过本文前面描述的 `<associate>` 元素指定。如果名称在配置文件中没有关联的安全上下文，将使用总线守护进程自身的安全上下文。

# APPARMOR

当应用程序连接到总线时，会存储 AppArmor 限制上下文。限制上下文由标签（`label`）和一个限制模式组成。当需要安全决策时，守护进程使用限制上下文查询 AppArmor 策略，以确定应该允许还是拒绝该操作，以及是否应对操作进行审计。

守护进程在三个地方执行 AppArmor 安全检查。

首先，每当消息从一个连接路由到另一个连接时，总线守护进程将以第一个连接的标签为源，第二个连接的标签为目标，对象类 "`dbus`" 以及请求的权限 "`send_msg`" 来检查权限。

其次，每当连接请求拥有一个名称时，总线守护进程将以连接的标签为源，配置文件中为该名称指定的标签为目标，对象类 "`dbus`" 以及请求的权限 "`acquire_svc`" 来检查权限。

第三，每当连接尝试监听时，总线守护进程将以连接的标签为源检查权限。

用于总线调停的 AppArmor 规则不存储在总线配置文件中。它们存储在应用程序的配置文件（`profile`）中。

# 调试

如果你正试图找出消息去了哪里，或者为什么你没有收到消息，有几种方法可以尝试。

记住，系统总线被严格限制，如果你没有安装安全策略来允许你的消息通过，它将无法工作。对于会话（`session`），不必担心。

弄明总线上发生了什么最简单的方法是运行 D-Bus 包自带的 `dbus-monitor` 程序。你也可以使用 `dbus-send` 发送消息。这些程序有自己的文档。

如果你想知道进程本身在做什么，可以考虑运行一个独立的守护进程副本进行测试。这将允许你使用调试器或带有详细输出运行它，而不会影响你真实的会话和系统守护进程。

要运行独立的守护进程副本，例如打开打开终端并：

```
DBUS_VERBOSE=1 dbus-daemon --session --print-address
```



守护进程启动时会打印测试地址。你需要复制粘贴此地址，并在启动想要测试的应用程序时将其作为 `DBUS_SESSION_BUS_ADDRESS` 环境变量的值。这将导致这些应用程序连接到你的测试总线，而不是真实会话总线的 `DBUS_SESSION_BUS_ADDRESS`。

除非你的 D-Bus 副本在编译时启用了详细模式，否则 `DBUS_VERBOSE=1` 将毫无效果。如果你的副本没有考虑到调试，你可能需要重新编译 D-Bus。`DBUS_VERBOSE` 也会影响 D-Bus 库，从而影响使用 D-Bus 的应用程序；在客户端和守护进程端都使用详细输出可能有用。

如果你想玩得高级一点，可以为测试总线创建一个自定义的总线配置（例如定义两个默认配置的 `session.conf` 和 `system.conf` 文件）。这将允许你指定不同的 `.service` 文件目录，例如。

### 作者

请访问 http://www.freedesktop.org/software/dbus/doc/AUTHORS

## 缺陷

请将缺陷报告发送至 D-Bus 邮件列表或缺陷跟踪器，访问 http://www.freedesktop.org/software/dbus/

`dbus-launch` - 从 shell 脚本启动消息总线的工具

### 摘要

`dbus-launch [--version] [--help] [--sh-syntax] [--csh-syntax] [--auto-syntax] [--binary-syntax] [--close-stderr] [--exit-with-session] [--autolaunch=MACHINEID] [----config-file=FILENAME] [PROGRAM] [ARGS...]`

### 描述

`dbus-launch` 命令用于从 shell 脚本启动 `dbus-daemon` 的会话总线实例。它通常在用户的登录脚本中调用。与守护进程本身不同，`dbus-launch` 会退出可以使用反引号或 `$()` 结构从 `dbus-launch` 中读取信息。

在不带参数的情况下，`dbus-launch` 将启动一个会话总线实例，并将实例的地址和 PID 打印到标准输出。

你可以指定要运行的程序；在这种情况下，`dbus-launch` 将启动一个会话总线实例，设置适当的环境变量以便指定的程序找到总线，并带有指定的参数执行程序。示例见下文。

如果你启动了一个程序，`dbus-launch` 将不会向标准输出打印有关新总线的信息。

当 `dbus-launch` 将总线信息打印到标准输出时，默认是简单的键值对格式。然而，你可以使用 `--sh-syntax`、`--csh-syntax`、`--binary-syntax` 或 `--auto-syntax` 选项请求替代语法。其中几个选项会导致 `dbus-launch` 输出用于设置的 shell 代码。

使用 `--auto-syntax` 选项时，`dbus-launch` 会查看 `SHELL` 环境变量的值来决定应该使用哪种 shell 语法。如果 `SHELL` 以“csh”结尾，则输出兼容 csh 的代码；否则输出 Bourne 代码。

与其传递 `--auto-syntax`，你可以通过使用 `--sh-syntax` 指定 Bourne 语法或使用 `--csh-syntax` 指定 csh 语法来显式指定特定语法。在脚本中，避免 `--auto-syntax` 更加健壮，且你可能知道脚本是用哪种 shell 编写的。

有关 D-Bus 的更多信息，请访问 http://www.freedesktop.org/software/dbus/。另见 `dbus-daemon` 的 man 页。

## 示例

在标准 X 会话部分运行 `dbus-launch` 的发行版应该在 X 服务器启动并可用后运行 `dbus-launch --exit-with-session`，作为作为“主”X 客户端（通常是会话管理器或窗口管理器）的封装，如下例所示：

```
dbus-launch --exit-with-session gnome-session
```

```
dbus-launch --exit-with-session openbox
```

```
dbus-launch --exit-with-session ~/.xsession
```

如果你的发行版没有这样做，你可以通过在 X 会话脚本（如 `~/.xsession`, `~/.xinitrc` 或 `~/.Xclients`）中以相同方式运行会话或窗口管理器来实现类似的效果。

要在文本模式会话中启动 D-Bus 会话，请使用 `dbus-launch`。请参阅 `dbus-run-session(1)`。

```bash
## 测试是否存在现有总线守护进程，为了安全起见，如果 test -z
"DBUS_SESSION_BUS_ADDRESS" ; then ## 如果未找到，启动一个新的
eval `dbus-launch --sh-syntax` echo "D-Bus per-session daemon address
is: $DBUS_SESSION_BUS_ADDRESS" fi
```

注意，在这种情况下，`dbus-launch` 将退出，且 `dbus-daemon` 不会在注销时自动终止。

# 自动启动

对于尝试使用 D-Bus 的进程，默认情况下没有设置 `DBUS_SESSION_BUS_ADDRESS`，该进程将尝试带上 `--autolaunch` 选项调用 `dbus-launch`，以启动新的会话总线，或在 X 显示器或 `~/.dbus/session-bus/` 中的文件中查找现有的总线地址。

每当发生自动启动时，必须启动新总线的应用程序将处于自己的世界中；如果它尝试使用许多总线服务，它可以有效地结束启动新会话。这取决于应用程序及其尝试的操作，可能是次优的或完全损坏的。

自动启动有两个常见原因。一个是 `ssh` 到远程机器。该问题的理想的修复方法是像转发 `DISPLAY` 一样转发 `DBUS_SESSION_BUS_ADDRESS`。期间，如果你喜欢，可以编辑 `session.conf` 配置文件来设置 `DBUS_SESSION_BUS_ADDRESS`。

自动启动的另一个原因是 `su` 到另一个用户，并将以第二个用户身份运行的 X 应用程序在属于第一个用户的显示器。在这种情况下，理想的修复方法可能是允许第二个用户连接到第一个用户的会话总线，就像他们连接到第一个用户的显示器一样。然而，尚未编写实现该功能的机制。

你可以通过手动设置 `DBUS_SESSION_BUS_ADDRESS` 来避免自动启动。`--autolaunch` 选项被认为是内部使用的，如果没有指定，它将启动会话。

### 选项

支持以下选项：

- `--auto-syntax`: 根据 `SHELL` 环境变量选择 shell 语法。
- `--binary-syntax`: 输出二进制消息流。
- `--config-file=FILENAME`: 传递配置文件。
- `--close-stderr`: 关闭标准错误。
- `--csh-syntax`: 输出兼容 csh 的代码。
- `--exit-with-session`: 会话终止时退出。
- `--autolaunch=MACHINEID`: 启动新的会话总线或查找现有的总线。
- `--help`: 打印帮助信息。
- `--sh-syntax`: 输出兼容 Bourne 的代码。
- `--version`: 打印版本。

# 注意事项

如果给出 `--autolaunch`，则隐含 `--monitor` 模式。

`dbus-monitor` 有两种不同的文本输出模式：“经典”风格的监控模式和分析模式。分析格式是一种紧凑的格式，具有单行消息和微秒级的时间信息。`--profile` 和 `--monitor` 选项分别选择分析和监控输出格式。

`dbus-monitor` 还有两种二进制输出模式。通过 `--binary` 选择的二进制模式输出整个二进制消息流（不包括初始身份握手）。通过 `pcap` 选择的 PCAP 模式在输出开头添加 PCAP 文件头，并在每个消息之前添加 PCAP 消息头；这将产生 Wireshark 读取的二进制文件。

如果没有指定模式，`dbus-monitor` 使用监控输出格式。为了让 `dbus-monitor` 看到你感兴趣的消息，你应该指定一组通配表达式，就像你预期传递给 `dbus_bus_add_match` 函数的那样。

消息总线配置可能会阻止 `dbus-monitor` 看到所有消息，特别是当你以非 root 用户运行监控时。

### 选项

- `-system`
监控系统总线。

- `-session`
监控会话总线。（默认选项。）

- `-address ADDRESS`
监控位于 `ADDRESS` 指定的任意消息总线。

- `-profile`
使用分析输出格式。

- `-monitor`
使用监控输出格式。（默认选项。）

## 示例

这里是一个使用 `dbus-monitor` 监听 gnome 输入器输出的示例：



dbus-monitor `"type='signal', sender='org.gnome.TypingMonitor', interface='org.gnome.TypingMonitor'"`

### 作者

`dbus-monitor` 由 Philip Blundell 编写。分析输出模式由 Olli Salli 添加。

## 缺陷

请将错误报告发送到 D-Bus 邮件列表或错误跟踪器，参见 http://www.freedesktop.org/software/dbus/m/

# DBUS-RUN-SESSION

`dbus-run-session` - 在新的 D-Bus 会话中启动进程

### 概要

```
dbus-run-session [--config-file FILENAME] [--dbus-daemon BINARY] [--] PROGRAM [ARGUMENTS...]
dbus-run-session --help
dbus-run-session --version
```

### 描述

`dbus-run-session`

用于从 shell 脚本启动 `dbus-daemon` 会话实例，并在该会话中启动指定的程序。`dbus-daemon` 的运行时间与程序相同，程序结束后将终止。

一种用法是在文本模式或 SSH 会话中运行带有自带 `dbus-daemon` 的 shell，并在离开子 shell 时自动终止 `dbus-daemon`，如下：

```
dbus-run-session -- bash
```

或者通过将 `dbus-run-session` 与 `exec` 内置命令结合，来完全替换登录 shell：

```
exec dbus-run-session -- bash
```

另一种用法是在隔离的 D-Bus 会话中运行总线回归测试和类似操作，以避免干扰“真实的” D-Bus 会话，或依赖于已经存在活跃的 D-Bus 会话，例如：

```
dbus-run-session -- make check
```

或在 `automake(1)` 中：

```
AM_TESTS_ENVIRONMENT = export MY_DEBUG=all; LOG_COMPILER = dbus-run-session AM_LOG_FLAGS ==
```

### 选项

- `--config-file=FILENAME`, `--config-file FILENAME`
将 `--config-file=FILENAME` 传递给总线守护进程，而不是作为 `--session` 参数。参见 `dbus-daemon(1)`。

- `--dbus-daemon=BINARY`, `--dbus-daemon BINARY`
将 `BINARY` 作为 `dbus-daemon(1)` 运行，而不是按照通常在 `PATH` 中搜索名为 `dbus-daemon` 的可执行文件。

- `--help`
打印用法信息并退出。

- `--version`
打印 `dbus-run-session` 的版本并退出。

# 退出状态

`dbus-run-session` 以 `PROGRAM` 的退出状态退出；如果使用了 `--help` 或 `--version` 选项，则返回 `0`；如果 `dbus-run-session` 内部发生错误，返回 `127`；如果 `PROGRAM` 被信号 `n` 杀死，则返回 `128+n`。

## 环境变量

在 `PATH` 中查找 `PROGRAM`，并（如果没有使用 `--dbus-daemon` 选项或其参数不包含 `/` 字符）查找 `dbus-daemon`。

会话总线的地址通过环境变量 `DBUS_SESSION_BUS_ADDRESS` 给 `PROGRAM`。

如果环境变量中存在 `DBUS_SESSION_BUS_PID`、`DBUS_SESSION_BUS_WINDOWOWID`、`DBUS_STARTER_BUS_TYPE` 和 `DBUS_STARTER_ADDRESS`，则将其移除。

## 缺陷

请将错误报告发送到 D-Bus 邮件列表或错误跟踪器，参见 http://www.freedesktop.org/software/dbus/m/

# 另见

`dbus-daemon(1)`, `dbus-launch(1)`

## 名称

`dbus-send` - 向总线发送消息

### 概要

```
dbus-send [--system | --session | --address=ADDRESS] [--dest=NAME] [--print-reply [=literal]] [--reply-timeout=MSEC] [--type=TYPE] OBJECT_PATH INTERFACE.MEMBER [CONTENTS...]
```

### 描述

`dbus-send` 命令用于向 D-Bus 总线发送消息。关于整体架构的更多信息请参见 http://www.freedesktop.org/software/dbus/m/。

有两种已的消息总线：系统总线（在许多系统中作为 "messagebus" 服务安装）和用户登录会话总线（在用户登录时启动）。`--system` 和 `--session` 选项允许 `dbus-send` 分别向系统或会话总线发送消息。如果两者都未指定，则分别向系统或会话总线发送消息。

## 名称

`dc` - 一个任意精度计算器

### 摘要

```
dc [-V] [-h] [-e expression] [-f script-file] [file ...]
```



### 描述
`dc` 是一个支持无限精度的逆波兰计算器。它还允许你定义和调用宏。通常情况下 `dc` 从标准输入读取；如果提供了任何参数，它们将被视为文件名，`dc` 会读取并执行文件内容。所有正常输出均指向标准输出；所有错误输出均指向标准错误。输入数字会将将其推入栈。算术运算会弹出栈顶元素并压入结果。要输入负数，以 `-` 开头。不支持指数计数法。如需连续输入两个数字，请用空格分隔开。

### 作者
原始的 `dc` 由 Andrew Tridell 创建，现在的 Samba 由 Bjorn Baumbach 开发。

# 版本
本帮助页适用于第 3 版本。

### 选项
可以使用以下命令行选项调用 `dc`：

- `-V`, `--version`
  打印正在运行的 `dc` 版本和版权声明，然后退出。

- `-h`, `--help`
  打印总结这些命令行选项和错误报告地址的用法信息，然后退出。

- `-e expression`, `--expression=expression`
  将 `expression` 中的命令添加到处理输入时要运行的命令集中。

- `-f script-file`, `--file=script-file`
  将文件 `script-file` 中包含的命令添加到处理输入时要运行的命令集中。

如果在处理完上述内容后仍有任何命令行参数，这些参数将被解释为要处理的文件名。文件名 `-` 指标准输入。如果未指定脚本文件或表达式，则将处理标准输入。

# 打印命令
`p`
打印栈顶的值，而不改变栈。在值之后打印一个换行符。

`n`
打印栈顶的值并将其弹出，且在之后不打印换行符。

`P`
弹出栈顶的值。如果它是一个字符串，则直接打印而不带尾随换行符。否则，它是一个数字，将其绝对值的整数部分作为“基数 `UCHAR_MAX+1`”字节流输出。假设 `UCHAR_MAX+1` 为 256（在大多数具有 8 位字节的机器上如此），序列 `KSK0k1/_1s [ls]*Ssd0>x [256<x]dsxxx[qSq[Lsd0>qaPlxx] dsxxx0sqLsqLk+k` 也可以实现此功能。（上述原生 `dc` 代码的大部分复杂性源于反向计算字符，以及为了确保所有寄存器都恢复到原始状态的愿。）

`f`
打印栈的所有内容而不改变任何内容。如果你迷了方向或想弄某些命令的效果，这是一个很好的命令。

## 缺陷
请向项目发送错误报告。

### 参见
`smbd(8)`, `samba(7)`

# 算术运算

`+` 从栈中弹出两个值，将它们相加，并将结果压栈。结果的精度仅取决于参数的值，且足以保证精确。

`-` 从栈中弹出两个值，用第二个弹出的值减去第一个弹出的值，并将结果压栈。

`*` 从栈中弹出两个值，将它们相乘，并将结果压栈。小数位数取决于当前的精度值以及两个参数的小数位数。

`/` 从栈中弹出两个值，用第一个弹出的值除以第二个弹出的值，并将结果压栈。小数位数由精度值指定。

`%` 从栈中弹出两个值，计算 `/` 命令执行的除法余数，并将其压栈。计算的值与序列 `Sd dld/Ld*-.` 计算的结果相同。

`~` 从栈中弹出两个值，用第一个弹出的值除以第二个弹出的值。先入栈商，再入栈余。除法使用的数位数由精度值指定。（序列 `SdSn ld/LnLd` 也可以实现此功能，但错误检查略有不同。）

`^` 从栈中弹出两个值进行幂运算，以第一个弹出的值为指数，第二个弹出的值为底数。指数的小数部分被忽略。精度值指定结果的小数位数。

`|` 从栈中弹出三个值并计算模幂。第一个弹出的值作为模数；该值必须是非零数且应该是整数。第二个弹出的值作为指数；该值必须是非负数，且该指数的任何小数部分都会使用。第三个弹出的值作为指数的底数，应为整数。对于小整数，这类似于序列 `Sm^Lm%`，但与 `^` 不同，此命令可以处理任意大的指数。

`$` 从栈中弹出一个值，计算其平方根并将其压栈。精度值指定结果的小数位数。

大多数算术运算受“精度值”的影响，可以通过 `k` 命令设置。默认精度值为零，这意味着除了加法和减法外，所有算术运算都会产生整数结果。

# 栈控制

`c` 清空栈，使其为空。

`d` 复制栈顶的值，将其另一个副本压栈。因此，“`4d*p`”会计算 4 的平方并打印它。

`r` 反转栈顶前两个值的顺序（交换）。这也可以通过序列 `SaSbLaLbLb` 实现。

# 寄存器

`dc` 提供了至少 256 个内存寄存器，每个由单个字符命名。你可以在寄存器中存储数字或字符串，并在稍后检索。

`s r` 从栈顶弹出值并将其存储到寄存器 `r` 中。

`l r` 复制寄存器 `r` 中的值并压栈。这不会改变 `r` 的内容。

每个寄存器也包含自己的栈。当前寄存器值是该寄存器栈的栈顶。

`S r` 从主栈顶弹出值并压入寄存器 `r` 的栈中。寄存器的旧值将无法访问。

`L r` 从寄存器 `r` 栈顶弹出值并压入主栈。寄存器 `r` 栈中的旧值（如果有）现在可以通过 `l r` 命令访问。

### 参数
`dc` 有三个控制其操作的参数：精度、输入进制和输出进制。精度指定了大多数算术运算结果中保留的小数位数。输入进制控制对输入数字的解释；所有输入的数字都使用该进制。输出进制用于打印数字。

输入进制和输出进制是独立的参数；你可以让它们不等，这可能有用也可能引起困惑。输入进制必须在 2 到 16 之间（包含）。输出进制至少为 2。精度必须大于等于0。无论当前的输入或输出进制如何，精度始终以十进制位数衡量。

`i` 从栈顶弹出值并将其设置为输入进制。
`o` 从栈顶弹出值并将其设置为输出进制。
`k` 从栈顶弹出值并将其设置为精度。
`I` 将当前输入进制压栈。
`O` 将当前输出进制压栈。
`P` 将当前精度压栈。

# 字符串

`dc` 处理字符串的能力有限，与处理数字的能力不相同；你对字符串能做的唯一事情就是打印它们以及将其作为宏（宏）执行它们（这意味着字符串的内容被当作 `dc` 命令处理）。所有寄存器和栈都可以存储字符串，且 `dc` 始终知道任何给定对象是字符串还是数字。某些命令（如算术运算）要求数字作为参数，如果给定字符串则打印错误。其他命令可以接受数字或字符串；例如，`p` 命令可以接受两者，并根据其类型打印对象。

`[characters]`
创建一个包含指定字符的字符串（包含在平衡的 `[` 和 `]` 之间），并将其压栈。例如，`[foo]P` 会打印字符 `foo`（无换行）。

`a` 弹出栈顶。如果它是数字，则将该数字的低位转换为字符串并压栈。否则，栈顶是字符串，则将其第一个字符压回。

`x` 从栈中弹出一个值并作为宏执行。通常它应该是字符串；如果它是数字，则简单地将其压栈。例如，`[1p]x` 执行宏 `1p`，将 1 压栈并打印 1 在单独的一行。

宏通常存储在寄存器中；`[1p]sa` 将 1 存储寄存器 `a`，`lax` 调用此宏。

`>r` 从栈中弹出两个值并假设它们是数字，如果栈顶值大于第二个值，则执行寄存器 `r` 的内容。因此 `2>a` 会调用寄存器 `a`，而 `1>a` 不会。

`!r` 如果栈顶值不大于（小于等于）第二个值，则执行宏。

`<r` 如果栈顶值小于第二个值，则执行宏。

`=r` 如果两个弹出的值相等，则执行宏。

`!=r` 如果两个弹出的值不相等，则执行宏。

`?` 从终端读取一行并执行。此命令允许宏请求用户输入。

`q` 退出宏并退出调用它的宏。如果从顶层调用，或从直接从顶层调用的宏调用，`q` 命令将导致 `dc` 退出。`3Q` 会退出三层。`Q` 命令不会导致 `dc` 退出。

# 状态查询

`Z` 从栈弹出值，计算其位数（如果是字符串则计算字符数）并压入该数字。数字的计数不包括任何导零，即使它们出现在小数点右侧。

`X` 从栈弹出值，计算其小数位数并压入该数字。对于字符串，压入的值为0。

`z` 压入栈深度：执行 `z` 命令前栈上的对象数量。

# 其他

`!` 将行的剩余部分作为系统命令运行。注意 `<`、=` 和 `>` 命令的解析具有优先级，因此如果你想运行以 `<` `=` `>` 开头的命令，需要在 `!` 后面添加一个空格。

# 将行的剩余部分解释为注释。

`:r` 从栈中弹出两个值。旧的第二个值将存储在数组 `r` 中，索引为旧的栈顶值。

`;r` 弹出栈顶值并作为数组 `r` 的索引。然后将选中的值压栈。

注意，寄存器的每个堆栈实例都关联着它自己的数组。因此 `1 0:a 0Sa 2 0:a La 0;ap` 会打印 1，因为 2 存储在随后弹出的 `0:a` 实例中。

# 故障
请将故障报告邮件发送至 `bug-dc@gnu.org`。

## 名称
`dconf-service` - 用于向 dconf 数据库写入数据的 D-Bus 服务

### 概要
`dconf-service`

### 描述
**`dconf-service`** 程序在会话或系统总线上提供一个 *ca.desrt.dconf* 名称。用户或管理员永远不需要手动启动该服务，因为当应用程序尝试写入设置时，**`dbus-daemon(1)`** 都会自动启动它。

从 dconf 数据库读取值不涉及该服务；它仅在写入时需要。该服务是无状态的，可以随时自由地退出（因此对崩溃具有鲁棒性）。

### 参见
`dconf(7)`, `dbus-daemon(1)`, `systemd(1)`

## 名称
`dconf` - 用于操纵 dconf 数据库的简单工具

### 概要
```



### dconf

`dconf` `read` `KEY`

`dconf` `list` `DIR`

`dconf` `write` `KEY` `VALUE`

`dconf` `reset` `[-f]` `PATH`

`dconf` `compile` `OUTPUT` `KEYDIR`

`dconf` `update`

`dconf` `watch` `PATH`

`dconf` `dump` `DIR`

`dconf` `load` `DIR`

`dconf` `help` `[COMMAND]`

#### 描述
`dconf` 程序可以对 `dconf` 数据库执行各种操作，例如读取或写入单个值或整个目录。此工具直接作用于 `dconf`，不使用 `gsettings` schema 信息。因此，它无法对值进行类型和一致性检查。如果需要此类检查，可以使用 `gsettings(1)` 工具作为替代方案。

`DIR` 参数必须是目录路径（以 `'/'` 开头并结尾），`KEY` 参数必须是键路径（以 `'/'` 开头，但不以 `'//'` 结尾），`PATH` 参数可以是目录路径也可以是键路径。

`OUTPUT` 参数必须是写入（二进制）`dconf` 数据库的位置，而 `KEYFILEDIR` 参数必须是一个包含键文件的 `.d` 目录。

`VALUE` 参数必须是 `GVariant` 格式，例如，一个字符串必须包含显式引号：`"foo"`。此格式也用于在输出值时。

请注意，`dconf` 需要一个 D-Bus 会话总线连接才能将更改写入 `dconf` 数据库。

#### 命令
`read`
读取键的值。

`list`
列出目录的子键和子目录。

`write`
向键写入新值。

`reset`
重置键或整个目录。对于目录，必须指定 `-f`。

`compile`
从键文件编译二进制数据库。结果始终是小端字节序，因此可以安全地安装在 `share` 中。如果在大端机器上使用，`dconf` 将在读取时自动交换内容。

`update`
更新系统的 `dconf` 数据库。

`watch`
监控键或目录的变化。

`dump`
将整个子路径转储到标准输出。输出采用类似于键文件的格式，值使用 `GVariant` 语法。

`load`
从标准输入填充子路径。预期的格式与 `dump` 产生的格式相同。

`help`
显示帮助并退出。如果给出 `COMMAND`，则显示该命令的帮助。

#### 环境变量
`DCONF_PROFILE`
此环境变量决定使用哪种 `dconf` 配置文件。参见 `dconf(7)`。

#### 参见
`dconf(7)`, `gsettings(1)`, `dconf-editor(1)`

### dd - 转换并复制文件

#### 概要
```
dd [OPERAND]...
dd OPTION
```

#### 描述
复制文件并根据操作数进行转换和格式化。

```
bs=BYTES
```
一次读写最多 `BYTES` 字节

```
cbs=BYTES
```
一次转换 `BYTES` 字节

```
conv=CONVS
```
根据逗号分隔的符号列表转换文件

```
count=N
```
仅复制 `N` 个输入块

```
ibs=BYTES
```
一次读取最多 `BYTES` 字节（默认值: 512）

```
if=FILE
```
从 `FILE` 而不是标准输入读取

```
iflag=FLAGS
```
根据逗号分隔的符号列表读取

```
obs=BYTES
```
一次写入 `BYTES` 字节（默认值: 512）

```
of=FILE
```
写入 `FILE` 而不是标准输出

```
oflag=FLAGS
```
根据逗号分隔的符号列表写入

```
seek=N
```
在输出开始处跳过 `N` 个 `obs` 大小的的块

```
skip=N
```
在输入开始处跳过 `N` 个 `ibs` 大小的的块

```
status=LEVEL
```
打印到 stderr 的信息级别；`'none'` 抑制错误消息以外的所有内容，`'noxfer'` 抑制最后的传输统计，`'progress'` 显示定期的传输统计。

`N` 和 `BYTES` 后可以跟以下乘法后缀：`c =1`, `w =2`, `b =512`, `kB =1000`, `K =1024`, `MB =1000*1000`, `M =1024*1024`, `xM =M` `GB =1000*1000`, `G =1024*1024`，以此类推 `T`, `E`, `Y`。

每个 `CONV` 符号可以是：

```
ascii
```
从 EBCDIC 转换为 ASCII

```
ebcdic
```
从 ASCII 转换为 EBCDIC

```
ibm
```
从 ASCII 转换为备用 EBCDIC

```
block
```
用空格填充 `cbs-size` 的换行符终止记录

```
unblock
```
将 `cbs-size` 末尾的空格替换为换行符

```
ucase
```
将大写改为小写

```
sparse
```
将小写改为大写

```
swab
```
对于 `NUL` 输入块，尝试寻址而不是写入输出

```
sync
```
每同步一对 `ibs-size` 大小的输入字节；当与 `block` 或 `unblock` 使用时，用空格填充而非 `NUL`

```
nocreat
```
如果输出文件已存在则失败

```
notrunc
```
不创建输出文件

```
noerror
```
在读取错误后继续

```
async
```
在物理写入输出数据之前

```
fsync
```
同样写入元数据

```
append
```
模式追加

```
direct
```
写入元数据

直接作用于 I/O

```
fullblock
```
完整块

```
dsync
```
同样写入元数据

```
nonblock
```
非阻塞使用

```
noatime
```
不更新访问时间

```
nocache
```
丢弃缓存

```
notty
```
不分配终端

```
nofollow
```
不跟踪符号链接

```
count_bytes
```
计数

详细文档见：`http://www.gnu.org/software/`

### deallocvt - 释放空闲虚拟终端

#### 概要
`deallocvt [N]`

#### 描述
该命令释放所有空闲虚拟终端的内存和数据结构。如果给出一个多个参数 `N`，则释放对应的 `/dev/ttyN`。

如果一个虚拟终端不是前台终端，没有进程对其打开读取或写入，且屏幕上没有文本，则它就是空闲的。

#### 参见
`chvt(1)`, `openvt(1)`

### delv - DNS 查询与验证工具

#### 概要
```
delv [@server] [-4] [-6] [-a anchor-file] [-b address] [-c class] [-d level] [-i] [-m] -p port|[-q name] [-t type] [-x addr] [name] [type] [class] [queryopt...]
delv [-h]
delv [-v]
delv [queryopt...] [query...]
```

#### 描述
`delv`（实体查询与验证）是一个发送 DNS 查询并验证结果的工具，使用了与 `named` 相同的内部解析器和验证器。

`delv` 将向指定的服务器发送获取和验证所需的所有查询；这包括原始请求查询、跟随 `CNAME` 或 `DNAME` 链的后续查询，以及用于建立信任链的 `DNSKEY`、`DS` 和 `DLV` 记录。它不执行迭代解析，而是模拟了配置了 DNSSEC 验证和转发的服务器的行为。

默认情况下，使用内置的 DNSSEC 信任锚对根区域 `(.)` 以及 ISC DNSSEC 旁路验证区域 (`"dlv.isc.org"`) 进行验证。`delv` 返回的记录要么经过完全验证，要么未签名。如果验证失败，输出中包含失败的解释；可以详细跟踪验证过程。由于 `delv` 不依赖外部服务器执行验证，因此它可以在本地 DNS 服务器可能不可信的环境中检查 DNS 响应的有效性。

除非指定特定的服务器，`delv` 将尝试 `/etc/resolv.conf` 中列出的所有服务器。如果没有找到可用的服务器地址，`delv` 将向本地地址发送查询（IPv4 为 `127.0.0.1`，IPv6 为 `::1`）。

当没有给出命令行参数或选项时，`delv` 将对 `"."`（根区域）执行 `NS` 查询。

#### 简单用法
`delv` 的典型调用方式如下：
```
delv @server name type
```
其中：

`server`
是要查询的名称服务器的名称或 IP 地址。它可以是点分十进制表示的 IPv4 地址，也可以是冒号分隔表示的 IPv6 地址。当提供的 `server` 参数为主主机名时，`delv` 在查询该名称服务器之前会解析名称（但注意，此初始查找不会通过 DNSSEC 验证）。

如果未提供 `server` 参数，`delv` 将查询 `/etc/resol.conf`；如果在该文件中找到地址，则只使用该地址的服务器。如果使用了 `-4` 或 `-6` 选项中的任一，则仅尝试对应传输协议的地址。如果未找到可用的地址，`delv` 将向本地地址发送查询（IPv4 为 `127.0.0.1`，IPv6 为 `::1`）。

`name`
是要查找的域名。

`type`
表示所需的查询类型 – `ANY`、`A`、`MX` 等。`type` 可以是是任何有效的查询类型。如果未提供 `type` 参数，`delv` 将对 `A` 记录进行查找。

#### 选项
`-anchor-file`
指定从文件中读取 DNSSEC 信任锚点。默认是 `/etc/bind.keys`，该文件随 `BIND 9` 一起，包含根区域（`"."`）和 DNSSEC 旁路验证区域（`dlv.isc.org"`）的信任锚点。

与查询或 `DLV` 信任锚点名称匹配匹配密钥将被忽略；这些密钥名称可以使用 `+dlvNAME` 和 `+root=NAME` 选项进行覆盖。



注意：在读取信任锚点文件时，`delv` 对 `managed-keys` 语句和 `trusted-keys` 语句的处理方式相同。也就是说，对于托管密钥，受信任的是初始密钥；不支持 RFC 5011 管理。`delv` 不会咨询 `named` 维护的 `managed-keys` 数据库。这意味着如果 `/etc/bind.keys` 中的两个密钥中的任一被撤销并滚动，则需要更新 `/etc/bind.keys` 以在 `delv` 中使用 DNSSEC 验证。

`-b address`

将查询的源 IP 地址设置为 `address`。这必须是主机任一网络接口上的有效地址，或者是 `"0.0.0.0"` 或 `""`。可以通过附加 `"#<port>"` 来指定可选的源端口。

`-c class`

为请求的数据设置查询类（`class`）。目前 `delv` 仅支持 `"IN"` 类，任何其他值都会被忽略。

`-d level`

将系统调试级别设置为 `level`。允许范围从 0 到 99。默认值为 0（不调试）。随着调试级别的增加，`delv` 的调试跟踪信息会变得更加详细。使用下方的 `+mtrace`、`+rtrace` 和 `+vtrace` 选项可以获取额外的调试细节。

`-h`

显示 `delv` 的帮助用法输出并退出。

`-i`

不安全模式。这将禁用内部 DNSSEC 验证。（但注意，这并不会在上游查询中设置 CD 位。如果正在查询的服务器正在执行 DNSSEC 验证，则它将不会返回无效数据；这可能导致 `delv` 超。当需要检查无效数据以调试 DNSSEC 问题时，请使用 `dig +cd`。）

`-m`

启用内存使用调试。

`-p port`

指定一个用于查询的目的端口，而不是标准的 DNS 端口号 53。此选项用于已配置为非标准端口查询的名称服务器。

`-q name`

将查询名称设置为 *name*。虽然可以在不使用 `-q` 的情况下指定查询名称，但有时需要将名称与类型或类区分开来（例如，当查找名称 `"ns"` 或 `"ch"` 时，它们可能被误解为类 CH）。

`-t type`

将查询类型设置为 *type*，它可以是 BIND 支持的任何有效查询类型，但区域传输类型 AXFR 和 IXFR 除外。与 `-q` 类似，这在查询名称、类型或类存在歧义时非常有用。有时需要将查询名称、类型或类区分开来。

默认查询为 `"A"`，除非提供了 `-x` 选项来指示反向查找，在这种情况下查询为 `delv` `"PTR"`。

`-v`

打印 `delv` 版本并退出。

`-x addr`

执行反向查找，将地址映射到名称。*addr* 是点分十进制表示的 IPv4 地址，或冒号分隔的 IPv6 地址。使用 `-x` 时，不需要提供 *name* 或 *type* 参数。`delv` 会自动对诸如 `11.12.13.10.in-addr.arpa` 的名称进行查找，并将查询类型设置为 PTR。IPv6 地址在 IP6.ARPA 域名下使用半字节格式（nibble format）进行查找。

`-4`

强制 `delv` 仅使用 IPv4。

`-6`

强制 `delv` 仅使用 IPv6。

# 查询选项

`delv` 提供了许多查询选项，影响查询结果的显示方式并在某些情况下影响查询查找的执行方式。

每个查询选项通过加号（`+`）前的关键字来识别。某些关键字设置或重置选项。这些关键字前面可以加上字符串 `no` 来否定该关键字的含义。其他关键字为选项（如超时间隔）分配值。它们的格式为 `+keyword=value`。查询选项如下：

`+nocd`

控制是否在 `delv` 发送的查询中设置 CD（禁用检查）位。这在排查 DNSSEC 问题时可能有用。设置 CD 标志将导致解析器返回无效响应，从而更容易看到常见的故障并在内部对其进行验证。

`+noclass`

控制在打印记录时是否显示类（CLASS）。默认是显示类。

`+nott`

控制在打印记录时是否显示 TTL。默认是显示 TTL。

`+nrtrace`

切换解析获取日志。这会报告 `delv` 在解析和验证过程中发送的每个查询的名称和类型。这等同于将 `"resolver"` 日志类的调试级别设置为 1。使用 `-d` 设置为 1 将产生相同的输出。

`+nmtrace`

切换消息日志。这会产生 `delv` 在解析和验证过程中接收到的响应的详细转储。这等同于将 `"resolver"` 日志类的 `"packets"` 模块的调试级别设置为 10。使用 `-d` 设置为 10 将产生相同的输出。

`+vtrace`（隐含）

切换日志。这显示了验证器在确定答案是否有效签名、未签名或无效时的内部过程。这等同于将 `"dnsec"` 日志类的 `"validator"` 模块的调试级别设置为 3。使用 `-d` 设置为 3 将产生相同的输出。

`+ncomments`

切换输出中注释行的显示。默认是打印注释。

`+norrcomments`

切换输出中每记录注释显示（例如，关于 DNSKEY 记录的可读密钥信息）。默认是打印每记录注释。

`+notrust`

切换 DNSSEC 记录中加密字段显示。这些字段的内容对于调试 DNSSEC 验证失败并非必要的，移除它们更容易看到常见的故障。默认显示这些字段。省略时，它们会被字符串 `"[omitted]"` 替换，或者在 DNSKEY 情况下，显示密钥 ID 作为替换，例如 `"[key id = value]"`。

`+split`

将资源记录中的长十六进制或 base64 格式字段拆分为 W 个字符的块（W 向上取整为 4 的倍数）。`+nosplit` 或 `+split=0` 字段完全不分割。默认是 56 个字符，在多行模式激活时为 44 个字符。

`+nall`

一组设置或清除显示选项 `+ncomments`、`+norrcomments` 和 `+notrust`。

## multiline

以带有可读注释的详细多行格式打印长记录（如 RRSIG、DNSKEY 和 SOA 记录）。默认将每个记录打印在单行上，以便机器对 `delv` 输出进行解析。

## dnssec

指示是否在 `delv` 输出中显示 RRSIG 记录。默认显示。请注意（与 `dig` 不同），这并不控制是否请求 DNSSEC 记录或是否对其进行验证。DNSSEC 记录总是会被请求的，除非使用 `-i` 或 `+noroot` 和 `+nodlv` 进行抑制，否则始终会验证。

## root=[ROOT]

指示是否执行传统的（非旁路）DNSSEC 验证，如果是，则指定信任锚点的名称。默认使用 `"."`（根区域）作为信任锚进行验证，该锚点有一个内置密钥。如果指定了不同的信任锚，则必须使用 `-a` 来指定包含该密钥的文件。

## dv=[DLV]

指示是否执行 DNSSEC 旁路验证（lookaside validation），如果是，则指定 DLV 信任锚点的名称。默认使用 `"dlv.isc.org"` 作为信任锚进行旁路验证，该锚点有一个内置密钥。如果指定了不同的名称，则必须使用 `-a` 来指定包含 DLV 密钥的文件。

## FILES

`/etc/bind.keys`

`/etc/resolv.conf`

## SEE ALSO

`dig(1)`, `named(8)`, RFC4034, RFC4035, RFC4431, RFC5074, RFC5155.

## COPYRIGHT

Copyright © 2014 Internet Systems Consortium, Inc (“ISC”)

# NAME

`derdump_` - 从 DER 编码的证书文件中导出 C-sequence 字符串

# SYNOPSIS

```
derdump [-r] [-i input-file] [-o output-file]
```

# STATUS

此文档正在进行中。请在 Mozilla NSS bug 836477 中参与初始审查工作。

# DESCRIPTION

`derdump` 从 DER 编码的证书文件中导出 C-sequence 字符串

# OPTIONS

`-r`

对于格式化项目，也导出原始字节

`-i DER 编码文件`

定义要使用的输入文件（默认为 stdin）

`-o 输出文件`

定义要使用的输出文件（默认为 stdout）。

# ADDITIONAL RESOURCES

NSS 通过 Mozilla Fedora 与 PKI 及与安全相关的项目共同维护。最贴相关的项目是 Dogtag PKI，其项目 wiki 位于 PKI Wiki。

有关 NSS 的特定信息，NSS 项目 wiki 位于 Mozilla NSS site。NSS 站点直接关系到 NSS 代码更改和发布。

邮件列表：`pki-devel@redhat.com` 和 `pki-users@redhat.com`

IRC: Freenode  `#dogtag-pki`

# AUTHORS

NSS 工具由曾在 Netscape 现于 Red Hat 的开发者编写并维护。

作者：Gerhardus Geldenhuis <gerhardus.geldenhuis@gmail.com>. Elio Maldonado <emaldona@redhat.com>, Deon Lackey <dlackey@redhat.com>

# LICENSE



根据 Mozilla Public License 1.1 版本、和/或 GNU General Public License 2 或更高版本、和/或 GNU Lesser General Public License 2.1 或更高版本进行许可。

## NOTES
- 1. Mozilla NSS bug 836477
  https://bugzilla.mozilla.org/show_bug.cgi?id=836477
- 2. PKI Wiki
  http://pki.fedoraproject.org/wiki/
- 3. Mozilla NSS site
  http://www.mozilla.org/projects/security/pki/nss/
`desktop-file-install`, `desktop-file-edit` - 桌面文件的安装与编辑

## SYNOPSIS
`desktop-file-install [--dir=DIR] [-m MODE|--mode=MODE] [--vendor=VENDOR] [--delete-original] [--rebuild-mime-info-cache] [EDITOPTION]... FILE...`
`desktop-file-edit [EDITOPTION]... FILE`

## DESCRIPTION
`desktop-file-install` 程序是一个用于安装（以及可选编辑）桌面文件的工具。`desktop-file-edit` 程序是一个用于编辑桌面文件的工具。它们对于开发者和打包人员来说非常有用。
有多种可用选项来编辑桌面文件。编辑选项可以多次指定，并将按照传递给程序的选项相同顺序进行处理。
`desktop-file-install` 和 `desktop-file-edit` 将始终尝试验证生成的桌面文件。验证失败可能会导致生成的桌面文件异常。

## OPTIONS
- `--dir=DIR`
  安装桌面文件。
- `-m MODE|--mode=MODE`
  将模式设置为 `MODE`。
- `--vendor=VENDOR`
  将厂商设置为 `VENDOR`。
- `--delete-original`
  删除原始文件。
- `--rebuild-mime-info-cache`
  重建 mime-info 缓存。
- `[EDITOPTION]... FILE...`
  `desktop-file-install` 和 `desktop-file-edit` 将
  `desktop-file-install` 和 `desktop-file-edit` 将始终尝试验证生成的桌面文件。验证失败可能会导致生成的桌面文件异常。

- `--set-key=NAME`
  将名称（key Name）设置为 `NAME`。如果已设置了名称，它将被覆盖。
- `--set-value=VALUE`
  将值（key Value）设置为 `VALUE`。如果已设置了值，将被覆盖。
- `--copy-name`
  将 Name 键的值复制到 Name 键。
- `--copy-value`
  将 Value 键的值复制到 Value 键。
- `--set-comment=COMMENT`
  将注释（key Comment）设置为 `COMMENT`。如果已设置了注释，将被覆盖。
- `--set-icon=ICON`
  将图标（key Icon）设置为 `ICON`。如果已设置了图标，将被覆盖。
- `--add-category=CATEGORY`
  将 `CATEGORY` 添加到类别列表（Categories）。如果 `CATEGORY` 已经在列表中，则该操作无效。
- `--remove-category=CATEGORY`
  从类别列表（Categories）移除 `CATEGORY`。
- `--add-mime-type=MIME-TYPE`
  将 `MIME-TYPE` 添加到 MIME 类型列表（key Mtype）。如果 `MIME-TYPE` 已经在列表中，则该操作无效。
- `--remove-mime-type=MIME-TYPE`
  从 MIME 类型列表（key Mtype）移除 `MIME-TYPE`。
- `--add-only-show-in=ENVIRONMENT`
  将 `ENVIRONMENT` 添加到显示的桌面环境列表（key OnlyShowIn）。如果 `ENVIRONMENT` 已经在列表中，未注册的桌面环境应前缀 X-。
- `--remove-only-show-in=ENVIRONMENT`
  从显示的桌面环境列表（key OnlyShowIn）中移除 `ENVIRONMENT`。如果 `ENVIRONMENT` 不在列表中，则该操作无效。
- `--add-not-show-in=ENVIRONMENT`
  将 `ENVIRONMENT` 添加到不显示的桌面环境列表（key NotShowIn）。如果 `ENVIRONMENT` 已经在列表中，应前缀 X-。
- `--remove-not-show-in=ENVIRONMENT`
  从不显示的桌面环境列表（key NotShowIn）中移除 `ENVIRONMENT`。如果 `ENVIRONMENT` 不在列表中，则该操作无效。

## 环境变量
某些环境变量会改变 `desktop-file-install` 的行为：

### DESKTOP_FILE_VENDOR
此变量可以作为 `--vendor` 选项的替代方案。如果使用了 `--vendor` 选项，则会忽略此环境变量。

### DESKTOP_FILE_INSTALL_DIR
此变量可以作为 `--dir` 选项的替代方案。如果使用了 `--dir` 选项，则会忽略此环境变量。

### RPM_BUILD_ROOT
此变量在构建 RPM 软件包时设置。如果没有使用 `--dir` 选项和 `DESKTOP_FILE_INSTALL_DIR` 环境变量，它将自动前置到默认安装目录之前，以便在构建包时正确地安装桌面文件。

## 缺陷
如果您在 `desktop-file-install` 程序中发现缺陷，请在 https://bugs.freedesktop.org 报告。

# 另请
`desktop-file-validate(1)` `update-desktop-database(1)`

## 名称
`desktop-file-validate` - 验证桌面条目文件

# 概要
`desktop-file-validate [--no-hints] [--no-warn-deprecated] [--warn-kde] FILE...`

### 描述
`desktop-file-validate` 程序是一个根据桌面条目规范 1.1 验证桌面条目文件的工具。
规范描述了一种文件格式，用于为应用程序提供名称、图标和描述等信息。该文件随后可以作为应用程序启动器，并在应用程序菜单中显示应用程序。
有关桌面条目规范的信息，请参阅 http://freedesktop.org/wiki/Specifications/desktop-entry-spec。
桌面条目文件通常被称为桌面文件 (`desktop files`)。

### 选项
支持以下选项：
- `-no-hints`
  不输出关于桌面文件中可能改进内容的提示。
- `-no-warn-deprecated`
  不对使用规范旧版本中定义的弃用项发出警告。
- `-warn-kde`
  对使用规范的 KDE 扩展发出警告。这包括使用 KDE 桌面条目组、ServiceTypes、DocPath、Keywords、InitialPreference、Dev、FSType、MountPoint、ReadOnly、UnmountIcon 键，或者 Service、PolicyService 和 FSDevice 类型。

## 缺陷
如果您在 `desktop-file-validate` 程序中发现缺陷，请在 https://bugs.freedesktop.org 报告。

# 另请
`desktop-file-edit(1)` `desktop-file-install(1)`

## 名称
`devassistant` - 设置开发环境并创建各种语言的基础项目

# 概要
`devassistant [--debug] [--no-cache] [ ASSISTANT_TYPE ] [ OPTIONS ] [[ SUBASSISTANT ] [OPTIONS] ...]`
`devassistant [--debug] [--no-cache] [ ACTION ] [ OPTIONS ]`

### 描述
请注意，`da` 命令是运行 DevAssistant 的推荐方式（尽管其工作完全相同）。
`devassistant` 是 DevAssistant 的主命令。它负责将命令行调用调度给助手或操作。它接受一些可选标志：
- `--debug` 让 DevAssistant 记录大量的调试信息
- `--no-cache` 让 DevAssistant 读取所有独立的助手并完全忽略缓存

# 描述 - ASSISTANT_TYPE



DevAssistant 可以在开发过程中帮助您完成各种任务。这些任务由所谓的“助手 (`assistants`)”执行——共有四种助手：

- `create` - 创建新项目、安装依赖项并设置环境
- `modify` - 修改之前创建的项目（例如将其导入 Eclipse）
- `prepare` - 为上游项目准备开发环境
- `task` - 执行与特定项目相关的自定义任务

您可以将 `"create"` 缩写为 `"crt"`, `"modify"` 缩写为 `"mod"`, `"prepare"` 缩写为 `"prep"`。

每个助手类型都可以有许多关联助手（例如 `python`, `ruby`），每个助手都可以有许多关联子助手（例如 `django`, `flask`）。您可以通过运行例如 `devassistant crt -h` 和 `devassistant crt python -h` 来显示这些（以及其他选项）。一旦您选择了所需的助手（及其子助手），只需运行它即可，例如 `devassistant crt python django -n newproject`。

助手列表及其功能可能会根据您的安装情况而异——只需运行 `help` 即可查看当前可用的助手。（注意：`devassistant crt -h text` 在源码中重复出现并在此处合并）。

## 描述 - ACTION

DevAssistant 设计还旨在通过所谓的“操作 (`actions`)”提供自定义功能。

目前，这些包含：

- `help` - 显示详细帮助信息。
- `version` - 显示 `devassistant` 版本。

再次，要显示选项，只需在操作时使用 `-h`，例如 `devassistant version -h`。

## 通用选项

许多助手之间共享一些常用选项。它们的通常含义如下所示：

- `-h`
  打印助手的帮助信息。
- `-n`
  项目名称。
- `-e`
  将项目导入 eclipse。
- `-g`
  生成一个 SPEC 文件。
- `-b`
  构建 RPM
- `-v`
  vim 设置。

### 环境变量

`DEVASSISTANT_PATH`

一个用冒号分隔的目录列表，用于在其中搜索。如果找到多个同名的助手，将使用其中的第一个。

## 另请

`da(1)` `gui(1)`

## 名称

`df` - 报告文件系统磁盘占用

## 概要

```
df [OPTION]... [FILE]
```

### 描述

本帮助页文档了 GNU 版本的 `df`。`df` 显示文件系统上的可用空间。如果没有给出文件名，则显示所有当前挂载文件系统的空间。默认以 1K 块显示磁盘空间，除非设置环境变量 `POSIX_CORRECT`，则使用 512 字节块。

如果参数是包含挂载文件系统的绝对文件名，`df` 显示该文件系统的可用空间。此版本的 `df` 无法显示未挂载文件系统的可用空间，因为大多数此类操作需要对文件系统结构的非移植知识。

### 选项

显示文件所在文件系统的信息，默认显示所有。

长选项的强制参数对于短选项也是强制的。

- `-a`, `--all`
  包括伪文件、不可访问的文件系统
- `-B`, `--block-size=SIZE`
  打印前按 SIZE 缩放；例如‘BM’以 1048576 字节为单位打印；使用 SIZE 前缀
- `--direct`
  显示文件而非挂载点的统计信息
- `-h`, `--human-readable`
  以 1024 的幂打印大小（例如 1023M）
- `-H`, `--si`
  以 1000 的幂打印大小（例如 1.1G）
- `-i`, `--inodes`
  列出 inode 信息而不是块使用
- `-k`
  同 `--block-size=1K`
- `-l`, `--local`
  限制于本地文件系统
- `--no-sync`
  在获取使用信息时不调用同步（默认）
- `--output=[FIELD_LIST]`
  使用由 FIELD_LIST 定义的输出格式，如果省略则打印所有字段
- `-P`, `--portability`
  使用 POSIX 输出格式
- `--sync`
  在获取使用信息前调用同步
- `--total`
  忽略所有对可用空间不重要的条目，产生总计
- `-t`, `--type=TYPE`
  限制为类型 TYPE 文件系统
- `-T`, `--print-type`
  打印文件系统类型
- `-x`, `--exclude-type=TYPE`
  限制为非类型 TYPE 文件系统
- `-v`
  （被忽略）
- `--help`
  显示此帮助并退出

## 版本

输出版本信息并退出

显示值的单位取决于 `--block-size` 以及 `DF_BLOCK_SIZE`、`BLOCK_SIZE` 和 `BLOCKSIZE` 环境变量中的第一个可用值。否则，单位默认为 1024 字节（如果设置了 `POSIXLY_CORRECT`，则为 512）。

SIZE 参数是一个整数和一个可选单位（例如：10K 是 10*1024）。单位有 K、M、G、T、P、E、Z、Y（1024 的幂）或 KB、MB,...（1000 的幂）。

FIELD_LIST 是一个用逗号分隔的列列表，表示要包含的列。有效的字段名有：'source'、'ftype'、'itotal'、'iused'、'iaval'、'ipcent'、'size'、'used'、'avail'、'pcent'、'file' 和 'target'

### 作者

由 Torbjorn Granlund、David MacKenzie 和 Paul Eggert 编写。

## 报告错误

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 将 `df` 的翻译错误报告到 <http://translationproject.org/team/>

## 版权

Copyright © 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 3 版或更高版本 <http://gnu.org/licenses/gpl.html>。这是一个自由软件：你可以自由地更改和重新发行它。在法律允许的范围内不提供任何保证。

## 另请

完整文档位于：<http://www.gnu.org/software/coreutils/df> 或通过本地信息可用：info ‘(coreutils)’ `df` 调用

## 名称

`dgst`, `sha`, `sha1`, `mdc2`, `ripemd160`, `sha224`, `sha256`, `sha384`, `sha512`, `md2`, `md4`, `md5`, `dss1` - 消息摘要

### 概要

```
openssl digest [-sha1|-mdc2|-ripemd160|-sha224|-sha256|-sha384|-sha512|-md2|-md4|-md5|-dss1] [-c] [-d] [-hex] [-binary] [-r] [-hmac arg] [-non-fips-allow] [-filename] [-sign filename] [-keyform arg] [-passin arg] [-verify filename] [-prverify filename] [-signature filename] [-hmac key] [-non-fips-allow] [-fips-fingerprint] [file...]
openssl [digest] [...]
```

### 描述

摘要函数以十六进制格式输出提供的文件的消息摘要。

摘要函数还使用消息摘要生成并验证数字签名。

### 选项

- `-c`
  仅在使用十六进制格式输出时，以冒号分隔的两位一组形式打印摘要。
- `-d`
  打印 BIO 调试信息。
- `-hex`
  以十六进制转储输出摘要。这是“正常”摘要（相对于数字签名）的默认情况。参见下方的数字签名 -hex。
- `-binary`
  以二进制形式输出摘要或签名。
- `-r`
  以 sha1sum 等程序使用的“coreutils”格式输出摘要。
- `-hmac arg`
  将 HMAC 密钥设置为“arg”。
- `-non-fips-allow`
  在 FIPS 模式下允许使用非 FIPS 摘要。这在非 FIPS 模式下没有影响。
- `-out filename`
  输出的文件名，默认为标准输出。
- `-sign filename`
  使用“filename”中的私钥对摘要进行数字签名。
- `-keyform arg`
  指定用于签名摘要的密钥格式。支持 DER、PEM、P12 和 ENGINE 格式。
- `-engine id`
  使用引擎进行操作（包括私钥存储）。此引擎不作为摘要算法的源，除非在配置文件中也指定。
- `-sigopt nm:v`
  在签名或验证操作期间将选项传递给签名算法。这些选项的名称和值取决于算法。
- `-passin arg`



私钥密码源。关于 `arg` 格式的更多信息请参见 `openssl(1)` 中的 `PASS PHRASE ARGUMENTS` 部分。

- `-verify filename`

使用“filename”中的公钥验证签名。输出为“Verification OK”或“Verification Failure”。

- `-prverify filename`

使用“filename”中的私钥验证签名。

- `-signature filename`

要验证的实际签名。

- `-hmac key`

使用“key”创建哈希 MAC。

# mac 算法

MAC（密钥化消息认证码）。最流行的 MAC 算法是 HMAC（基于哈希的 MAC），但其他其他基于哈希的 MAC 算法，例如 `ccgos` 引擎支持的 `gost-mac` 算法。MAC 密钥和其他选项应通过 `-macopt` 参数设置。

`-macopt nm:v`

将选项传递给由 `-mac` 指定的 MAC 算法。HMAC 和 `gost-mac` 都支持以下选项：

`key:string`

指定 MAC 密钥为字母数字字符串（如果密钥包含...后续文本略）

使用 `-dsaparam` 选项生成 DH 参数快得多，且推荐的指数长度更短，这使得密钥交换更高效。注意，对于 DSA 风格的 DH 参数，每次使用都应该创建一个新的 DH 密钥以避免小子群攻击。

- `-text` 此选项以人类可读的形式打印 DH 参数。

- `-C` 此选项将参数转换为 C 代码。然后可以通过调用 `get_dhnnumbits()` 函数加载这些参数。

- `-engine id` 指定引擎（通过其唯一 ID 字符串）将使 `dhparam` 尝试获取指定引擎的功能引用，从而在需要时对其进行初始化。该引擎将被设置为所有可用算法的默认引擎。

# 警告

程序 `dhparam` 结合了以前版本 OpenSSL 和 SSLLeay 中 `dh` 和 `gendh` 程序的功能。`dh` 和 `gendh` 程序目前仍保留，但在未来的 OpenSSL 版本中可能会有不同的用途。

# 注意事项

PEM 格式的 DH 参数使用头部和页脚行：

```
-----BEGIN DH PARAMETERS-----
-----END DH PARAMETERS-----
```

OpenSSL 目前仅支持旧的 PKCS#3 DH，不支持较新的 X9.42 DH。

此程序处理的是 DH 参数而非密钥。

## 缺陷

应该有一种生成和处理 DH 密钥的方法。

### 参见

`dsaparam(1)`

# 历史

`dhparam` 命令在 OpenSSL 0.9.5 中引入。`-dsaparam` 选项在 OpenSSL 0.9.6 中引入。

## 名称

`diff` -逐行比较文件

### 概要

```
diff [OPTION]... FILES
```

### 描述

逐行比较 `FILES`。

长选项的强制性参数对于短选项也是强制性的。

- `-normal`

输出普通 `diff`（默认值）

- `-q`, `--brief`

仅在文件不同时报告

- `-s`, `--report-identical-files`

当两个文件相同时进行报告

- `-c`, `-C NUM`, `--context[NUM]`

输出 `NUM`（默认 3）行复制的上下文

- `-u`, `-U NUM`, `--unified[NUM]`

输出 `NUM`（默认 3）行统一上下文

- `-e`, `--ed`

输出一个 `ed` 脚本

- `-n`, `--rcs`

输出 RCS 格式的 `diff`

- `-y`, `--side-by-side`

分两列输出

- `-W`, `--width=NUM`

输出最多 `NUM`（默认 130）列打印

---left-column

仅输出公共行的左侧列

- `-suppress-common-lines`

不输出公共行

- `-p`, `--show-c-function`

显示每个更改所属的 C 函数

- `-F`, `--show-function-line=RE`

显示匹配 `RE` 的最后一行

- `-label LABEL`

使用 `LABEL` 作为文件名（可以重复使用）

- `-t`, `--expand-tabs`

在输出中将制表符扩展为空格

- `-T`, `--initial-tab`

通过在开头添加制表符使制表符对齐

- `-tabsize=NUM`

每 `NUM`（默认 8）个打印列停止

- `-suppress-blank-empty`

抑制空输出行之前的空格或制表符

- `-l`, `--paginate`

将输出通过 `'pr'` 进行分页

- `-r`, `--recursive`

递归比较找到的任何子目录

- `--no-dereference`

不跟随符号链接

- `-N`, `--new-file`

将缺的文件的文件视为空

- `--unidirectional-new-file`

将不存在的第一个文件视为空

- `--ignore-file-name-case`

比较文件名时忽略大小写

- `--no-ignore-file-name-case`

比较文件名时考虑大小写

- `-x`, `--exclude=PAT`

排除匹配 `PAT` 的文件

- `-X`, `--exclude-from=FILE`

排除匹配 `FILE` 中任何模式的文件

- `--S`, `--starting-file=FILE`

在比较目录时从 `FILE` 开始

- `--from-file=FILE1`

将 `FILE1` 与所有操作数比较；`FILE1` 可以是目录

- `--to-file=FILE2`

将所有操作数与 `FILE2` 比较；`FILE2` 可以是目录

- `-i`, `--ignore-case`

忽略内容的差异

- `-E`, `--ignore-tab-expansion`

忽略制表符扩展导致的更改

- `--Z`, `--ignore-trailing-space`

忽略行尾的空白字符

- `-b`, `--ignore-space-change`

忽略空格数量的更改

- `--w`, `--ignore-all-space`

忽略所有空白字符

- `--B`, `--ignore-blank-lines`

忽略空行的更改

- `-I`, `--ignore-matching-lines=RE`

忽略所有行匹配 `RE` 的更改

- `-a`, `--text`

将所有文件视为文本

- `--strip-trailing-cr`

删除输入行末尾的回车符

- `-D`, `--ifdef=NAME`

输出带有‘`#ifdef NAME`’差异的合并文件

- `--GTYPE-group-format=GFMT`

使用 `GFMT` 格式化 `GTYPE` 输入组

- `--line-format=LFMT`

格式化所有输入行=`LFMT`

- `--LTYPE-line-format=LFMT`

`LTYPE` 输入选项对 `diff` 的输出提供细粒度控制，是 `-D/--ifdef` 的扩展。

`LTYPE` 为 `'old'`、`'new'` 或 `'unchanged'`。

`GTYPE` 为 `LTYPE` 或 `'changed'`。

`GFMT`（仅）可以包含：

`%<`

来自 `FILE1` 的行

`%>`

来自 `FILE2` 的行

`%=`

`FILE1` 和 `FILE2` 的公共行

### 作者

由 Randy Smith 编写。

# 报告漏洞

向此处报告漏洞：`bug-diffutils@gnu.org` GNU `diffutils` 主页：

`<http://www.gnu.org/software/diffutils/>` 使用 GNU 软件的通用帮助：

`<http://www.gnu.org/gethelp/>`

# 版权

版权所有 © 2011 Free Software Foundation, Inc. 许可协议 GPLv3+: GNU GPL 3 或更高版本 `<http://gnu.org/licenses/gpl.html>`。这是一款自由软件：你可以自由地更改和分发它。在法律允许的范围内，不提供任何保证。

### 参见

`cmp(1)`, `diff(1)`, `sdiff(1)`

`diff3` 的完整文档作为 Texinfo 手册维护。如果你的站点上正确安装了 `info` 和 `diff3` 程序，则命令

```
info diff3
```

应该让你能够访问完整手册。

## 名称

`dig` - DNS 查找工具

### 摘要

```
dig [@server] [-b address] [-c class] [-f filename] [-k filename] [-m] [-p port#] [-q name]
[-t type] [-v] [-x addr] [-y [hmac:name:]key] [-4] [-6] [name] [type] [class] [queryeryopt...]
```

```
dig [-h]
dig [global-queryopt...] [query...]
```

#



`dig`（domain information groper）是一个用于查询 DNS 服务器的灵活工具。它可以执行 DNS 查找并显示从查询的服务器返回的答案。大多数 DNS 管理员使用 `dig` 来排查 DNS 问题，因为它灵活灵活、易于使用且输出清晰。其他查找工具的功能通常比 `dig` 少。

虽然 `dig` 通常配合命令行参数使用，但它也有一个批处理模式，用于从文件中读取查找请求。当给出 `-h` 选项时，会打印出其命令行参数和选项的简要总结。与之前的版本不同，BIND 9 实现的 `dig` 允许从命令行发出多次查找。

除非被指示查询特定的名称服务器，否则 `dig` 将尝试尝试 `/etc/resolv.conf` 中列出的每个服务器。如果未找到可用的服务器地址，`dig` 将将查询发送到本地主机。

当给出命令行参数或选项时，`dig` 将对 `"."`（根节点）执行 NS 查询。

可以通过 `${HOME}/digrc` 为 `dig` 设置每个用户的默认值。该文件会被读取，并在执行命令行参数之前应用其中的任何选项。

IN 和 CH 类名与 IN 和 CH 顶级域名重叠。可以使用 `-t` 和 `-c` 选项来指定类型和类，使用 `-q` 选项来指定域名，或者在查找这些顶级域名时使用 `"IN."` 和 `"CH."`。

# 简单用法

`dig` 的典型调用方式如下：

```
dig @server name type
```

其中：

`server`

是要要查询的名称服务器的名称或 IP 地址。这可以是点分十进制表示法的 IPv4 地址，也可以是冒号分隔符表示法的 IPv6 地址。当提供的 `server` 参数是主机名时，`dig` 在查询名称服务器之前会解析该名称。

如果没有提供 `server` 参数，`dig` 将查询 `/etc/resolv.conf`；如果其中有地址，它将查询该地址处的名称服务器。如果使用了 `-4` 或 `-6` 选项之一，则只尝试对应传输协议的地址。如果未找到可用的地址，`dig` 将将查询发送到本地主机。将显示响应的名称服务器的回复。

`name`

是待查找的资源记录的名称。

`type`

指示所需的查询类型 – ANY, A, MX, SIG 等。类型可以可以是任何有效的查询类型。如果没有提供类型参数，`dig` 将对 A 记录进行查找。

### 选项

`-4`

仅使用 IPv4。

`-6`

仅使用 IPv6。

`-b address[#port]`

设置查询的源 IP 地址。该地址必须是主机任一网络接口上的有效地址，或者是 `"0.0.0.0"` 或 `""`。可以通过附加 `"#<port>"` 来指定端口。

`-c class`

设置查询类。默认类是 IN；其他类为用于 Hesiod 记录的 HS 或用于 Chaosnet 记录的 CH。

`-f file`

批处理模式：`dig` 从给定文件读取要处理的查找请求列表。文件中的每行的组织方式应与通过命令行界面向 `dig` 呈现查询的方式相同。

`-i`

使用已弃的 RFC1886 IP6.INT 域进行反向 IPv6 查找，该域已不再使用。不尝试过时的位字符串标签（RFC2874）。

`-k keyfile`

使用 TSIG 签名查询，从给定文件读取密钥。密钥可以使用 `tsig-keygen(8)` 生成。在 `dig` 中使用 tsig 认证时，查询的名称服务器需要知道正在使用的密钥和算法。在 BIND 中，通过在 `named.conf` 中提供相应的 key 和 server 来实现。

`-m`

启用内存使用。

`-p port`

将查询发送到非标准端口。

`-q name`

域名。

`-t type`

资源类型。

`-v`

打印版本并退出。

`-x addr`

简化反向查找。

`-y [hmac:name:]key`

使用指定的密钥通过 TSIG 签名查询。

# 查询选项

`dig` 提供了许多查询选项，影响查找方式和结果的显示。某些选项设置或重置查询头中的标志位，某些选项决定答案的哪些部分被打印，另一些决定超时和重试策略。

每个查询选项都由加号（`+`）前缀关键字标识。某些关键字会重置选项。可以在关键字前面加上字符串 `no` 来否定该关键字的含义。其他关键字为选项（如超时间隔）分配值。它们的格式为 `+keyword=value`。关键字可以缩写，只要缩写没有歧义；例如，`+cd` 等同于 `+cdflag`。查询选项有：

`++[no]aaflag`

是 `+[no]aaonly` 的同义词。

`++[no]aaonly`

在查询中设置 `"aa"` 标志。

`++[no]additional`

显示[不显示]回复中的附加部分。默认是显示它。

`++[no]adflag`

在查询中设置[不设置] AD（真实数据）位。这请求服务器返回所有答案部分和权威部分是否都已根据服务器的安全策略被验证为安全的。AD=1 表示所有记录都已验证为安全的，且答案不是来自 OPT-OUT 范围。AD=0 表示答案的某些内容不安全或未验证。此位默认设置。

`++[no]all`

设置或清除所有显示标志。

`++[no]answer`

显示[不显示]回复中的答案部分。默认是显示它。

`++[no]authority`

显示[不显示]回复中的权威部分。默认是显示它。

尝试显示格式错误的消息内容。默认情况下不显示格式错误的答案。

`+bufsize=B`

设置使用 EDNS0 宣告的 UDP 消息缓冲区大小为 B 字节。此缓冲器的最大和最小尺寸分别为 65535 和 0。范围之外的值将被相应地向上取整或向下取整。非零值将导致发送 EDNS 查询。

`+nocdflag`

在查询中设置[不设置] CD（禁用检查）位。这请求服务器不要对响应进行 DNSSEC 验证。

`+nclass`

在打印记录时[不显示] 类别（CLASS）。

`+nocmd`

切换输出中初始注释的打印状态，该注释用于标识 `dig` 的版本以及已应用的查询选项。默认情况下打印此注释。

`+nocomments`

切换输出中注释行的显示。默认情况下打印注释。

`+nocrypto`

切换 DNSSEC 记录中加密字段的显示。此字段的内容对于调试大多数（most）DNSSEC 验证失败失败来说是非必要的，移除它们可以更容易看到常见的失败。默认显示这些字段。当省略时，它们被替换为字符串 `"[omitted]"`，或者在 DNSKEY 情况下，显示密钥 id 作为替换内容，例如 `"[key id = value]"`。

`+nodef`

已弃用，视为 `+[no]search` 的同义词。

`+nodnssec`

通过在查询附加部分的 OPT 记录中设置 DNSSEC OK 位（DO），请求发送 DNSSEC 记录。

`+domain=somename`

将搜索列表设置为单个域名 `somename`（如 `/etc/resolv.conf` 中 `domain` 指令指定的指定），并启用搜索列表处理，就像给出了 `+search` 选项一样。

`+noedns=[#]`

指定查询时使用的 EDNS 版本。有效值为 0 到 255。设置 EDNS 版本将导致发送 EDNS 查询。`+noedns` 清除记录的 EDNS 版本。EDNS 默认设置为 0。

`+noednsflags=[#]`

将必须为零的 EDNS 标志位（Z 位）指定的值。接受十进制、十六进制和八进制编码。设置命名标志（例如 DO）将被静忽略忽略。默认情况下不设置任何 Z 位。

`+noednsnegotiation`

启用/禁用 EDNS 版本协商。默认启用 EDNS 版本协商。

`+noednsopt]=code[:value]`

指定带有代码点 `code` 和可选的十六进制字符串格式负载 `value` 的 EDNS 选项。`+noedsopt` 清除要发送的 EDNS 选项。

`+noexpire`

发送一个 EDNS Expire 选项。

`+nofail`

如果收到 SERVFAIL，不要尝试下一个服务器。默认不尝试下一个服务器，这与标准的存根解析器（stub resolver）行为相反。

`+noidentify`

在启用 `+short` 选项时，显示[或不显示]提供答案的 IP 地址和端口号。如果请求短格式答案，默认不显示提供答案的服务器源地址和端口号。

`+noignore`

忽略 UDP 响应中的截断，而不是使用 TCP 重试。默认情况下执行 TCP 重试。

`+nokeopen`

在查询之间保持 TCP 套接字打开并重用它，而不是为每次查找创建新的 TCP 套接字。默认是 `+nokeopen`。

`+[no]multiline`

以详细的多行格式和人类可读的注释打印记录（如 SOA 记录）。默认每条记录打印在一行上，以便机器对 `dig` 输出进行解析。

`+ndots=D`

设置名称中必须出现 D 个点，该名称才能被视为绝对路径。默认值由 `/etc/resolv.conf` 中的 `ndots` 语句定义，如果没有 `ndots` 语句，则为 1。点数少于 D 的名称被解释为相对名称，并且如果设置了 `+search`，则将在 `/etc/resolv.conf` 中 `search domain` 指令列出的域名中进行搜索。

`+[no]nsid`

在发送查询时包含 EDNS 名称服务器 ID 请求。

`+[no]nssearch`



当设置此选项时，`dig` 尝试查找包含被查询名称的区域权威名称服务器，并显示每个名称服务器为该区域的 SOA 记录。

# `+[no]onesoa`

在执行 `AXFR` 时仅打印一个（起始）SOA 记录。默认同时打印起始和结束的 SOA 记录。

# `+[no]opcode=value`

将 DNS 消息操作码（opcode）[恢复]为指定的值。默认值是 `QUERY` (0)。

# `+[no]qr`

在发送查询时打印[或不打印]查询。默认情况下不打印查询。

# `+[no]question`

当返回答案时打印[或不打印]查询的问题部分。默认将问题部分作为注释打印。

# `+[no]rdflag`

`+[no]recurse` 的同义词。

# `+[no]recurse`

切换查询中 RD（想要递归）位的设置。该位默认设置，这意味着 `dig` 通常会发送递归查询。当使用 `+nsearch` 或 `+trace` 查询选项时，会自动禁用递归。

# `+retry=T`

将向服务器尝试 UDP 查询的次数设置为 T，而不是使用默认的 3 次。如果 T 小于或等于 0，则尝试次数被静默向上取整为 1。

# `+norrcomments`

切换输出中每条记录注释的显示（例如 `DNSKEY` 记录）。除非激活多行模式，否则不打印。

# `+[no]search`

使用[不使用] `resolv.conf` 中定义的搜索列表（如果有）。默认行为是使用搜索列表。`resolv.conf` 中的 `ndots`（默认 1）决定了名称是否被视为相对名称。

# `+[no]short`

提供简短答案。默认以详细形式打印答案。

# `+[no]showsearch`

执行[不执行]显示中间结果的搜索。

# `+[no]sigchase`

追踪 DNSSEC 签名链。需要编译时带有 `-DDIG_SIGCHASE`。

# `+sit=`

提供源身份 EDNS 选项，带有可选值。重放响应的 SIT 将允许服务器识别客户端。默认是 `+nosit`。目前实验性代码 65001。

# `+split=W`

将资源记录中的十六进制或 base64 格式字段拆分为 W 个字符的块（W 是 4 的倍数）。`+nosplit` 或 `+split=0` 完全不分割。默认是 56 个字符，在多行模式下为 44 个字符。

# `+stats`

此查询选项切换统计打印：查询的时间、响应的大小等。默认行为是打印查询统计信息。

# `+subnet-addr/prefix`

带有指定的 IP 地址或网络前缀发送 EDNS 客户端子选项。

# `+ntcp`

查询名称服务器时[不使用] TCP。默认行为是使用 UDP，除非请求 `tcp=N` 查询，此时默认使用 TCP。`AXFR` 查询始终使用 TCP。

# `+time=T`

设置查询超时为 T 秒。默认超时时间为 5 秒。尝试将 T 设置为小于 1 将导致 1 秒的查询超时。

# `+nottopdown`

追踪 DNSSEC 签名链时执行自顶向验证。需要编译时带有 `-DDIG_SIGCHASE`。

# `+[no]trace`

切换从根名称服务器到被查询名称的委托路径追踪。默认禁用追踪。当启用追踪时，`dig` 进行迭代查询以解析被查询名称。它将遵循根服务器的引用，显示用于解析查找的每个服务器的答案。

如果指定了 `@server`，它仅影响根服务器的初始查询。

设置 `+trace` 时也会设置 `+dnsec`，以便模拟名称服务器的默认查询。

# `+tries=T`

将向服务器尝试 UDP 查询的次数设置为 T，而不是使用默认的 3 次。如果 T 小于或等于 0，则尝试次数被静默向上取整为 1。

## `trusted-key=####`

指定一个包含信任密钥的文件，用于 `+sigchase`。每个 `DNSKEY` 记录必须单独占一行。

如果未指定，`dig` 将首先查找 `/etc/trusted-key.key`，然后查找当前目录下的 `trusted-key.key`。

要求 `dig` 在编译时带有 `-DDIG_SIGCHASE` 参数。

## `+[no]ttl`

在打印记录时[显示/不显示] TTL。

## `+[no]vc`

在查询名称服务器时[使用/不使用] TCP。这是 `+[no]tcp` 的替代语法，为了向后兼容而提供的。“vc”代表“virtual circuit（虚拟电路）”。

## 次重查询

`**dig**` 的 BIND 2 实现支持在命令行指定多个查询（此外还支持 **`-f`** 批量文件选项）。每个此类查询都可以提供其单独的一套标志、选项和查询选项。

在这种情况下，每个查询参数代表上述命令行语法描述中的一个单独查询。每个查询由任何标准选项和标志、要查找的名称、可选的查询类型和类，以及任何适用于该查询的查询选项组成。

还可以提供一组应用于所有查询的全局查询选项。这些全局查询选项必须在命令行提供的第一组“名称、类、类型、选项、标志和查询选项”元组之前。任何全局查询选项（`+ [no]cmd` 选项除外）都可以被特定查询的选项集覆盖。例如：

```
dig +qr www.isc.org any -x 127.0.0.1 isc.org ns +noqr
```

显示了如何从命令行使用 `dig` 进行三次查找：对 `www.isc.org` 的 ANY 查询、对 `127.0.0.1` 的反向查找，以及对 `isc.org` NS 记录的查询。应用了全局查询选项 `+qr`，因此 `dig` 显示了每次查找时执行的初始查询。最后一个查询具有本地查询选项 `+noqr`，这意味着 `dig` 在查找 `isc.org` 的 NS 记录时不会打印初始查询。

## IDN 支持

如果 `dig` 在构建时启用了 IDN（国际化域名名）支持，它就可以接受并显示非 ASCII 域名。`dig` 在向 DNS 服务器发送请求之前或显示服务器回复之前，会适当转换域名的字符编码。如果你出于某些原因关闭 IDN 支持，请定义环境变量 `CHARSET=ASCII`。当 `dig` 运行时设置了该变量时，IDN 支持被禁用。

## 返回码

`Dig` 的返回码为：

- * 0: 一切顺利，包括 NXDOMAIN 等情况

- 1: 使用错误

- 8: 无法打开批量文件

- 9: 服务器未响应

- 10: 内部错误

### 文件

`/etc/resolv.conf`

`${HOME}/.digrc`

### 参见

`host(1)`, `named(8)`, `dnssec-keygen(8)`, `RFC1035`.

## 缺陷

查询选项可能太多了。

## 版权

Copyright © 2004-2011, 2013-2015 Internet Systems Consortium, Inc. (“ISC”) Copyright © 2000-2003 Internet Software Consortium.

## 名称

`dircolors` - 为 ls 颜色设置

### 摘要

`dircolors [OPTION]... [FILE]`

### 描述

输出用于设置 `LS_COLORS` 环境变量的命令。

确定输出格式：

- `-b`, `--sh`, `--bourne-shell`

  输出设置 `LS_COLORS` 的 Bourne shell 代码

- `-c`, `--csh`, `--c-shell`

  输出设置 `LS_COLORS` 的 C shell 代码

- `-p`, `--print-database`

  输出默认值

- `--help`

  显示此帮助并退出

- `--version`

  输出版本信息并退出

如果指定了 FILE，将读取它以确定为哪些文件类型和扩展使用哪些颜色。否则，将使用预编译的数据库。有关这些文件格式的详细信息，请运行 `dircolors --print-database`。

### 作者

H. Peter Anvin 编写。

## 报告缺陷

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 向 <http://translationproject.org/team/> 报告 `dircolors` 翻译缺陷。

## 版权

Copyright © 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL 3 或更高版本 <http://gnu.org/licenses/gpl.html>。这是一个免费软件：你可以自由地更改和重新发它。在法律允许的范围内，不提供任何保证。

### 参见

完整文档位于：<http://www.gnu.org/software/coreutils/dircolors> 或通过本地信息可用：info ‘coreutils dircolors invocation’

## 名称

`dirmngr-client` - 访问 Dirmngr 服务的工具

### 摘要

```
dirmngr-client [options] [file|pattern]
```

### 描述



`dirmngr-client` 是一个用于联系 `dirmngr` 并测试证书是否已撤销（通过列在 CRL 中或通过运行 OCSP）的简单工具。如果没有 `dirmngr` 在运行，将启动新实例。运行此工具的通常方法是：

```
dirmngr-client acert
```

或者

```
dirmngr-client acert
```

其中 `acert` 是一个 X.509 证书。

## 返回值

`dirmngr-client` 返回这些值：

- `0` 涉及的证书是有效的；即有有效的 CRL 可
- `1` 证书已撤销
- `2` 检查状态时出现问题（以及其他值）

### 选项

`dirmngr-client` 可以带有以下选项调用：

- `-version`

  打印程序版本和许可信息。注意你不能省略此命令。
- `-help`, `-h`

  打印汇总常用选项的使用消息。注意你不能省略此命令。
- `-quiet`, `-q`

  通过抑制信息消息使输出额外简洁。
- `-v`

  在运行时输出附加信息。你可以增加详细程度，如 `-v`。
- `-pem`

  假设给定的证书是 PEM（加密）格式。
- `-ocsp`

  使用 OCSP 协议检查并忽略任何 CRL。
- `-force-default-responder`

  在使用 OCSP 时强制使用默认响应者，而不是使用证书提供的响应者。
- `-ping`

  检查 `dirmngr` 守护进程是否运行。
- `-cache-cert`

  将给定的证书放入 `dirmngr` 的缓存中。这主要用于调试。
- `-validate`

  使用 `dirmngr` 的代码验证给定的证书。这主要用于调试。
- `-load-crl`

  此命令期望 DER 编码 CRL 文件的文件名列表。选项 `--url` 替代文件名并直接从给定位置加载。所有 CRL 将被验证并加载到 `dirmngr` 缓存中。
- `-lookup`

  获取剩余参数并对每个参数运行查找。结果是 Base64 编码输出（不包含标题行）。这可以从服务器检索证书。然而，如果返回多个证书，输出格式并不理想。
- `--url`, `-u`

  修改 `lookup` 和 `load-crl` 命令以接受 URL。
- `--local`, `-l`

  让 `lookup` 命令仅搜索本地缓存。
- `--squid-mode`

  以模式运行 `dirmngr-client`，适用于 Squid `external_acl_type` 选项的辅助程序。

### 参见

`dirmngr(8)`, `gpgsm(1)`

此工具的完整文档维护在 Texinfo 手册。如果 GnuPG 和 `info` 程序在你的站点正确安装，执行命令

```
info gnupg
```

应该可以让你访问完整的手册，包括菜单结构和索引。

## 名称

`dirname` - 去掉文件名的最后一个部分

### 摘要

`dirname [OPTION] NAME...`

### 描述

输出每个 `NAME` 并保留其最后一个非斜杠组件，同时移除末尾的斜杠；如果 `NAME` 不包含 `'/'`，则输出 `'.'`（表示当前目录）。

- `-z`, `--zero`

  在每个输出行末尾以 NUL ，而不是换行符
- `--help`

  显示此帮助信息并退出
- `--version`

  输出版本信息并退出

## 示例

```
dirname /usr/bin/
-> "usr"
dirname dir1/str dir2/str
-> "dir1" 后接 "dir2"
dirname stdio.h
-> " "
```

### 作者

由 David MacKenzie 和 Jim Meyering 编写。

## 报告错误

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 请向 <http://translationproject.org/team/> 报告 `dirname` 的翻译错误

## 版权所有

版权所有 © 2015 Free Software Foundation, Inc. 许可证 GPLv3+: 遵循 GPL 第3 版或更高版本 <http://gnu.org/licenses/gpl.html>。这是一个自由软件：你可以自由地更改和重新分发它。在法律允许范围内不提供任何保证。

## 另请

`basename(1)`, `readlink(1)`

完整文档可见：<http://www.gnu.org/software/coreutils/dirname> 或通过本地查看：`info '(coreutils) dirname invocation'`

## 名称

`dmesg` - 打印或控制内核环形缓冲区

### 摘要

`dmesg [options]`

`dmesg --clear` `dmesg --read-clear [options]` `dmesg --console-level level` `dmesg --console-on` `dmesg --console-off`

### 描述

`dmesg` 用于检查或控制内核环形缓冲区。

默认操作是显示内核环形缓冲区的所有消息。

### 选项

`--clear`, `--read-clear`, `--console-on`, `--console-off` 和 `--console-level` 选项是互斥的。

- `-C`, `--clear`

  清空环形缓冲区。
- `-c`, `--read-clear`

  在打印内容后清空环形缓冲区。
- `-D`, `--console-off`

  禁用向控制台打印消息。
- `-d`, `--show-delta`

  显示时间戳和消息之间的时间差。如果与 `--then` 配合使用，则只打印时间差而不打印时间戳。
- `-E`, `--console-on`

  启用向控制台打印消息。
- `-e`, `--reltime`

  以人类可读的格式显示本地时间和增量。注意，转换为本地时间可能是不准确的（详情请参见 `-T`）。
- `-F`, `--file file`

  从给文件读取消息。
- `-f`, `--facility list`

  将输出限制为指定的（逗号分隔）设施列表。例如：

  ```
  dmesg --facility=daemon
  ```

  将只打印系统守护进程的消息。对于所有支持的功能，请参阅 `--help` 输出。
- `-H`, `--human`

  启用人类可读输出。另请参见 `--color`, `--reltime` 和 `--nopager`。
- `-k`, `--kernel`

  打印内核消息。
- `-L`, `--color[when]`

  输出上色。可选参数 `when` 可以是 `auto`、`never` 或 `always`。如果省略 `when`，则默认为 `auto`。可以禁用颜色，适用于当前内置的 `--help` 输出。另请参见 COLORS 章节。
- `-l`, `--level list`

  将输出限制为指定的（逗号分隔）级别列表。例如：

  ```
  dmesg --level=err,warn
  ```

  将只打印错误和警告消息。对于所有支持的功能，请参阅 `--help` 输出。
- `-n`, `--console-level level`

  设置打印到控制台的级别。级别是一个数字或级别名称的缩写。对于所有支持的级别，请参阅 `--help` 输出。

  例如，`-n 1` 或 `-n alert` 会防止紧急（恐慌）消息以外的所有消息出现在控制台上。所有层级的消息仍会被写入 `/proc/kmsg`，因此可以使用 `syslog(8)` 精确控制内核消息出现的位置。当使用 `-n` 选项时，`dmesg` 将不会打印或清空内核环形缓冲区。

- `-P`, `--nopager`

  不将输出通过管道交给分页器。对于 `--human` 输出，默认启用分页器。
- `-r`, `--raw`

  打印原始格式缓冲区，即不剥离日志级前缀。注意，原始格式返回内核消息。`/dev/kmsg` 设备使用的格式与 `syslog(2)` 不同。为了向后兼容，`dmesg(1)` 始终以 `syslog(2)` 格式返回数据。可以通过命令 `'dd iflag=nonblock'` 等从 `/dev/kmsg` 读取原始数据。
- `-S`, `--syslog`

  强制 `dmesg` 使用 `syslog(2)` 内核接口读取内核消息。从内核 3.5.0 开始，默认使用 `/dev/kmsg` 而不是 `syslog(2)`。
- `-s`, `--buffer-size`

  使用大小为相应的缓冲区查询内核环形缓冲区。默认为 `16392`。（默认内核缓冲区大小在 3.5.4 之后为 4096 或 8192）。如果将内核缓冲区设置为大于默认值，则可以使用此选项查看整个缓冲区。
- `-T`, `--ctime`

  打印人类可读的时间戳。注意，时间戳将是不准确的！日志源在挂起后不会更新。
- `-t`, `--time format`

  使用给定的格式打印时间戳，格式可以是 `ctime`、`reltime`、`delta` 或 `iso`。前三种格式是别名。`iso` 格式是实现。对于 `iso` 格式的 time戳：`iso` 格式是 `YYYY-MM-DD<HH:MM:SS>`。`iso` 格式是 `time` 格式的实现。`iso` 格式是 `time` 格式的实现。
- `-u`, `--userspace`

  打印用户空间消息。
- `-w`, `--follow`

  等待用户空间。
- `-x`, `--decode`



解码时间和级别。

- `-V`, `--version`

显示版本信息并退出。

- `-h`, `--help`

显示帮助文本并退出。

# COLORS

输出上色。可选参数 `when` 可以是 `auto`、`never` 或 `always`。如果省略 `when`，则默认为 `auto`。可以禁用颜色，适用于当前内置的 `--help` 输出。另请参见 COLORS 章节。

- 消息优先级。`time` 格式是：

- `alert`: 消息优先级。

- `crit`: 消息优先级。

- `err`: 消息优先级。

- `warn`: 消息优先级。

- `segfault`: 消息优先级。

# 另请

`syslogd(8)` `terminal-colors(5)`

### 作者

Karel

`dmesg` 最初由 Theodore 编写。

# 可用性

`dmesg` 命令是 `util-linux` 软件包的一部分，适用于 Linux 内核

## 名称

`dmesg` - 打印或控制内核环形缓冲区

### 摘要

```
dmesg [options]
dmesg --clear
dmesg --read-clear [options]
dmesg --console-level level
dmesg --console-on
dmesg --console-off
```

### 描述

`dmesg` 用于检查或控制内核环形缓冲区。

默认操作是显示内核环形缓冲区的所有消息。

### 选项

`--clear`, `--read-clear`, `--console-on`, `--console-off` 和 `--console-level` 选项是互斥的。

- `-C`, `--clear`

清空环形缓冲区。

- `-c`, `--read-clear`

在打印内容后清空环形缓冲区。

- `-D`, `--console-off`

禁用向控制台打印消息。

- `-d`, `--show-delta`

显示时间戳和消息之间的时间差。如果与 `--then` 配合使用，则只打印时间差而不打印时间戳。

- `-E`, `--console-on`

启用向控制台打印消息。

- `-e`, `--reltime`

以人类可读的格式显示本地时间和增量。注意，转换为本地时间可能是不准确的（详情请参见 `-T`）。

- `-F`, `--file file`

从给文件读取消息。

- `-f`, `--facility list`

将输出限制为指定的（逗号分隔）设施列表。例如：

```
dmesg --facility=daemon
```

将只打印系统守护进程的消息。对于所有支持的功能，请参阅 `--help` 输出。

- `-H`, `--human`

启用人类可读输出。另请参见 `--color`, `--reltime` 和 `--nopager`。

- `-k`, `--kernel`

打印内核消息。

- `-L`, `--color[when]`

输出上色。可选参数 `when` 可以是 `auto`、`never` 或 `always`。如果省略 `when`，则默认为 `auto`。可以禁用颜色，适用于当前内置的 `--help` 输出。另请参见 COLORS 章节。

- `-l`, `--level list`

将输出限制为指定的（逗号分隔）级别列表。例如：

```
dmesg --level=err,warn
```

将只打印错误和警告消息。对于所有支持的功能，请参阅 `--help` 输出。

- `-n`, `--console-level level`

设置打印到控制台的级别。级别是一个数字或级别名称的缩写。对于所有支持的级别，请参阅 `--help` 输出。

例如，`-n 1` 或 `-n alert` 会防止紧急（恐慌）消息以外的所有消息出现在控制台上。所有层级的消息仍会被写入 `/proc/kmsg`，因此可以使用 `syslog(8)` 精确控制内核消息出现的位置。当使用 `-n` 选项时，`dmesg` 将不会打印或清空内核环形缓冲区。

- `-P`, `--nopager`

不将输出通过管道交给分页器。对于 `--human` 输出，默认启用分页器。

- `-r`, `--raw`

打印原始格式缓冲区，即不剥离日志级前缀。注意，原始格式返回内核消息。`/dev/kmsg` 设备使用的格式与 `syslog(2)` 不同。为了向后兼容，`dmesg(1)` 始终以 `syslog(2)` 格式返回数据。可以通过命令 `'dd iflag=nonblock'` 等从 `/dev/kmsg` 读取原始数据。

- `-S`, `--syslog`

强制 `dmesg` 使用 `syslog(2)` 内核接口读取内核消息。从内核 `3.5.0` 开始，默认使用 `/dev/kmsg` 而不是 `syslog(2)`。

- `-s`, `--buffer-size`

使用大小为相应的缓冲区查询内核环形缓冲区。默认为 `16392`。（默认内核缓冲区大小在 `3.5.4` 之后为 `4096` 或 `8192`）。如果将内核缓冲区设置为大于默认值，则可以使用此选项查看整个缓冲区。

- `-T`, `--ctime`

打印人类可读的时间戳。注意，时间戳将是不准确的！日志源在挂起后不会更新。

- `-t`, `--time format`

使用给定的格式打印时间戳，格式可以是 `ctime`、`reltime`、`delta` 或 `iso`。前三种格式是别名。`iso` 格式是实现。对于 `iso` 格式的 time戳：`iso` 格式是 `YYYY-MM-DD<HH:MM:SS>`。`iso` 格式是 `time` 格式的实现。`iso` 格式是 `time` 格式的实现。

- `-u`, `--userspace`

打印用户空间消息。

- `-w`, `--follow`

等待用户空间。

- `-x`, `--decode`

解码时间和级别。

- `-V`, `--version`

显示版本信息并退出。

- `-h`, `--help`

显示帮助文本并退出。

# COLORS

输出上色。可选参数 `when` 可以是 `auto`、`never` 或 `always`。如果省略 `when`，则默认为 `auto`。可以禁用颜色，适用于当前内置的 `--help` 输出。另请参见 COLORS 章节。

- 消息优先级。`time` 格式是：

- `alert`: 消息优先级。

- `crit`: 消息优先级。

- `err`: 消息优先级。

- `warn`: 消息优先级。

- `segfault`: 消息优先级。

# 另请

`syslogd(8)` `terminal-colors(5)`

### 作者

Karel

`dmesg` 最初由 Theodore 编写。

# 可用性

`dmesg` 命令是 `util-linux` 软件包的一部分，适用于 Linux 内核

## 名称

`dmesg` - 打印或控制内核环形缓冲区

`hostname` - 显示或设置系统主机名

`domainname` - 显示或设置 NIS/YP 域名

`ypdomainname` - 显示或设置 NIS/YP 域名

`nisdomainname` - 显示或设置 DNS 域名

### 摘要

```
hostname [-a|alias] [-d|domain] [-f|fqdn|--long] [-A|all-fqdns] [-i|ip-address] [-I|all-addresses] [-s|short] [-y|py|nis] [-b|boot] [-F|file] hostname [-h|help] [-V|version]
domainname [-F file]
ypdomainname [-F file]
nisdomainname [-F file]
```

### 描述

Hostname 用于显示系统的 DNS 名称，并显示或设置其主机名或 NIS 域名。

# 获取

当不带任何参数调用时，程序显示当前名称：

`hostname` 将打印 `gethostname(2)` 返回的系统名称。`domainname` 将打印 NIS 域名。`domainname` 使用 `gethostname(2)` 函数，而 `ydupdomainname` 和 `nisdomainname` 使用 `yp_get_default_domain(3)`。

`dnsdomainname` 将打印 FQDN（完全域名）的部分。系统的完整 FQDN 通过 `hostname --fqdn` 返回（但请参见下文 FQDN 章节的警告）。

`gethostname(2)` 用于获取主机名。当调用 `hostname -a`, `-d`, `-f` 或 `-i` 时，调用 `gethostnameby(3)`。`gethostname(2)` 和 `gethostnameby(3)` 的区别在于 `gethostnameby(3)` 感知网络，因此它会查询 `/etc/nwitch.conf` 和 `/etc/host.conf` 以决定从 `/etc/hostname` 或 `/etc/hosts` 读取信息

# 设置

当带有一个参数或使用 `--file` 选项时，命令设置主机名或 NIS 域名。`hostname` 使用 `sethostname(2)` 函数，而三个命令 `domainname`, `ydupdomainname` 和 `nisdomainname` 均使用 `sethostname(2)`。注意，这在下次重启前有效。编辑 `/etc/hostname` 进行永久更改。

注意，只有超级用户可以更改名称。

无法通过 `dnsdomainname` 命令设置 FQDN 或 DNS 域名（参见下文 FQDN 章节）。

# FQDN



系统的 FQDN（完全域名）是解析器(3) 返回的主机名，例如，`ursula.example.com`。它通常是主机名后接 DNS 域名（第一个点之后的部分）。你可以检查 FQDN

使用 `hostname --fqdn` 或使用 `dnsdomainname` 的域名。

你无法通过 `hostname` 或 `dnsdomainname` 修改 FQDN。

设置 FQDN 的推荐方法是通过 `/etc/hosts`、DNS 或 NIS 将 hostname 设为完全限定域名（FQDN）的别名。例如，如果 hostname 为“ursula”，在 `/etc/hosts` 中可能有这样一行：

```
127.0.1.1 ursula.example.com ursula
```

从技术上讲：FQDN 是 `getaddrinfo(3)` 为 `gethostname(2)` 返回的主机返回的名称。DNS 域名是第一个点之后的部分。

因此，如何更改它取决于解析器的配置（通常在 `/etc/host.conf` 中）。通常 `hosts` 文件在 DNS 或 NIS 之前被解析，因此最常见的方法是在 `/etc/hosts` 中更改 FQDN。

如果一台机器具有多个网络接口/地址，或者在移动环境中使用，它可能有多个 FQDN/域名，或者一个都没有。因此，请避免使用 `hostname --fqdn`、`hostname --domain` 和 `dnsdomainname`。`hostname --address` 也存在同样的限制，因此也应避免。

# OPTIONS

- `-a`, `--alias`

显示主机的别名（如果已使用）。此选项已弃用，不应再次使用。

- `-A`, `--all-fqdns`

显示机器的所有 FQDN。此选项会列出所有配置的网络接口上的所有配置的地址，并将它们转换为 DNS 域名。无法转换的地址（例如，因为它们没有适当的反向 IP 条目）将被跳过。注意不同的地址可能解析为相同的名称，因此输出可能包含重复项。不要对输出的顺序做任何假设。

- `-b`, `--boot`

始终设置 hostname；如果 `-F` 指定的文件不存在或为空，则在未设置时将使用默认的 hostname `localhost`。

- `-d`, `--domain`

显示 DNS 域名的名称。不要使用 `domainname` 命令来获取 DNS 域名，而不是 DNS 域名。请改用 `dnsdomainname`。请查看上文“THE FQDN”章节中的警告，并使用此选项。

- `-f`, `--fqdn`, `--long`

显示 FQDN（完全限定域名）。一个 FQDN 由短主机名和 DNS 域名组成。除非你为主机查找绑定了 NIS，否则你可以在 `/etc/hosts` 文件中更改 FQDN 和 DNS 域名（它是 FQDN 的一部分）。请查看上文“THE FQDN”章节中的警告，并尽可能使用 `hostname--all-fqdns`。

- `-F`, `--filename`

从指定文件中读取名称。忽略注释（以 `#` 开头的行）。

- `-i`, `--ip-address`

显示主机名的网络地址。注意，这仅在主机名可以解析时才有效。请避免使用此选项；请改用 `hostname--all-ip-addresses`。

- `-I`, `--all-ip-addresses`

显示主机的所有网络地址。此选项列出所有网络接口上的所有配置的地址。跳过回环接口和 IPv6 链路地址。与 `-i` 不同，此选项不依赖名称解析。不要对输出的顺序做任何假设。

- `-s`, `--short`

显示短主机名。这是在第一个点处截断的主机名。

- `-V`, `--version`

在标准输出上打印版本信息并成功退出。

- `-y`, `--yp`, `--nis`

显示 NIS 域名。如果给出了参数（或 `--file`），则 root 也可以设置新的 NIS 域。

- `-h`, `--help`

打印用法信息并退出。

# NOTES

`hostname` 在查找主机的 FQDN、别名和网络地址时尝试的地址族由你的解析器配置决定。例如，在 GNU Libc 系统上，可以通过使用 `/etc/resolv.conf` 中的 `inet6` 选项指示解析器优先尝试 IPv6 查询。

# FILES

`/etc/hostname`: 历史上，此文件本应只包含 hostname 而不是完整的规范 FQDN。现在，大多数软件都能处理完整的 FQDN。系统初始化脚本在启动时会读取此文件以设置 hostname。

`/etc/hosts`: 通常，在此处通过将 hostname 别名为 FQDN 来设置域名。

# AUTHORSORS

- Peter Tobias, <tobias@debian.de>

- Bernd Eckenfels, <nettools@debian.de>

- Michael Meskes, <meskes@debian.org>

# dos2unix

# NAME

`dos2unix` - DOS/Mac 转 Unix 文本文件转换

# SYNOPSIS

```
dos2unix [options] [FILE...]
unix2dos [options] [FILE...] [-n OUTFILE...]
```

# DESCRIPTION



`dosunix`软件包包含了 `dosunix` 和 `unix2dos` 工具，用于转换 DOS 或 Mac 格式的纯文件以及反之。在 DOS/Windows 文件中，换行符（也称为 newline）是两个字符的组合：回车（`CR`）后跟换行（`LF`）。在 Unix 文件中，换行符是单个字符：换行（`LF`）。在 Mac OS 之前的 Mac 文件中，换行符是单个回车（`CR`）。现在的 Mac 使用 Unix 风格（`LF`）换行符。`dos2unix` 还可以转换文件的编码。`Dos` 页面可以转换为 `Latin-1`。`Windows` (`UTF-16`) 文件可以转换为 `Unicode` (`UTF-8`) 文件。除非强制转换，否则二进制文件将被跳过。带有字节顺序标记（`BOM`）的文件可以 `dos`。



dosunix 软件包包含了 `dosunix` 和 `unix2dos` 工具，用于转换 DOS 或 Mac 格式的纯文件以及反之。在 DOS/Windows 文件中，换行符（也称为 newline）是两个字符的组合：回车（CR）后跟换行（LF）。在 Unix 文件中，换行符是单个字符：换行（LF）。在 Mac OS 之前的 Mac 文件中，换行符是单个回车（CR）。现在的 Mac 使用 Unix 风格（LF）换行符。`dos2unix` 还可以转换文件的编码。Dos 页面可以转换为 Latin-1。Windows (UTF-16) 文件可以转换为 Unicode (UTF-8) 文件。除非强制转换，否则二进制文件将被跳过。

```
dos2unix [options] [FILE...]
unix2dos [options] [FILE...] [-n OUTFILE...]
```

# OPTIONS

- `-a`, `--alias`
显示主机的别名（如果已使用）。此选项已弃用，不应再次使用。

- `-A`, `--all-fqdns`
显示机器的所有 FQDN。此选项会列出所有配置的网络接口上的所有配置的地址，并将它们转换为 DNS 域名。无法转换的地址（例如，因为它们没有适当的反向 IP 条目）将被跳过。注意不同的地址可能解析为相同的名称，因此输出可能包含重复项。不要对输出的顺序做任何假设。

- `-b`, `--boot`
始终设置 hostname；如果 `-F` 指定的文件不存在或为空，则在未设置时将使用默认的 hostname `localhost`。

- `-d`, `--domain`
显示 DNS 域名的名称。不要使用 `domainname` 命令来获取 DNS 域名，而不是 DNS 域名。请改用 `dnsdomainname`。请查看上文“THE FQDN”章节中的警告，并使用此选项。

- `-f`, `--fqdn`, `--long`
显示 FQDN（完全限定域名）。一个 FQDN 由短主机名和 DNS 域名组成。除非你为主机查找绑定了 NIS，否则你可以在 `/etc/hosts` 文件中更改 FQDN 和 DNS 域名（它是 FQDN 的一部分）。请查看上文“THE FQDN”章节中的警告，并尽可能使用 `hostname—all-fqdns`。

- `-F`, `--filename`
从指定文件中读取名称。注释（以 `#` 开头的行）被忽略。

- `-i`, `--ip-address`
显示主机名的网络地址。注意，这仅在主机名可以解析时才有效。请避免使用此选项；请改用 `hostname--all-ip-addresses`。

- `-I`, `--all-ip-addresses`
显示主机的所有网络地址。此选项列出所有网络接口上的所有配置的地址。跳过回环接口和 IPv6 链路地址。与 `-i` 不同，此选项不依赖名称解析。不要对输出的顺序做任何假设。

- `-s`, `--short`
显示短主机名。这是在第一个点处截断的主机名。

- `-V`, `--version`
在标准输出上打印版本信息并成功退出。

- `-y`, `--yp`, `--nis`
显示 NIS 域名。如果给出了参数（或 `--file`），则 root 也可以设置新的 NIS 域。

- `-h`, `--help`
打印用法信息并退出。

# NOTES

`hostname` 在查找主机的 FQDN、别名和网络地址时尝试的地址族由你的解析器配置决定。例如，在 GNU Libc 系统上，可以通过使用 `/etc/resolv.conf` 中的 `inet6` 选项指示解析器优先尝试 IPv6 查询。

# FILES

`/etc/hostname`: 历史上，此文件本应只包含 hostname 而不是完整的规范 FQDN。现在，大多数软件都能处理完整的 FQDN。系统初始化脚本在启动时会读取此文件以设置 hostname。

`/etc/hosts`: 通常，在此处通过将 hostname 别名为 FQDN 来设置域名。

# AUTHORS

- Peter Tobias, <tobias@debian.de>
- Bernd Eckenfels, <nettools@debian.de>
- Michael Meskes, <meskes@debian.org>

# dos2unix

# NAME

`dos2unix` - DOS/Mac 转 Unix 文本文件转换

# SYNOPSIS

```
dos2unix [options] [FILE...]
unix2dos [options] [FILE...] [-n OUTFILE...]
```

# DESCRIPTION

dosunix 软件包包含了 `dosunix` 和 `unix2dos` 工具，用于转换 DOS 或 Mac 格式的纯文件以及反之。在 DOS/Windows 文件中，换行符（也称为 newline）是两个字符的组合：回车（CR）后跟换行（LF）。在 Unix 文件中，换行符是单个字符：换行（LF）。在 Mac OS 之前的 Mac 文件中，换行符是单个回车（CR）。现在的 Mac 使用 Unix 风格（LF）换行符。`dos2unix` 还可以转换文件的编码。Dos 页面可以转换为 Latin-1。Windows (UTF-16) 文件可以转换为 Unicode (UTF-8) 文件。除非强制转换，否则二进制文件将被跳过。

- 显示程序的许可证。

- `-l`, `--newline` 添加额外的换行符。

- `dos2unix`: 仅将 dos 换行符转换为两个 Unix 换行符。在 Mac模式下，仅将 Mac 换行符转换为两个 Unix 换行符。

- `unixdos`: 仅将 Unix 换行符转换为两个 dos 换行符。在 Mac模式下，Unix 换行符转换为两个 Mac 换行符。

- `-m`, `--add-bom` 在输出文件中写入顺序标记 (BOM)。默认写入 UTF-8 BOM。

当输入文件为 UTF-16 且使用 `-u` 选项时，将写入 UTF-16 BOM。

当输出编码不是 UTF-8 或 GB18030 时，请勿使用此选项。另请参见 UNICODE。

- `-n`, `--newfile OUTFILE ...` 新文件模式。转换 INFILE 并输出写入 OUTFILE。文件名必须成对给出，且不应使用通配符名称，否则你将丢失文件。

在新文件（成对）模式下启动转换的人将成为转换后文件的所有者。新文件的读/写权限将是原文件的权限减去运行转换者的 `umask(1)`。

- `-o`, `--oldfile FILE ...` 旧文件模式。转换 FILE 并覆盖输出到该文件。程序默认在此模式下运行。可以使用通配符名称。

在旧文件（原地）模式下，转换后的文件将与原文件相同的所有者、组和读/写权限。当由另一个具有文件写权限的用户（例如 root 用户）转换文件时，也是如此。如果无法保留原始值，转换将终止。所有者的更改可能意味着原所有者无法再读取该文件。组的更改可能带来安全风险，导致文件对非目标人员可读。对所有者、组和读/写权限的保留仅在 Unix 支持。

- `-q`, quiet 抑制所有警告和信息。返回值为零。使用错误的命令行选项除外。

- `-r`, `--remove-bom` 移除顺序标记 (BOM)。不在输出文件中写入 BOM。这是转换为 Unix 换行符时的默认行为。

- `-s`, `--Safe` 保留二进制标记（默认）。

- `-u`, `--keep-utf16` 保留输入文件的原始 UTF-16 编码。输出文件将以相同的 UTF-16 编码（小端或大端）写入。这防止了转换为 UTF-8。将正确写入 UTF-16 BOM。可以使用 `-ascii` 标记禁用此选项。

- `-ul`, `--assume-utf1le` 假设输入文件格式为 UTF-1LE。

当输入文件中存在顺序标记时，BOM 的优先级高于此选项。

当你做了一个错误的假设（输入文件并非 UTF-1LE 格式）且转换成功时，你将得到一个文本错误的 UTF-8 输出文件。可以通过 `iconv()` 将 UTF-8 输出文件转换回 UTF-16LE 来撤销错误的转换。这将恢复原始文件。

UTF-16LE 的假设作为一种*转换模式*工作。通过切换到默认的*ascii模式*，UTF-16LE 假设会被关闭。

- `-ub`, `--assume-utf16be` 假设输入文件格式为 UTF-16BE。

此选项的作用与选项 `-u1` 相同。

- `-v`, `--verbose` 显示详细信息。显示关于字节标记和转换换行符数量的额外信息。

- `-F`, `--follow-symlink` 跟踪符号链接并转换目标。

- `-R`, `--replace-symlink` 将符号链接替换为转换后的文件（原始目标文件不变）。

- `-S`, `--skip-symlink` 保持符号链接和目标不变（默认）。

- `-V`, `--version` 显示版本信息并退出。

# MAC模式

在普通模式下，换行符从 DOS 转换为 Unix 反之亦然。Mac 换行符不转换。



在 Mac 模式下，换行符从 Mac 转换为 Unix 反之亦然。DOS 换行符不改变。

要在 Mac 模式下运行，请使用命令行选项 `-c mac` 或使用命令 `mac2unix` 或 `unix2mac`。

# 转换模式

## ascii

在模式下仅转换换行符。这是位转换模式。

尽管此模式名为 ASCII（7 位标准），但实际模式是 8 位的。转换 Unicode UTF-8 文件时请始终使用此模式。

## 7bit

在此模式下，所有 8 位非 ASCII 字符（值从 128 到 255）均被转换为 7 位空间。

## iso

字符在 DOS 字符集（代码页）和 Unix 上的 ISO 字符集 ISO-8859-1 (Latin-1) 之间转换。没有 ISO-8859-1 等效项的 DOS 字符（无法转换）将被转换为点。没有 DOS 对应的 ISO-8859-1 字符同样如此。

当仅使用选项 `-iso` 时，`dosunix` 将尝试确定活动页面。如果无法确定，`dosunix` 将使用默认代码页 `CP437`（主要用于美国）。要强制指定代码页，请使用选项 `-437`（美国）、`-850`（西欧）、`-860`（葡萄牙）、`-863`（法语加拿大）或 `-865`（北欧）。选项 `-1252` 支持 Windows 代码页 `CP1252`。

一些示例：

从 DOS 默认页转换为 Unix:

```bash
dosunix -iso file.txt
```

从 `CP850` 转换为 Unix:

```bash
dosunix -850 file.txt
```

从 `CP1252` 转换为 Unix:

```bash
dosunix -1252 file.txt
```

从 Unix 默认页转换为 DOS:

```bash
unixdos -iso file.txt
```

从 Unix `CP850` 转换为 DOS:

```bash
unixdos -850 file.txt
```

从 Unix `CP1252` 转换为 DOS:

```bash
unixdos -1252 file.txt
```

`Dos2unix` 默认在输出文件中不写入 BOM。使用选项 `-b` 时，如果输入文件包含 BOM，`Dos2unix` 会写入 BOM。

当输入文件包含 BOM 时，`Unix2dos` 默认会在输出文件中写入 BOM。使用选项 `-r` 可以移除 BOM。

当使用选项 `-m` 句用时，`Dos2unix` 和 `unix2dos` 总是会写入 BOM。

# Unicode 示例

将 Windows UTF-16（带 BOM）转换为 Unix UTF-8:

```
dos2unix -n in.txt out.txt
```

将 Windows UTF-16LE（不带 BOM）转换为 Unix UTF-8:

```
dos2unix -ul -n in.txt out.txt
```

将 Unix UTF-8 转换为带 BOM 的 Windows UTF-8:

```
unix2dos -m -n in.txt out.txt
```

将 Unix UTF-8 转换为 Windows UTF-16:

```
unix2dos < in.txt | iconv -f UTF-8 -t UTF-16 > out.txt
```

# GB18030

`GB18030` 是中国政府标准。`GB18030` 标准的一个强制性子集在中国销售的所有软件产品中官方要求的。另见 <http://en.wikipedia.org/wiki/GB_18030>。

`GB18030` 与 Unicode 完全兼容，可以视为一种 Unicode 转换格式。与 UTF-8 一，`GB18030` 与 ASCII 兼容。`GB18030` 也兼容 Windows 代码页 `936`（也称为 `GBK`）。

在 Unix/Linux 上，当 locale 编码被设置为 `GB18030` 时，UTF-16 文件会被转换为 `GB18030`。注意，只有当系统支持该 locale 时此操作才有效。使用命令 `locale -a` 获取支持的 locale 列表。

在 Windows 上，你需要使用选项 `-gb` 将 UTF-16 文件转换为 `GB18030`。

`GB18030` 编码的文件可以像 Unicode 文件一样包含一个字节顺序标记（BOM）。

## 示例

从 `stdin` 读取输入并将输出写入 `stdout`：

`d2unix dos2unix -l -c mac`

转换并替换 `a.txt`。规避并替换 `b.txt`：

`d2unix a.txt b.txt dos2unix -o a.txt b.txt`

在 `ascii` 转换模式下转换并替换 `a.txt`：

`d2unix a.txt`

在 `ascii` 转换模式下转换并替换 `a.txt`，在 `7bit` 转换模式下转换并替换 `b.txt`：

`d2unix a.txt -c 7bit b.txt dos2unix -c ascii a.txt -c 7bit b.txt dos2unix -ascii a.txt -7 b.txt`

将 `a.txt` 从 Mac 转换为 Unix 格式：

`d2unix -c mac a.txt mac2unix a.txt`

将 `a.txt` 从 Unix 转换为 Mac 格式：

`unix2dos -c mac a.txt unix2mac a.txt`

保留原始时间戳的同时转换并替换 `a.txt`：

`d2unix -k a.txt dos2unix -o a.txt`

转换 `a.txt` 并写入 `e.txt`：

`d2unix -n a.txt e.txt`

转换 `a.txt` 并写入 `e.txt`，保持 `e.txt` 的时间戳与 `a.txt` 相同：

`d2unix -k -n a.txt e.txt`

转换并替换 `a.txt`，转换 `b.txt` 并写入 `e.txt`：

`d2unix a.txt -n b.txt e.txt dos2unix -o a.txt -n b.txt e.txt`

转换 `c.txt` 并写入 `e.txt`，转换并替换 `a.txt`，转换并替换 `b.txt`，

转换 `d.txt` 并写入 `f.txt`：

`dos2unix -n c.txt e.txt -o a.txt b.txt -n d.txt f.txt`

# 递归转换

将 `dos2unix` 结合 `find(1)` 和 `xargs(1)` 命令用于递归转换目录树结构中的文本文件。例如，要转换当前目录树下的所有 `.txt` 文件，输入：

```
find . -name *.txt |xargs dos2unix
```

# 本地化

# LANG

主语言通过环境变量 `LANG` 选择。`LANG` 变量由几个部分组成。第一部分是小写的语言代码。第二部分是可选的，是大写的国家代码，前面有一个下划线。还可选可选的第三部分：字符编码，前面有一个点。posix 标准类型的几个示例：

```
export LANG=n1 Dutch export LANG=n1_NL Dutch, The Netherlands export LANG=n1_be Dutch, Belgium export LANG=es_ES Spanish, Spain export LANG=es_MX Spanish, Mexico export LANG=en_US.iso88591 English, USA, Latin-1 encoding export=en_GB.UTF-8 English, UK, UTF-8 encoding
```

语言和国家代码的完整列表请参 `gettext` 手册：<http://www.gnu.org/software/gettext/manual/html_node/Usual-Language-Codes.html>

在 Unix 系统上，你可以使用命令 `locale(1)` 获取特定 locale 的信息。

# LANGUAGE

通过 `LANGUAGE` 环境变量，你可以指定一个语言优先级列表，用冒号分隔。`Dos2unix` 对 `LANGUAGE` 的优先级高于 `LANG`。例如，首先使用荷兰语，然后是德语：`LANGUAGE=n1:de`。你必须通过将 `LANG`（或 `LC_ALL`）设置为除“C”以外的值来启用本地化。

### 描述

`dsa` - 处理 DSA 密钥。

# 语法

`openssl dsa [-inform PEM|DER] [-outform PEM|DER] [-in filename] [-passin arg] [-out filename] [-passout arg] [-aes128|aes256|camellia128|camellia192|camellia256|des|des3|idea] [-text] [-noout] [-modulus]`

### 描述

`**dsa**` 命令处理密钥。它们可以在各种格式之间转换并打印组件。

### 命令选项

`-inform PEM|DER`

指定输入格式。对于私钥，该选项使用 DER 编码的 ASN.1 序列。

`-outform PEM|DER`



指定输出格式，其含义与 `-inform` 选项相同。默认格式为 PEM；它包含额外的头部和尾部行。对于私钥，也接受 PKCS#8 格式。

`-in filename`

指定从文件读取密钥，未指定此选项则从标准输入读取。如果密钥是加密的，将提示密码。

`-passin arg`

输入文件密码。关于 `arg` 格式的更多信息请参见 `openssl(1)` 中的 `PASSRASE` 部分。

`-out filename`

指定写入密钥的文件名，未指定此选项则写入标准输出。如果设置了任何加密选项，将提示密码。输出文件名不应与输入文件名相同。

`-passout arg`

输出文件密码。关于 `arg` 格式的更多信息请参见 `openssl(1)` 中的 `PASSRASE` 部分。

`-aes128`|`-aes256`|`-camellia128`|`-camellia192`|`-camellia256`|`-des`|`-des3`|`-idea`

这些选项在输出之前使用指定的加密算法对私钥进行加密。将提示密码。如果未指定其中任何一个，密钥将以明文形式写入。这意味着使用 `dsa` 工具读取加密密钥且不带加密选项可以用来移除密钥的密码，或者通过设置加密选项可以添加或更改密码。这些选项只能与 PEM 输出格式一起使用。

`-text`

打印公钥、私钥组件和参数。

`-noout`

此选项防止输出编码后的密钥。

`-modulus`

此选项打印密钥中公钥组件的值。

`-pubin`

默认情况下从输入文件读取私钥：使用此选项时读取公钥。

# 返回值

成功时返回 `0`。发生错误时返回系统错误。

# 标准

<http://en.wikipedia.org/wiki/BOM>

<http://en.wikipedia.org/wiki/Newline>

<http://en.wikipedia.org/wiki/Text>

### 作者

`Benjamin Lin`, `Johannes W`, `Christian Wurll`, `Erwin Waterlander` - 维护 `maintainer`

# 项目页面

<http://sourceforge.org/projects/dos2unix/>

### 参见

`file(1)` `find(1)` `iconv(1)` `locale(1)` `xargs(1)`

默认情况下会输出私钥。使用此选项将改为输出公钥。如果输入的是公钥，则此选项会被设置。

`-engine id`

指定一个引擎（通过其唯一 `id` 字符串）将导致 `dsa` 尝试获取指定引擎的功能引用，从而在需要时对其进行初始化。然后，该引擎将设置为所有可用算法的默认引擎。

# 注意

PEM 私钥格式使用头部和页脚行：

```
-----BEGIN DSA PRIVATE KEY-----
END DSA PRIVATE KEY-----
```

PEM 公钥格式使用头部和页脚行：

```
-----BEGIN PUBLIC KEY-----
END PUBLIC KEY-----
```

## 示例

移除 DSA 私钥上的密码短：`\openssl dsa -in key.pem -out keyout.pem`

使用三重 DES 加私钥：`\openssl dsa -in key.pem -des3 -out keyout.pem`

将私钥从 PEM 格式转换为 DER 格式：`\openssl dsa -in key.pem -outform DER -out keyout.der`

将私钥的组件打印到标准输出：`\openssl dsa -in key.pem -text -noout`

仅输出私钥的公部：`\openssl dsa -in key.pem -pubout pubkey.pem`

### 参见

`dsaparam(1)`, `gendsa(1)`, `rsa(1)`, `genrsa(1)`

`dsaparam` - DSA 参数处理与生成

```
openssl dsaparam [-inform DER|PEM] [-outform DER|PEM] [-in filename] [-out filename] [-noout] [-text] [-C] [-rand file(s)] [-genkey] [-engine id] [numbits]
```

### 描述

此命令用于处理或生成 DSA 参数文件。

### 选项

`-inform DER|PEM`

指定输入格式。该选项使用兼容 RFC2459 `PKIX` DSS-Parms 的 DER1 编码 DER 形式，其是一个由 `p`、`q` 和 `g` 组成的 SEQUENCE。PEM 格式是默认格式：它由 DER 格式经过 base64 编码，并带有额外的头部和页脚行。

`-outform DER|PEM`

指定输出格式，这些选项与 `-inform` 选项含义相同。

`-in filename`

指定要读取参数的输入文件名，如果未指定此选项，则使用标准输入。如果包含了 `numbits` 参数，则此选项将被忽略。

`-out filename`

指定参数输出的文件名。如果不存在此选项，则使用标准输出。输出文件名不应与输入文件名相同。

`-nout`

此选项抑制参数的编码版本的输出。

`-text`

此选项以人类可读的形式打印 DSA 参数。

`-C`

此选项将参数转换为 C 代码。然后可以通过调用 `get_dsaXXX()` 函数加载这些参数。

`-genkey`

此选项将使用指定的或生成的参数生成 DSA。

`-rand file(s)`

包含随机数据的文件或文件，用于初始化随机数生成器，或一个 EGD 套接（见 `RAND_egd(3)`）。多个文件可以使用依赖于系统的字符分隔。MS-Windows、VMS 使用 `;` 分隔，其他系统使用 `:` 分隔。

`numbits`

此选项指定生成大小为 `numbits` 的参数集。它必须是最后一个选项。如果包含此选项，则忽略输入文件（如果有的话）。

`-engine id`

指定一个引擎（通过其唯一 `id` 字符串）将导致 `dsaparam` 尝试获取指定引擎的功能引用，从而在需要时对其进行初始化。然后，该引擎将设置为所有可用算法的默认引擎。

# 注意

PEM 格式 DSA 参数使用头部和页脚行：

```
-----BEGIN DSA PARAMETERS-----
END DSA PARAMETERS-----
```

DSA 参数生成是一个缓慢的过程，因此通常使用同一组 DSA 参数生成多个不同的密钥。

### 参见

`gendsa(1)`, `dsa(1)`, `genrsa(1)`, `rsa(1)`

`dgst`, `sha`, `sha1`, `mdc2`, `ripemd160`, `sha224`, `sha256`, `sha384`, `sha512`, `md2`, `md4`, `md5`, `dss1` 消息摘要

# 语法

```
openssl dgst [-sha1|-mdc2|-ripemd160|-sha224|-sha256|-sha384|-sha512|-md2|-md4|-md5-dss1] [-c] [-d] [-hex] [-binary] [-r] [-hmac arg] [-non-fips-allow] [-out filename] [-sign filename] [-keyform arg] [-passin arg] [-verify filename] [-prverify filename] [-signature filename] [-hmac key] [-non-fips-allow] [-fips-fingerprint file...]

openssl [digest] [...]
```

### 描述

摘要函数以十六进制格式输出提供的文件或文件的消息摘要。

摘要函数还使用消息摘要生成并验证数字签名。

### 选项

`-c`

以冒号分隔的两位位一组的形式打印摘要，仅在使用了 `hex` 格式输出时有效。

`-d`

打印 BIO 调试信息。

`-hex`

摘要将以十六进制转储的形式输出。这是“正常”摘要（相对于数字签名）的默认情况。使用 `-hex` 的数字签名请参见下文的注意。

`-binary`

以二进制形式输出摘要或签名。使用 `sha1sum` 等程序使用的“coreutils”格式。

`-hmac arg`

设置 HMAC 密钥。

`-non-fips-allow`

在 FIPS 模式下允许使用非 FIPS 算法。

`-out filename`

输出摘要的文件名。

`-sign filename`

使用私钥签名。

`-keyform arg`

密钥格式。

`-passin arg`

密码输入参数。

`-verify filename`

验证签名。

`-prverify filename`

验证签名。

`-signature filename`

要验证的签名。

`-hmac key`

HMAC 密钥。

`-fips-fingerprint file...`

为某些 OpenSSL-FIPS 操作计算 HMAC 指纹。

`-engine id`

指定引擎（通过其唯一 `id` 字符串）将导致 尝试获取指定引擎的功能引用，从而在需要时对其进行初始化。对于签名算法，使用 `engine id` 指定私密钥源。

`-sigopt nm`

在签名或验证时传递给算法的选项。

`-passin arg`



私钥密码。

`-verify` `filename`

使用公钥验证签名。输出为“Verification OK”或“Verification Failure”。

`-mac` `filename`

mac签名。

通过 `-mac` 传递选项。

`key:string`

以字符串形式指定 MAC 密钥（如果密钥包含打印字符）。字符串长度必须符合算法的任何限制。

`hexkey:string`

以十六进制格式指定 MAC 密钥（每字节两个十六进制位）。密钥长度必须符合算法的任何限制。

`-rand` `file(s)`

包含随机数据的文件或文件，用于初始化随机数生成器，或一个 EGD 套接（见 `RAND_egd(3)`）。多个文件可以使用依赖于系统的字符分隔。MS-Windows、VMS 使用 `;` 分隔，其他系统使用 `:` 分隔。

`-non-fips-allow`

在 FIPS 模式下允许使用非 FIPS 算法。

`-fips-fingerprint`

使用特定密钥计算 HMAC。

`file...`

要摘要的文件或文件。如果没有指定任何文件，则使用标准输入。

## 示例

创建文件的十六进制编码消息摘要：`openssl dgst -md5 -hex file.txt`

使用 SHA-256 签名文件并输出二进制文件：`openssl dgst -sha256 - sign privatekey.pem -out signature.sign file.txt`

验证签名：`openssl dgst -sha256 -verify publickey.pem \ - signature signature.sign \ file.txt`

# 注意

所有新应用程序的摘要选择是 SHA1。然而，其他摘要仍被广泛使用。

## 名称

`du` - 估计文件空间占用情况

# 语法概要

```
du [OPTION]... [FILE]... du [OPTION]... --files0-from=F
```

### 描述

汇总一组 `FILE` 的磁盘使用情况，对于目录则进行递归处理。

长选项的强制性参数对于短选项也是强制性的。

+   `-0`, `--null`

    以 NUL 结束每行输出，而不是换行符

- `-a`, `--all`

    为所有文件写入计数，而不仅仅是目录

- `--apparent-size`

    打印表义大小，而不是磁盘占用情况；虽然表义大小通常较小，但它可能比（“稀疏”）文件中的空洞、内部碎片、间接块等要大

- `-B,--block-size=SIZE`

    在打印大小前按 `SIZE` 缩放大小；例如，‘BM’ 以 1,048,576 字节为单位打印大小；见下文的 `SIZE` 格式

- `-b,--bytes`

    等同于 ‘apparent-size --block-size=1’

- `-c,--total`

    生成总计

- `-D`, `--dereference-args`

    仅对命令行中列出的符号链接进行解引用

- `-d,--max-depth=N`

    仅当目录（或文件，配合 `--all`）位于命令行下方 `N` 级以下时，打印其总计；`--max-depth=0` 等同于 `--summarize`

- `--files0=F`

    汇总 `F` 中指定的 NUL 终止的文件名的磁盘使用情况；如果 `F` 为 `-`，则从标准输入读取名称

- `-H`

    等同于 `--dereference-args (-D)`

- `-h`, `--human-readable`

    以人类可读的格式打印大小（例如 1K 234M 2G）

- `--inodes`

    列出 inode 使用信息而不是块使用情况

- `-k`

    同于 `--block-size=1K`

- `-L`, `--dereference`

    解引用所有的符号链接

- `-l`, `--count`

    如果是硬链接，则多次计数大小

- `-m`

    同于 `--block-size=1M`

- `-P`, `--no-dereference`

    不跟随任何符号链接（这是默认设置）

+   `-S`, `--separate-dirs`

    对于目录，不包含子目录的大小

+   `-si`

    类似 `-h`，但使用 1000 的幂次而不是 1024

+   `-s`, `--summarize`

    仅为每个参数显示总计

+   `-t`, `--threshold=SIZE`

    如果是正数，则排除小于 `SIZE` 的条目；如果是负数，则排除大于 `SIZE` 的条目

+   `-time`

    显示目录或任何子目录中任何文件的最后修改时间

+   `-time=WORD`

    用 `WORD` 显示时间而不是修改时间：`atime`（访问）、`use`、`ctime` 或 `status`（状态）

+   `-time-style=STYLE`

    使用 `STYLE` 显示时间，`STYLE` 可以是：`full-iso`, `long-iso`, `iso`, 或 `+FORMAT`；

    `FORMAT` 的解释方式类似于 ‘`date`’ 

+   `-X`, `--exclude-from=FILE`

    排除匹配 `FILE` 中任何模式的文件

+   `-exclude=PATTERN`

    排除匹配 `PATTERN` 的文件

+   `-x`, `--one-file-system`

    跳过不同文件系统上的目录

+   `-help`

    显示此帮助并退出

+   `-version`

    输出版本信息并退出

显示的值以第一个可用 `SIZE -block-size` 为单位，并由 `DU_BLOCK_SIZE`、`BLOCK_SIZE` 和 `BLOCKSIZE` 环境变量决定。否则，单位默认为 1024 字节（如果设置了 `POSIXLY_CORRECT` 则为 512）。

`SIZE` 参数是一个整数和一个可选单位（例如：`10K` 是 `10*1024`）。单位有 `K,M,G,T,P,E,Z,Y`（1024 的幂次）或 `KB,MB,...`（1000 的幂次）。

# 模式

`PATTERN` 是一个 shell 模式（不是正则表达式）。模式 `?` 匹配任何字符，而 `*` 匹配任何字符串（由零、一个或多个字符组成）。例如，`*.o` 将匹配任何以 `.o` 结尾的文件。因此，命令

```
du --exclude='*.o'
```

将跳过所有以 `.o` 结尾的文件和子目录（包括文件 `.o` 本身）。

### 作者

由 Torbjorn Granlund, David MacKenzie, Paul Eggert 和 Jim Meyerering 编写。

# 报告

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 向 <http://translationproject.org/team/> 反馈 `du` 翻译错误。

# 版权

Copyright © 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL 3 或更高版本 <http://gnu.org/licenses/gpl.html>。这是免费软件：你可以自由地更改和重新发行它。在法律允许范围内不提供任何保证。

# 另请

完整文档见：<http://www.gnu.org/software/coreutils/du> 或通过本地可用：info ‘(coreutils) du invocation’

## 名称

`dumpiso` - 倾储 IEEE 1394 同步通道数据包

# 语法概要

```
dumppiso [ options ] [ FILE ]
```

### 描述

`dumpiso` 监听选定的通道范围并将所有接收的数据包转储到文件 `FILE`，如果没有给出，则转储到标准输出。在转储过程中，接收到的数据包当前数量写入标准错误，并在每个数据包更新时更新。

它使用简单的文件格式用于 `dumpiso` 监听选定的通道范围并将所有接收的数据包转储到文件 `FILE`，如果没有给出，则转储到标准输出。在转储过程中，接收到的数据包当前数量写入标准错误，并在每个数据包更新时更新。它使用简单的文件格式 `isodump(5)`。

### 选项

`-c`, `--channels=CHANNELS`

    设置监听的通道。`CHANNELS` 可以是单个数字，或者是 `X-Y` 形式的范围。`-p`, `--port=PORT`

    选择接收端口。端口范围为 0 到 63。`-h`, `--help`

    显示帮助并退出。这种格式见 `isodump(1)`。

# 错误

无。

# 另请

`sendiso(1)`, `isodump(5)`

### 作者

Andreas Bombe <a@debian.org>

## 名称

`dvcont` - 向 DV 发送命令

# 语法概要

```
dvcont <command1> [ <command2> ]
```

### 描述

`dvcont` 是一个通过火线电发送命令的命令行工具。以下是命令：`dev <number>`

    选择使用的设备号。（`dvcont` 会尝试自动检测相机。）`play`

    让相机播放。如果已经在播放，则切换慢动作。`reverse`



让相机以反向播放。如果已经在播放，则切换慢动作。`trickplay < -14 to14>`

让相机以各种速度播放。`0` = 正向播放,`-14` = 最快反向，`-8` = 倍速反向,`-1` = 最慢反向，`1` = 最慢正向，`8` = 倍速正向，`14` = 最快正向。（并非所有相机都支持。）`stop`

让相机停止。`rewind`

让相机倒带（在停止或播放模式下）。`ff`

让相机快进（在停止或播放模式下）。`pause`

让相机切换暂停/播放。`next`

让相机跳转到下一帧（在暂停或模式下）。`nextindex`

让相机搜索下一个场景（在暂停或播放模式下）。`prev`

让相机跳转到上一帧（在暂停模式下）。`previousindex`

让相机搜索上一个场景（在暂停或播放模式下）。`record`

让相机录制。（请谨慎使用！）`eject`

让相机吐出磁带。（并非所有相机都支持。）`timecode`

报告磁带上的时间码，格式为 HH:MM:SS:FF（时、分、秒、帧帧）。`seek <timecode>`

让相机跳转到时间码，格式如上述 HH:MM:SS:FF。`status`

报告设备状态。

# 插件信息

报告可用的插件。

# 详细

让程序显示调试信息。

# 版本

让程序显示程序版本。

# 帮助

让程序显示帮助屏幕。

### 作者

`dvcont` 由 Jason Howard <jason@spectsoft.com> 和 Dan Dennedy <dan@dennedy.org> 编写。此帮助页是在 Daniel Kobras <kobras@debian.org> 的帮助下为 Debian GNU/Linux 发行版编写（但供其他人使用）。由 Dan Dennedy <dan@dennedy.org> 更新。

## 名称

`dvipdf` - 使用 `ghostscript` 和 `dvips` 将 TeX DVI 文件转换为 PDF

### 摘要

```
dvipdf [ options ] input.dvi [ output.pdf ] ...
```

### 描述

此脚本带有 `-q` 选项调用 `dvips(1)`，并将其输出通过以下选项传递给 `gs(1)`：

```
-q -dNOPAUSE -dBATCH -sDEVICE=pdfwrite
```

以及 `-sOutputFile` 和命令行中的任何选项。

# 另请

`gs(1)`, `dvips(1)`

# 版本

此文档最后针对 Ghostscript 版本 9.16 进行修订。

### 作者

Artifex Software, Inc. 是 Ghostscript 的主要维护者。本手册由 George Ferguson 编写。

## 名称

`ec` - EC 密钥处理

### 摘要

```
openssl ec [-inform PEM|DER] [-outform PEM|DER] [-in filename] [-passin arg] [-out filename] [-passout arg] [-des] [-des3] [-idea] [-text] [-noout] [-param_out] [-pubin] [-pubout] [-conv_form arg] [-param_enc arg] [-engine id]
```

### 描述

`ec` 命令处理 EC 密钥。它们可以在各种形式之间进行转换并打印其组件。**注意** OpenSSL 使用“SEC 1: 椭圆曲线密码学”（http://www.secg.org/）中指定的私钥格式。要将 OpenSSL EC 私钥转换为 PKCS#8 私钥格式，请使用 `pkcs8` 命令。

### 命令选项

`-inform DER|PEM`

这指定输入格式。带有私钥的选项使用 ASN.1 DER 编码的 SEC1 私钥。当与公钥配合使用时，它使用 RFC 3280 中指定的 SubjectPublicKeyInfo 结构。PEM 格式是默认格式：它由 DER 格式经过 base64 编码，并带有额外的头部和页脚行。对于私钥，也接受 PKCS#8 格式。

`-out DER|PEM`

这指定输出格式，这些选项的含义与 `-inform` 相同。

`-in filename`

这指定读取密钥的输入文件名，如果未指定此选项则使用标准输入。如果密钥已加密，将提示输入密码。

`-pass arg`

文件密码源。有关 arg 格式的更多信息，请参见 `openssl(1)` 中的 PASS PHRASE ARGUMENTS 部分。

`-out`

这指定写入密钥的输出文件名，如果没有指定则使用标准输出。如果设置了任何加密选项，将提示输入密码。输出文件名不应与输入文件名相同。

`-passout`

文件密码源。有关 arg 格式的更多信息，请参见 `openssl(1)` 中的 PASS PHRASE ARGUMENTS 部分。

`-des-3|-idea`

这些选项在输出私钥之前使用 DES、三 DES、IDEA 或 OpenSSL 支持的任何其他算法对其进行加密。将提示输入密码。如果没有指定这些选项之一，密钥将以明文写入。这意味着使用 `ec` 工具读取不带加密选项的加密密钥可以移除密钥中的密码，或者通过设置加密选项来添加或更改密码。这些选项仅可与 PEM 格式的文件一起。

`-text`

打印公钥、私钥组件和参数。

`-noout`

此选项防止输出密钥的编码版本。

`-pubin`

默认情况下从输入文件读取私钥：使用此选项将改为读取公钥。

`-pubout`

默认输出私钥。使用此选项将输出公钥。如果输入是公钥，则会自动设置此选项。

`-conv_form`

这指定如何将椭圆曲线上的点转换为字节串。

可能的值为 `compressed`（默认值）、`uncompressed`（未压缩）和 `hybrid`（混合）。有关点转换形式的更多信息，请阅读 X.62 标准。**注意**由于专利问题，二进制曲线默认禁用了 `compressed` 选项，可以通过编译时定义预处理器宏 `OPENSSL_EC_BIN_PT_COMP` 来启用。

## `-param_enc arg`

这指定如何编码椭圆曲线参数。可能的值为：`named_curve`，即 EC 参数通过 OID 指定；或 `explicit`，其中 EC 参数被显式给出（EC 参数结构的定义请参见 RFC 3279）。默认值是 `named_curve`。注意，RFC 3279 中指定的 `implicitlyCA` 替代方案目前在 OpenSSL 中尚未实现。

## `-engine id`

指定一个引擎（通过其唯一的 `id string`）将使 `ec` 尝试获取指定引擎的函数引用，从而在需要时初始化它。该引擎将设置为所有可用算法的默认引擎。

# 注意

PEM 私钥格式使用头部和页脚行：

```
-----BEGIN EC PRIVATE KEY-----
END EC PRIVATE KEY-----
```

PEM 公钥格式使用头部和页脚行：

```
-----BEGIN PUBLIC KEY-----
END PUBLIC KEY-----
```

## 示例

使用三 DES 加密私钥：

```
openssl ec -in key.pem -des3 -out keyout.pem
```

将私钥从 PEM 转换为 DER 格式：

```
openssl ec -in key.pem -outform DER -out keyout.der
```

将私钥的组件打印到标准输出：

```
openssl ec -in key.pem -text -nout
```

仅输出私钥的公钥部分：

```
openssl ec -in key.pem -pubout -out pubkey.pem
```

将参数编码更改为 `explicit:`：

```
openssl ec -in key.pem -param_enc explicit -out keyout.pem
```

将点转换形式更改为 `compressed:`：

```
openssl ec -in key.pem -conv_form compressed -out keyout.pem
```

# 另请

`ecparam(1)`, `dsa(1)`

# 历史

`ec` 命令首次引入于 OpenSSL 9.8。

### 作者

Nils Larsch 为 OpenSSL 项目贡献（http://www.openssl.org/）。

## 名称

`echo` - 显示一行文本

### 摘要

```
echo [SHORT-OPTION] [STRING]... echo LONG-OPTION
```

### 描述

将 STRING(s) Echo 到标准输出。

- `-n`

不输出末尾换行符

- `-e`

启用反斜杠转义解释

- `-E`

禁用反斜杠转义解释（默认）

- `--help`

显示此帮助并退出

- `--version`

输出版本信息并退出

如果 `-e` 生效，将识别以下序列：

- `\a` 警报 (BEL)



- `\b` 退格格
- `\c` 不产生输出
- `\e` 转义键
- `\f` 换页
- `\n` 换行
- `\r` 回车
- `\t` 水平制表符
- `\v` 垂直制表符
- `\NNN` 十八进制值为 `NNN` 的字节（1 到 3 位）
- `\xHH` 十六进制值为 `HH` 的字节（1 到 2 位）

![](img/9e4ee58043860d21149562b68ac7238_1825.png)

注意：您的 shell 可能有自己版本的 `echo`，它通常会优于此处描述的版本。请参考您的 shell 文档以了解其支持的选项。

### 作者

由 Brian Fox 和 Chet Ramey 编写。

# 报告错误

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 向 <http://translationproject.org/team/> 报告 `echo` 翻译错误。

# 版权

版权 © 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL 3 或更高 <http://gnu.org/licenses/gpl.html>。这是免费软件：您可以更改和重新分发它。法律允许范围内不保证。

# 另请

完整文档见：<http://www.gnu.org/software/coreutils/echo> 或通过本地信息可用：info ‘(coreutils) echo invocation’

## 名称

`ecparam` - EC 参数处理和生成

### 描述

此命令用于处理或生成 EC 参数文件。

### 选项

`-inform DER|PEM`

指定输入格式。该选项使用指定的 ASN.1 DER 编码形式，可与 RFC 3279 `EcpParameters` 兼容。`PEM` 是默认格式；它由 DER 格式经过 base64 编码，并带有额外的头部和页脚。

`-outform DER|PEM`

指定输出格式，这些选项的含义与 `-inform` 选项相同。

`-in filename`

指定用于读取参数的输入文件名，如果未指定此选项，则从标准输入读取。

`-out filename`

指定输出参数的文件名。如果不存在此选项，则使用标准输出。输出文件名不应与输入文件名相同。

`-noout`

抑制参数的编码版本的输出。

`-text`

此选项以人类可读的格式打印出 EC 参数。

`-C`

此选项将 `get_ec_group_XXX()` 函数转换的 EC 参数转换为 C 代码。可以通过调用以下函数加载这些参数：

`-check`

验证椭圆曲线参数。

`-name arg`

使用指定的“短”名称使用 EC 参数。使用 `list_curves` 获取所有已实现的 EC 参数列表。

`-list_curves`

如果指定了此项，`ecparam` 将打印所有已实现的 EC 参数列表并退出。

`-conv_form`

指定将椭圆曲线上的点转换为字节串。可能的值为：`compressed`（压缩，默认值）、`uncompressed`（未压缩）和 `hybrid`（混合）。有关点转换形式更多信息，请参阅 X.92 标准。注意：由于专利问题，二进制曲线的压缩选项默认是禁用的，可以通过在编译时定义预处理器宏 `OPENSSL_EC_BIN_PT_COMP` 来启用。

`-param_enc arg`

指定椭圆曲线参数的编码方式。可能的值为：`named_curve`（命名曲线），即通过 OID 指定 EC 参数；`explicit`（显式），即显式给出 EC 参数（EC 结构的定义参见 RFC 3279）。默认值为 `named_curve`。注意，RFC 3279 中指定的 `implicitlyCA` 备选项目前在 OpenSSL 中尚未实现。

`-no_seed` 此选项抑制用于参数生成的“种子（seed）”包含在 `ECParameters` 结构中（参见 RFC 3279）。

`-genkey`

此选项将使用指定的参数生成 EC 私钥。

`-rand file(s)`

包含用于为随机数生成器提供种子的随机数据的文件，或 EGD socket（参见 `RAND_egd(3)`）。可以指定多个文件并用依赖于系统的字符分隔。Windows 使用 `;`，OpenVMS 使用 `,`，其他所有系统使用 `:`。

`-engine id`

指定一个引擎（通过其唯一 ID 字符串）将导致 `ecparam` 尝试获取指定引擎的功能引用，从而在需要时对其初始化。该引擎将被设置为所有可用算法的默认引擎。

# 注意

PEM 格式的 EC 参数使用头部和页脚行：

```
-----BEGIN EC PARAMETERS-----
END EC PARAMETERS
```

OpenSSL 目前无法生成新组，因此 `ecparam` 只能从已知的（命名）曲线创建 EC 参数。

## 示例

创建一个组为 'prime192v1' 的 EC 参数：

```
openssl ecparam -out ec_param.pem -name prime192v1
```

创建一个具有显式参数的 EC 参数：

```
openssl ecparam -out ec_param.pem -name prime192v1 -param_enc explicit
```

验证给定的 EC 参数：

```
openssl ecparam -in ec_param.pem -check
```

创建一个 EC 参数和一个私钥：

```
openssl ecparam -out ec_key.pem -name prime192v1 -genkey
```

将点编码改为 'compressed'：

```
openssl ecparam -in ec_in.pem -out ec_out.pem -conv_form compressed
```

将 EC 参数打印到标准输出：

```
openssl ecparam -in ec_param.pem -noout -text
```

# 另请

`ec(1)`, `dsaparam(1)`

# 历史

`ecparam` 命令首次在 OpenSSL 0.9.8 中引入。

### 作者

Nils Larsch，来自 OpenSSL 项目 (http://www.openssl.org)

`edid-decode` - 以人类可读的格式解码 EDID 数据

### 概要

`edid-decode [in] [out]`

### 描述

`edid-decode` 以人类可读的格式解码 EDID 数据。它接受零、一个或两个参数。如果不带参数调用，它将从标准输入读取并写入标准输出。如果带一个参数，则读取参数命名的文件。如果带两个参数，则抑制普通输出，并将二进制 EDID 块写入第二个参数命名的文件中。

输入文件可以是原始二进制文件或 ASCII 文本。ASCII 输入会扫描十六进制转储（hex dumps），包含了启发式方法来搜索 `xrandr(1)` 属性输出和 `Xorg(1)` 日志文件格式中的十六进制转储，否则数据被视为原始十六进制转储。在支持内核模式设置（kernel modesetting）的现代现代 Linux 系统上，可以在 `/sys/class/drm*/edid` 找到连接的显示器的 EDID 块。

# 注意

并非所有字段都已解码，或已完全解码。某些字段的解码可能看起来损坏了输出（例如，详细字符串部分的内容按字面打印）。`edid-decode` 确实尝试根据相关标准验证输入，但其意见尚未经过相关标准机构的双重检查，因此它们可能是错误的。不要依赖输出格式，因为它可能会发生变化。

# 另请

`Xorg(1)`, `xrandr(1)`

# true

`edid-decode` 由 Adam Jackson 编写，Eric Anholt 和其他人有贡献。

## 名称

`edid-decode` 解码 EDID 数据。

### 概要

```
grep [OPTIONS] PATTERN [FILE...]
```

### 描述

`grep` 在文件中搜索包含模式的行。它接受零、一个或两个参数。如果不带参数，它将从标准输入读取。如果带一个参数，则读取参数命名的文件。如果带两个参数，则抑制普通输出，并将结果写入第二个参数命名的文件中。

输入文件可以是原始二进制文件或 ASCII 文本。ASCII 输入会扫描十六进制转储，包含了启发式方法来搜索 `xrandr(1)` 属性输出和 `Xorg(1)` 日志文件格式中的十六进制转储，否则数据被视为原始十六进制转储。

# 注意

在找到 `NUM` 行匹配后，`grep` 停止读取文件，无论是否存在尾随上下文。当 `grep` 在 `NUM` 行匹配后停止时，它会输出任何上下文。如果使用了 `-c` 或 `--count`，`grep` 不输出大于计数。

### 选项

# 通用程序信息

`-help`

输出用法信息并退出。

`-V`, `--version`

输出版本号并退出。

# 匹配选择

`-E`, `--extended-regexp`

将模式解释为扩展正则表达式（ERE），见下。

`-F`, `--fixed-strings`

将模式解释为固定字符串列表。如果是多个模式，按换行分隔。

`-G`, `--basic-regexp`



将模式解释为基本正则表达式（BRE），见下。

`-P`, `--perl-regexp`

将模式解释为 Perl 正则表达式。这是实验性的。

# 匹配控制

`-e PATTERN`, `--regexp=PATTERN`

指定模式。可以指定多个模式，用 `|` 分隔。

`-f FILE`, `--file=FILE`

从文件中获取模式，每行一个。如果文件是空的。

`-i`, `--ignore-case`

在模式和输入时不区分大小写。

`-v`, `--invert-match`

反转匹配方向，选择非匹配行。

`-w`, `--word-regexp`

仅选择形成单词的匹配。匹配字符串必须位于行首，或者前面是非单词字符。同样，必须位于行尾。单词字符是字母、数字和下划线。

`-x`, `--line-regexp`

仅选择精确匹配整行的模式。

`-y`

`-i` 的过时同义词。

# 普通输出控制

`-c`, `--count`

抑制普通输出，而是为每个输入文件打印匹配行的计数。配合 `-v`, `--invert=match`（见下），计算非匹配行。

`--color=[WHEN]`, `--colour=[WHEN]`

在终端中匹配字符串、匹配行、上下文、文件名、行号、偏移量和分隔符（字段和上下文组）周围使用转义序列显示颜色。颜色由环境变量 `GREP_COLORS` 定义。弃用的环境变量 `GREP_COLOR` 仍然支持，但其设置没有优先级。`WHEN` 是从、始终或自动。

`-L`, `--files-with-match`

抑制普通输出，而是打印没有输出的文件名。。扫描在第一次匹配项处停止。

`-i`, `--max-count=NUM`

抑制普通输出，而是打印通常会有输出的文件名。扫描在第一次匹配项处停止。

`-m NUM`, `--max-count=NUM`

在读取 `NUM` 行匹配后停止读取文件。如果输入是标准输入，并且找到了 `NUM` 行匹配，`grep` 确保标准输入在最后一条匹配行之后退出，无论是否存在尾随上下文。

`-o`, `--only-matching`

仅打印匹配行的（非空）部分，每个部分单独占一行。

`-q`, `--silent`

静默；不在标准输出写入任何内容。如果发现任何匹配，立即以零状态退出，即使检测到错误。另见 `-s` 或 `--no-messages` 选项。

`-s`, `--no-messages`

抑制关于不存在或不可读文件的错误信息。

# 输出行缀控制

`-b`, `--byte-offset`

在每行输出之前打印输入文件内从 0 开始的字节偏移量。如果指定了 `-0 (only-matching)`，则打印匹配部分本身的偏移量。

`-H`, `--filename`

为每个匹配项打印文件名。当有多个文件需要搜索时，这是默认选项。

`-h`, `--no-filename`

在输出时抑制文件名前缀。当只有一个文件（或标准输入）需要搜索时，这是默认选项。

`--label=LABEL`

将实际来自标准输入的输入显示为来自 `LABEL` 的输入。这在实现如 `zgrep` 等工具时特别有用，例如：`gzip -cd foo.gz` `grep --label=foo -H something`。另参见 `H` 选项。

`-n`, `--line-number`

在每行输出前加上其在输入文件中从 1 开始的行号。

`-T`, `--initial-tab`

确保实际行内容的第一个字符位于制表符之后，以便制表符对齐看起来正常。这对于在实际内容前添加输出前缀的选项（`-H,-n` 和 `-b`）非常有用。为了提高单个文件的行起始于同一列的概率，这还会导致行号和字节偏移量（如果存在）以最小字段宽度打印。

`-u`, `--unix-offsets`

报告 Unix 风格的字节偏移量。这使得 `grep` 报告字节偏移量就像文件是 Unix 风格文本文件一样，即去除了 CR 字符。这将产生与在 Unix 上运行 `grep` 相同的结果。除非同时使用了 `-b` 选项，否则此选项无效；它对 MS-DOS 和 MSWindows 以外的平台没有影响。

`-Z`, `--null`

输出零（ASCII NUL 字符）而不是通常紧随文件名后的字符。例如，`grep -Z` 在每个文件名后输出一个零而不是通常的换行符。此选项使得输出即使存在包含换行符等特殊字符的文件也不会歧义。此选项可以与 `find -print0`、`perl -0`、`sort -z` 和 `xargs -0` 等命令配合使用，处理包含换行符的任意文件名。

# 上下文行控制

`-A NUM`, `--after-context=NUM`

在匹配行之后打印 `NUM` 行尾部上下文。在连续的匹配组之间插入一行包含组分隔符（在 `--group-separator` 下描述）的行。使用 `-o` 或 `--only-matching` 选项时，此选项无效并会有警告。

`-B NUM`, `--before-context=NUM`

在匹配项之前打印 `NUM` 行头部上下文。在连续的匹配组之间插入一行包含组分隔符（在 `--group-separator` 下描述）的行。使用 `-o` 或 `--only-matching` 选项时，此选项无效并会有警告。

`-C NUM`, `--context=NUM`

打印 `NUM` 行输出上下文。在连续的匹配组之间插入一行包含组分隔符（在 `--group-separator` 下描述）的行。使用 `-o` 或 `--only-matching` 选项时，此选项无效并会有警告。

`--group-separator=SEP`

使用 `SEP` 作为组分隔符。默认情况下，`SEP` 为双连字符符（—）。

`--no-group-separator`

使用空字符串作为组分隔符。

# 文件和目录选择

`-a`, `--text`

将二进制文件视为文本处理；这等同于 `--binary-files=text` 选项。

`--binary-files=TYPE`

如果文件的前几个字节指示文件包含二进制数据，则假设该文件类型为 `TYPE`。默认情况下，`TYPE` 为 `binary`，`grep` 通常会输出单行消息表示二进制文件已匹配，或者在没有匹配项时不输出任何消息。如果 `TYPE` 为 `without-match`，`grep` 假设二进制文件是不匹配的；这等同于 `-I` 选项。它将二进制文件视为文本处理；这等同于 `-a` 选项。警告：`grep --binary-files=text` 可能会输出二进制垃圾，如果输出到终端且终端驱动程序将某些内容解释为命令，可能会产生严重的副作用。

`-D ACTION`, `--devices=ACTION`

如果输入是设备、FIFO 或套接字，则使用 `ACTION` 处理它。默认情况下，`ACTION` 为 `read`，意味着像读取普通文件一样读取设备。如果 `ACTION` 为 `skip`，则静跳过设备。

`-d ACTION`, `--directories=ACTION`

如果输入是目录，则使用 `ACTION` 处理它。默认情况下，`ACTION` 为 `read`，即像读取普通文件一样读取目录。如果 `ACTION` 为 `skip`，则递归地跳过目录，仅在它们出现在命令行时跟踪符号链接。这等同于 `-r` 选项。

`--exclude=GLOB`

跳过基名匹配 `GLOB` 的文件（使用通配符匹配）。文件名 `glob` 使用 `*`、`?` 和 `[...]` 作为通配符，并使用 `\` 字面转义通配符或反斜杠字符。

`--exclude-from=FILE`

跳过基名匹配从 `FILE` 读取的 `glob` 的文件（使用 `--exclude` 下描述的通配符匹配）。

`--exclude-dir=DIR`

在递归搜索中排除匹配模式 `DIR` 的目录。

`-I`

将二进制文件视为不包含匹配数据的处理；这等同于 `--include binary-files=without-match` 选项。

`--include=GLOB`

仅搜索基名匹配 `GLOB` 的文件（使用 `--exclude` 下描述的通配符匹配）。

`-r`, `--recursive`

递归读取每个目录下的所有文件，仅在符号链接出现在命令行时跟踪它们。这等同于 `-r` 选项。

`-R`, `--dereference`

递归读取每个目录下的所有文件，跟踪符号链接。

# 其他选项

`-U`, `--binary`

将二进制文件视为文本。基础和扩展模式没有区别。

`--line-buffered`

在输出时使用缓冲。

`-z`, `--data-zeros`

将输入视为空字符终止而非换行符终止。

`--text`

将二进制文件视为文本处理。

`--line-size`

将输入视为固定长度而非换行符终止。

`--line-number`

在每行输出前加上其在输入文件中从 1 开始的行号。

# 正则表达式

正则表达式是描述字符串集的模式。正则表达式通过各种运算符以类似的方式构建。`grep` 理解三种不同版本的语法：“基础（basic）”、“扩展（extended）”和“perl”。在 `grep` 中，基础和扩展的可用功能没有区别。Perl 正则表达式提供了额外功能，并记录在手册页中。



基础构建单元是匹配单个字符的正则表达式。大多数字符（包括所有字母和数字）匹配自身。具有特殊含义的元字符可以通过反斜杠进行转义。

点匹配任何单个字符。

# 字符类和括号表达式

括号表达式是封装在 `[]` 中的字符列表。它匹配列表中的任何单个字符；如果列表的第一个字符是脱字符 `^`，则匹配不在列表中的任何字符。例如，表达式 `[0123456789]` 匹配任意数字。

在括号表达式内部，范围表达式由由连字符分隔的两个字符组成。它根据区域的排序序列和字符集匹配两个字符之间的任何单个字符（包含边界）。例如，在默认 C 区域中，`[a-d]` 等同于 `[abcd]`。许多区域按字典顺序排序，在这些区域中 `[a-d]` 通常不等同于 `[abcd]`；它可能等同于 `[AaCcDd]`。为了获得括号表达式传统解释，可以通过将环境变量 `LC_ALL` 设置为 `C` 来使用 C 区域。

最后，命名字符类在括号表达式中预定义，名称自解释，它们是 `[alnum]: [alpha]: [cntrl]: [digit]: [graph]: [lower]: [print]: [punct]: [space]: [upper]: [:digit]`。例如，`[alnum:]` 匹配当前区域中的数字和字母类。在 C 区域和 ASCII 字符编码中，这等同于 `[0-9A-Za-z]`。（注意，这些类中的括号是符号名称的一部分，必须在边界括号表达式的括号之外包含。）大多数元字符在括号表达式内部失去特殊含义。要包含字面量 `]`，请将其放在列表中。同样，要包含字面量 `^`，请放在除第一个以外的位置。最后，要包含字面量 `-`，请放在最后。

脱字符 `^` 和美元符号 `$` 是元字符，分别匹配行开头和结尾的空字符串。

# 反斜线字符与特殊表达式

符号 `\<` 和 `\>` 分别匹配单词开头和结尾的空字符串。符号 `\b` 匹配单词边缘的空字符串，而 `\B` 在不在单词边缘时匹配空字符串。符号 `\w` 是 `[[:alnum:]]` 的同义词，`\W` 是 `[^[:alnum:]]` 的同义词。

# 重复

正则表达式后面可以跟几个重复操作符之一：

- `?` 前一个项目是可选的，最多匹配一次。
- `*` 前一个项目将匹配 0 次或多次。
- `+` 前一个项目将匹配一次或多次。
- `{n}` 前一个项目恰好匹配 `n` 次。
- `{n,}` 前一个项目将匹配 `n` 次或多次。
- `{m}` 前一个项目最多匹配 `m` 次。这是一个 GNU 扩展。
- `{n,m}` 前一个项目将匹配至少 `n` 次，但不超过 `m` 次。

# 拼接

两个正则表达式可以拼接；生成的正则表达式匹配由两个子字符串拼接成的任何字符串，这两个子字符串分别匹配拼接后的表达式。

# 择替

两个正则表达式可以通过中缀运算符 `|` 连接；生成的正则表达式匹配任何任一交替表达式的字符串。

# 优先级

重复的优先级高于拼接，而拼接的优先级高于交替。整个表达式可以用圆括号括起来以覆盖这些优先级规则并形成子表达式。

# 反引用与子表达式

反引用 `\n`（其中 `n` 是单个数字）匹配正则表达式中第 `n` 个括号子表达式之前匹配的子字符串。

# 基础与扩展正则表达式

在基础正则表达式中，元字符 `?`、`+`、`{`、`|`、`(` 和 `)` 失去它们的特殊含义；相反，请使用反斜杠版本 `\?`、`\+`、`\{`、`\|`、`\(` 和 `\)`。

## 环境变量

`grep` 的行为受以下环境变量的影响。

`LC_foo` 的区域通过按顺序检查三个环境变量 `LC_ALL`、`LC_foo`、`LANG` 来指定。这些变量中第一个设置的变量指定了区域。例如，如果未设置 `LC_ALL` 但其被设置为 `pt_BR`，则 `LC_MESSAGES` 类别使用葡萄牙语区域。如果这些环境变量都没有设置、区域目录未安装，或者 `grep` 在编译时没有启用自然语言支持 `NLS`，则使用 C 区域。

# GREP_OPTIONS

此变量指定位于任何显式选项之前的默认选项。这在编写可移植脚本时会产生问题，此功能将在 `grep` 的未来版本中移除，且 `grep` 在使用时会发出警告。请改用别名或脚本。

# GREP_COLOR

此变量指定用于高亮匹配的（非空）文本的颜色。它已被弃用并转而使用 `GREP_COLORS`，但仍然支持。`GREP_COLORS` 的 `mt`、`ms` 和 `mc` 功能优先级高于它。它只能指定用于高亮任何行中匹配非空文本的颜色（在省略 `-v` 命令行选项时为选定行，在指定 `-v` 时为上下文行）。默认是 `01;31`，这在终端的默认背景上显示粗体红色前景。

# GREP_COLORS

指定用于高亮输出不同部分的颜色和其他属性。其值为 `ms=01;31:mc=cx:fn=35:ln=32:bn=32:se=36`，省略了 `rv` 和 `ne` 布尔功能（即 `false`）。支持的功能如下：

- `sl=` 整个选定行的 SGR 子字符串（即在省略 `-v` 命令行选项时为匹配行，在指定 `-v` 时为非匹配行）。然而，如果同时指定了布尔 `rv` 功能和 `-v` 命令行选项，它将应用于上下文行。默认为空（即终端的默认颜色对）。
- `cx=` 上文行的 SGR 子字符串（即在省略 `-v` 命令行选项时为非匹配行，在指定 `-v` 时为匹配行）。然而，如果同时指定了布尔 `rv` 功能和 `-v` 命令行选项，它将应用于选定的非匹配行。默认为空（即终端的默认颜色对）。
- `rv` 布尔值，当指定 `-v` 命令行选项时会反转（交换）`sl=` 和 `cx=` 功能的含义。默认为 `false`（即省略该功能）。

# mt=01;31

任何匹配行中非空文本的 SGR 子字符串（即在省略 `-v` 命令行选项时为选定行，在指定 `-v` 时为上下文行）。设置此项等于同时将 `ms=` 和 `mc=` 设置为相同的值。默认是当前行背景上的粗体文本前景。

# ms=01;31

选定行中非空文本的 SGR 子字符串。（这仅在省略 `-v` 命令行选项时使用）。当此项生效时，`sl=`（或 `cx= rv`）的功能保持有效。默认是当前行背景上的粗体文本前景。

# mc=01;31

上下文行非空文本的 SGR 子字符串。（这仅在指定 `-v` 命令行选项时使用）。当此项生效时，`cx=`（如果 `rv` 则为 `sl=`）的功能保持有效。默认是当前行背景上的粗体文本前景。

# fn=35

前缀文件名的 SGR 子字符串。默认是终端背景上的洋色前景。

# ln=32

前缀行号的 SGR 子字符串。默认是终端背景上的绿色前景。

# bn=32

前缀字节偏移的 SGR 子字符串。默认是终端背景上的绿色前景。

# se=36

插入在选定字段之间（`:`）、上下文行之间（`-`）以及指定非零上下文时的相邻行之间（`—`）的分隔符的 SGR 子字符串。默认是终端默认背景上的青色前景。

# ne 布尔值

防止在每行结束时使用向右的 EL (`\33[K`) 来清除行尾。这对于不支持 EL 的终端是需要的。对于不适用 `back_color bce` 功能的终端非常有用。默认为 `false`（即省略该功能）。注意布尔功能作为字符属性没有意义。它们默认省略（即 `false`）。请参见所用终端文档中的选择渲染（SGR）部分获取允许的值。这些值是十进制表示的整数，可以用分号连接。常用值包括：`1` 粗体、`4` 下划线、`5` 闪烁、`7` 反转、`39` 默认前景色、`30` 到 `37` 前景色、`90` 到 `97` 16 色前景色、`38:0` 到 `38:255` 256 色模式、`49` 默认背景色、`40` 到 `47` 背景色、`100` 107 16 色背景色，以及 `48:0` 到 `48:255` 256 色模式背景色。

# 退出状态

通常情况下，如果选择了行，退出状态为 `0`；如果没有选择任何行，为 `1`；如果发生错误，则为 `2`。然而，如果使用了 `-q` 或 `--quiet` 或 `--silent` 且选择了行，即使发生了错误，退出状态也为 `0`。

# 版版权

Copyright 1998-2000, 2002, 2005-2014 Free Software Foundation, Inc.

这是免费软件；复制条件见源代码。不提供任何保证；即使对于商业用途或特定用途的适用性。

反向引用非常慢，可能需要指数级的时间。

应该可以让你访问完整的手册。

# 备注

此帮助页的维护并不频繁；完整的文档通常会有更新更新。

# EMPATHY-ACCOUNTS

`empathy-accounts` - Empathy 即时消息客户端的账户配置对话框

### 概要

`empathy-accounts [options]`

### 描述

Empathy 即时消息客户端的账户配置对话框

此工具允许你为 Empathy 配置即时消息账户。

### 选项

- `-h, --hidden`

  不显示任何对话；执行任何工作（例如，导入）并退出
- `-n, --if-needed`

  如果有非 salut 账户，则不显示任何对话
- `-s account-id`

  `--select-account=account-id` 初始选择给定的账户（例如 `gabble/jabber/foo_40example_2eorg`）

### 作者



本手册页由 Laurent Bigonville 为 Debian GNU/Linux 系统编写（但也供他人使用）。

# 另请

`empathy`(1), The Telepathy 项目 The Empathy 项目

## 名称

`empathy` - GNOME 多协议聊天和通话客户端

### 概要

`empathy`

### 描述

GNOME 多协议聊天和通话客户端。支持多种协议的文本、语音、视频、文件传输和应用程序间通信的即时消息程序，这些协议包括：AIM, MSN, Google Talk (Jabber/XMPP), Facebook, Yahoo!, Salut, Gadu-Gadu, Groupwise, ICQ 和 QQ。

主用户界面由联系人列表窗口和通知区域的一个图标组成。

- `-n`, `--no-connect`

启动时不连接

- `-h`, `--start-hidden`

启动时不显示联系人列表或任何对话框

- `-v`, `--version`

显示版本

# 环境

`EMPATHY_LOGFILE=filename`

如果设置，调试输出将进入指定的文件而不是 stderr。

`EMPATHY_DEBUG=type`

可以设置为“all”以获得完整的调试输出，或设置为各种未记录的选项（可能会随版本发布而变化）来过滤输出。

### 作者

本手册页由 Laurent Bigonville 为 Debian GNU/Linux 系统编写（但也供他人使用）。

# 另请

`empathy-accounts`(1), The Telepathy 项目 The Empathy 项目

## 名称

`enc` - 对称加密例程

### 概要

`openssl enc -ciphername [-in filename] [-out filename] [-pass arg] [-e] [-d] [-a/-base64] [-A] [-k password] [-kfile filename] [-K key] [-iv iv] [-S salt] [-salt] [-nosalt] [-z] [-md] [-p] [-P] [-bufsize number] [-nopad] [-debug] [-none] [-engine id]`

### 描述

对称加密命令允许使用基于密码或显式提供的密钥对各种块加密和流加密进行加密或解密。Base64 编码或解码也可以单独执行，也可以在加密或解密之外执行。

### 选项

- `-in filename`

输入文件名，默认为标准输入。

- `-out filename`

输出文件名，默认为标准输出。

- `-pass arg`

密码源。有关关于 arg 格式的更多信息，请参阅 `openssl`(1) 中的 PASS PHRASE ARGUMENTS 章节。

- `-salt`

在密钥派生例程中使用盐（salt）。这是默认设置。

- `-nosalt`

不在密钥派生例程中使用盐。此选项仅用于测试目的或与旧版本的 OpenSSL 和 SSLeay 兼容。

- `-e`

加加密输入数据：这是默认设置。

- `-d`

解密输入数据。

- `-a`

对数据进行 base64 处理。这意味着如果正在进行加密，则数据在加密后会进行 base64 编码。如果设置了解密，则输入数据在解密前会进行 base64 解码。

- `-base64`

与 `-a` 相同

- `-A`

如果设置了 `-a` 选项，则在一行内对数据进行 base64 处理。

- `-k password`

用于导出密钥的密码。这是为了与之前的 OpenSSL 版本兼容。已被 `-pass` 参数取代。

- `-kfile filename`

从 `filename` 的第一行读取读取用于导出密钥的密码。这是为了与之前的 OpenSSL 版本兼容。已被 `-pass` 参数取代。

- `-nosalt`

不使用盐

- `-salt`

加密时使用盐（随机生成或通过 `-S` 提供）（这是默认设置）。

- `-S salt`

实际使用的盐：必须是十六进制字符串。

- `-K key`

实际使用的密钥：必须是十六进制字符串。如果只指定密钥，则必须显式指定 `-iv`。当同时指定密钥和密码时，将使用 `-K` 提供的密钥，并从密码生成 IV。

- `-iv iv`

实际使用的 IV（初始化向量）：必须是十六进制字符串。如果只通过 `-K` 指定密钥，则必须显式定义 IV。当通过其他选项指定密码时，IV 将从密码生成。

- `-p`

输出所使用的密钥和 IV。

- `-P`

输出所使用的密钥和 IV 后立即退出：不做任何加密或解密。

- `-bufsize number`

设置 I/O 的缓冲区大小

- `-nopad`

禁用标准填充

- `-debug`

调试用于 I/O 的 BIO。

- `-z`

在加密前或解密后使用 zlib 压缩或解压文本。此选项仅在编译了 zlib 或 zlib-dynamic 选项 OpenSSL 中存在。

- `-none`

使用空算法（不对输入进行加密或解密）。

# 备注

可以通过 `openssl ciphertext` 或 `openssl -ciphertext` 调用程序。但第一种格式不支持引擎提供的算法，因为该格式在处理配置文件和任何加载项之前就被处理了。提供全新加密算法的引擎（例如提供 cost89 算法的 cost engine）应该在配置文件配置。在命令行中使用 `-engine` 选项指定的引擎只能用于 OpenSSL 核心或配置文件指定的其他引擎支持的硬件加速实现。

当 `enc` 命令列出支持的算法时，由引擎提供的算法也会列出来。

如有必要，将提示输入密码以派生密钥和 IV。

如果密钥是从密码派生的，除非为了与旧版本的 OpenSSL 和 SSLay 兼容，否则应始终使用 `-salt` 选项。

如果不使用 `-salt`，就可以对密码进行有效的字典攻击并攻击流加密加密数据。这是因为在没有相同盐的情况下，密码总是生成相同的加密结果。在使用盐时，加密数据的前八字节保留给盐：在加密文件时随机生成盐，解密时从加密文件中读取。

# 支持的算法

请注意，这些算法中的某些在编译时被禁用了，某些只有在配置文件中配置了适当引擎时才可用。使用不支持的选项运行 `enc` 命令（例如 `openssl enc -help`），其输出将包含你的 OpenSSL 版本支持的算法列表，包括由引擎提供的算法。

`enc` 程序不支持 CCM 和 GCM 等身份验证加密模式。该工具不存储或检索认证标记。



```
base64 Base fb-cbc Blowfish in CBC mode as Afias for fb-cbc bf-cbc
Blowfish in CFB mode bf-ecb Blowfish in ECB mode bf-ofb Blowfish in OFB
mode-cast CAST in CBC mode cast Alias for cast-cast5 cast5-cast CAST5
cast-cast5 CAST5 in CBC mode cast5-ecb ECB mode cast5-ofb
cast5 in OFB mode DES in CBC mode as des-des-des DES in des-des-des
in CBC mode des-des-ecb in ECB mode des-ede-cdes-Two
key triple DES EDE in E mode des-ede-ede Two triple DES EDE in ECB
des-cfb Two triple DES EDE in mode-ede-ofb Two key
des E in OFB mode des-ede3 Three triple EDE in CBC mode des-ede3-cdes-
ede3-cfb Three triple DES EDE in CFB mode des-ede3-ofb Three key triple
des in OFB mode desX DES gost89 GOST 21847-89 in CNT mode (provided
by cgos engine) idea-idea IDEA in CBC mode idea same as idea-cbc
idea-cfb in IDEA mode idea-idea IDEA in ECB mode idea-ofb in OFB
mode rc2-cbc 128 bit RC2 in CBC mode rc2-Alias for rc2-cbc RC2 128 bit
RC2 in CFB mode rc2-cbc 128 bit RC2 in ECB mode rc2-ofb 128 bit in OFB
mode rc4-64 64 bit RC4 in CBC mode rc2-40-cbc 40 bit RC2 in CBC mode
rc4 128 bit RC4-64 64 bit RC4-49 bit RC4-53 cipher in
cbc mode rc5 EDE mode rc5-ofb RC5 cipher in CFB mode rc5-ecb RC5
cipher in OFB mode aes-128|192|256]-cbc
128/192/256 bit AES in CBC mode aes-[128|192|256] AES for-
[128|192|256]-cbc aes-[128|192|256]-cfb 128/192/256 bit AES in 128 bit
CFB mode aes-[128|192|256]-cfb1 128/192/256 bit AES in 1 CFB mode aes-
[128|192|256]-cfb 128/192/256 bit AES in 8 CFB mode aes-[128|192|256]-
ecb 128/192/256 bit AES in ECB mode aes-[128|192|256]-ofb 128/192/256 bit
AES in OFB mode
```

## 示例

仅对二进制文件进行 base64 编码：

```
openssl base64 -in file.bin -out file.b64
```

解码同一个文件：

```
openssl base64 -d -in file.b64 -out file.bin
```

使用提示密码通过 CBC 模式下的三重 DES 加密文件：

```
openssl des3 -salt -in file.txt -out file.des3
```

使用提供的密码解密文件：

```
openssl des3 -d -salt -in file.des3 -out file.txt -k password
```

使用 CBC 模式下的 Blowfish 算法加密文件并进行 base64 编码（例如以便可以通过邮件发送）：

```
openssl bf -a -salt -in file.txt -out file.bf
```

对文件进行 base64 解码然后解密：

```
openssl bf -d -salt -a -in file.bf -out file.txt
```

使用提供的 40 位 RC4 密钥解密某些数据：

```
openssl rc4-40 -in file.rc4 -out file.txt -K 0102030405
```

## 缺陷

当处理大文件时，`-A` 选项无法正常工作。

应该有一个选项允许包含迭代次数。

`enc` 程序仅支持带有特定参数的固定数量算法。因此，如果你想使用带有 76 位密钥的 RC2 或 84 位密钥的 RC4，你将无法使用此程序。

`enca` — 检测并转换文本文件的编码

# 语法概要

```
enca [-L LANGUAGE] [OPTION]... [FILE]... encovy [-L LANGUAGE] [OPTION]... [FILE]...
```

# 介绍与示例

如果你足够幸运，你唯一需要知道的两个东西就是命令 `enca FILE`，它会告诉你 `FILE` 使用了什么种编码（而不更改它），以及 `encov FILE`，它会将 `FILE` 转换为你的本地编码。

两者都支持多个文件和标准输入（输出）。例如 `enca -x latin2 <sometet | lpr` 确保在将 `sometet` 发送到打印机之前它是 ISO Latin2 格式。

该命令失败并将你的文件变成乱码的主要原因是 `enca` 需要知道语言来解码编码。它尝试从区域设置中确定语言和首选字符集，这可能不是你想要的。

你可以（或必须）使用 `-L` 选项告诉它正确的语言。假设你下载了一个俄罗斯 HTML 文件 `file.htm`，它声称是 windows-1251，但 `enca -L russian file.htm` 显示实际上是 KOI8-R。

### 说明

`enca` 读取给的文件或在未提供文件时读取标准输入，并结合解析和猜测来确定它们的编码。默认情况下，它以人类可读的格式显示结果。输出选择决定了 `enca` 在确定编码后采取的操作；其中一个 `-x` 是特殊的：它告诉 `enca` 将文件重编码为 `ENC`。

`enca` 还可以使用内置转换器或调用外部转换器将文件转换为另一种编码。它不在乎输入文件的结构，将其视为统一的文本块。对于多部分文件（例如邮箱），你必须先使用某些工具提取各个部分。这是能够检测任何损坏、不完整或错误文件的代价。

此名称在调用外部转换器时同样适用。

**-f,--human-readable**

打印检测到的字符集和表面（surfaces）的文字描述——这是人类最易理解的方式。这是默认行为。

精确格式如下：第一行仅包含字符集名称，随后是零或多个缩进的行，包含检测到的表面名称。然而，这种格式不适合也不旨在用于进一步的机器处理，且这些描述在未来可能会发生。

**-i,--icon-name**

打印 `iconv(3)`（和/或 `iconv(1)`）调用检测到的字符集的方式。具体地说，它会打印一个或多个 `iconv` 接受的、某种程度上是任意选择的别名。`iconv` 未知的字符集将被视为未知。

这种输出类型仅在 Enca 编译了 `iconv` 支持（特性 `+iconv-interface`）时才有意义。

**-r,--rfc1345-name**

打印 `RFC~1345` 字符集名称。当由于 `RFC~1345` 没有定义编码导致该名称不存在时，将打印在其他 RFC 中定义的其他名称，或者作者认为“最规范”的名称。

由于 `RFC~1345` 不定义表面，因此不会附加表面信息。

**-n,--mime-name**

打印检测到的字符集的首选 MIME 名称。这是你在修 电子邮件或网页时通常应该使用的名称。

未出现在 `http://www.iana.org/assignments/character-sets` 中的字符集将被视为未知。

**-s,--csocks-name**

打印 `cstocs(1)` 调用检测到的字符集的方式。`cstocs` 未知的字符集将被视为未知。

**-n,--name=WORD**

打印由 `WORD` 选择的字符集（编码）名称（只要没有歧义即可缩写）。对于上述列出的名称，`--name=WORD` 等同于 `--WORD`。

使用别名作为输出类型会导致 Enca 打印检测到的字符集的所有接受的别列表。

**-x,--convert-to=[..].ENC**

将文件转换为编码 `ENC`。



编码名称前的可选 `..` 没有特殊含义，你可以用它来提醒自己，与 `recode(1)` 不同，你应该指定所需的编码，而不是当前编码。

你可以为 `ENC` 使用 `recode(1)` 转换链或任何其他简单的编码规范，只要你告诉 `Enca` 使用某些理解该的工具进行转换（见 `CONVERSION` 章节）。

当 `Enca` 无法确定编码时，它会打印警告并保持文件不变；当它作为过滤器运行时，它会尽力将标准输入原样复制到输出。尽管如此，你不应依赖此并进行备份。

### `-C`, `--try-converters=LIST`

将逗号分隔的 `LIST` 添加到当你请求转换时将尝试的转换器列表中。它们的名称只要没有歧义即可缩写。

`enca --list converters`

获取所有有效转换器名称的列表（描述见 `CONVERSION` 章节）。

默认列表取决于 `Enca` 是如何编译的，运行

`enca --help`

查找默认转换器列表。

注意，默认列表仅在你完全没有指定 `-C` 时使用。否则，该列表将像初始为空一样构建，并且每个 `-C` 都会向其中添加新的转换器。

此外，将 `none` 作为转换器名称会导致清空转换器列表。

### `-E`, `—external-converter-program=PATH`

将外部转换器程序设置为 `PATH`。默认的外部转换器取决于 `enca` 是如何编译的，并且可能无法使用外部转换器。运行

`enca —help`

查找你的 `enca` 构建中默认的转换器程序。

# 通用选项

不属于其他选项类别……

### `-P`, `—with-filename`

强制 `Enca` 在每个结果前加上相应的文件名。默认情况下，当 `Enca` 在多个文件上运行时，它会在结果前加上文件名名前。

标准输入打印为 `STDIN`，标准输出打印为 `STDOUT`（后者仅在错误消息中可见）。

### `-P`, `—no-filename`

强制 `Enca` 不在结果前加上文件名。默认情况下，当 `Enca` 在单个文件（包括标准输入）上运行时，不会在结果前加上文件名。

### `-V`, `—verbose`

增加详细程度（每次使用增加一级）。

目前此选项并不十分有用，因为 `Enca` 的不同部分对相同详细程度的响应不同，大多数情况下没有响应。

# 列表

都是终端选项，即当 `Enca` 遇到其中某些项时，它会打印所需的列表并终止，不再处理任何后续选项。

### `-h`, `—help`

打印简要用法帮助。

### `-G`, `—license`

打印完整的 `Enca` 许可证（如果可能，通过分页器显示）。

### `-l`, `—list=WORD`

打印由 `WORD` 指定的列表（只要没有歧义即可缩写）。

可用列表包括：

- `built-in-charsets`. 所有通过内置转换器可转换的编码，按分组划分（输入和输出编码都必须来自此列表且属于同一组，才能进行内部转换）。
- `built-in-encodings.` 等同于 `built-in-charsets`，但被认为是过时的；在一段时间内将在带有警告的情况下接受。
- `converters.` 所有有效的转换器名称（配合 `-C` 使用）。
- `charsets.` 所有编码（字符集）。你可以选择哪些名称将通过 `name` 或任何名称输出类型选择器打印（当然，只有在给定命名空间具有名称的编码才会被打印），该选择器必须在*那时*指定。
- `encodings.` 等同于 `built-in-charsets`，但被认为是过时的；在一段时间内将在带有警告的情况下接受。
- `languages.` 所有支持的语言。
- `surfaces.` 所有可能的表面。
- `names.` 所有可能的名称。
- `lists.` 所有可能的列表。

# 默认目标字符集

指定目标字符集的直接方法是使用 `-x` 选项，它会覆盖任何默认设置。当作为 `encv` 调用 `Enca` 时，默认目标字符集的选择方式与 `recode(1)` 完全相同。

如果设置了 `DEFAULT_CHARSET` 环境变量，将将其作为目标字符集。否则，如果你的系统提供了 `nl_langinfo(3)` 函数，则使用当前区域的本地字符集作为目标字符集。

当这两种方法都失败时，`Enca` 会报错并终止。

# 可逆性说明

可逆性对你来说至关重要，你不根本应该将 `enca` 作为转换器使用（也许你可以，但要配合专门设计的 `recode(1)` 包装器）。否则，你至少应该知道处理不可争议字符实体的四种方法：

- `失败（fail）`——这也是一种可能性，顺便说，这正是 `GNU libc iconv` 实现所做的（`recode` 也可以告诉它这样做）
- `不动它们（don’t touch them）`——这是 `enca` 内部转换器总是做的，`recode` 也能做到；虽然它是不可逆的，但人类通常能够重建原始内容（至少在原理上）
- `近似化它们（approximate them）`——这是 `cstos` 能做的，`recode` 也能，尽管方式不同；如果你只是想让出现的文本变得可读，这是最佳选择
- `丢弃它们（drop them out）`——这是 `recode` 和 `cstos` 能做的（`cos` 用某些固定字符替换这些字符，而不仅仅是忽略）；当提交的字符只包含噪声时非常有用。

请参阅你常用的转换器手册以获取此问题的详细信息。通常，如果你不够幸运文件没有包含所有可转换字符，无论也需要人工干预。

# 性能说明

可用转换器性能低下的是 `enca` 包含内置转换器的主要原因之一。尽可能尝试使用它，即当文件的字符集足够干净，或者字符集混乱到它的零内置智能变得无关紧要时。它不需要磁盘空间也不需要额外内存，在大文件上性能可以比 `recode(1)` 高 10 倍以上，在小文件上比 `cstos(1)` 的 Perl 版本（即更快的版本）快 400 倍以上（事实上，它几乎和 `mer cp(1)` 一样快）。

在不是绝对必要的情况下尽量避免使用外部转换器，因为所有的分叉和移动操作都极其缓慢。

# 编码

你可以获取识别的字符集列表：

`enca --list charsets`

并使用 `--name` 参数，你可以选择任何你想要在列表中使用的名称。

你也可以通过以下命令列出所有表面（surfaces）：

`enca --list surfaces`

编码和表面名称不区分大小写，且不考虑字母数字字符。然而，大多数字母数字是不允许的。唯一允许的是：`-`、`_`、`*`、'`'、':' 以及 `~/`（作为字符集/表面分隔符）。`IBM-852` 和 `IBM852` 是相同的，而 `IBM 852` 不受接受。

# 字符集

以下识别的字符集列表使用了 `Enca` 的名称 (`-e`) 和 `Enca` 报告的口头描述 (`-f`)：

- `ASCII 7bit` 7 `ASCII` 字符
- `ISO-8859-2` `ISO 8859-2` 标准；`ISO Latin 2`
- `ISO-8859-4` `ISO 8859-4` 标准；`Latin 4`
- `ISO-8859-5` `ISO 8859-5` 标准；`ISO Cyrillic`
- `ISO-8859-13` `ISO 8859-13` 标准；`ISO Baltic`；`Latin 7`
- `ISO-8859-16` `ISO 8859-16` 标准
- `CP1225` `MS-Windows` 代码页 1125
- `CP1250` `MS-Windows` 代码页 1250
- `CP1251` `MS-Windows` 代码页 1251
- `CP1257` `MS-Windows` 代码页 1257；`Windows`
- `IBM852` `IBM/MS` 代码页 852；`PC (DOS) Latin 2`
- `IBM855` `IBM/MS` 代码页 855
- `IBM775` `IBM/MS` 代码页 775
- `IBM866` `IBM/MS` 代码页 866
- `baltic` `ISO-IR-179`；`Baltic`
- `KEYBCS2` 编码；`KEYBCS2`
- `macce` `Macintosh Central European`
- `maccyr` `Macintosh Cyrillic`
- `ECMA-113` `Ecma Cyrillic`；`ECMA-113`
- `KOI-8_CS_2` `KOI-8-CS2`
- `KOI-8-R` `KOI-R Cyrillic`
- `KOI8-U` `KOI8-Cyrillic`
- `KOI8-UNI` `KOI8-Unified Cyrillic`
- `TeX (LaTeX)`
- `UCS-2` 字符集 2 字节；`UCS-2`；`BMP`
- `UCS-4` 字符集 4 字节；`UCS-4`；`ISO-1046`
- `UTF-7` 转换格式 7 字节；`UTF-7`
- `UTF-8` 转换格式 8 字节；`UTF-8`；`T1`
- `GBK` 简体中文国家标准；`GB312`
- `BIG5` 传统中文工业标准；`Big5`
- `unknown`（`Enca` 无法给出可靠答案时报告的未识别编码）

# 表面 (Surfaces)

`Enca` 对所谓的表面有一些实验性支持（见下文）。它检测以下表面（并非适用于所有字符集）：

- `/CR` 行终止符
- `/LF` 行终止符
- `/CRLF` `CRLF` 行终止符
- `N.A.` 混合行终止符
- `N.A.` 混合对 (`1,2 -> 2,1`)



- `/21` 翻转字节序 (1,2,3,4 -> 4,3,2,1)

- `/4321` 大小中文块，连接

- `/qp` 引号打印编码

注意某些表面具有 `N.A.` 标识符——它们无法在命令行上指定，只能由 `Enca` 报告。这是故意的，因为它们告诉你文件不能被视为表面而非真实的表面。每个字符集都有其自然表面（在 `recode` 中称为“隐含”），但不会报告，例如 `IBM 852` 字符集的 `CR` 行终止符。对于 `UCS` 编码，大端被视为自然表面；不寻字节序由 `21` 和 `4321` 构建。`2143` 报告为 `21`，而 `3412` 报告为 `4321` 和 `21` 的组合。双重编码 `UTF-8` 既不是字符集也不是表面，它只是报告。

# 关于字符集、编码和表面

字符集是字符实体集，而编码是其字节和位的表示。在 `Enca` 中，编码一词意味着“文本表示”，即组成文本的字符实体序列与组成文件的字节（位）序列之间的关系。

因此，编码既是字符集也是所谓的表面（行终止符、字节序、组合、`Base64` 转换等）。尽管如此，将某些 `{charset,surface}` 对视为真实的字符集来处理是方便的。就像在 `recode` 中一样，所有的 `UCS-` 和 `UTF-` 编码都是字符集。

表面唯一的优点是：当你不启动时，`Enca` 将表现得像不感知表面的程序，与 `recode` 通信。

# 语言

`Enca` 需要知道输入的语言才能可靠工作，至少在 8 位编码的情况下。多字节编码应能识别任何拉丁语、希腊语。你可以（或必须）使用 `-L` 告诉 `Enca` 语言。当然，这可能是完全错误的并导致乱码和损坏文件，请不要忘记使用 `-L`。你也可以使用 `ENCAOPT` 环境变量设置默认语言（见相应章节）。

`Enca` 支持以下语言（每个语言都与 8 位编码一起列出）：

- 白俄罗斯语 `CP1251` `IBM866` `ISO-8859-5` `KOI-UI` `macyr` `IBM855`

- 保加尼亚语 `CP1251` `IBM855` `maccyr` `ECMA-113`

- 捷克语 `ISO-8859-2` `CP1250` `IBM852`

- 爱沙尼亚语 `ISO-8859-4` `CP1257` `IBM775` `ISO-8859-13` `baltic`

- 罗地亚语 `CP1250` `ISO-8859-2` `IBM852` `CORK`

- 匈牙语 `ISO-8859-2` `CP1250` `IBM852` `CORK`

- 立陶宛语 `CP1257` `ISO-8859-4` `IBM775` `ISO-8859-13` `macce` `baltic`

- 拉脱亚语 `CP1257` `ISO-8859-4` `IBM852` `macce` `ISO-8859-13` `celtic`

- 波兰语 `ISO-8859-2` `CP1250` `IBM852` `macce` `ISO-8859-13` `celtic` `CORK`

- 俄语 `KOI8-R` `CP1251` `ISO-8859-5` `IBM866` `maccyr`

- 斯洛伐克语 `ISO-8859-2` `CP1250` `IBM852` `KEYBC2` `macce` `KOI-8_CS_CORK`

- 斯洛文尼亚语 `ISO-8859-2` `CP1250` `IBM852` `macce` `CORK`

- 乌克兰语 `CP1251` `IBM8856` `ISO-8859-5` `CP1125` `KOI8-U` `macy`

- 中文 `GBK` `BIG5` `HZ`

特殊语言 `none` 可以缩写为 `_`，它不包含 8 位编码，因此只检测多字节编码。

你也可以使用区域设置（locale）代替语言：

- `be`

- `bg`

- `cs`

- `et`

- `hr`

- `hu`

- `lt`

拉脱维语 `lv`

波兰语 `pl`

俄语 `ru`

斯洛伐语 `sk`

斯洛文尼亚语 `sl`

乌克兰语 `uk`

中文 `zh`

# 特性

`Enca` 的某些功能取决于你系统的可用性以及编译方式。你可以通过以下命令获取它们的列表：

```
enca --version
```

功能名称前的加号 `+` 表示可用，减号 `-` 表示此版本缺少该功能。

- `librecode-interface`. `Enca` 提供了与 `GNU recode` 库字符转换函数的get接口。

- `iconv-interface`. `Enca` 提供了与 `UNIX98 iconv` 字符转换函数的接口。

- `external-converter`. `Enca` 可以使用外部转换程序（如果你安装了某些合适的程序）。

- `language-detection`. `Enca` 尝试从区域设置（locales）中猜测语言（`-L`）。至少在原则上，你不需要需要使用 `--language` 选项。

- `locale-alias`. `Enca` 能够解析用于语言名称的区域设置别名。

- `target-charset-auto`. `Enca` 尝试从区域设置中检测你偏好的字符集。`--auto-convert` 选项以及将 `Enca` 作为 `enconv` 调用，至少在原则上是有效的。

- `ENCAOPT`. `Enca` 能够在命令行参数之前正确解析此环境变量。像 `ENCAOPT="-L uk"` 这样简单的操作即使没有此功能也能正常工作。

# 环境

变量 `ENCAOPT` 可以包含一组默认 `Enca` 选项。其内容在命令行参数之前被解释。遗憾的是，这在所有地方都不生效（必须具备 `+ENCAOPT` 功能）。

`LC_CTYPE`, `LC_COLLATE`, `LC_MESSAGES`（可能继承自 `LC_ALL` 或 `LANG`）用于猜测你的语言（必须具备 `+language-detection` 功能）。

变量 `DEFAULT_CHARSET` 可以被 `encoy` 作为默认目标字符集。

# 诊断

当所有输入文件都成功处理时，`Enca` 返回退出代码 `0`（即检测到了所有编码，并且如果要求了转换，则所有文件都已转换为所需的编码）。如果 `Enca` 因为不够智能而无法猜测编码或无法对任何输入文件执行转换，则返回退出代码 `1`。发生严重问题（例如 I/O 问题）时，返回退出代码 `2`。

# 安全

让 `Enca` 在无人值守的情况下工作应该是其目标。但是：

- 不保证检测工作 100% 有效。不要对此押注，你可能会丢失宝贵的数据。

- 不要使用 `enca`（程序），如果你想要任何类似于安全的东西，请链接到 `libenca`。你必须亲自执行转换。

- 不要使用外部转换器。理想情况下，在编译时禁用它们。

- 注意 `ENCAOPT` 以及所有从环境（即区域设置）自动猜测各种内容的内置功能。

### 参见

`autoconvert(1)`, `cstocs(1)`, `file(1)`, `iconv(1)`, `iconv(3)`, `nl_langinfo(3)`, `map(1)`, `piconv(1)`, `recode(1)`, `locale(5)`, `locale(7)`, `ltt(1)`, `umap(1)`, `unicode(7)`, `utf-8(7)`, `xcode(1)`

# 已知 Bug

它有太多*未知*的 bug。

使用 `LC_*` 值作为语言的想法简直是脑残。然而我喜欢它。

它无法在破坏文件之前对其进行备份。

在某些情况下，它在大于 31 位的文件系统和/或通过 `NFS` 上可能会表现不正确（两者均未测试，但在实践中不应引起问题）。

内置转换器不转换来自 `KOI8-CS2` 的字符 `ch`，可能还有你从未听过的其他字符。

`EOL` 类型识别在 `Quoted-printable` 编码的文件上效果很差。这应该某日被修复。

没有命令行选项来调整 `libenca` 参数。这是故意的（即 `Enca` 应该 `DWIM` 自动处理），但有时这是一种麻烦。

手册页太长了，特别是这一节。这并不重要，因为没人读。

将错误报告发送到 <https://github.com/nijel/enca/issues>。

# 趣

`Enca` 是 `Extremely Naive Charset Analyser`（极其天真的字符集分析器）。尽管如此，`enc` 最初源于 `encoding`，因此开头的 `e` 应该像 `encoding` 那样读，而不是 `extreme`。

### 作者

David Necas (Yeti) <yeti@physics.muni.cz>

Michal Cihar <michal@cihar.com>

Unicode 数据来自各种免费的在线资源或使用 `GNU recode` 生成。统计数据来自网络上的各种文本，希望字符计数不会违反任何人的版权。

## 致谢

请参阅发行包中的 `THANKS` 文件。

# 版权

Copyright (C) 2000-2003 David Necas <michal@cihar.com>.

Copyright (C) 2009 Michal Cihar <michal@cihar.com>.

`Enca` 是免费软件；你可以根据自由软件基金会发布的 GNU 通用许可证第 2 版条款对其进行重新分发和/或修改。

`Enca` 的发布是希望它是有用的，但**不提供任何保证**；甚至没有对于商品性或针对特定用途的适用性的暗示保证。更多信息请参阅 GNU 通用许可证。

Copyright (C) 2000-2003 David Necas <michal@cihar.com>.

Copyright (C) 2009 Michal Cihar <michal@cihar.com>.



Enca 是免费软件；你可以根据自由软件基金会发布的 GNU 通用许可证第 2 版条款对其进行重新分发和/或修改。

Enca 的发布是希望它是有用的，但**不提供任何保证**；甚至没有对于商品性或针对特定用途的适用性的暗示保证。更多信息请参阅 GNU 通用许可证。

拉脱维语 `lv`

波兰语 `pl`

俄语 `ru`

斯洛伐语 `sk`

斯洛文尼亚语 `sl`

乌克兰语 `uk`

中文 `zh`

# 特性

`--version`

- `librecode-interface`. Enca 提供了与 GNU recode 库字符转换函数的接口。
- `iconv-interface`. Enca 提供了与 UNIX98 `iconv` 字符转换函数的接口。
- `external-converter`. Enca 可以使用外部转换程序（如果你安装了某些合适的程序）。
- `language-detection`. Enca 尝试从区域设置（locales）中猜测语言（`-L`）。至少在原则上，你不需要需要使用 `--language` 选项。
- `locale-alias`. Enca 能够解析用于语言名称的区域设置别名。
- `target-charset-auto`. Enca 尝试从区域设置中检测你偏好的字符集。`--auto-convert` 选项以及将 Enca 作为 `enconv` 调用，至少在原则上是有效的。
- `ENCAOPT`. Enca 能够在命令行参数之前正确解析此环境变量。像 `ENCAOPT="-L uk"` 这样简单的操作即使没有此功能也能正常工作。

# 环境

变量 `ENCAOPT` 可以包含一组默认 Enca 选项。其内容在命令行参数之前被解释。遗憾的是，这在所有地方都不生效（必须具备 `+ENCAOPT` 功能）。

`LC_CTYPE`, `LC_COLLATE`, `LC_MESSAGES`（可能继承自 `LC_ALL` 或 `LANG`）用于猜测你的语言（必须具备 `+language-detection` 功能）。

变量 `DEFAULT_CHARSET` 可以被 `encov` 作为默认目标字符集。

# 诊断

当所有输入文件都成功处理时，Enca 返回退出代码 `0`（即检测到了所有编码，并且如果要求了转换，则所有文件都已转换为所需的编码）。如果 Enca 因为不够智能而无法猜测编码或无法对任何输入文件执行转换，则返回退出代码 `1`。发生严重问题（例如 I/O 问题）时，返回退出代码 `2`。

# 安全

让 Enca 在无人值守的情况下工作应该是其目标。但是：

- 不保证检测工作 100% 有效。不要对此押注，你可能会丢失宝贵的数据。
- 不要使用 `enca`（程序），如果你想要任何类似于安全的东西，请链接到 `libenca`。你必须亲自执行转换。
- 不要使用外部转换器。理想情况下，在编译时禁用它们。
- 注意 `ENCAOPT` 以及所有从环境（即区域设置）自动猜测各种内容的内置功能。

### 参见

`autoconvert(1)`, `cstocs(1)`, `file(1)`, `iconv(1)`, `iconv(3)`, `nl_langinfo(3)`, `map(1)`, `piconv(1)`, `recode(1)`, `locale(5)`, `locale(7)`, `ltt(1)`, `umap(1)`, `unicode(7)`, `utf-8(7)`, `xcode(1)`

# 已知 Bug

它有太多未知的 bug。

使用 `LC_*` 值作为语言的想法简直是脑残。然而我喜欢它。

它无法在破坏文件之前对其进行备份。

在某些情况下，它在大于 31 位的文件系统和/或通过 NFS 上可能会表现不正确（两者均未测试，但在实践中不应引起问题）。

内置转换器不转换来自 `KOI8-CS2` 的字符 `ch`，可能还有你从未听过的其他字符。

EOL 类型识别在 Quoted-printable 编码的文件上效果很差。这应该某日被修复。

没有命令行选项来调整 `libenca` 参数。这是故意的（即 Enca 应该 DWIM 自动处理），但有时这是一种麻烦。

手册页太长了，特别是这一节。这并不重要，因为没人读。

将错误报告发送到 <https://github.com/nijel/enca/issues>。

# 趣

Enca 是 Extremely Naive Charset Analyser。尽管如此，`enc` 最初源于 `encoding`，因此开头的 `e` 应该像 `encoding` 那样读，而不是 `extreme`。

### 作者

David Necas (Yeti) <yeti@physics.muni.cz>

Michal Cihar <michal@cihar.com>

Unicode 数据来自各种免费的在线资源或使用 GNU recode 生成。统计数据来自网络上的各种文本，希望字符计数不会违反任何人的版权。

## 致谢

请参阅发行包中的 THANKS 文件。

# 版权

Copyright (C) 2000-2003 David Necas <michal@cihar.com>.

Copyright (C) 2009 Michal Cihar <michal@cihar.com>.

Enca 是免费软件；你可以根据自由软件基金会发布的 GNU 通用许可证第 2 版条款对其进行重新分发和/或修改。

Enca 的发布是希望它是有用的，但不提供任何保证；甚至没有对于商品性或针对特定用途的适用性的暗示保证。更多信息请参阅 GNU 通用许可证。

（注：由于原文存在大量重复内容，此处已按要求翻译并保留了所有文本结构）

# 更多信息

http://www.abisource.com/enchant/

# 另请

`aspell(1)`, `ispell(1)`,

### 作者

Dom Lachowicz WEB: http://www.abisource.com/enchant/

MAIL: domlachowiczz@gmail.com

## 名称

`enca` — 检测并转换文本文件的编码

### 概要

```
enca [-L LANGUAGE] [OPTION]... [FILE]... encovy [-L LANGUAGE] [OPTION]... [FILE]
```

# 介绍与示例

如果你足够幸运，你唯一需要知道的两件事是：执行命令 `enca FILE` 会告诉你文件 FILE 使用的是什么编码（不改变它），而执行 `encov FILE` 会将文件 FILE 转换为你本地的编码。使用 `-x` 选项可以将文件转换为其他编码（详情请参见 OPTIONS 章节中的 `-x` 条目，以及 CONVERSION 和 ENCODINGS 章节）。

两者都支持处理多个文件以及标准输入（输出）。例如：`enca -x latin2 <sometext| lpr` 确保文件 `sometext` 在发送到打印机时使用的是 ISO Latin-2 编码。这些命令之所以失败并导致你的文件变成垃圾数据的主要原因是 Enca 需要知道它们的语言来检测编码。它会尝试从本地设置（locale settings）中确定你的语言和首选字符集，而这可能不是你想要的。

你可以（或必须）使用 `-L` 选项来告诉它正确的语言。假设你下载了一个俄语的 HTML 文件 `file.htm`，它声称是 windows-1251 编码，但事实并非如此。于是你运行了 `enca -Lu file.htm`，并发现它是 KOI8-R 编码（例如）。请注意，目前支持的语言并不多（参见 LANGUAGES 章节）。另一个警告是，Enca 的某些功能（即字符集转换能力）很大程度上取决于系统上安装了哪些工具（参见 CONVERSION 章节）——运行 `enca—version` 获取功能列表（参见 FEATURES 章节）。还可以尝试 `enca—help` 获取所有其他 Enca 选项的描述（并发现此手册页的其他部分是冗余的）。

### 描述

Enca 读取给文件（在未提供时读取标准输入），并根据其语言（必须由你支持）的知识以及解析、统计分析、猜测和“黑魔法”的混合手段确定它们的编码，然后将其打印到标准输出（或承认不知道编码可能是什么）。默认情况下，Enca 以多行人类可读的描述呈现结果，还有其他几种格式可用——参见下文的“输出类型选择器”。

当你要求时，Enca 还可以将文件转换为其他编码 ENC——可以使用内置转换器、某些转换库或调用外部转换器来实现。

Enca 的主要目标是作为一种自动转换工具进行无人值运行，尽管它可能尚未达到这一步（请参见 SECURITY 章节）。

请注意，除少数情况外，Enca 确实知道输入文件的语言才能给你提供可靠的答案。另一方面，它也可以很好地处理非纯文本文件，甚至检测某些二进制文件内部文本字符串的字符集；当然，这取决于非文本组件的特征。

Enca 不关心输入文件的结构，它将其视为统一的文本/数据块。对于多部分文件（例如邮件邮箱），你必须使用某些了解结构的工具先提取出各个部分。这是检测任何损坏、不完整或有错误的文件编码的代价。

### 选项

选项分为几类：操作模式选项、输出类型选择器、猜测参数、转换参数、通用选项和列表。

所有长选项在没有歧义的情况下都可以缩写，长选项的强制性参数对于短选项也是强制性的。

# 操作模式

如下：



进入`/path/to/xxx`目录，找到`xxx.json`。

## 选项

- `-c`, `--auto-convert`

  等同于通过 `encov` 调用 `Enca`。

  如果未指定输出类型选择器，则检测文件编码，从本地设置中猜测你的首选字符集，并将其文件转换为该字符集（仅在支持 `+target-charset-auto` 功能时可用）。

- `-g`, `--guess`

  等同于通过 `enca` 调用 `Enca`。

  如果未指定输出类型选择器，则检测文件编码并报告它们。

# 输出类型选择器

选择 `Enca` 在确定编码后将采取的操作；大多数选项只是在不同的名称、格式和编码打印方法/约定之间进行选择，但其中一个 `-x` 是特殊的：它告诉 `Enca` 将文件重编码为其他编码 `ENC`。这些选项是互斥的；如果你指定了多个输出类型选择器，最后一个将优先。

几种输出类型代表了某些其他程序使用的字符集名称，但并非所有这些程序都认识 `Enca` 识别的所有字符集。请注意，在某些情况下，`Enca` 不区分无法识别的字符集与给定命名空间内没有的字符集。

- `-d`, `--details`

  用于打印关于猜测过程的详细信息，但由于 `Enca` 只是一个链接到 `Enca` 库的程序，这是可能的。此选项大致等同于 `--human-readable`，例外是 `Enca` 无法识别编码时会报告失败原因。

- `-e`, `--enca-name`

  打印字符集的 `Enca` 友好名称，即可能是最通用的定义。

- `-f`, `--human-readable`

  打印检测字符集的口语描述。这是默认选项。

- `-i`, `--human-readable`

  打印检测字符集的口语描述。也可以尝试 `enca --help` 获取所有其他 `Enca` 选项的描述（并发现此手册页的其他部分是冗余的）。

- `-n`, `--name`

  打印检测字符集的首选名称。这是你在修复电子邮件或网页时通常使用的名称。

- `-r`, `--rfc1345-name`

  打印检测字符集的 `RFC1345` 名称。

- `-s`, `--cstocs-name`

  打印 `cstocs(1)` 如何调用检测到的字符集。

- `-x`, `--convert-to=[.]`

  将文件转换为编码 `ENC`。编码名称前的可选 `..` 没有特殊含义，除非你用来提醒自己：与 `recode(1)` 不同，你应该指定目标编码而不是当前编码。

# 猜测参数

只有一个：`-L` 设置输入文件的语言。此选项是强制性的（但请看下文）。

- `-L`, `--language=LANG`

  将输入文件的语言设置为 `LANG`。更准确地说，`LANG` 可以是支持语言的任何有效本地名称（或带有 `+locale-alias` 功能的别名）。你也可以指定 `none`，此时仅识别多字节编码。运行 `enca --list languages` 获取支持语言的列表。当你没有指定语言时，`Enca` 会尝试从本地设置中猜测你的语言并假设输入文件使用该语言。详情参见 `LANGUAGES` 章节。

# 转换参数

让你对执行的字符集转换进行更细粒度的控制。如果没有指定输出类型类型，它们不会产生任何影响。具体的转换细节请参见 `CONVERSION` 章节。

- `-C`, `--try-converters=LIST`

  当你请求转换时，将逗号分隔的 `LIST` 添加到将尝试的转换器列表中。它们的名称在没有歧义的情况下可以缩写。运行 `enca --list converters` 获取所有有效转换器名称的列表（描述请参见 `CONVERSION` 章节）。默认列表取决于 `Enca` 的编译方式，运行 `enca --help` 默认转换器列表。注意，只有在你完全没有指定 `-C` 时才会使用默认列表。否则，使用指定的列表。

  构建方式就像最初为空，并且每个 `-C` 都会向其添加新的转换器。此外，指定 `none` 为转换器名称将清空转换器列表。

- `-E`, `--external-converter-program=PATH`

  将外部转换器程序名称设置为 `PATH`。默认外部转换器取决于 `enca` 的编译方式，并且可能完全无法使用外部转换器。运行

```
enca --help
```

以查找你 `enca` 编译中的默认转换器程序。

## 通用选项

不属于其他选项类别...

- `-P`, `--with-filename`

  强制 `Enca` 在每个结果前加上对应的文件名。默认情况下，当 `Enca` 在多个文件上运行时，它会在结果前前缀文件名。

  标准输入将打印为 `STDIN`，标准输出将打印为 `STDOUT`（后者可能仅在错误消息中可见）。

- `-P`, `--no-filename`

  强制 `Enca` 不在结果前前缀文件名。默认情况下，当 `Enca` 在单个文件（包括标准输入）上运行时，它不在结果前前缀文件名。

- `-V`, `--verbose`

  增加详细程度级别（每使用一次增加一级）。

  目前此选项并不好用，因为 `Enca` 的不同部分对相同详细程度的响应不同，大多数情况下完全没有响应。

## 列表

这些都是终止性的，即当 `Enca` 遇到其中某些项时，它会打印所需的列表并终止，不再处理后续选项。

- `-h`, `--help`

  打印简短的用法帮助。

- `-G`, `--license`

  打印完整的 `Enca` 许可证（如果可能，通过分页器）。

- `-l`, `--list=WORD`

  打印指定的 `WORD` 列表（只要没有歧义，可以缩写）。

可用的列表包括：

- `built-in-charsets`. 内置转换器可转换的所有编码，按分组（输入和输出编码都必须来自此列表且属于同一组才能进行内部转换）。

- `built-in-encodings`. 等同于 `built-in-charsets`，但被认为过时；在一段时间内，将在带警告的情况下被接受。

- `converters`. 所有有效的转换器名称（配合 `-C` 使用）。

- `charsets`. 所有的编码。你可以选择在任何输出类型选择器中打印哪些名称（当然，只有在给定命名空间中具有名称的编码才会被打印），该选择器必须指定在 `--list` *之前*。

- `encodings`. 等同于 `charsets`，但被认为过时；在一段时间内，将在带警告的情况下被接受。

- `languages`. 所有支持的语言及其字符集。注意这里指的是语言风格，而不是字符集名称。

- `names`. 选项的所有可能值。

- `lists`. 此项的所有可能值。

- `surfaces`. `Enca` 识别的所有表面。

- `-v`, `--version`

  打印程序版本和功能列表（参见 `FEATURES`）。

## 转换

尽管 `Enca` 最初设计为仅用于猜测编码的工具，但它现在具有几种字符集转换方法。你可以通过 `-C` 控制使用其中的哪种。`Enca` 会按照 `-C` 指定列表顺序尝试转换器，直到找到可以执行所需转换的转换器，或者耗尽列表。你应该先指定首选转换器，后指定次选转换器。外部转换器 `extern` 应作为最后手段指定，因为它失败时通常无法恢复。默认转换器列表始终从内置开始，然后继续来自第一个可用的：`librecode`, `iconv`, ... 需要注意的是，当 `Enca` 表示它无法执行转换时，意味着没有转换器可以执行该转换。仍然可能使用多个转换器分几个步骤执行所需的转换，但弄清楚这一点可能需要人类智能。

## 内置转换器

是所有转换器中最简单且最快的，只能执行少数字节转换并直接在原地修改文件（可能被认为是危险的，但效率很高）。此外，它的主要优势（也是缺点）是它不在乎：只需转换在目标编码中有表示的字符，不触碰任何内容，且从不打印任何错误消息。你可以获取它可以转换的所有编码器列表。可以通过 `-C` 将其指定为内置。

## Librecode 转换器

是 `GNU recode` 库的接口，负责实际的重编码工作。它可能已编译在；运行 `enca --version` 以查找其在你 `enca` 编译中的可用性（特性 `librecode-interface`）。在使用它之前，你应该熟悉 `recode(1)`，因为 `recode` 是一个非常复杂且强大的字符集工具。在与 `Enca` 一起使用可能会遇到问题，特别是因为 `Enca` 对功能的支持并非 100% 兼容，因为 `recode` 过于努力使转换变得可逆，因为它有时会忽略 I/O 错误，而且它 Bug 非常多。请参 `GNU info` 页面有关 `recode` 库的详情。此转换器可以指定为 `librecode -C`。

## Iconv 转换器

是 `UNIX98 iconv(3)` 转换函数的接口，负责实际的重编码工作。它可能已编译在；运行 `enca --version` 以查找其在你 `enca` 编译中的可用性（特性 `iconv-interface`）。虽然 `iconv` 存在于大多数系统上，但它很少提供有用的转换集，唯一著名的例外是 `GNU libc` 中的 `iconv`。它对表面通常也很挑剔（此时，未实现表面转换）。然而，它可能代表了执行 `Unicode` 之间转换的唯一标准化工具。请参阅 `iconv` 文档了解其在你特定系统上的功能详情。此转换器可以指定为 `iconv -C`。

## 外部转换器



是任意的外部转换器，可以使用 `-E` 选项指定（同时最多定义一个）。`enca` 一带提供了一些标准工具：`cstocs`, `recode`, `map`, `umap` 和 `piconv`。所有都是包装脚本：对应 `cstocs(1)`, `recode(1)`, `map(1)`, `umap(1)` 和 `piconv(1)`。请注意 `enca` 无法控制外部转换器到底做了什么。如果你设置了它，你对后果负责。

如果你想让你自己的转换器使用 `enca`，你应该知道它总是调用

```
CONVERTER ENC_CURRENT FILE [-]
```

其中 `CONVERTER` 是通过 `-E` 指定的，`ENC_CURRENT` 是通过 `-x` 指定的检测编码，`FILE` 是要转换的文件，即它是每个文件单独调用的。第四个参数 `-` 如果存在，会将标准输出而不是覆盖 `FILE`。转换器应该处理不更改文件权限、失败时返回错误代码以及清理临时文件。请参见标准外部转换器。此转换器可以指定为 `extern -C`。

## 默认目标字符集

指定目标字符集的直接方法是 `-x` 选项，它可以覆盖任何默认设置。当调用 `encov` 时，目标字符集的选择与 `recode(1)` 完全相同。如果设置了环境变量 `DEFAULT_CHARSET`，则将其作为目标字符集。否则，如果你的系统提供了 `nl_langinfo(3)` 函数，则使用本地字符集作为目标字符集。当两种方法都失败时，`enca` 会报错并终止。

## 可逆性说明

如果可逆性对你至关重要，你不应该将 `enca` 作为转换器（或者你可以使用，配合专门设计的 `recode(1)` 包装器）。否则，你至少应该知道处理可逆实体的四种基本方法：

- 失败——这是一个可能，恰恰是 GNU libc `iconv` 实现所做的（`recode` 也可以被告知这样做）

- 不触碰——这是 `enca` 内部转换器总是做的，`recode` 也可以这样做；虽然它是不可逆的，但人类通常能够（原则上）还原。

- 近似——这是 `cstops` 可以做的，`recode` 也可以但方法不同；如果你只想让文本可读，这是最好的选择。

- 删除——这是 `recode` 和 `cstops` 都可以做的（`cstops` 可以用固定字符替换这些字符而不是仅仅忽略）；当省略的字符仅包含噪声时非常有用。

请参阅你喜欢的转换器手册了解有关此问题的详情。通常，如果你足够的文件没有包含所有可转换的字符，仍然需要人工干预。

## 性能说明

可用转换器性能低下是导致内置转换器引入 `enca` 的主要原因之一。请尽可能使用它。

在绝对必要的情况下，请避免使用外部转换器，因为所有的分支（forking）和移动操作都极其缓慢。

# 编码 (ENCODINGS)

你可以获取已识别的字符集列表

- - `enca --list charsets`

并使用 `--name` 参数，你可以选择任何想要在列表中使用的名称。

你还通通过以下命令列出所有表面（surfaces）：

- - `enca --list surfaces`

编码和表面名称不区分大小写，且不考虑非字母数字字符。然而，大多数字母数字是不允许的。唯一允许的是：`-`、`_`、`*`、'`'、':'、';' 以及 `~/`（作为字符集/表面分隔符）。`IBM852’` 是相同的，而 `IBM 852` 则不被接受。

# 字符集 (Charsets)

以下识别的字符列表使用了 Enca 的名称 (`-e`) 和 Enca 报告的文字描述 (`-f`)：

- ASCII 7bit ASCII 字符

- ISO-8859-2 ISO 8859-2 标准；ISO Latin 2

- ISO-8859-4 ISO 8859-4 标准；Latin 4

- ISO-8859-5 ISO 8859-5 标准；ISO Cyrillic

- ISO-8859-13 ISO 8859-13 标准；ISO Baltic; Latin 7

- ISO-8859-16 ISO 8859-16 标准

- CP1225 MS-Windows 代码页 1125

- CP1250 MS-Windows 代码页 1250

- CP1251 MS-Windows 代码页 1251

- CP1257 MS-Windows 代码页 1257；WinBaltRim

- IBM852 IBM/MS 代码页 852；PC (DOS) Latin 2

- IBM855 IBM/MS 代码页 855

- IBM775 IBM/MS 代码页 775

- IBM866 IBM/MS 代码页 866

- baltic ISO-IR-179; Baltic

- KEYBCS2 Kamenicky 编码；KEYBCS2

- macce Macintosh 中欧语

- maccyr Macintosh 西里尔语

- ECMA-113 Ecma 西里尔语；ECMA-113

- KOI-8_CS_2 KOI-8-CS2 代码 (`T602`)

- KOI-8-R KOI-8-R 西里尔语

- KOI8-U KOI8-U 西里尔语

- KOI8-UNI KOI8-Unified 西里尔语

- UCS-2 2字节通用字符集；UCS-2; BMP

- 4字节通用字符集；UCS-4; ISO-10646

- 通用转换格式 7 位；UTF-7

- 通用转换格式 8 位；UTF-8

- CORK 编码；T1

- 简体中文标准；GB2312

- 繁体中文标准；Big5

- HZ 编码 GB2312

- unknown 未识别的编码

其中 `unknown` 不是任何真实的编码，当 Enca 无法给出可靠答案时会报告此项。

# 表面 (Surfaces)

Enca 对所谓的表面（surfaces）提供一些实验支持（见下文）。它可以检测以下表面（并非所有表面都能适用于所有字符集）：

- `/CR` CR 换行符

- `/LF` LF 换行符

- `/CRLF` CRLF 换行符

- N.A. 混合换行符

- N.A. 被非文本数据包围/混合

- `/21` 双字节序反转（1,2 -> 2,1）

- `/4321` 四字节字节序反转（1,2,3,4 -> 4,3,2,1）

- N.A. 大端和小端序均有，且串联

- `/qp` 可打印字符

注意，某些表面用 N.A. 代替了标识——它们无法在行中指定，只能由 Enca 报告。这是刻意的，因为它们告知你为什么该文件不能被视为表面一致的，而不是代表一个真实的表面。每个字符集都有其自然表面（在 recode 中称为“implied”），这不会被报告，例如，对于 IBM 852 字符集，它是 CR 换行符。对于 UCS 编码，大端序被视为自然表面；异常的字节序由 21 和 4321 的排列构造而成：2143 被报告为 21，而 3412 被报告为 432 和 21 的组合。双重编码 UTF-8 既不是字符集也不是表面，仅会被报告。

# 关于字符集、编码和表面 (About charsets, encodings and surfaces)

字符集是字符实体的集合，而编码是其字节字节表示。在 Enca 中，这个词的意思与“文本表示”相同，即构成文本的字符实体序列与构成文件的字节（位）序列之间的关系。因此，编码既是字符集也是所谓的表面（换行符、字节序、组合、Base64 转换等）。尽管如此，像 `recode(1)` 那样处理某些字符集-表面对是非常方便的，所有的 UCS-UTF 编码都被称为字符集。请参阅 `recode` 文档获取有关此问题的更多信息。表面的唯一好处是：当你不从它们开始时，Enca 将不会启动，并会尝试像一个不感知表面的程序一样运行，即使在与 `recode` 通信时也是如此。

# 语言 (LANGUAGES)

Enca 需要知道输入文件的语言才能可靠工作，至少在常规 8 位编码时。多字节编码应该能够识别任何拉丁语、西里尔语或希腊语。你可以（或必须）使用 `-L` 选项告诉 Enca 语言。由于人们经常使用与其本地设置（locales）相同的语言工作，Enca 会尝试通过检查 `LC_CTYPE` 的值和其他本地设置类别（请参阅 `locale(7)`）来猜测语言，并在你未指定时将其用于语言识别。当然，它可能是完全错误的，并给你无意义的答案且损坏你的文件，所以请不要忘记使用 `-L` 选项。由于人们经常使用与其本地设置相同的语言工作，Enca 会尝试通过使用本地设置变量来猜测语言。以下是 Enca 支持的语言：

- 俄罗斯罗俄罗斯语

- 保加利亚语

- 捷克语

- 爱斯波尼亚语

- 匈牙利语

- 拉脱维尼亚语

- 波兰语

- 俄罗斯语

- 斯洛伐克语

- 斯洛文尼亚语

- 乌克兰语

- 中文

# 功能 (FEATURES)

Enca 的某些功能取决于系统的可用性以及它的编译方式。你可以通过以下命令获取列表：

`enca --version`

功能名称前的加号表示可用，减号表示此版本缺少该功能。

**librecode-interface.** Enca 拥有 GNU recode 库字符转换函数。

**iconv-interface.** Enca 拥有 UNIX98 `iconv` 字符转换函数。

**external-converter.** Enca 可以使用外部转换程序（如果你安装了的话）。



`language-detection.` Enca尝试从本地设置猜测语言 (`-L`)。你不需要 `--language` 选项，至少在原理上。

`locale-alias.` Enca 能够解析用于语言的本地别名。

`target-charset-auto.` Enca 尝试从本地设置检测你的首选字符集。选项 `--auto-convert` 并调用 Enca 是可行的，至少在原理上。

`ENCAOPT.` Enca 能够在命令行参数之前正确解析此环境变量。简单的 `ENCAOPT="-L uk"` 即使没有此功能也能工作。

## 环境变量 (ENVIRONMENT)

环境变量 `ENCAOPT` 可以包含一组默认 Enca 选项。其内容在命令行参数之前解释。遗憾的是，这在所有地方都不适用（必须具有 `+ENCAOPT` 功能）。

`LC_CTYPE`, `LC_COLLATE`, `LC_MESSAGES`（可能继承自 `LC_ALL` 或 `LANG`）用于猜测语言（必须具有 `+language-detection` 功能）。

变量 `DEFAULT_CHARSET` 可以被 `enconv` 作为默认目标字符集。

# 检测 (DIAGNOSTICS)

当 Enca 成功处理所有输入文件时返回退出码 `0`（即所有编码都已检测，且如果要求转换，所有文件都已转换为所需的编码）。当 Enca 无法猜测编码或对任何输入文件执行转换时（因为它不够聪明），返回退出码 `1`。在发生严重问题（例如 I/O）时返回退出码 `2`。

# 安全

让 Enca 能够在无人值守的情况下运行是它的目标。但是：

不保证检测功能能 100% 有效。不要为此赌注，你可能会轻易丢失宝贵的数据。

不要使用 `enca`（程序），如果你想要任何类似于安全的功能，请链接到 `libenca`。然后你必须亲自执行最终的转换。

不要使用外部转换器。理想情况下，请在编译时禁用它们。

请注意 `ENCAOPT` 以及所有内置的从环境（即区域设置 locales）自动猜测各种事情的功能。

# 另请

`autoconvert(1)`, `cstocs(1)`, `file(1)`, `iconv(1)`, `iconv(3)`, `nl_langinfo(3)`, `map(1)`, `piconv(1)`, `recode(1)`, `locale(5)`, `locale(7)`, `ltt(1)`, `umap(1)`, `unicode(7)`, `utf-8(7)`, `xcode(1)`

# 已知 Bug

它有太多的*未知* Bug。

使用 `LC_*` 值作为语言标识的想法简直是脑残的。但我喜欢它。

它无法在破坏文件之前进行备份。

在某些情况下，它在 >31bit 文件系统上/或通过 NFS 可能会表现异常（这两者均未经测试，但在实践中不应引起问题）。

内置转换器不转换来自 `KOI8-CS2` 的字符 `ch`，可能还有一些你从未听过的字符。

EOL 类型识别在引文打印（Quoted-printable）编码的文件上效果很。这应该在以后被修复。

没有命令行选项来调整 `libenca` 参数。这是刻意的设计——Enca 应该“自作聪明”（DWIM），但有时这是一种麻烦。

手册页太长了，尤其是这一节。这并不重要，因为没人读。

将 Bug 报告发送至 <https://github.com/nijel/enca/issues>。

# 趣味

Enca 代表的是 Extremely Naive Charset Analyser（极其天真的字符分析器）。尽管如此，`enc` 原本来自 `encoding`，因此开头的 `e` 应该像 `encoding` 中那样读，而不是 `extreme` 中。

### 作者

David Necas (Yeti) <yeti@physics.muni.cz>

Michal Cihar <michal@cihar.com>

Unicode 数据生成自各种（免费）在线资源或使用 GNU recode 生成。统计数据生成自网络上的各种文本，我希望字符计数不会侵犯任何版权。

## 致谢

请查看分发包中的 THANKS 文件。

# 版权

Copyright (C) 2000-2003 David Necas (Yeti).

Copyright (C) 2009 Michal Cihar <michal@cihar.com>.

Enca 是免费软件；你可以根据自由软件基金发布的 GNU 通用公共许可协议第 2 版条款进行分发和/或修改它。

分发 Enca 是希望它有用，但**不提供任何保证**；甚至甚至不包括对商品性或适用于特定用途的暗示保证。更多细节请参阅 GNU 通用公共许可协议。

你应该已随 Enca 收到一份 GNU 通用公共许可协议的副本；如果没有，请写信 Free Software Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA。

## 名称

`env` - 在修改后的环境中运行程序

# 语法概要

```
env [OPTION]... [-] [NAME=VALUE]... [COMMAND [ARG]...]
```

### 描述

在环境中将每个 NAME 设置为 VALUE 并运行 COMMAND。

长选项的强制参数对于短选项也是强制的。

- `-i,--ignore-environment`

  从空环境开始

- `-0,--null`

  每个输出行以 NUL 结束，而不是换行符

- `-u,--unset=NAME`

  从环境中移除变量

- `--help`

  显示此帮助并退出

- `--version`

  输出版本信息并退出

单独的 `-` 意味着 `-i`。如果没有 COMMAND，则打印结果环境。

### 作者

由 Richard Mlynarik 和 David MacKenzie 编写。

# 报告 Bug

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 请向 <http://translationproject.org/team/> 报告 `env` 翻译 Bug。

# 版权

Copyright © 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 版本 3 或更高版本 <http://gnu.org/licenses/gpl.html>。这是免费软件：你可以自由地更改和分发它。在法律允许的范围内没有任何保证。

# 另请

完整文档位于：<http://www.gnu.org/software/coreutils/env> 或通过本地的：info ‘(coreutils) env invocation’ 获取。

`envsubst` - 替换 shell 格式字符串中的环境变量

# 语法概要

```
envsubst [OPTION] [SHELL-FORMAT]
```

### 描述

替换环境变量的值。

# 运行模式：

- `-v, —variables`

输出出现在 SHELL-FORMAT 中出现的变量

# 提示性输出：

- `-h, —help`

显示此帮助并退出

`-V, —version`

输出版本信息并退出

在正常运行模式下，标准输入被复制到标准输出，形式为 `$VARIABLE` 或 `${VARIABLE}` 的环境变量引用被替换为相应的值。如果给定了 SHELL-FORMAT，则只替换 SHELL-FORMAT 中引用的环境变量；否则，标准输入中出现的所有环境变量都会被替换。

使用 `—variables` 时，将忽略标准输入，输出由 SHELL-FORMAT 中引用的环境变量组成，每行一个。

### 作者

由 Bruno Haible 编写。

# 报告 Bug

将 Bug 报告至 <bug-gnu-gettext@gnu.org>。

# 版权

Copyright © 2003-2007 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 版本 3 或更高版本 <http://gnu.org/licenses/gpl.html>。这是免费软件：你可以自由地更改和分发它。在法律允许的范围内没有任何保证。

# 另请

`envsubst` 的完整维护为 Texinfo 手册。如果 `envsubst` 程序在你的站点正确安装，那么：

```
info envsubst
```

应该让你访问手册。

## 名称

`epiphany` - 用于 GNOME 的简单 浏览器

# 语法概要

```
epiphany [OPTION...] [url]
```

### 描述

帮助选项

- `?, —help`

显示帮助

应用程序选项

- `-n,--new-tab`

在现有窗口中打开新标签页

- `--new-window`

打开新窗口

- `-b,--bookmarks-editor`

启动书签编辑器

- `--import-bookmarks=FILE`

从文件导入书签

- `-l,--load-session=FILE`

加载会话



- `-t,--add-bookmark=URL`

添加书签

- `--private-instance`

启动私有实例

- `--profile=FILE`

私有实例使用的配置文件

- `--display=DISPLAY`

使用的 X 显示

- `--version`

显示版本

Epiphany 有完善帮助系统。运行浏览器并从菜单选择帮助。

### 作者

由 Marco Pesenti Gritti、Christian Pesch 及其他人编写。

### 概要

`[ -rvCNR ] [ -d xy ] [ -T name ] [ -M dir ] [ -f F ] [ -s n ] [ -p n ] [ -m n ] [files..]`

### 描述

本手册页介绍了 GNU 版本的 `eqn`，它是 `groff` 文档格式系统的一部分。`eqn` 将嵌入在 `stoff` 输入文件的方程描述编译为 `stoff` 可理解的命令。通常，应该使用 `stoff` 的 `-e` 选项来调用它。其语法与 Unix `eqn` 高度兼容。GNU `eqn` 的输出无法用 Unix `stoff` 处理；必须用 GNU `stoff` 处理。如果命令行上没有给出文件，则读取标准输入。文件名为 `-` 会导致读取标准输入。

`eqn` 在 `-M` 选项指定的目录中搜索 `eqnprc`，然后在 `/etc/groff/site-tmac`、`/etc/groff/site-tmac`，以及最后在标准宏目录 `/usr/share/groff/1.22.3/tmac` 中搜索。如果该文件存在，`eqn` 会在处理其他输入之前处理它。`-R` 选项可防止此操作。

GNU 不提供 `neqn` 的功能：它不支持低分辨率、类打字机的设备（尽管对于非常简单的输入可能运行良好）。

### 选项

命令行选项与其参数之间可以存在空白符。

- `-dxy` 分别指定内联方程左右端的定界符 `x` 和 `y`。源文件中的任何语句都会覆盖此设置。

- `-C` 即使在后面跟着非空格或换行符的字符，也识别 `EQ` 和 `.EN`。此外，`delim on` 语句不会被特殊处理。

- `-N` 不允许定界符内出现换行。此选项允许 `eqn` 从缺失定界符的情况下更好地恢复。

- `-v` 打印版本号。

- `-r` 仅进行一次尺寸缩小。

- `-mn` 最小点号为 `n`。`eqn` 不会将下标或上标的尺寸缩小到比 `n` 更小的尺寸。

- `-Tname` 输出用于设备名称。通常，此选项的唯一作用是定义一个值为 `I` 的宏名称；`eqn` 使用该名称来提供适用于输出设备的句定义。然而，如果指定的设备是 `MathML`，则输出将为 MathML 标记而非 `troff` 命令，且完全不会加载 `eqn`。默认设备是 `ps`。

- `-Mdir` 在默认目录之前搜索 `eqn` 的目录。

- `-R` 不加载 `eqn`。

- `-ff` 等同于 `gfont F` 命令。

- `-sn` 等同于 `gsize n`。此选项已废弃。`eqn` 通常在遇到方程时按当前的点号尺寸设置方程。

- `-pn` 表示下标和上标应比周围文本小 `n` 磅。此选项已废弃。通常 `eqn` 将下标和上标的尺寸设为周围文本尺寸的 70%。

# 用法

此处仅描述了 GNU `eqn` 和 Unix 之间的差异。

GNU `eqn` 通过 `-TMathML` 选项调用 Presentation MathML 输出。

GNU `eqn` 将输入标记设置为三个点或低点，而不是经典 `eqn` 的三个居中点。要获得三个居中点，我们使用 `\dots` 和 `\cdot cdot cdot`。

GNU `eqn` 输入语言的大部分新功能都基于 TeX。下文有一些关于 TeX 和 GNU `eqn` 差异的引用；如果你不熟悉 TeX，可以忽略忽略。

# 控制定界符

如果不在兼容模式下，`eqn` 识别

`delim on`

用于恢复之前通过 `delim off` 调用禁用的定界符。如果未指定定界符，则调用无效。

# 自动间距

`eqn` 为方程的每个组件分配类型，并使用该类型调整组件之间的间距。可能的类型有：

- `ordinary`：普通字符，如 `1` 或 `x`；
- `operator`：运算符
- `binary`：二元运算符，如 `+`；
- `relation`：关系运算符，如 `=`；
- `opening`：左括号，如 `(`；
- `closing`：右括号，如 `)`；
- `punctuation`：标点字符，如 `,`；
- `inner`：包含括号内的子公式；
- `suppress spacing`：抑制自动间距调整。

# 方程的组件通过两种方式之一获取类型。

# `type t e`

这会产生一个包含 `e` 但类型为 `t` 的方程组件，其中 `t` 是上述提到的类型。例如，`times` 被定义为：

`type "binary" \mu`

类型的名称不需要加引号，引号可以防止宏展开。`charset text` 字符组的文本。未加引号的字符组会被拆分成单个字符，并查找每个字符的类型；这会更改存储的每个字符的类型；它表示从现在起 `text` 中的字符都具有类型 `t`。例如：

`charset "punctuation" :,;;;`

这将使得字符 `...` 在之后出现在任何方程中都具有类型 `punctuation`。类型 `v` 也可以是字母或数字；在这些情况下，`charset` 会改变字符的字体类型。参见 `字体` 部分。

# 新原语

# `big e`

放大它修改的表达式；意为具有类似于 CSS `large` 的语义。在 `troff` 输出中，点号增加了 5；在 MathML 输出中，表达式使用 `<msmallower size="big">`。

`e1 e2` 类似于 `over`；`over` 缩小了 `e1` 和 `e2` 的尺寸；它还在 `e1` 或 `e2` 与 之间放置了垂直空间。`eqn` 在 `-M` 选项指定的目录中搜索 `eqnprc`，然后在 `/etc/groff/site-tmac`、`/etc/groff/site-tmac`，以及最后在标准宏目录 `/usr/share/groff/1.22.3/tmac` 中搜索。如果该文件存在，`eqn` 会在处理其他输入之前处理它。`-R` 选项可防止此操作。

GNU 不提供 `neqn` 的功能：它不支持低分辨率、类打字机的设备（尽管对于非常简单的输入可能运行良好）。



类型的名称不需要加引号，引号可以防止宏展开。`charset text`字符组的。未加引号的字符组会被拆分成单个字符，并查找每个字符的类型；这会更改存储的每个字符的类型；它表示从现在起`text`中的字符都具有类型`t`。例如：

`charset "punctuation" :,;;;`

这将使得字符‘...;’在之后出现在任何方程中都具有类型`punctuation`。类型`v`也可以是字母或数字；在这些情况下，`charset`会改变字符的字体类型。参见“字体”部分。

# 新原语

## big e

放大它修改的表达式；意为具有类似于 CSS ‘large’的语义。在`troff`输出中，点号增加了 5；在 MathML 输出中，表达式使用`<msmallower size="big">`

`e1 e2`类似于`over`；`over`缩小了`e1`和`e2`的尺寸；它还在`e1`或`e2`与 放置了垂直空间。`eqn`在`-M`选项指定的目录中搜索`eqnprc`，然后在`/etc/groff/site-tmac`、`/etc/groff/site-tmac`，以及最后在标准宏目录`/usr/share/groff/1.22.3/tmac`中搜索。如果该文件存在，`eqn`会在处理其他输入之前处理它。`-R`选项可防止此操作。

GNU 不提供`neqn`的功能：它不支持低分辨率、类打字机的设备（尽管对于非常简单的输入可能运行良好）。

### 选项

命令行选项与其参数之间可以存在空白符。

- `-dxy`分别指定内联方程左右端的定界符`x`和`y`。源文件中的任何语句都会覆盖此设置。
- `-C`即使在后面跟着非空格或换行符的字符，也识别`EQ`和`.EN`。此外，`delim on`语句不会被特殊处理。
- `-N`不允许定界符内出现换行。此选项允许`eqn`从缺失定界符的情况下更好地恢复。
- `-v`打印版本号。
- `-r`仅进行一次尺寸缩小。
- `-mn`最小点号为`n`。`eqn`不会将下标或上标的尺寸缩小到比`n`更小的尺寸。
- `-Tname`输出用于设备名称。通常，此选项的唯一作用是定义一个值为`I`的宏名称；`eqn`使用该名称来提供适用于输出设备的句定义。然而，如果指定的设备是`MathML`，则输出将为 MathML 标记而非`troff`命令，且完全不会加载`eqn`。默认设备是`ps`。
- `-Mdir`在默认目录之前搜索`eqn`的目录。
- `-R`不加载`eqn`。
- `-ff`等同于`gfont F`命令。
- `-sn`等同于`gsize n`。此选项已废弃。`eqn`通常在遇到方程时按当前的点号尺寸设置方程。
- `-pn`表示下标和上标应比周围文本小`n`磅。此选项已废弃。通常`eqn`将下标和上标的尺寸设为周围文本尺寸的 70%。

# 用法

此处仅描述了 GNU `eqn`和 Unix 之间的差异。

GNU `eqn`通过`-TMathML`选项调用 Presentation MathML 输出。

GNU `eqn`将输入标记设置为三个点或低点，而不是经典`eqn`的三个居中点。要获得三个居中点，我们使用`\dots`和`\cdot cdot cdot`。

GNU `eqn`输入语言的大部分新功能都基于 TeX。下文有一些关于 TeX 和 GNU `eqn`差异的引用；如果你不熟悉 TeX，可以忽略。

# 控制定界符

如果不在兼容模式下，`eqn`识别

```
delim on
```

用于恢复之前通过`delim off`调用禁用的定界符。如果未指定定界符，则调用无效。

# 自动间距

`eqn`为方程的每个组件分配类型，并使用该类型调整组件之间的间距。可能的类型有：

- `ordinary`：普通字符，如‘1’或‘x’；
- `operator`
- `binary`：二元运算符，如‘+’；
- `relation`：关系运算符，如‘=’；
- `opening`：左括号，如‘(’；
- `closing`：右括号，如‘)’；
- `punctuation`：标点字符，如‘,’；
- `inner`：包含括号内的子公式；
- `suppress spacing`：抑制自动间距调整。

# 方程的组件通过两种方式之一获取类型。

## type t e

这会产生一个包含`e`但类型为`t`的方程组件，其中`t`是上述提到的类型。例如，`times`被定义为：

```
type "binary" \mu
```

类型的名称不需要加引号，引号可以防止宏展开。`charset text`字符组的。未加引号的字符组会被拆分成单个字符，并查找每个字符的类型；这会更改存储的每个字符的类型；它表示从现在起`text`中的字符都具有类型`t`。例如：

```
charset "punctuation" :,;;;
```

这将使得字符‘...;’在之后出现在任何方程中都具有类型`punctuation`。类型`v`也可以是字母或数字；在这些情况下，`charset`会改变字符的字体类型。参见“字体”部分。



这将使得字符‘...;’在之后出现在任何方程中都具有类型 `punctuation`。类型 `v` 也可以是字母或数字；在这些情况下，`charset` 会改变字符的字体类型。参见“字体”部分。

# 新原语

## big e

放大它修改的表达式；意为具有类似于 CSS ‘large’的语义。在 `troff` 输出中，点号增加了 5；在 MathML 输出中，表达式使用 `<msmallower size="big">`

`e1 e2` 类似于 `over`；`over` 缩小了 `e1` 和 `e2` 的尺寸；它还在 `e1` 或 `e2` 与 放置了垂直空间。`eqn` 在 `-M` 选项指定的目录中搜索 `eqnprc`，然后在 `/etc/groff/site-tmac`、`/etc/groff/site-tmac`，以及最后在标准宏目录 `/usr/share/groff/1.22.3/tmac` 中搜索。如果该文件存在，`eqn` 会在处理其他输入之前处理它。`-R` 选项可防止此操作。

GNU 不提供 `neqn` 的功能：它不支持低分辨率、类打字机的设备（尽管对于非常简单的输入可能运行良好）。

### 选项

命令行选项与其参数之间可以存在空白符。

- `-dxy` 分别指定内联方程左右端的定界符 `x` 和 `y`。源文件中的任何语句都会覆盖此设置。
- `-C` 即使在后面跟着非空格或换行符的字符，也识别 `EQ` 和 `.EN`。此外，`delim on` 语句不会被特殊处理。
- `-N` 不允许定界符内出现换行。此选项允许 `eqn` 从缺失定界符的情况下更好地恢复。
- `-v` 打印版本号。
- `-r` 仅进行一次尺寸缩小。
- `-mn` 最小点号为 `n`。`eqn` 不会将下标或上标的尺寸缩小到比 `n` 更小的尺寸。
- `-Tname` 输出用于设备名称。通常，此选项的唯一作用是定义一个值为 `I` 的宏名称；`eqn` 使用该名称来提供适用于输出设备的句定义。然而，如果指定的设备是 `MathML`，则输出将为 MathML 标记而非 `troff` 命令，且完全不会加载 `eqn`。默认设备是 `ps`。
- `-Mdir` 在默认目录之前搜索 `eqn` 的目录。
- `-R` 不加载 `eqn`。
- `-ff` 等同于 `gfont F` 命令。
- `-sn` 等同于 `gsize n`。此选项已废弃。`eqn` 通常在遇到方程时按当前的点号尺寸设置方程。
- `-pn` 表示下标和上标应比周围文本小 `n` 磅。此选项已废弃。通常 `eqn` 将下标和上标的尺寸设为周围文本尺寸的 70%。

# 用法

此处仅描述了 GNU `eqn` 和 Unix 之间的差异。

GNU `eqn` 通过 `-TMathML` 选项调用 Presentation MathML 输出。

GNU `eqn` 将输入标记设置为三个点或低点，而不是经典 `eqn` 的三个居中点。要获得三个居中点，我们使用 `\dots` 和 `\cdot cdot cdot`。

GNU `eqn` 输入语言的大部分新功能都基于 TeX。下文有一些关于 TeX 和 GNU `eqn` 差异的引用；如果你不熟悉 TeX，可以忽略。

# 控制定界符

如果不在兼容模式下，`eqn` 识别

```
delim on
```

用于恢复之前通过 `delim off` 调用禁用的定界符。如果未指定定界符，则调用无效。

# 自动间距

`eqn` 为方程的每个组件分配类型，并使用该类型调整组件之间的间距。可能的类型有：

- `ordinary`：普通字符，如‘1’或‘x’；
- `operator`
- `binary`：二元运算符，如‘+’；
- `relation`：关系运算符，如‘=’；
- `opening`：左括号，如‘(’；
- `closing`：右括号，如‘)’；
- `punctuation`：标点字符，如‘,’；
- `inner`：包含括号内的子公式；
- `suppress spacing`：抑制自动间距调整。

# 方程的组件通过两种方式之一获取类型

## type t e

这会产生一个包含 `e` 但类型为 `t` 的方程组件，其中 `t` 是上述提到的类型。例如，`times` 被定义为：

```
type "binary" \mu
```

类型的名称不需要加引号，引号可以防止宏展开。`charset text` 字符组的。未加引号的字符组会被拆分成单个字符，并查找每个字符的类型；这会更改存储的每个字符的类型；它表示从现在起 `text` 中的字符都具有类型 `t`。例如：

```
charset "punctuation" :,;;;
```

这将使得字符‘...;’在之后出现在任何方程中都具有类型 `punctuation`。类型 `v` 也可以是字母或数字；在这些情况下，`charset` 会改变字符的字体类型。参见“字体”部分。



`e1` `e2` 类似于 `over`；`over` 缩小了 `e1` 和 `e2` 的尺寸；它还在 `e1` 或 `e2` 与 放置了垂直空间。`eqn` 在 `-M` 选项指定的目录中搜索 `eqnprc`，然后在 `/etc/groff/site-tmac`、`/etc/groff/site-tmac`，以及最后在标准宏目录 `/usr/share/groff/1.22.3/tmac` 中搜索。如果该文件存在，`eqn` 会在处理其他输入之前处理它。`-R` 选项可防止此操作。

GNU 不提供 `neqn` 的功能：它不支持低分辨率、类打字机的设备（尽管对于非常简单的输入可能运行良好）。

### 选项

命令行选项与其参数之间可以存在空白符。

- `-dxy` 分别指定内联方程左右端的定界符 `x` 和 `y`。源文件中的任何语句都会覆盖此设置。
- `-C` 即使在后面跟着非空格或换行符的字符，也识别 `EQ` 和 `.EN`。此外，`delim on` 语句不会被特殊处理。
- `-N` 不允许定界符内出现换行。此选项允许 `eqn` 从缺失定界符的情况下更好地恢复。
- `-v` 打印版本号。
- `-r` 仅进行一次尺寸缩小。
- `-mn` 最小点号为 `n`。`eqn` 不会将下标或上标的尺寸缩小到比 `n` 更小的尺寸。
- `-Tname` 输出用于设备名称。通常，此选项的唯一作用是定义一个值为 `I` 的宏名称；`eqn` 使用该名称来提供适用于输出设备的句定义。然而，如果指定的设备是 `MathML`，则输出将为 MathML 标记而非 `troff` 命令，且完全不会加载 `eqn`。默认设备是 `ps`。
- `-Mdir` 在默认目录之前搜索 `eqn` 的目录。
- `-R` 不加载 `eqn`。
- `-ff` 等同于 `gfont F` 命令。
- `-sn` 等同于 `gsize n`。此选项已废弃。`eqn` 通常在遇到方程时按当前的点号尺寸设置方程。
- `-pn` 表示下标和上标应比周围文本小 `n` 磅。此选项已废弃。通常 `eqn` 将下标和上标的尺寸设为周围文本尺寸的 70%。

# 用法

此处仅描述了 GNU `eqn` 和 Unix 之间的差异。

GNU `eqn` 通过 `-TMathML` 选项调用 Presentation MathML 输出。

GNU `eqn` 将输入标记设置为三个点或低点，而不是经典 `eqn` 的三个居中点。要获得三个居中点，我们使用 `\dots` 和 `\cdot cdot cdot`。

GNU `eqn` 输入语言的大部分新功能都基于 TeX。下文有一些关于 TeX 和 GNU `eqn` 差异的引用；如果你不熟悉 TeX，可以忽略。

# 控制定界符

如果不在兼容模式下，`eqn` 识别

```
delim on
```

用于恢复之前通过 `delim off` 调用禁用的定界符。如果未指定定界符，则调用无效。

# 自动间距

`eqn` 为方程的每个组件分配类型，并使用该类型调整组件之间的间距。可能的类型有：

- `ordinary`：普通字符，如 `1` 或 `x`；
- `operator`
- `binary`：二元运算符，如 `+`；
- `relation`：关系运算符，如 `=`；
- `opening`：左括号，如 `(;`
- `closing`：右括号，如 `);`
- `punctuation`：标点字符，如 `,`
- `inner`：包含括号内的子公式；
- `suppress spacing`：抑制自动间距调整。

# 方程的组件通过两种方式之一获取类型。

# `type t e`

这会产生一个包含 `e` 但类型为 `t` 的方程组件，其中 `t` 是上述提到的类型。例如，`times` 被定义为：

```
type "binary" \mu
```

类型的名称不需要加引号，引号可以防止宏展开。`charset text` 字符组的。未加引号的字符组会被拆分成单个字符，并查找每个字符的类型；这会更改存储的每个字符的类型；它表示从现在起 `text` 中的字符都具有类型 `t`。例如：

```
charset "punctuation" :,;;;
```

这将使得字符 `...` 在之后出现在任何方程中都具有类型 `punctuation`。类型 `v` 也可以是字母或数字；在这些情况下，`charset` 会改变字符的字体类型。参见“字体”部分。

# 新原语

# `big e`

放大它修改的表达式；意为具有类似于 CSS `large` 的语义。在 `troff` 输出中，点号增加了 5；在 MathML 输出中，表达式使用 `<msmallower size="big">`

`e1` `e2` 类似于 `over`；`over` 缩小了 `e1` 和 `e2` 的尺寸；它还在 `e1` 或 `e2` 与 放置了垂直空间。`eqn` 在 `-M` 选项指定的目录中搜索 `eqnprc`，然后在 `/etc/groff/site-tmac`、`/etc/groff/site-tmac`，以及最后在标准宏目录 `/usr/share/groff/1.22.3/tmac` 中搜索。如果该文件存在，`eqn` 会在处理其他输入之前处理它。`-R` 选项可防止此操作。

GNU 不提供 `neqn` 的功能：它不支持低分辨率、类打字机的设备（尽管对于非常简单的输入可能运行良好）。

参数的数量。在生成 MathML 模式时，它们不起作用，因为排版和微调动作被推给了下游的 MathML 渲染引擎。这些参数可以使用 `set` 命令设置。

```
set p
```

这会将参数 `~p` 设置为值 `~n`；`n` 是一个整数。例如，

```
set x_height 45
```

表示 `eqn` 假设 `x~height` 为 `0.45~ems`。

可能的参数如下。除非另有说明，否则值以 em 的百分分之一（hundredths of an em）为单位。这些描述旨在说明，而非最终定义。

## `minimum_size`

`eqn` 不会设置比此点号更小的任何内容。值的单位为磅（points）。

## `fat_offset`

粗体字体（`fat` primitive）通过水平偏移该量并重叠两个公式副本来加粗公式。此参数在 MathML 模式下不使用；特征文本使用 `<mstyle mvariant="double-struck">`。

- `over_hang`（悬浮）：分数上方比分子和分母宽度最大值的两倍该数值更大；换句话说，它比分子和分母至少悬出该量。
- `accent`（重音）：当横线或下划线产生的线宽度等于其应用对象的深度时；对于单个字符，这往往会产生一条看起来太宽的线。
- `delimiter_factor`（分隔符因子）：使用左、右原语符产生的可扩展分隔符，其总高度和深度至少为子公式超出轴线向上部分（最大值的两倍）的几千分之一。
- `delimiter_shortfall`（分隔符缺失）：使用左、右原语符产生的可扩展分隔符，其总高度和深度不小于子公式超出轴线向上部分（最大值的两倍）与此值的差。
- `null_delimiter_space`（空分隔符空间）：在分数的每侧插入此等宽的水平空间。
- `script_space`（脚本空间）：下标和上标的宽度增加此数额。
- `thin_space`（窄空格）：在标点字符后自动插入此等宽的空间。
- `medium_space`（中等空格）：在关系符号两侧自动插入此宽的宽空格。
- `x_height`（x 高）：不带升部部的字符（如 `x` 和 `h`）的基线高度。对于你正在使用的字体，该值准确至关重要。
- `default_rule_thickness`（默认规则粗细）：这应设置为使用 `\D` 转义序列产生的水平线的粗细。
- `num1`：`over` 命令将分子向上移动至少此数额。
- `num2`：`smallover` 命令将分子向上移动至少此数额。
- `denom1`：`over` 命令将分母向下移动至少此数额。
- `denom2`：`smallover` 命令将分母向下移动至少此数额。
- `sup1`：上标通常向上移动至少此数额。
- `sup2`：上标中的上标或上限或分数分子中的上标向上移动至少此数额。这通常比 `sup1` 小。
- `sup3`：分母内根号内或下标下限中的上标向上移动至少此数额。这通常比 `sup2` 小。
- `sub1`：下标通常向下移动至少此数额。
- `sub2`：当同时存在下标和上标时，下标向下移动至少此数额。
- `sub_drop`（下标下降）：上标的基线距离其所设置的对象的顶部不超过此数额。
- `sub_drop`（下标下降）：下标的基线至少低于其所设置的对象的底部此数额。
- `big_of_spacing1`（大间距1）：上限的基线至少高于其所设置的对象的顶部。
- `big_of_spacing2`（大间距2）：下限的基线至少低于其所设置的对象的底部。
- `big_of_spacing3`（大间距3）：上限的顶部至少高于其所设置的对象的顶部。
- `big_of_spacing4`（大间距4）：下限的顶部至少低于其所设置的对象的底部。
- `big_of_spacing5`（大间距5）：在界符上下添加此宽的垂直空间。
- `baseline_sep`（基线间距）：堆叠或矩阵中行的基线通常距离很大。在某些情况下，这应该等于 `num1` 和 `denom1` 之和。
- `shift_down`（向下移动）：矩阵或堆叠中顶部与基线之间的中点向下移动此数额。在某些情况下，这应该等于 `axis_height`。
- `column_sep`（列间距）：在矩阵列之间添加此空间。



- `matrix_side_sep`（矩阵侧边）：如果此值不零，则使用 `\D` 转义序列绘制线条，而不是使用超出 `\` 转义序列和 `\ru` 字符。

- `body_height`（正文高度）：公式高度超过此值的部分作为包含公式的行之前的额外空间（使用 `\x`）。默认值为 85。

- `body_depth`（正文深度）：公式深度超过此值的部分作为包含公式的行之后的额外空间（使用 `\x`）。默认值为 35。

- `nroff`：如果此值不零，`ndfine` 的行为将像 `define` 一样，`tdefine` 的行为也像 `define` 一样，且 `ndfine` 被忽略。默认值为 0（这通常由 `eqnrc` 文件为 `ascii`、`latin1`、`utf8` 和 `cp1047` 设备改为 1）。

关于这些许多参数作用的更精确描述，可以在《The TeXbook》的附录 H 中找到。

## 宏

宏可以接受参数。在 n 等于 1~9 之间的宏中，它会被替换为 n；如果宏在调用时带有参数，将被替换为 n 个参数；如果宏在调用时带有带参数的左括号，将被替换为 n 个参数；如果宏在调用时带有带参数的右括号，将被替换为 n 个参数；如果宏在调用时没有参数，则被替换为 n。（注：此处此处根据原文逻辑，翻译为：宏可以接受参数。在 n 等于 1~9 之间的宏中，它会被替换为 n；如果宏在调用时带有参数，将被替换为 n 个参数；如果宏在调用时带有带参数的左括号，将被替换为 n 个参数；如果宏在调用时带有带参数的右括号，将被替换为 n 个参数；如果宏在调用时没有参数，则被替换为 n 个参数。）

## `sdefine` name X anything

这类似于 `define` 命令，但如果在调用时带有参数，则忽略。

## `include` sfiles

包含文件的内容（`include` 和 `copy` 是同义词）。以 `.EQ` 或 `.EN` 开头的行会被忽略。

如果 `name` 已经定义，则处理括号内的任何字符。

## `undef` name

移除 `name` 的定义使其未定义。

除了上述宏外，以下定义可用：`Alpha`, `Beta`, ..., `Omega`（与 `ALPHA`, `BETA`, ..., `OMEGA` 相同），`ldots`（基线上的三个点）以及 `dollar`。

## 字体

`eqn` 通常使用至少两种字体来设置公式：用于字母的斜体字体和用于其他所有内容的正体字体。现有 `font` 命令更改作为斜体的字体。默认是 `I`。用于正体的字体可以使用新的 `grfont` 命令更改。

### `grfont` f

将正字体设置为 `f`。

斜体原语使用 `gfont` 设置的斜体字体；正体原语使用 `grunt` 设置的正体字体。还有一个 `gbfont` 命令，更改粗体原语使用的字体。

可以使用上述的 `chartype` 命令控制哪些字符被视为字母（因此设置为斜体）。字母类型会导致字符设置为斜体类型。数字类型会导致字符设置为正体类型。

### 文件

`u+2n`

```
/usr/share/groff/1.22.3/tmac/eqnrc 初始化文件。
```

## MATHML 模式局限性

MathML 的设计假设它无法知道对其渲染的介质和设备的精确物理特性。它无法像 `troff` 那样对动作和尺寸进行精细控制。因此：

+ `eqn` 参数对生成的 MathML 没有影响。

+ 特殊（special）、向上（up）、向下（down）、向前（fwd）和向后（back）操作无法实现，而是产生 MathML `<error>` 消息。

+ `vcenter` 关键字被静默忽略，因为在数学轴上中心是 MathML 的默认设置。

+ `eqn` 在 `troff` 中设置额外巨大的字符（特别是积分号）可能看起来太小，需要手动调整它们的 `<style>` 包装器。

与其在 `troff` 模式下一样，MathML 模式下的 `eqn` 在显示公式处保留 `.EQ` 和 `.EN` 分隔符，但不会在内联公式周围产生显式分隔符。然而，它们可以被识别为以 `<math>` 开头并以 `</math>` 结尾且不跨行边界的字符串。

见 BUGS 部分查看 `eqn` 特定的翻译限制。

# 错误

行内公式的大小根据输入行开始时的当前字号设置。

在 MathML 模式下，`mark` 和 `lineup` 特性不起作用。理论上，这些可以通过 `<maligngroup>` 元素来实现。

在 MathML 模式下，每个数字字面量的每个数字都会获得一个独立的 `<mn></mn>` 对，而小数点则被标记为 `<mo>:</mo>`。这在规范中是允许的，但效率低下。

### 参见

`groff(1)`, `troff(1)`, `pic(1)`, `groff_font(5)`, 《The TeXbook》

# 复制

Copyright © 1989-2014 Free Software Foundation, Inc.

在确保所有副本上均保留版权声明、本副本以及本许可声明的情况下，允许制作并分发本手册的逐字副本。

在满足逐字复制的条件下，允许复制和分发本手册的修改版本，前提是整个生成的作品必须按照与此相同的许可声明条款进行分发。

在满足上述修改版本的条件下，允许复制和分发本手册的其他语言译本，但该许可声明可以包含在由自由软件基金批准的译本中，而不是原始英文版。

`errstr` - 查找错误代码

### 概要

```
openssl errstr error_code
```

### 描述

有时应用程序不会加载错误信息，只有数字形式可用。可以使用 `errstr` 工具显示十六进制代码的含义。十六进制代码是第二个冒号之后的十六进制数字。

## 示例

错误代码：

`27594:error:2006D0D0:lib(32):func(109):reason(128): bss_file.c:107:`

可以通过以下命令显示：

`openssl errstr 2006D0D0`

产生错误消息：

`error:2006D0D0:BIO routines:BIO_new_file:no such file`

### 参见

`err(3)`, `ERR_load_crypto_strings(3)`, `SSL_load_error_strings(3)`

`escputil` - 维护 Epson Stylus 喷墨打印机

### 概要

```
escputil [options]
```

### 描述

`escputil` 是一个用于对 Stylus 喷墨打印机执行维护任务的命令行工具。这些任务包括头对齐、头清洗、喷嘴检查和墨水位获取。

### 选项

`escputil` 接受以下参数：

- `-P`, `--printer-name`

  指定打印机名称。默认为 `lp0`。

- `-r`, `--raw-device`

  指定设备名称而不是通过打印机进行。

- `-m`, `--model`

  指定打印机型号。

- `-u`, `--new`

  打印机是新的。

- `-S`, `--short`

  获取打印机名称。

- `-C`, `--choices`

  指定数量。

- `-p`, `--patterns`

  指定组数。

- `-c`, `--clean-head`

  清洁打印头。

- `-n`, `--nozzle-check`

  打印喷嘴测试。

- `-a`, `--align-head`

  对齐打印头。

- `-i`, `--ink-level`

  从打印机获取墨水位。

- `-d`, `--identify`

  查询打印机的制造和型号信息。

- `-o`, `--align-color`

  对齐打印头。

- `-s`, `--status`

  获取状态。

- `-l`, `--license`

  显示此程序的许可/保修条款。

- `-M`, `--list-models`

  列出支持的打印机型号。

- `-h`, `--help`

  显示所有命令行选项列表。

- `-q`, `--quiet`

  抑制横幅。

# 错误

USB 连接的打印机有时无法识别或返回墨水位。你可能需要重复执行命令。这可能是 `escputil` 中的一个计时问题，而不是打印机的缺陷。

如果打印机在开机时正在执行自检或头清洗，则识别和墨水位命令将超时，尽管打印机成功接收了命令。当打印机静默时，需要重新发布命令。

### 作者

Robert Krawitz.

# 版版权

Copyright © 2000 Robert Krawitz (rlk@alum.mit.edu)

本程序是自由软件；你可以根据自由软件基金发布的《通用公共许可证》条款对其进行重新分发和/或修改，遵循该许可证的第 2 版本或（根据你的选择）任何更高版本。

# 其他信息

贡献此工具的 Gutenberg 项目主页位于 http://gimp-print.sourceforge.net/

### 参见

`lp(4)`, `tunelp(8)`.
