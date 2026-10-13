
以下示例设置了一个直接映射 `auto_direct`——包含一个自动挂载手册页的条目——并将其添加到 `auto_master` 映射中。

```
auto_direct.org_dir.wellard.COM.
```

| 表类型 | `automount_map` |
| :--- | :--- |
| 列数 | 2 |

### 从 NIS+ 主映射中删除条目

你可以使用 `nistbladm` 命令通过指定一个列从 NIS+ 自动挂载映射中删除行。

`nistblad -r` 选项的语法如下：

```
nistblad -r column= table-name,domainname
```

针对 NIS+ 的更具体语法如下：

```
nistblad -r column= auto_name.domainname
```

### 在自动挂载器中使用公共句柄

Solaris 7 版本扩展了 `mount` 和 `automount` 命令，使得挂载请求可以使用公共句柄代替 MOUNT 协议。这种访问方法是 WebNFS 服务使用的。通过绕过 MOUNT 协议，你可以跨越防火墙进行挂载。此外，由于服务器和客户端之间的事务更少，挂载速度更快。请参阅第 9 章“介绍 WebNFS”获取更多关于 WebNFS 协议的信息。

按照以下步骤在自动挂载器中使用公共句柄：

1. 成为超级用户。
2. 在自动挂载映射中添加条目

   `/usr/local -ro,public server:/filesystem`

## 216 设置自动挂载 (Automounter)

以下示例为 `castle` 上的 `/export/share/local` 文件系统添加了公共文件句柄。

```
/usr/local -ro.public castle:/export/share/local
```

`public` 选项强制使用公共文件句柄。如果 NFS 服务器不支持公共文件句柄，挂载将失败。

在某些情况下，使用 `-public` 选项可能会挂载失败。添加 NFS URL 也会让情况变得复杂。以下列表描述了在使用 `-public` 选项时文件系统是如何挂载的：

- 使用 NFS URL配合 `public` 选项会强制使用公共文件句柄。如果不支持公共文件句柄，挂载失败。
- 使用普通路径配合 `public` 选项会强制使用公共文件句柄。如果不支持公共文件句柄，挂载失败。
- 仅使用 NFS URL 时，如果 NFS 服务器已启用，则使用公共文件句柄。如果公共文件句柄挂载失败，请尝试挂载协议。
- 仅使用普通路径，不使用公共文件句柄。使用 MOUNT 协议。

默认的公共文件句柄（为 0000）会跳过从 `portmap` 服务获取信息并确定 NFS 端口号的所有事务。

## 在自动挂载中使用 NFS URL

Solaris 2.6 版本引入了 NFS 协议的扩展，使得互联网上的文件系统可以通过防火墙访问。该服务是 NFS 版本 3 和版本 2 协议的扩展。在重负载下，NFS 服务器提供的吞吐量大于通过超文本传输协议（HTTP）访问 Web 服务器。更高的吞吐量可以缩短检索所需的时间。此外，WebNFS 协议提供了在没有匿名 FTP 服务器管理开销的情况下共享文件的能力。

使用以下步骤在自动挂载中使用 NFS URL：

1. 变为超级用户。
2. 在自动挂载映射中添加条目：`/usr/local -ro nfs://server/filesystem`。

## 设置 NIS+ 自动挂载映射

以下示例为 `castle` 上的 `/export/share/local` 文件系统添加了 NFS URL。

```
/usr/local    -ro nfs:castle/export/share/local
```

关于 WebNFS 协议的更多信息，请参阅第 9 章“介绍 WebNFS”。

## 禁用自动挂载的浏览功能

自动挂载浏览功能在 Solaris 2.6 版本中引入。浏览功能允许所有潜在的挂载点均可见可见，无论它们是否已挂载。你可以使用 `-nobrowse` 选项关闭浏览功能。尽管默认的 `/etc/auto_master` 文件为 `/home` 和 `/net` 条目指定了 `-nobrowse` 选项，但在安装后，你可能需要手动更改或关闭特定站点 autofs 挂载点的浏览功能。

