
软件通过存储库（`repositories`）发布。所有已知仓库都支持软件包签名。签名使用公钥技术来证明软件包是由仓库发布的的，且自应用签名以来未发生过更改。这可以防止安装在您下载之前创建后可能被恶意篡改的软件。

使用过多的仓库、不可信的仓库或带有未签名软件包的仓库会增加向系统中引入恶意或存在漏洞代码的风险。在向 `yum`/`software update` 添加仓库时请务必小心。

# 第 7 章 系统审计

Linux 审计（Audit）系统提供了一种跟踪系统上安全相关信息的方法。根据预配置的规则，Audit 会生成条目，尽可能尽可能记录有关系统正在发生的事件的信息。这些信息对于任务关键型环境至关重要，用于确定违反安全策略的者及其所执行的操作。Audit 并不会为您的系统提供额外的安全性；相反，它可以用于发现系统上安全策略的违规行为。这些违规行为可以通过 SELinux 等额外的安全措施进一步防止。

以下列表总结了 Audit 能够在日志文件中记录的一些信息：

- 主体（subjects）和对象（objects）的敏感性标签。
- 事件与触发该事件的用户身份的关联。
- 对 Audit 配置的所有修改以及对 Audit 日志文件的访问。
- 所有身份验证机制的使用（如 SSH、Kerberos 等）。
- 对任何受信任数据库（如 `/etc/passwd`）的更改。
- 向系统或从系统导入/导出信息的尝试。
- 根据用户身份、主体和对象标签以及其他属性包含或排除事件。

使用 Audit 系统也是许多安全相关认证的要求。Audit 的设计旨在满足或达到以下认证或合规指南的要求：

- 受控访问保护特性文件 (CAPP)
- 标记安全保护特性文件 (LSPP)
- 规则集基本访问控制 (RSBAC)
- 国家工业安全计划操作手册 (NISPOM)
- 联邦信息安全管理法 (FISMA)
- 支付卡行业数据数据安全标准 (PCI-DSS)
- 安全技术实施指南 (STIG)

Audit 还通过：

- 被国家信息保证伙伴关系 (NIAP) 和最佳安全工业 (BSI) 评估。
- 在 Red Hat Enterprise Linux 4 上通过了控制访问保护特性文件 / 评估保证级别 4+ (CAPP/EAL4+) 。
- 在 Red Hat Enterprise Linux 5 上通过了 LSPP/CAPP/RSBAC/EAL4+ 。
- 在 Red Hat Enterprise Linux 6 上通过了操作系统保护特性文件 / 评估保证级别 4+ (OSPP/EAL4+) 。

## 用例

### 监控文件访问

Audit 可以跟踪文件或目录是否被访问、修改、执行，或者文件的属性是否被更改。这非常有用，例如可以检测对重要文件的访问，并在这些文件损坏时提供审计追踪（Audit trail）。

### 监控系统调用

可以配置 Audit 在每次使用特定系统调用时生成日志条目。例如，可以通过监控 `setimeofday`、`clock_adjtime` 和其他时间相关的系统调用来跟踪系统的更改。

### 记录用户运行的命令

由于 Audit 可以跟踪文件是否被执行，可以定义许多规则来记录特定命令的每次执行。例如，可以为 `/bin` 目录下的每个可执行文件定义规则。生成的日志条目随后可以通过用户 ID 进行搜索。

### 记录安全事件

`pam_ock` 认证模块能够记录登录失败。Audit 也可以设置为记录登录尝试，并提供有关尝试登录用户的额外信息。

### 搜索事件

Audit 提供了 `ausearch` 工具，可以根据多种条件过滤日志条目并提供完整的审计追踪。

### 运行摘要报告

`aureport` 工具可用于生成记录事件的报告（以及其他）。系统管理员随后分析这些报告并调查可疑活动。

### 监控网络访问

可以配置 `iptables` 和 `ables` 工具触发 Audit 事件，允许管理员监控网络访问。

