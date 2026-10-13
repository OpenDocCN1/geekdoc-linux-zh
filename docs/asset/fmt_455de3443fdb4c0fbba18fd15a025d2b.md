
- `gunzip` 解压缩文件。
- `gzcat` 解压缩文件。
- `gzcomp` 比较压缩文件。
- `gzdiff` 比较压缩文件。
- `gzexe` 原地压缩可执行文件。
- `gzforce` 对所有 gzip 文件强制使用 `.gz` 扩展。
- `gzip` 压缩文件。
- `gzmore` 用于查看压缩文本的过滤器。
- `gznew` 将 `.z` 文件重新压缩为 `.gz` 文件。
- `kpasswd` 更改用户的 Kerberos 密码。
- `ktutil` Kerberos 密钥表维护命令。

# 23 引言

- `ldap`: 作为命名库的 LDAP。
- `ldaplist`: 从 LDAP 目录服务搜索并列出命名信息。
- `llc2_autoconfig`: 生成 LLC2 配置。
- `llc2_config`: 配置 LLC2 接口参数。
- `llc2_stats`: LLC 部分、SAP 和连接统计。
- `mailp`, `digestp`, `filep`, `filofaxp`, `franklinp`, `newsp`, `timemanp`, `timesysp`
- `mdb`: 模块化调试器。
- `mixerctl`: 音频混合器控制命令行应用程序。
- `mp` 文本到 PDL 美化过滤器。
- `nca`, `snca`: Solaris 网络缓存和加速器 (NCA)。
- `ncab2clf` 将二进制日志文件转换为常见日志文件格式。
- `ncakmod` 启动或停止 NCA 内核模块。
- `netscape`: 启动 Solaris 版 Netscape Communicator。
- `nisopasscess`: NIS+ 访问控制管理命令。
- `perl`: 实用提取和报告语言。
- `pfexec`, `pfscsh`, `pfcksh`: 在配置文件中执行命令。
- `praliases` 显示系统邮件别名。
- `profiles` 打印用户的执行配置。
- `roles`: 打印授予用户的角色。

## Solaris 8 版本中移除的命令

- `appletviewer`: 查看 Java applets。
- `makekey`: 生成加密密钥。
- `native2ascii`: 原生到 ASCII 转换器。
- `pcmapkeys`: 为文本模式下的 PC 控制台设置键盘扩展映射和扫描码翻译。
- `rmic`: Java RMI 存根编译器。
- `rmireistry` 注册远程 Java 对象。
- `serialver` 显示序列版本。

# 24 引言

## Solaris 9 版本中新增的命令

`allocate`: 设备分配。
`am`: 运行抽象机器。
`cdrw`: CD 读写写。
`deallocate`: 设备去分配。
`ftpcount`: 显示用户数。
`ftpwho`: 显示当前类。
`list_so`: 页面大小。
`newtask`: 创建任务。
`ppgs`: 优选页大小。
`prctl`: 资源控制。
`preap`: 被父进程收割。
`rmformat`: 可移动介质。
`pmio`: 转换 cpio 归档。
`runat`: 在空间中执行。
`scp`: 安全复制。
`setgrp`: 组 ID。
`sftp`: 安全传输。
`ssh-add`: 添加密钥。
`ssh-agent`: 身份验证代理。
`ssh-http`: HTTP 代理。
`ssh-keygen`: 密钥生成。
`ssh-socks`: SOCKS 代理。

## Solaris 9 版本中移除的命令

`adb`: 通用调试器。
`case`, `switch`, `select`: shell 函数。
`for`, `foreach`, `repeat`: shell 函数。
`if`: 评估条件。
`jar`: 归档工具。
`javac`: Java 编译器。
`javadoc`: API 文档生成器。
`javah`: 封装。
`javald`: 类文件反汇器。
`javap`: 类文件。
`jre`: 运行时解释器。
`kerberos`: 安全系统。
`ksrvtgt`: 获取存储票据。
`loadfont`: 显示或更改显卡信息。
`smart2cfg`: Smart-2 EISA/PCI 数组 ioctl 命令。
`smart2SL`: 执行条件的 shell 函数。
`while`:

## A

## `acctcom` — 搜索并打印统计文件

### 语法

`/usr/bin/acctcom [-abfhkmqrtv] [-C sec] [-e time] [-E time] [-g group] [-H factor] [-I chars] [-l line] [-n pattern] [-o output-file] [-O sec] [-s time] [-S time] [-u user] [-filename...]`

