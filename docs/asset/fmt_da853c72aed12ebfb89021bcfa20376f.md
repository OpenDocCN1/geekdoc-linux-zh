
如果 RPC 运行正常，你会至少看到四个 `rpcbind` 列表条目（UDP 和 TCP 各两个）以及 NFS 守护进程 `portd` 的条目。在上面的示例中，没有 `portd` 条目，因此我们知道 NFS 守护进程尚未激活。

要想在系统中运行 NFS，必须在安装 Linux 时加载了 NFS 例程（运行安装脚本时，Linux 通常会提示你希望是否激活 NFS）。如果初始程序加载时未加载它，则需要通过你的 Linux 版本提供的任意磁盘集安装例程在需要时添加。某些系统（例如 Caldera 的 `OpenLinux` 和许多 `Slackware` 版本）在系统启动时会自动加载 NFS，无论你是否使用它。

## 配置 Linux 服务器

在大多数版本的 Linux 中，NFS 由名为 `/etc/nfs` 的脚本启动和停止。通过将该文件链接到启动例程，可以在系统启动时自动加载 NFS，即把 `/etc/nfs` 文件链接到 `/etc/rc2.d/Sname` 文件。为了正确关闭 NFS，还需要将 `/etc/nfs` 链接到 `/etc/rc0.d/Kname` 文件。如果希望手动启动和停止 NFS 守护进程，可以使用以下命令：

- `/etc/nfs start`
- `/etc/nfs stop`

> **注意**
>
> 某些版本的 Linux 使用不同的文件和目录来存储 NFS 脚本和配置信息。如果本章中提到的文件似乎不存在，请尝试使用 `/etc/rc.d/init.d/nfs` 或 `/etc/init.d/nfs` 作为启动脚本文件。

`/etc/nfs` 命令在发出适当指令时启动和关闭 NFS 服务器守护进程。发出启动命令时，激活的守护进程会回显到屏幕上：

```
$ /etc/nfs start
Starting NFS services: exportfs mountd nfsd pcnfsd biod(x4)
Starting NLM services: statd lockd
```

使用停止命令时，你会看到守护进程和服务器已关闭的消息：

```
$ /etc/nfs stop
NFS shutdown: [NFS Shutdown Complete]
```

要使 Linux 机器上的文件系统对其他系统上的 NFS 客户端可用，该文件系统必须列在 `/etc/exports` 文件中。在某些版本的 Linux 中，如果启动时存在 `/etc/exports` 文件，NFS 守护进程会自动启动。这将调用一个名为 `exportfs` 的程序，该程序将文件系统设置为可用于 NFS。如果在系统运行时对 `/etc/exports` 文件进行了更改，可以发出另一个 `exportfs` 命令或简单重启机器以使更改生效。

`/etc/exports` 文件的格式如下：

```
directory [ -option, option ... ]
```

`directory` 是被 NFS 共享（在 NFS 术语中称为导出）的目录或文件的路径名，`options` 可以从以下选项中选择：

- `ro` 将目录导出为只读。（默认值是导出为读写。）
- `rw=hostnames` 将目录导出为大多数情况只读，即对大多数机器只读，但对特定指定的机器可读可写。
- `anon=uid` 如果 NFS 请求来自未知用户，则使用 `uid` 作为所有权和权限的有效用户 ID。
- `root=hostnames` 允许指定机器的 `root` 用户获得 `root` 访问权限。
- `access=client` 授予每个列出的客户端挂载访问权限。客户端可以是主机名或网络组。

一个 `/etc/exports` 文件的示例有助于展示这些选项的用法。行首的井号（pound sign，即 `#`）表示注释。以下是一个 `/etc/exports` 文件示例：

```
/usr/stuff -ro # 向任何人导出为只读
/usr -access=clients # 向名为 clients 的组导出
/usr/public # 向任何人导出为可读可写
```

如果对 `/etc/exports` 文件进行了更改，请关闭 NFS 服务器守护进程并重新启动。发出 `exports` 命令，系统应该会显示所有导出文件系统的名称。此时，NFS 已准备好在你的服务器上使用了。

> **警告**
>
> 你可能会注意到，某些版本的 Linux 会创建一个名为 `/etc/xtab` 的新文件，其中包含文件系统信息。不要编辑此文件！你不应该修改其内容，否则 NFS 服务器将无法正常工作。`/etc/xtab` 文件是由 `exportfs` 命令生成的。

