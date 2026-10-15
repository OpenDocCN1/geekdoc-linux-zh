
## `ftphosts`

你使用 `ftphosts` 文件来允许或拒绝其他主机计算机访问你的 FTP 站点。当远程系统访问你的系统时，它是通过以注册用户的身份登录的。访问是通过已经在你的系统中设置好的用户账户进行的。你可以允许远程主机以特定用户身份登录，或者拒绝某个特定用户的访问。你可以使用这种控制方法来允许或拒绝远程主机对 FTP 服务器的匿名访问。

`ftphosts` 文件有两种类型的条目：一种用于允许访问，另一种用于拒绝访问。允许访问的条目以关键字 `allow` 开头，然后是你的系统中被允许访问的用户账户，最后是远程主机的地址。该地址可以是一个用于匹配多个用户的模式。你可以使用任何文件名生成符号（参见第 10 章）。拒绝访问的条目以关键字 `deny` 开头，然后是你的系统中被拒绝访问的用户账户，最后是远程主机的地址。`deny` 和 `allow` 术语是一种限制严格得多的控制，而 `deny` 则是一种更开放的控制。`allow only` 只允许从远程主机到指定账户的访问。不允许任何其他访问。你可以使用 `allow` 仅允许远程主机匿名访问。`deny` 在主机上仅拒绝对指定账户的访问。你可以使用 `deny` 拒绝特定系统的匿名访问，但不允许一个用户到另一个用户的直接 FTP 访问。

## `ftusers` 和 `ftgroups`

`ftusers` 文件列出了无法访问 FTP 服务的用户。例如，即使知道密码，也不应允许 FTP 连接访问 `root` 用户。该文件最初将包含你系统中所有用户（如 `root`、`mail` 和 `bin`）的列表。

`ftgroups` 是一个组访问文件，允许 FTP 用户成为你系统中指定组的成员。该文件列出了特殊的组密码。要使这些密码生效，必须在 `ftppasswd` 文件将 `Private` 条目设置为 `yes`。

## `ftpconversions`

`ftpconversions` 文件存储了压缩和归档操作可能的 FTP 转换。它作为一个 FTP 转换数据库运行，列出了所有可能的转换。安装包包含一个默认的 `ftpconversions` 文件，其中已经包含了最常用转换的条目。文件中的每一行都是一个包含八个字段的记录，字段用逗号分隔。这些字段是 `Strip`、`Prefix`、`Postfix`、`External Command`、`Types`、`Options` 和 `Description`。

`Prefix` 和 `Postfix` 字段指的是执行指定操作后对文件名的更改。`Strip Prefix` 从文件名中移除指定的后缀名，例如，`gzip` 压缩的文件后缀为 `.gz`。如果命令是使用 `gzip` 压缩文件，那么 `Add Postfix` 条目中应该放置 `.gz`。当文件被压缩时，`.gz` 会被加到末尾。如果你使用 `gzip` 解压文件，那么你可能想要移除 `.gz` 后缀名。为此，你将把 `.gz` 放在 `Strip` 字段中。`Strip` 和 `Add Postfix` 对前缀执行相同类型的操作。

`external command` 是你用于转换文件的命令。你可以列出文件的文件的选项。`Prefix` 和 `Postfix` 字段指的是执行指定操作后对文件名的更改。`Strip Prefix` 从文件名中移除指定的后缀名，例如，`gzip` 压缩的文件后缀为 `.gz`。如果命令是使用 `gzip` 压缩文件，那么 `Add Postfix` 条目中应该放置 `.gz`。当文件被压缩时，`.gz` 会被加到末尾。如果你使用 `gzip` 解压文件，那么你可能想要移除 `.gz` 后缀名。为此，你将把 `.gz` 放在 `Strip` 字段中。`Strip` 和 `Add Postfix` 对前缀执行相同类型的操作。

## FTP 日志文件：`xfer`

此文件包含你的服务器执行的连接和任务的日志信息。在 `Red Hat` 系统上，它位于 `/var/log`。在其他系统中，它可能在 `/usr/adm`。该文件由服务器条目组成，每行一个。条目分为几个字段。这些字段是 `current-time`、`transfer-time`、`remote-host`、`file-size`、`transfer-type`、`action-direction`、`access-mode`、`username`、`service-name`、`authentication-method` 和 `authenticated-user-id`。

`transfer-time` 是传输时间（秒）。`remote-host` 是建立连接的远程系统地址，`username` 是用户名。`transfer-type` 是 `a`（ASCII）或 `b`（二进制）。`access-mode` 是用户登录的方法：匿名用户为 `a`，游客为 `g`，真实登录（到账户）为 `r`。`direction` 是 `o`（输出）或 `i`（输入）。以下示例显示了用户 `larisa` 传输的文件。第一个条目显示了时间、FTP 服务器和文件大小以及文件名。

```
