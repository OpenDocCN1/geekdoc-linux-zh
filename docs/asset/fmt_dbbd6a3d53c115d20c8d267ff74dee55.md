
有许多工具可用于 NIS。有些用于诊断，但另一些是普通用户程序（例如用于更改 NIS 密码的 `yppasswd`）。

这些工具位于 `yp-tools` 软件包中。以下是一些最常用的工具：

- `bin/ypdomainname`。如果你在不带参数的情况下输入 `ypdomainname`，该命令将显示当前 NIS 域的名称。
- 要设置新域，使用命令 `ypdomainname`。例如，要将当前域名设置为 `planets`，请输入 `ypdomainname planets`。
- `usr/ypwitch`。你可以使用此工具显示客户端所使用的 NIS 服务器。

你也可以查询其他机器上的 NIS 客户端以其指向的服务器（如下所示）：

```
DA50: ~ # ypwitch
sun.example.com
DA50: ~ # ypwitch sun.example.com
localhost
```

在此示例中，输入 `ypwitch` 显示本地计算机正在使用的 NIS 服务器（`sun.example.com`）。

- 17. 关闭“用户和组管理”对话框和“YaST 控制中心”。

## NIS 安全考虑

实现 NIS 时的一个重要问题是访问保护。你如何限制只有受信任的计算机才能访问 NIS 域及其存储在其中的信息？你可以在 `/var/yp/securenets` 文件中配置此类限制。所有需要访问 NIS 服务器的网络都必须在该在该。

例如，以下 `securenets` 文件允许 NIS 服务器从网络 `192.168.0.0/24`、计算机 `192.168.1.1` 及其自身进行访问（并拒绝所有其他计算机的访问）：

```
255.0.0.0 127.0.0.0
255.255.255.0 192.168.0.0
255.255.255.0 192.168.1.1
```

也可以使用关键字 `*host 192.168.1.1*` 为单个计算机创建条目。虽然 YaST 不接受此选项，但在手动编辑文件时可以使用该选项。

> 注意：关于 `/var/yp/securenets` 文件结构的更多信息，请输入 `man 8 ypserv`。在 `/var/yp/securenets` 中只有 IP 地址是有效的；你不能使用主机或网络名称。

## 在网络上管理 523

如果你使用的 `ypserv` 版本包含 TCP wrapper 支持，可以相应修改 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。

详细信息，输入 `man 5 hosts_access` 或 `man 5 hosts_options`。

## NIS 工具

有许多工具可用于 NIS。有些用于诊断，但另一些是普通用户程序（例如用于更改 NIS 密码的 `yppasswd`）。

这些工具位于 `yp-tools` 软件包中。以下是一些最常用的工具：

- `bin/ypdomainname`。如果你在不带参数的情况下输入 `ypdomainname`，该命令将显示当前 NIS 域的名称。
- 要设置新域，使用命令 `ypdomainname`。例如，要将当前域设置为 `planets`，请输入 `ypdomainname planets`。
- `usr/ypwitch`。你可以使用此工具显示客户端所使用的 NIS 服务器。你也可以查询其他机器上的 NIS 客户端以其指向的服务器（如下所示）：

```
DA50: ~ # ypwitch
sun.example.com
DA50: ~ # ypwitch sun.example.com
localhost
```

在此示例中，输入 `ypwitch` 显示本地计算机正在使用的 NIS 服务器（`sun.example.com`）。

## 第 8 部分基础设施

- `usr/ypwitch`。你可以使用此工具显示客户端所使用的 NIS 服务器。你也可以查询其他机器上的 NIS 客户端以其指向的服务器（如下所示）：

```
DA50: ~ # ypwitch
sun.example.com
DA50: ~ # ypwitch sun.example.com
localhost
```

在此示例中，输入 `ypwitch` 显示本地计算机正在使用的 NIS 服务器（`sun.example.com`）。

## 第 8 部分基础设施

- `usr/ypwitch`。你可以使用此工具显示客户端所使用的 NIS 服务器。你也可以查询其他机器上的 NIS 客户端以其指向的服务器（如下所示）：

```
DA50: ~ # ypwitch
sun.example.com
DA50: ~ # ypwitch sun.example.com
localhost
```

在此示例中，输入 `ypwitch` 显示本地计算机正在使用的 NIS 服务器（`sun.example.com`）。

## 第 8 部分基础设施

