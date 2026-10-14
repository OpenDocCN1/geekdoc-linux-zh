
与浏览服务器最相关的 smb.conf 选项如下：

```
workgroup = name
```

将工作组设置为 name。

```
domain master = true|false|auto
```

将 domain master 设置为 true 会使 nmbd（NetBIOS 名称服务器）试图成为您所在工作组的域主浏览器。如果其他服务已经声明自己为主浏览器，nmbd 将不会尝试作为主浏览器运行。如果您在启动一个与您的工作组具有相同 NT 域名的 Windows NT 主域控制器之前，错误地使用此选项启动了 nmbd，则可能会出现浏览问题（网上邻居浏览器中缺少计算机、响应异常缓慢）。

```
local master = true|false
```

此参数设置为 true 时，将要求 nmbd 试图成为子网的本地主浏览器。如果您想使用此参数，请同时查看 WINS 服务器参数（wins server 和 wins support）；您可能需要在域主浏览器上设置一个 WINS 服务器，并使本地浏览器指向它。

## 问题 33

> 症状：虽然您希望 nmbd 成为您子网中的本地主浏览器，但另一台机器似乎占用了该角色，因此您在 lmhosts 文件中设置的主机映射没有出现在网络浏览器中。
> 
> 问题：您的 nmbd 在与 Windows 机器的本地主浏览器选举中落败。
> 
> 修复：使用 smb.conf 中的 OS level 参数。如果指定 OS level = 65，您将每次都能击败 NT 服务器。如果您正在处理一群您无法控制的机器，且它们的用户有打开所有服务的坏习惯，这会很有用。

## 名称解析与 lmhosts 文件

lmhosts 是一个简单的文件，将 IP 地址映射到 NetBIOS 名称。它看起来像这样：

```
10.1.1.37 CRUMMYNTBOX
10.1.1.4 SPIFFYLINUX
```

SAMBA 使用 lmhosts 进行直接的名称查找，这样就不必浪费时间通过网络请求 IP 地址。默认情况下，SAMBA 首先在 lmhosts 中查找 IP 地址。如果在 lmhosts 中没有找到所需内容，它会执行标准的主机解析（使用 /etc/nsswitch.conf 中设置的任何内容——通常是 /etc/hosts 和 DNS，按该顺序）。SAMBA 尝试的下一种方法是 WINS（请参阅下面的 WINS 部分）。如果所有这些都失败了，它就会在整个子网中广播请求。

要更改此默认行为，请设置 name resolve order 参数。例如，如果您只想让它使用 lmhosts 和 WINS 进行搜索，而不广播或使用标准 Internet 主机查找，请使用以下设置：

```
name resolve order = lmhosts wins
```

（用于广播和标准主机查找的参数值分别为 bcast 和 host。）

### 注意

默认情况下，lmhosts 文件位于 SAMBA 安装的 etc 目录中。您可以使用 nmbd 的 -H 文件选项来设置位置，但在撰写本文时，smbclient 还没有等效的选项。如果您计划将 lmhosts 放在默认位置以外的位置，请在默认位置放置一个指向该位置的符号链接。否则，在调试时可能会遇到困难。

## WINS

由于 NetBIOS 的局限性，您将需要一个 WINS 服务器来解析从一个子网到另一个子网的主机名（也就是说，如果您有多个子网的话）。该服务器类似于 DNS 服务器，但仅限于小型 NetBIOS 风格名称，并且您应该仅将其用于本地 Windows 网络。所有子网应该只有一个 WINS 服务器。以下是与 WINS 相关的 smb.conf 参数：

```
wins server = name|ip
```

name 或 ip 是一个 WINS 服务器。如果 SAMBA 需要通过 WINS 查找名称，它会查询此服务器。

```
wins support = true|false
```

此参数使 nmbd 充当 WINS 服务器。

```
dns proxy = yes|no
```

如果将此参数设置为 yes，当 nmbd 充当 WINS 服务器时，它将尝试通过 DNS 查找未知的 NetBIOS 名称。

## 更多访问控制选项

有时您需要更好地控制谁可以访问共享。以下大多数参数是按共享设置的——也就是说，您通常在 [global] 以外的节中指定它们。

```
allow hosts = list
```

此参数允许与 list 中的主机建立连接。其格式类似于 /etc/hosts.allow 的格式（参见第 2 章和 hosts_access(5) 手册页）。下面是一个示例：

```
allow hosts = @goodguys, 10.1.1.0/255.255.255.0 EXCEPT 10.1.1.37
```

@goodguys 是一个 NIS 网络组。

```
deny hosts = list
```

此参数拒绝来自 list 的连接。

## 问题 34

症状：虽然您使用了 deny hosts，但似乎仍有不期望的主机可以访问。
问题：allow hosts 对明确允许的主机拥有最终决定权。
修复：在 allow hosts 设置中使用 EXCEPT 关键字。

```
available = yes|no
```

设置为 no 将禁用共享。

```
guest ok = yes|no
```

设置为 yes 允许以访客身份访问共享（也就是说，访问时无需密码）。

```
guest only = yes|no
```

