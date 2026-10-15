

使用以下 datafile2 作为示例 6.112 和 6.113。

```
% cat datafile2
Joel Craig:northwest:NW:3.0:.98:3:4
Sharon Kelly:western:WE:5.3:.97:5:23
Chris Foster:southwest:SW:2.7:.8:2:18
May Chin:southern:SO:5.1:.95:4:15
Derek Johnson:southeast:SE:4.0:.7:4:17
Susan Beal:eastern:EA:4.4:.84:5:20
TJ Nichols:northeast:NE:5.1:.94:3:13
Val Schultz:north:NO:4.5:.89:5:9
Sheri Watson:central:CT:5.7:.94:5:13
```

## 示例 6.112

```
% awk -F: 'NR == 5{print NF}' datafile2
7
```

## 解释

字段分隔符在命令行中通过 -F 选项设置为冒号。如果记录的编号（NR）为 5，则打印字段数（NF）。

## 示例 6.113

```
% awk 'BEGIN{OFMT="%.2f";print 1.23456789,12E-2}' datafile2
1.25 0.12
```

## 解释

OFMT，即 print 函数的输出格式变量，被设置为使浮点数以小数点后两位精度打印。数字 1.23456789 和 12E-2 以新格式打印。

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

## 示例 6.114

```
% nawk '{$9 = $6 * $7; print $9}' datafile
2.94
4.85
1.6
3.8
2.8
4.2
2.82
4.45
4.7
```

## 解释

第六个字段（$6）和第七个字段（$7）相乘的结果存储在新的字段 $9 中并打印。原来有八个字段；现在有九个。

## 示例 6.115

```
% nawk '{$10 = 100; print NF, $9, $0}' datafile
10 northwest NW Joel Craig 3.0 .98 3 4 100
10 western WE Sharon Kelly 5.3 .97 5 23 100
10 southwest SW Chris Foster 2.7 .8 2 18 100
10 southern SO May Chin 5.1 .95 4 15 100
10 southeast SE Derek Johnson 4.0 .7 4 17 100
10 eastern EA Susan Beal 4.4 .84 5 20 100
10 northeast NE TJ Nichols 5.1 .94 3 13 100
10 north NO Val Shultz 4.5 .89 5 9 100
10 central CT Sheri Watson 5.7 .94 5 13 100
```

## 解释

为每个记录分配一个第十个字段（$10）为 100。这是新字段。第九个字段（$9）不存在，因此将被视为空字段。打印字段数（NF），随后是 $9 的值、空字段以及整个记录（$0）。第十个字段的值为 100。

以下 datafile2 用于示例 6.118。

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

## 示例 6.118

```
% awk 'BEGIN {FS=";";OFS="\t"} /Sharon/{print $1, $2, $8}' datafile2
Sharon Kelly	western	28
```

## 解释

BEGIN 动作块用于初始化变量。FS 变量（字段分隔符）被赋值为冒号。OFS 变量（输出字段分隔符）被赋值为制表符（\t）。在处理完 BEGIN 动作块后，awk 打开 datafile2 并开始从文件中读取输入。如果记录以正则表达式 Sharon 开头，则打印第一个、第二个和第八个字段（$1、$2、$8）。输出中的每个字段都由制表符分隔。

### 6.16.4  END 模式

以下 datafile 用于示例 6.119 和 6.120。

```
% cat datafile
northwest    NW    Joel Craig       3.0    .98    3    4
western      WE    Sharon Kelly     5.3    .97    5    23
southwest    SW    Chris Foster     2.7    .8     2    18
southern     SO    May Chin         5.1    .95    4    15
southeast    SE    Derek Johnson    4.0    .7     4    17
eastern      EA    Susan Beal       4.4    .84    5    20
northeast    NE    TJ Nichols       5.1    .94    3    13
north        NO    Val Shultz       4.5    .89    5    9
central      CT    Sheri Watson     5.7    .94    5    13
```