### 描述

`acctcom` 是构建统计系统时使用的结构化工具集之一。使用 `acctcom` 命令搜索由 `acct(4)` 创建的统计文件并将选定的记录到标准输出。

`acctcom` 读取文件、标准输入或 `/var/adm/pacct`，其格式由 `acct` 定义，并将选定的记录写入标准输出。每个记录代表一次进程的执行。输出显示命令、用户、TTY、开始时间、结束时间、CPU (SEC)、平均大小 (K)，以及可选的 F (`fork()/exec()` 标志：1 为没有 exec 的 fork())、STAT（系统退出状态）、H 因子、KCORE、CPU 因子、CHARS 传输和 OCKS（总读写记录）

当以超级权限执行命令时，命令名称前会加上井号 (#)。当进程未关联终端时，TTY 字段将显示 ?。

当你不指定文件名且标准输入与终端或 `/dev/null` 关联（如在 shell 中使用 & 时）时，读取 `/var/adm/pacct`。

任何文件名参数都按其顺序读取。每个文件通常按正向读取，即按进程完成时间的顺序顺序排列。文件

# 28

### `acctcom`

`/var/adm/pacct` 通常是当前要检查的文件；忙碌的系统可能需要多个文件，其中所有当前文件都位于 `/var/adm/pacct` 中。`acctcom` 仅报告已终止的进程。活动进程请使用 `ps(1)`。

### 选项

- `-a` 显示所选进程的某些平均统计数据。在输出记录后打印统计信息。
- `-b` 反向读取，先显示最新的命令。当从标准输入读取时，此选项无效。
- `-C sec` 仅显示总 CPU 时间（系统时间 +用户时间）超过 `sec` 秒的进程。
- `-e time` 显示在 `time` 刻或在此之前存在的进程。
- `-E time` 显示在 `time` 刻或在此之前结束的进程。通过对 `-S` 和 `-E` 使用相同的时间，可以显示在该时间点上存在的进程。
- `-f` 在输出中打印 `fork()/exec()` 标志并显示退出状态列。以八进制格式显示数值输出。
- `-g group` 仅显示属于某个组的进程。你可以通过组 ID 或组名来指定该组。
- `-h` 代替内存大小，显示进程在执行期间消耗的总可用 CPU 时间的比例。该占用因子（hog factor）的计算方法为 (总 CPU 时间)/(已通过时间)。
- `-H factor` 仅显示超过 `factor` 的进程，其中 `factor` 是如上文 `-h` 中解释的占用因子。
- `-i` 在输出中打印包含 I/O 计数的行。
- `-I chars` 仅显示传输字符超过截断值 `chars` 的进程。
- `-k` 代替内存大小，显示总 kcore-分钟。
- `-1 line` 仅显示属于终端 `/dev/term/line` 的进程。
- `-m` 显示平均核心大小（默认值）。
- `-n pattern` 显示匹配模式的命令，模式可以是如 `regcomp(3)` 中的正则表达式，但加号或多次出现的情况除外。
- `-o output-file` 将选定的进程记录按输入数据格式复制到 `output-file`，抑制到标准输出的打印。
- `-O sec` 仅显示 CPU 系统时间超过 `sec` 秒的进程。
- `-q` 不打印任何输出记录，仅配合 `-a` 选项打印平均统计数据。
- `-r` 显示 CPU 因子（用户时间/(系统时间 + 用户时间)）。
- `-s time` 显示在 `time` 刻或之后存在的进程，格式为 hr:min(sec)。
- `-S time` 显示在 `time` 刻或之后启动的进程。

### `acctcom`

# 29

- `-t` 分别显示系统和用户 CPU 时间。
- `-u user` 仅显示属于用户用户的进程：你可以指定用户 ID、转换为用户 ID 的登录名、`#`（指定以超级用户权限执行的进程）或 `?`（指定与未知用户 ID 关联的进程）。
- `-v` 从输出中排除列标题。

### 示例

以下示例开启了计时，使用不带参数的 `acctcom` 命令列出 `/var/adm/pacct` 文件的内容，然后关闭计时。注意，用于开启计时的 `acctcom` 前面有一个美元符号，因为它是由超级用户运行的。

```
castle su
cast#/usr/lib/acct/acctcom /var/adm/pacct
castle exit
cast acctcom
```
