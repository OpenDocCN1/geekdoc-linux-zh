
# 第 6 章 WEB 服务器 7.0 请求处理

[04/May/2008:12:46:05] finest (1128): for host 127.0.0.1 trying to GET `/index.html`, func_exec reports: fn="ntrans-j2ee" name="j2ee" **Directive="NameTrans** returned -2 (`REQ_NOACTION`)

这两条条目表明服务器目前正在 `NameTrans` 阶段进行处理，并且刚刚完成了 `ntrans-j2ee` SAF 的执行。调用 SAF 的返回码为 `REQ_NOACTION`。这表示该 SAF 未采取任何操作，应该继续执行当前服务器阶段的下一个 SAF。
（完整的 SAF 状态列表请参阅表 6.3。）

[04/May/2008:12:46:05] finest (1128): for host 127.0.0.1 trying to GET `/index.html`, func_exec reports: executing fn="pfx2dir" from="/icons" dir="C:/Sun/WebServer7/lib/icons" name="internal" **Directive="NameTrans**

[04/May/2008:12:46:05] finest (1128): for host 127.0.0.1 trying to GET `/index.html`, func_exec reports: fn="pfx2dir" from="/mc-icons" dir="C:/Sun/WebServer7/lib/icons" name="internal" **Directive="NameTrans** returned -2 (`REQ_NOACTION`)

这两条条目表明服务器目前正在 `pfx2dir` 阶段进行处理，并且刚刚完成了 SAF 的调用。返回码为 `REQ_NOACTION`。这表示该 SAF 未采取任何操作，应该继续执行当前服务器阶段的下一个 SAF。这是 `NameTrans` 阶段处理的最后一个指令，且没有任何指令匹配成功。发生这种情况时，默认行为是根据 `$uri` 和 `$doctype` 变量的拼接创建一个文档路径。

[04/May/2008:12:46:05] finest (1128): for host 127.0.0.1 trying to GET `/index.html`, func_exec reports: executing fn="uri-clean" **Directive="PathCheck**

[04/May/2008:12:46:05] finest (1128): for host 127.0.0.1 trying to GET `/index.html`, func_exec reports: fn="uri-clean" **Directive="PathCheck** returned 0 (`REQ_PROCEED`)

这两条条目表明服务器目前正在 `PathCheck` 阶段进行处理，并且刚刚完成了 `uri-clean` SAF 的执行。调用 SAF 的返回码为 `REQ_PROCEED`。这表示该 SAF 成功实现了目标（清理 URI），并应该继续执行当前服务器阶段的下一个 SAF。（参考表 6.3 以了解为什么 `REQ_PROCEED` 码会让 `PathCheck` 指令继续处理。）

## 6.5 调试请求处理

乍一看，这些条目包含的信息似乎与 `PathCheck` 指令的放置冲突。事实并非如此。与创建默认文档根的内部 SAF 处理类似，`PathCheck` 指令在服务器日志中是隐藏的。你需要意识到每个请求在处理剩余阶段（`PathCheck`, `ObjectType`, `Service`, `AddLog`）时都会调用 SAF。

由于由于对象配置文件中引入了额外复杂性，该请求在处理剩余阶段时生成的其余条目被刻意省略了。这些条目包含的数据与已讨论的条目相似。表 6.3 包含了对每个 SAF 调用返回代码码的解释。其中某些返回码根据当前处理的阶段而具有不同的含义。理解这些代码有助于更好地理解请求处理。

### 表 6.3 SAF 返回码

| 返回码 | 解释 |
| --- | --- |
| `REQ_PROCEED` | | SAF 实现了其目标。[注：此处原文重复，修正为：]
| `REQ_PROCEED` | 表示 SAF 实现了其目标。对于某些请求-响应步骤（`AuthTrans`, `NameTrans`, `Service` 和 `Error`），此代码告诉服务器跳转到下一个请求-响应阶段，跳过当前阶段的所有其他 SAF。对于其他请求-响应步骤（`Input`, `Output`, `PathCheck`, `ObjectType` 和 `AddLog`），服务器将继续执行当前阶段的下一个 SAF。 |
| `REQ_NOACTION` | | SAF 未采取任何操作。服务器继续执行当前阶段的下一个 SAF。 |
| `REQ_ABORTED` | 表示发生了错误，并应向客户端发送 HTTP 响应以指示错误原因。返回 `REQ_ABORTED` 的 SAF 还应设置 HTTP 状态码。如果服务器发现匹配状态码或原因描述的 Error 指令，服务器将执行指定的指令并发送一个反映状态码和原因描述的短 HTML 页面。服务器跳转到第一个 `AddLog` 指令。 |
| `REQ_EXIT` | 表示与客户端的连接丢失。当 SAF 在读取或写入客户端失败时，应返回此代码。服务器跳转到第一个 `AddLog` 指令。 |

