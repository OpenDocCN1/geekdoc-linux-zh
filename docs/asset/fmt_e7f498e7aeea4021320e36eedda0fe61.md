
## RLIMITMEM

默认设置：未设置；使用操作系统的默认值

上下文：服务器配置 (Server config)，虚拟主机 (virtual host)

`RLIMITMEM` 指令接受两个参数。第一个参数为所有进程设置软资源限制，第二个参数（可选）设置最大资源限制。请注意，提高最大资源限制需要由 root 用户启动服务器。对于这些参数中的每一个，都有两种可能的取值：

- `n` 是每个进程的字节数
- `max` 是操作系统允许的最大资源限制

## RLIMITNPROC

`RLIMITNPROC` 指令设置了每个用户 ID 允许同时运行的 Apache 子派生进程的最大数量。

语法：`RLIMITNPROC n | 'max' [ n | 'max']`

默认设置：未设置；使用操作系统的默认值

上下文：服务器配置 (Server config)，虚拟主机 (virtual host)

`RLIMITNPROC` 指令接受两个参数。第一个参数为所有进程设置软资源限制，第二个参数（可选）设置最大资源限制。提高最大资源限制需要服务器以 root 身份运行或处于初始启动阶段。对于这些参数中的每一个，都有两种可能的取值：

- `n` 是每个进程的字节数
- `max` 是操作系统允许的最大资源限制

![](img/6d176ba5e3d859ca2b04a3bba254354c_124_0.png)

如果 CGI 进程在与服务器进程相同的用户 ID 下运行，则使用 `RLIMITNPROC` 将限制服务器可以启动（或“fork”派生）的进程数量。如果限制设置得太低，你将在错误日志文件中收到类型为“Cannot fork process”（无法派生进程）的消息。在这种情况下，你应该增加限制或直接保持默认值。

## LIMITREQUESTBODY

`LimitRequestBody` 指令允许你设置 Apache 服务的 HTTP 请求大小限制。默认限制为 0，意味着无限制。你可以将此限制设置为 0 到 2147483647 (2GB)。

语法：`LimitRequestBody bytes`

默认设置：`LimitRequestBody 0`

上下文：服务器 (Server)，虚拟主机 (virtual host)，目录 (directory), .htaccess

只有当你经历过基于 HTTP 的拒绝服务攻击（此类攻击试图通过大型 HTTP 请求淹没服务器）时，才建议设置限制。这是一个增强服务器安全性的有用指令。

## LIMITREQUESTFIELDS

`LimitRequestFields` 指令允许你限制单个 HTTP 请求中允许的请求头数量。此限制范围为 0 到 32767 (32K)。该指令可以帮助你实施针对基于大型请求的拒绝服务攻击的安全措施。

语法：`LimitRequestFields number`

默认设置：`LimitRequestFields 100`

上下文：服务器配置 (Server config)

## LIMITREQUESTFIELDSSIZE

`LimitRequestFieldsize` 指令允许你限制请求头字段的大小（字节）。默认大小 8190 (8K) 对于大多数情况已经足够了。然而，如果你遭遇了基于大型 HTTP 请求的拒绝服务攻击，将其更改为较小的数字以拒绝超过限制的请求。值 0 设置限制为无限制。

语法：`LimitRequestFieldsize bytes`

默认设置：`LimitRequestFieldsize 8190`

上下文：服务器配置 (Server config)

## LIMITREQUESTLINE

`LimitRequestLine` 指令设置了请求行的大小限制。这有效地限制了发送到服务器的 URL 大小。默认限制应足够应对大多数情况。如果你遭遇了使用长 URL 设计来浪费服务器资源的拒绝服务攻击，你可以减少限制以拒绝此类请求。

语法：`LimitRequestLine bytes`

默认设置：`LimitRequestLine 8190`

上下文：服务器配置 (Server config)

## 使用动态模块 (Using dynamic modules)

Apache 在启动时加载所有预编译模块；然而，它还提供了动态模块加载和卸载功能，这在某些情况下可能非常有用。当你使用以下动态模块指令时，你可以在不重新编译服务器的情况下更改活动模块列表。

### CLEARMODULE

