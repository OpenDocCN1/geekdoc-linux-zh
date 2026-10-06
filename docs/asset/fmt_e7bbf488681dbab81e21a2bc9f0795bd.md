
Linux `grep` 选项的完整列表出现在本章节末尾的参考部分。

## 定位文件

`locate` 命令查询数据库并返回包含一组字符的所有路径名列表，类似于固定字符串匹配的 `grep`。

```bash
$ locate /orders.txt

/home/kburtch/test/orders.txt

/home/kburtch/orders.

$ locate orders.txt

/home/kburtch/test/orders.txt

/home/kburtch/test/advocacy/old_orders.txt

/home/kburtch/orders.txt
```

旧版本的 `locate` 会显示系统上的任何文件，即使是你通常没有访问权限的文件。

`locate` 数据库由一个名为 `updatedb` 的命令维护。Linux 发行版通常每天执行一次。因此，`locate` 速度非常快，但对于查找至少有一天以前的文件非常有用。

## 查找文件

`find` 命令搜索符合特定条件的名称或文件，例如特定文件名大于特定大小的文件。`find` 类似于下面的循环，其中 `MATCH` 是匹配标准：

```bash
ls -recursive | while read FILE; do
  # 测试文件是否匹配
  if [ $MATCH ]; then
    printf "%s\n" "$FILE"
  fi
done
```

该脚本递归地搜索当前目录下的目录，寻找符合名为 `MATCH` 条件的文件名。

## 查找文件 211

`find` 比这个脚本片段强大得多。与内置的 `test` 命令一样，`find` 选项可以创建描述要查找文件属性的表达式。还有选项可以改变 `find` 的整体行为，以及其他用于指定在匹配成功时要执行的操作的选项。

基础匹配是 `-name`，它指定要查找的文件名。`name` 可以是特定的文件名，也可以包含如 `*` 和 `?` 这样的路径通配符。如果使用模式匹配，则必须将模式括在引号中，以防止 `shell` 在 `find` 命令执行之前对其进行扩展。

```bash
$ find -name "*.txt"
./orders.txt
./advocacy/linux.txt
./advocacy/old_orders.txt
```

第一个参数是开始搜索的目录。在这种情况下，它是当前目录。之前的 `find` 命令匹配任何类型的文件，包括作为管道的文件或目录，这在用户输入中并不常见。`-type` 选项将文件限制为特定类型。`-type f` 匹配普通文件，这是最常见的搜索类型。类型也可以是 `b`（块设备）、`c`（字符设备）、`d`（目录）、`p`（管道）、`l`（符号链接）或 `s`（套接字）。

```bash
$ find -name "*.txt" -type f
./orders.txt
./advocacy/linux.txt
./archive/old_orders.txt
```

选项 `-name *.txt -type f` 是 `find` 表达式的一个示例。这些选项匹配同时符合这两个条件的文件（隐含的逻辑“与”）。还有其他运算符选项用于将条件组合成逻辑表达式，如下：

- `-` `expr`—强制先测试括号中的选项
- `-not expr`（或 `! expr`）—确保选项不匹配
- `expr -and expr`（或 `expr -a expr`）—默认行为；查找同时匹配两组选项的文件
- `expr -or expr`（或 `expr -o expr`）—逻辑“或”。查找匹配其中一组选项的文件
- `expr ,`—始终检查两组选项，但使用其中一组的结果来判断匹配

例如，要统计普通文件和目录的数量，可以这样操作：

```bash
$ find -type d -o -type f | wc -l
224
```

也可以统计不带 `.txt` 后缀的文件数量。

```bash
$ find ! -name "*.txt" -type f | wc -l
185
```

括号必须用反斜杠或引号进行转义，以防止 Bash 将其解释为子壳。使用括号可以表示以 `.txt` 或 `.sh` 结尾的文件数量：

```bash
$ find -name "*.txt" -or name "*.sh" -type f | wc -l
11
```

某些表达式选项引用时间的测量。在历史上，`find` 时间以天为单位，但 GNU 版本为选项增加了分钟。`find` 查找的是精确匹配。

要查找超过某个时间的文件，请包含加号或减号。如果加号 `+` 在时间值之前，`find` 查找大于该值的时间。如果减号 `-` 在时间值之前，`find` 查找小于该值的时间。加号和减号零标记是不一样的：天数的 `+0` 表示“没有更旧”，换句话说，就是一天或更久的文件。同样，分钟的 `-5` 表示“小于 5 分钟”或“0 到 4 分钟”。

有几个选项可以测试访问时间，即文件被读取或写入的时间。`-atime` 选项检查文件是否在最近被访问，`-atime` 后的数字是文件被访问的天数。`-amin` 检查分钟分钟的访问时间。

同样，你可以用 `-ctime`、`-ctmin` 检查更改时间。`ctime` 表示文件创建的时间。你可以用 `-mtime`、`-mmin` 检查修改时间，即文件写入的时间。