可以通过多种方式关闭浏览功能：

- 通过 `automd` 守护进程的 `-n` 命令行选项禁用浏览功能。该命令完全禁用 NFS 客户端的 autofs 浏览功能。
- 在使用 NIS 或 NIS+ 命名空间使用 autofs 映射的所有客户端上，禁用每个映射条目的浏览功能。
- 在未使用命名服务的情况下，禁用每个使用 autofs 映射的客户端上的每个映射条目的浏览功能。

### 如何完全禁用单个 NFS 客户端上的 Autoofs 浏览

使用以下步骤在 NFS 客户端上完全禁用 autofs 浏览功能：

1. 在 NFS 客户端上变为超级用户。
2. 以 root 身份编辑 `/etc/init.d/autofs` 脚本，并在启动自动挂载守护进程的行添加 `-n` 选项，如下。
3. 重启 NFS 客户端以重启 autofs 服务。

```
/usr/lib/autofs/automount -n <dev/null > /dev/console 2>&1 # start daemon
```

本节列出了由 `automount -v` 选项生成的自动挂载错误消息以及可能随时出现的错误消息。

## 自动挂载错误消息

### automount -v 错误消息

在排除自动挂载问题时，使用 `automount -v` 选项。以下列表显示了此命令生成的错误消息。

| Error | Description |
| :--- | :--- |
| bad key key in direct map mapname | 自动挂载在扫描直接映射时发现没有前缀 `/` 的条目键。直接映射中的键必须是绝对名称。 |
| bad key in indirect map mapname | 自动挂载在扫描间接映射时发现一个包含 `/` 的条目。间接映射键必须是相对的，而不是绝对路径名。 |
| can't mount server:pathname: reason | 服务器上的守护进程拒绝为 `server:pathname` 提供文件句柄。请检查服务器上的导出表。 |
| couldn't create mount point mountpoint: reason | 自动挂载无法创建挂载所需的挂载点。这种情况经常发生在 autofs 尝试分级挂载服务器的所有导出文件系统时。所需的挂载点可能存在于无法挂载（无法导出）的文件系统中，且由于导出的父文件系统是以只读方式导出的，因此无法创建。 |
| leading space in map entry text in mapname | 自动挂载在自动映射中发现一个包含前导的条目。此情况通常表示映射条目配置不当。检查映射条目以确保续行以反斜杠 (`\`) 正确结束。 |
| mapname: Not Found | 自动挂载无法找到所需的映射。此消息仅在使用 `-v` 选项时产生。检查映射名称的拼写和路径名。 |
| remount server:pathname: mountpoint: not responding | 自动挂载挂载已挂载项失败。 |

## 设置自动挂载

> 警告：`mountpoint` 已挂载

自动挂载正尝试挂载到

此错误消息意味着发生了内部自动挂载错误（异常）。

## 杂错误消息

- `dir mountpoint must start with '/'`: 自动挂载挂载点必须是绝对路径。检查挂载点的拼写和路径名。
- `host not responding`: 自动挂载尝试联系服务器但未收到响应。
- `hostname: exports: rpc_err`: 自动挂载在获取 `hostname` 导出列表时遇到错误。此消息表示存在问题。
- `map mapname, key: bad`: 条目格式错误，自动挂载无法解析。重新检查条目；可能条目包含必须转义的字符。
- `mapname: nis_err`: 在 NIS 映射中查找条目时出错。此消息表示 NIS 存在问题。
- `mount of server:pathname on mountpoint: reason`: 自动挂载执行挂载失败。此消息可能表示服务器或网络问题。
- `mountpoint: Not a directory`: 自动挂载无法挂载到 `mountpoint`，因为其不是一个目录。检查挂载点的拼写和路径名。
- `nfcast: cannot send packet: reason`: 自动挂载无法向文件系统列表中的服务器发送查询包。
- `nfcast: cannot receive reply: reason`: 自动挂载无法从文件系统列表中的任何服务器接收回复。

## 自动挂载错误消息

| Error | Description |
| :--- | :--- |
