
```python
import logging
import sys

# 创建一个向 stderr 输出 CRITICAL 级别消息的处理器
crit_hand = logging.StreamHandler(sys.stderr)
crit_hand.setLevel(logging.CRITICAL)

# 创建一个名为 'app' 的 logger
app_log = logging.getLogger('app')
app_log.setLevel(logging.INFO)
app_log.addHandler(logging.FileHandler('app.log'))
app_log.addHandler(crit_handler)
```

在这个示例中，有一个名为 `'app'` 的单一 `logger`，级别为 `INFO`。它附加了两个处理器，但其中一个处理器（`crit_handler`）具有它自己的 `CRITICAL` 级别。尽管此处理器会接收 `INFO` 或更高级别的日志消息，但它会选择性地丢弃那些不是 `CRITICAL` 的消息。

# 处理器清理

在处理器上使用以下方法来执行清理。

```
h.flush()
```

刷新所有日志输出。

```
h.close()
```

关闭处理器。

# 消息格式化

默认情况下，`Handler` 对象按照 `logging` 调用中的格式完全地输出日志消息。然而，有时你可能想向消息中添加额外的上下文信息，例如时间戳、文件名、行号等。

# logging 365

描述了如何将这些额外信息自动添加到日志消息中。

# Formatter 对象

`Formatter([fmt, datetime])`

创建一个新的 `Formatter` 对象。`fmt` 为消息提供一个格式字符串。在 `fmt` 中，你可以像之前为 `basicConfig()` 函数描述的那样放置各种扩展。`datetime` 是一个与 `time.strftime()` 函数兼容的日期字符串。如果省略，日期格式将被设置为 ISO8601 格式。

要使其生效，`Formatter` 对象必须附加到 `handler` 对象。这是通过使用 `Handler` 实例 `h` 的 `h.setFormatter()` 方法实现的。

```
h.setFormatter(format)
```

设置 `Handler` 实例 `h` 上用于创建日志消息的格式化对象。

`h.format` 必须是 `Formatter` 的实例。

以下是一个说明如何在处理器上自定义日志消息格式的示例：

```python
import logging
import sys

# 设置消息格式
format = logging.Formatter("%(levelname)s -10s %(asctime)s %%(message)s")

# 创建一个向 stderr 输出 CRITICAL 日志消息的处理器
crit_handler = logging.StreamHandler(sys.stderr)
crit_handler.setLevel(logging.CRITICAL)
crit_handler.setFormatter(format)
```

在这个示例中，在 `crit_handler` 处理器上设置了一个自定义的 `Formatter`。如果一条如 `"Creeping death detected."` 的日志消息被此处理器处理，将产生以下日志消息：

```
CRITICAL    2005-10-25 20:46:57:12 Creeping death detected.
```

# 为消息添加额外上下文

在某些应用程序中，向日志消息中添加额外的上下文信息是有帮助的。这些额外信息可以通过两种方式提供。首先，所有的日志操作（例如 `log.critical()`、`log.warning()` 等）都有一个关键字参数，用于提供一个包含额外字段的字典，供格式字符串使用。这些字段将与之前为 `Formatter` 对象描述的上下文数据合并。以下是一个示例：

```python
import logging
import socket
logging.basicConfig(format="%%(hostname)s %%(levelname)s -10s %(asctime)s %%(message)s")
# 一些额外上下文
netinfo = {
    'hostname': socket.gethostname(),
    'ip': socket.gethostbyname(socket.gethostname())
}
log = logging.getLogger('app')
```

# 使用额外上下文数据发布日志消息

```python
log.critical("Could not connect to server", extra=-netinfo)
```

这种方法的缺点是，你必须确保每次日志操作都包含了额外信息，否则程序将崩溃。另一种方法是使用 `LogAdapter` 类作为现有 `logger` 的包装器。

```
LogAdapter(log, extra)
```

在 `Logger` 对象 `log` 周围创建一个包装器。`extra` 是一个提供给消息格式化器的额外上下文信息字典。`LogAdapter` 的实例与 `Logger` 对象具有相同的接口。然而，发布日志消息的操作会自动添加 `extra` 中提供的额外信息。

以下是使用 `LogAdapter` 对象的示例：

```python
import logging
```

# 杂项实用函数

`logging` 中的以下函数控制日志的其他方面：

```
disable(level)
```

全局禁用所有级别低于 `level` 参数指定的日志消息。这可以用于在整个应用程序范围内关闭日志——例如，如果你想临时禁用或减少日志输出的量。

```
addName(level, levelName)
```

创建一个全新的日志级别和名称。`level` 是一个数字，`levelName` 是一个字符串。这可以用于默认支持的级别名称。

```
getLevel(level)
```

返回与数值值 `level` 对应的级别名称。

```
shutdown()
```

关闭所有日志对象，必要时刷新输出。

# 日志配置

设置应用程序使用日志模块通常涉及以下基本步骤：

- 1. 使用 `getLogger()` 创建各种 `Logger` 对象。设置合适的日志级别。
- 2. 通过实例化各种类型的处理器（`FileHandler`、`StreamHandler`、`SocketHandler` 等）创建 `Handler` 对象并设置合适的级别。
- 3. 创建 `Formatter` 对象并使用 `setFormatter()` 将其附加到 `Handler` 对象。
- 4. 使用 `addHandler()` 方法将 `Handler` 对象附加到 `Logger` 对象。

由于每个步骤的后果可能相当复杂，最好的做法是将所有的日志配置放在一个单一的记录位置。例如，你可以创建一个 `appconfig.py` 文件，并在你的主程序程序导入它：

```python
# appconfig.py
import logging
import sys
```

```python
# 设置格式
format = logging.Formatter("%(levelname)s -10s %(asctime)s %%(message)s")
```

```python
# 创建一个向 stderr 输出 CRITICAL 消息的处理器
crit_handler = logging.StreamHandler(sys.stderr)
crit_handler.setLevel(logging.CRITICAL)
crit_handler.setFormatter(format)
```

```python
# 创建一个向文件输出消息的处理器
app_log = logging.FileHandler('app.log')
app_log.setFormatter(format)
```

```python
# 修改 'app.net' logger 的级别
logging.getLogger("app.net").setLevel(logging.ERROR)
```

如果需要对日志配置的任何部分进行更改，将所有内容放在一起更易于维护。请记住，此文件只需要在程序的一个位置导入一次。在代码的其他需要发布日志消息的部分，你只需包含如下代码即可：

```python
import logging
app_log = logging.getLogger("app")
app_log.critical("An error occurred")
```

# logging.config 子模块

作为在 Python 代码中硬编码日志配置的替代方案，可以使用 INI 配置来通过使用来配置日志模块。要做到这一点，请使用 `logging.config` 中的以下函数：

```
fileConfig(filename [, defaults [, disable_existing_loggers]])
```
