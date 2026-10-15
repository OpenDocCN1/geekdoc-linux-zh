
输出应显示用户 `bobby` 不再列为具有访问 `allusers` 数据库的权限。（结果可能只是显示 `Empty set`。）

## 检查和修复数据库

随着时间的推移，数据库可能会损坏或存储信息效率低下。`MySQL` 附带了可用于检查和修复数据库的命令。`myisamchk` 和 `isamchk` 命令可分别用于检查 `MyISAM` 和 `ISAM` 数据库表。

`MyISAM` 表是 `MySQL` 的默认使用表。表默认存储在目录 `/var/lib/mysql/dbname` 中，其中 `dbname` 用你使用的数据库名称替换。每个表在该目录中有三个文件。每个文件以表名开头，以以下三个后缀之一结尾：

- `.frm` 包含表的定义（或表单）
- `.MYI` 包含表的索引。
- `.MYD` 包含表的数据。

以下流程描述如何使用 `myisamchk` 命令检查你的 `MyISAM` 表。（检查 `ISAM` 表的流程相同，只是改用 `isamchk` 命令。）

> **警告：** 在使用 `myisamchk` 进行修复之前，请备份你的数据库表。尽管 `myisamchk` 不太可能损坏你的数据，但备份仍然是良好的预防措施。

1. 通过在终端窗口中以 `root` 用户输入以下内容暂时停止 `MySQL`：

```
# /etc/init.d/mysql stop
```

2. 你可以一次检查所有或部分数据库表。第一个示例显示如何检查 `allusers` 数据库中名为 `names` 的表。

```
# myisamchk /var/lib/mysql/allusers/names.MYI

Checking MyISAM file: /var/lib/mysql/allusers/names.MYI

Data records:       5    Deleted blocks:       0

- check file-size

- check key delete-chain

- check record delete-chain

- check index reference

- check record links
```

你也可以按如下方式一次检查所有数据库的表：

```
# myisamchk /var/lib/mysql/*/*.MYI
```

前面的示例显示了一个简单的五条记录数据库，未遇到错误。如果看到与上面所示不同的如下输出，你可能需要修复数据库：

```
Checking MyISAM file: names.MYI

Data records:         5    Deleted blocks:       0

- check file-size

myisamchk: warning: Size of datafile is: 89  Should be: 204

- check key delete-chain

- check record delete-chain

- check index reference

- check record links

myisamchk: error: Found wrong record at 0

MyISAM-table 'names.MYI' is corrupted

Fix it using switch "-r" or "-o"
```

3. 要修复损坏的数据库，可以运行以下命令

```
# myisamchk -r /var/lib/mysql/allusers/names.MYI

- recovering (with keycache) MyISAM-table 'names.MYI'
```

```
Data records: 5

Found wrong stored record at 0

Data records: 4
```

4. 如果由于某种原因 `-r` 选项不起作用，你可以尝试使用 `-o` 选项运行 `myisamchk` 命令。这是一种较慢、较旧的修复方法，但可以处理 `-r` 选项无法处理的几个问题。以下是示例：

```
# myisamchk -o /var/lib/mysql/allusers/names.MYI
```

如果你的计算机内存充足，请提高 `myisamchk` 命令行上的键缓冲区大小值，这将减少检查数据库所需的时间。例如，你可以使用以下命令行：

```
myisamchk -r -O --key_buffer_size=64M *.MYI
```
