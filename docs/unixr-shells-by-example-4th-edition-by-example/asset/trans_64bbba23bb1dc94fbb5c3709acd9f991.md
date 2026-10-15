

| % cat datafile |  |  |  |  |  | |
|---|---|---|---|---|---|---|
| northwest | NW | Charles Main | 3.0 | .98 | 3 | 34 |
| western | WE | Sharon Gray | 5.3 | .97 | 5 | 23 |
| southwest | SW | Lewis Dalsass | 2.7 | .8 | 2 | 18 |
| southern | SO | Suan Chin | 5.1 | .95 | 4 | 15 |
| southeast | SE | Patricia Hemenway | 4.0 | .7 | 4 | 17 |
| eastern | EA | TB Savage | 4.4 | .84 | 5 | 20 |
| northeast | NE | AM Main Jr. | 5.1 | .94 | 3 | 13 |
| north | NO | Margot Weber | 4.5 | .89 | 5 | 9 |
| central | CT | Ann Stephens | 5.7 | .94 | 5 | 13 |

## 示例 5.10

```
% sed '3d' datafile
northwest    NW    Charles Main    3.0    .98    3    34
western      WE    Sharon Gray      5.3    .97    5    23
southern     SO    Suan Chin        5.1    .95    4    15
southeast    SE    Patricia Hemenway 4.0    .7     4    17
eastern      EA    TB Savage        4.4    .84    5    20
northeast    NE    AM Main Jr.      5.1    .94    3    13
north        NO    Margot Weber     4.5    .89    5    9
central      CT    Ann Stephens     5.7    .94    5    13
```

## 解释

删除第三行。默认情况下，所有其他行都会打印到屏幕上。

## 示例 5.11

```
% sed '3,$d' datafile
northwest    NW    Charles Main    3.0    .98    3    34
western      WE    Sharon Gray      5.3    .97    5    23
```

## 解释

从第三行到最后一行都被删除。美元符号（$）表示文件的最后一行。逗号称为范围运算符。剩余的行会被打印出来。在此示例中，地址范围从第 3 行开始，到最后一行结束，最后一行用美元符号（$）表示。

## 示例 3.12

```
% sed '$d' datafile
northwest    NW    Charles Main    3.0    .98    3    34
western      WE    Sharon Gray      5.3    .97    5    23
southwest    SW    Lewis Dalsass    2.7    .8     2    18
southern     SO    Suan Chin        5.1    .95    4    15
southeast    SE    Patricia Hemenway 4.0    .7     4    17
eastern      EA    TB Savage        4.4    .84    5    20
northeast    NE    AM Main Jr.      5.1    .94    3    13
north        NO    Margot Weber     4.5    .89    5    9
```

## 解释

删除最后一行。美元符号（$）表示最后一行。默认情况下，除了受 d 命令影响的行外，所有行都会被打印。

## 示例 3.13

```
% sed '/north/d' datafile
western      WE    Sharon Gray      5.3    .97    5    23
southwest    SW    Lewis Dalsass    2.7    .8     2    18
southern     SO    Suan Chin        5.1    .95    4    15
southeast    SE    Patricia Hemenway 4.0    .7     4    17
eastern      EA    TB Savage        4.4    .84    5    20
central      CT    Ann Stephens     5.7    .94    5    13
```

## 解释

删除所有包含模式 north 的行。剩余的行会被打印出来。

## 5.9.3 替换：s 命令

s 命令是替换命令。通过 sed 的 s 命令实现文件中文本的替换和修改。s 命令后正斜杠之间的文本是正则表达式，其右侧是替换文本。如果使用 g 标志，则可以在整行范围内进行全局替换。

% cat datafile
northwest NW Charles Main 3.0 .98 3 34
western WE Sharon Gray 5.3 .97 5 23
southwest SW Lewis Dalsass 2.7 .8 2 18
southern SO Suan Chin 5.1 .95 4 15
southeast SE Patricia Hemenway 4.0 .7 4 17
eastern EA TB Savage 4.4 .84 5 20
northeast NE AM Main Jr. 5.1 .94 3 13
north NO Margot Weber 4.5 .89 5 9
central CT Ann Stephens 5.7 .94 5 13

## 示例 5.14

```
% sed 's/west/north/g' datafile
northnorth NW Charles Main 3.0 .98 3 34
northern WE Sharon Gray 5.3 .97 5 23
southnorth SW Lewis Dalsass 2.7 .8 2 18
southern SO Suan Chin 5.1 .95 4 15
southeast SE Patricia Hemenway 4.0 .7 4 17
eastern EA TB Savage 4.4 .84 5 20
northeast NE AM Main Jr. 5.1 .94 3 13
north NO Margot Weber 4.5 .89 5 9
central CT Ann Stephens 5.7 .94 5 13
```

## 解释

s 命令用于替换。命令末尾的 g 标志表示替换在整行范围内是全局的；也就是说，如果找到多个 west 的出现，所有都会被替换为 north。如果没有 g 命令，则每行中 west 的第一次出现才会被替换为 north。

## 示例 5.15

```
% sed -n 's/^west/north/p' datafile
northern WE Sharon Gray 5.3 .97 5 23
```

## 解释

s 命令用于替换。-n 选项与命令末尾的 p 标志一起告诉 sed 仅打印发生替换的行；也就是说，如果在行首找到 west 并替换为 north，则只打印这些行。