> 注意
>
> 系统性能取决于 Audit 收集的信息量。

## 7.1. 审计架构

Audit 系统由两部分组成：用户空间应用程序和工具，以及内核系统调用处理。内核组件接收来自用户空间的系统调用，并通过三个过滤器之一进行过滤：用户、任务或退出。一旦系统调用通过这些过滤器之一，将根据 Audit 规则配置通过排除过滤器，发送到 Audit 守护进程进行进一步处理。图 7.1 “审计架构”说明了这一过程。

![](img/fa49fe194038627f7baabbe849816a0e_150_0.png)

图 7.1 审计架构

用户空间的 Audit 守护进程从内核收集并在日志文件中创建条目。其他 Audit 用户空间工具与 Audit 守护进程、内核审计组件或 Audit 日志文件交互：

- `audisp` —— Audit 分发器守护进程与 Audit 守护进程交互，并将事件发送到其他应用程序进行进一步处理。该进程的目的是提供一种插件机制，以便实时分析程序可以与 Audit 事件交互。
- `auditctl` —— Audit 工具与内核审计组件交互，以控制事件生成过程许多设置和参数。
- 剩余的 Audit 工具以 Audit 日志文件内容作为输入，并根据需求生成输出。例如，`aureport` 工具生成所有记录事件的报告。

## 7.3.1. 为 CAPP 环境配置 auditd

默认的 `auditd` 配置适用于大多数环境。然而，如果你的环境必须满足受控访问保护配置文件（CAPP）设置的标准（而 CAPP 是通用标准（Common Criteria）认证的一部分），则必须对 Audit 守护进程进行以下设置：

- 存放 Audit 日志文件的目录（通常为 `/var/log/audit/`）应该位于独立的分区上。这可以防止其他进程消耗该目录的空间，并为 Audit 守护进程提供对剩余剩余的准确检测。
- `max_log_file` 参数指定单个 Audit 日志文件的最大大小，必须设置该参数，以充分利用存储 Audit 日志文件的分区上的可用空间。
- `max_log_file_action` 参数定义当达到 `max_log_file` 限制时采取的操作，应将其设置为 `keep_logs` 以防止 Audit 日志被覆盖。
- `space_left` 参数指定磁盘上的空闲空间，当达到该空间时触发 `space_left_action` 参数设置的操作，必须设置为一个数值，以便让管理员有足够的时间响应并释放空间。`space_left` 的值取决于 Audit 日志生成的速率。
- 建议将 `space_left_action` 参数设置为 `email` 或 `exec`，并带有适当的通知方法。
- `admin_space_left` 参数指定触发 `admin_space_left_action` 操作的绝对最小空闲空间，必须设置为一个允许管理员执行操作留有足够空间的值。
- `admin_space_left_action` 参数必须设置为 `single`，以将系统置于单用户模式并允许管理员释放一些磁盘空间。
- `disk_full_action` 参数指定当存储 Audit 日志文件的分区上没有可用剩余空间时触发的操作，必须设置为 `halt` 或 `single`。这确保了当 Audit 无法记录事件时，系统将关闭或运行在单用户模式下。
- `disk_error_action` 参数指定在存储 Audit 日志文件的分区上检测到错误时触发的操作，必须设置为 `syslog`、`single` 或 `halt`，取决于你关于处理硬件故障的本地安全策略。
- `flush` 配置参数必须设置为 `sync` 或 `data`。这些参数确保 Audit 事件数据完全与磁盘上的日志同步。

其余配置选项应根据你的本地安全策略进行设置。

## 7.4. 启动 Audit 服务

一旦正确配置了 `auditd`，即可启动服务以收集 Audit 信息并将其存储在日志文件中。以 root 用户执行以下命令启动 `auditd`：

```bash
# service auditd start
```

可选地，你可以以 root 用户执行以下命令配置 `auditd` 在启动时自动运行：

```bash
# chkconfig auditd on
```

