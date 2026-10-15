
# `SAM POLICY SET <account policy> <value>`

设置账户策略的值。有效值可以是：`“forever”`、`“never”`、`“off”`或数字。

# `SAM PROVISION`

仅在设置 `ldaps:editpolicy` 且 `winbindd` 运行时可用。它在 `idap` 树上正确地填充基本账户（`Administrator`）和组（`Domain Users`, `Domain Admins`, `Domain Guests`）。

# `IDMAP DUMP <local tdb file name>`

转储指定的本地 `tdb` 文件包含的映射。此命令用于仅转储由 `idmap_tdb` 后端产生的映射。

# `IDMAP RESTORE [input file]`

从指定的文件或标准输入恢复映射。

# `IDMAP SET SECRET <DOMAIN> <secret>`

为指定的域存储密钥，主要用于使用 `idmap_ldap` 作为后端的域。在这种情况下，该密钥被用作绑定到 `ldap` 服务器的用户 `DN` 的密码。

# `IDMAP SET RANGE <RANGE> <SID> [index] [--db=<DB>]`

在 `autorid` 数据库中为指定的域（及索引）存储域范围映射。

# `IDMAP SET CONFIG <config> [--db=<DB>]`

从 `autorid` 数据库更新 `CONFIG` 条目。

# `IDMAP GET RANGE <SID> [index] [--db=<DB>]`

从 `autorid` 数据库中获取指定域和索引的范围。

# `IDMAP GET RANGES <SID> [--db=<DB>]`

获取所有域或由给定 `SID` 标识的域的范围。

# `IDMAP GET CONFIG [--db=<DB>]`

从 `autorid` 数据库获取 `CONFIG` 条目。

# `IDMAP DELETE MAPPING [-f] [--db=<DB>] <ID>`

从 `IDMAP` 数据库中删除映射 `<ID> -> gid <-> uid`。映射由 `<ID>` 提供，其可能是一个 `sid: S-x...` 一个 `gid: "GID number"` 或一个 `uid: "UID number"`。使用 `-f` 删除无效的部分映射 `<ID> -> xx`

使用 `"smcontrol idmap ..."` 通知正在运行的 `smbd` 实例。详情请参考 `smbcontrol(1)` 手页。

# `IDMAP DELETE RANGE [-f] [--db=<TDB>] <RANGE>|<SID> <INDEX>]`

从 `autorid` 数据库中删除由 `'RANGE'` 或 `"domain SID 和 INDEX"` 标识的域范围映射。使用 `-f` 删除无效映射。

# `IDMAP DELETE RANGES [-f] [--db=<TDB>] <SID>`

删除由 `SID` 标识的域的所有域范围映射。使用 `-f` 删除无效映射。

# `IDMAP CHECK [-v] [-r] [-a] [-T] [-f] [-l] [--db=<DB>]`

检查并修复 `IDMAP` 数据库。如果没有提供任何选项，则对数据库进行只读检查。此外，可以选择以下选项之一的交互或自动修复模式：

- `repair`

交互式修复模式，会提出很多问题。

- `auto`

非交互式修复模式，使用默认答案。

- `verbose`

产生更多输出。

- `force`

尝试应用更改，即使它们无法干净地应用。

- `test`

空运行，显示将进行哪些更改但不触碰任何内容。

- `lock`

在检查时锁定数据库。

- `<db < >`

检查指定的数据库。

它将报告发现的以下错误：

缺失反向映射（Missing reverse mapping）：

存在映射 `A->B` 的记录，但没有 `B->A`。修复映射的默认操作是通过添加反向映射来“修复”此问题。

无效映射（Invalid mapping）：

存在映射 `A->B` 的记录，其中 `B->C`。默认操作是“修复”。

缺失高水位线（Missing HWM）：

未设置高水位线。默认操作是“修复”。

无效记录（Invalid record）：

解析失败。默认操作是“修复”。

从 `3.0` 版本开始，Samba 现在支持非根用户使用 `smb.conf` 参数：`“usershare owner only”`、`“usershare allow list”`和`“usershare deny list”`创建定义的共享。设置如下：

