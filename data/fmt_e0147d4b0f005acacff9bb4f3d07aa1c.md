
```
help [command]
```

打印关于 `ftp` 命令 `ftp-command` 的信息消息。如果未指定 `ftp-command`，则打印所有 `ftp` 命令列表。

```
id [seconds]
```

将远程服务器上的空闲计时器设置为秒数。如果省略 `seconds`，`ftp` 将打印当前空闲计时器。

```
lcd [local-directory]
```

将本地工作目录设置为 `local-directory`。如果未指定 `local-directory`，则将本地工作目录设置为用户的家目录。

```
ls [remote-directory] [local-file]
```

将 `remote-directory` 列表写入 `local-file`。列表包含服务器选择包含的任何依赖于系统的信息；例如，大多数 UNIX 系统通过 `ls` 命令生成（另参见 `list`）。如果既未指定 `remote-directory` 也 `local-file`，则列出远程工作目录。如果启用了通配符，元字符将被展开。

```
macdef macro-name
```

定义一个宏。随后的行将存储为宏 `macro-name`；空行将终止宏输入模式。所有定义的宏限制为 16 个，总字符数为 4096 个。宏将一直保留到执行 `close` 命令。宏处理器将 `$` 和 `\` 解析为特殊字符。`$` 后跟一个数字（或多个数字）将被替换为宏调用命令行上的对应参数。

```
rm remote-file
```

删除 `remote-file`。`remote-file` 可以是一个空目录。禁用通配符。

```
delete remote-file.
```

删除 `remote-file`。`remote-file` 可以是一个空目录。

```
get remote-file [local-file]
```

将 `remote-file` 复制到 `local-file`。如果未指定 `local-file`，`ftp` 使用指定的 `remote-file` 名称作为 `local-file` 名称，但受当前 `case`、`ntrans` 和 `nmap` 设置的影响。

```
glob
```

切换文件通配符。当启用文件匹配通配符时，`ftp` 会展开文件名和目录中的 `sh(*)`。这些字符包括 `*`、`?`、`[`、`]`、`~` 和 `()`。服务器会展开远程文件和目录名。`ftp` 命令的通配符始终会被展开。如果启用了通配，多文件命令 `mdelete`、`mdr`、`mget`、`mls` 和 `mput` 也会展开这些元字符。

```
hash
```

每传输 1024 字节切换一次哈希符号（`#`）。