可以通过 `service auditd action` 命令执行多项操作。

## 7.5. 定义 Audit 规则

命令，其中 `action` 可以是以下之一：

- `stop` 停止 `auditd`。
- `restart` 重启 `auditd`。
- `reload` 或 `force-reload` 从 `/etc/audit/auditd.conf` 文件重新加载 `auditd` 的配置。
- `rotate` 轮转 `/var/log/audit/` 目录下的日志。
- `resume` 在之前被挂起后恢复 Audit 事件的记录，例如，当存储 Audit 日志文件的磁盘分区上没有足够的可用空间时。
- `condrestart` 或 `try-restart` 仅当 `auditd` 已经在运行时重启 `auditd`。
- `status` 显示 `auditd` 的运行状态。

Audit 系统基于一组规则运行，这些规则定义了要在日志文件中捕获的内容。可以指定三种类型的 Audit 规则：

- 控制规则（Control rules）允许修改 Audit 系统的行为及其部分配置。
- 文件系统规则（File system rules），也称为监视（watches），对访问操作进行审计。
- Audit 规则可以在命令行中指定，也可以写入 `/etc/audit/audit.rules` 文件。

Audit 规则可以通过 `auditctl` 工具定义，这需要 root 权限。

### 7.5.1. 使用 auditctl 定义 Audit 规则

命令，其中 `action` 可以是以下之一：

- `stop` 停止 `auditd`。
- `restart` 重启 `auditd`。
- `reload` 或 `force-reload` 从 `/etc/audit/auditd.conf` 文件重新加载 `auditd` 的配置。
- `rotate` 轮转 `/var/log/audit/` 目录下的日志。
- `resume` 在之前被挂起后恢复 Audit 事件的记录，例如，当存储 Audit 日志文件的磁盘分区上没有足够的可用空间时。
- `condrestart` 或 `try-restart` 仅当 `auditd` 已经在运行时重启 `auditd`。
- `status` 显示 `auditd` 的运行状态。

#### 控制规则

控制规则允许修改 Audit 系统的行为及其部分配置。

- `b` 设置单个 Audit 日志文件的最大大小，例如：

```bash
auditctl -b 8192
```

- `f` 设置检测到错误时执行的操作，例如：

```bash
auditctl -f 2
```

- `e` 启用或禁用 Audit 系统，例如：

```bash
auditctl -e 2
```

- `r` 设置每秒生成的速率，例如：

```bash
auditctl -r 0
```

- `s` 报告 Audit 系统的状态，例如：

```bash
auditctl -s
AUDIT_STATUS: enabled=1 flag=2 pid=0
lost=0
```

- `l` 列出所有已加载的 Audit 规则，例如：

```bash
auditctl -l
LIST_RULES: exit, always watch=/etc/localtime perm=wa
LIST_RULES: exit, always watch=/etc/group perm=wa
LIST_RULES: exit, always watch=/etc/passwd perm=wa
LIST_RULES: exit, always watch=/etc/gshadow perm=wa
```

- `D` 删除所有已加载的 Audit 规则，例如：

```bash
auditctl -D
No rules
```

#### 文件系统规则

文件系统规则，也称为监视（watches），对访问操作进行审计。

要定义文件系统规则，使用以下语法：

```bash
auditctl -w path_to_file -p permissions -k key_name
```

其中：

- `path_to_file` 是被审计的文件或目录。
- `permissions` 是记录的权限：
  - `r` 对文件或目录的读取权限。
  - `w` 对文件或目录的写入权限。
  - `x` 对文件或目录的执行权限。
  - `a` 文件属性的更改。
- `key_name` 是可选字符串，有助于识别是哪个规则或规则集产生了特定的日志条目。

#### 示例 7.1. 文件系统规则

要定义一个记录 `/etc/passwd` 文件所有访问和属性变化的规则，执行以下命令：

```bash
# auditctl -w /etc/passwd -p -k passwd_changes
```

