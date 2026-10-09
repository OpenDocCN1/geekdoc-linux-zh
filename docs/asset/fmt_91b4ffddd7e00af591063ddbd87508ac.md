
前面的示例与早期的示例`d & e & f`不同，后者的任务`a`和`b`是顺序启动的，而不是并发启动的。同样，以下命令行在后台顺序执行`a`和`b`，同时顺序执行`c`和`d`。运行`a`和`b`的子壳与运行`c`和`d`的子壳并发运行。`shell`立即显示提示符。

```
(a ; b) & (c ; d)
```

`[1] 15528`

`[2] 15529`

## shell 基础

下一个命令将一个目录复制到另一个目录。第二对括号创建一个子壳来运行管道后面的命令。由于这些括号，尽管中间插入了命令，第一个命令的输出对第二个命令仍然可用。如果没有这些括号，第一个命令的输出将发送到`cd`并丢失，因为`cd`不处理标准输入。变量`$1`和`$2`代表第一个和第二个命令参数（第 95 页）。第一对括号创建一个子壳来运行前两个命令，允许使用户使用相对路径调用`cd`。如果没有它们，第一个命令将更改工作目录（随之也会影响第二个命令）。有了它们，`shell`的工作目录就会被改变。

```
$ cd

$ $1 ; tar -cf .. ) | (cd $2 ; tar -xvf -)

$ ./home/max/sources /home/max/memo

```

`cd`命令复制文件和目录。此`shell`操作几乎同于使用带有`-r`选项的`cp`。信息请参考`cp`和`tar`页面。

### 作业控制

作业是一个命令管道。每当你向`shell`提供一个命令时，你就运行了一个简单作业。例如，如果你在命令行上输入`date`并按回车，你就运行了一个作业。你还可以在单行中创建多个包含多个命令的多个作业：

```
$ find | sort | lpr & grep /tmp/* > max &

[1] 18839

[2] 18876

```

命令行中到`&`之前的部分处理通过管道连接的内容：`find`、`sort`（第 154 页）和`lpr`（第 151 页）。第二个作业是一个运行`grep`的单个进程。末尾的`&`字符将每个作业放入后台，因此`bash`在显示提示符之前不需要等待它们完成。使用`job`你可以将命令从前台移动到后台（反之亦然），临时停止命令，并列出所有正在后台运行或停止的命令。

## jobs：列出作业

内置`jobs`列出所有后台作业。随后，`sleep`命令在后台运行创建一个`jobs`报告的后台作业：

```
$ sleep 60 &

[1] 7809

$ jobs

[1] + Running sleep 60 &

```

## 将作业调回前台

`shell`为后台运行的每个命令分配作业编号。对于每个在后台运行的作业，`shell`在发布提示符之前立即列出作业编号和`PID`号：

```
$ xclock &

[1] 1246

$ date &

[2] 1247

$ Tue Dec 2 11:44:40 PST 2008

$ [2]+ date

$ find /usr-ace -print > findout &

[2] 1269

$ jobs

[1]- Running xclock &

[2]+ Running find /usr-ace -print > findout

```

作业编号在作业完成后会被丢弃，可以重用。当你启动或将作业放入后台时，`shell`分配的作业编号比当前使用的最高作业编号大`1`。在前面的示例中，`jobs`命令将第一个作业`xclock`列为作业`1`。`date`命令没有出现在`jobs`列表中，因为它在运行`jobs`之前已经完成了。由于`date`命令在运行`find`之前已完成，前台命令变为作业`2`。

要将作业移动到前台，使用`fg`内置命令，或者你可以提供百分号（`%`）后跟作业编号作为命令。以下任一命令都可以将作业`2`移动到前台。当你将作业移动到前台时，`shell`会显示它正在前台执行的命令。

```
$ fg 2

find /usr-ace -print > findout

```

```
$ % 2

find /usr-ace -print > findout

```

