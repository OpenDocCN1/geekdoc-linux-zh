
## 使用 locate 和 updatedb

`locate` 和 `updatedb` 是用于在 Linux 系统中快速查找匹配给定模式文件的命令。但与 `find` 不同，`locate` 不会在文件系统中搜索该模式：相反，它在通过运行 `updatedb` 命令构建的数据库中查找。这可以提供非常快速的结果，但根据数据库最后更新的时间，结果可能不够精确。

使用 `locate` 最简单的方法是直接给它一个要搜索的模式。例如，要找到系统中的每个 JPEG 图像，你可以使用 `locate .jpg`。结果列表可能很长，但应该如下所示：

```bash
$ locate jpg
/home/carol/Downloads/Expert.jpg
/home/carol/Downloads/Hotbit.jpg
/home/carol/Downloads/Mate1.jpg
/home/carol/Downloads/Mate2.jpg
/home/carol/Downloads/Mate3.jpg
/home/carol/Downloads/Pentaro.jpg
/home/carol/Downloads/Sala.jpg
/home/carol/Downloads/pixel_3a_seethrough_1.jpg
/home/carol/Downloads/jpg_specs.doc
```

当请求 `jpg` 模式时，`locate` 会显示包含此模式的任何内容，无论其前后是什么。你可以在上述列表中的文件 `jpg_specs.doc` 中看到这一点：它包含该模式，但扩展名不是 `.jpg`。

**提示** 请记住，使用 `locate` 时匹配的是模式，而不是文件扩展名。

默认情况下，模式是区分大小写的。这意味着包含 `.JPG` 的文件不会被显示，因为模式是小写的。为避免这种情况，请向 `locate` 传递 `-i` 参数。重复我们之前的示例：

```bash
$ locate -i .jpg
/home/carol/Downloads/Expert.jpg
/home/carol/Downloads/Hotbit.jpg
/home/carol/Downloads/Mate1.jpg
/home/carol/Downloads/Mate1_old.JPG
/home/carol/Downloads/Mate2.jpg
/home/carol/Downloads/Mate3.jpg
/home/carol/Downloads/Pentaro.jpg
/home/carol/Downloads/Sala.jpg
/home/carol/Downloads/pixel_3a_seethrough_1.jpg
```

请注意，文件 `Mate1_old.JPG`（如上所述加粗显示）并未出现在之前的列表中。

你可以向 `locate` 传递多个模式，只需将它们用空格分开即可。下面的示例将对匹配 `zip` 和 `jpg` 模式的任何文件进行不区分大小写的搜索：

```bash
$ locate -i zip jpg
/home/carol/Downloads/Expert.jpg
/home/carol/Downloads/Hotbit.jpg
/home/carol/Downloads/Mate1.jpg
/home/carol/Downloads/Mate1_old.JPG
/home/carol/Downloads/Mate2.jpg
/home/carol/Downloads/Mate3.jpg
/home/carol/Downloads/OPENMSXPIHAT.zip
/home/carol/Downloads/Pentaro.jpg
/home/carol/Downloads/Sala.jpg
/home/carol/Downloads/gbs-control-master.zip
/home/carol/Downloads/lineage-16.0-20190711-MOD-quark.zip
/home/carol/Downloads/pixel_3a_seethrough_1.jpg
/home/carol/Downloads/jpg_specs.doc
```

使用多个模式时，你可以要求 `locate` 仅显示匹配所有这些模式的文件。这是通过使用 `-A` 选项来完成的。以下示例将显示任何匹配 `.jpg` 和 `.zip` 模式的文件：

```bash
$ locate -A .jpg .zip
/home/carol/Downloads/Pentaro.jpg.zip
```

如果你希望计算匹配给定模式的文件数量，而不是显示它们的完整路径，可以使用 `-c` 选项。例如，要计算系统中的 `.jpg` 文件数量：

```bash
$ locate -c .jpg
1174
```

`locate` 的一个问题是，它仅显示由 `updatedb` 生成的数据库（位于 `/var/lib/mlocate.db`）中存在的条目。如果数据库已过时，输出可能会显示自上次更新以来已删除的文件。避免这种情况的一种方法是添加 `-e` 参数，这将使其在输出中显示文件之前先检查该文件是否仍然存在。

当然，这并不能解决在最后一次数据库更新后创建的文件未显示出来的问题。为此，你必须使用命令 `updatedb` 更新数据库。这将花费多长时间取决于磁盘上的文件数量。

## 控制 updatedb 的行为

`updatedb` 的行为可以通过文件 */etc/updatedb.conf* 来控制。这是一个文本文件，其中每一行控制一个变量。空行将被忽略，以 # 字符开头的行被视为注释。

