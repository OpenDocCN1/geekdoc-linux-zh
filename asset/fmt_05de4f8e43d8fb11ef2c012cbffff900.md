
$ docker pull debian

Using default tag: latest

latest: Pulling from library/debian

f50f925413f5: Download complete

d8d0657cb25f: Download complete

Digest: sha256:e7d3e8d35175...

Status: Downloaded newer image for debian

十六字符串是联合文件系统的层。如果同一个层被多个镜像使用，Docker 只需要一份。使用 `docker images` 查看本地可用镜像：

| 仓库 | 标签 | 镜像 ID | 创建时间 | 大小 |
|---|---|---|---|---|
| ubuntu | latest | 07c8617cdc4 | 2 周前 | 187.9 MB |
| ubuntu | wily | b5e99ec0d52 | 5 天前 | 136.1 MB |
| ubuntu | trusty | 9743da46f197 | 5 天前 | 187.9 MB |
| ubuntu | 15.84 | dib55fd07698 | 8 周前 | 131.3 MB |
| centos | 7 | d0e27f81cac65 | 2 周前 | 196.6 MB |
| centos | latest | d0e27f81cac65 | 2 周前 | 196.6 MB |
| debian | jessie | f50f925413f5 | 3 周前 | 125.1 MB |
| debian | latest | f50f925413f5 | 3 周前 | 125.1 MB |

为了确保下载镜像的完整性，你可以启用内容信任。此功能会验证发布者的签名。例如：

```bash
$ export DOCKER_CONTENT_TRUST=1
```

启用内容信任将防止你拉取未受信任的镜像。

# Docker：开源容器引擎

这台机器拥有了几个 Linux 发行版的镜像，包括刚刚下载的 Debian 镜像。同一个镜像可以被标记多次。请注意 `debian:essie` 和 `debian:latest` 共享同一个镜像 ID；它们是同一个镜像的两个名称。

有了镜像，运行一个基础容器非常简单：

```
# docker run debian /bin/echo "Hello World"
Hello World
```

发生了什么？Docker 根据 Debian 基础镜像创建了一个容器，并在其中运行了命令 `/bin/echo "Hello World"`。容器在命令退出后就会停止运行：在这种情况下，它在 `echo` 完成后立即停止。如果本地不存在 "debian" 镜像，守护进程将在运行命令之前尝试下载它。由于我们没有指定标签，因此默认使用了 "latest" 镜像。

我们使用 `-i` 和 `-t` 标志通过 `docker run` 启动了一个交互式 shell。从下文的命令在容器内启动了一个 `bash` shell，并将“外部” shell 的 I/O 通道连接到它。我们还分配了一个主机名，这在日志中标识它很有帮助。（否则，我们在日志消息中只会看到容器的随机 ID。）

```
root@host$ docker run debian -it /bin/bash
root@host# ls
 dev home lib m64 mnt proc run srv tmp var
 bot ec lib media opt root sbin sys usr
root@host# ps aux
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 1 0.5 0.4 26236 1884 ? Ss 19:02 0:00 /bin/bash
root 7 0.0 0.2 17492 1144 ? R+ 19:02 0:00 ps aux
root@host# uname -r
3.10.0-327.10.1.e17.x86_64
root@host# exit
exit
root@host# uname -r
3.10.0-327.10.1.e17.x86_64
```

这种体验与访问虚拟机的体验非常相似。它有一个完整的根文件系统，但进程树看起来几乎是独立的。`/bin/bash` 是 PID 1，是因为 Docker 是在容器内启动的。

`uname -r` 的结果在容器内外是相同的。情况将始终如此；我们展示这一点是为了提醒大家内核是共享的。

由于 PID 命名空间（namespace），容器中的进程无法看到系统上运行的其他进程。然而，主机上的进程可以看见容器进程。从容器内部看到的进程 PID 与从主机上可见的 PID 不同。

- 4. 这是 GNU 的 `echo`，不要与大多数 shell 内置的 `echo` 命令混淆。它们的作用完全相同。

# 第 25 章 容器

对于实际工作，你需要能够在后台运行并接受网络连接的长时间运行容器。以下命令在后台（`-d`）运行一个名为 'nginx' 的容器，该容器由官方 NGINX 镜像生成。我们将从主机的 80 端口隧道到容器内的相同 80 端口：

```
# docker run -p 80:80 --hostname nginx --name nginx -d nginx
Unable to find image 'nginx:latest'
latest: Pull from library/nginx
fd5d827ff33: Already exists
a3ed95caeb02: Pull complete
e6488abab39: Pull complete
2a76fa68fb0b: Pull complete
Digest: sha256a23a23b46f6893b9a13811f2c81b46cfac885cb141dfe4275ed23ca18492abe4
```

Status: Downloaded newer image for nginx:latest
镜像下载完成后，Docker 启动了容器并打印了它的 ID，这是一个唯一的 65 位十六进制字符串。

我们本地没有 "nginx" 镜像，因此 Docker 必须从仓库拉取它。镜像下载完成后，Docker 启动了容器并打印了它的 ID，这是一个唯一的 65 位十六进制字符串。

`docker ps` 显示运行中容器的简要摘要：

```
# docker ps
| IMAGE | COMMAND | STATUS | PORTS |
| --- | --- | --- | --- |
| nginx | nginx -g 'daemon off' | Up 2 minutes | 0.0.0.0:80->80/tcp |
```

我们没有告诉 docker 在容器内运行，因此它使用了镜像创建时指定的默认命令。输出显示该命令为 `nginx -g 'daemon off'`，它将 nginx 作为前台进程运行，而不是后台守护进程。容器本身没有 init 来管理进程，如果 nginx 服务器作为守护进程启动，容器将会在 nginx 进程派生（fork）并退出进入后台时立即退出。

大多数服务器都允许通过命令行标志来强制它们在前台运行。如果你的软件没有在前台运行，或者你需要在一个容器中运行多个进程，你可以分配一个如 `supervisord` 类的进程控制系统作为容器的轻量级 init。

由于 NGINX 在容器中运行并从主机映射了 80 端口，我们可以向容器发送请求。容器提供了一个通用页面：

```
root@host$ curl http://localhost:80/
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>This page is served by nginx.</p>
</body>
</html>
```
