
显然，基于主机的 X 认证并不是 X11R6 服务器最理想的访问控制类型。

## 基于令牌的认证 (Token-Based Authentication)

为了克服基于主机的认证的局限性，X 的设计者还实现了基于令牌交换系统的远程用户认证。当远程系统建立连接时，X 服务器会将其提供的魔法 cookie（magic cookie，一种唯一识别码）与存储在本地系统上的魔法 cookie 进行比较。如果两个 cookie 匹配，则允许访问。如果不匹配，则拒绝访问。假设只有拥有权限的用户才会提供 cookie。

通常情况下，一旦用户拥有了 cookie，它就会存储在位于 `$HOME/.authority` 的文件中，之后与 X 服务器交互时仅需少少干预。每次尝试连接时，都会自动读取远程服务器的 cookie 并将其作为身份交换的一部分提供。

实际实现要稍微复杂一些，但通过实践，它看起来可以像控制访问的 `xauth` 方法一样于管理。

### 使用 xauth 命令

在启用基于令牌的认证启动 X 服务器之前，必须先生成魔法 cookie 并将其添加到由 `xauth` 命令维护的魔法 cookie 文件中。用于操作基于令牌认证的魔法 cookie 和 cookie 文件的命令是 `xauth`。要生成 cookie 并将其添加到文件（通常位于 `$HOME/.authority`）中，你需要执行：

```
xauth add host:display keyvalue
```

`:display` 的值通常是运行 X 服务器的系统的主机名，后面跟上数字 0（零），除非你计划在多个设备上运行 X。`keyvalue` 应该是一个具有偶数位数字的大随机或伪随机值，据此生成魔法 cookie。例如，在主机名为 `station-john` 的工作站上，使用当前日期和时间的变体作为键值，你必须执行命令来生成魔法 cookie 并将其添加到认证文件中：

```
xauth add station-john:$ $(date +%S%M%H%y%d)
```

### 加固 X11R6 访问

如果你想将此 cookie 添加到 `$HOME/.Xauthority` 以外的其他文件，需要向 `xauth` 命令提供 `-f` 参数：

```
xauth -f /etc/xauth add station-john:0 $(date +%S%M%H%y%d%m)
```

要从认证文件中删除现有的 cookie，请使用 `remove` 参数以及匹配现有条目的字符串。例如，要删除刚刚为 `station-john` 添加的 cookie，使用：

```
xauth -f /etc/xauth remove station-john:0
```

在完成 cookie 操作后，从 cookie 文件移除魔法 cookie 是非常好的主意。要提取指定主机的魔法 cookie，请使用 `extract` 参数。例如，要将 `station-john` 的魔法 cookie 写入名为 `cookie.auth` 的文件，使用：`xauth extract cookie.auth station-john:0`

如果输出文件名为横杠 (`-`)，则 cookie 将发送到标准输出，可以在那里根据需要对其进行重定向或管道处理。要将提供的 cookie 合并到现有的授权文件中，请使用 `merge` 参数。例如，要将 `cookie.auth` 文件中的 cookie 合并到 `/etc/xauth` 授权文件中，使用：`xauth -f /etc/xauth merge cookie.auth`

如果输入文件名为横杠 (`-`)，则将从标准输入读取 cookie 然后将其纳入授权文件中。

### 启动 X 服务器

一旦你为系统和显示了魔法 cookie，使用基于令牌的认证启动 X 服务器就是件简单的事。只需向服务器提供 `-auth` 参数，随后是包含认证令牌的文件名。例如，以下任何一个命令都可能是正确的，取决于你的安装细节和服务器启动周围的情况：

```
X -auth /etc/X11/global-cookies
wwrapper -auth $HOME/.Xauthority
startx -- $HOME/.Xauthority
```

所有这些命令的效果相同：它们启动 X 服务器并指示其使用提供的 cookie 文件进行基于令牌的认证。服务器如果是这样启动的，它将能够在授予访问之前对连接请求进行魔法 cookie 挑战。

### 分发 Cookie