你也可以通过在百分号后跟一个唯一标识启动作业的命令行开头的字符串来引用作业。与其使用前面的命令，你可以使用`fg %find`或`fg %f`，因为这两者都能唯一标识作业`2`。如果你在百分号后跟一个问号和一个字符串，则该字符串可以匹配命令行的任何部分。在前面的示例中，`fg %?`也能将作业调回前台。通常情况下，你希望调回前台的作业是唯一带有（`+`）标记的运行作业。

## 挂起作业

按下挂起键（通常是`CONTROL-Z`）会立即挂起（临时停止）前台作业并显示消息。

```
CONTROL-Z

[2]+ Stopped find /usr-ace -print > findout

```

更多信息请参阅第 241 页的“将作业从前台移动到后台”。

## bg：将作业发送后台

要将前台作业移动到后台，必须必须挂起作业（如上）。然后可以使用`bg`内置命令在后台恢复作业的执行。

```
$ bg

[2]+ find /usr-ace -print &

```

如果后台作业尝试从终端读取内容，`shell`会停止程序并显示作业已停止的消息。你必须将该作业移动到前台以便其从终端读取。

```
$(sleep 5; cat >mytext) &

[1] 1343

$ date

Tue Dec 2 11:58:20 PST 2008

[1]+ Stopped (sleep 5; cat >mytext )

$ fg

(sleep 5; cat >mytext )

Remember to let the cat out!

CONTROL-D

$

```

![](img/7decc2e43bc591b4d8cc4d0cd9fb2ae8_345_0.png)

图 9-2 Shell 中的目录结构

如果你在有作业停止时尝试退出`shell`，`shell`会发出警告并不允许你退出。此时，如果你使用`jobs`命令查看作业列表，或者立即再次尝试退出`shell`，`shell`就会允许你退出。如果没有设置`hupexit`（第 339 页）（默认值），则停止的作业和后台作业将继续后台运行。如果设置了该选项，`shell`将终止这些作业。

## 操作目录栈

Bourne Again Shell (`Bash`) 允许你存储一个正在操作的目录列表，以便你轻松地在它们之间移动。这个列表被称为栈（`stack`）。它类似于一叠叠盘子：你通常从栈的顶部添加和移除盘子，因此这种类型的栈被로“后进先出”（LIFO）栈。

## dirs：显示栈

`dirs`内置命令显示目录栈的内容。如果你在目录栈为空时调用`dirs`，它会显示工作目录的名称：

```bash
dirs

~/literature
```

![](img/7decc2e43bc591b4d8cc4d0cd9fb2ae8_345_1.png)

图 9-3 创建目录栈

![](img/7decc2e43bc591b4d8cc4d0cd9fb2ae8_346_0.png)

图 9-4 使用 pushhd 更改工作目录

`dirs`内置命令使用波浪号（`~`）表示用户主目录的名称。接几章节中的示例假设你指的是图 9-2 中的目录结构。

## pushhd：将目录推入栈中

当你向`pushhd`（`push directory`）内置命令提供一个参数时，它会将参数指定的目录推入栈中，切换到指定的目录，并显示栈。下面的示例如图 9-3 所示：

```bash
$ pushhd ../demo

~/literature

$ pwd

/home/sam/demo

$ pushhd ../names

~/names ~demo ~/

$ pwd

/home/sam/names

```

当你不带参数使用`pushhd`时，它会交换栈顶部的两个目录，将新的顶部目录（原来的第二个目录）变为新的工作目录，并显示栈（图 9-4）：

```bash
$ pushhd

~/names ~/literature

$ pwd

/home/sam/demo

```

通过这样使用`pushhd`，你可以轻松地在两个目录之间来移动。你也可以使用`cd -`切换到上一个目录，无论你是否显式地创建了目录栈。要访问栈中的另一个目录，请在`pushhd`前加上一个数字参数。栈中的目录从顶部目录开始编号，顶部目录为`0`。接下来的`pushhd`命令继续上一个示例，将工作目录更改为`literature`并将`literature`移动到栈顶部：

