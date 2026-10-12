
在本章中，我们将检查创建更安全的 `Linux` 安装的选项。我们使用“加固”一词表示减少系统破解可能性而采取的过程和程序。讨论的话题包括：

- `Linux` 系统日志
- 可插身份验证模块 (Pluggable Authentication Modules)
- 使用 `sudo` 委托超级用户权限
- 使用 `TCP_wrappers` 保护 Internet 服务
- 使用 `Bastille` 加固 `Linux`

## 3.1 `Linux` 系统日志

`Linux` 日志由 `syslog` 工具控制。`syslogd` 守护进程接受来自各种来源的输入日志消息，例如：

- `Linux Kernel`
- 系统服务（如 `mail`, `cron`, `PAM`）
- 应用程序

除了消息文本外，输入日志消息还指示：

- 生成消息的服务或应用程序（`facility`）
- 消息的严重程度（`level`）

`syslog` 工具向输入消息中添加时间戳、主机标识符和进程标识符，然后根据 `/etc/syslog.conf` 配置文件中定义的规范处理消息。消息的 `facility` 和 `level` 统称为 `selector`。

### 3.1.1 配置 `syslogd`

`/etc/syslog.conf` 文件用于确定输入消息的处理方式。`/etc/syslog.conf` 中的条目格式如下：

`facility.level action`

定义的 `syslog facilities` 包括：

| Facility | 描述 |
| :--- | :--- |
| `auth` | 身份验证消息（已弃用） |
| `authpriv` | 身份验证消息 |
| `cron` | 来自 `cron` 的消息 |
| `daemon` | 来自系统守护进程的消息 |
| `kern` | 内核消息 |
| `lpr` | 打印服务消息 |
| `mail` | 邮件服务消息 |
| `mark` | 内部 `syslog` 时间戳消息 |
| `news` | 新闻服务消息 |
| `syslog` | `syslog` 消息 |
| `user` | 用户应用程序消息 |
| `uucp` | `uucp` 消息 |
| `local0-local7` | 来自本地定义的服务 |

定义的 `syslog levels` 包括：

- `emerg`: 致命系统错误
- `alert`: 需要立即注意的错误
- `crit`: 禁用服务的错误
- `err`: 禁用系统组件的错误
- `warning`: 警告
- `info`: 信息
- `debug`: 调试消息

`action` 指明 `syslog` 将消息定向到何处。`syslog` 可以报告：

- **日志文件**
  `action` 指定日志文件名。通常为所有 `syslog` 消息指定 `/var/log/messages`。如果文件名以 `-` 字符开头，`syslog` 将在每次写入后不同步文件。

- **远程主机**
  `action` 可以指定远程主机名或 `IP` 地址。在这种情况下，`@` 在 `IP` 地址或主机名之前。日志消息随后将定向到该主机上的 `syslog`。我们将在 3.1.2 “使用中央日志服务器”中讨论向远程主机日志。

- **控制台**
  要将日志定向到控制台，请指定 `/dev/console` 为 `action`。

- **用户登录**
  要将日志定向到用户，请指定用户名作为 `action`。可以指定用户列表（每个用户名用逗号 `,` 分隔），`action` 指定为 `*`，日志将定向到所有用户。

- **命名管道**
  要将日志消息定向到命名管道，在管道名称前指定 `|` 前缀。

示例 3-1 展示了一个示例 `syslog` 配置文件。

### 3.1.2 使用中央日志服务器

将 `syslog` 消息重定向到中央日志服务器的优势包括：

- **简化日志管理**
  通过中央日志服务器，可以从一个位置查看并备份来自所有 `Linux` 机器的日志文件。

- **增强日志的完整性**
  如果 `Linux` 服务器上发生入侵，攻击者可能会尝试从日志文件中删除任何关于入侵的记录。中央日志服务器可以进行加固和严格控制。如果日志文件被修改，中央日志服务器可以保留一个未被修改的版本。

要配置 `syslog` 以接收远程传入的日志消息，请在 `syslog` 中使用 `-r` 选项。对于 `SLES`，请在 `/etc/sysconfig/syslog` 的 `SYSLOG_PARAMS` 变量中添加 `-r`：

```
# 如果不为空：则为 syslogd 的参数
#### 例如 SYSLOG_PARAMS="-r -s my.domain"
#
SYSLOG_PARAMS="-p"
```