查找在一天内更改的文件：

```bash
$ find -name "*.txt" -type f -ctime +0
./archive/orders.txt
```

查找在 10 分钟内访问的文件：

```bash
$ find -name "*.txt" -type f -amin -10
./advocacy/linux.txt
```

`-size` 选项测试文件的大小。单位可以是 `b`（字节）、`c`（字符）、`k`（千字节）或 `M`（兆字节）。与时间选项一样，减号 `-` 测试较小的，加号 `+` 测试较大的。

## 查找文件 213

例如，使用此命令查找大于 1MB 的文件：

```bash
$ find -type f -name "*.log" -size +1M
./logs/giant.log
```

`find` 将路径输出到标准输出。历史上，必须使用 `-print` 选项。大多数 Unix 系统包括 Linux 默认如此。如果考虑兼容性，请在 `find` 末尾添加 `-print`。

要在匹配成功时执行不同的操作，请使用 `-exec`。`-exec` 选项对每个文件运行程序。这通常与 `rm` 结合以删除文件，或与 `grep` 结合以测试它们是否包含模式。文件名通过一对大括号 `{}` 插入命令，并以转义的分号 `\;` 结束。如果没有转义，`shell` 将其解释为 `find` 命令的结束。

```bash
$ find -type f -name "*.txt" -exec grep {} \;
```

`find exec` 可用于每个匹配项执行。当你可以选择将结果管道到第二个命令时，执行速度会比使用 `-exec` 快得多。管道通过两个命令生成结果，而不是成百上千个命令。

`-ok` 选项的作用与 `-exec` ，只需它会交互式地验证是否运行命令。

```bash
$ find -type f -name "*.txt" -ok rm {} \;
< rm ../orders.txt ? n
< rm ../advocacy/linux.txt ? n
< rm ../advocacy/old_orders.txt ? n
```

`-ls` 操作带有更详细的信息列出匹配的文件。`find` 对每个匹配的文件运行 `ls -dils`。

```bash
$ find -type f -name "*.txt"*
243300 4 -rw-rw-r- 1 kburtch kbch 592 May 17 14:41 ./orders.txt
114683 0 -rw-rw-r- 1 kburtch kbch 0 May 17 14:41 ./advocacy/
```

## 第 12 章文本文件处理

```
linux.txt
114684 4 -rw-rw-r- 1 kburtch kburtch 592 May 17 14:41 ./advocacy/old_orders.txt
```

`printf` 选项可以类似于 `stat` 命令的搜索版本。`%` 代码表示要打印文件的什么类型信息。其中许多代码与 `stat` 提供相同的功能，但使用了不同的代码。

- `a`-以 C `time` 函数返回的格式的文件最后访问时间。
- `c`-以 C `time` 函数返回的格式的文件状态更改时间。
- `f`-去除了前导目录的文件名（仅保留最后一个元素）。
- `g`-文件的组名，如果该组没有名称，则显示数字组 ID。
- `h`-文件名的前导目录（除最后一个元素外的所有部分）。
- `i`-文件的 inode 节点（十进制）。
- `m`-文件的权限位（八进制）。
- `p`-文件的路径。
- `q`-带有删除该文件的命令行参数名称的路径。
- `s`-以字节为单位的文件大小。
- `t`-以 C `time` 函数返回的格式的文件最后修改时间。
- `u`-文件的用户名，如果用户没有名称，则显示数字用户 ID。

完整列表出现在参考部分。
时间代码也与 `stat` 不同：`stat` 记住上一种时间类型，而 `printf` 则要求为每个打印的时间都指定时间类型。

```bash
$ find -type f -name "*.txt" -printf "%q access time is %a\n"
orders.txt access time is Thu May 17 16:47:08 2001
linux.txt access time is Thu May 17 16:47:08 2001
old_orders.txt access time is Thu May 17 16:47:08 2001
$ find -type f -name "*.txt" -printf "%T modified time as %T\nhours:minutes is %TH:%TM:%TN\n"
orders.txt modified time as hours:minutes is 14:41
linux.txt modified time as hours:minutes is 14:41
old_orders.txt modified time as hours:minutes is 14:41
```

`find` 选项的完整列表出现在参考部分。

## 排序

Linux `sort` 对一个文件或一组文件进行排序。可以显式地或通过重定向标准输入进行排序。`sort` 的选项与 `grep` 或 `cut` 等命令完全不同。`sort` 是最后一批支持长格式选项的命令之一：因此，这里使用的是短选项。尽管如此，常用选项的名称与其他 Linux 命令并不相同。

要正确地排序文件，`sort` 命令需要知道排序键，即决定每行顺序的字符。键中的任何内容在排序时都会被忽略。默认情况下，整行被视为排序键。