## 7.0 请求处理

通常，当你尝试排排除请求处理问题时，应该始终检查日志文件。如果日志文件中不包含足够帮助确定问题的信息，则你应该将日志级别增加到 `finest`。然后重现问题并再次检查日志文件。

## 6.6 总结

Web Server 7.0 中的请求处理比之前的版本更健壮。为了应对对象配置文件引入的额外复杂性，解析器被重写以捕获更多的配置错误并以逻辑方式处理其他错误。尽管如此，在实现容器和复杂的正则表达式时，很容易误配置你的 Web Server 实例。确保在对对象配置文件进行重大更新之前保存配置，并在非生产系统上彻底测试你的更改。但是，如果你犯了错误，请放心，你有多种调试技术可以帮助确定并解决问题。

## 6.7 自学实验室

使用本章包含的信息执行以下练习。这些将将验证你对本章描述概念的理解。

1. 通过以下步骤为终端用户主页提供支持：
   a) 在服务器上创建一个目录结构以包含用户目录，b) 在其下方创建新的特定于用户的目录，例如：
   - `/var/websites/people/rodale`
   - `/var/websites/people/wclay`
   - `/var/websites/people/relise`
   c) 在用户特定目录中填充示例 `index.html` 文件，并 d) 使用 `If Container` 和适当 `NameTrans` 指令访问内容。更新 `NameTrans` 指令以接受用户目录的大小写字母。

2. 创建单个容器和 `NameTrans` 指令以支持虚拟服务器内的别名和多个网站。使用正则表达式、表达式函数和反向引用来解决问题。参考以下项目：
   - `www.example.com` 映射到 `/var/websites/sites/www.example.com`
   - `w3.example.com` 映射到 `/var/websites/sites/www.example.com`
   - `example.com` 映射到 `/var/websites/sites/www.example.com`

3. 向服务器日志发送用户自定义消息，指示你正在使用的浏览器。

4. 为各种浏览器类型创建不同的网页（例如，`mozilla.html`, `msie.html`），并使用 `If/ElseIf/Else` 容器结构为每个浏览器显示不同的网页。

5. 使用管理控制台启用 CGI 作为目录的 `NameTrans` 指令。查看对对象 配置文件进行的更改（你应该看到一个针对 CGI `NameTrans` 指令的新 `pfxdir` SAF 条目）。验证你有一个在匹配 `NameTrans` 指令时调用 `cgi` 对象的项。在 CGI 目录下方放置一个输出 "Hello World!" 的脚本，并验证你可以访问/处理该脚本。

> 注意：访问 `http://www.sunwebserver.com` 可获得如何回答这些每个问题的详细说明。

6. 将日志级别更改为 `finest` 并重新创建生成步骤 1-6 响应的客户端请求。检查为每个客户端请求生成的条目。

## 监控 Web Server 7.0

**有效监控** Web Server 是维护最佳生产环境的基本任务。通过持续关注，你可以识别性能瓶颈，从而能够对系统进行调整以获得最佳性能。监控 Web Server 允许你通过确定何时需要额外的节点来服务不断增长的客户群，采取主动的容量规划方法。如果你计划在网站上添加新的服务或功能，且预计这会吸引更多访问者，那么这一点就至关重要。监控可以让你判断网站的配置是否正确，或者网页内是否存在错误的链接。它还能允许你检测并预测某些故障，在发生故障时进行根原因分析，并在某些情况下只需确保一切运行都符合预期。

本章解释了你用于监控 Web Server 的各种方法。这可能简单到关注 Web 日志文件，也可以是将统计数据存储在数据库中并查找趋势。你监控的内容、类型以及如何处理这些数据完全由你决定。

本章将介绍 Web Server 7.0 内部的监控子系统以及你如何使用各种工具从该子系统中提取数据。随后，它将探索如何评估数据模式，并利用这些知识微调你的 Web Server 性能。通常，我们将讨论以下主题：

- Web Server 统计数据
- Web Server 监控子系统
- 监控 Web Server 方法
- 如何使用监控数据调优 Web Server

## 7.1 Web Server 统计数据

Web Server 为收到的每个请求维护统计数据。这些数据允许你监控服务器活动并获取有助于微调系统的信息。统计数据显示了你的服务器处理了多少请求以及处理这些请求的情况如何。你可以查看单个虚拟服务器、服务器实例或跨多个节点配置的统计数据。

统计数据在每个节点与其注册的管理服务器（Administration Server）之间传输。因此，即使服务器实例已重启，你也可以查看统计数据。这在你需要排除一个停止响应或已重启的实例时特别有用。

统计数据可以按实例进行配置。与 Web Server 的之前的版本不同，Web Server 7.0 中的统计功能默认启用，并在 `server.xml` 文件中配置如下：

```xml
```
