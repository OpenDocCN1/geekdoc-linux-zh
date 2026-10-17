
你还可以在你的 NFS 条目中包含若干个 NFS 特有的挂载选项。你可以指定往返发送的数据包的大小，以及等待主机系统响应的时间。你还可以指定文件系统是进行硬挂载（`hard-mounted`）还是软挂载（`soft-mounted`）。对于硬挂载的文件系统，如果由于某种原因远程系统未能响应，你的计算机将不断尝试建立联系。软挂载的文件系统在指定的间隔后将放弃尝试建立联系并发布错误消息。硬挂载是默认设置。如果进行硬挂载的系统持续失败，它将由于不断尝试实现挂载而停止响应用户输入。出于某些原因，软挂载可能更好，因为它们会简单地停止尝试持续失败的挂载。表 40-2 和 Man 页包含了这些 NFS 客户端选项的列表。它们与之前指出的 NFS 服务器选项不同。

842 第七部分：网络管理

| 选项 | 描述 |
| --- | --- |
| `rsize=n` | NFS 在从 NFS 服务器读取文件时使用的字节数。默认值为 1,024。设置为 8,192 可以显著提高性能。 |
| `wsize=n` | NFS 在向 NFS 服务器写入文件时使用的字节数。默认值为 1,024。设置为 8,192 可以显著提高性能。 |
| `timeout=n` | 在超时后发送第一次重传之前的数值（以十分之一秒为单位）。默认值为 0.7 秒。 |
| `retry=n` | 在放弃之前重试 NFS 挂载操作的分钟数。默认值为 10,000 分钟（一周）。 |
| `retrans=n` | 在发生主超时之前，NFS 挂载操作的重传次数或次要超时次数（默认为 3）。此时，连接将取消，或显示“服务器未响应”的消息。 |
| `soft` | 使用软挂载挂载系统。 |
| `hard` | 使用硬挂载挂载系统。这是默认设置。 |
| `intr` | 允许 NFS 中断文件操作并返回到调用程序。默认是不允许中断文件操作。 |
| `bg` | 如果第一次挂载尝试超时，则在后台继续挂载。默认是失败且不进行后台运行。 |
| `tcp` | 使用 TCP 协议挂载 NFS 文件系统，而不是 UDP 协议。 |

## 表 40-2 NFS 挂载选项

这是一个 NFS 条目的示例。远程系统是 `rabbit.mytrek.com`，文件系统挂载在 `/home/projects`。该文件系统将挂载到本地系统的 `/home/dylan/projects` 目录。本地系统必须已经创建了 `/home/dylan/projects` 目录。系统类型为 NFS，`timeout` 选项指定本地系统最多等待 20 个十分之一（两秒）响应。软挂载可以被 NFS 中断。

```
rabbit.mytrek.com:/home/projects /home/dylan/projects nfs soft,intr,timeout=20
```

## 手动挂载：mount

你也可以使用带有 `-t nfs` 选项的 `mount` 命令显式挂载 NFS 文件系统。对于 NFS4 文件系统你会使用 `-t nfs4`。要显式挂载之前的条目，请使用以下命令：

```
# mount -t nfs -o soft,intr,timeout=20 \\abbit.mytrek.com:/home/projects /home/dylan/projects
```

当然，你可以使用 `umount` 命令卸载 NFS 文件系统。你指定挂载点，例如：

```
# umount /home/dylan/projects
```

第 40 章：NFS、NIS 和 GFS 843

注意 在 Fedora 系统上，你也可以使用 `fstab` 文件挂载和卸载所有文件系统。`start` 参数挂载 `fstab` 中的条目。`stop` 参数卸载文件系统，`restart` 参数重新挂载它们。

## 按需挂载 NFS：autofofs

你可以使用 `autofofs` 服务挂载 NFS 文件系统。这需要在客户端上进行配置。`autofofs` 服务只有在你访问它时才会挂载文件系统。进入指定的目录（`cd`）将触发该文件系统的自动挂载。

`autofofs` 服务使用主文件来配置以列出映射文件，映射文件列出文件系统。`/etc/auto.master` 是主文件。主文件将列出可以挂载文件系统的路径。`/auto` 目录已实现文件系统的根路径。如果你愿意，可以将自己的文件系统以及映射文件添加到 `/etc/auto.master` 文件中。你会发现 `/etc/auto.master` 包含 `/auto` 条目，使用 `auto.misc` 作为其映射文件：

