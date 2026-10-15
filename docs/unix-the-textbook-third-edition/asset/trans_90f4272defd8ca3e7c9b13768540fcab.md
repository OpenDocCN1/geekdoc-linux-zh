
注意，学生文件中的行按所有字符从左到右升序排列（整个行用作排序键）。以下命令使用从姓氏（即第二个字段，字段编号 1）开始的整行内容作为排序键对文件进行排序。

```
% sort +1 students
Jamie Davidson    j.davidson@uet.edu    515.001.1212
John Johnsen      j.johnsen@psu.net     301.999.8888
John Johnsen      john.johnsen@tp.com   503.555.1111
David Kendall     d_kendall@msnbc.org   229.111.2013
Kelly Kimberly    kellyk@umich.gov      555.123.9999
Hassaan Sarwar    hsarwar@k12.st.or     503.444.2132
Ibraheem Sarwar   ibraheem@abc.sci.com  222.123.4567
Nabeel Sarwar     n.sarwar@xyz.net      434.555.1212
Maham Sarwar      smsarwar@k12.st.or    713.888.0000
%
```

以下命令使用电话号码作为排序键并按逆序对文件排序，同时忽略前导空白（空格和制表符）。+3 选项指定电话号码为排序键（因为电话号码是最后一个字段），-r 选项通知 sort 以逆序显示排序输出，-b 选项要求 sort 工具忽略字段之间的前导空白。

```
% sort +3 -r -b students
Maham Sarwar      smsarwar@k12.st.or    713.888.0000
Kelly Kimberly    kellyk@umich.gov      555.123.9999
Jamie Davidson    j.davidson@uet.edu    515.001.1212
John Johnsen      john.johnsen@tp.com   503.555.1111
Hassaan Sarwar    hsarwar@k12.st.or     503.444.2132
Nabeel Sarwar     n.sarwar@xyz.net      434.555.1212
John Johnsen      j.johnsen@psu.net     301.999.8888
David Kendall     d_kendall@msnbc.org   229.111.2013
Ibraheem Sarwar   ibraheem@abc.sci.com  222.123.4567
%
```

如果字段由多个空格分隔，并且空格数量因行而异（如学生文件的情况），则 -b 选项很重要。原因是空格字符（按 ASCII 值）比所有字母和数字都要“小”，如果不跳过空白，将产生意外的输出。排序键可以组合，其中一个作为主键，其他的作为次键，按优先顺序指定（主键在前）。以下命令以姓氏作为主键、电话号码作为次键对学生文件进行排序。

## 常用选项/功能：

| 选项 | 描述 |
| --- | --- |
| `-exec CMD` | 如果命令 `CMD` 返回 0 作为其退出状态（对于成功执行的命令为真值），则被搜索的文件满足条件；`CMD` 必须以带引号的分号（`\;`）结尾。 |
| `-inum N` | 搜索 inode 编号为 N 的文件。 |
| `-links N` | 搜索链接数为 N 的文件。 |
| `-name pattern` | 搜索符合指定模式的文件。 |
| `-newer file` | 搜索在 file 之后被修改过（即比 file 更新）的文件。 |
| `-ok CMD` | 类似于 `-exec`，但首先会提示用户确认。 |
| `-perm octal` | 如果文件的权限为八进制，则搜索该文件。 |
| `-print` | 显示通过其余条件找到的文件的路径名。 |
| `-size ±N[c]` | 搜索大小为 N 块的文件；N 后跟 c 可用于以字符为单位衡量大小；+N 表示大小大于 N 块，-N 表示大小小于 N 块。 |
| `-user name` | 搜索由用户名或 ID 名拥有的文件。 |
| `\( expr \)` | 如果 expr 为真则为真；用于将条件与 OR 或 AND 组合分组。 |
| `! expr` | 如果 expr 为假则为真。 |

附录 A 中给出了更多条件。你可以使用 `[-a]` 或一个空格对两个条件进行逻辑 AND，使用 `-o` 进行逻辑 OR。注意，左括号 `\(` 或右括号 `\)` 前后以及 `-o` 前后至少需要一个空格。复杂的表达式可以用括号 `\(` 和 `\)` 括起来。我们现在讨论一些示例。

find 命令最常见的用法是搜索一个或多个目录中的文件，如第一个示例所示。这里，该命令在你的主目录中搜索 USA.gif 和 Pakistan.gif 文件，并显示包含它们的目录的路径名。如果被搜索的文件出现在多个目录中，则显示所有目录的路径名。

```
$ find ~ \( -name USA.gif -o -name Pakistan.gif \) -print
/home/sarwar/myweb/USA.html
/home/sarwar/myweb/Pakistan.html
$
```

以下命令显示你的主目录中以 .c 和 .C 结尾的所有文件的绝对路径名。

```
$ find ~ \( -name '*.c' -o -name '*.C' \) -print
...
$
```

下一个命令递归搜索 /usr/include 目录中名为 socket.h 的文件，并打印该文件的绝对路径名。
