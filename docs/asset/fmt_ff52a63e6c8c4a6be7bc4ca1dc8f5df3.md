
`rmformat` 会进行必要的检查，以检测任何重叠分区或超出考虑介质容量的地址请求。每个分片 `n` 只允许一个分片信息项。如果你为同一个分片 `n` 提供了多个分片信息项，将显示相应的错误信息。分片 `2` 是覆盖整个磁盘容量的备份分片。你可以使用井号（`#`）来描述输入文件中的注释行。如果行以 `#` 开头，则 `rmformat` 会忽略 `#` 之后直到行尾的所有字符。

你可以尝试对某些容量非常小的介质进行分区，但在某些设备上使用此选项时要小心。

### 选项

- `-U amount`
在任何文件系统上指定数量，然后进行格式化。参阅 `mount(1M)`。此选项将卸载所有已挂载的分片并在请求的设备上执行长格式化。

- `-V read write`
在格式化后验证介质的每个块。写验证是一种破坏性机制。在开始验证之前，系统会询问你确认。此选项的输出是被识别为坏块的数字列表。

读取验证只验证块并报告易出错的块。

你可以配合 `-c` 选项使用块号列表进行修复。

- `-w enable disable`
启用或禁用介质上的写保护。在不具备软件写保护功能的设备上，将显示指示该功能不可用的消息。

- `-W enable disable`
启用或禁用带密码的写保护。此选项始终在交互模式下工作，因为需要密码来维护安全性。

对于支持此功能的 Iomega 产品，允许最大长度为 32 字节的密码。在不具备此类写保护功能的设备上，将显示一条该功能不可用的消息。

### 参数

对于支持此功能的 Iomega 产品，允许最大长度为 32 字节的密码。此选项仅适用于 Iomega 产品。Iomega 产品不允许在没有密码的情况下进行读/写保护。在未配备此类软件读/写保护功能的设备上，将提供指示该功能不可用的警告信息。

### 文件

```
/usr/share/lib/tmac/tmac.bib
```

`nroff/troff` 使用的宏文件。

### 属性

有关以下属性的描述请参见 `attributes(5)`：

| 属性类型 | 属性值 |
|---|---|
|可用性 | SUNdoc |

### 参见

`addbib(1)`, `indxbib(1)`, `lookbib(1)`, `nroff(1)`, `refer(1)`, `sortbib(1)` `troff(1)`, `attributes(5)`

### Bug

用户必须重写宏以创建自定义格式。

# 新角色 — 授予用户的打印角色

### 概要

```
bin/roles [user...]
```

### 描述

`roles` 命令是 Solaris 8 操作系统环境中新增的，用于在标准输出上打印你或可选指定的用户被授予的基于角色的访问控制 (`RBAC`) 角色。角色是特殊的账户，对应于功能职责而非实际的人员（称为普通用户）。

每个用户可以拥有零或多个角色。角色拥有普通用户的大部分属性，并像 `passwd(4)` 和 `shadow(4)` 中的普通用户一样被识别。每个角色必须在 `user_attr(4)` 文件中有一个条目将其标识为角色。角色可以有自己的权限和配置文件。参见 `auths(1)` 和 `profile(1)`。

角色不能作为主用户登录系统。用户必须先以自己的身份登录，然后切换角色。角色的操作可以归属于普通用户。当启用审计时，角色的审计事件包含假设该角色的原始用户 ID。

角色会计算自身和任何分配的角色。角色没有层次级关系。然而，从 Solaris 9 发布版本的配置文件（参见 `prof_attr(4)`）开始是层次级的，你可以使用它们来实现与层次级角色相同的效果。

角色必须具有有效密码以及一种解释配置文件的 shell —— 要是 `pfscsh`、`pksh` 或 `pfsh`。参见 `pfexec(1)`。

用户可以使用 `su(1M)`、`login(1)` 或某些支持 `PAM_USER` 变量的服务来切换角色。要成功接管角色，用户必须是该角色的成员并知道角色密码。角色分配在 `user_attr(4)` 中指定。

### 示例

以下示例显示了 `roles` 命令对三个用户的输出。

```
mopoke% roles winsor ray des

winsor : printadm

ray : printadm

roles: des : No roles

mopoke%
```

输出显示用户 `winsor` 和 `ray` 都是 `printadm` 角色的成员。用户 `des` 未被分配任何角色。

### 退出状态

- `0` 成功完成。
- `1` 发生了错误。

### 文件

- `/etc/security/exec_attr`
执行配置文件数据库。
- `/etc/security/prof_attr`
配置文件描述数据库。
- `/etc/user_attr`
扩展用户属性数据库。

### 属性

有关以下属性的描述请参见 `attributes(5)`。

| 属性类型 | 属性值 |
| --- | --- |
|可用性 | SUNwcs |

### 参见

`auths(1)`, `pfexec(1)`, `profiles(1)`, `login(1)`, `su(1M)`, `getauusername(3BSM)`, `auth_attr(4)`, `passwd(4)`, `shadow(4)`, `user_attr(4)`, `attributes(5)`

# `rpcgen` — RPC 协议编译器

### 概要

```
/usr/bin/rpcgen [-a] [-A] [-b] [-C] -Dname = value] [-i size] -I [-K seconds] [-L] [-M] [-N] [-T] [-v] [-Y Pathname] infile

/usr/bin/rpcgen [-c -h -l -m -t -Sc -Ss -Sm -o outfile] infile - *
```

```
/usr/bin/rpcgen [-s netype] [-o outfile] [infile]

/usr/bin/rpcgen [-n netid] [-o outfile] [infile]
```
