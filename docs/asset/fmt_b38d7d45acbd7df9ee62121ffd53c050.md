
# service nfs start

```
2. 要永久开启 NFS 服务，输入：
```bash
# config nfs
```
```

3. 如果您配置了防火墙，请确保 UDP 端口 `111` 和 `2049` 接受请求。（配置防火墙的信息请参见第 14 章。）

接部分将介绍您刚刚创建的 `/etc/exports` 文件。此时，客户端只有在将其挂载到本地文件系统时才能使用您的共享目录。请参阅本章后后的“使用 NFS 文件系统”部分。

# 配置 `/etc/exports` 文件

您在 NFS 服务器配置窗口中输入的共享目录信息被添加到 `/etc/exports` 文件中。`root` 用户，您可以使用任何文本编辑器来配置和修改 `/etc/exports` 文件。

`/etc/exports` 文件的格式为：

```
Directory Host (Options) # Comments
```

- `Directory`（目录）是您想要共享的目录名称。
- `Host`（主机）表示共享限制在哪些主机。
- `Options`（选项）可以包含各种选项，用于定义附加到目录的安全措施。
- `Comments`（注释）是符号 `#` 之后的的任何可选注释。

# `/etc/exports` 中的主机名

您可以在 `/etc/exports` 文件中指定哪些主机可以访问您的共享目录。确保每个主机名之间有空格。以下是标识主机的方法：

- **单个主机（Individual host）** — 输入一个或多个 TCP/IP 主机名或 IP 地址。如果主机位于本地域，可以指定主机名。否则，可以使用 `host.domain` 格式。以下是标识计算机的有效方法：

```
maple
map.handsonhistory.com
10.0.0.11
```

- **IP 网络（IP network）** 要允许特定网络的所有主机，请指定名称及其掩码，并用斜杠 `/` 隔开。以下是标识网络数的有效方法：

```
10.0.0.0/255.0.0
172.16.0.0/255.255.0.0
192.168.0.0/24
192.168.18.0/255.255.255.0
```

- **TCP/IP 域（TCP/IP domain）** — 使用通配符，可以在此处包含域层级的所有或部分主机计算机。以下是使用星号和问号通配符的有效方法：

```
*.handsonhistory.com
*craft.handsonhistory.com
???.handsonhistory.com
```

第一个示例匹配 `handsonhistory.com` 域中的所有主机。第二个示例匹配 `handsonhistory.com` 域中以 `woodcraft`、`basketcraft` 或任何以 `craft` 结尾的主机名。最后一个示例匹配该域中任何三个字母的主机名。

> NOTE：
>
> 注意：您也可以用空格分隔多个主机名，但如果您为每个主机添加了选项，请在主机名与括号之间不要留空格。例如：
>
> `*.handsonhistory.com (rw) *example.net (ro)`

## 第 18 章：设置文件服务器

- NIS 组 — 你可以允许包含 NIS 组中的主机进行访问。要指定 NFS 组，请在组名前加上 `@` 符号（例如，`@group`）。

## `/etc/exports` 中的访问选项

当你通过 NFS 导出一个目录时，并不非交出你的文件和目录。在 `/etc/exports` 中每个条目的选项中，你可以通过设置读/写权限来添加允许或限制访问的选项。这些传递给 NFS 的选项包括：

- `ro` — 仅允许客户端只读地挂载此导出的文件系统。默认是以读/写方式挂载文件系统。
- `rw` — 显式请求以读/写权限共享目录。（如果用户选择，他们仍然可以只读方式挂载该目录。）

## `/etc/exports` 中的用户映射选项

此外，如果通用处理权限，你还可以使用选项来设置特定用户对 NFS 文件系统的权限。

简化此过程的方法是让拥有多个用户账户的用户在每台机器上具有相同的用户名和 UID。这使得映射用户变得更容易，使他们在挂载的文件系统上的权限与它们存储在本地磁盘上的文件权限相同。如果这种方法不方便，可以通过许多其他方式映射用户 ID。以下是设置权限的方法以及每种方法使用的 `/etc/exports` 选项：

