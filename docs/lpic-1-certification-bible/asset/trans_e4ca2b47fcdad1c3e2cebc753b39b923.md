
## `xhost` 命令

`xhost` 命令还可以用于检查是否允许在远程系统上显示客户端。这通过将 `DISPLAY` 变量更改为远程主机的值，然后运行 `xhost` 来实现。例如，要查看是否能在 `redhat.the-nashes.net` 上显示应用程序，您可以输入：

```
export DISPLAY=redhat.the-nashes.net:0.0
xhost
```

`DISPLAY` 变量将在下一节中详细介绍。

`xhost` 命令使用一些简单的命令行选项。要启用基于主机的身份验证并清除所有允许的主机，请使用 `xhost -`。例如：

```
[root@redhat /root]# xhost -
access control enabled, only authorized clients can connect
```

要禁用所有身份验证并允许任何人连接到您的系统并显示应用程序，请输入 `xhost +`。例如：

```
[root@redhat /root]# xhost +
access control disabled, clients can connect from any host
```

> 注意：运行 `xhost +` 是个坏主意，因为任何用户都可以连接到您的 X 服务器。

授权主机连接也是使用 `+` 选项完成的。例如，要允许三个主机连接，请输入以下内容：

```
[root@redhat /root]# xhost +dedee +marvin +brain
dedee being added to access control list
marvin being added to access control list
brain being added to access control list
```

要从允许列表中移除主机，请使用 `-` 选项。例如，要移除 `dedee`，请输入以下内容：

```
[root@redhat /root]# xhost -dedee
dedee being removed from access control list
```

最后，为确保您的身份验证正确，只需输入 `xhost`：

```
[root@redhat /root]# xhost
access control disabled, clients can connect from any host
INET:brain
INET:marvin
```

> 考试提示：主机身份验证方法是通过 `xhost` 命令配置的。

## 配置远程客户端

您可以用两种基本方法告知客户端应用程序在远程系统上显示。第一种方法是使用 `DISPLAY` 环境变量。`DISPLAY` 变量的格式如下：

```
DISPLAY=hostname:display.screen
```

例如：

```
DISPLAY=marvin.the-nashes.net:0.0
```

主机名字段可以是 DNS 名称或 IP 地址。如果远程系统上的 X 服务器只有一个用户在使用，显示编号将为 0。屏幕编号仅用于多屏幕环境，如果只使用一个屏幕，可以省略。更改 `DISPLAY` 变量后，如果身份验证允许，任何启动的 X 客户端将自动在变量指定的系统上显示。

远程显示客户端的第二种方法是使用大多数客户端使用的 `-display` 命令行参数。语法如下：

```
xclient -display hostname:display.screen [xclient arguments]
```

请注意，格式与 `DISPLAY` 变量相同。如果您希望仅在另一个系统上显示一两个客户端，这非常有用。

## 配置远程登录

XDM 的另一个非常实用的功能是允许您远程登录到另一个系统，并将本地系统仅用于显示。您还可以配置系统，为客户端提供可能的登录系统菜单。此功能的基础由 XDMCP（X 显示管理器控制协议）提供和控制。此配置应与支持 XDMCP 的任何 X 客户端和服务器兼容。

> **交叉参考**
>
> Linux 终端服务器项目创建了一种用于无盘工作站的登录系统。您可以在 http://www.ltsp.org 找到更多信息。

### 登录远程系统

如果远程系统正在运行 XDM，则很容易在 X 内部登录到该系统并从中执行应用程序。使用的语法如下：

```
X -query <server_name>
```

X 还支持在本地网络上广播以查找运行 XDM 的任何服务器。这通过以下命令完成：

```
X -broadcast
```

Linux 系统也可以设置为提供选择器，这是您可以登录的主机列表。要请求选择器，请使用以下命令：

```
X -indirect <server name>
```

> 考试提示：请务必为考试了解这三个命令之间的区别。

## 配置 XDM 提供选择器

要配置 XDM 提供选择器，您需要修改 `/etc/X11/xdm/Xaccess` 文件。您需要在文件中添加一个或多个选择器指令。它们的格式如下：

```
client CHOOSER server_list
```