- **PRUNEFS=**
  在此参数后面指示的任何文件系统类型都不会被 `updatedb` 扫描。类型列表应通过空格分隔，并且类型本身不区分大小写，因此 NFS 和 nfs 是相同的。

- **PRUNENAMES=**
  这是一个以空格分隔的目录名称列表，这些目录不应被 `updatedb` 扫描。

- **PRUNEAPTHS=**
  这是一个 `updatedb` 应忽略的路径名称列表。路径名称必须通过空格分隔，并应按 `updatedb` 显示它们的方式指定（例如，*/var/spool* */media*）

- **PRUNE_BIND_MOUNTS=**
  这是一个简单的 *yes* 或 *no* 变量。如果设置为 yes，绑定挂载（使用 `mount --bind` 命令挂载在其他位置的目录）将被忽略。

## 查找二进制文件、手册页和源代码

`which` 是一个非常有用的命令，它显示可执行文件的完整路径。例如，如果你想定位 `bash` 的可执行文件，你可以使用：

```bash
$ which bash
/usr/bin/bash
```

如果添加了 `-a` 选项，该命令将显示所有匹配该可执行文件的路径名。观察区别：

```bash
$ which mkfs.ext3
/usr/sbin/mkfs.ext3

$ which -a mkfs.ext3
/usr/sbin/mkfs.ext3
/sbin/mkfs.ext3
```

**提示** 要查找 PATH 中有哪些目录，请使用 `echo $PATH` 命令。这将打印（echo）变量 PATH ($PATH) 的内容到你的终端。

`type` 是一个类似的命令，它将显示有关二进制文件的信息，包括其位置及其类型。只需使用 `type` 后跟命令名称：

```bash
$ type locate
locate is /usr/bin/locate
```

`-a` 参数的作用与 `which` 中相同，显示所有匹配该可执行文件的路径名。如下所示：

```bash
$ type -a locate
locate is /usr/bin/locate
locate is /bin/locate
```

而 `-t` 参数将显示命令的文件类型，可以是别名、关键字、函数、内置命令或文件。例如：

```bash
$ type -t locate
file

$ type -t ll
alias

$ type -t type
type is a built-in shell command
```

命令 `whereis` 更加多功能，除了二进制文件外，还可以用于显示手册页的位置，甚至程序的源代码（如果在你的系统中可用）。只需键入 `whereis` 后跟二进制文件名称：

```bash
$ whereis locate
locate: /usr/bin/locate /usr/share/man/man1/locate.1.gz
```

上述结果包括二进制文件（/usr/bin/locate）和压缩的手册页（/usr/share/man/man1/locate.1.gz）。

你可以使用命令行开关（如 `-b`，将结果限制为仅二进制文件；`-m`，将结果限制为仅手册页；或 `-s`，将结果限制为仅源代码）快速过滤结果。重复上面的例子，你会得到：

```bash
$ whereis -b locate
locate: /usr/bin/locate
$ whereis -m locate
locate: /usr/share/man/man1/locate.1.gz
```

## 引导练习

- 1. 假设一个程序需要创建一个一次性临时文件，该文件在程序关闭后将不再需要。在哪个目录下创建此文件是正确的？
- 2. 哪个临时目录*必须*在启动过程中被清除？
- 3. 使用 `find`，仅搜索当前目录，查找用户可写、在过去 10 天内修改过且大于 4 GiB 的文件。
- 4. 使用 `locate`，查找文件名中包含模式 `report` 以及 `updated`、`update` 或 `updating` 中任意一个的所有文件。
- 5. 如何查找 `ifconfig` 的手册页存储在哪里？
- 6. 需要向 `/etc/updatedb.conf` 添加哪个变量才能使 `updatedb` 忽略 ntfs 文件系统？
- 7. 系统管理员希望挂载一个内部磁盘（`/dev/sdc1`）。根据 FHS（文件系统标准），这个磁盘应该挂载在哪个目录之下？

## 探索性练习

- 1. 使用 **locate** 时，结果是从由 **updatedb** 生成的数据库中获取的。然而，该数据库可能会过时，导致 **locate** 显示不再存在的文件。如何让 **locate** 仅在其输出中显示现有的文件？
- 2. 查找当前目录或子目录（向下最多 2 层）中任何文件名包含模式 Status 或 statute 的文件，排除已挂载的文件系统。
- 3. 将搜索限制在 ext4 文件系统上，查找 /mnt 下至少对组具有执行权限、对当前用户可读且在过去 2 小时内有任何属性更改的文件。
- 4. 查找创建于 30 天前且距离当前目录至少两层深度的空文件。
- 5. 假设用户 carol 和 john 是组 mkt 的一部分。在 john 的主目录中查找 carol 也可以读取的任何文件。