一旦使用基于令牌的认证启动服务器，将 cookie 提供给那些应该对运行中的 X 服务器有访问权限的用户或账户就至关重要。此此最简单的方法是如前所述，使用 `xauth` 命令的 `extract` 和 `merge` 参数。然而，在主机之间传输提取的 cookie 文件可能会很麻烦。因此，有一种经常用于交换 cookie 的快捷方法可能对你有帮助。

结合使用 `xauth` 命令、`rsh` 和管道，可以在 X 会话中将 cookie 从你的账户传输到另一个主机上的账户。假设远程主机名为 `foobar`，命令将是：

```
xauth extract :0 | rsh foobar xauth merge -
```

此命令指示 `xauth` 将当前显示的 cookie 放在标准输出，然后通过管道交给 `xauth` 命令。

![image](https://example.com/image.png) (文中提到的图像链接占位符)

此命令指示 `xauth` 将当前显示的 cookie 放在标准输出，然后通过管道交给 `xauth` 命令。

该问题的解决方案是使用 `ssh` 代替 `rsh`。

## 基于主机和基于令牌的交互

由于大多数 X 客户端与 X 服务器位于同一台机器上，因此自动化基于令牌认证的管理是可能的。这是通过 X 显示管理器（XDM）实现的，它包含在几乎所有的 X 安装中，并且现在在许多 Linux 安装中默认安装并运行。

### X 显示管理器 (XDM)

XDM 包含在几乎所有的 X 安装中，并且现在在许多 Linux 安装中默认安装并运行。

启动时，XDM 会自动生成魔法 cookie 并使用基于令牌的认证启动 X 服务器。随后 `xdm` 进程将提供图形登录界面而不是文本登录界面。当用户登录到 X 会话时，他的 `$HOME/.authority` 文件将更新，以包含本地 X 服务器的魔法 cookie。当他再次注销时，cookie 将被移除。

远程 X 会话也可以进一步自动化，使用 X 服务器的一个附加选项：字符串 `-query` 后面跟着运行 `xdm` 的主机名。例如，你本地 X 服务器上的几乎所有客户端都将来自运行 xdm 的主机 foobar。你可以如下方式启动本地 X 服务器：

```
X -query foobar
```

这将导致本地 X 服务器与你的账户 `foobar` 启动 cookie 交换，然后你就可以像在 `foobar` 上运行一样安全地登录 X 会话，如图 15.2 所示。

图 15.2

查询会话中的 X 显示管理器。

```
mysys.mynet.com

login:
Password:
```

有关使用 xdm 的更多信息，请参 `xdm(1)`。

## X 与数据包过滤

许多 X 服务器（包括 XFree86 服务器）不包含规定 X 服务器运行端口的功能。在 Linux 上最常用的 XFree86 服务器简单地从 6000 开始查找未占用的端口，并继续向上查找，直到找到一个为止。确保 6000 范围内至少有一个端口开放供 X 使用是至关重要的，并且如果你想在经过过滤的机器上允许网络 X 使用，你的过滤规则必须考虑到这一点。

对于网络 X 来说，端口 177 同样，它被 XDMCP 协议用于连接认证。通过 `ipchains` 和 `iptables` 允许网络 X 的数据包过滤规则如列表 15.2 和 15.3 所示。

### 列表 15.2 使用 ipchains 的包过滤规则

```
ipchains -A input -p tcp -s trusted.ext.system.ip \
  -d ext.ip.number.here 6000:6100 -j ACCEPT
ipchains -A input -p tcp -s trusted.ext.system.ip \
  -d ext.ip.number.here xdmcp -j ACCEPT
ipchains -A input -p udp -s trusted.ext.system.ip \
  -d ext.ip.number.here xdmcp -j ACCEPT
```

```
ipchains -A input -i lo \
  -d ext.ip.number.here 6000:6100 -j DENY -1
ipchains -A input -i lo \
  -d ext.ip.number.here xdmcp -j DENY -1
```

### 列表 15.3 使用 iptables 的包过滤规则