```bash
$ pushhd +2

~/literature ~demo ~/names

$ pwd

/home/sam/literature

```

![](img/7decc2e43bc591b4d8cc4d0cd9fb2ae8_347_0.png)

图 9-5 使用 popd 从栈中移除目录

## popd：从栈中弹出目录

要从栈中移除目录，请使用`popd`（`pop directory`）内置命令。如下例和图 9-5 所示，不带参数时，`popd`从栈中移除目录并将工作目录更改为新目录：

```bash
$ dirs

~/literature ~names

$ popd

~/demo ~names

$ pwd

/home/sam/demo

```

要移除栈中除顶部以外的目录，请使用带加号的数字参数调用`popd`。移除`0`号目录不会更改工作目录。

```bash
$ dirs

~/literature ~names

$ popd +1

~/literature ~names

```

## 参数与变量

在`shell`中，一个参数（`parameter`）关联一个值，该值对用户可见。有多种类型的参数。由字母、数字和下划线组成的参数通常被称为`shell`变量。变量名必须以字母或下划线开头，不能以数字开头。因此`A76`、`MY_CAT`和`____`是有效的变量名，而`69TH_STREET`（以数字开头）和`MY-NAME`（包含连字符）则不是。

你命名并赋值的`shell`变量是用户创建变量。你可以随时更改用户创建变量的值，或将其设置为只读（`readonly`）以便无法更改值。你还可以将用户创建变量设为全局。全局变量（也称为环境变量）对所有的`shell`以及从它派生的其他程序可用。一种命名约定是全局变量仅使用大写字母，其他变量使用大小写混合的字母。请参见“变量的局部性”。

在`bash shell`中为变量赋值，使用以下语法：

```bash
VARIABLE=value
```

下面的示例显示了如何显示变量的值：

```bash
$ person=max

$ echo person

person

$ echo $person

max

```

`echo`内置命令将其参数复制到标准输出，因此你可以用它显示变量的值。上一个示例的第二行显示`person`并不代表`max`。相反，显示的是字符串`person`。只有当你在变量名前加上美元符号（`$`）时，`shell`才会替换变量的值。因此，命令`echo $person`显示变量`person`的值；它没有显示`person`，因为`shell`没有将`person`作为参数传递给`echo`。由于有开头的`$`，`shell`识别出`$person`是一个变量，替换变量的值并将该值传递给`echo`。`echo`内置命令显示变量的值而不是它的名称，永远“不知道”你调用的是变量。

引用`$`：你可以通过对开头的`$`符号加引号来防止`shell`替换变量的值。双引号不能防止替换；可以使用单引号或反斜杠（`\`）。

```bash
$ echo $person

max

$ echo "$person"

max

$ echo '$person'

$person

$ echo \$person

$person

```

## 参数与变量

空格（`SPACES`）：由于双引号不会阻止变量替换，但会关闭大多数其他字符的特殊含义，因此在给变量赋值以及使用这些值时，双引号是非常有用的。若要将包含空格或制表符（`TABS`）的值赋值给变量，请在变量周围使用双引号。虽然在所有情况下都不强制要求双引号，但使用它们是一个好习惯。

```
$ person="max and zach"

$ echo $person

max and zach

$ person=max and zach

bash: and command not found

```

当你引用一个包含制表符或多个连续空格的值的变量时，你需要使用引号来保留间距。如果你不对变量加引号，`shell`在将变量传递给实用程序之前，会将每个空白字符字符串折叠为单个空格：

```
$ person="max zach"

$ echo $person

max zach

$ echo "$person"

max and zach

```

赋值中的路径名扩展：当你执行变量作为参数的命令时，`shell`会将变量名替换为变量的值，并将该值传递给正在执行的程序。如果变量的值包含特殊字符（例如`*`或`?`），`shell`可能会扩展该变量。

以下命令序列中的第一行将字符串`max*`赋值给变量`memo`。Bourne Again Shell 不扩展该字符串，因为`bash`在给变量赋值时不会执行路径名扩展（第 242 页）。所有的`shell`都按照特定的顺序处理命令行。在这个顺序中，`bash`扩展变量，双引号引用了`memo`扩展值中的星号（`*`），并防止`bash`在将值传递给`echo`命令之前对扩展后的`memo`变量执行路径名扩展：

```
$ memo=max*

