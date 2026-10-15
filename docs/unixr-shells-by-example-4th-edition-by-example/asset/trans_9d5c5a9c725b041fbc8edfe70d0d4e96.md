

```
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
```

## EXAMPLE 4.19

```
% grep '\<north' datafile
northwest NW Charles Main 3.0 .98 3 34
northeast NE AM Main Jr. 5.1 .94 3 13
north NO Margot Weber 4.5 .89 5 9
```

## EXPLANATION

打印所有包含以 north 开头的单词的行。\< 是单词开始的锚点。

## EXAMPLE 4.20

```
% grep '\<north\>' datafile
north NO Margot Weber 4.5 .89 5 9
```

## EXPLANATION

如果包含单词 north 则打印该行。\< 是单词开始的锚点，\> 是单词结束的锚点。

## EXAMPLE 4.21

```
% grep '\<[a-z].*n\' datafile
northwest NW Charles Main 3.0 .98 3 34
western WE Sharon Gray 5.3 .97 5 23
southern SO Suan Chin 5.1 .95 4 15
eastern EA TB Savage 4.4 .84 5 20
northeast NE AM Main Jr. 5.1 .94 3 13
central CT Ann Stephens 5.7 .94 5 13
```

## EXPLANATION

打印所有包含以小写字母开头的单词、后跟任意数量字符、并以 n 结尾的单词的行。请注意 . 符号。它的意思是任意字符，包括空白字符。

## 4.3 grep 的选项

grep 命令有许多控制其行为的选项。并非所有版本的 UNIX 都支持完全相同的选项，因此请务必查阅你的手册页以获取完整列表。

以下 datafile 用于本节的示例，为方便起见会定期重复。

| % cat datafile | | | | | | |
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

## EXAMPLE 4.22

```
% grep -n 'south' datafile
3:southwest    SW    Lewis Dalsass    2.7    .8    2    18
4:southern     SO    Suan Chin        5.1    .95   4    15
5:southeast    SE    Patricia Hemenway 4.0    .7    4    17
```

## EXPLANATION

-n 选项在每一行前加上找到该模式的行号，然后是该行。

## EXAMPLE 4.23

```
% grep -i 'pat' datafile
southeast    SE    Patricia Hemenway 4.0    .7    4    17
```

## EXPLANATION

-i 选项关闭大小写敏感。表达式 pat 中的字母无论是大写还是小写组合都不重要。

```
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
```

## EXAMPLE 4.24

```
% grep -v 'Suan Chin' datafile
northwest NW Charles Main 3.0 .98 3 34
western WE Sharon Gray 5.3 .97 5 23
southwest SW Lewis Dalsass 2.7 .8 2 18
southeast SE Patricia Hemenway 4.0 .7 4 17
eastern EA TB Savage 4.4 .84 5 20
northeast NE AM Main Jr. 5.1 .94 3 13
north NO Margot Weber 4.5 .89 5 9
central CT Ann Stephens 5.7 .94 5 13
```

## EXPLANATION

这里，-v 选项打印所有不包含模式 Suan Chin 的行。此选项用于从输入文件中删除特定条目时。要真正删除该条目，你需要将 grep 的输出重定向到临时文件，然后将临时文件的名称改回原始文件的名称，如下所示：

```
grep -v 'Suan Chin' datafile > temp
mv temp datafile
```

请记住，在从 datafile 重定向输出时必须使用临时文件。如果你将 datafile 重定向到 datafile，shell 会“破坏”datafile。 （参见第 25 页的“重定向”。）

## EXAMPLE 4.25

```
% grep -l 'SE' .
datafile
datebook
```

## EXPLANATION

-l 选项使 grep 只打印找到该模式的文件名，而不是文本行。

