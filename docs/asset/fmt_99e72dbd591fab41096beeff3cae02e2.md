
### systemd-analyze critical-chain

`systemd-analyze critical-chain` [*UNIT*...] 打印时间关键链单元的树（针对每个指定的 *UNIT*，否则针对默认目标）。单元处于活动或启动状态后的时间打印在 “@” 字符后。单元启动所花费的时间打印在 “+” 字符后。请注意，输出可能会产生误导，因为某个服务的初始化可能依赖于套接字激活，且由于单元的并行执行。

### systemd-analyze plot

`systemd-analyze plot` 打印 SVG 图形，详细说明哪些系统服务在什么时间启动，并突出显示其用于初始化的时间。

### systemd-analyze dot

`systemd-analyze dot` 生成 dot 格式的文本依赖图描述，以便使用 GraphViz `dot(1)` 工具进一步处理。使用类似 `systemd-analyze dot | dot -Tsvg > systemd.svg` 的命令行来生成图形化依赖树。除非传递了 `--order` 或 `--require`，否则生成的图将显示顺序依赖和需求依赖。可选的模式通配符风格规范（例如 `*.target`）可以最后给出。如果这些模式中的任意一个匹配源节点或目标节点，则单元依赖包含在图中。

### systemd-analyze dump

`systemd-analyze dump` 输出完整的服务器状态的（通常非常长的）人类可读序列化。其格式可能会在没有通知的情况下更改，应用程序不应对其进行解析。

### systemd-analyze set-log-level

`systemd-analyze set-log-level` *LEVEL* 将 `systemd` 守护进程的当前日志级别更改为 *LEVEL*（接受 `systemd(1)` 中描述的 `--log-level=` 相同的值）。

### systemd-analyze verify

`systemd-analyze verify` 将加载单元文件，如果在检测到任何错误时打印警告。命令行上指定的文件将被加载，但也会加载它们引用的其他任何单元。此命令通过在单元加载路径的开头添加所有命令行参数的目录来实现这意味着那些目录中发现的所有单元文件将优先于在标准位置发现的单元文件使用，即使未明确列出。

如果未传递任何命令，则隐含 `systemd-analyze time`。

## 选项

理解以下选项：

**-user**

操作用户 `systemd` 实例。

**-system**

操作系统 `systemd` 实例。这是隐含的默认值。

**-order, -require**

与 `dot` 命令（见上文）结合使用时，选择依赖图中显示哪些依赖关系。如果传递了 `--order`，仅显示类型为 *After=* 或 *Before=* 的依赖关系。如果传递了 `--require`，仅显示类型为 *Requires=*、*RequiresOverridable=*、*Requisite=*、*RequisiteOverridable=*、*Wants=* 和 *Conflicts=* 的依赖关系。如果两者均未传递，则显示所有这些类型的依赖关系。

**-from-pattern=, -to-pattern=**

与 `dot` 命令（见上文）结合使用时，选择依赖图中显示哪些关系。这两个选项都需要 `glob(7)` 模式作为参数，该模式将与关系的左端和右端节点分别进行匹配。

每个选项都可以多次使用，在这种情况下，单元名称必须匹配其中一个值。当关系两端的测试都存在时，关系必须通过两个测试才会显示。当模式也作为位置参数指定时，它们必须匹配关系的一端。换句话说，使用这两个选项指定的模式将修剪由位置参数匹配的边列表（如果给出了位置参数），否则完全确定显示的边列表。

**-fuzz=***tspan*

与 `critical-chain` 命令（见上文）结合使用时，也显示比同一层级中最新单元提前 *tspan* 完成的单元。*tspan* 的单位默认为秒，除非指定了不同的单位，例如 `"50ms"`。

**-no-man**

不调用 `man` 来验证 *Documentation=* 中列出的 man 页面的存在。

**-H, -host=**

### systemd-analyze (1)

远程执行操作。指定一个主机名，或“@”分隔的用户名和主机名以进行连接。主机名后可选地附加一个容器名，以“:”分隔，从而直接连接到指定主机上的特定容器。这将使用 SSH 与远程机器管理器实例通信。可使用 `machinectl -H HOST` 列出容器名称。

- **`-M, --machine=`**

  在本地容器上执行操作。指定要连接的容器名称。

- **`-h, --help`**

  打印简短的帮助信息并退出。

- **`--version`**

  打印简短的版本信息并退出。

- **`--no-pager`**

  不将输出通过分页器管道。

## 退出状态

成功时返回 0，否则返回非零的失败代码。

## DOT 的示例

示例 1. 绘制所有名称以“avahi-daemon”开头的单元的所有依赖项

```bash
$ systemd-analyze dot 'avahi-daemon.*' | dot -Tsvg > avahi.svg
$ eog avahi.svg
```

示例 2. 绘制所有已知目标单元之间的依赖关系

```bash
$ systemd-analyze dot --to-pattern='*.target' --from-pattern='*.target' | dot -Tsvg > targets.svg
$ eog targets.svg
```

## VERIFY 的示例

当前检测到的以下错误：

- 未知的部分和指令，
- 启动给定单元所必需的缺失依赖项，
- 在 *Documentation=* 中列出但在系统中未找到的手册页，
- 在 *ExecStart=* 及类似指令中列出但在系统中未找到或不可执行的命令。

### 示例 3. 拼写错误的指令

```bash
$ cat ./user.slice
[Unit]
WhatIsThis=11
Documentation=(1)
Requires=different.service

[Service]
Description=x

$ systemd-analyze verify ./user.slice
[.user.slice:9] Unknown lvalue 'WhatIsThis' in section 'Unit'
[.user.slice:13] Unknown section 'Service'. Ignoring.
Error: org.freedesktop.systemd1.LoadFailed: Unit different.service failed to load: No such file or directory.
Failed to create user.slice/start: Invalid argument
user.slice: man (1) command failed with code 16
```

### 示例 4. 缺失的服务单元

```bash
$ tail ./a.socket ./b.socket
==> ./a.socket <==
[Socket]
ListenStream=100

==> ./b.socket <==
[Socket]
ListenStream=100
Accept=yes

$ systemd-analyze verify ./a.socket ./b.socket
Service a.service not loaded, a.socket cannot be started.
Service b@0.service not loaded, b.socket cannot be started.
```

## 环境变量

`$SYSTEMD_PAGER`

在未给出 `--no-pager` 时使用分页器；覆盖 `$PAGER`。将其设置为空字符串或值“cat”等同于传递 `--no-pager`。

`$SYSTEMD_LESS`

覆盖传递给 `less` 的默认选项 ("FRSXMK")。

## 另见

`systemd (1)`, `systemctl (1)`, `systemd (8)`, `systemd.system.conf (5)`

## SYSTEMD-ASK-PASSWORD

### 名称

`systemd-ask-password` - 向用户查询系统密码

### 概要

`systemd-ask-password [OPTIONS...] [MESSAGE]`

### 描述

`systemd-ask-password` 可用于使用命令行指定的问题消息向用户查询系统密码或口令。当从 TTY 运行时，它会在 TTY 上查询密码并将其打印到标准输出。当在没有 TTY 的情况下或带有 —**no-tty** 运行时，它将在全系统范围内查询密码，并允许活跃用户通过多个代理进行响应。后者仅对特权进程可用。

此工具的目的是查询全系统范围的密码——即未绑定到特定用户账户的密码。示例包括：插入时或启动时解锁加密硬盘，为 Web 和 VPN 服务器输入 SSL 证书口令。
