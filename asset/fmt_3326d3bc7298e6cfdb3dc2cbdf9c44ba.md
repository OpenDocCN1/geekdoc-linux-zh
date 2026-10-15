
`io` 模块是 Python 的新增内容，首次出现在 Python 3 中并回移植到了 Python 2.6。截至编写时，该模块尚不成熟，运行时极其糟糕——特别是对于任何涉及大量文本 I/O 的应用程序。如果你正在使用 Python 2，将使用内置的 `open()`。

## logging

`logging` 模块为应用程序提供了一个灵活的设施，用于记录事件、错误和调试信息。这些信息可以被收集、过滤、写入文件，甚至发送到远程机器。本节涵盖了使用该模块的核心细节。

### 日志级别

`logging` 模块的主要关注在于日志消息的发布和处理。每个消息包含一些文本以及指示其严重程度的关联级别。级别具有如下符号名称和数值：

| 级别 | 数值 | 描述 |
|---|---|---|
| CRITICAL | 50 | 严重错误/消息 |
| ERROR | 40 | 错误 |
| WARNING | 30 | 警告 |
| INFO | 20 | 信息 |
| DEBUG | 10 | 调试 |
| NOTSET | 0 | 未设置级别 |

这些不同的级别用于 `logging` 模块中的各种函数和方法。例如，有可以在每个级别发布日志消息的方法，以及阻塞不符合特定阈值的过滤器。

### 基础配置

在使用 `logging` 模块的任何其他函数之前，应首先对特殊对象（如根日志器）进行基础配置。根日志器负责管理日志消息的默认行为，包括日志级别、输出目标、消息格式和其他基本细节。使用以下函数进行配置：

```
basicConfig(**kwargs)
```

对根日志器进行基础配置。此函数应在任何其他日志调用之前调用。该函数接受多个关键字参数：

| 关键字参数 | 描述 |
|---|---|
| filename | 将日志消息附加到指定的文件。 |
| filemode | 指定打开文件的模式。默认使用 'a'（追加）模式。 |
| format | 用于生成日志消息的字符串。 |
| datefmt | 用于输出日期和时间的字符串。 |
| level | 设置根日志器的级别。所有等于或高于此级别的日志消息都将被处理。低级别的消息将被静默忽略。 |
| stream | 提供一个发送日志消息的打开文件。默认流为 `sys.stderr`。此参数可以与 `filename` 参数同时使用 |

## 第 19 章 操作系统服务

这些参数大部分都是自解释其的。`format` 参数用于指定日志消息的格式，并包含可选的上下文信息，如文件名、级别、行号等。`datetime` 是与 `time.strftime()` 函数兼容的日期字符串。如果省略，日期格式设置为 ISO8601 格式。

`format` 中可以识别以下扩展项：

| 格式 | 描述 |
| --- | --- |
| `%(name)s` | 日志器的名称。 |
| `%(level)s` | 数字日志级别。 |
| `%(levelname)s` | 执行日志调用的级别文本。 |
| `%(pathname)s` | 执行日志调用的源文件路径。 |
| `%(filename)s` | 执行日志调用的源文件名。 |
| `%(funcName)s` | 执行日志调用的函数名。 |
| `%(module)s` | 执行日志调用的模块名。 |
| `%(lineno)d` | 执行日志调用的行号。 |
| `%(created)f` | 执行日志调用的时间。该值由 `time.time()` 返回的数字。 |
| `%(asctime)s` | 执行日志调用时的 ASCII 格式日期和时间。 |
| `%(msecs)s` | 执行日志调用时的毫秒部分。 |
| `%(thread)d` | 线程 ID。 |
| `%(threadName)s` | 线程名。 |
| `%(process)d` | 进程 ID。 |
| `%(message)s` | 日志消息（由用户提供）。 |

下面的示例说明了一个单一配置，将级别为 INFO 及以上的日志消息附加到文件中：

```python
import logging
logging.basicConfig(
    filename = 'app.log',
    format = '%(levelname)s-10s %(asctime)s %(message)s',
    level = logging.INFO
)
```

使用此配置，一条为 'Hello World' 的 CRITICAL 日志消息将如下出现在日志文件 'app.log' 中：

> CRITICAL 2005-10-25 20:46:57,126 Hello World

## Logger 对象

为了记录消息，你必须获取一个 Logger 对象。本节描述了创建、配置和使用这些对象的过程。

### 创建 Logger

要创建一个新的 Logger 对象，你使用以下函数：

```python
getLogger([name])
```

返回一个与名称 `loggername` 关联的 Logger 实例。如果不存在此类对象，将创建并返回一个新的 Logger 实例。`loggername` 是一个字符串，指定一个名称或一组由点分隔的系列名称（例如 'app' 或 'app.net'）。如果你省略 `logname`，将获得与根日志器（root logger）关联的 Logger 对象。

Logger 实例的创建与你在大多数其他模块中发现的不同。当你创建一个 Logger 时，你总是给它一个名称，该名称将作为 `Logger` 参数传递给 `getLogger()`。在内部，`getLogger()` 维护 Logger 实例及其关联名称的缓存。如果程序的其他部分请求相同名称的日志器，将返回之前创建的实例。这种安排极大地简化了大型应用程序中日志消息的处理，因为你不需要考虑如何在不同的模块之间传递 Logger 实例。相反，在每个需要记录日志的模块中，只需使用 `getLogger()` 获取适当 Logger 对象的引用即可。

### 选择名称

由于某些原因（稍后会变得清晰），在使用 `Logger()` 时你应该始终选择有意义的名称。例如，如果你的应用程序 way 'app'，那么在构成应用程序的每个程序模块顶部，至少应该使用 `getLogger('app')`。例如：

```python
import logging
log = logging.getLogger('app')
```

你可能还会考虑将模块添加到日志器中，例如 `getLogger('app.net')` 或 `getLogger('app.user')`，以便更清晰地指示日志消息的来源。

### 发布日志消息

如果 `log` 是一个 Logger 对象实例（使用上一节中的 `getLogger()` 函数创建），则使用以下方法在不同级别发布日志消息：

| 日志级别 | 方法 |
| --- | --- |
| CRITICAL | `log.critical(fmt, *args [, [exc_info, {extra}]])` |
| ERROR | `log.error(fmt, *args [, [exc_info, {extra}]])` |
| WARNING | `log.warning(fmt, *args [, [exc_info, {extra}]])` |
| INFO | `log.info(fmt, *args [, [exc_info, {extra}]])` |
| DEBUG | `log.debug(fmt, *args [, [exc_info, {extra}]])` |

`fmt` 参数是指定日志消息格式的字符串。`args` 中的剩余参数将作为格式字符串中格式位符的参数。字符串格式化运算符 `%` 用于从参数形成结果消息。如果提供了多个参数，它们将存放在一个元组中进行格式化。如果只提供一个参数，它将直接放在 `%` 之后。

## 第19章 操作系统服务

以下示例演示了如何创建一个自定义过滤器：

```python
class FilterPunc(Logging.Filter):
    def __init__(self, name):
        self.funcName = name
    def filter(self, record):
        if recordName == self.funcName: return False
        else: return True
```

```python
log.addFilter(FilterPunc('foo')) # 忽略所有来自 foo 的消息
log.addFilter(FilterPunc('bar')) # 忽略所有来自 bar 的消息
```

## 消息传播与分级日志器
