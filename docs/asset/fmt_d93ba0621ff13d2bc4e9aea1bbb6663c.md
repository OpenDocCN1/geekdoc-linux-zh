
![](img/e11fcbd2818a3495ac70085e5d8d1c26_129_0.png)

`username`和`groupname`必须存在于你的系统中，Apache 才能使用它们。例如，在 Linux 系统上，`username`和`groupname`必须分别存在于`/etc/passwd`和`/etc/group`文件中。

#### `ConnectionStatus`

`ConnectionStatus`指令设置状态信息是否在内部存储。当设置为`on`时，使用状态信息的模块将正常工作。

- **语法：**`ConnectionStatus On | Off`
- **默认设置：**`ConnectionStatus On`
- **上下文：** 服务器配置

#### `CoreDumpDirectory`

参见“MPM threaded 专用指令”部分中的`CoreDumpDirectory`指令。

#### `Group`

参见“MPM threaded 专用指令”部分中的`Group`指令。

#### `Listen`

参见“MPM threaded 专用指令”部分中的`Listen`指令。

#### `ListenBacklog`

参见“MPM threaded 专用指令”部分中的`ListenBacklog`指令。

#### `LockFile`

参见“MPM threaded 专用指令”部分中的`LockFile`指令。

#### `MaxRequestsPerChild`

参见“MPM threaded 专用指令”部分中的`MaxRequestsPerChild`指令。

#### `MaxSpareThreads`

参见“MPM threaded 专用指令”部分中的`MaxSpareThreads`指令。

#### `MaxThreadsPerChild`

`MaxThreadsPerChild`指令设置每个子进程的最大线程数。默认数量是一个硬限制。如果你想更改此限制，必须修改相应的头文件。详见第 2 章中的表 2-3。

- 语法：`MaxThreadsPerChild number`
- 默认设置：`MaxThreadsPerChild 64`
- 上下文：服务器配置

#### `MinSpareThreads`

参见“MPM threaded 专用指令”部分中的`MinSpareThreads`指令。

#### `NumServers`

`NumServers`指令设置 Apache 创建的并发子进程数量。

- 语法：`NumServers number`
- 默认设置：`NumServers 2`
- 上下文：服务器配置

每子进程 MPM 使用此指令设置的值来确定同时运行的子进程数量。默认值 2 可能并不适合大多数系统。您可能希望将其设置为更高的限制，例如 15 或 20。更高的数值会生成更多的 Apache 进程，这意味着可以处理更多的同时连接。

#### `PidFile`

参见 “MPM 线程特有指令” 章节下的`PidFile`指令。

#### `ScoreBoardFile`

参见 “MPM 线程特有指令” 章节下的`ScoreBoardFile`指令。

#### `SendBufferSize`

参见 “MPM 线程特有指令” 章节下的`SendBufferSize`指令。

#### `StartThreads`

`StartThreads`指令设置每个子进程的初始线程数。由于线程数是动态控制的，在大多数情况下，没有必要将其设置为高于默认值的数字。

- **语法：**`StartThreads number`
- **默认设置：**`StartThreads 5`
- **上下文：** 服务器配置

#### `User`

参见 “MPM 线程特有指令” 章节下的`User`指令。

## MPM Winnt 特有指令

这是适用于所有 Windows 平台版本的 MPM，包括 Windows NT/2000/XP 和 Windows 9x/ME。此模块是多线程的；使用该模块时，Apache 将创建一个父进程和一个子进程。子进程创建处理请求的所有线程。此模块现在利用了一些 Windows 专用的原生函数调用，这使其在 Windows 平台上的性能优于早期版本的 Apache 服务器。

#### `CoreDumpDirectory`

参见 “MPM 线程特有指令” 章节下的`CoreDumpDirectory`指令。

#### `Listen`

参见 “MPM 线程特有指令” 章节下的`Listen`指令。

#### `ListenBacklog`

参见 “MPM 线程特有指令” 章节下的`ListenBacklog`指令。

#### `MaxRequestsPerChild`

参见 “MPM 线程特有指令” 章节下的`MaxRequestsPerChild`指令。

#### `PidFile`

参见 “MPM 线程特有指令” 章节下的`PidFile`指令。

#### `SendBufferSize`

参见 “MPM 线程特有指令” 章节下的`SendBufferSize`指令。

#### `ThreadsPerChild`

参见 “MPM 线程特有指令” 章节下的`ThreadsPerChild`指令。

## MPM prefork 特有指令

prefork MPM 创建一个子进程池来提供服务请求。每个子进程只有一个线程。例如，如果 Apache 启动 30 个子进程，它可以同时服务 30 个请求。

