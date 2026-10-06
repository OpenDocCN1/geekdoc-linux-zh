
`PATH` 记录记录了路径信息。`item=0` 是项索引，`name="/etc/ssh/sshd_config"` 是文件名，`inode=40928` 是索引号。

## 第四记录

`type` 字段包含记录的类型。在此示例中，`PROCTITLE` 值指定了该记录通过系统调用到内核，提供了由此 Audit 事件触发的完整命令行。

`proctitle:636174002F6574632F7376382F73766845F63F6E66969`

`proctitle` 字段记录了用于调用分析进程的命令完整命令行。该字段采用十六进制编码，以便允许用户影响 Audit 日志解析器。该文本解码了触发此 Audit 事件的命令。当使用 `ausearch` 命令搜索 Audit 记录时，使用 `-i --interpret` 选项自动将十六进制值转换为人类可读的等效值。`636174002F6574632F7376382F73766845F63F6E66969` 值解释为 `cat /etc/ssh/sshd_config`。

## 10.6. 使用 AUDCTL 定义和执行审计规则

Audit 系统根据一组捕获在日志文件中的规则运行。Audit 规则可以通过命令行使用 `auditctl` 工具进行设置，也可以通过在 `/etc/audit/rules.d/` 目录下进行设置。

`auditctl` 命令允许你控制 Audit 系统的基本功能，并定义决定哪些 Audit 事件被记录的规则。

### 文件系统规则示例

- 1. 定义一条规则，允许对 `/etc/passwd` 文件的所有访问和每次属性更改：
  > `# auditctl -w /etc/passwd -p wa -k password_changes`
- 2. 定义一条规则，允许对 `/etc/selinux/` 目录下的所有文件的所有访问和每次属性更改：
  > `# auditctl -w /etc/selinux/ -p wa -k sel_changes`

### 系统调用规则示例

- 1. 定义一条规则，每当程序使用 `adjtime` 或 `setwimeday` 系统调用时，创建一个日志条目，并使用 64 位架构：
  > `# auditctl -a always,exit -F arch=b64 -S adjtime -S settimeday -k time_change`
- 2. 定义一条规则，每当 ID 为 1000 或更大的系统用户删除或重命名文件时，创建一个日志条目：
  > `# auditctl -a always,exit -S unlink -S unlink -S rename -F audit>=1000 -F audit!=429467295 -k delete`

注意，`-F audit!=429467295` 选项用于排除设置了登录 UID 的用户。

### 可执行文件规则

要定义一条记录所有对 `/bin/id` 程序执行操作的规则，请执行以下命令：

```
# auditctl -a always, -F exe=/bin/id -F arch=b64 -S execve -k execution_bin_id
```

其他资源

- 查看 `auditctl(8)` 手页以获取更多信息、性能提示和额外的用法示例。

## 10.7. 定义持久化审计规则

要定义跨重启有效的持久化审计规则，你必须将它们包含在 `/etc/audit/rules.d/audit.rules` 文件中，或者使用 `augrules` 程序读取位于 `/etc/audit/rules/` 下的规则。

注意，`/etc/audit/rules.rules` 文件在每次审计服务启动时都会生成。`/etc/audit/rules/` 中的文件使用相同的 `auditctl` 命令行语法来指定规则。空行和注释（`#`）会被忽略。此外，你可以使用 `auditctl` 命令通过 `-R` 选项从指定文件读取规则，例如：

```
# auditctl -R /usr/share/audit/sample-rules/30-stig.rules
```

## 10.8. 使用预配置规则

在 `/usr/share/audit/sample-rules` 目录下，audit 软件包提供了一组遵循各种标准的预配置规则：

- `30-nis.rules`: 审计规则配置符合《国家安全计划操作手册》中规定的要求。
- `30-ospp-v4.rules`: 审计规则配置符合 OSPP（通用系统保护规范文件）版本 4.2 定义的要求。
- `30-pci-dss-v3.rules`: 审计规则配置符合支付卡行业数据标准（PCI DSS）v3.1 设的要求。
- `30-stig.rules`: 审计规则配置符合安全实施指南（STIG）设的要求。

要使用这些配置文件，请将它们复制到 `/etc/audit/rules.d/` 目录并使用 `augrules --load` 命令，例如：

```
# cd /usr/share/audit/sample-rules/
# cp 10-base-config.rules 30-stig.rules 31-privileged.rules 99-finalize.rules /etc/audit/rules.d/
# augrules --load
```

