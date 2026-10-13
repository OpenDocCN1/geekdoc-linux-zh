
# service nfs start

```
# service nfs start
```

- 2. 要永久打开 NFS 服务，请输入：

```
# chkconfig nfs on
```

- 3. 如果您已配置防火墙，则必须确保 UDP 端口 111 和 2049 正在接受请求。（请参阅第 10 章，了解有关配置 `iptables` 或 `ipchains` 防火墙的信息。）

下几节将描述您刚刚创建的 `/etc/exports` 文件。此时，客户端只有在将其挂载到本地文件系统后才能使用您的共享目录。请参阅本章后面“使用 NFS 文件系统”部分。

## 配置 /etc/exports 文件

您输入到 NFS 服务器配置窗口中的共享目录信息将添加到 `/etc/exports` 文件中。作为 root 用户，您可以使用任何文本编辑器配置 `/etc/exports` 文件以修改共享目录条目或添加新条目。下面是 `/etc/exports` 文件的示例，其中包含它可能包含的一些条目：

```
/cal      *.linuxtoys.net(rw)                # Company events

/pub      (ro,insecure,all_squash)      # Public dir

/home     maple(rw,squash_uids=0-99) spruce(rw,squash_uids=0-99)
```

以下文本描述了这些条目：

- `/cal` — 代表包含与公司相关事件信息的目录。它对公司域（`*.linuxtoys.net`）中任何计算机上的所有有账户的用户开放。用户可以向目录写入文件，也可以读取文件（由 `rw` 选项表示）。注释（`# Company events`）只是提醒您目录包含的内容。
- `/pub` — 代表公共目录。它允许任何计算机和用户从目录读取文件（由 `ro` 选项表示），但不能写入文件。`insecure` 选项

允许任何计算机，甚至不使用安全 NFS 端口的计算机，访问该目录。`all_squash` 选项会导致所有用户（UIDs）和组（GIDs）映射到 `nfsnobody` 用户，从而使它们对文件和目录只有最小的权限。

- `/home` — 此条目使一组用户能够在不同计算机上拥有相同的 `/home` 目录。例如，假设你从名为 oak 的计算机共享 `/home`。名为 maple 和 spruce 的计算机各自可以将该目录挂载到自己的 `/home` 目录上。如果你在所有机器上为所有用户提供相同的用户名/UIDs，则无论用户登录哪台计算机，都可以为每个用户提供相同的 `/home/user` 目录。`squash_uids=0-99` 用于排除来自另一台计算机的任何管理员登录更改共享目录中任何文件。

当然，你可以共享你选择的任何目录（这些只是示例），包括整个文件系统（`/`）。共享整个文件系统或其敏感部分（如 `/etc/`）会带来安全隐患。可以在 `/etc/exports` 文件中添加的安全选项在以下各节中进行了描述。

`/etc/exports` 文件的格式是：

`Directory Host (Options) # Comments`

`Directory` 是你想要共享的目录的名称。`Host` 表示此目录共享所限制的主机计算机。`Options` 可以包含各种选项，用于定义针对主机所共享目录的安全措施。（你可以重复 `Host/Option` 对。）`Comments` 是你想要添加的任何可选注释（`#` 符号之后）。

## /etc/exports 中的主机名

你可以在 `/etc/exports` 文件中指定哪些主机计算机可以访问你的共享目录。请确保每个主机名之间有一个空格。以下是识别主机的方法：

- **单个主机** — 你可以输入一个或多个 TCP/IP 主机名或 IP 地址。如果主机在你的本地域中，只需指定主机名即可。否则，你可以使用完整的 `host.domain` 格式。以下是表示单个主机计算机的有效方法：

```
maple

maple.handsonhistory.com

10.0.0.11
```

- **IP 网络** — 要允许来自特定网络地址的所有主机访问，请指定网络号及其子网掩码，以斜杠（`/`）分隔。以下是表示网络号的有效方法：

```
10.0.0.0/255.0.0.0

172.16.0.0/255.255.0.0

192.168.18.0/255.255.255.0
```

- **TCP/IP 域** — 使用通配符，你可以包含来自特定域级别的所有或部分主机计算机。以下是星号和问号通配符的一些有效用法：

```
*.handsonhistory.com

*craft.handsonhistory.com

???.handsonhistory.com
```