如果出现问题且子进程死亡，则只丢失单个请求。子进程的数量通过最小和最大设置进行控制。当请求数量增加时，将添加新的子进程，直到达到最大值。同样，当请求减少时，多余的子进程会被终止。

#### `CoreDumpDirectory`

参见 “MPM 线程特有指令” 章节下的`CoreDumpDirectory`指令。

#### `Group`

参见 “MPM 线程特有指令” 章节下的`Group`指令。

#### `Listen`

参见 “MPM 线程特有指令” 章节下的`Listen`指令。

#### `ListenBacklog`

参见 “MPM 线程特有指令” 章节下的`ListenBacklog`指令。

#### `LockFile`

参见 “MPM 线程特有指令” 章节下的`LockFile`指令。

#### `MaxClients`

参见 “MPM 线程特有指令” 章节下的`MaxClients`指令。

#### `MaxRequestsPerChild`

参见 “MPM 线程特有指令” 章节下的`MaxRequestsPerChild`指令。

#### `MaxSpareServers`

此指令允许您设置服务器上空闲的 Apache 子进程数量。

- **语法：**`MaxSpareServers number`
- **默认设置：**`MaxSpareServers 10`
- **上下文：** 服务器配置

如果空闲的 Apache 子进程数量超过`MaxSpareServers`指令指定的最大数量，则父进程会终止多余进程。只有在非常繁忙的站点上，才需要调整此参数。除非您知道自己在做什么，否则请勿更改默认值。

#### `MinSpareServers`

`MinSpareServers`指令设置期望的空闲子服务器进程的最小数量。空闲进程是指未处理请求的进程。如果空闲的 Apache 进程数量少于`MinSpareServers`指令指定的数量，则父进程将以每秒最多 1 个的速度创建新的子进程。只有在非常繁忙的站点上，才需要调整此参数。除非您知道自己在做什么，否则请勿更改默认值。

- **语法：**`MinSpareServers number`
- **默认设置：**`MinSpareServers 5`
- **上下文：** 服务器配置

#### `PidFile`

参见 “MPM 线程特有指令” 章节下的`PidFile`指令。

#### `ScoreBoardFile`

参见 “MPM 线程特有指令” 章节下的`ScoreBoardFile`指令。

#### `SendBufferSize`

参见 “MPM 线程特有指令” 章节下的`SendBufferSize`指令。

#### `StartServers`

参见 “MPM 线程特有指令” 章节下的`StartServers`指令。

#### `User`

参见 “MPM 线程特有指令” 章节下的`User`指令。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_135_0.png)
![](img/e11fcbd2818a3495ac70085e5d8d1c26_135_1.png)

# Apache 模块

在第 4 章中，我讨论了核心和多处理器模块（MPM）指令。Apache 提供了更多来自标准源代码分发中可用的模块指令。这些模块通过指令的使用提供了大量的功能。本章讨论这些模块及其指令。

## 模块概览

我不按字母顺序列出所有模块，而是根据功能相似性对模块进行了分组。这些模块分为以下类别：

- **环境相关：** 这些指令允许您设置和重置环境变量。
- **认证和访问控制：** 这些指令允许您验证和授权用户对网站受限部分的访问。
- **动态内容生成：** 这些指令允许您运行外部程序（如 CGI 脚本或服务器端包含）以创建动态内容。
- **内容类型配置：** 这些指令允许您控制文件的 MIME 类型。
- **目录列表：** 这些指令允许您控制目录列表的格式。
- **响应头：** 这些指令允许您控制 HTTP 响应头。
- **服务器信息和日志记录：** 这些指令允许您控制服务器日志和状态信息。
- **URL 映射：** 这些指令允许您为 URL 进行映射、重写和创建别名。
- **杂项模块：** 这些指令允许您控制 Apache 的杂项方面，例如代理服务、WEBDEV 模块等。

## 本章内容

- 如何使用环境模块
- 如何使用认证和访问控制模块
- 如何使用动态内容生成模块
- 如何使用目录列表模块
- 如何使用内容类型模块
- 如何使用动态内容生成模块
- 如何使用响应头模块
- 如何使用服务器信息和日志记录模块
- 如何使用 URL 映射模块
- 如何使用其他杂项模块

## 环境相关模块

表 5-1 中列出的模块使您可以操作可供其他模块或外部程序（如 CGI（通用网关接口）脚本、SSI（服务器端包含）、`mod_perl` 脚本、PHP 脚本、Java 服务程序等）使用的环境。

**表 5-1 环境相关模块**

