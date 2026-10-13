
#!/bin/sh

# `add_modem` 脚本。必须以 root 身份从 bourne shell 运行

# 为仅拨出的调制解调器启用 Solaris

根据你的具体需求更改这些参数。

| 参数 | 含义 |
| --- | --- |
| `PORT` | 要设置的端口，"a" |

## 在 Solaris 2.x 上设置终端

Solaris 2.x 端口监控器 `ttymon` 是否已配置并运行？

- 以 root 身份登录，输入 `sacadm -l -t ttymon` 并按回车。
如果收到类似 `Invalid request, ttymon does not exist` 的消息，说明 `ttymon` 端口监控器未配置。请继续下一步。

如果得到如下结果，请跳到第 3 。

| PMTAG | PMTYPE | FLGS | STATUS | COMMAND |
|---|---|---|---|---|
| zsmon | ttymon | | ENABLED | `/usr/lib/saf/ttymon` |

- 配置一个名为 `zsmon` 的 `ttymon` 实例。输入 `sacadm -a -p zsmon -t ttymon -c /usr/lib/saf/ttymon -v ttyadm-V` 并按回车。
注意：字符串 `zsmon` 被称为 `PMTAG`。

- `zsmon` 端口监控器上是否有正在运行的服务？输入 `pmadm -1` 并按回车。
如果得到如下结果

| PMTAG | PMTYPE | SVCTAG | FLGS | ID | <PMSPECIFIC> |
|---|---|---|---|---|---|
| zsmon | ttymon | ttya | | u root | `/dev/term/a` I |

你需要删除该运行的服务。输入 `pmadm -r -p zsmon -s ttya` 并按回车。`pmadm` 是 `PMTAG`，`zsmon` 是 `SVCTAG`。
如果你没有列出你的端口（如 `/dev/term/a`），则说明正常。

- 设置终端

- 为你所需的速率设置终端（下面的 `add_terminal` 脚本假设你正在使用 9600 波特。）

- 终端到电脑电缆中真正需要的线条是 2、3 和 7。确保你的电缆中的第 2 线和第 3 线交叉。使用空调制电缆效果良好。

- 为 XON/XOFF 流控设置终端

- 将终端设置为 7 位、偶校验（如果你有该设置，则 1 个停止位）。如果你需要不同的奇偶校验或字长，请参阅第 703 页的“设置串口模式”。

- 为终端启用 Solaris。

- 编辑并保存以下脚本为 `add_terminal`。

## 702 Solaris 2.x 调制解调器和终端教程

b. 要使脚本具有执行权限，输入 `chmod 700 add_terminal` 并按回车。

c. 编辑 `add_terminal` 以满足你的特定需求。

d. 以 root 身份执行 `add_terminal`。

e. 如果在按回车时终端没有给你登录界面，重启一次机器。

创建以下 shell 脚本。

```sh
#!/bin/sh

# add_terminal shell 脚本。必须以 root 身份运行。

# 此脚本带有以下参数调用 invmod。

# 根据你的特定需求更改这些参数。

# 参数                      含义

# PORT                        你 想要设置的端口，"a" 或 "b"

# TTSSPEED                  速率设置，来自 /etc/ttydev

# LOGMSG                     将显示的消息。

# -s tty$PORT                实际端口设备，你可能需要

# -d /dev/term/$PORT         来自/etc/ttydevs。选择一个

# -t $TTSSPEED               满足你需求的 TTSSPEED

#                             vt100               此端口的终端类型。这是一个

#                             终端类型

# - 'terminal disabled'      如果端口 禁用，发送到 tty 端口的消息

# -y                         开启软件载波检测

############################################################

LOGINMSG="Always be nice to your sysad, login:

PORT="*"

# 选择你的速率设置。设置 /etc/ttydevs 以获得更多设置。

# 根据本文其余部分的示例构建你自己的。

ttypeed -Y 9600bps - 7 bits parity, as supplied by Sun

ttydev="$PORT"

chown udev /dev/$ttydev; chgrp tty /dev/$ttydev

chmod root:tty; chmod 660 /dev/term/$PORT

# 更改端口外部的所有权以使用 ugrp，组 tty。

# 更改端口内部的所有权以使用端口，但如果你现在

# 这样做，那么当你在端口上添加调制解调器时，它将就绪绪。

chown udev /dev/$PORT; chgrp tty /dev/$PORT

chmod root:tty; chmod 660 /dev/term/$PORT

# 端口上现有的监控。

# 你可以忽略此命令的任何错误消息。

# 你可能正在尝试移除一个的端口监控器。

/sbin/pmade -d dsmon -s $ttyPORT

############################################################

# 创建新的端口监控器

# 双引号界定禁用消息

[disabled] are FORWARD QUOTES

/usr/sbin/pmade -d dsmon -s $ttyPORT -l root -i \

- /usr/sbin/ttyadm /usr/sbin/ttyadm -l $TTSSPEED \

- p "$LOGMSG" - /dev/term/$PORT -t vt100 -i 'terminal disabled' \

- -s /usr/login -j -of add_terminal script"

############################################################
```

f. 要使脚本具有执行权限，输入 `chmod 700 /sbin/add_terminal` 并按回车。

g. 运行脚本，输入 `/sbin/add_terminal` 并按回车。

## 设置串口模式

Sun 未提供你在 `ttydefs` 中可能需要的全部速率。`ttydefs` 中的条目格式所示。

```
ttylabel:initial-flags:final-flags:autobaud
```

### `ttydefs` 中的 133 条目

| 字段 | 描述 |
|---|---|
| `ttylabel` | `tymmon` 尝试匹配的 TTY 字段。 |
| `initial-flags` | 设置的初始设置。 |
| `final-flags` | 必须与 `initial-flags` 格式相同。 |
| `autobaud` | 如果 `autobaud` 字段包含 A，则启用自动波。否则，禁用自动波。 |
| `nextlabel` | 如果用户通过 Break 表示当前设置不合适，`tymmon` 会搜索 `ttylabel` 字段匹配 `nextlabel`。如果找到匹配，`tymmon` 将该字段作为其 `ttylabel` 字段。一组速率通常链接在一起，被称为搜索序列。例如，4800 可能连接到 1200，然后连接到 2400，最后连接到 4800。 |

> **重要规则。** 将模式设置为 8 位时，不要输入 `-parity ... sane ... -parity`，因为 `sane` 将端口重置为 7 位。

## `/ttydefs` 示例

这些示例应让你熟悉基础。我一直主张使用 8 位、无奇校验；38400 bps、8 位、无奇校验示例（下方）将向你展示如何设置它。（每个条目应占一行。在这里拆分是为了此文档打印打印。）

- 19200 bps、7 位、偶校验示例。
Sun 提供的 `conty5H` 是 19200 bps、7 位偶校验
`conty5H:19200 opost onlcr:19200 hupcl sane::conty6H`
这等同于

```
conty5H:19200 evenp opost onlcr:19200 sane evenp hupcl::conty6H
```