你可以使用 `ClearModule` 指令来清除活动模块列表并启用动态模块加载功能。然后使用 `AddModule` 指令添加你想激活的模块。

语法：`ClearModuleList`

默认设置：无 (None)

上下文：服务器配置 (Server config)

### ADDMODULE

`AddModule` 指令可启用当前未激活的预编译模块。服务器带有一个预加载的活动模块列表；此列表可以使用 `ClearModule` 指令清除。然后可以使用 `AddModule` 指令添加新模块。

语法：`AddModule module`

默认设置：无 (None)

上下文：服务器配置 (Server config)

在你通过上述指令组合配置好 Apache 后，你就可以专注于调整你的静态和动态内容交付机制。在接下来的章节中，我将展示

## 加速静态网页 (Speeding Up Static Web Pages)

尽管动态内容是由数据库驱动或由复杂的应用程序提供的，但静态 Web页面仍然存在。事实上，在不久的未来静态页面不太被动态内容完全取代。某些动态系统甚至定期生成静态页面作为缓存以便更快交付。因为提供静态页面通常比提供动态页面快，因此静态页面不会消失。在本节中，我将使用 Apache 和新的内核 HTTP 模块提高静态页面交付的速度。

## 减少静态页面交付的磁盘 I/O (Reducing disk I/O for static page delivery)

当 Apache 接收到静态页面请求时，它会执行目录树遍历。如果 CGI 进程在与服务器进程相同的用户 ID 下运行，使用 `RLIMITNPROC` 将限制服务器可以启动（或“fork”派生）的进程数量。如果限制设置得太低，你将在错误日志文件中收到类型为“Cannot fork process”（无法派生进程）的消息。在这种情况下，你应该增加限制或直接保持默认值。

当 Apache 接收到静态页面请求时，它会执行目录树遍历。如果 CGI 进程在与服务器进程相同的用户 ID 下运行，使用 `RLIMITNPROC` 将限制服务器可以启动（或“fork”派生）的进程数量。如果限制设置得太低，你将在错误日志文件中收到类型为“Cannot fork process”（无法派生进程）的消息。在这种情况下，你应该增加限制或直接保持默认值。

当 Apache 接收到静态页面请求时，它会执行目录树遍历。如果 CGI 进程在与服务器进程相同的用户 ID 下运行，使用 `RLIMITNPROC` 将限制服务器可以启动（或“fork”派生）的进程数量。如果限制设置得太低，你将在错误日志文件中收到类型为“Cannot fork process”（无法派生进程）的消息。在这种情况下，你应该增加限制或直接保持默认值。

当 Apache 接收到静态页面请求时，它会执行目录树遍历。如果 CGI 进程在与服务器进程相同的用户 ID 下运行，使用 `RLIMITNPROC` 将限制服务器可以启动（或“fork”派生）的进程数量。如果限制设置得太低，你将在错误日志文件中收到类型为“Cannot fork process”（无法派生进程）的消息。在这种情况下，你应该增加限制或直接保持默认值。

当 Apache 接收到静态页面请求时，它会执行目录树遍历。如果 CGI 进程在与服务器进程相同的用户 ID 下运行，使用 `RLIMITNPROC` 将限制服务器可以启动（或“fork”派生）的进程数量。如果限制设置得太低，你将在错误日志文件中收到类型为“Cannot fork process”（无法派生进程）的消息。在这种情况下，你应该增加限制或直接保持默认值。

当 Apache 接收到静态页面请求时，它会执行目录树遍历。如果 CGI 进程在与服务器进程相同的用户 ID 下运行，使用 `RLIMITNPROC` 将限制服务器可以启动（或“fork”派生）的进程数量。如果限制设置得太低，你将在错误日志文件中收到类型为“Cannot fork process”（无法派生进程）的消息。在这种情况下，你应该增加限制或直接保持默认值。

当 Apache 接收到静态页面请求时，它会执行目录树遍历。如果 CGI 进程在与服务器进程相同的用户 ID 下运行，使用 `RLIMITNPROC` 将限制服务器可以启动（或“fork”派生）的进程数量。如果限制设置得太低，你将在错误日志文件中收到类型为“Cannot fork process”（无法派生进程）的消息。在这种情况下，你应该增加限制或直接保持默认值。
