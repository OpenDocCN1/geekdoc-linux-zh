

每子进程 MPM 使用此指令设置的值来确定同时运行的子进程数量。默认值 2 可能并不适合大多数系统。您可能希望将其设置为更高的限制，例如 15 或 20。更高的数值会生成更多的 Apache 进程，这意味着可以处理更多的同时连接。

## PidFile

参见 “MPM 线程特有指令” 章节下的 `PidFile` 指令。

## ScoreBoardFile

参见 “MPM 线程特有指令” 章节下的 `ScoreBoardFile` 指令。

## SendBufferSize

参见 “MPM 线程特有指令” 章节下的 `SendBufferSize` 指令。

## StartThreads

`StartThreads` 指令设置每个子进程的初始线程数。由于线程数是动态控制的，在大多数情况下，没有必要将其设置为高于默认值的数字。

- **语法：** `StartThreads number`
- **默认设置：** `StartThreads 5`
- **上下文：** 服务器配置

## User

参见 “MPM 线程特有指令” 章节下的 `User` 指令。

## MPM Winnt 特有指令

这是适用于所有 Windows 平台版本的 MPM，包括 Windows NT/2000/XP 和 Windows 9x/ME。此模块是多线程的；使用该模块时，Apache 将创建一个父进程和一个子进程。子进程创建处理请求的所有线程。此模块现在利用了一些 Windows 专用的原生函数调用，这使其在 Windows 平台上的性能优于早期版本的 Apache 服务器。

## CoreDumpDirectory

参见 “MPM 线程特有指令” 章节下的 CoreDumpDirectory 指令。

## Listen

参见 “MPM 线程特有指令” 章节下的 Listen 指令。

## ListenBacklog

参见 “MPM 线程特有指令” 章节下的 ListenBacklog 指令。

## MaxRequestsPerChild

参见 “MPM 线程特有指令” 章节下的 MaxRequestsPerChild 指令。

## PidFile

参见 “MPM 线程特有指令” 章节下的 PidFile 指令。

## SendBufferSize

参见 “MPM 线程特有指令” 章节下的 SendBufferSize 指令。

## ThreadsPerChild

参见 “MPM 线程特有指令” 章节下的 ThreadsPerChild 指令。

## MPM prefork 特有指令

prefork MPM 创建一个子进程池来提供服务请求。每个子进程只有一个线程。例如，如果 Apache 启动 30 个子进程，它可以同时服务 30 个请求。

如果出现问题且子进程死亡，则只丢失单个请求。子进程的数量通过最小和最大设置进行控制。当请求数量增加时，将添加新的子进程，直到达到最大值。同样，当请求减少时，多余的子进程会被终止。

## CoreDumpDirectory

参见 “MPM 线程特有指令” 章节下的 CoreDumpDirectory 指令。

## Group

参见 “MPM 线程特有指令” 章节下的 Group 指令。

## Listen

参见 “MPM 线程特有指令” 章节下的 Listen 指令。

## ListenBacklog

参见 “MPM 线程特有指令” 章节下的 ListenBacklog 指令。

## LockFile

参见 “MPM 线程特有指令” 章节下的 LockFile 指令。

## MaxClients

参见 “MPM 线程特有指令” 章节下的 MaxClients 指令。

## MaxRequestsPerChild

参见 “MPM 线程特有指令” 章节下的 MaxRequestsPerChild 指令。

## MaxSpareServers

此指令允许您设置服务器上空闲的 Apache 子进程数量。

- **语法：** `MaxSpareServers number`
- **默认设置：** `MaxSpareServers 10`
- **上下文：** 服务器配置

如果空闲的 Apache 子进程数量超过 MaxSpareServers 指令指定的最大数量，则父进程会终止多余进程。只有在非常繁忙的站点上，才需要调整此参数。除非您知道自己在做什么，否则请勿更改默认值。

## MinSpareServers

`MinSpareServers` 指令设置期望的空闲子服务器进程的最小数量。空闲进程是指未处理请求的进程。如果空闲的 Apache 进程数量少于 `MinSpareServers` 指令指定的数量，则父进程将以每秒最多 1 个的速度创建新的子进程。只有在非常繁忙的站点上，才需要调整此参数。除非您知道自己在做什么，否则请勿更改默认值。

- **语法：** `MinSpareServers number`
- **默认设置：** `MinSpareServers 5`
- **上下文：** 服务器配置

## PidFile

参见 “MPM 线程特有指令” 章节下的 `PidFile` 指令。

## ScoreBoardFile

参见 “MPM 线程特有指令” 章节下的 `ScoreBoardFile` 指令。

## SendBufferSize

参见 “MPM 线程特有指令” 章节下的 `SendBufferSize` 指令。

## StartServers

参见 “MPM 线程特有指令” 章节下的 `StartServers` 指令。

## User

参见 “MPM 线程特有指令” 章节下的 `User` 指令。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_135_0.png)
![](img/e11fcbd2818a3495ac70085e5d8d1c26_135_1.png)

## Apache 模块

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

表 5-1 中列出的模块使您可以操作可供其他模块或外部程序（如 CGI（通用网关接口）脚本、SSI（服务器端包含）、mod_perl 脚本、PHP 脚本、Java 服务程序等）使用的环境。

**表 5-1 环境相关模块**

| 模块 | 目的 |
| :--- | :--- |
| `mod_env` | 将环境传递给 CGI 和 SSI 脚本等外部程序。 |
| `mod_setenvif` | 使用来自客户端的信息设置条件环境变量。 |
| `mod_unique_id` | 此模块为每个请求生成唯一 ID。它没有指令。此模块默认未编译。您必须使用 `-enable-unique-id` 选项通过 `configure` 脚本配置源代码，并编译和安装 Apache。 |

## mod_env

`mod_env` 默认被编译。它使您可以将环境变量传递给外部程序，如 CGI 脚本、SSI、`mod_perl` 脚本、PHP 脚本等。`mod_env` 具有以下指令。

## PassEnv

`PassEnv` 指令告诉该模块将服务器自身环境中的一个或多个环境变量传递给 CGI 和 SSI 脚本。

- **语法：** `PassEnv variable [...]`
- **上下文：** 服务器配置，虚拟主机

例如，以下指令将 HOSTTYPE 和 PATH 环境变量传递给程序。

`PassEnv HOSTTYPE PATH`

