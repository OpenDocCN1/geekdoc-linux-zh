
`<switch>` 为 YES（开启）或 NO（关闭）。`<typelist>` 是受此命令影响的用户类型列表，类型用逗号分隔。可用的用户类型有 `anonymous`（匿名）、`guest`（客人）和 `real`（真实）。

## delete

`delete` 命令告诉服务器 FTP 客户端是否有权删除服务器上的文件。命令的格式如下：

```
delete <switch> <typelist>
```

`<switch>` 为 YES（开启）或 NO（关闭）。`<typelist>` 是受此命令影响的用户类型列表，类型用逗号分隔。可用的用户类型有 `anonymous`、`guest` 和 `real`。

## overwrite

使用 `overwrite` 命令来控制 FTP 客户端是否可以上传文件并替换服务器上的文件。格式如下：

```
overwrite <switch> <typelist>
```

`<switch>` 为 YES（开启）或 NO（关闭）。`<typelist>` 是受此命令影响的用户类型列表，类型用逗号分隔。可用的用户类型有 `anonymous`、`guest` 和 `real`。

## rename

客户端软件可以向服务器发送 `rename` 请求来重命名文件。`rename` 命令决定此请求是否可以接受。格式如下：

```
rename <switch> <typelist>
```

`<switch>` 为 YES（开启）或 NO（关闭）。`<typelist>` 是受此命令影响的用户类型列表。用户可以是 `anonymous`、`guest` 和 `real`。

## umask

`umask` 命令决定客户端是否可以更改默认权限，类似于 `chmod` 命令。`umask` 命令的格式如下：

```
umask <switch> <typelist>
```

`<switch>` 为 YES（开启）或 NO（关闭）。`<typelist>` 是受此命令影响的用户类型列表。用户可以是 `anonymous`、`guest` 和 `real`。

## password-check

提供有效的邮件地址作为密码时，`passwd-check` 命令允许你监管匿名 FTP 站点。其格式如下：

```
passwd-check <strictness> <enforcement>
```

`<strictness>` 是三种可能的字符串之一：`none`、`trivial` 或 。`<enforcement>` 是两种可能的字符串之一：`warn` 或 `enforce`。通过使用 `warn` 作为 `<enforcement>`，当用户不符合 `<strictness>` 时将收到警告。

![](img/cbac72550c7126a22162e94d91a0c360_370_0.png)

## 网络服务

第二部分

## path-filter

如果你允许用户向服务器上传文件，你可能希望设置文件名（例如，不允许包含特殊字符）。你可以通过 `path-filter` 命令来实施此限制。其格式如下：

```
path-filter <typelist> <mesg> <allowed-regexp> <denied-regexp>
```

`<typelist>` 是受此命令影响的用户列表，用逗号分隔。用户类型有 `anonymous`、`guest` 和 `real`。`<mesg>` 是当文件不符合此标准时显示的文件名。`<allowed-regexp>` 是文件名必须符合的正则表达式。`<denied-regexp>` 是如果符合则文件被显式拒绝的正则表达式；`<denied-regexp>` 是可选参数。

例如，以下行会在匿名或客人上传不以 UL 开头或以 gif 结尾的文件时显示 `/ftp/.badfilename`：

```
path-filter anonymous,guest /ftp/.badfilename UL* gif
```

## upload

你可以使用 `upload` 命令结合 `path-filter` 来控制放置在服务器上的文件。`upload` 命令决定客户端在特定目录下放置文件的权限。该命令还决定了文件放置在该目录中的权限。`upload` 的格式如下：

```
upload <directory> <dirglob> <switch> <owner> <group> <mode> <mkdir>
```

`<directory>` 是受此命令影响的目录`<dirglob>` 是用于判断 `<directory>` 下的子目录是否为有效上传位置的正则表达式，`<switch>` 为 YES 或 NO，从而确定了可以或不可以进行上传。`<owner>`、`<group>` 和 `<mode>` 参数建立了文件放置在服务器上后的所有者、组和权限。你可以指定 `<mkdir>` 选项为 `dirs`（可以在指定的目录下创建子目录）或 `nodirs`（无法执行此操作）。

以下是一个示例 no：

