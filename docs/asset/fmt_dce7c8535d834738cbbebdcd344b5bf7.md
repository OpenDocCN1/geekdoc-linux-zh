
dbus-monitor `"type='signal', sender='org.gnome.TypingMonitor', interface='org.gnome.TypingMonitor'"`

### 作者

`dbus-monitor` 由 Philip Blundell 编写。分析输出模式由 Olli Salli 添加。

## 缺陷

请将错误报告发送到 D-Bus 邮件列表或错误跟踪器，参见 http://www.freedesktop.org/software/dbus/m/

# DBUS-RUN-SESSION

`dbus-run-session` - 在新的 D-Bus 会话中启动进程

### 概要

```
dbus-run-session [--config-file FILENAME] [--dbus-daemon BINARY] [--] PROGRAM [ARGUMENTS...]
dbus-run-session --help
dbus-run-session --version
```

### 描述

`dbus-run-session`

用于从 shell 脚本启动 `dbus-daemon` 会话实例，并在该会话中启动指定的程序。`dbus-daemon` 的运行时间与程序相同，程序结束后将终止。

一种用法是在文本模式或 SSH 会话中运行带有自带 `dbus-daemon` 的 shell，并在离开子 shell 时自动终止 `dbus-daemon`，如下：

```
dbus-run-session -- bash
```

或者通过将 `dbus-run-session` 与 `exec` 内置命令结合，来完全替换登录 shell：

```
exec dbus-run-session -- bash
```

另一种用法是在隔离的 D-Bus 会话中运行总线回归测试和类似操作，以避免干扰“真实的” D-Bus 会话，或依赖于已经存在活跃的 D-Bus 会话，例如：

```
dbus-run-session -- make check
```

或在 `automake(1)` 中：

```
AM_TESTS_ENVIRONMENT = export MY_DEBUG=all; LOG_COMPILER = dbus-run-session AM_LOG_FLAGS ==
```

### 选项

- `--config-file=FILENAME`, `--config-file FILENAME`
将 `--config-file=FILENAME` 传递给总线守护进程，而不是作为 `--session` 参数。参见 `dbus-daemon(1)`。

- `--dbus-daemon=BINARY`, `--dbus-daemon BINARY`
将 `BINARY` 作为 `dbus-daemon(1)` 运行，而不是按照通常在 `PATH` 中搜索名为 `dbus-daemon` 的可执行文件。

- `--help`
打印用法信息并退出。

- `--version`
打印 `dbus-run-session` 的版本并退出。

# 退出状态

`dbus-run-session` 以 `PROGRAM` 的退出状态退出；如果使用了 `--help` 或 `--version` 选项，则返回 `0`；如果 `dbus-run-session` 内部发生错误，返回 `127`；如果 `PROGRAM` 被信号 `n` 杀死，则返回 `128+n`。

## 环境变量

在 `PATH` 中查找 `PROGRAM`，并（如果没有使用 `--dbus-daemon` 选项或其参数不包含 `/` 字符）查找 `dbus-daemon`。

会话总线的地址通过环境变量 `DBUS_SESSION_BUS_ADDRESS` 给 `PROGRAM`。

如果环境变量中存在 `DBUS_SESSION_BUS_PID`、`DBUS_SESSION_BUS_WINDOWOWID`、`DBUS_STARTER_BUS_TYPE` 和 `DBUS_STARTER_ADDRESS`，则将其移除。

## 缺陷

请将错误报告发送到 D-Bus 邮件列表或错误跟踪器，参见 http://www.freedesktop.org/software/dbus/m/

# 另见

`dbus-daemon(1)`, `dbus-launch(1)`

## 名称

`dbus-send` - 向总线发送消息

### 概要

```
dbus-send [--system | --session | --address=ADDRESS] [--dest=NAME] [--print-reply [=literal]] [--reply-timeout=MSEC] [--type=TYPE] OBJECT_PATH INTERFACE.MEMBER [CONTENTS...]
```

### 描述

`dbus-send` 命令用于向 D-Bus 总线发送消息。关于整体架构的更多信息请参见 http://www.freedesktop.org/software/dbus/m/。

有两种已的消息总线：系统总线（在许多系统中作为 "messagebus" 服务安装）和用户登录会话总线（在用户登录时启动）。`--system` 和 `--session` 选项允许 `dbus-send` 分别向系统或会话总线发送消息。如果两者都未指定，则分别向系统或会话总线发送消息。

## 名称

`dc` - 一个任意精度计算器

### 摘要

```
dc [-V] [-h] [-e expression] [-f script-file] [file ...]
```
