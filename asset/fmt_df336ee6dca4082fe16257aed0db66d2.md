
现在您已经有了所需的容器镜像，可以使用它们来运行容器。容器处于以下状态之一：

- `Created`（已创建）：已创建但未启动的容器。
- `Running`（运行中）：正在运行的容器。
- `Stopped`（已停止）：进程已停止的容器。
- `Paused`（已暂停）：进程已暂停的容器。无 root 容器不支持。
- `Deleted`（已删除）：进程处于死亡状态的容器。

`podman ps` 命令列出系统上运行的容器。使用 `podman ps -a` 命令查看机器中的所有容器（已创建、已停止、已暂停或运行中）。

您使用 `podman create` 命令创建稍后运行的容器。创建容器时，您使用 `localhost/python36` 容器镜像的 ID。您还使用了用于设置容器名称的选项。命令的输出是容器的完整 ID。

```bash
[user@host ~]$ podman create --name python36 dd6ca291f097
5c4c72ee28158198cb9b60d78a0f94be083ae94dacbae69c05bd8cd354bbec
```

> 注意：如果你没有使用 `podman create` 或 `podman run` 命令的 `--name` 选项为容器设置名称，podman 工具将为容器分配一个随机名称。

随后，你使用 `podman ps` 和 `podman -a` 命令来验证容器是否已创建。你可以看到关于 `python36` 容器的信息，例如短 ID、容器名称以及启动时运行的命令，并可以启动你创建的容器。

```bash
[user@host ~]$ podman create --name python36 dd6ca291f097
5c4c72ee28158198cb9b60d78a0f94be083ae94dacbae69c05bd8cd354bbec
[user@host ~]$ podman ps -a
CONTAINER IMAGE COMMAND CREATED STATUS PORTS
PORTS NAMES CREATED STATUS
5c4c72ee2815 localhost/python36:1.0 /bin/bash -c slee... 5 seconds ago Created /python36
```

现在你已经验证了容器已创建，可以决定启动容器，因此运行 `podman start python36`。你可以使用名称或 ID 来启动容器。该命令的输出是容器的名称。

```bash
[user@host ~]$ podman start python36
python36
[user@host ~]$ podman ps
CONTAINER IMAGE COMMAND CREATED STATUS
PORTS NAMES CREATED STATUS
5c4c72ee2815 localhost/python36:1.0 /bin/bash -c slee... 6 minutes ago Up 3 seconds ago python36
```

# 第 11 章 | 运行容器

## 从远程仓库运行容器

你可以使用 `podman run` 一步创建并运行容器。`podman run` 命令在容器内部运行一个进程，该进程会启动新容器。

你使用 `podman run` 命令的 `-d` 选项以分离模式运行容器，容器会在后台运行而不是在会话中运行。在 `python36` 容器的示例中，你不需要为容器提供运行命令，因为在创建该容器镜像的文件中已经提供了 `sleep infinity` 命令。

为了创建 `python38` 容器，你决定使用 `podman run` 命令并引用 `registry.access.redhat.com/ubi8/python-38` 镜像。你还决定使用 `sleep infinity` 命令防止容器退出。

```bash
[user~$] podman run -d --name python38 \
registry.access.redhat.com/ubi8/python-38 \
sleep infinity
[user~$] podman ps
CONTAINER ID  STATUS    PORTS               NAMES               COMMAND
c547e2ee815c  localhost/python36:1                   /bin/bash -c
slee... 37 seconds  Up 30 seconds ago  python             python36
a0f71a2c1bba    .access.redhat.com/ubi8/python-38:latest sleep infinity
32 seconds ago  Up 33 seconds ago  python             python38
```

> 如果你使用全限定名称运行容器但镜像尚未存储，`podman run` 命令会先从仓库拉取镜像然后运行。

## 容器中的环境隔离

容器隔离应用程序的环境。每个容器都有自己的文件系统、网络和进程。当你查看 `ps` 命令的输出并比较主机和运行的容器时，可以注意到这种隔离功能。在主机上运行 `ps -ax` 会返回许多进程的结果。

```bash
[root@host ~]# ps -ax
PID TTY  STAT TIME COMMAND
ndeseriali\       S    0:00 /usr/lib/systemd/systemd --switched-root
2       S    0:00 [thread]
3       I<   0:00 [rcu]
4       I<   0:00 [rcu]
```

`podman` 命令在运行的容器内执行命令。容器取名称或 ID 作为后续参数在容器内运行。你使用 podman 命令查看 `python36` 容器中运行的进程。`ps` 命令的输出与主机不同。

```bash
[student~$] podman exec python38 ps -ax
PID TTY  STAT TIME COMMAND
1       S    0:00 /bin/coreutils-sleep=/usr/bin/sleep infinity
7       R    0:00 ps -ax
```

你可以使用 `sh -c` 命令来封装要在容器内执行的命令。如果封装 `ps -ax > /tmp/process`，Podman 可能将 `>` 解释为命令的一部分。你可以比较主机上安装的 python 版本与容器内安装的 python 版本。

```bash
[host ~]$ python3 --version
3.10
[host ~]$ podman exec python36 --version
3.6
[host ~]$ podman exec python38 --version
3.8
```

## 容器中的文件系统隔离

开发者可以使用文件系统隔离编写不同版本的应用程序，而无需使用多个物理或虚拟机。你在 `/tmp` 目录下创建一个显示 "hello world" 的简单 bash 脚本。

```bash
[host ~]$ echo "hello world" > /tmp/hello.sh
```

`/tmp/hello.sh` 在主机上存在，但在容器的文件系统内部不存在。如果你尝试使用 `podman exec` 执行该脚本，它会报错，因为容器中没有 `/tmp/hello.sh`。

```bash
[host ~]$ stat /tmp/hello.sh
File: /tmp/hello.sh
Size: 19 Blocks: 8 IO: 4096
Device: fc0a:6456 Inode: 1765599 Links: 1
Access: (rw-r--) (uid: 1000/user) (gid: 1000/user)
Context: unconfined_u:object_r:home_t:s0
Access: 2022-04-19 21:47:36.497588132 -0400
Modify: 2022-04-19 21:47:36.497588132 -0400
Change: 2022-04-19 21:47:36.497588132 -0400
Birth: 2022-04-19 21:45:24.785976758 -0400
```

```bash
[host ~]$ podman exec python38 stat /tmp/hello.sh
stat: '/tmp/hello.sh': No such file or directory
```

`podman cp` 命令在主机和容器系统之间拷贝文件。你可以使用 `podman cp` 命令将 `/tmp/hello.sh` 文件拷贝到 `python38` 容器。
