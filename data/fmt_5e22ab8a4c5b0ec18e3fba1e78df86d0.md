
## `echo b > /proc/sysrq-trigger`

```bash
echo b > /proc/sysrq-trigger
```

以下是可用命令：

| 命令键 | 功能 |
|---|---|
| `b` | 立即重启系统。不会同步或卸载磁盘。这可能会导致数据损坏！ |
| `c` | 通过空指针引用引发系统崩溃。如果配置了 `kdump` 则会拍摄转储。 |
| `d` | 显示所有持有的锁。 |
| `e` | 向除 `init` 外的所有进程发送 `SIGTERM` 信号。 |
| `f` | 调用 `o` 来杀死占用内存的进程。 |
| `g` | 用于内核调试器 (`kgdb`)。 |
| `h` | 显示帮助。记住这个选项！ |
| `i` | 向除 `init` 外的所有进程发送 `SIGKILL` 信号。 |
| `j` | 使用 `FREEZE` `ioctl` 冻结文件系统。 |
| `k` | 杀死当前虚拟控制上的所有程序。允许从控制台安全登录，因为杀死了尝试获取你键盘输入的恶意软件，例如。 |
| `l` | 显示活动 `CPU` 的堆栈跟踪。 |
| `m` | 将内存信息转储到控制台。 |
| `n` | 你可以使用此为实时任务设置 `nice` 值。 |
| `o` | 关闭系统并关闭（如果配置并支持）。 |
| `p` | 将当前寄存器和标志转储到控制台 |
| `q` | 列出每个 `CPU` 所有已启动的 `hrtimes`（`timer_list` 定器除外），带有关于所有时钟设备的详细信息。 |
| `r` | 关闭键盘的原始模式并将其设置为 `XLATE`。 |
| `s` | 尝试同步所有挂载的文件系统，将未写入的数据提交其中。 |

| 架构 | 组合键组合 |
|---|---|
| `x86` | `<Alt><SysRq>s` |
| `Sparc` | `<Alt><SysRq>b` |
| 串口控制台（仅限 `PC`） | `<Alt><SysRq>g` |
| `PowerPC` | `<Alt><SysRq>q` |

![](img/a6dbf749be83c0f947.png)

| 命令 | 功能 |
| --- | --- |
| `t` | 将当前任务列表及其信息转储到控制台。 |
| `u` | 尝试将您的所有文件系统重新挂载为只读卷。 |
| `v` | 这将导致 `ETM` 缓冲区转储（`ARM` 架构特定）。 |
| `w` | 转储所有处于不可中断（阻塞）状态的任务。 |
| `x` | 此命令供 `ppc/powerpc` 上的 `xmon` 直接使用。它会显示 `SPARC64` 上的全局 `PMU` 寄存器。 |
| `y` | 显示全局 `CPU` 寄存器（`SPARC64` 架构特定）。 |
| `z` | 转储 `ftrace` 缓冲区。 |
| `0 - 9` | 这将设置控制台的日志级别，用于控制哪些消息将被打印。数字越大，输出越详细。 |

### 另参

有关关于 `SysRq` 和 `systemd` 的详细信息，请参考以下页面：`https://github.com/systemdaemon/systemd/blob/master/src/linux/Documentation/sysrq.txt`

`Red Hat` 在 `https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Kernel_Crash_Dump_Guide/index.html` 提供了完整的崩溃转储指南。

## 使用 `ABRT`

`ABRT`（自动错误报告工具）是一组工具集，可以帮助用户检测和分析应用程序的崩溃。

### 如何操作

首先，我们将安装必要的软件包，然后查看如何使用这些工具。

### 安装和配置 `abrtd`

让我们安装 `abrt` 并运行它：

1. 通过以下命令行安装 `abrt` 守护进程和工具：
   `yum install -y abrt-cli`

### 加固 `RHEL 7`

2. 现在，通过这些命令启用并启动 `abrt` 守护进程：

```bash
systemctl enable abrtd
systemctl restart abrtd
```

还有更多...

### 使用 `abrt-cli`

执行以下命令列出所有检测到的段错误：

```bash
abrt-cli list
```

输出内容应该是这样的：

```text
abrt-cli list

cored-20151031-7af3d0c8-f00c6f2a-data

Directory:
 /var/tmp/abrt/cpp-2015-10-31-14:14:41-10289
executable:
 /usr/bin/slleep
package:
 libreport-dbus-0.17
time:
 31 Oct 2015 02:42:41 PM CET
user:
 root
```

运行 `abrt-cli report /var/tmp/abrt/cpp-2015-10-31-14:14:41-10289` 在 `Red Hat` 客户门户中创建案例。

显示的路径包含有关该段错误的所有信息。你可以用它来分析出了什么问题，如果你需要 `Red Hat` 的帮助，可以使用 `abrt-cli report` 向 `Red Hat` 支持部门提交报告。

### 更多

当 `RHEL 7` 系统注册到 satellite 卫星时，所有错误都将自动报告到卫星系统。

你可以通过以下方式安装插件来自动报告错误：

- 报告到 `Bugzilla` (`libreport-plugin-bugzilla`)
- 通过 `ftp` 上传 (`libreport-plugin-reportuploader`)
- 报告到 `Red Hat` 支持 (`libreport-plugin-rhtupport`)
- 报告到 `abrt` 服务器 (`libreport-plugin-ureport`)

除了基本的错误报告外，你还可以安装 `abrt-java-connector` 软件包为 `Java` 创建自动错误报告。

### 另参

有关如何使用 `abrt` 工具的更多信息，请参阅 `https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/System_Administrators_Guide/ch-abrt.html`。

## 审计系统

审计系统允许你跟踪系统的安全相关信息。它允许你监控安全事件、文件系统访问、网络访问、用户运行的命令以及系统调用。

### 如何操作

默认情况下，`audit` 是核心包的一部分安装的。因此无需安装。

### 配置集中式 `syslog` 服务器以接收审计日志

执行以下步骤设置 `syslog` 服务器：

1. 在 `syslog` 服务器上，创建一个 `/etc/rsyslog.d/audit_server.conf` 文件，内容如下：
```text
# 通过端口 65514 经 TCP 接收 syslog 审计消息
$Mod imptcp
$InputTCPServerRun 65514
$AllowedSenderTemplate 127.0.0.1, 192.168.1.0/24
$Template HostAudit "/var/log/audit/%%YEAR%%%%%%MONTH%%%%%%DAY-$%HOSTNAME%.audit.log"
$Template auditFormat "$msg\n" local6.*
$HostAudit,auditFormat
```
2. 在 `syslog` 服务器上，按如下方式重启 `rsyslog`：
   `systemctl restart rsyslog`
3. 在客户端上，创建一个 `/etc/rsyslog.d/audit_client.conf` 文件，内容如下：
```text
$Mod impfile
$InputFile /var/log/audit/audit.log
$InputFileTag tag_audit_log
$InputFileState audit_log
$InputFacility local6
$InputFile @syslog.example.com
```
4. 接下来，在客户端上重启 `rsyslog`：
   `systemctl restart rsyslog`

### 加固 `RHEL 7`

某些审计规则可以记录 `/etc/` 下的更改：

```bash
auditctl -w /etc/ -p wa -k changes
```

你可以通过以下命令记录 `/etc/sysconfig` 的活动：

```bash
auditctl -w /etc/sysconfig -p wa -k always
```

查看标记 `changes` 的审计日志：

```bash
ausearch -k changes
```