```bash
$ sort -f orders.txt
Bar Stool,45.99,1,756
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Bunk Bed,705.99,1,757
Cedar Armoire,825.99,1,757
Cedar Toy Chest,65.99,1,757
Chair - Rocking,287.99,1,757
Garden Bench,149.99,1,757
Grandfather Clock,2045.99,1,756
Lawn Chair,55.99,1,756
Mahogany Writing Desk,463.99,1,756
Pine Round Table,375.99,1,756
Queen Bed,92.99,1,757
Reclining Chair,1599.99,1,756
Rocking Chair,287.99,1,756
Six-drawer Dresser,525.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Two-drawer Nightstand,1225.99,1,756
Victorian-style Sofa,1225.99,1,756
Walnut TV Stand,388.99,1,756
```

`-r`（反转）选项反转排序顺序。

```bash
$ head orders.txt | sort -f -r
Two-drawer Nightstand,1225.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Six-drawer Dresser,525.99,1,756
Reclining Chair,1599.99,1,756
Queen Bed,92.99,1,757
Pine Round Table,375.99,1,756
Cedar Toy Chest,65.99,1,757
Bunk Bed,705.99,1,757
Bookcase Oak Veneer,205.99,1,756
Birchwood China Hutch,475.99,1,756
```

如果仅将行的部分作为排序键，字段分隔符可以是任何空格或制表符，但你可以通过 `-t` 选项进行更改。要对第二个字段及后续字段的前 10 行进行排序，使用 `-k2`。

```bash
$ head orders.txt | sort -f -k2
Two-drawer Nightstand,1225.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Six-drawer Dresser,525.99,1,756
Reclining Chair,1599.99,1,756
Queen Bed,92.99,1,757
Pine Round Table,375.99,1,756
Cedar Toy Chest,65.99,1,757
Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
```

这里有许多影响如何解释键的选项。如果字段具有小数部分，它表示排序键开始的位置。第一个字符总是从行开始。例如，要忽略第一个字符，从第一个字段的第二个字符开始，使用 `-k1.2`。

```bash
$ head orders.txt | sort -f -k1.2
Reclining Chair,1599.99,1,757
Cedar Toy Chest,65.99,1,757
Round Table,375.99,1,757
Birchwood China Hutch,475.99,1,756
Six-drawer Dresser,525.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Bookcase Oak Veneer,205.99,1,756
Queen Bed,925.99,1,757
Bunk Bed,705.99,1,757
Two-drawer Nightstand,125.99,1,756
```

`-b`（空格）选项将键视为忽略前导空格的字符串。`-n`（数值）选项将键视为数字。`-g`（通用数字）选项将键视为 C 浮点数，允许无限大、NaN 和科学计数法。此选项比 `-n` 慢。数字选项始终适用于 `-b`。`-d`（数字）选项仅在排序键中使用字母和数字字符，忽略句号、连字符和其他标点符号。`-i`（忽略不可打印字符）选项仅在排序键中使用可打印字符。`-M`（月份）选项按月份缩写排序。

可以有多个排序键。可以通过在键末尾添加字符来应用于单个键，例如 `-k4,4M` 意味着“按包含月份第四字段排序”。`-r` 和 `-f` 选项也可以这样使用。

对于更复杂的示例，以下 `sort` 命令按账户号码进行反序排序，然后按产品名称排序。排序不区分大小且跳过前导空格：

```bash
$ head orders.txt | sort -t, -k4,4n -k1,1
Bunk Bed,705.99,1,757
Cedar Toy Chest,65.99,1,757
Pine Round Table,375.99,1,757
Queen Bed,925.99,1,757
Reclining Chair,1599.99,1,757
Six-drawer Dresser,525.99,1,757
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Boxcase Oak Veneer,205.99,1,756
```

对于长排序，`-c`（仅检查）选项在尝试排序文件之前检查它们是否需要排序。如果文件完成，则返回状态码 0。

`sort` 选项的完整列表出现在参考部分。

## 字符编辑 (tr)

Linux `tr`（翻译）命令替换或删除标准输入上的字符，并将结果写入标准输出。
`-d`（删除）选项用于删除特定字符。

```bash
$ printf "%s\n" 'The total is $234.45 US'
The total is $234.45 US
$ printf "%s\n" 'The total is $234.45 US ' | tr -d '$'
The total is 234.45 US
```

字符范围表示为第一个字符、一个减号和最后一个字符。

```bash
$ printf "%s\n" 'The total is $234.45 US ' | tr -d 'A-Z'
The total is 234.45
```

`tr` 支持 GNU 字符类。

```bash
$ printf "%s\n" 'The total is $234.45 US' | tr '[:upper:]'
The total is 234.45
```

在没有任何选项的情况下，`tr` 将一组字符映射到另一组。第一个参数中的字符更改为第二个参数中的字符。以此此类推。
