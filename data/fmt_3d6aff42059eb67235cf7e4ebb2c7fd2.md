
`redland-db-upgrade` 将 Redland 数据库从 0.9.11 及更早版本的格式转换为新格式。必须在每个 Redland 数据库上运行。例如，如果数据库 `a` 创建了文件 `a-sp2o.db`、`a-so2p.db` 和 `a-po2s.db`，则可以将其转换为新数据库 `b`：

```
redland-db-upgrade a b
```

### 参见

`(3)`,

### 作者

Dave Beckett -

## regdiff

### 名称

`regdiff` - Windows 注册表文件的差异比较程序

### 概要

`regdiff` [--help] [--backend=BACKEND] [--credentials=CREDENTIALS] [位置]

### 描述

`regdiff` 逐键逐值比较两个 Windows 注册表文件，并生成一个包含两个文件之间差异的文本文件。

`regdiff` 生成的文件随后可以通过 `regpatch` 实用程序应用于注册表文件。

`regdiff` 和 `regpatch` 使用与 Windows 中的 `regedit32.exe` 实用程序相同的文件格式。

### 选项

`--help`

显示可用选项列表。

`--backend BACKEND`

要加载的后端名称。可能的值有：`creg`、`regf`、`dir` 和 `rpc`。默认值是 `dir`。此参数可以指定两次：一次用于第一个注册表文件，一次用于第二个。

`--credentials=CREDENTIALS`

使用的凭据（如果有）。密码应与用户名用百分号分隔。

此参数可以指定两次：一次用于第一个注册表文件，一次用于第二个。

### 版本

本手册页适用于 Samba 套件的 4.0 版本。

### 参见

`grededit`, `regshell`, `regpatch`, `regtree`, `samba`, `patch`, `diff`

### 作者

此实用程序是 Samba 套件的一部分，由全球 Samba 团队开发。此手册页和 `regdiff` 由 Jelmer Vernooij 编写。

### 注释

1. Samba

2. Samba 团队

## regpatch

### 名称

`regpatch` - 将注册表补丁应用于注册表文件

### 概要

`regpatch` [--help] [--backend=BACKEND] [--credentials=CREDENTIALS] [位置] [补丁文件]

### 描述

`regpatch` 实用程序将注册表补丁应用于 Windows 注册表文件。补丁文件的格式应与 Windows 自带的 `regdiff` 实用程序和 `regedit32.exe` 所使用的格式相同。

如果未在命令行中指定补丁文件，`regpatch` 会尝试从标准输入读取。

### 选项

`--help`

显示可用选项列表。

`--backend BACKEND`

要加载的后端名称。可能的值为：`creg`、`regf`、`dir` 和 `rpc`。默认值为 `dir`。

`--credentials=CREDENTIALS`

要使用的凭据（如有）。密码应与用户名用百分号分隔。

### 版本

此 man 页适用于 Saa 套件的 4.0 版本。

### 参见

`regdiff`, `regtree`, `regshell`, `gregedit`, `saa`, `diff`, `patch`

### 作者

此实用程序是 `Saa` 套件的一部分，由全球 `Saa` 团队开发。此 man 页和 `regpatch` 由 Jclr Vernooij 编写。

### 注释

- 1. Saa

- 2. Saa 团队

## REGSHELL

### 名称

`regshell` - 使用 readline 的 Windows 注册表文件浏览器

### 概要

```
regshell [--help] [--backend=BACKEND] [--credentials=CREDENTIALS] [location]
```

### 描述

`regshell` 是一个实用程序，允许你像在常规 unix shell 中浏览文件系统一样浏览 Windows 注册表文件。

### 选项

`--help`

显示可用选项列表。

`--backend BACKEND`

要加载的后端名称。可能的值为：`creg`、`regf`、`dir` 和 `rpc`。默认值为 `dir`。

`--credentials=CREDENTIALS`

要使用的凭据（如有）。密码应与用户名用百分号分隔。

### 命令

`ck|cd <keyname>`

进入指定的子项。

`ch|predef [predefined-key-name]`

进入指定的预定义项。

`list|ls`

列出当前项的子项和值。

`mkkey|mkdir <keyname>`

创建一个项，其项名为指定 keyname，作为当前项的子项。

`rmval|rm <valname>`

删除指定的值。

`rmkey|rmdir <keyname>`

递归删除指定的子项。

`pwd|pwk`

打印当前项的完整名称。

`set|update`

更新项值的值。目前未实现。

`help|?`

打印可用命令列表。

`exit|quit`

退出 `regshell`。

### 示例

浏览 nt4 注册表文件

```
regshell -b nt4 NTUSER.DAT $$${PROTO.HIV}> ls K AppEvents K Console K Control Panel K Environnt K Identities K Keyboard Layout K Network K Printers K Software K UNICODE Program Groups K Windows 3.1 Migration Status $$${PROTO.HIV}> exit
```

在远程计算机上列出 HKEY_CURRENT_USER\AppEvents 的子项：

```
regshell --remote=ncacn_np:aurelia -c "jclr%secret" HKEY_CURRENT_MACHINE> p redef HKEY_CURRENT_USER HKEY_CURRENT_USER> cd AppEvents Current path is: HKEY_CURRENT_USER\AppEvents HKEY_CURRENT_USER\AppEvents> ls K EventLabels K Sches HKEY_CURRENT_USER\AppEvents> exit
```

### 版本

此 man 页适用于 Saa 套件的 4.0 版本。

### 参见

`regtree`, `regdiff`, `regpatch`, `gregedit`, `saa`

### 作者

此实用程序是 `Saa` 套件的一部分，由全球 `Saa` 团队开发。

此 man 页和 `regshell` 由 Jclr Vernooij 编写。

### 注释

- 1. Saa

- 2. Saa 团队

## REGTREE

### 名称

`regtree` - 文本模式注册表查看器

### 概要

```
regtree [--help] [--backend=BACKEND] [--fullpath] [--no-values] [--credentials=CREDENTIALS] [location]
```

### 描述

`regtree` 实用程序打印出 Windows 注册表文件的所有内容。子项的缩进级别比其父项多一级。

### 选项

`--help`

显示可用选项列表。

`--backend BACKEND`

要加载的后端名称。可能的值为：`creg`、`regf`、`dir` 和 `rpc`。默认值为 `dir`。

`--credentials=CREDENTIALS`

要使用的凭据（如有）。密码应与用户名用百分号分隔。

`--fullpath`

打印每个项的完整路径，而不仅仅是其名称。

`--no-values`

不打印值，只打印项。

### 版本

此 man 页适用于 Saa 套件的 4.0 版本。

### 参见

`grededit`, `regshell`, `regdiff`, `regpatch`, `saa`

### 作者

此实用程序是 `Saa` 套件的一部分，由全球 `Saa` 团队开发。此 man 页和 `regtree` 由 Jclr Vernooff 编写。

### 注释

- 1. Saa

- 2. Saa 团队

## RENAME

### 名称

`rena` - 重命名文件

### 概要

`rena` `[options]` *expression replacement file...*

### 描述
