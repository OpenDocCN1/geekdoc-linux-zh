
Kubernetes 是一个开源集群管理器，用于管理负载并适用于各种云架构。插图显示本文开始定义集群管理应用的基础知识，例如由 Google 发起的开源 Kubernetes 项目，以实现微服务架构。Kubernetes Pod 和命令行界面 `kubectl` 是用于调整编排和扩展运行时 Pod 数量的配置和工具。遵循该示例，我们将展示如何使用复制配置通过 `kubectl` 运行应用容器。

- 用于

- .NET Core 和 Core 镜像的 Docker 镜像概览

对于 `hub.docker.com` 上可用的 ASP.NET Core 容器化 Docker 镜像，第一类面向开发团队，包含了在开发背景下的 .NET 服务器生产级基础镜像，同时也作为当前版本。面向开发者的容器可以从此处下载：

```docker
FROM microsoft/dotnet:latest
```

或者你可以选择具有以下变体的 Docker 镜像：

```docker
FROM microsoft/dotnet:version-
```

另一类 Docker 镜像侧重于运行时，在某些背景下，减小 Docker 镜像的大小非常重要。

```docker
FROM microsoft/dotnet:core
```

# 12 与 NGINX 共存

Kestrel 是高性能 HTTP 服务器，作为 ASP.NET Core 技术的一部分用于跨平台托管。该 Web 服务器是一个新的工具，随着 1.0 版本的发布，它在功能上明显优于 Kestrel，并声称具有更好的安全性。最终结果是与 HTTP 引擎配合，每秒可以处理超过百万次的请求。

或者你可以选择具有以下变体的 Docker 镜像：

```docker
FROM microsoft/dotnet:version-
```

# Yeoman 和 Docker

Microsoft Image-Generator 在 GitHub 上作为一个开源项目存在。该生成器支持为 ASP.NET Core 生成 Docker 镜像生成，并帮助你使用该生成器构建更针对 ASP.NET Core 应用优化的 Docker 镜像，因此如果你喜欢 Yeoman 标准的 Docker 或其他 Docker 商业需求，它可能是你的工具。它还会生成 Bash 和 PowerShell 脚本来驱动 Docker 链，因此值得关注：

# 教程

# Ubuntu 系统管理

## 在 Ubuntu 中管理进程

## 深入观察 Ubuntu 进程

![](img/db87aeaad27e4efbbf36e01180be02e6_41_0.png)

| USER | PID | %CPU | %MEM | VSZ | RES | S | TTY | STAT | PRIME | NIO | TIME | COMMAND |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| top | | | | | | | | | | | | | |
| ps | | | | | | | | | | | | | |

`ps` 命令提供了一个面向屏幕、持续更新的运行命令列表。这里指出每个 Linux 系统都拥有 `ps` 命令。快速查看下 Ubuntu 系统上 `ps` 的一些示例。

```bash
$ ps -u
pswawan@VirtualBox:~$ ps -u
```

命令的输出在此显示：

Srakash 拥有计算机工程硕士学位。他在信息技术领域工作了多年，专注于操作系统、网络安全、电子产品、互联网服务、LDAP 和 Web 开发等领域。他编写过许多出版物并在行业会议上进行过演讲。可以通过 srakash.prakash@gmail.com 与他联系。

| PID | TTY | TIME | COMMAND |
|---|---|---|---|
| 7293 | | 00:00 | bash |
| 987 | | 00:00 | system |
| 986 | | 00:00 | system |
| 985 | | 00:00 | kworker |
| 1120 | | 00:00 | user |
| 1121 | | 00:00 | user |
| 1130 | | 00:00 | process |
| 1130 | | 00:00 | process |
| 1135 | | 00:00 | process |
| 1137 | | 00:00 | process |
| 1198 | | 00:00 | user |
| 1199 | | 00:00 | dbus-daemon |
| 1224 | | 00:00 | startup |
| 1243 | | 00:00 | getty |
| 1245 | | 00:00 | getty |
| 1302 | | 00:00 | dbus-daemon |
| 1364 | | 00:00 | user |

`ps` 命令提供了一个面向屏幕、持续更新的运行命令列表。这里指出每个 Linux 系统都拥有 `ps` 命令。快速查看下 Ubuntu 系统上 `ps` 的一些示例。

```bash
$ ps -u
pswawan@VirtualBox:~$ ps -u
```

命令的输出在此显示：
