
`smclient //mypc/myshare "" -N -Tx backup.tar`

```
- 恢复 users/docs 以外的所有内容
```

`smclient //mypc/myshare "" -N -Txx backup.tar users/docs`

```
- 为 users/docs 下的文件创建 tar 文件。
```

`smclient //mypc/myshare "" -N -Tc backup.tar users/docs`

```
- 创建与上述相同的 tar 文件，但这次使用 DOS 路径名。
```

`smclient //mypc/myshare "" -N -tc backup.tar users\edocs`

```
- 创建共享目录下所有文件和目录的 tar 文件。
```

`smclient //mypc/myshare "" -N -Tc backup.tar *`

```
- -D 初始目录 在开始前切换到初始目录。可能仅配合 `tar -T` 选项有用。
- -c 命令字符串是一个由分号分隔的命令列表，用于执行命令而不是提示标准输入（stdin）。`-N` 被 `-c` 隐含。

这在脚本以及将标准输入打印到服务器上时特别有用，例如 `-c 'print ' '-'`

## 操作

一旦客户端运行，用户将看到一个提示符：

```
smb: \\
```

提示符表示客户端已就绪并等待执行用户命令。每个命令都是单个单词，可选地带有参数以指定该命令。除非这些注释另有说明，否则命令和参数之间用空格分隔。所有命令均不区分大小写。命令参数可能敏感也可能不敏感，取决于具体命令。

你可以通过用双引号括起名称来指定包含空格的文件名，例如 `"a long file name"`。

显示在方括号中的参数（例如 `[parameter]` `）是可选的。如果不提供，命令将使用合适的默认值。显示在角括号中的参数（例如 `<parameter>`）是必填的。

请注意，所有在服务器上操作的命令实际上都是通过向服务器发送请求完成的。这种行为可能因服务器而异，取决于服务器的实现方式。

## 可用命令按字母顺序列出如下：

（注：此处命令列表翻译遵循了格式要求）

- * `[command]` 如果指定了 "`command`"，`?` 命令将显示关于指定命令的简要信息消息。如果未指定命令，将显示可用命令列表。
- `!` `[shell command]` 如果指定了 "`shell command`"，`!` 命令将在本地执行 shell 并运行指定的 shell 命令。如果未指定命令，将运行本地 shell。
- `cd` `[directory name]` 如果指定了 "`directory name`"，服务器上的当前工作目录将更改为指定的目录。由于任何原因导致指定的目录无法访问，此操作将失败。
- `del` `<mask>` 客户端将请求服务器尝试删除当前工作目录中匹配 "`mask`" 的所有文件。
- `dir` `<mask>` 将从服务器检索并显示服务器当前工作目录中匹配 "`mask`" 的文件列表。
- `exit` 退出程序。
- `get` `<remote file>` `[local file]` 将服务器上的 `<remote file>` 复制到 `[local file]`。
- `help` `[command]` 查看 `?` 命令。
- `lcd` `[directory name]` 如果指定了 "`directory name`"，服务器上的当前工作目录将更改为指定的目录。
- `ls` `<mask>` 查看 `dir` 命令。
- `mask` `<mask>` 允许在 `get` 和 `put` 命令中使用掩码过滤器。
- `lowercase` 切换文件名是否转换为小写。
- `md` `<mask>` 归档归档位。计算在备份文件时重置归档位。
- `md` `<mask>` 查看 `ls` 命令。
- `mkdir` `<directory name>` 在服务器上创建一个新目录。
- `mget` `<mask>` 从服务器复制匹配 "`mask`" 的所有文件到本地机器。
- `mput` `<local file>` `[remote file]` 将本地机器上的 `<local file>` 推送到服务器。
- `print` `<file>` 从服务器打印指定的 `<file>`。
- `printmode` `<binary or text>` 将打印模式设置为二进制或文本。
- `prompt` 切换在 `get` 和 `put` 命令执行期间的提示。
- `queue` 显示队列，显示作业 ID、名称和当前状态。
- `quit` 查看 `exit` 命令。
- `rd` `<directory>` 查看 `rmdir` 命令。
- `recurse` 切换目录递归。这些命令将处理所有目录（即它们正在复制的目录），并进入任何匹配指定掩码的目录。
- `rm` `<mask>` 删除服务器当前工作目录中所有匹配 `mask` 的文件。
- `rmdir` `<directory>` 在权限允许的情况下从服务器上删除指定的目录。
- `tar` `<cx>[IXBag]` 执行 tar 操作——见上面的 `-T` 命令。使用 `g`（增量）可能会受到 `tarmode` 命令的影响。使用 `N`（新于）将影响 tar 设置。注意，tar 的 `-x` 选项可能无效——请改用命令行。
- `blocksize` `<blocksize>` 块大小。后面必须跟一个有效的（大于零的）块大小。导致文件以 `blocksize*TBLOCK`（通常为 512 字节）为块写入。
- `tarmode` `<inlinereset>` 更改 tar 关于归档位的行为。在完整模式下，tar 将备份除归档设置以外的所有内容（这是默认模式）。在增量模式下，tar 将备份具有归档位的文件。

# 326
# 附录 C：Samba 手页

位设置。在重置模式下，tar 将重置其所备份的所有文件的归档位（这暗示意味着读/写共享）。

- `setmode` `<filename>` `<perm=[+\-rsha->]` DOS 属性命令的一个版本，用于设置文件权限。例如：

```
setmode myfile +r
```
