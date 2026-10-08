

# 548
# join 
# 选项

下面的某些选项使用了参数 `filename`。该参数应该是 1 或 2，分别引用 `file1` 或 `file2`。

- -a filename

除了正常输出外，为文件 `filename` 中的每一行无法配对的行生成一条输出，其中 `filename` 为 1 或 2。如果你同时指定了 `-a 1` 和 `-a 2`，则输出所有无法配对的行。

- -e string

将空输出字段替换为 `string`。

- -j filename

等同于 `-1 filename` `-2 filename`。

- -j1 fieldname

等同于 `-1 filename`。

- -j2 fieldname

等同于 `-2 filename`。字段从 1 开始编号。

- -o list

在每行输出包含 `list` 中指定的字段。由 `list` 选择但在输入中未出现的字段被视为空输出字段（即 `-e 选项` 的效果）。每个元素要么是文件名编号，要么是 0（0 表示连接字段）。除非特别请求，否则不打印公共字段。

- -t char

使用字符 `char` 作为分隔符。行中 `char` 的每次出现都具有意义。使用字符 `char` 作为输入和输出的字段分隔符。当你指定此选项时，排序术语（collating term）应与带有 `-b `的 `sort` 相同。

- -v filename

代替默认输出，仅为 `filename` 中的每一行无法配对的行生成一条输出，其中 `filename` 为 1 或 2。如果你同时指定了 `-v 1` 和 `-v 2`，则输出所有无法配对的行。

- -1 filename

在 `file1` 的第 `filename-th` 个字段上连接。字段为从 1 开始的整数。

- -2 filename

在 `file2` 的第 `filename-th` 个字段上连接。字段为从 1 开始的整数。

# 操作数

- file1
file2

要连接的文件路径名。如果 `file1` 或 `file2` 操作数之一为 `-`，则使用标准输入代替。

`file1` 和 `file2` 必须按照 `LC_COLLATE` 确定的连接字段的升序排序顺序进行排序，通常是每行的第一个字段（参见 `sort(1)`）。

# join 549
# 用法

关于 `join` 在遇到大于或等于 2 Gbytes(**31 bytes**) 的文件时的行为描述，请参见 largefile(5)。

# 示例

以下命令行连接了密码文件和用户组文件，根据数字组 ID 进行匹配，并输出用户名、组名和登录目录。假设这些文件已在组 ID 字段上按照 ASCII 排序顺序进行了排序。

```
castle@ join -j1 4 -j2 -o 1.1 2.1 1.6 -t: /etc/passwd /etc/group
root::
daemon:
bin:/usr/bin
sys:
adm:/var/adm
lp:/usr/spool/lp
nuucp:nuucp:/usr/spool/uucpublic
```

-o 0 字段本质上选择了连接字段的并集。例如，给定文件 `phone`：

| 姓名 | 电话号码 |
| :--- | :--- |
| Don | +1 123-456-7890 |
| Hal | +1 234-567-8901 |
| Yasushi | +2 345-678-9012 |

以及文件 `fax`：

| 姓名 | 传真号码 |
| :--- | :--- |
| Don | +1 123-456-7899 |
| Keith | +1 456-789-0122 |
| Yasushi | +2 345-678-9012 |

-o 0 字段（field） 元素。每个元素要么是文件名编号，要么是 0（0 表示连接字段）。除非特别请求，否则不打印公共字段。

```
example@ join -t "tab" phone fax
```

-t char 使用字符 `char` 作为分隔符。如果文件 `phone` 如下：

| 姓名 | 电话号码 |
| :--- | :--- |
| Don | +1 123-456-7890 |
| Hal | +1 234-567-8901 |
| Yasushi | +2 345-678-9012 |

文件 `fax` 如下：

| 姓名 | 传真号码 |
| :--- | :--- |
| Don | +1 123-456-7899 |
| Keith | +1 456-789-0122 |
| Yasushi | +2 345-678-9012 |

-e string 将空输出字段替换为 `string`。如果文件 `phone` 如下：

| 姓名 | 电话号码 |
| :--- | :--- |
| Don | +1 123-456-7890 |
| Hal | +1 234-567-8901 |
| Yasushi | +2 345-678-9012 |

文件 `fax` 如下：

| 姓名 | 传真号码 |
| :--- | :--- |
| Don | +1 123-456-7899 |
| Keith | +1 456-789-0122 |
| Yasushi | +2 345-678-9012 |

-a filename 除了正常输出外，为文件 `filename` 中的每一行无法配对的行生成一条输出，其中 `filename` 为 1 或 2。如果你同时指定了 `-a 1` 和 `-a 2`，则输出所有无法配对的行。

-v filename 代替默认输出，仅为文件 `filename` 中的每一行无法配对的行生成一条输出，其中 `filename` 为 1 或 2。如果你同时指定了 `-v 1` 和 `-v 2`，则输出所有无法配对的行。

-1 filename 在 `file1` 的第 `filename-th` 个字段上连接。字段为从 1 开始的整数。

-2 filename 在 `file2` 的第 `filename-th` 个字段上连接。字段为从 1 开始的整数。