$ echo "$memo"

max*

```

当你引用一个包含未引号特殊字符的变量时，所有的`shell`都将该字符解释为特殊字符。在下面的示例中，`shell`扩展了`memo`变量的值，因为它没有引号：

```
$ echo $memo

max.report

max.summary

$ echo $memo

max.report max.summary

```

在这里，`shell`将变量`memo`扩展为`max*`，将`max*`扩展为`max.report`和`max.summary`，并将这两个值传递给`echo`。

大括号`$VARIABLE`语法是更通用的语法`${VARIABLE}`的特例，其中变量名被`{}`包围。大括号将变量名与相邻的字符隔离开。在将变量值与字符串拼接时，大括号是必要的：

```
$ PRE=counter

$ WAY=$PREFClock

$ FAKE=$PREFFeit

$ echo WAY $FAKE

```

上述示例并未按运行。只输出了一个空行，因为虽然`PREclockwise`和`PREfeit`符号是有效的变量名，但它们并没有被设置。默认情况下，`bash`将未设置的变量评估为空（`null`）字符串并显示该值。要实现这些语句的意图，请使用大括号引用`PRE`变量：

```
$ PRE=counter

$ WAY=${PRE}clockwise

$ FAKE=${PRE}feit

$ echo WAY $FAKE counterfeit

```

Bourne Again Shell 通过位置引用其命令行上的参数，使用特殊变量`$1`、`$2`、`$3`等到`$9`。如果你想引用第九个参数之后的参数，必须使用大括号：`${10}`。命令名称存储在`$0`中（第 953 页）。

## unset：移除变量

除非你删除变量，否则只要创建它的`shell`存在，它就会存在。要删除变量的值而不是变量本身，请给变量赋值一个空值：

```
$ person=

$ echo $person

```

你可以使用`unset`内置命令删除变量。以下命令删除了变量：

```
$ unset person

```

## 变量属性

本节讨论了属性并解释了如何将它们分配给变量。

## readonly：使变量值永久

你可以使用`readonly`内置命令确保变量的值不能被更改。下一个示例将变量`person`声明为只读。你必须在声明为只读之前给变量赋值；声明后不能更改它的值。当你尝试`unset`或更改只读变量的值时，`shell`会显示错误信息：

```
$ person=zach

$ echo $person

zach

$ readonly person

$ person=helen

bash: person: readonly variable

```

如果你不带参数使用`readonly`内置命令，它会列出所有只读`shell`变量。此列表包含了自动设置为只读的关键字变量，以及你声明为只读的关键字或用户创建的变量。参见第 302 页。

## typeset：将属性分配给变量

`readonly`和`export`内置分别是命令`declare -r`和`-x`的同义词。你可以声明一个变量而不为其赋值，使其对所有子`shell`可用（即变为全局变量）。在对变量赋值之前，它的值为空值。

表 3 变量属性 (typeset 或 declare)

| 属性 | 含义 |
| :--- | :--- |
| `-a` | 将变量声明为数组（第 946 页） |
| `-f` | 将变量声明为函数（第 333 页） |
| `-i` | 将变量声明为整数类型（第 302 页） |
| `-r` | 使变量变为只读；也可用 `readonly`（第 301 页） |
| `-x` | 导出变量（使其全局化）；也可用 `export`（第 948 页） |

以下命令声明了变量并设置属性。第一行声明了`person1`并赋值为`max`。无论是否带有`declare`单词，该命令的效果相同。

```
$ declare person1=max

$ declare -r person2=zach

$ declare -rx person3=helen

$ declare -x person4

```

你可以以任何顺序列出`declare`选项。以下是等效的

```
$ declare -x-person3=halen
```
