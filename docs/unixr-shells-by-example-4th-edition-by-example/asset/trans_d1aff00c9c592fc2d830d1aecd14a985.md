

# 示例 6.42

```
nawk '$5 ~ /\.[7-9]/' datafile
southwest  SW  Chris Foster  2.7  .8  2  18
central    CT  Sheri Watson  5.7  .94 5  13
```

# 解释

如果第五个字段 ($5) 包含一个字面量的句点，后跟一个或多个介于 7 到 9 之间的数字，则记录会被打印。

# 示例 6.43

```
nawk '$2 !~ /E/{print $1, $2}' datafile
northwest NW
southwest SW
southern SO
north NO
central CT
```

# 解释

如果第二个字段不包含模式 E，则打印第一个字段后跟第二个字段 ($1, $2)。

# 示例 6.44

```
nawk '$3 ~ /Joel/{print $3 " is a nice guy."}' datafile
Joel is a nice guy.
```

# 解释

如果第三个字段 ($3) 以模式 Joel 开头，则打印第三个字段后跟字符串 is a nice guy.。请注意，如果要打印字符串，则其中包含一个空格。

# 示例 6.45

```
nawk '$8 ~ /[0-9][0-9]$/{print $8}' datafile
23
18
15
17
20
13
13
```

# 解释

如果第八个字段 ($8) 以两位数字结尾，则会被打印。

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

# 示例 6.46

```
nawk '$4 ~ /Chin/{print "The price is $" $8 "."}' datafile
The price is $15.
```

# 解释

如果第四个字段 ($4) 以 Chin 结尾，则打印用双引号括起来的字符串 ("The price is $")、第八个字段 ($8) 以及包含句点的字符串。

# 示例 6.47

```
nawk '/TJ/{print $0}' datafile
northeast NE TJ Nichols 5.1 .94 3 13
```

# 解释

如果记录包含模式 TJ，则打印 $0（记录）。

# 6.10.4 输入字段分隔符

使用以下 datafile2 作为示例 6.48 至 6.52。

```
% cat datafile2
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

# 示例 6.48

```
nawk '{print $1}' datafile2
Joel
Sharon
Chris
May
Derek
Susan
TJ
Val
Sheri
```

# 解释

默认输入字段分隔符为空白。打印第一个字段 ($1)。

# 示例 6.49

```
nawk -F: '{print $1}' datafile2
Joel Craig
Sharon Kelly
Chris Foster
<more output here>
Val Shultz
Sheri Watson
```

# 解释

-F 选项指定冒号作为输入字段分隔符。打印第一个字段 ($1)。

# 示例 6.50

```
nawk '{print "Number of fields: "NF}' datafile2
Number of fields: 2
Number of fields: 2
Number of fields: 2
<more of the same output here>
Number of fields: 2
Number of fields: 2
```

# 解释

因为字段分隔符是默认值（空白），每个记录的字段数为 2。唯一的空格在名和姓之间。

# 示例 6.51

```
nawk -F: '{print "Number of fields: "NF}' datafile2
Number of fields: 7
Number of fields: 7
Number of fields: 7
<more of the same output here>
Number of fields: 7
Number of fields: 7
```

# 解释

因为字段分隔符是冒号，每个记录中的字段数为 7。

# 示例 6.52

```
nawk -F'[ :]' '{print $1, $2}' datafile2
Joel Craig northwest
Sharon Kelly western
Chris Foster southwest
May Chin southern
Derek Johnson southeast
Susan Beal eastern
TJ Nichols northeast
Val Shultz north
Sheri Watson central
```

# 解释

可以使用 nawk 以正则表达式的形式指定多个字段分隔符。空格或冒号将被指定为字段分隔符。打印第一个和第二个字段 ($1, $2)。（方括号必须加引号以防止 shell 将其解释为 shell 元字符。）

# 6.10.5 awk 脚本编写

以下 datafile 用于下一个示例。

| % cat datafile | | | | | | |
|---|---|---|---|---|---|---|
| northwest | NW | Joel Craig | 3.0 | .98 | 3 | 4 |
| western | WE | Sharon Kelly | 5.3 | .97 | 5 | 23 |
| southwest | SW | Chris Foster | 2.7 | .8 | 2 | 18 |
| southern | SO | May Chin | 5.1 | .95 | 4 | 15 |
| southeast | SE | Derek Johnson | 4.0 | .7 | 4 | 17 |
| eastern | EA | Susan Beal | 4.4 | .84 | 5 | 20 |
| northeast | NE | TJ Nichols | 5.1 | .94 | 3 | 13 |
| north | NO | Val Shultz | 4.5 | .89 | 5 | 9 |
| central | CT | Sheri Watson | 5.7 | .94 | 5 | 13 |