```
/auto auto.misc --timeout 60
```

在映射文件之后，你可以像前面的示例那样添加选项。`timeout` 选项指定了尝试自动卸载之前的空闲秒数。

在映射文件中，你列出键、挂载选项以及文件系统。键将是本地系统中挂载文件系统的子目录。例如，为了将 `rabbit.mytrek.com` 主机上的 `/home/projects` 目录挂载到 `/auto/projects` 目录，你会使用：

```
projects soft,intr,timeout=20 rabbit.mytrek.com:/home/projects
```

你也可以在主文件中为文件系统创建一个新条目，如下所示：

```
/projects auto.projects --timeout 60
```

你会创建一个 `/etc/auto.projects` 文件并在其中放置 NFS 文件系统挂载的条目，如下：

```
dylan soft,intr,rw rabbit.mytrek.com:/home/projects
newgame soft,intr,ro lizard.mytrek.com:/home/supergame
```

注意 `autofofs` 服务可以用于任何文件系统，包括软磁盘和 CD-ROM。请参见第 32 章。

# 网络信息服务：NIS

在支持 NFS 的网络中，许多资源和设备由相同的系统共享。通常情况下，每个系统都需要为每个设备或资源准备属于自己的配置文件。任何更改都将需要逐个更新每个系统。然而，NFS 提供了一种名为网络信息系统（NIS）的特殊服务，它可以维护整个网络的配置文件。对于此类更改，你只需要更新 NIS 文件即可。NIS 适用于大多数管理任务所需的信息，例如与用户、网络访问或设备相关的信息。例如，你可以通过 NIS 服务维护用户和密码信息，只需更新 NIS 密码即可。

> 注意：NIS 是 NIS 的高级形式，提供了对加密和身份验证的支持。然而，它的管理起来更加复杂。

NIS 由太阳微系统公司（Sun Microsystems）开发，最初被称为 Sun 的黄页服务（YP）。NIS 文件存储在 NIS 服务器上（NIS 服务器有时也被称为 YP 服务器）。网络上的各个系统使用 NIS 客户端向 NIS 服务器发送请求。NIS 服务器在名为“映射（maps）”的特殊数据库文件中维护其信息。Linux 存在存在 NIS 客户端和服务器版本。Linux 客户端可以通过 NIS 轻松地连接到任何网络。

在大多数 Linux 发行版中，客户端作为初始安装的一部分进行。NIS 客户端程序包括 `ypbind`（NIS 客户端守护进程）、`yp`、`ypcat`、`yppoll`、`ymatch`、`passwd` 和 `yppset`。每个程序都有带有详细说明的 Man 页。NIS 服务器程序包括 `yps`（NIS 服务器）、`ypinit`、`passwd`、`yppush`、`ypfr` 和 `netgroup`——每个程序都有自己的 Man 页。你可以使用 `service` 命令启动和停止 `ypbind` 客户端守护进程和 `ypserv` NIS 服务器。或者，你可以使用 `system-config-services` 来启动和停止 NIS 客户端和服务器守护进程。

```
service ypbind start
service ypserv start
```

注意：你可以使用 `system-config-authentication` 指定网络上的远程 NIS 服务器。

# NIS 服务器

在设置 NIS 服务器时你有很大的灵活性。如果你的网络较小，可能只需要一个 NIS 域以及一个 NIS 服务器。对于较大的网络，你可以将网络划分为几个 NIS 域，每个域都有自己的所有者。即使你只有一个域，可能也需要若干 NIS 服务器和若干 NIS 从用服务器。从用服务器可以作为备份，以防主服务器宕机。从用服务器仅包含 NIS 主服务器上设置的配置文件的副本。

配置 NIS 服务器涉及几个步骤，列举如下：

- 定义 NIS 服务器将工作的 NIS 域名。
- 启动 `ypserv` 守护进程。
# 第 40 章：NFS、NIS 和 GFS
- 3. 在 `/var/yp/Makefile` 文件中，设置任何 NIS 服务器选项并指定要管理的配置文件。
- 4. 使用 `ypbind` 创建配置文件的 NIS 版本。

# 定义 NIS 域
