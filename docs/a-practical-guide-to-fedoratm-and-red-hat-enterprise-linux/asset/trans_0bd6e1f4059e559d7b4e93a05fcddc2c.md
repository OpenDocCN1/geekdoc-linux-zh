
## 挂起作业

按下挂起键（通常是 CONTROL-2）会立即挂起（临时停止）前台作业，并显示包含 *Stopped*（已停止）一词的消息。

```
CONTROL-2
[2]+ Stopped            find /usr -name ace -print > findout
```

有关更多信息，请参阅第 164 页的“将作业从前景移动到后台”。

### bg: 将作业发送到后台

要将前台作业移动到后台，您必须先挂起该作业（如上所述）。然后，您可以使用 bg 内置命令在后台恢复该作业的执行。

```
$ bg
[2]+ find /usr -name ace -print > findout &
```

如果后台作业试图从终端读取，shell 会停止该作业，并显示一条消息，说明该作业已停止。然后，您必须将该作业移至前台，以便它可以读取终端。

```
$ ( sleep 5; cat mytext ) &
[1] 1343
$ date
Sat Dec 7 11:58:20 PST 2013
[1]+ Stopped            ( sleep 5; cat mytext )
$ fg
( sleep 5; cat mytext )
*Remember to let the cat out!*
CONTROL-D
$
```

在上面的示例中，shell 在后台作业一开始就显示其作业编号和 PID 编号，随后是一个提示符。为了说明此时您可以输入命令，用户输入了 date 命令，其输出出现在屏幕上。Shell 等待到即将发出提示符之前（在 date 命令完成后）通知您作业 1 已停止。当您输入 fg 命令时，shell 将该作业放入前台，您可以输入该命令等待的数据。在这种情况下，输入需要使用 CONTROL-D 终止，这会向 cat 发送 EOF（文件结束）信号。然后，shell 显示另一个提示符。

Shell 会让您了解作业状态的变化，并在后台作业启动、完成或停止时通知您，可能是因为它在等待来自终端的输入。Shell 还会让您了解前台作业被挂起的情况。由于关于在后台运行的作业的通知可能会干扰您的工作，因此 shell 会延迟显示这些通知，直到即将显示提示符之前。您可以设置 **notify**（第 402 页）以使 shell 立即显示这些通知。

如果尝试在非登录 shell 中 *exit*（退出），而此时有作业已停止，shell 会发出警告并不允许您 *exit*。然后，如果您使用 **jobs** 查看作业列表，或者再次立即尝试从 shell *exit*，shell 将允许您 *exit*。如果未设置 **huponexit**（第 402 页）（默认情况下未设置），已停止的作业将保持停止状态，后台作业将继续在后台运行。如果已设置，shell 将终止这些作业。

## 操作目录堆栈

Bourne Again Shell 允许您存储正在使用的目录列表，以便您可以在它们之间轻松移动。此列表被称为*堆栈*（stack）。它类似于一摞餐盘：通常将盘子添加到堆栈顶部，并从堆栈顶部取走盘子，因此这种类型的堆栈被称为 LIFO（后进先出）堆栈。

### dirs: 显示堆栈

**dirs** 内置命令显示目录堆栈的内容。如果在目录堆栈为空时调用 **dirs**，它将显示*工作*目录的名称：

```
$ dirs
~/literature
```

**dirs** 内置命令使用波浪号（~）来表示用户主目录的名称。下一节中的示例假设您指的是图 9-2 中显示的目录结构。

![](img/243613168ac865b539f12460d966088e_405_0.png)

**图 9-2** 示例中使用的目录结构

### pushd: 将目录推入堆栈

当您提供 pushd（push directory）内置命令一个参数时，它会将参数指定的目录推入堆栈，更改目录到指定目录，并显示堆栈。下面的示例如图 9-3 所示：

```
$ pushd ../demo
~/demo ~/literature
$ pwd
/home/sam/demo
$ pushd ../names
~/names ~/demo ~/literature
$ pwd
/home/sam/names
```

