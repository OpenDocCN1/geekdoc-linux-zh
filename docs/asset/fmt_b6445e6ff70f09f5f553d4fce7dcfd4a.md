
## 安装服务脚本

RPM 版本的 Internet 服务器包含 `/etc/rc.d/init.d` 目录中的脚本，安装 RPM 软件包会在运行目录（如 `/etc/rc.d/rc3.d`）中安装相应的链接。如果你决定使用源代码创建服务器，可以手动安装启动脚本。如果没有启动脚本，首先复制 `httpd` 脚本——重命名并编辑将其所有对 `httpd` 的引用替换为你的服务器守护名称。然后将脚本副本放在 `/etc/rc.d/init.d` 目录中，并使用 `chkconfig` 在 `/etc/rc.d/rc3.d` 中创建链接。当你启动系统时，新服务器会自动启动并并发运行等待请求。

## 扩展 Internet 服务守护 (xinetd)

如果你对某个特定服务的请求很少，就不需要该服务一直运行。只有当远程用户访问其服务时才需要它。扩展 Internet 服务守护 (`xinetd`) 管理 Internet 服务器，仅当你的系统接收到服务请求时调用它们。`xinetd` 持续检查远程用户对特定 Internet 请求；当收到请求时，它启动相应的守护进程。

`xinetd` 程序旨在替代 `inetd`，提供安全增强、日志支持甚至用户通知。例如，通过 `xinetd`，当用户无法访问服务时向他们发送横幅通知并告知原因。`xinetd` 的安全功能可防止拒绝服务攻击、限制主机并发连接或限制传入连接的速率。`xinetd` 还整合了 `TCP`，无需调用 `tcpd` 守护即可提供安全的 TCP。此外，你不需要在 `/etc/services` 文件列出服务。`xinetd` 可以配置为启动任何特殊用途服务器。Red Hat Linux 7.0 及更高版本使用 `xinetd`。

## 启动和停止 xinetd 服务

你可以使用 `/etc/rc.d/init.d` 目录中的启动脚本启动、停止和重启 `xinetd`，如下：

```
# service xinetd
# service xinetd start
# service xinetd restart
```

在 Red Hat 上，你还可以像之前描述的那样使用 `chkconfig` 开启关闭特定的 `xinetd` 服务。我们使用 `on` 和 `off` 选项来启用或禁用服务。`config` 会编辑服务的禁用选项，将其值更改为关闭时的 `"yes"`，开启时的 `"no"`。例如，要启用 `swat` 服务器，你可以输入：

```
chkconfig swat on
```

## xinetd 配置：xinetd.conf

`xinetd.conf` 文件是 `xinetd` 的配置文件。其中的条目定义了在带有任何选项和安全预防请求时激活的不同服务器。每个条目由为不同功能定义的属性块组成，例如服务器程序名称、协议和安全限制。每个 Internet 服务（如服务器）的块之前都有 `service` 关键字，以及你标识它的名称。一对大括号括住了属性块。每个属性以属性名称开始，后面跟着赋值操作符（如 `=`），然后是分配的值或多个值。由 `default` 关键字指定的特殊块包含服务的默认属性。语法所示：

```
service <service_name>
{
<attribute> <assign_op> <value> <value>
...
}
```

## xinetd 属性

大多数属性接受单个值，你使用标准的赋值操作符 `=`。某些属性可以接受值列表。你可以使用 `=` 操作符分配值，但你

### 第五部分：Red Hat 服务器

还可以使用 `+` 和 `=` 运算符从这些列表中添加或删除项目。使用 `+` 添加值，使用 `=` 移除值。你经常使用 `+` 和 `=` 运算符将值添加到可能在默认块中已分配了初始值的属性中。

属性如表 20-6 所示。某些属性是服务必需的，包括 `socket_type` 和 `wait`。对于标准的 Internet 服务，你还需要提供用户（服务的服务的用户 ID）、`server`（服务的服务的名称）和 `protocol`（服务器使用的协议）。通过 `server_args`，你还可以列出任何你想传递给服务器程序的参数（这不包括像 `tcp` 那样的服务器名称）。如果未定义 `protocol`，将使用服务的默认协议。

```
service tftp
{
  socket_type = stream
  wait = no
  user = root
  protocol = ftp
  server = /usr/sbin/in.tftpd
  server_args = -1 -a
  disable = yes
}
```