`client` 条目定义了哪些工作站将被提供选择器列表，而 `server_list` 指定了哪些服务器将出现在选择器中。可以在客户端主机列表中指定通配符。以下是一个示例：

```
*.the-nashes.net      CHOOSER     marvin brain
Norbert              CHOOSER     brain
!bugs
*                    CHOOSER     dag
```

如果主机匹配多行，则使用遇到的第一行。这些行定义了以下内容：

- 第一行指定 `the-nashes.net` 域中的任何主机都将在选择器中显示 `marvin` 和 `brain` 服务器。
- 第二行指定主机 `norbert` 将在选择器中显示服务器 `brain`。
- 条目前的 `!` 表示拒绝该主机接收选择器。
- 最后一行指定任何主机都将在选择器中显示服务器 `dag`。

如果您希望动态生成选择器列表，可以使用以下指令：

```
*                    CHOOSER     BROADCAST
```

这将导致 X 服务器为任何请求的主机生成显示在选择器上的列表。您可以将此指令与本节中讨论的其他指令结合使用。

XDM 的默认安装会忽略选择器请求。要启用选择器请求，您必须从 `xdm-config` 文件中删除或注释掉以下行。

```
! SECURITY: do not listen for XDMCP or Chooser requests
! Comment out this line if you want to manage X terminals with xdm
DisplayManager.requestPort:	0
```

## 要点总结

X 窗口系统为 Linux 提供了高度可定制的图形界面。虽然有时系统安装和配置起来很复杂，但新的配置工具在很大程度上帮助了这一问题。请记住，LPI 考试涵盖的是在各发行版中通用的 X 基础内容。许多发行版有自己启动 X 并进行详细更改的方式。

- X 服务器在系统上运行，并显示桌面和应用程序。
- X 客户端是连接到 X 服务器并显示的应用程序。
- 窗口管理器处理窗口边框、图标、虚拟桌面、工具栏等。
- 桌面环境将窗口管理器与其他系统工具、编程工具包、应用程序和配置编辑器结合起来，创建一个完整的环境。
- X 可以从发行版创建的包文件或 XFree 组织分发的二进制文件中安装。
- X v3 为不同的视频芯片组使用单独的 X 服务器。
- X 服务器可执行文件链接到 `/etc/X11/X` 文件。
- X v3 服务器的主配置文件是 `XF86Config`。
- `XF86Config` 文件分为多个部分，包括 `Files`、`ServerFlags`、`Keyboard`、`Pointer`、`Monitor`、`Device` 和 `Screen`。
- 字体路径列在 `Files` 部分中，指向包含字体文件的目录或字体服务器。
- `XF86Setup` 是 `XF86Config` 文件的图形配置工具。
- `xf86config` 是 `XF86Config` 的基于文本的配置工具，但使用起来可能非常令人困惑。
- `SuperProbe` 可用于检测一些视频硬件。
- `xvidtune` 是一个允许您定制视频显示并创建可用于 `XF86Config` 文件中的模式线的工具。
- 每当安装新字体时，都应运行 `mkfontdir` 命令。
- `startx` 命令是一个用于从命令行启动 X 的脚本。
- 在 `startx` 执行 `xinit` 之后，它会查找用户的 `.xinitrc` 文件，如果未找到，则执行系统的 `xinitrc`。
- XDM 应用程序用于在启动时为用户提供图形登录屏幕。
- XDM 通过 `xdm-config` 文件进行配置。
- 可以通过使用其 Xresources 文件来定制 XDM 显示。
- 编写为使用 X 工具包库的 X 应用程序接受标准的命令行参数来配置其启动选项。
- 有许多不同的终端模拟器可用于 X，每个都有自己的优缺点。
- 通过将它们的 Xresource 条目放入用户的 `.Xdefaults` 文件中，可以定制 X 应用程序的显示。
- 一些复杂的 X 应用程序行为异常，不响应退出指令，或意外崩溃。
- X 可以使用基于主机的安全性，由 `xhost` 工具控制。
- X 客户端的显示可以通过使用 `DISPLAY` 环境变量或 `-display` 命令行选项发送到另一个主机。
- 可以使用 XDM 远程登录到系统并从远程服务器运行客户端，同时显示在本地系统上。
- 可以配置 XDM 向客户端呈现菜单，提示他们要登录的系统。

