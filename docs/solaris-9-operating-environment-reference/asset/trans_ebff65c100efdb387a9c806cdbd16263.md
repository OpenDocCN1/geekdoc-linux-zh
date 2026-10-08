

# alias, unalias

# 示例

## C Shell

以下示例为 `alias` 命令创建了一个别名，并使用别名快捷方式为 `history` 命令创建一个别名，并为 `more` 命令创建一个更多的别名。

```
castle% alias a alias
castle% a h history
castle% a moer more
```

以下示例列出了在 .cshrc 文件中设置的别名。

```
castle% alias
G3 172.16.8.21
a alias
c clear
history
mac 172.16.8.20
caste%
```

## Korn Shell

以下别名将 `ls` 修改为以列格式格式提供更具注释的输出。
`alias ls="ls -CF"`

以下别名创建了一个简单的重做，用于重复命令历史文件中的之前的条目。
`alias r='fc -s'`

以下别名为 `du` 使用 1-千字节为单位。
`alias du="du -k"`

或者，你可以以以下形式创建别名，使用反斜杠转义空格字符，并省略命令周围的双双引号。
`alias du\=du -k`

以下别名设置了 `nohup`，使其能够处理本身是别名名的参数。
`alias nohup="nohup `

以下示例列出了为 Korn Shell 设置的默认别名。

```
$ alias
autoload='typeset -fu'
command='command '
functions='typeset -f'
history='fc -1'
integer='typeset -i'
local=typeset
nohup='nohup '
r='fc -e -'
```

# allocate

```
stop='kill -STOP'
suspend='kill -STOP $$'
$
```

# 环境变量

请查看 environ(5) 以了解以下影响 `alias` 和 `unalias` 执行的环境变量描述：LC_TYPE, LC_MESSAGES 和 NLPATH。

# 退出状态

- 成功完成。
- 指定的别名操作数之一没有别名定义，或者发生了错误。

# 属性

请查看 attributes(5) 以了解以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNWcsu |

# 参见

csh(1), ksh(1), shell_buildins(1), attributes(5), environ(5)

# allocate — 设备分配

# 概要

```
/usr/sbin/allocate [-s][-U name] device
/usr/sbin/allocate [-s][-U name] -g dev-type
/usr/sbin/allocate [-s][-U name] -F device
```

# 描述

使用 Solaris 9 操作系统环境中新增的 `allocate` 命令，通过其分配机制管理设备的所有权。`allocate` 命令确保每个设备一次仅由一个合格的用户使用。

> 注意 — 只有在启用基本安全模块 (BSM) 时，本手册页描述的功能才可用。更多信息请参见 bsm(1)。

Solaris 9 操作系统提供了一种设备分配方法——通过 allocate(1)、dminfo(1) 和 devices(1) 命令——满足 C2级及以上计算系统的可信计算机系统评估标准 (TCSEC) 对象需求。设备分配机制防止同时访问设备，防止一个用户的数据被另一个用户读取，并防止在一个用户完成设备操作后，另一个用户访问设备或驱动器内部存储中的任何信息。

例如，多个用户共享单个带驱动，该带驱动可能并不位于单个用户的位置。如果带驱动位于远程，用户在驱动器中加载磁带到调用命令访问带驱动之间可能会可能会过一段时间。由于其他用户可以在磁带无人看管时访问驱动器，另一个用户可能会访问或覆盖磁带上的数据。通过设备分配机制，你可以确保一次只有一个用户可以访问特定的带设备。

为了维护设备的完整性，`allocate` 操作将在与该设备相关的所有设备特殊文件上执行。

只有授权的用户才能分配设备。所需的授权在 device_allocate(4) 中指定。

# 选项

- -g dev-type

分配一个类型与 dev-type 匹配的未分配设备。使用 dev-type 参数指定设备类型。你可以从 `list_devices -1` 命令的输出中确定设备类型。请参见“示例”以获取示例。

- -s

抑制诊断输出。

- -F device

将设备重新分配给另一个用户。此选项通常与 -U 一起使用，将特定设备重新分配给特定用户。只有具有 solaris.devices.revoke 权限的用户才允许使用此选项。

使用 device 参数指定要操作的设备，例如用于流式带驱动的 st0。你可以使用 list_devices(1) 命令的 -1 选项显示可用设备列表，该命令也是 Solaris 9 操作系统环境中新增的。请参见第685页的“示例”获取 list_devices -1 输出的示例。默认分配操作分配与当前进程 UID 相关的设备特殊文件。

当你指定 -F 选项时，执行时会运行设备清理程序。位于 /etc/security/lib。该程序的名称可以在 dev-exec-fd 中对应设备的 device_allocate(4) 条目中找到。

- -U uname

执行时使用用户 ID uname 代替当前进程的用户 ID。

# 示例

以下示例分配了一个带驱动器。

```
mokoke% allocate st0
mokoke%
```

以下示例按类型分配音频文件。

```
mokoke% allocate -g audio
mokoke%
```

# 诊断

出错时返回非零退出状态。

# 文件

```
/etc/security/device_allocate
```

关于每个设备的访问控制信息。

```
/etc/security/device_maps
```

关于物理设备的访问控制信息。

```
/etc/security/dev/*
```

必须存在于可分配设备的。

```
/etc/security/lib/*
```

设备分配文件。

# 属性

查看以下属性。

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNwcs |

# 参见

deallocate(1), list_devices(1), bsmconv(1), dminfo(1), deallocate(4), device_maps(4), attributes(5)

# amt — 抽象机器测试

# 概要

```
/usr/bin/amt [-s]
```

# 描述

amt 命令用于 Solaris 9 操作系统环境中通用标准系统。使用该命令验证执行控制访问配置文件所需的底层函数工作正常。/usr/bin/amt 是一个执行测试的器脚本。对于 32 位系统，测试作为 32 位应用程序运行。对于 64 位系统，测试运行两次：一次作为 32 位应用程序，一次作为 64 位应用程序。

# amt

amt 会列出每个执行测试的结果（通过或失败），除非你使用 s 选项抑制输出。

# 选项

s 抑制输出。

# 示例

以下显示 amt 命令在 64 位系统上的输出。
mokoke& amt

```
AMT Test Program -- 64 bit application
============================
Test 1- 栈边界测试
TEST 1 PASSED
Test 2- 数据边界测试。
PASS: 数据区域读写成功。
TEST 2 PASSED
Test 3- 文本区域不可写
验证对文本空间的写入不会导致对源执行文件的写入，也不会影响共享该文本的另一个进程。
PASS: 捕捉到段错误，意味着无法写入文本区域。
TEST 3 PASSED
Test 4- 写入后内存不共享
两个进程共享的匿名内存（例如 fork 之后）在任何一个进程对其写入后不再共享。
TEST 4 PASSED
Test 5- 内存分配不共享
验证通过 fork 创建的两个进程中新分配的内存不会导致另一个进程产生新分配的内存。
更改前的父空地址：0010BD50
更改前的子空结束：0010BD50
更改后的子空结束：0010DD50
更改后的父空地址：0010BD50
PASS: 父进程中的空洞大小相同。
TEST 5 PASSED
```

测试全部通过