其他资源

## 第 10 章. 审计审计

- 审计规则有一套编号方案，允许你进行排序。要了解更多关于命名方案的信息，请查看 `/usr/share/doc/audit/rules/README`。
- 查看 `audit.rules(7)` 手页以获取更多信息、故障排除和额外的用法示例。

## 10.9. 使用 AUGENRULES 定义持久化规则

`augenrules` 脚本读取位于 `/etc/audit/rules.d/` 目录下的规则并将其编译为 `audit.rules` 文件。该脚本根据自然排序按特定顺序处理所有以 `.rules` 结尾的文件。此目录中的文件组织成具有以下含义的组：

- 10 - 内核和审计配置
- 20 - 匹配通用规则但你想要不同匹配的规则
- 30 - 主规则
- 40 - 可选规则
- 50 - 服务器特定规则
- 70 - 系统本地规则
- 90 - 最终完成（不可变）

这些规则并非用于所有情况。它们是策略的一部分，应该经过深思熟虑并单独复制到 `/etc/audit/rules.d/`。例如，要在 STIG 配置下设置系统，请复制规则 10-base-config、30-stig、31-privileged 和 99-finalize。

一旦你向 `/etc/audit/rules.d/` 目录中放入这些规则，可以通过运行带有 `--load` 指令的 `augenrules` 脚本来加载它们：

```
# augenrules --load
/sbin/augenrules: No change
No rules
enabled 1
failure 1
pid 742
rate_limit 0
...
```

其他资源

- 有关审计规则和 `augenrules` 脚本的更多信息，请查看 `audit.rules(8)` 和 `augenrules(8)` 手页。

## 10.10. 禁用 AUGENRULES

使用以下步骤禁用 `augenrules` 工具。这将 Audit 切为使用 `/etc/audit/audit.rules` 文件定义的规则。

步骤

- 1. 将 `/lib/systemd/system/auditd.service` 文件复制到 `/etc/systemd/system/` 目录：
```
# cp -f /lib/systemd/system/auditd.service /etc/systemd/system/
```
- 2. 使用你喜欢的编辑器编辑 `/etc/systemd/system/auditd.service` 文件：
```
# vi /etc/systemd/system/auditd.service
```
- 3. 注释掉包含 `augenrules` 的行，并取消包含 `auditctl -R` 的行：
```
ExecStartPost=/augenrules
ExecStartPost=/auditctl -R /etc/audit/audit.rules
```
- 4. 重新加载系统守护进程：
```
# systemctl daemon-reload
```
- 5. 重启 auditd 服务：
```
# service auditd
```

其他资源

- `augenrules(8)` 和 `audit.rules(8)` 手页。
- 对 `/etc/audit/audit.rules` 更改的文章。

## 10.11. 相关信息

有关审计系统的更多信息，请参考以下来源。

在线来源

- RHEL 审计系统参考。
- Auditd 执行选项文章。
- Linux 审计项目页面。

已安装文档

audit 软件包提供的文档可以在 `/usr/share/doc/audit/` 找到。

手册页

- `audispd.conf(5)`
- `auditd.conf(5)`
- `ausearch-expression(5)`
- `audit.rules(7)`
- `audispd(8)`
- `auditctl(8)`
- `auditd(8)`
- `aulast(8)`
- `aulastlog(8)`
- `aureport(8)`
- `ausearch(8)`
- `ausyscall(8)`
- `autrace(8)`
- `aaudit(8)` (注：根据上下文从 auvirt 纠正)

## 第 11 章. 配置和管理白名单

应用程序白名单有效地防止未知和可能的恶意软件的执行。

## 11.1. RHEL 中的 POLICYD 白名单

`policyd` 框架引入了基于用户策略的应用程序白名单和黑名单。应用程序白名单是防止不受限制的可能恶意软件的最有效方法之一。

`policyd` 框架提供了以下组件：

管理员可以根据路径、哈希、MIME 类型或信任定义允许和拒绝规则。

应用程序白名单引入了“信任”的概念。当应用程序通过软件包管理器正确安装时，它会被注册到系统 RPM 数据库中。`policyd` 插件注册任何由 YUM 软件包管理器处理的系统更新。该插件通知数据库的变化。

使用 `rpm` 工具安装需要手动刷新数据库，而其他添加应用程序的方法需要创建规则并重启 `policyd` 服务。

