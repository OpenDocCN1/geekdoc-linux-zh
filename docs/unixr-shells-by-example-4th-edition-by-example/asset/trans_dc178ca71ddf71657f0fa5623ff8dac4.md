

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

## 示例 6.191

```
% nawk '{if ($2 =~ /5/) {print ; exit 0}}' datafile
southwest SW Chris Foster 2.7 .8 2 18

% echo $status (csh) or echo $? (sh or ksh)
0
```

## 说明

如果第二个字段包含5，则打印该记录并且awk程序退出。C shell的状态变量包含退出值。如果使用Bourne或Korn shell，则$?变量包含退出状态。

## 6.2.6 用户自定义函数

## 示例 6.192

```
(The Command Line)
% cat nawk.sc7
1 BEGIN{largest=0}
2 {maximum=max($5)}

3 function max ( num ) {
4   if ( num > largest) {largest=num}
5   return largest
6 }
6 END{ print "The maximum is " maximum "."}

% nawk -f nawk.sc7 datafile
The maximum is 5.7.
```

## 说明

- 1. 在BEGIN块中，用户自定义变量largest被初始化为0。
- 2. 对于文件中的每一行，变量maximum被赋值为函数max返回的值。函数max以$5作为其参数。
- 3. 定义用户自定义函数max。函数语句用花括号括起来。每次从输入文件datafile读取新记录时，都将调用函数max。
- 4. 它将比较num和largest中的值，并返回两个数中较大的一个。
- 5. 函数定义块结束。
- 6. END块打印maximum中的最终值。

## 6.26.7 awk/gawk 命令行选项

Awk有许多命令行选项。Gawk有两种命令行选项格式：GNU长格式，以双破折号（--）加单词开头；以及传统的短POSIX格式，由一个破折号和一个字母组成。Gawk特有的选项通过-W选项或其对应的长选项来使用。提供给长选项的任何参数要么用=号连接（中间没有空格），要么在下一个命令行参数中提供。gawk的--help选项（参见示例6.193）列出了所有gawk选项。参见表6.15。

## 示例 6.193

```
% awk --help
Usage: awk [POSIX or GNU style options] -F progfile [--] file ...
      awk [POSIX or GNU style options] [--] 'program' file ...
POSIX options:          GNU long options:
  -f progfile           --file=progfile
  -F fs                 --field-separator=fs
  -v var=val            --assign=var=val
  -m[f|r] val
  -W compat             --compat
  -W copyleft            --copyleft
  -W copyright           --copyright
  -W help                --help
  -W lint                --lint
  -W lint-old            --lint-old
  -W posix               --posix
  -W re-interval         --re-interval
  -W source-program-text --source=program-text
  -W traditional         --traditional
  -W usage               --usage
  -W version             --version
```

## 示例 6.193（续）

> 请将bug报告发送至bug-gnu-utils@prep.ai.mit.edu,\n并且抄送arnold@gnu.ai.mit.edu

**表6.15** *awk* 命令行选项

| 选项 | 含义 |
|---|---|
| `-F fs`,<br>`--field-separator fs` | 指定输入字段分隔符，其中fs可以是字符串或正则表达式；例如，`FS=";"`或`FS="\t"`。 |
| `-v var=value`,<br>`--assign var=value` | 在awk脚本开始执行之前，将值赋给用户自定义变量var。可用于BEGIN块。 |
| `-f scriptfile`,<br>`--file scriptfile` | 从脚本文件读取awk命令。 |
| `-mf nnn`,<br>`-mr nnn` | 将内存限制设置为nnn的值。使用`-mf`选项时，将字段的最大数量限制为nnn；使用`-mr`选项时，设置记录的最大数量。不适用于awk。 |
| `-W traditional`,<br>`-W compat`,<br>`--traditional`,<br>`--compat` | 以兼容模式运行，使gawk的行为与UNIX版本的awk完全一致。所有gawk扩展都被忽略。两种模式作用相同；`--traditional`是首选。 |
| `-W copyleft`,<br>`-W copyright`,<br>`--copyleft` | 打印版权信息的简要版本。 |
| `-W help`,<br>`-W usage`,<br>`--help`,<br>`--usage` | 打印可用的awk选项及其功能的简短摘要。 |
| `-W lint`,<br>`--lint` | 打印关于使用可能无法移植到传统UNIX awk版本的构造的警告。 |
| `-W lint-old`,<br>`--lint-old` | 提供关于无法移植到原始UNIX实现版本的构造的警告。 |
| `-W posix`,<br>`--posix` | 打开兼容模式。不识别`\x`转义序列、不识别当FS被赋值为单个空格时将换行符作为字段分隔符、不识别函数关键字`func`、不识别用运算符`&&`和`||`替换`^`和`^=`，以及fflush。 |
| `-W re-interval`,<br>`--re-interval` | 允许使用间隔正则表达式（参见第176页的“POSIX字符类”）；即括号表达式，如`a{1alpha}`。 |

