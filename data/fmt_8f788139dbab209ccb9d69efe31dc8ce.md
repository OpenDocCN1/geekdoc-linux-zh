
如果你尝试在不先调用 `simpleSup:start_link()` 的情况下调用 `app:print_message()` 或 `app:get_connections()`，它不会按预期工作。等等，看看调用 `app:crash/0` 会发生什么：

```
> app:crash().
```

### 如何编写 Erlang 程序

要终止一个 Erlang 程序，你需要知道它的 ID 或者能够使用 `Observer` 等工具找到它。终止进程有很多方法。一种方法是调用 `exit(child)`，它有两个参数：第一个参数是进程 ID，第二个参数是退出原因。虽然 Erlang 程序可以处理各种退出，你可以指定任何退出原因，这将终止进程。因此，这里有一个简单的示例：

```
> (ok, Pid) = app:start_link().

{ok, Pid}

> exit(Pid, kill).

exception: killed
```

崩溃！

`ok`

图 4 显示了生成的命令。现在是时候发现应用程序仍在工作：

```
> app:print_message().

This is a working gen_server!

ok
```

这就是我们看到的！

# Erlang 中的错误日志

在本节中，你将使用三个更简单的 Erlang 函数学习 Erlang 中的错误日志操作：

```
--- erlang

--- 28 Mar-2017, 12:03:42 ---

Your version (28.4.1) [source] [embedded 64 bit] [wx:x86_64] 4.4

> This is with (4.4)

> version()

= {ok, "28.4.1"}

> init()

= {ok, "0.65"}

> This is with getting_error()

> app:get_connection()

> crash(crch)

--- REPORT: 20-Mar-2017, 12:03:42 ---

ERROR_REPORT: crash(crch)

  function: {crch,crch}

  state: {state, []}

  stack: [{crch,crch}, {gen_server,call}]
```

# 关于 behaviours

`behaviour` 定义了用于交互的机制并提供了格式化常见模式的方法。

```
> logging_warning("This is a warning message")
WARNING REPORT===20-Mar-2017:10:02:46 ===
> "This is a warning message"
ok
```

你也可以通过查看 `app` 模块中的代码 `handle_info/2` 和 `terminate/2` 来使用 `error_logger:info_msg`。你可以在 `http://erlang.org/doc/man/error_logger` 找到关于 `error_logger` 的信息。

# Erlang Observer

如果你想手动记录 Erlang 进程，可以通过 `Erlang Observer` 找到它的 ID。`Observer` 随 Erlang 一起提供，你可以通过执行以下命令启动它：

```
$ erlang-observer -setcookie Mycookie
```

图 5 显示了运行中的 Erlang，你可以看到所有运行的进程以及每个进程的 ID。然而，在随后的示例中有一个技巧。首先，你应该找到 Erlang shell 的 PID：

有各种 `behaviours`，包括 Erlang 中使用的 `gen_server`、`gen_stat`、`gen_event` 和 `gen_behaviour`。`gen_server` 用于实现状态机，而 `gen_stat` 是实现有限状态机的新方法。`gen_behaviour` 用于实现通用功能。如果你愿意，可以开发自己的 `behaviours`。

```
3 = self().
```

由于进程不是字符串，以下命令将返回 `false`：

```
4 "0.61" == self().

false
```

所以，为了将代表有效 PID 的字符串转换为有效进程，你需要在 Erlang 或 Erlang shell 中执行以下操作：

```
5 list_to_pid("0.61") == self().

true
```

抱歉在教程中频繁引用 `child`。它有一个强制的一面。现在我们继续对 OTP 的努力。

在 `app.er` 中使用 `simple_start/link` 启动服务器以及如何使用 `crash/0` 崩溃服务器。这显示了监控器会自动重启服务器。带有 Erlang 代码的文件名为 `logging`。该文件的导入代码如下：

```
log_message(String)

  error_logger:info_msg("~p-n", [String]).

report_message(String)

  error_logger:info_report("~p-n", [String]).

warning_message(String)

  error_logger:warning_msg("~p-n", [String]).
```

以下 Erlang 代码分别定义了调用 `error_logger:info_msg/1`、`error_logger:info_report/1` 和 `error_logger:warning_msg/1` 的函数。在 Erlang shell 中执行 `logging.erl` 中的三个函数将显示：

```
2 = logging_message("This is a log message")

ok

> INFO REPORT===20-Mar-2017:10:02:12 ===

> "This is a log message"

3 = report_message("This is a report message")
```