# `USERSHARE add <path> [comment] [acl] [guest_ok=[y|n]]`

添加或替换名为 `"sharename"` 的新定义共享。`"path"` 指定了系统上要导出的绝对路径。可以对该路径进行限制，请使用全局 `smb.conf` 参数：`“usershare owner only”`，并设置为。

可选的 `"comment"` 参数是客户端浏览时在共享上显示的注释。

可选的 `"acl"` 字段指定哪些用户对整个共享具有读写权限。请注意，除非设置了 `smb.conf` 参数 `"usershare allow guests"`，否则不允许访客连接。用户共享 `acl` 的定义为：`“user:permission”`，其中 `user` 是系统上的有效用户名，`permission` 可以 `"F"`、`R"` 或 `"D"`。

- `F`: 完全权限，即读和写权限。

- `D`: 拒绝某个用户，即防止该用户访问此共享。

- `R`: 只读，即对此共享仅有读取访问权限（无法创建新文件或目录或写入文件）。

在未给出 `"acl"` 的情况下，默认值为 `"Everyone:R"`，这意味着任何经过身份验证的用户都有只读访问权限。

可选的 `"guest_ok"` 与 `smb.conf` 中的同名参数具有相同效果，即允许访问此用户共享。只有在 `smb.conf` 中将全局参数 `"usershare allow guests"` 设置为 `true` 时该参数才有效。命令如下：

- `net ushare add <path> [comment] [acl] [guest_ok=[y|n]]`

添加或更改定义的共享，使用与要修改相同的 `sharename`。

- `net ushare delete <sharename>`

删除定义的共享。

- `net ushare info [-l|long] <wildcard sharename>`

打印关于用户共享的信息。

- `net ushare list [-l|long] <wildcard sharename>`

列出定义的共享。

没有单独修改现有定义共享的命令，只需使用 `"net ushare add [sharename]"` 命令，使用与要修改相同的 `sharename` 并指定你想要的新选项即可。Samba `smbd` 在连接时感知用户定义共享的修改，因此可以立即生效，无需在添加、删除或更改定义共享时重启 `smbd`。

# `USERSHARE DELETE sharename`

按名称删除自定义共享。Samba `smbd` 进程会立即检测到此更改，尽管它不会断开当前连接到已删除共享的用户。

# `USERSHARE INFO [-l|--long [wildcard sharename]`

获取当前用户拥的所有匹配给定模式的自定义共享信息，或所有用户的信息。

`net ushare info` 命令本身会列出当前用户创建的共享信息，或限制为匹配给定通配符模式的共享名称（`*` 匹配一个或多个字符，`?` 仅匹配一个字符）。如果给出了 `-l` 或 `--long` 选项，它将打印其他用户创建的共享信息。

关于共享提供的信息所示：`[foobar] path=/home/jeremy comment=testme_acl=Everyone:F guest ok=n`。这是自定义共享的当前设置列表，可以通过 `net ushare add` 命令进行修改。

# `USERSHARE LIST [-l|--long wildcard sharename`

列出当前用户拥有的所有匹配给定模式的自定义共享，或所有用户的信息。

`net ushare list` 命令本身会列出当前用户创建的共享名称，或限制为匹配通配符模式的共享名称（`*` 匹配一个或多个字符，`?` 仅匹配一个字符）。如果给出了 `-l` 或 `--long` 选项，它将列出其他用户创建的共享名称。

# `[RPC] CONF`

从 `3.2.0` 版本开始，Samba 服务器可以通过存储在注册表的数据进行配置。这些配置数据可以使用新的 `net conf` 命令进行编辑。此外还可以通过启用 `RPC` 模式并指定远程服务器的地址来配置远程 Samba 服务器。

此类配置数据的部署可以在 `smb.conf` 文件中两个级别激活：注册表共享定义通过在 `[global]` 部分将注册表共享设置为 `"yes"` 来激活；全局选项则通过在 `[global]` 部分中设置 `include = registry[]` 来激活混合配置，或者通过在 `[global]` 部分中设置 `config backend = registry[]` 来激活仅限注册表的配置。详细信息请参 `smb.conf(5)` 手册。