- `root` 用户 — 通常，客户端的 `root` 用户被映射为 `nfsnobody` 用户（UID `65534`）。这防止了客户端计算机的 `root` 用户能够更改共享文件系统中的所有文件和目录。如果你在服务器上拥有 `root` 权限，请使用 `no_root_squash` 选项。

> 提示：除了 `root` 之外，可能还有你想压缩（squash）的管理员用户。我建议如下如下压缩 UIDs：`squash uids=0-99`。

- `nfsnobody/group` — 通过使用 `nfsnobody` 用户名和组名，你本质上创建了一个用户/组，其权限将不允许访问服务器上任何用户的文件（除非这些用户设置了所有人权限）。然而，由 `nfsnobody` 用户或组创建的文件，任何被分配为 `nfsnobody` 用户或组的人都可以访问。将所有用户设置为 `all_squash` 选项。

`nfsnobody` 用户被分配了 UID 和 GID 为 `65534`。这防止了该 ID 与有效的用户或组 ID 冲突。使用 `anuid` 或 `anongid` 选项可以分别更改 `nfsnobody` 用户或组。例如，`anonuid=175` 将所有匿名用户设置为 UID `175`，而 `anongid=300` 将 GID 设置为 `300`。（但是，当你列出文件权限时只会显示数字，除非你为 `/etc/password` 和 `/etc/group` 为新的 UID 添加条目。）

- 用户映射 — 如果相同的用户在一组计算机上有登录账户（并且它们具有相同的 ID），NFS 默认将映射这些 ID。这意味着如果用户在挂载点（`mike`, UID `110`）上使用用户名 `mike` (UID `110`)，他就可以使用来自其他计算机的远程挂载文件。

如果服务器上没有设置的客户端用户在挂载的 NFS 目录上创建文件，它将被分配给客户端的 UID 和 GID。（在服务器上运行 `ls -1` 将显示所有者的 ID）。你可以使用 `map_static` 选项来识别包含用户映射的文件。

> 提示：`exports` 管理 `map_static` 选项，它应该允许你创建一个包含新 ID 映射的文件。这些映射应让你将客户端 ID 重新映射为服务器上不同的 ID。

## 导出文件系统

在你向 `/etc/exports` 文件中添加条目后，你可以使用 `exports` 命令手动导出目录。如果你重启电脑或重启 NFS 服务，`exports` 命令将自动运行以导出你的目录。然而，如果你想立即导出它们，可以通过从命令行（以 `root` 身份）运行 `exports` 来实现。

> 提示：在更改 `exports` 文件后运行 `exports` 命令是一个是一个好主意。如果文件中存在任何错误，`exports` 将为你识别这些错误。如果你无法立即从客户端访问更改后的 NFS 共享，你可能需要重启 NFS 和 `portmap` 服务。

这里是 `exports` 命令的一个示例：

```
# /usr/sbin/exportsfs -a -v
exporting maple:/pub
exporting spruce:/pub
exporting maple:/home
exporting spruce:/home
exporting *:media/win
```

`-a` 选项表示 `/etc/exports` 中的所有目录都应该被导出。`-v` 选项允许打印详细输出。在这个示例中，本地服务器的 `/pub` 和 `/home` 目录可供命名为（`maple` 和 `spruce`）的计算机挂载。`/media/win` 目录对所有计算机可用。

运行 `exportsfs` 命令将使你导出的 NFS 目录立即可用。对 `/etc/exports` 文件的更改将在下一次重启或重启 NFS 服务时再次生效。

## 启动 `nfsfd` 守护进程

出于安全考虑，你的 Fedora 或 RHEL 系统上默认关闭了 NFS 服务。你可以使用 `chkconfig` 命令开启 NFS 服务，以便在系统启动时导出你的文件并运行 `nfs` 守护进程。

对于 NFS 服务，有两个想要开启的启动脚本。NFS 服务监听请求。`nfsfd` 守护进程处理导出的文件系统。`lockd` 守护进程允许文件锁定。

> 提示：如果你看到“Cannot register RPC: connection refused”消息，你可能需要重启 `portmap` 服务。你可以使用 `chconfig` 命令开启 NFS 服务：

```
# chconfig nfs on
```

下次重启时，NFS 服务将启动。如果你想立即启动，请使用：

```
# /init.d/nfs start
```