- `usr/ypwitch`。你可以使用此工具显示客户端所使用的 NIS 服务器。你也可以查询其他机器上的 NIS 客户端以其指向的服务器（如下所示）：

```
DA50: ~ # ypwitch
sun.example.com
DA50: ~ # ypwitch sun.example.com
localhost
```

在此示例中，输入 `ypwitch` 显示本地计算机正在使用的 NIS 服务器（`sun.example.com`）。

## 第 8 部分基础设施

- `usr/ypwitch`。你可以使用此工具显示客户端所使用的 NIS 服务器。

## 第 8 部分基础设施

- `usr/ypwitch`。你可以使用此工具显示客户端所使用的 NIS 服务器。

## 第 8 部分基础设施

- `usr/ypwitch`。你可以使用此工具到第 8 部分基础设施。
- 5. 输入完整的用户名、用户登录 ID 和密码（输入两次）。
- 6. 选择“详细”。

## 第 8 部分基础设施

- `usr/ypwitch`。你可以使用此工具显示客户端所使用的 NIS 服务器。

## 第 8 部分基础设施

- `/usr/sbin/yppoll`。你可以使用此工具显示映射的 ID 号。

此 ID 号由系统分配的。每当映射更新时，它就会更改。当你确保确保服务器正在使用最新版本的映射时，使用该命令。

`yppoll` 的语法为：

```
yppoll [-h host] [-d domain] mapname
```

将 `mapname` 替换为映射的全名。命令无法处理别名。表 8–4 描述了这些选项。

## 表 8-4

| 选项 | 说明 |
|---|---|
| `-h host` | 此选项允许你指定默认服务器以外的服务器。要查找命令默认使用哪个服务器，请使用命令 |
| `-d domain` | 如果未指定主机，则查询的服务器为默认服务器。此选项允许你指定默认域以外的域。要查找命令默认使用哪个域，请使用命令 `ypdomainname`。如果未指定域，则查询的域为默认域。 |

## 练习 8-4 在你的网络上启用网络信息服务 (NIS)

在此练习中，你将执行以下操作：

- 第一部分：使用 YaST 配置 NIS 服务器
- 第二部分：创建 NIS 用户
- 第三部分：更新 NIS 映射
- 第四部分：验证本地 NIS 配置
- 第五部分：为 NIS 网络服务准备
- 第六部分：使用 YaST 配置 NIS 客户端

在此练习中，你将与同学一起工作，由你们中的一个人作为 NIS 服务器，另一个人作为 NIS 客户端。

> 重要：为了使练习正常运行，必须按顺序执行步骤。

例如，在第五部分中，在完成 NFS 客户端计算机的步骤之前，先在 NFS 服务器计算机上完成步骤。

## 第一部分：使用 YaST 配置 NIS 服务器

在 NIS 服务器计算机上，执行以下操作：

+ 1. 从 KDE 桌面，选择 YaST 图标；然后输入新密码并点击确定。

YaST 控制中心出现。

## 526 第 8 节启用基础设施服务

+ 2. 选择网络服务 > NIS 服务器。

出现网络信息服务 (NIS) 服务器设置对话框。

+ 3. 选择创建 NIS 主服务器；然后通过选择“下一步”继续。

出现主服务器设置对话框。

+ 4. 在 NIS 域名字段中输入 `NIS-DAXX`（其中 `xx` 为您服务器的主机号）。

例如，如果您的主机名为 `DA50`，则应输入 `NIS-DA50`：

+ 5. 选择以下选项：
  - 此主机也是 NIS 客户端
  - 快速映射分布 (`rpc.pyxfrd`)
  - 允许更改密码
  - 允许更改 GECOS 字段
  - 允许更改登录 shell

+ 6. 选择“下一步”继续。

出现 NIS 服务器映射（NIS Server Maps）对话框。

+ 7. 从服务器映射列表中，取消勾选 `netid`；然后确保选择了 `group`（组）、`password`（密码）、`rpc` 和 `services`（服务）。

+ 8. 选择“下一步”继续。

出现 NIS 服务器查询主机设置对话框。

+ 9. 接受默认设置并通过选择“完成”完成 NIS 服务器设置。

## 第二部分：创建 NIS 用户

在测试 NIS 配置之前，您需要在配置了 NIS 服务器的计算机上创建一个 NIS 用户。

在 NIS 服务器计算机上，执行以下操作：