`policyd` 服务配置位于 `/etc/policyd/` 目录，结构如下：

- `policyd.rules` 文件包含允许和拒绝执行规则。
- `policyd.conf` 文件包含守护选项。该文件主要用于性能调优。

## 11.2. 部署应用程序白名单

要在 RHEL 中部署 `policyd` 框架：

### 步骤

- 1. 安装 `policyd` 软件包：
```
# yum install facolicyd
```
- 2. 启用并启动 facolicyd 服务：
```
# systemctl enable --now facolicyd
```

### 验证步骤

- 1. 验证 facolicyd 服务是否正常运行：
```
# systemctl status facolicyd
● facolicyd.service - File Access Policy Daemon
 Loaded: loaded (/usr/lib/systemd/system/facolicyd.service; enabled: vendor preset)
 Active: active (running) since Tue 2019-10-15 18:02:35 CEST, 55s ago
```
- 2. 以没有 root 权限的用户登录，并检查应用程序白名单是否生效，例如：
```
$ /bin/ls /tmp
$ /tmp
bash: /tmp/ls: Operation not permitted
```

## 11.3 为应用程序白名单添加自定义规则

facolicyd 包中的默认规则集不会影响系统功能。对于自定义场景（例如在非标准目录存储二进制文件和脚本，或不通过 yum 或 rpm 安装管理器添加应用程序），您必须修改现有规则或添加新规则。以下步骤演示了如何添加新规则以将自定义二进制文件加入白名单。

### 前提条件

- 您的系统中已部署 facolicyd 框架。

### 步骤

- 1. 将您的自定义二进制文件复制到所需的目录，例如：
```
$ /bin/ls /tmp
$ /tmp
bash: /tmp/ls: Operation not permitted
```
停止 facolicyd 服务：
```
# systemctl stop facolicyd
```
使用调试模式识别原因。由于 `facolicyd --debug` 命令的输出非常详细，且您可以通过 Ctrl+C 停止它或杀死相应的进程，请将错误输出重定向到文件：
```
# facolicyd --debug facolicyd.output &
[1] 51341
```
或者，您可以在另一个终端中运行 facolicyd 调试模式。

重复之前被允许的命令：
```
$ /tmp/ls
bash: /tmp/ls: Operation not permitted
```
通过将任务切回前台并按下 Ctrl+C 来停止调试模式：
```
# fg
facolicyd --debug
^C shut down...
Inter-thread max queue depth 1
Allowed accesses: 2
Denied accesses: 1
...]
```
或者，杀死 facolicyd 调试模式的进程：
```
# kill 51341
```
找到拒绝执行您的应用程序的规则：
```
# cat facolicyd.output
...]
rule:9 dec=deny_audit perm=execute auid=1000 pid=51362 exe=/usr/bin/bash file=/tmp/ls
type=application/x-executable
...]
```
在 `/etc/facolicyd/facolicyd.rules` 文件中，于拒绝您自定义二进制文件的规则之前添加新的允许规则。根据上一个命令的输出，在本例中该规则编号为 9：
```
allow perm=execute exe=/usr/bin/bash trust=1 : path=/tmp/ls ftype=application/x-executable
trust=0
```
或者，您可以通过在 `/etc/facolicyd/facolicyd.rules` 文件中添加以下规则来允许 /tmp 目录下所有二进制文件的执行：
```
allow perm=execute exe=/usr/bin/bash trust=1 : dir=/tmp/ all trust=0
```
- 8. 为了防止自定义二进制文件的内容更改，使用 SHA-256 校验和定义所需的规则：
```
$ sha256sum /tmp/ls
780b75c90b2d4a1ea4679fcb358c892b1251b68d91927c80fc0d9d9d148b25e836 ls
```
将规则更改为遵循以下定义：
```
allow perm=execute exe=/usr/bin/bash trust=1 :
sha256hash=780b75c90b2d4a1ea4679fcb358c892b1251b68d91927c80fc0d9d9d148b25e836
```
- 9. 启动 facolicyd

### Red Hat Enterprise Linux 8 安全加固

### 验证步骤

- 验证 **usbguard** 服务正在运行：
```
systemctl enable --now usbguard
usbguard.service - USBguard daemon
Loaded: (/usr/lib/systemd/system/usbguard.service); enabled; vendor preset: disabled
Active: active (running) since Thu 2019-11-07 09:44:07 CET; 3min 16s ago
```
