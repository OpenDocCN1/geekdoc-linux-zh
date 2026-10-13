
添加 `paperbark.wellard.com` 的凭据...
Enter root login: password:

输入 root 密码
正在创建 NIS+ 管理组：`admin.wellard.com`。
正在将主体 `paperbark.wellard.com` 添加到 `admin.wellard.com`。

正在重启安全级别 2 的根主服务器
正在启动 NIS+ 密码...
正在启动 NIS+ 缓存管理器

该系统已配置为 `wellard.com` 域的根服务器。
你可以使用 `nisopulate` 脚本或 `/usr/lib/nis/nisisadd` 命令填充标准的 NIS+ 表格。

## 填充 NIS+ 表格

在运行 `nisserver` 脚本配置根主服务器后，你可以使用 `nisopulate` 脚本来填充标准的 NIS+ 表格。
本节描述了如何使用带有默认设置的 `nisserver` 脚本（列如下）来填充 NIS+ 表格。

## 设置 NIS+ 根服务器

- 由 `nisserver` 脚本创建的域。
- 以 `/etc` 或 NIS 映射作为名称服务信息的源。
- 标准 NIS+ 表格：`auto_master`, `auto_home`, `ethers`, `group`, `hosts`, `ipnodes`, `networks`, `passwd`, `protocols`, `services`, `rpc`, `netmasks`, `bootparams`, `netgroup`, 和 `aliases`。

注意：当 `/etc` 文件作为名称服务的源时，`/etc/shadow` 文件的内容将与 `/etc/passwd` 文件合并以创建 `passwd` 表。不会创建 shadow 表。

## 准备运行 nisnopulate 命令

在运行 `nisnopulate` 命令之前，你需要执行以下任务。

- 检查每个本地的 `/etc` 文件或 NIS 映射，以确保没有错误或不完整的条目。
- 确保域名和主机名不同。
- 移除所有 `/etc` 文件的副本以及（如果你没有使用 DNS 的话）`/etc/inet/hosts` 和 `/etc/inet/ipnodes` 文件，并使用这些副本填充表格。以下示例使用了来自 `/tmp/nisplusfiles` 目录的文件。

注意：已添加了新的 `ipnodes.org_dir` 表以处理 IPv6 地址。它包含了一个主机的 IPv4 和 IPv6 地址。现有的 `hosts.org_dir` 表格保留以方便现有应用程序。你必须保持 `hosts.org_dir` 和 `ipnodes.org_dir` 表格与 IPv4 地址一致。表格不会自动同步。管理 `ipnodes.org_dir` 表与管理 `hosts.org_dir` 表类似。

- 编辑 `passwd`、`shadow`、`aliases`、`hosts` 和 `ipnodes` 文件。移除 root、daemon、bin、sys、adm、l1p、smtp、uocp、nuuc、list、nobody 和 noaccess 条目，以确保这些条目不会跨命名空间可用。
- 必须配置域且主服务器必须正在运行。
- 域服务器必须有足够的磁盘空间来容纳新的表格信息。
- 你必须以 root 身份登录，因为 NIS+ 凭表尚未填充以建立 NIS+ 主体凭据。

## 设置 NIS+ 服务器与客户端

如果从 `/etc` 文件填充，你需要以下信息：

- NIS+ 域名。
- 用于传输数据的已编辑文本文件路径。
- root 密码。

如果从 NIS 映射填充，你需要以下信息：

- NIS+ 域名。
- NIS 域名。
- NIS 服务器的名称。
- NIS 服务器的 IP 地址。

# 设置 NIS+ 客户端系统

你可以忽略任何解析错误警告。此类错误表示脚本在 NIS 映射（map）中发现了空值或意外值。你可能需要在脚本执行完成后对数据进行验证。

- 将你自己和其他用户添加到根域（root domain）的管理员组。

# 设置 NIS+ 客户端系统

在你从文件或 NIS 映射填充了根主服务器的表格后，你就可以初始化 NIS+ 客户端系统。你不需要执行任何进一步步骤来初始化根主服务器，因为它本身已经是其所在域的 NIS+ 客户端。

下一节描述了如何使用 `niscient` 脚本设置 NIS+ 客户端。

## 准备运行 niscient 命令

在运行 `niscient` 命令之前，必须满足以下条件。

- 域必须已经配置好，且其主服务器必须正在运行。
- 主服务器的 NIS+ 表格必须填充。至少 `hosts` 或 `ipnodes` 表必须包含客户端系统的条目。如果你正在使用 DNS，则 NIS+ `hosts` 和 `ipnodes` 表应该是空的，且 `/etc/nsswitch.conf` 中的 `hosts` 条目应为 `hosts: files dns`。
- 你必须以超级用户（superuser）身份登录到要命名为 NIS+ 的系统。在以下示例中，新客户端系统命名为 `paperbark`。
- 域名。
- 默认 Secure RPC 密码（`nisplus`）。
- 客户端系统的根密码。
- 客户端主域（home domain）中 NIS+ 服务器的 IP 地址。
- 如果你使用 `AUTHENTICATION`，请使用与主服务器相同的 Diffie-Hellman 密钥长度。使用 `nisauthconf` 来确定主服务器的 Diffie-Hellman 密钥长度。

在运行 `niscient` 命令之前，你需要以下信息。

## 安全注意事项

管理员和客户端都必须拥有正确的凭据和访问权限。管理员可以拥有以下任意：

- 客户端主域中的 DES 凭据。
- 管理员主域中的 DES 凭据组合。
- 客户端域中的 LOCAL 凭据。

请参阅第 5 节“介绍 NIS+ 环境”，获取更多关于 DES 和 LOCAL 凭据的信息。

在 NIS+ 域中创建了客户端凭据后，你可以在客户端系统上完成设置过程。NIS+ 服务器上其主域的目录对象必须对“World”（世界）和“Nobody”类别具有读取（Read）访问权限。如果你将客户端添加到已存在客户端的 NIS+ 域中，该目录对象可能已经拥有正确的访问权限。

你可以使用 `niscat -o` 命令检查目录对象的访问权限。访问权限显示在输出的第五行。例如，`World` 具有读取权限，如访问权限末尾的 `r--` 所示：

```
rootmaster# niscat -o ESG.Eng.wellard.com.

Object Name     : ESG

Owner          : oak.ESG.Eng.sun.COM.

Group          : admin.ESG.Eng.sun.COM.

Domain         : Eng.sun.COM.

Access Rights : r--rncdcmdr-

Time to Live    : 12:0:0

Object Type    : DIRECTORY

Name           : ESG.Eng.sun.COM.

Type           : NIS

Master Server  :

Name            : oak.ESG.Eng.sun.COM.

Public Key     : None.

Universal addresses: (6)

[1] - udp inet, 127.0.0.1.011

[2] - tcp inet, 127.0.0.1.011

[3] - inet, 127.0.0.1.011

[4] - loopback, oak.rpc

[5] - loopback, oak.rpc

[6] - loopback, oak.rpc

Time to live    : 12:0:0

Default Access rights :
```

如果你拥有 `Modify`（修改）权限，你可以更改访问权限。