命令如下：

- `[rpc] conf list` - 以类似 `smb.conf` 的格式转储完整配置。

- `net [rpc] conf import` - 从 `smb.conf` 格式的文件导入配置。

- `net [rpc] conf listshares` - 列出注册表共享。

- `net [rpc] conf drop` - 删除注册表中完整配置。

- `net [rpc] conf showshare` - 显示注册表共享的定义。

- `net [rpc] conf addshare` - 创建一个新的注册表共享。

- `net [rpc] conf delete` - 删除注册表共享。

- `net [rpc] conf setparam` - 存储一个参数。

- `net [rpc] conf getparam` - 获取参数值。

- `net [rpc] conf delparam` - 删除一个参数。

- `net [rpc] conf getincludes` - 显示共享定义的包含项。

- `net [rpc] conf setincludes` - 设置共享的包含项。

- `net [rpc] conf delincludes` - 删除共享定义中的包含项。

# `[RPC] CONF LIST`

将存储在注册表中的配置数据以类似 `smb.conf` 的格式打印到标准输出。

# `[RPC] CONF IMPORT—[test]-[T] filename [section]`

此命令从 `smb.conf` 格式的文件导入。如果输入文件中遇到的节在注册表中存在，则其内容将被替换。注册表中在输入文件中没有对应项的节将不受影响。如果你想删除这些项，则必须使用 `net conf drop` 或 `net conf delshare` 命令。可以选择指定一个节以将导入命令的影响限制在该特定节内。通过在命令行上指定参数 `-T` 可启用测试模式。在测试模式下，注册表不会发生任何更改，而是将结果配置打印到标准输出。

# `[RPC] CONF LISTSHARES`

列出注册表中定义的共享名称。

# `[RPC] CONF DROP`

删除注册表中的完整配置数据。

# `[RPC] CONF SHOWSHARE sharename`

显示指定的共享或节的定义。指定 `“global”` 作为共享名称从注册表中检索全局配置选项是有效的。

# `[RPC] CONF ADDSHARE sharename path [writeable={y|N} [guest_ok={y|N} [comment]]`

创建一个新的注册表共享。指定的 `sharename` 和 `path` 是有效的。可以指定 `writeable={y|N}`、`guest_ok={y|N}` 和 `comment`。通过 `net conf setparm` 命令可以获得相同的结果。

# `[RPC] CONF DELSHARE sharename`

删除注册表中的共享定义。

# `[RPC] CONF SETPARM section value`

在注册表中存储参数。节可以是 `global` 或特定的 `sharename`。如果节不存在，则创建它。

# `[RPC] CONF GETPARM section`

显示存储在注册表中的参数。

# `[RPC] CONF DELPARM section`

删除注册表中的参数。

# `[RPC] CONF GETINCLUDES section`

获取节的包含项列表。由于注册表的性质和包含指令的性质，包含项需要特殊处理：参数按参数名称存储在注册表中，因此每个参数只有一个实例。

# `[RPC] CONF SETINCLUDES section`

设置节的包含项列表。

# `[RPC] CONF DELINCLUDES section`

从共享定义中删除包含。

# `REGISTRY`

操作 Samba 的注册表。注册表命令有：

- `enumerate` - 枚举键值。

- `enumerate_recursive` - 枚举值和子键。

- `createkey` - 如果不存在则创建新键。

- `deletekey` - 在没有子键的情况下删除键。

- `deletekey_recursive` - 删除指定的键及其所有子键。

- `getvalue` - 输出键值的类型和实际值。

- `getvaluer` - 输出值的实际值。

- `setvalue` - 设置现有键的值名。类型可以是 `sz`、`multi_sz` 或 `dword`。对于 `multi_sz`，值可以多次给定。

- `increment` - 在锁定期间将键的 `DWORD` 值增加 `inc`。`inc` 默认为 `1`。

- `deletevalue` - 删除键的值名。

- `getsdl` - 获取键的安全描述符。

