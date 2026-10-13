
# CUPS 指令

某些指令允许你在特定位置设置访问控制。这些位置可以是打印机或资源，例如管理工具或打印池目录。位置控制通过 `Location` 指令实现。`Allow From` 和 `Deny From` 指令可以允许或拒绝来自特定主机的访问。CUPS 同时支持基础（Basic）和摘要（Digest）身份验证，这些在 `AuthType` 指令中指定。基础认证使用用户名和密码。例如，在使用 Web 界面时，系统会提示你输入 root 用户和 root 用户密码。摘要认证利用存储在 CUPS `/etc/cups/passwd.md5` 文件中的用户名和密码信息，使用用户名和密码的 MD5 版本进行验证。`AuthClass` 指令指定允许访问的类。`System`

| 文件名 | 描述 |
|---|---|
| `classes.conf` | 不同打印机类的配置 |
| `client.conf` | 为指定客户端列出特定选项 |
| `cupsd.conf` | 配置 CUPS 服务器 `cupsd` |
| `printers.conf` | 可用本地打印机的打印机配置 |

表26-2 CUPS 配置文件

## 第 26 章：打印服务器：CUPS

`class` 包含 `root`、`sys` 和 `system` 用户。以下示例显示了 `/admin` 资源（管理工具）的 `Location` 指令：

```
<Location /admin>

AuthType Basic

AuthClass System

## 限制本地域的访问

Order Deny

Deny From All

Allow From 127.0.0.1

</Location>
```

## CUPS 命令行打印客户端

一旦打印作业被放入打印队列，你可以使用多个打印客户端来管理打印机或打印机上的打印作业，例如 `Klpq`、`GNOME` 打印管理器和 CUPS 打印机配置工具。你还可以使用多个命令行打印 CUPS 客户端。这些包括 `lpr`、`lpc`、`lpq` 和 `lrpm` 命令（见第 10 章）。打印系统切换允许你在它们之间切换。通过这些客户端，你可以打印文档、列出打印队列、重新排序并删除打印作业（有效取消作业）。对于网络连接，CUPS 为其命令提供了加密选项 `-E`，用于加密通过网络发送的打印作业和打印信息。表 26-3 显示了各种打印机命令。

> 注意：命令行客户端的名称和语法与 Unix 和旧版 Linux 系统使用的 LPR 和 LPRng 命令行相同。

| 打印机管理 | 描述 |
|---|---|
| GNOME 打印管理器 | GNOME 打印队列管理工具 (CUPS)。 |
| CUPS 配置工具 | 打印、管理和配置 CUPS。 |
| `lpr` 选项列表 | 打印文件，将文件复制到打印机的打印池目录，并将其放入打印队列中提交。`-P printer` 在指定的打印机上打印文件。 |
| `lpq` 选项 | 显示打印队列中的作业。`-P printer` 显示指定打印机的队列。`-1` 打印详细列表。 |
| `lprstat` 选项 | 显示打印状态。 |
| `lrpm` 选项 `printjob-id` or `printer` | 从打印队列中移除打印作业。你通过 `lpq` 列出的编号识别特定的打印作业。`-P printer` 移除指定打印机的所有打印作业。 |
| `lpc` | 管理你的打印机。在 `<lpc>` 提示符下，你可以输入命令检查打印机状态并采取其他操作。 |

表 26-3 CUPS 打印客户端

# 第 V 部分：网络服务器

## `lpr`

`lpr` 客户端提交作业，然后 `lpd` 按顺序接收并将其放入适当的打印队列；`lpr` 以文件名作为参数。如果没有指定打印机，则使用默认打印机。`-P` 选项允许你指定特定的打印机。在下一个示例中，用户首先打印文件 `prefix`，然后将文件 `report` 打印到名为 `mypson` 的打印机：

```
$ lpr prefix

$ lpr -P mysylon report
```

## `lpc`

你可以使用 `lpc` 启用或禁用打印机、重新排序队列并配置设置。`lpc` 命令显示打印机状态。以下示例设置了打印机：

```
# lpc
```

## 第 V 部分：网络服务器

使用 `all`（全部）或 `none`（无）来允许或拒绝所有或无访问。你可以通过结合 `all` 或 `none` 与特定用户的访问权限来创建异常。以下示例允许所有人访问用户，`justin` 除外：

```
lpadmin -p myayson -u allow:all deny:justin
```

### `lpoptions`

`lpoptions` 命令允许你设置选项和默认值，这些设置主要控制打印作业的打印方式。例如，你可以为特定的打印机设置颜色或页面格式。所有用户的默认设置由 `root` 用户在 `/etc/cups/lpoptions` 文件中管理，每个用户也可以创建自己的配置并保存在自己的 `.lpoptions` 文件中。`-p` 选项指定打印机（你也可以使用 `-d` 选项设置默认打印机）。

打印机选项使用 `o` 选项配合选项名和值设置，即 `-o option=value`。使用 `-r` 选项移除打印机。例如，要在纸张上双面打印，你可以将 `sides` 选项设置为 `two-sided:`：

```
lpoptions -p myayson -o sides=two-sided
```

要移除该选项，使用 `-r`。

```
lpoptions -p myayson -r sides
```

要显示可用选项列表，请查看 `www.cups.org` 上 CUPS 软件手册中的标准打印选项。

### enable and disable

`enable` 命令启动打印机，`disable` 命令停止打印机。使用 `-c` 选项，你可以取消打印机队列中的所有作业；使用 `-r` 选项广播一条解释关机的消息。

```
disable myayson
```

### accept and reject

`accept` 和 `reject` 命令允许你控制对特定打印机打印队列的访问。`reject` 命令阻止打印机接受作业，而 `accept` 则允许新的打印作业。

```
reject myayson
```

### Lpinfo

`lpinfo` 命令是一个实用的工具，可以让你知道系统上有哪些 CUPS 设备和驱动程序。使用 `-v` 选项查看设备，使用 `-m` 选项查看驱动程序。

```
lpinfo -m
```
