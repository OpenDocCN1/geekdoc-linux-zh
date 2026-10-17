
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
