
一旦操作系统类型已知，Samba 需要知道打印机配置文件的位置。打印机配置文件的路径名由全局 `printcap name` 参数指定。Samba 将客户端打印机访问请求与配置文件中列出的队列名称进行匹配。匹配的有效目标包括打印机数据库中定义的所有打印机别名。基于指定操作系统类型的 `printcap name` 默认值包括 BSD 系统的 `/etc/printcap`、AIX 的 `/etc/qconfig` 以及 SYSV 系统的 `lpstat`。在 SYSV 系统的情况下，Samba 调用 `lpstat` 命令以获取可用打印机的列表：

```
printcap name = <printer config file>
```

如果你不想让打印机配置文件中列出的所有打印机都可供客户端访问，请考虑为你的工作组或域使用替代配置文件。使用不同的文件名或路径复制默认打印机配置文件。删除你希望限制访问的打印机定义。将复制的配置文件用作 `printcap name` 参数的值。不要忘记你需要保持驻留在每个文件中的打印机配置同步。

要使可用打印机的集合对浏览可见，请启用全局 `load printers` 参数。默认设置 `yes` 将把打印机配置文件中列出的所有打印机添加到浏览列表。

```
load printers = <yes, no>
```

### 打印共享

打印共享要么使用方括号括起来的显式共享名称定义，要么使用特殊的 `[printers]` 共享。最小的打印共享定义将包括 `path` 参数，指定世界可写排队目录的位置。它还必须设置为 `printable`，否则服务器将不会加载配置。将 `writeable` 参数设置为 `no` 以限制与排队无关的对共享的写入。如果你想允许打印机公开访问，请启用 `guest ok` 参数并验证 `guest` 账户是否设置为已知的 UNIX 账户。如果所选共享名称与 UNIX 打印机配置文件中的条目不匹配，请使用 `printer` 参数指定有效的打印机名称。

```
[print share name]
comment = <text description>
printer = <printcap printer name>
path = <spooling directory>
writeable = no
```

```
guest ok = yes
printable = yes
```

混合打印共享可以在与 `print command` 参数和打印机输入过滤器如 `smbprint` 结合使用时配置为支持其他功能。例如，使用 `HylaFAX` 和 `mgetty+sendfax` 等工具可以将传真作为网络打印功能集成。其他选项包括为图形设置原始打印共享。有关更多信息，请参阅 `Faxing.txt` 和 `Printing.txt` 发行版文档。

**HylaFAX:** http://www.hylafax.org

**mgetty+sendfax:** http://alpha.greenie.net/mgetty/

### `[printers]` 共享

Samba 提供了一种简单机制，使 UNIX 打印机配置文件中识别的所有打印机都可供使用。`[printers]` 共享是一个特殊的 `smb.conf` 部分，类似于第 11 章中讨论的 `[homes]` 共享。当服务器收到 SMB 连接设置请求时，Samba 首先扫描 `smb.conf`，尝试将请求与其中一个具体命名的共享匹配。如果未找到匹配项，它将扫描 `passwd` 数据库，尝试基于客户端用户名查找匹配项。如果未找到匹配项并且配置文件中定义了 `[printers]` 共享，它将扫描 UNIX 打印机配置文件以查找匹配项。如果找到打印机名称匹配，Samba 将授予对通过克隆 `[printers]` 部分定义创建的临时 `[printer name]` 共享的访问权限。示例 12.1 中列出了 `[printers]` 共享的示例。

#### 示例 12.1 示例 `[printers]` 共享

```
[printers]
    path = /var/spool/samba
    writeable = no
    guest ok = yes
    printable = yes
```

### 共享级参数

Samba 提供了一组额外的共享参数，允许你进一步定制单个打印共享的行为。这些参数大多涉及指定命令脚本，这些脚本将用于从 Windows 和 LAN Manager 客户端查询和管理本地 UNIX 打印队列。基于 `printing` 参数指定的操作系统类型，为 `some` 命令参数提供了默认值。

#### 表 12.1 打印共享参数

| `print command` | 打印文件处理命令或脚本。使用 `%s` 或 `%f`。 |
| `lpq command` | 查询打印队列。使用 `%p`（打印机）。 |
| `lpq cache time` | `lpq` 信息缓存多长时间；限制 Windows 客户端重复查询请求带来的服务器负载。默认值为 10 秒。每个客户端上的 Windows 假脱机管理器每 15 秒查询一次远程打印队列。缓存文件存储在 `/tmp/lpq.xxxx` 中，其中 `xxxx` 是所使用 `lpq` 命令的哈希值。 |
| `lprm command` | 从队列中删除打印作业。使用 `%p`（打印机）和 `%j`（作业 #）。 |
| `lppause command` | 暂停特定打印作业。使用 `%p`（打印机）和 `%j`（作业 #）。 |
| `lpresume command` | 恢复特定打印作业。使用 `%p`（打印机）和 `%j`（作业 #）。 |
| `postscript` | 强制以 PostScript 模式打印；通过在发送文件到打印机之前在文件开头添加 `%!` 序列来修复前导 ctl-d 问题。 |
| `queuepause command` | 暂停特定打印队列。使用 `%p`（打印机）。 |
| `queueresume command` | 恢复特定打印队列。使用 `%p`（打印机）。 |

### 打印命令

特别是，您需要验证 `print command` 参数指定的选项。`print command` 的值是一个文本字符串，将通过 `system()` 调用在文件写入到假脱机目录后被调用来处理打印文件。通常，这将导致文件被移交给打印子系统。`print command` 必须在处理完成后从假脱机目录中删除打印文件。示例 12.2 显示了支持的操作系统类型的 `print command` 默认值。

#### 示例 12.2 默认打印命令值

```
print command = lpr -r -P%p %s    AIX, BSD, LPRNG, PLP, QNX
print command = lp -c -d%p %s; rm %s    HPUX, SYSV
print command = lp -d%p -s %s; rm %s    SOFTQ
```

请注意，指定的命令必须指明假脱机文件名，并且可选地指明打印机名称。此外，如果为打印机指定了 `guest ok`，一些系统在 `guest` 账户值为 `nobody` 时会出现打印失败。在这种情况下，请在 `guest account` 参数中使用另一个 UNIX 账户。

### 命令参数脚本

表 12.1 中列出的 `print command` 参数指定一个文本字符串，表示任何有效的 UNIX 命令或 shell 脚本组合。参数字符串值会传递给 C 库 `system()` 例程，后者随后 `fork` 并执行 `sh`（命令语言解释器）来解析和执行传递的字符串。命令字符串值很可能包含 Samba 替换变量的实例。变量值将在传递字符串到 `system()` 例程之前解析。最好在命令参数值中使用任何命令或脚本的完整路径名。这避免了执行期间解析路径相关的问题。示例命令字符串列在示例 12.3 中。

#### 表 12.2 打印机共享替换变量

| 变量 | 描述 |
|---|---|
| `%p` | 打印机名称 |
| `%j` | 整数作业编号 |
| `%s` | 假脱机文件名 |
| `%f` | 不带完整路径前缀的假脱机文件名 |

#### 示例 12.3 示例命令字符串

##### AIX, BSD, LPRNG, PLP, QNX

```
lpq command = lpq %p
```

```
lprm command = lprm -P%p %j
```

##### HPUX, SYSV

```
lpq command = lpstat -o%p
```

```
lprm command = cancel %p-%j
```

## Windows 客户端设置