```
upload /home/ftp * no
upload /home/ftp /incoming yes ftp ftp 0775 nodirs
```

此示例指定了 `/home/ftp/incoming` 目录（对匿名客户端而言为 `/incoming`）是放置文件的唯一位置。当文件放置在该目录中后，其所有者变为 `ftp`，组变为 `ftp`，权限为 775。`nodirs` 表示无法创建子目录。

第二行末尾的选项防止匿名客户端在 `/incoming` 下创建子目录。

> 提示
>
> 建议通过 ftp 将上传的文件设置为组所有，并赋予 775 文件权限。这允许只读访问，使得 `/incoming` 目录不会成为可疑材料（例如非法软件）的交易场所。

## 动态转换文件——ftpconversions 文件

`ftpconversions` 文件的格式如下：

`<1>:<2>:<3>:<4>:<5>:<6>:<7>:<8>`

`<1>` 是移除前缀（strip prefix）；`<2>` 是移除后缀（strip postfix）；`<3>` 是添加前缀（add-on prefix）；`<4>` 是添加后缀（add-postfix）；`<5>` 是调用的用于执行转换的外部命令；`<6>` 是文件类型；`<7>` 是用于日志的选项信息；`<8>` 是操作描述。

困惑吗？不用担心。每个选项实际上非常简单。接下来的章节将逐一描述。

## 移除前缀 (Strip Prefix)

移除前缀是文件名开头的字符串，在获取文件时应将其删除。例如，如果你想对以 `discography.` 开头的文件执行特殊操作，并在操作后删除该前缀，你可以指定 `.discography`。当客户端指定文件名时，不应包含该移除前缀。也就是说，如果文件名为 `discography.orb` 且客户端发出 `get orb` 命令，服务器将对文件执行可选命令并将结果传输给客户端。尽管文档中了他的相关说明，但目前不支持此功能。

## 移除后缀 (Strip Postfix)

移除后缀是文件名末尾的字符串，在获取文件时应将其删除。移除后缀通常用于在将 gzipped 文件传回客户端之前进行解压时，移除末尾的 `.gz`。

![](img/cbac72550c7126a22162e94d91a0c360_374_0.png)

## 添加前缀 (Add-On Prefix)

添加前缀是在文件从服务器传输到或传输时，插入文件名前的字符串。例如，你可能想在所有从服务器拉取并转换为大写的文件前插入字符串 `uppercase.`。尽管文档中了他的相关说明，但目前不支持此功能。

## 添加后缀 (Add-On Postfix)

添加后缀是在对文件执行操作完成后附加到文件名后的字符串。这种后缀通常用于客户端发出 `largefile.gz` 命令时，实际文件名仅为 `largefile`；在这种情况下，服务器使用 `gzip` 压缩文件并执行传输。

## 外部命令 (External Command)

每行的核心组件是外部命令。该条目指定了文件在与服务器之间传输时运行的程序。在文件传输过程中，它将通过程序进行过滤，其中下载（发送给客户端的文件）需要发送到标准输出，而上传（发送到服务器的文件）将来自标准输入。例如，如果你想为下载的文件提供 gzip 解压缩，条目将所示：

```
gzip -dc %s
```

行中的 `%s` 告诉服务器替换为用户请求的文件名。

## 文件类型字段 (Type of File Field)

`ftpconversions` 的 `type` 字段是可以处理的文件类型列表，类型名称之间用管道符号 (`|`) 分隔。识别的三种文件类型 `T_REG`、`T_ASCII` 和 `T_DIR` 分别代表普通文件、ASCII 文件和目录。该条目的示例为 `T_REG|T_ASCII`。

## 选项字段 (Options Field)

`ftpconversions` 的 `options` 字段与 `type` 字段类似，由一组用管道符号 (`|`) 分隔的名称组成。支持的三种选项类型 `O_COMPRESS`、`O_UNCOMPRESS` 和 `O_TAR` 分别指定命令是压缩文件、解压文件还是使用 `tar` 命令。示例条目为 `O_COMPRESS|O_TAR`，表示文件既经过压缩又进行了 tar 处理。

## ftpconversions 描述 (Description of ftpconversions)
