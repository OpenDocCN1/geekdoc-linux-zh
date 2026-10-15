

## 解释

strftime 函数根据作为参数提供的格式说明来格式化时间和日期。（参见表 6.14。）如果 systime 作为第二个参数给出或根本没有给出参数，则假定为此区域设置的当前时间。如果给出第二个参数，则它必须与 systime 函数的返回值格式相同。

下一节中的示例使用以下数据文件 database，为方便起见会定期重复。

| % cat datafile |   |   |   |   |   |   |
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

```
% cat argv$.sc
# Testing command-line arguments with ARGV and ARGC using a for loop.

BEGIN{
    for(i=0;i < ARGC;i++)
        printf("argv[%d] is %s\n", i, ARGV[i])
        printf("The number of arguments, ARGC=%d\n", ARGC)
}

% nawk -f argv$.sc datafile
argv[0] is nawk
argv[1] is datafile
The number of arguments, ARGC=2
```

### 解释

BEGIN 块包含一个 for 循环来处理命令行参数。ARGC 是参数的数量，ARGV 是一个包含实际参数的数组。Awk 不将选项计为参数。在此示例中，唯一有效参数是 nawk 命令和输入文件 datafile。

```
% cat datafile
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

### 解释

- **1.** 名称 "Derek" 在 BEGIN 块中被赋给变量 `name`。在模式-动作块中，nawk 尝试将 "Derek" 作为输入文件打开并失败。
- **2.** 将 "Derek" 赋给变量 `name` 后，`ARGV[1]` 被删除。开始模式-动作块时，nawk 不会尝试将 "Derek" 作为输入文件打开，而是改为打开 `datafile`。

## 6.26.4 读取输入 (getline)

### 示例 6.186

```
% nawk 'BEGIN{ "date" | getline d; print d }' datafile
Mon Jan 15 11:24:24 PST 2004
```

### 解释

UNIX/Linux date 命令通过管道传递给 getline 函数。结果存储在变量 d 中并打印。

### 示例 6.187

```
% nawk 'BEGIN{ "date" | getline d; split( d, mon ); print mon[2] }' datafile
Jan
```

### 解释

UNIX/Linux date 命令通过管道传递给 getline 函数，结果存储在 d 中。split 函数将字符串 d 拆分为名为 mon 的数组。打印该数组的第二个元素。

### 示例 6.188

```
% nawk 'BEGIN{ printf "Who are you looking for? "; getline name < "/dev/tty" }'
```

### 解释

输入从终端 /dev/tty 读取并存储在名为 name 的变量中。

### 示例 6.189

```
% nawk 'BEGIN{ while (getline < "/etc/passwd" > 0) lc++; print lc }' datafile
16
```

### 解释

while 循环用于一次一行地遍历 /etc/passwd 文件。每次进入循环时，getline 读取一行并递增变量 lc 的值。循环退出时，lc 的值被打印（即 /etc/passwd 文件中的行数）。只要 getline 的返回值不是 0（即已读取一行），循环就会继续。

## 6.26.5 控制函数

### 示例 6.190

```
% nawk '{if ($5 >= 4.5) next; print $1}' datafile
northwest
southwest
southeast
eastern
north
```

### 解释

如果第五个字段大于或等于 4.5，则从输入文件 datafile 读取下一行，并从 awk 脚本开头开始处理（BEGIN 块之后）。否则，打印第一个字段。