注意 `-k` 参数是任意的。

要定义一个记录 `/etc/selinux/` 目录下所有文件所有访问和属性变化的规则，执行以下命令：

```bash
# auditctl -w /etc/selinux/ -p wa -k selinux_changes
```

要定义一个记录执行 `/sbin/insmod` 命令（该命令向 Linux 内核插入模块）的规则，执行以下命令：

```bash
# auditctl -w /sbin/insmod -p x -k module_insertion
```

## 示例 7.2. 系统调用规则

要定义一个规则，当程序使用 `adjex` 或 `settimeofday` 系统调用时创建一个日志条目，系统使用 64 位架构，执行以下命令：

```bash
# auditctl -a always,exit -F arch=b64 -S adjex -S settimeofday -k time_change
```

要定义一个规则，当 ID 等于或大于 500 的系统用户删除或移除文件时创建一个日志条目（使用 -F audit=424967295 选项排除 UID 不为 0 的用户），执行以下命令：

```
# auditctl -a always,exit -S unlink -S rename -S renameat -F audit=500 -F audit=424967295 -k delete
```

也可以使用调用规则语法定义文件系统规则。以下命令创建的系统调用规则与 `-w /etc/shadow -p wa` 文件规则类似：

```bash
# auditctl -a always,exit -F path=/etc/shadow -F perm=wa
```

## 7.5.2. 在 /etc/audit/audit.rules 文件中定义持久审计规则和控制

要定义重启后依然有效的审计规则，必须将其包含在 `/etc/audit/audit.rules` 文件中。该文件使用相同的 `auditctl` 命令行语法来指定规则。任何空行或跟随井号 (`#`) 的文本都会被忽略。

`auditctl` 命令还可以使用 `-R` 选项从指定文件读取规则，例如：

```bash
# auditctl -R /usr/share/doc/audit-version/stig.rules
```

## 定义控制规则

文件可以包含以下修改 Audit 系统行为的控制规则：`-b`, `-D`, `-e`, `-f` 和 `-r`。有关这些选项的更多信息，请参阅第 7.5.1 节，“定义控制规则”。

### 示例 7.3. audit.rules 中的控制规则

```bash
# 删除所有之前的规则
-D

# 设置缓冲区大小
-b 8192

# 使配置不可变 -- 修改审计规则需要重启
-e 2

# 发生故障时触发内核崩溃
-f 2

# 每秒最多生成 100 条审计消息
-r 100
```

## 定义文件系统和系统调用规则

文件系统和系统调用规则使用 `auditctl` 语法定义。第 7.5.1 节，“使用 auditctl 工具定义审计规则”中的示例可以用以下规则文件表示：

### 示例 7.4. audit.rules 中的文件系统和系统调用规则

```bash
-w /etc/passwd -p wa -k password_changes
-w /etc/selinux -p wa -k selinux_changes
-w /sbin/insmod -p x -k module_insertion

-a always,exit -F arch=b64 -S adjimetime -S timeofday -k time_change
-a always,exit -S unlink -S rename -F audit>=500 -F auid=4294967295 -k delete
```

## 预配置规则文件

在 `/usr/doc/audit-version/` 目录下，audit 包为各种认证标准提供了一组预配置规则文件：

- **nisnorm.rules** — 满足《国家工业安全计划操作手册》第 8 章要求的审计规则配置。
- **capp.rules** — 满足[受控访问保护配置文件](CAPP)要求的审计规则配置，该配置是通用标准（Common Criteria）认证的一部分。
- **lspw.rules** — 满足[标记安全保护配置文件](LSPP)要求的审计规则配置，该配置是通用标准认证的一部分。
- **stig.rules** — 满足安全技术实施指南（STIG）要求的审计规则配置。

要使用这些配置文件，请对原始的 `/etc/audit/audit.rules` 文件进行备份，并将选择的配置文件覆盖到 `/etc/audit/audit.rules` 文件：
