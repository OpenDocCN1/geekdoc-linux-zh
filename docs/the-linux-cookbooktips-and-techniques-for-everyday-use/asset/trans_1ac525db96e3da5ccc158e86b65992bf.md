

## 8.2.4 按所有者在目录树中查找文件

要查找由特定用户拥有的文件，请将要搜索的用户名作为参数传递给 `-user` 选项。

- 要列出 `/usr/local/fonts` 目录树中由用户 warwick 拥有的所有文件，请输入：

```
$ find /usr/local/fonts -user warwick RET
```

`-group` 选项类似，但它匹配的是组所有权而不是用户所有权。

要列出在过去两到四天内被修改过的主目录树中的所有文件，请输入：

```
$ find ~ -mtime 2 -mtime -4 -daystart RET
```

在前面的示例中，组合选项 `-mtime 2` 和 `-mtime -4` 匹配在两到四天前被修改过的文件。

要查找比给定文件更新的文件，请将该文件的名称作为参数传递给 `-newer` 选项。

- 要查找 `/etc` 目录树中比文件 `/etc/motd` 更新的文件，请输入：

```
$ find /etc -newer /etc/motd RET
```

要查找比给定日期更新的文件，请使用 find Info 文档中描述的技巧：在 `/tmp` 中使用 touch 创建一个临时文件，将其时间戳设置为你想要搜索的日期，然后将该临时文件指定为 `-newer` 的参数。

- 要列出主目录树中在当年 5 月 4 日之后被修改过的所有文件，请输入：

```
$ touch -t 05040000 /tmp/timestamp RET
$ find ~ -newer /tmp/timestamp RET
```

在此示例中，创建了一个名为 `/tmp/timestamp` 的临时文件；搜索后，你可以将其删除（参见 删除文件和目录 部分）。

> NOTE: 你也可以通过将该数字作为参数传递给 `-used` 选项来查找最后访问时间比修改时间晚了若干天的文件。这对于查找使用率低的文件很有用——例如匹配 `-used +100` 的文件是在上次修改后 100 天或更长时间才被访问的。

## 8.2.5 对找到的文件运行命令

你还可以使用 find 对每个找到的文件执行指定的命令，通过将命令作为参数传递给 `-exec` 选项。如果在命令中使用字符串 `{ }`，则在命令执行时该字符串会被替换为当前找到的文件名。用字符串 `;` 标记命令的结束。

- 要查找 `~/html/` 目录树中扩展名为 `.html` 的所有文件，并输出这些文件中包含字符串 `organic` 的行，请输入：

```
$ find ~/html/ -name '*.html' -exec grep organic '{}' ';' RET
```

在此示例中，对于 find 找到的每个文件，都会执行命令 grep organic file，其中 file 依次为每个文件的名称。

要让 find 在执行每个找到的文件之前暂停并确认，请使用 `-ok` 代替 `-exec`。

- 要从主目录树中删除上次修改后超过一年才被访问的文件，并在每次删除前暂停确认，请输入：

```
$ find ~ -used +365 -ok rm '{}' ';' RET
```

## 8.2.6 按多个条件查找文件

你可以组合 find 的许多选项来查找符合多个条件的文件。

- 要列出主目录树中文件名以字符串 `top` 开头，并且比文件 `/etc/motd` 更新的文件，请输入：

```
$ find ~ -name 'top*' -newer /etc/motd RET
```

## The Linux Cookbook: Tips and Techniques for Everyday Use:

- 要压缩主目录树中所有大小为两兆字节或更大的文件，并且尚未使用 gzip 压缩的文件（文件名扩展名为 `.gz`），请输入：

```
$ find ~ -size +2000000c -regex '.*[^gz]' -exec gzip '{}' ';' RET
```

下表描述了你可以用 find 使用的许多其他选项。第一个表列出了并描述了 find 的通用选项，用于指定其行为。正如你所见，find 可以接受许多不同的选项；请参阅其手册页或 info 文档以获取全部选项。

| OPTION | DESCRIPTION |
|---|---|
| -daystart | 使用今天的开始时间而不是 24 小时前作为时间条件。 |
| -depth | 在每个目录之前先搜索其子目录。 |
| -help | 输出帮助信息并退出。 |
| -maxdepth levels | 指定在指定目录树中下降的最大目录层数。 |
| -mount or -xdev | 不下降挂载有其他磁盘的目录。 |
| -version | 输出版本号并退出。 |

下表列出了并描述了 find 的选项，用于指定要查找哪些文件。

以三种方式之一指定这些选项的数字参数：前面加上加号 (`+`) 以匹配大于或等于给定参数的值；前面加上连字符或减号 (`-`) 以匹配小于或等于给定参数的值；或单独给出数字以精确匹配该值。

| OPTION | DESCRIPTION |
|---|---|
| -amin minutes | 文件上次被访问以来的分钟数。 |
| -anewer file | 文件比 file 访问得更近。 |
| -atime days | 文件上次被访问以来的天数。 |
| -cmin minutes | 文件上次被更改以来的分钟数。 |
| -cnewer file | 文件比 file 更改得更近。 |
| -ctime days | 文件上次被更改以来的天数。 |
| -empty | 文件为空。 |
| -group group | 文件所属组的名称。 |
| -iname pattern | 不区分大小写的文件名模式匹配（`report` 匹配文件 `Report`、`report`、`REPORT` 等）。 |
| -ipath pattern | 文件的完整路径名与模式 pattern 匹配，不区分大小写（`./r*rt` 匹配 `./records/report` 和 `./Record-Labels/ART`）。 |