当您不带参数调用 pushd 时，它会交换堆栈顶部的两个目录，使新的顶层目录（即第二个目录）成为新的工作目录，并显示堆栈（图 9-4）。

```
$ pushd
~/demo ~/names ~/literature
$ pwd
/home/sam/demo
```

![](img/243613168ac865b539f12460d966088e_406_1.png)

![](img/243613168ac865b539f12460d966088e_407_0.png)

图 9-5 使用 popd 从堆栈中移除目录

以这种方式使用 pushd，您可以轻松地在两个目录之间来回移动。您也可以使用 cd - 更改到上一个目录，无论您是否显式创建了目录堆栈。要访问堆栈中的另一个目录，请调用 pushd 并传入前面带有加号的数字参数。堆栈中的目录从顶层目录（编号为 0）开始编号。下面的 pushd 命令延续之前的示例，将工作目录更改为 literature，并将 literature 移动到堆栈顶部：

```
$ pushd +2
~/literature ~/demo ~/names
$ pwd
/home/sam/literature
```

### popd: 从堆栈中弹出目录

要从堆栈中移除目录，请使用 popd（pop directory）内置命令。如下面的示例和图 9-5 所示，不带参数时，popd 会从堆栈中移除顶层目录，并将工作目录更改为新的顶层目录：

```
$ dirs
~/literature ~/demo ~/names
$ popd
~/demo ~/names
$ pwd
/home/sam/demo
```

要从堆栈中移除除顶层以外的目录，请使用前面带有加号的数字参数调用 popd。下面的示例移除了编号为 1 的目录，即 demo。移除编号不为 0 的目录不会更改工作目录。

```
$ dirs
~/literature ~/demo ~/names
$ popd +1
~/literature ~/names
```

## 参数和变量

Shell 参数：在 shell 中，shell 参数关联着您或 shell 脚本可以访问的值。本节介绍了以下类型的 shell 参数：用户创建的变量、关键字变量、位置参数和特殊参数。

- 变量：名称由字母、数字和下划线组成的参数称为变量。变量名必须以字母或下划线开头，不能以数字开头。因此 A76、MY_CAT 和 X__ 是有效的变量名，而 69TH_STREET（以数字开头）和 MY-NAME（包含连字符）则不是。
- 用户创建的变量：您命名并赋值给它们的变量是用户创建的变量。您可以随时更改用户创建变量的值，或者使它们只读，以便其值不能被更改。
- Shell 变量和环境变量：默认情况下，变量仅在创建它的 shell 中可用（即局部变量）；这种类型的变量称为 shell 变量。您可以使用 export 使变量在由创建它的 shell 生成的 shell 中可用（即全局变量）；这种类型的变量称为环境变量。一种命名惯例是对 shell 变量使用混合大小写或小写字母，而对环境变量仅使用大写字母。有关 shell 变量和环境变量的更多信息，请参阅第 1031 页的“Variables”。

要在 bash 中声明和初始化变量，请使用以下语法：

```
VARIABLE=value
```

等号（=）的两侧不能有空格。示例如下：

```
$ myvar=abc
```

为脚本声明和初始化变量：Bourne Again Shell 允许您将变量赋值放在命令行的开头。这种类型的赋值将变量放入命令 shell 的环境中——也就是说，该变量仅由命令运行的程序（以及程序的子进程）可访问。它不能从运行命令的 shell 访问。my_script shell 脚本显示 TEMPDIR 的值。以下命令在 TEMPDIR 设置为 /home/sam/temp 的情况下运行 my_script。echo 内置命令表明，在运行 my_script 后，交互式 shell 没有 TEMPDIR 的值。如果 TEMPDIR 已在交互式 shell 中设置，以这种方式运行 my_script 将不会对其值产生任何影响。

```
$ cat my_script
echo $TEMPDIR
$ TEMPDIR=/home/sam/temp ./my_script
/home/sam/temp
$ echo $TEMPDIR
$ 
```

