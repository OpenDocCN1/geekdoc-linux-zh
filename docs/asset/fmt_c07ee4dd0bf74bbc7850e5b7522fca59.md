
`% nawk 'NR==1{print length($1)}' datafile`

```
9
```

# 解释

如果这是第一条记录，则打印第一个字段中的长度（字符数）。

# 示例 6.176

`% nawk 'NR==1{print index($1,"west")}' datafile`

```
6
```

# 解释

如果这是第一条记录，则打印第一个字段中子字符串 `west` 首次出现的位置。字符串 `west` 从第六个位置（索引）开始出现在字符串 `northwest` 中。

以下 `datafile2` 用于示例 6.179。

`% cat datafile2`

```
Joel Craig:northwest:NW:3.0:.98:3:4
Sharon Kelly:western:WE:5.3:.97:5:23
Chris Foster:southwest:SW:2.7:.8:2:18
May Chin:southern:SO:5.1:.95:4:15
Derek Johnson:southeast:SE:4.0:.7:4:17
Susan Beal:eastern:EA:4.4:.84:5:20
TJ Nichols:northeast:NE:5.1:.94:3:13
Val Shultz:north:NO:4.5:.89:5:9
Sheri Watson:central:CT:5.7:.94:5:13
```

# 示例 6.179

`% awk -F: '/north/{split($1, name, " ");\nprint "First name: " name[1];\nprint "Last name: " name[2];\nprint "\n----------------"}' datafile2`

```
First name: Joel
Last name: Craig
----------------
First name: TJ
Last name: Nichols
----------------
First name: Val
Last name: Shultz
----------------
```

# 解释

输入字段分隔符设置为冒号（`-F:`）。如果记录包含正则表达式 `north`，则第一个字段被拆分为名为 `name` 的数组，其中空格为分隔符。数组的元素被打印。

## 6.26.2 使用 gawk 的时间函数

`gawk` 提供了两个用于获取时间和格式化时间戳的函数：`systime` 和 `strftime`。

### systime 函数

`systime` 函数返回自 1970 年 1 月 1 日（称为 Epoch）以来，非闰年秒数表示的当天时间。

#### 格式

```
systime()
```

#### 示例 6.182

`% awk 'BEGIN{now=systime(); print now}'`

```
939515282
```

#### 解释

`systime` 函数的返回值被赋给用户定义的变量 `now`。该值是自 1970 年 1 月 1 日以来，非闰年秒数表示的当天时间。

### strftime 函数

`strftime` 函数使用 C 库 `strftime` 函数格式化时间。格式规范的形式为 `%T`、`%D` 等（参见表 6.14）。时间戳的形式与 `systime` 的返回值相同。如果省略时间戳，则默认使用当前时间。

#### 表 6.14 日期和时间格式规范

| 日期格式 | 定义 |
|---|---|
| 对于以下定义，假设当前日期和时间如下：日期：2004 年 10 月 17 日星期日 时间：15:26:26 PDT |
| `%a` | 星期几的缩写名称（Sun） |
| `%A` | 星期几的全称（Sunday） |
| `%b` | 月份的缩写名称（Oct） |
| `%B` | 月份的全称（October） |
| `%c` | 区域设置的日期和时间（Sun Oct 17 15:26:46 2004） |
| `%d` | 十进制表示的月份中的天数（17） |
| `%D` | 日期格式为 10/17/04 |
| `%e` | 月份中的天数，如果只有一位则用空格填充 |

#### 解释

`strftime` 函数根据作为参数提供的格式说明来格式化时间和日期。（参见表 6.14。）如果 `systime` 作为第二个参数给出或根本没有给出参数，则假定为此区域设置的当前时间。如果给出第二个参数，则它必须与 `systime` 函数的返回值格式相同。

下一节中的示例使用以下数据文件 `database`，为方便起见会定期重复。

| `% cat datafile` |   |   |   |   |   |   |
| --- | --- | --- | --- | --- | --- | --- |
| northwest | NW | Joel Craig | 3.0 | .98 | 3 | 4 |
| western | WE | Sharon Kelly | 5.3 | .97 | 5 | 23 |
| southwest | SW | Chris Foster | 2.7 | .8 | 2 | 18 |
| southern | SO | May Chin | 5.1 | .95 | 4 | 15 |
| southeast | SE | Derek Johnson | 4.0 | .7 | 4 | 17 |
| eastern | EA | Susan Beal | 4.4 | .84 | 5 | 20 |
| northeast | NE | TJ Nichols | 5.1 | .94 | 3 | 13 |
| north | NO | Val Shultz | 4.5 | .89 | 5 | 9 |
| central | CT | Sheri Watson | 5.7 | .94 | 5 | 13 |

## 6.26.3 命令行参数

### 示例 6.184

`% cat argv$.sc`

```
# Testing command-line arguments with ARGV and ARGC using a for loop.
BEGIN{
    for(i=0;i < ARGC;i++)
        printf("argv[%d] is %s\n", i, ARGV[i])
        printf("The number of arguments, ARGC=%d\n", ARGC)
}
```

`% nawk -f argv$.sc datafile`

```
argv[0] is nawk
argv[1] is datafile
The number of arguments, ARGC=2
```

#### 解释

`BEGIN` 块包含一个 `for` 循环来处理命令行参数。`ARGC` 是参数的数量，`ARGV` 是一个包含实际参数的数组。`Awk` 不将选项计为参数。在此示例中，唯一有效参数是 `nawk` 命令和输入文件 `datafile`。

`% cat datafile`

```
northwest NW Joel Craig 3.0 .98 3 4
western WE Sharon Kelly 5.3 .97 5 23
southwest SW Chris Foster 2.7 .8 2 18
southern SO May Chin 5.1 .95 4 15
southeast SE Derek Johnson 4.0 .7 4 17
eastern EA Susan Beal 4.4 .84 5 20
northeast NE TJ Nichols 5.1 .94 3 13
north NO Val Shultz 4.5 .89 5 9
central CT Sheri Watson 5.7 .94 5 13
```

### 示例 6.185

```
1 % nawk 'BEGIN{name=ARGV[1];}
$0 ~ name {print $3, $4}' "Derek" datafile
nawk: can't open Derek
source line number 1
2 % nawk 'BEGIN{name=ARGV[1]; delete ARGV[1];}
$0 ~ name {print $3, $4}' "Derek" datafile
Derek Johnson
```

#### 解释

- **1.** 名称 `"Derek"` 在 `BEGIN` 块中被赋给变量 `name`。在模式-动作块中，`nawk` 尝试将 `"Derek"` 作为输入文件打开并失败。
- **2.** 将 `"Derek"` 赋给变量 `name` 后，`ARGV[1]` 被删除。开始模式-动作块时，`nawk` 不会尝试将 `"Derek"` 作为输入文件打开，而是改为打开 `datafile`。

## 6.26.4 读取输入 (getline)

### 示例 6.186

`% nawk 'BEGIN{ "date" | getline d; print d }' datafile`

```
Mon Jan 15 11:24:24 PST 2004
```