## 配置其他 Linux 服务器

某些版本的 Linux 使用 `share` 命令来设置用于导出的目录。（许多版本的 Linux 不支持 `share` 命令，因为该功能已在 `/etc/exports` 文件中重复实现。）`share` 命令的语法如下：

```
share -F nfs -o options -d description path
```

其中，`-F` 选项表明在 `path` 中给出的目录或文件将被设置为 NFS 文件系统。`-o` 后面的选项以与上述 `/etc/exports` 文件相同的方式设置访问类型。`-d` 选项后可以跟随一段描述性语句，供客户端描述导出的文件系统。例如，要将目录 `/usr/public` 共享为可读可写（默认），可以发出以下命令：

```
share -F nfs -d "Server public directory" /usr/public
```

你可以结合使用选项，如本例所示：

```
share -F nfs -o ro=artemis,anon=200 -d "Book material" /usr/tparker/book
```

此命令共享目录 `/usr/tparker/book`，并标记描述为"Book material"，对所有人提供可读可写访问，除了名为 `artemis` 的机器（对该机器为只读）。任何访问该系统的匿名用户都使用 UID 200。

单独使用 `share` 命令通常会显示所有已导出文件系统的列表。

## 设置 Linux 客户端

Linux 可以使用 `mount` 命令挂载来自另一台机器的 NFS 导出文件系统。挂载 NFS 文件系统的语法如下：

![](img/e8e6b47ac20475e23d48b4c476f5d891_778_0.png)

```
mount -F nfs -o options machine:filesystem mount-point
```

`-F` 选项告诉 `mount` 命令该文件系统是 NFS 文件系统，`machine:filesystem` 是要挂载的远程机器名称和文件系统，`mount-point` 是远程文件系统在当前文件系统中的挂载位置。某些版本的 Linux 对语法做了一些更改。例如，某些版本使用小写 `f` 和大写 `NFS` 来表示类型。请查阅手册页以获取你的版本的确切语法。

在实际使用中，`mount` 很容易操作。例如，以下命令在本地机器的 `/usr/artemis` 目录中挂载名为 `artemis` 的远程机器上的 `/usr/public` 文件系统：

```
mount -F nfs artemis:/usr/public /usr/artemis
```

挂载点（在本例中为 `/usr/artemis`）必须存在，挂载才能成功。

`mount` 命令的 `-o` 可选组件可用于设置以下列表中的选项：

- `rw` 将挂载设置为可读可写（默认值）。
- `ro` 将挂载设置为只读。
- `timeout=x` 在放弃之前尝试挂载的超时值，单位为 0.1 秒。
- `retry=x` 在放弃之前重试 `x` 次。
- `soft` 如果未收到远程确认，则强制客户端放弃挂载尝试。
- `hard` 客户端继续尝试挂载文件系统，直到成功为止。
- `intr` 允许键盘中断挂载请求；否则，尝试将无限期进行。

这些选项中的任何一个都可以在一个 `mount` 命令中结合使用，就像在 `share` 命令中一样。例如，以下命令行尝试将 `artemis` 上的 `/usr/public` 目录挂载为只读，但如果 `artemis` 未确认挂载尝试，则放弃：

```
mount -F nfs -o soft,ro artemis:/usr/public /usr/artemis
```

单独使用 `mount` 命令通常会显示所有已挂载的文件系统。

还有一种更简单的方法来挂载常用目录。将目录名称及其挂载点放入 `/etc/fstab` 或 `/etc/vfstab` 文件中（使用哪个文件取决于 Linux 的版本）。然后，你只需输入挂载点名称即可挂载这些文件。例如，以下命令将正确的文件系统挂载为 `/skunk`：

`mount /skunk`

## 摘要

正如本章所示，作为客户端或服务器，NFS 的设置并不复杂。只需几分钟的工作，你就可以开始共享目录并访问其他机器上的目录。NFS 是访问远程机器上的应用程序和复制文件的一种非常快速且简单的方法。虽然配置取决于操作系统版本，但快速查看帮助屏幕或 `man` 页面将向你展示本章中使用的命令的正确格式。

从这里你可以找到相关信息：