- `getsdl_sdl` - 以安全描述定义语言（`SDDL`）字符串格式获取键的安全描述符。

- `setsdl_sdl` - 从安全描述定义语言（`SDDL`）字符串设置键的安全描述符。

# `REGISTRY IMPORT file [—precheck <precheck-file>] [opt]`

导入注册表项（`.reg`）文件。可用选项包括：

- `precheck check-file`: 这在应用导入文件之前，检查预检查文件中指定的某些键或值是否存在的机制。只有在预检查成功时，才会应用导入文件。

预检查遵循标准的注册表文件语法，具有以下语义：

- `<value name=><value>` 检查值是否存在且具有给定的值。

- `<value name>=-` 检查值不存在。

- `[key]` 检查键是否存在。

- `[-key]` 检查键不存在。

# `REGISTRY EXPORT keyfile[opt]`

将键导出到注册表项（`.reg`）文件。

# `REGISTRY CONVERT in out [inopt] optout`

转换输入的注册表项（`.reg`）文件。

# `REGISTRY CHECK [-ravTl] [-o <ODB>] [--wipe] [<ODB>]`

检查并修复注册表数据库。如果没有提供任何选项，则将对数据库进行只读检查。可以通过以下选项选择交互式或自动修复模式：

- `-r|repair`

交互式修复模式，会提出许多问题。

- `-a|auto`

非交互式修复模式，使用默认答案。

- `-v|verbose`

产生更多输出。

- `-T|test`

空运行，显示将进行哪些更改，但不触动任何内容。

- `-l|lock`

在执行检查时锁定数据库。

- `-reg-version={1,2,3}`

指定注册表数据库的格式。如果没有指定，则默认为二进制文件的值；或者如果命令行中显式指定了 `registry.tdb`，则默认为 `INFO/version` 记录中的值。

- `--db|<ODB>`

检查指定的数据库。

- `-o|output <ODB>`

创建一个新的注册表数据库 `<ODB>` 而不是修改输入。如果 `<ODB>` 已存在，则可能会覆盖它。

- `--wipe`

替换注册表数据库，而不是修改输入或覆盖现有的输出数据库。

# `EVENTLOG`

从 `3.4.0` 版本的 `net` 开始，可以读取、转储、导入和导出原生 `win32` 事件日志文件（通常为 `*.evt`）。`evt` 文件由原生 Windows 事件查看器工具使用。

只有当 `smb.conf` 中使用了 `eventlog list` 时，`evt` 文件的导入和导出才能成功。详情请参阅 `smb.conf(5)` 手页。

`eventlog` 命令有：

- `- eventlog dump` - 将事件 `*.evt` 文件打印到屏幕。

- `eventlog import` - 将事件 `*.evt` 导入 `samba` 内部事件日志的 `tdb` 表示。

- `eventlog export` - 将 `samba` 内部事件日志的 `tdb` 表示导出为事件 `*.evt` 文件。

# `EVENTLOG DUMP filename`

将事件日志 `*.evt` 文件打印到标准输出。

# `EVENTLOG IMPORT filename`

将由 `filename` 定义的事件 `*.evt` 文件导入由 `eventlog` 定义的 `samba` 内部事件日志 `tdb` 表示。`eventlog` 需要 `smb.conf` 中定义的 `eventlog list` 部分。详情请参阅 `smb.conf(5)` 手页。

# `EVENTLOG EXPORT filename eventlog`

将由 `eventlog` 定义的 `samba` 内部事件日志 `tdb` 表示导出为由 `filename` 定义的事件 `*.evt` 文件。`eventlog` 需要 `smb.conf` 中定义的 `eventlog list` 部分。详情请参阅 `smb.conf(5)` 手页。

# `DOM`

从 `3.2.0` 版本开始，Samba 支持远程加入和退出 `API`，涵盖客户端和服务端。Windows 从 Windows `2000` 开始就支持远程加入功能。

为了让 Samba 远程加入或退出域，必须使用属于 `Domain Admins` 组成员、`Local Administrators` 组成员或被授予 `SeMachineAccountPrivilege` 权限的用户账户。
