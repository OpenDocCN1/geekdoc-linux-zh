
### `admin_space_left_action`

应设置为 `single`，以将系统置于单用户模式，并允许管理员释放一些磁盘空间。

### `disk_full_action`

指定当存放审计日志文件的分区上没有可用空间时触发的操作，必须设置为 `halt` 或 `single`。这确保了当审计系统无法再记录事件时，系统要么关闭，要么运行在单用户模式下。

### `disk_error_action`

指定在检测到存放审计日志文件的分区上发生错误时触发的操作，必须根据你本地关于硬件故障处理的安全策略设置为 `syslog`、`single` 或 `halt`。

### `flush`

应设置为 `incremental_async`。它与 `freq` 参数配合使用，该参数决定在强制与硬盘进行硬同步之前可以发送到磁盘的记录数量。`freq` 参数应设置为 `100`。这些参数确保了在保持活动突发良好性能的同时，审计事件数据与磁盘上的日志文件保持同步。

其余配置选项应根据你的本地安全策略进行设置。

## 6.4. 启动审计服务

一旦配置了 `auditd`，请启动该服务以收集审计信息并将其存储在日志文件中。作为 root 用户执行以下命令以启动 `auditd`：

```bash
~]# service auditd start
```

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_187_0.png)

**注意**

`service` 命令是正确与 `auditd` 守护进程交互的唯一方式。你需要使用 `service` 命令，以便正确记录 `audit` 值。你只能使用 `systemctl` 命令执行两个操作：`enable` 和 `status`。

要配置 `auditd` 在系统启动时自动启动，请作为 root 用户执行以下命令：

```bash
~]# systemctl enable auditd
```

可以使用 `service auditd action` 命令对 `auditd` 执行其他多种操作，其中 `action` 可以是以下内容之一：

- `stop`

  停止 `auditd`。

- `restart`

  重启 `auditd`。

- `reload` 或 `force-reload`

  从 `/etc/audit/auditd.conf` 文件重新加载 `auditd` 的配置。

- `rotate`

  轮换 `/var/log/audit/` 目录中的日志文件。

- `resume`

  恢复之前暂停的审计事件日志记录，例如，当存放审计日志文件的磁盘分区没有足够的可用空间时。

- `condrestart` 或 `try-restart`

  仅在 `auditd` 已经运行时才重启它。

- `status`

  显示 `auditd` 的运行状态。

## 6.5. 定义审计规则

审计系统运行于一组规则之上，这些规则定义了要在日志文件中捕获的内容。可以指定以下类型的审计规则：

**控制规则**

允许修改审计系统的行为及其部分配置。

**文件系统规则**

也称为文件监视，允许对特定文件或目录的访问进行审计。

**系统调用规则**

允许记录任何指定程序发出的系统调用。

审计规则可以设置为：

- 使用 `auditctl` 工具在命令行上设置。请注意，这些规则在重启后不会持久化。详细信息请参阅第 6.5.1 节，“使用 `auditctl` 定义审计规则”
- 在 `/etc/audit/audit.rules` 文件中设置。详细信息请参阅第 6.5.3 节，“在 /etc/audit/audit.rules 文件中定义持久审计规则和控制项”

### 6.5.1. 使用 auditctl 定义审计规则

`auditctl` 命令允许你控制审计系统的基本功能，并定义决定哪些审计事件被记录在日志中的规则。

> **注意**
>
> 所有与审计服务和审计日志文件交互的命令都需要 root 权限。请确保你作为 root 用户执行这些命令。此外，设置审计服务需要 `CAP_AUDIT_CONTROL`，记录用户消息需要 `CAP_AUDIT_WRITE`。

#### 定义控制规则

以下是一些允许你修改审计系统行为的控制规则：

- `-b`

  设置内核中现有审计缓冲区的最大数量，例如：

  ```bash
  ~]# auditctl -b 8192
  ```

- `-f`

  设置检测到严重错误时执行的操作，例如：

  ```bash
  ~]# auditctl -f 2
  ```

  上述配置在发生严重错误时触发内核恐慌。

- `-e`

  启用或禁用审计系统，或锁定其配置，例如：

  ```bash
  ~]# auditctl -e 2
  ```

  上述命令锁定审计配置。

- `-r`

  设置每秒生成消息的速率，例如：

  ```bash
  ~]# auditctl -r 0
  ```

  上述配置不对生成的消息设置速率限制。

- `-s`

  报告审计系统的状态，例如：

  ```bash
  ~]# auditctl -s
  AUDIT_STATUS: enabled=1 flag=2 pid=0 rate_limit=0 backlog_limit=8192 lost=259 backlog=0
  ```

- `-l`

  列出当前已加载的所有审计规则，例如：

  ```bash
  ~]# auditctl -l
  -w /etc/passwd -p wa -k passwd_changes
  -w /etc/selinux -p wa -k selinux_changes
  -w /sbin/insmod -p x -k module_insertion
  :
  ```

- `-D`

  删除当前已加载的所有审计规则，例如：

  ```bash
  ~]# auditctl -D
  No rules
  ```

#### 定义文件系统规则

要定义文件系统规则，请使用以下语法：

```bash
auditctl -w path_to_file -p permissions -k key_name
```

其中：

- `path_to_file` 是被审计的文件或目录。
- `permissions` 是被记录日志的权限：
  - r – 对文件或目录的读取访问。
  - w – 对文件或目录的写入访问。
  - x – 对文件或目录的执行访问。
  - a – 文件或目录属性的变更。
- `key_name` 是一个可选字符串，有助于识别哪条规则或哪组规则生成了特定的日志条目。

**示例 6.1. 文件系统规则**

要定义一条记录对 `/etc/passwd` 文件的所有写入访问和所有属性变更的规则，请执行以下命令：

```bash
~/# auditctl -w /etc/passwd -p wa -k passwd_changes
```

请注意，`-k` 选项后面的字符串是任意的。

要定义一条记录对 `/etc/selinux/` 目录中所有文件的所有写入访问和所有属性变更的规则，请执行以下命令：

```bash
~/# auditctl -w /etc/selinux/ -p wa -k selinux_changes
```

要定义一条记录执行 `/sbin/insmod` 命令（该命令将模块插入到 Linux 内核中）的规则，请执行以下命令：

```bash
~/# auditctl -w /sbin/insmod -p x -k module_insertion
```

#### 定义系统调用规则

要定义系统调用规则，请使用以下语法：

```bash
auditctl -a action,filter -S system_call -F field=value -k key_name
```

其中：

- `action` 和 `filter` 指定何时记录特定事件。`action` 可以是 `always` 或 `never`。`filter` 指定应用于该事件的哪个内核规则匹配过滤器。规则匹配过滤器可以是以下内容之一：`task`、`exit`、`user` 和 `exclude`。有关这些过滤器的更多信息，请参阅第 6.1 节“审计系统架构”的开头部分。
- `system_call` 通过名称指定系统调用。所有系统调用的列表可以在 `/usr/include/asm/unistd_64.h` 文件中找到。可以将多个系统调用分组到一条规则中，每个系统调用在其各自的 `-S` 选项后指定。
- `field=value` 指定进一步修改规则以基于指定架构、组 ID、进程 ID 等匹配事件的额外选项。有关所有可用字段类型及其值的完整列表，请参阅 `auditctl(8)` man 手册页。
- `key_name` 是一个可选字符串，有助于识别哪条规则或哪组规则生成了特定的日志条目。
