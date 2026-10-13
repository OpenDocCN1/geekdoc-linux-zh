
```
lpadmin -p luna -c roughs
```

# 检查打印机状态

`lpstat` 命令用于验证打印机状态。可以使用此命令确定哪些打印机可用，或检查特定打印机的特性。`lpstat` 语法如下：

```
lpstat [-d] [-p <printer-name>] [-D] [-l] [-t] [-u <login-IDs>]
```

`lpstat` 命令选项见表 10.6。

| 选项 | 描述 |
| - | - |
| -a | 报告打印机是否接收请求。您也可以指定特定的打印机列表，如示例 `lpstat -a eps1 eps2 eps3`。 |
| -d | 显示默认打印机。 |
| -p <printer-name> | 显示打印机是激活还是禁用，以及是否接收请求。可以使用此命令指定多个打印机。使用空格或逗号分隔打印机。如果您使用空格，请将打印机列表括在引号中。如果不指定打印机名称，则显示所有打印机的状态。 |
| -D | 显示指定打印机的描述。 |
| -l | 显示指定打印机的特性。 |
| -t | 显示 LP 打印服务的状态信息，包括所有打印机的状态——它们是否激活以及正在什么请求。 |
| -u <login-IDs> | 打印用户输出请求的状态，其中 `<login-IDs>` 可以是以下所有之一： |
| <user> | 本地系统上的用户，如示例 `lpstat -u bcalls` |
| <host:user> | 系统上的用户，如示例 `lpstat -u systembcalls`。 |
| <host:all> | 特定系统上的所有用户，如示例 `lpstat -u systemall`。 |
| <all:user> | 所有系统上的特定用户，如示例 `lpstat -u all:bcalls`。 |
| all | 所有系统上的所有用户，指定如下：`lpstat -u all` |

以下是 `lpstat` 命令的几个示例：

```
lpstat -p hplaser
```

系统的返回如下：

```
printer hplaser is idle. enabled since Jun 16 10:09 1998.
available.
```

在下一个示例中，该命令请求打印机 hplaser1 和 hplaser2 的描述：

```
lpstat -p "hplaser1" hplaser2" -D
printer hplaser2 faulted. enabled since Jun 16 10:09 1998.
available.
unable to print: paper misfeed jam
```

Description: Printer By finance.

printer hplaser2 is idle. enabled since Jun 16 10:09 1998.

available.

Description: Printer in computer room.

在下一个示例中，该命令请求打印机 lpstat 的特性：

```
lpstat -p hplaser -l
printer hplaser is idle. enabled since Jun 16 10:11 1998.
available.
Content types: any
Printer types: unknown
Description: Printer by computer room.
Users allowed:
(all)
Forms allowed:
(none)
Banner not required
Character sets:
(none)
Default is pitch:
Default page size:
```

## 管理打印机队列

打印机管理的例行任务之一是管理它们的队列。有时，会提交不需要的大作业，这些作业是可以取消的。在其他情况下，你可能希望将高优先级作业排在其他等待打印的作业之前。以下列出了你可能想要在打印机队列上执行的一些例行任务。

### 删除打印作业

要从打印队列中删除他人的打印作业，你首先需要成为 root 权限。然后，使用如下所示的 `lpstat` 命令来确定要取消的打印请求的请求 ID：

```
lpstat -u bcalkins
eps1-1 bcalkins 1261 Mar 16 17:34
```

在此示例中，用户 bcalkins 现在是队列中的一个请求。请求 ID 为 eps1-1。

### 取消打印请求

使用 `cancel` 命令取消打印请求。命令语法如下：

```
cancel <request-id> | <printer-name>
```

`cancel` 命令的参数描述在表 10.7 中。

| 表 10.7 cancel 参数 |
| 参数 | 描述 |
| <request-id> | 要取消的打印请求的请求 ID。你可以指定多个请求 ID。使用空格或逗号来分隔请求 ID。如果你使用空格，请将请求 ID 列表包含在引号中。 |
| <printer-name> | 指定你想要取消当前正在打印请求的打印机。你可以通过此命令指定多个打印机名称。使用空格或逗号来分隔打印机名称。 |

在接下来的示例中，该命令取消了 eps1-3 和 eps1-4 打印请求：

```
cancel eps1-3 eps1-4
request "eps1-3" cancelled
request "eps1-4" cancelled
```

在下一个一个示例中，该命令取消了当前正在打印机 eps1 上打印的打印请求：

```
cancel eps1
request "eps1-9" cancelled
```

### 发送高优先级的打印作业

带有 `-q` 选项的 `lp` 命令用于为打印队列中的打印请求分配优先级。将优先级级别指定为 0–39 之间的整数。使用 0 表示最高优先级，39 表示最低优先级。如果未指定优先级，LP 管理员将为打印服务分配默认优先级。

以下示例说明了如何以最高优先级向打印机 eps1 发送打印作业：

```
lp -deps1 -q0 file
```

### 限制用户对打印机的访问

使用 `ladmin` 命令允许或拒绝用户访问打印机。命令语法如下：

```
ladmin -p <printer-name> -u allow:<user-list> \
[ deny:<user-list> ]
```

`ladmin` 命令的参数描述在表 10.8 中。

表 10.8

| 参数 | 描述 |
| -p <printer-name> | 应用于允许或拒绝用户访问的打印机名称。 |
| -u allow:<user-list> | 添加到允许用户访问列表的用户名。你可以通过此命令指定多个用户名。使用空格或逗号来分隔名称。如果你使用空格，请将名称列表包含在引号中。 |
| -u deny:<user-list> | 添加到拒绝用户访问列表的用户名。你可以通过此命令指定多个用户名。使用空格或逗号来分隔名称。表 10.9 提供了 user-list 的有效值。 |

Form mounted:

Content types: postscript

```
Printer types: PS
Description: epson
Connection: direct
Interface: /usr/lib/lp/model/standard
On fault: write to root once
After fault: continue
Users allowed:
bcalkins
bholzgen
Forms allowed:
(none)
Banner not required
Character sets:

Default pitch:
Default page size: 80 wide 66 long
Default port settings:
```

### 接受或拒绝打印机的打印请求

作为 root，你可以使用 `reject` 命令停止接受打印请求。命令语法如下：

```
reject [-r "reason"] <printer-name>
```

`reject` 命令的参数描述见表 10.9。

| 表 10.9 |
| 参数 | 描述 |
| --- | --- |
| -r "reason" | 告诉打印机拒绝请求。当用户使用 `lpstat` 查看状态时，该原因将被显示。 |
| <printer-name> | 停止接受请求的打印机名称。 |

在以下示例中，该命令停止 eps1 接受请求：

```
reject -r "eps1 is down" eps1
```

只要打印机启用，以下示例命令将让 eps1 重新接受：

```
accept eps1
```

### 取消特定用户的打印请求

使用 `cancel` 命令取消特定用户的打印请求。

```
cancel -u <user-list> <printer-name>
```

`cancel` 命令的参数描述在表 10.10 中。

| 表 10.10 |