要使更改生效，必须重启 `syslog`。重启时，`syslog` 会记录对日志文件 (`/var/log/messages`) 的更改：

`Mar 24 10:35:31 lnnxu2 syslog 1.4.1: restart (remote reception)`

> 注意：要配置远程主机连接中央日志服务器，请在主机的 `/etc/syslog.conf` 文件中使用 `@` 语法（指定中央日志服务器的 `IP` 地址或主机名）。

要测试新配置，使用 `logger` 命令。例如，对于远程主机，使用命令：

```
logger -p syslog.warning "test[123]: testing remote logging"
```

这将在中央日志服务器的日志文件中生成一条消息：

`May 24 10:56:56 lnnxu3 root:test[123]: testing remote logging`

> 注意：`logger` 命令的 `-p` 选项指定了消息设施（`facility`）和优先级（`priority`）。

## 3.2 可插入认证模块 (PAM)

`Linux` 中用于用户认证的默认机制使用可插入认证模块 (`PAM`)。`PAM` 为 `login`、`FTP`、`Telnet` 和 `SSH` 等常用服务提供集中化认证。`PAM` 使用动态链接库 (`DLLs`) 实现。可以使用 `PAM` 配置文件为感知 `PAM` 的服务自定义认证。图 3-1 展示了 `PAM` 的操作。

![](img/a2760634ecd5eb26c25e81867e88d740_44_0.png)

图 3-1 `PAM` 架构

每个感知 `PAM` 的应用程序的认证均通过 `/etc/pam.d` 目录下的配置文件配置（文件名表示其所配置的服务）。`PAM` 模块实现用户认证；默认情况下，`PAM` 模块位于 `/lib/security` 目录。某些 `PAM` 模块读取位于 `/etc/security` 目录的全局配置文件。

### 3.2.1 `PAM` 配置文件

`PAM` 配置文件由如下形式的行组成：

```
module-type control-flag module-path arguments
```

接下来的章节将描述每个字段。

#### `PAM` 模块类型

支持四种类型的认证机制（称为模块类型）。表 3-1 描述了每种模块类型。

**表 3-1 `PAM` 模块类型**

| 类型 | 描述 |
|---|---|
| `auth` | 用于根据用户名和密码认证用户 |
| `account` | 用于根据账户策略（如时间段）授予或拒绝访问 |
| `password` | 用于授权更新用户密码 |
| `session` | 用于在会话建立之前应用设置 |

> 注意：任何 `PAM` 模块类型都可以指定多行。这被称为模块堆栈（module stacking）。在这种情况下，每个模块按照从先到后的顺序执行。最终认证取决于 `PAM` 控制标志。

#### `PAM` 控制标志

`PAM` 控制标志根据模块的返回代码决定认证的如何进行。表 3-2 列出了可能的标志。

**表 3-2 `PAM` 控制标志**

| 标志 | 动作 |
|---|---|
| `required` | 必须的模块必须返回成功代码，认证才能成功。在任何情况下，所有堆栈模块都会被执行，且只有当这些模块也成功时，最终认证才会成功。 |
| `requisite` | 必要的模块在认证失败时立即终止。在成功时执行堆栈模块。 |
| `sufficient` | 表示一个成功的返回代码已足够完成认证。如果之前的 `required` 模块已失败，则认证将失败。 |
| `optional` | 可选模块不被认为是至关重要的。`PAM` 忽略成功或失败代码。 |

#### `PAM` 模块路径

模块路径字段指定用于实现 `PAM` 检查的 `DLL` 名称。名称可以指定为绝对路径或相对路径（在这种情况下，假设模块位于 `/lib/security` 目录）。

#### `PAM` 模块参数

`PAM` 模块参数通常是可选的，并被特定的 `PAM` 模块识别。表 3-3 显示了一些典型参数。

**表 3-3 `PAM` 参数**

| 参数 | 描述 |
|---|---|
| `debug` | 使用 `syslog` 调用将调试信息记录到系统。 |
| `audit` | 使用详细调试。 |
| `nullock` | 允许使用空密码。默认是要求非空密码。 |
| `no_delay` | 默认情况下，如果认证失败，模块将在等待 1 秒后提示新密码。此参数导致模块立即提示新密码。 |