| 模块 | 目的 |
| :--- | :--- |
| `mod_env` | 将环境传递给 CGI 和 SSI 脚本等外部程序。 |
| `mod_setenvif` | 使用来自客户端的信息设置条件环境变量。 |
| `mod_unique_id` | 此模块为每个请求生成唯一 ID。它没有指令。此模块默认未编译。您必须使用 `-enable-unique-id` 选项通过 `configure` 脚本配置源代码，并编译和安装 Apache。 |

## `mod_env`

`mod_env` 默认被编译。它使您可以将环境变量传递给外部程序，如 CGI 脚本、SSI、`mod_perl` 脚本、PHP 脚本等。`mod_env` 具有以下指令。

### `PassEnv`

`PassEnv` 指令告诉该模块将服务器自身环境中的一个或多个环境变量传递给 CGI 和 SSI 脚本。

- **语法：**`PassEnv variable [...]`
- **上下文：** 服务器配置，虚拟主机

例如，以下指令将 HOSTTYPE 和 PATH 环境变量传递给程序。

`PassEnv HOSTTYPE PATH`

### `SetEnv`

`SetEnv` 指令将环境变量设置为给定值，然后将其传递给 CGI/SSI 脚本。每个 `SetEnv` 指令只能定义一个变量和值对。

- **语法：**`SetEnv variable value`
- **上下文：** 服务器配置，虚拟主机

例如，下面的 `SetEnv` 指令将 `CURRENT_CITY` 变量设置为 `SACRAMENTO`：

```
SetEnv CURRENT_CITY SACRAMENTO
```

### `UnsetEnv`

`UnsetEnv` 指令从传递给 CGI/SSI 脚本的环境变量中移除一个或多个环境变量。这可用于确保 Apache 服务器可用的某些环境变量对您的 CGI 脚本不可用。

- **语法：**`UnsetEnv variable [ ... ]`
- **上下文：** 服务器配置，虚拟主机

例如，下面的 `UnsetEnv` 指令从环境变量列表中移除 `CURRENT_STATE` 变量：

```
UnsetEnv CURRENT_STATE
```

## `mod_setenvif`

`mod_setenvif` 模块默认在 Apache 中编译。它允许您使用 HTTP 请求中的信息创建自定义环境变量。您可以在重写 URL 或将用户重定向到不同页面时使用此类信息。

### `BrowserMatch`

当正则表达式匹配 HTTP 请求 User-Agent 头部中的模式时，`BrowserMatch` 指令会设置和取消自定义环境变量。User-Agent 头部由 Web 客户端（如 Web 浏览器、Web 机器人等）发送。

- **语法：**`BrowserMatch regex variable[=value] [ ... ]`
- **上下文：** 服务器配置

例如，下面的设置如果 HTTP 请求的 User-Agent 头字段包含单词 Mozilla，则将名为 `vbscript` 的变量设置为 `no`，并且因为该变量未指定值，所以名为 `javascript` 的环境变量被设置为 `1`：

```
BrowserMatch ^Mozilla vbscript=no javascript
```

让我们看另一个例子：

```
BrowserMatch IE vbscript !javascript
```

这里，如果在 User-Agent HTTP 请求头中找到单词 IE，则移除变量 `javascript` 并将 `vbscript` 设置为 `1`。`!` 字符会从环境中移除变量。

> **注意**：正则表达式匹配是区分大小写的。

### `BrowserMatchNoCase`

`BrowserMatchNoCase` 指令与 `BrowserMatch` 指令相同，除了它提供正则表达式的非区分大小写匹配。

- **语法：**`BrowserMatchNoCase regex variable[=value] [ ... ]`
- **上下文：** 服务器配置

例如，下面的指令匹配 MSIE、msie、Msie 等：

```
BrowserMatchNoCase ^MSIE vbscript=yes
```

### `SetEnvIf`

与 `BrowserMatch` 和 `BrowserMatchNoCase` 指令类似，`SetEnvIf` 指令允许您设置和取消自定义环境变量。实际上，`BrowserMatch` 和 `BrowserMatchNoCase` 是 `SetEnvIf` 的两个特殊版本。这两个指令只能对 User-Agent HTTP 请求头字段执行正则表达式，而 `SetEnvIf` 可用于所有请求头字段以及其他与请求相关的信息，如远程主机名（Remote_Host）、远程 IP 地址（Remote_Addr）、请求方法（Request_Method）、请求 URI（Request_URI）和引用者（Referer）。

- **语法：**`SetEnvIf attribute (regex envvar[=value] [ ... ])`
- **上下文：** 服务器配置

例如，如果 Remote_Host HTTP 头设置为 `yourdomain.com`，则下面的 `SetEnvIf` 指令将 `local_user` 变量设置为 `true`。

```
SetEnvIf Remote_Host "yourdomain\.com" local_user=true
```
