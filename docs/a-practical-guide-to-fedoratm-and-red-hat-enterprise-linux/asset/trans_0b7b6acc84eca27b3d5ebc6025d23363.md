
# 环境、环境变量与继承

本节解释命令执行环境和继承的概念。

## 环境

当 Linux 内核调用一个程序时，内核会向该程序传递一个由字符串数组组成的列表。这个列表被称为*命令执行环境*，或简称为*环境*，它以*名称*=*值*的形式保存一系列名称-值对。

### 1.1.1 环境变量

当*bash*被调用时，它会扫描其环境并为每个名称-值对创建参数，将对应的*值*分配给每个*名称*。这些参数中的每一个都是*环境变量*；这些变量位于 shell 的环境中。环境变量有时也被称为*全局变量*或*导出变量*。

继承。子进程（子 shell；有关进程结构的更多信息请参见第 373 页）从其父进程继承其环境。继承的变量是子进程的环境变量，因此其子进程也会继承该变量：所有后代进程，无论层级多少，都会从其祖先继承环境变量。进程可以创建、删除环境变量并改变其值，因此子进程继承的环境可能与其父进程继承的环境不同。

由于进程的局部性（见下文），父进程无法看到子进程对环境变量所做的更改，一旦子进程被生成（创建），子进程也无法看到父进程对环境变量所做的更改。此外，互不相关的进程也无法看到各自进程中同名变量（例如通常继承的环境变量，如*PATH*）的更改。

### 进程局部性：SHELL 变量

变量是*局部的*，这意味着它们是特定于某个进程的：*局部意味着局部于某个进程*。例如，当你在终端登录或打开终端模拟器时，你会启动一个运行 shell 的进程。假设在该 shell 中，*LANG* 环境变量（第 368 页）被设置为 en_US.UTF-8。

如果你随后在另一个终端登录或打开第二个终端模拟器，你会启动另一个运行不同 shell 的进程。假设在该 shell 中，*LANG* 环境变量也被设置为 en_US.UTF-8。当你在第二个终端上将 *LANG* 的值更改为 de_DE.UTF-8 时，第一个终端上的 *LANG* 值不会改变。之所以不会改变，是因为变量（包括名称和值）局部于某个进程，且每个终端都在运行一个独立的进程（即使两个进程都在运行 shell）。

### 1.1.2 EXPORT：将变量放入环境中

当你运行 *export* 命令（*declare* -x 的同义词；第 357 页）并将变量名作为参数时，shell 会将这些变量的名称（以及值，如果存在）放入环境中。如果没有参数，*export* 会列出环境（导出）变量。

以下 **extest1** shell 脚本将 **american** 的值赋给名为 *cheese* 的变量，然后显示其名称（shell 会将 `$0` 扩展为调用程序的名称）和 *cheese* 的值。**extest1** 脚本随后调用 **subtest**，后者尝试显示相同的信息，通过初始化声明一个 *cheese* 变量，显示该变量的值，并将控制权返回给正在执行 **extest1** 的父进程。最后，**extest1** 再次显示原始 *cheese* 变量的值。

```shell
$ cat extest1
cheese=american
echo "$0 1: $cheese"
./subtest
echo "$0 2: $cheese"

$ cat subtest
echo "$0 1: $cheese"
cheese=swiss
echo "$0 2: $cheese"

$ ./extest1
./extest1 1: american
./subtest 1:
./subtest 2: swiss
./extest1 2: american
```

**subtest** 脚本从未从 **extest1** 接收 *cheese* 的值（并且 **extest1** 从未丢失该值）；*cheese* 是一个 shell 变量，而不是环境变量（它不在父进程的环境中，因此在子进程中不可用）。当一个进程试图显示一个未声明且不在环境中的变量的值时，就像 **subtest** 的情况那样，该进程什么也不显示；未声明变量的值是空字符串。最后的 `echo` 显示 **extest1** 中 *cheese* 的值没有改变：在 **bash** 中——与现实世界不同——子进程永远无法影响其父进程的属性。

**extest2** 脚本与 **extest1** 相同，除了它使用 `export` 将 *cheese* 放入当前进程的环境中。结果是 *cheese* 出现在运行 **subtest** 脚本的子进程的环境中。

```shell
$ cat extest2
export cheese=american
echo "$0 1: $cheese"
./subtest
echo "$0 2: $cheese"

$ ./extest2
./extest2 1: american
./subtest 1: american
./subtest 2: swiss
./extest2 2: american
```

在这里，子进程继承 **cheese** 的值为 **american**，并在显示该值后，将*其副本*更改为 **swiss**。当控制权返回给父进程时，父进程的 **cheese** 副本保留其原始值：**american**。

或者，如下面的程序所示，你可以将一个变量放入子 shell 的环境中，而无需在父 shell 中声明它。有关此命令行语法的更多信息，请参见第 148 页。

```shell
$ cheese=cheddar ./substest
./substest 1: cheddar
./substest 2: swiss
$ echo $cheese
$
```

你可以在不赋值或赋值之前导出一个变量。此外，更改已导出变量的值后，你不需要再次导出该变量。例如，当你通常在 ~/.bash_profile 中为其赋值时，通常不需要 **export PATH**，因为它通常在全局启动文件中被导出。

你可以在同一行放置多个 **export** 声明（初始化）：

```shell
$ export cheese=swiss coffee=colombian avocados=us
```

**export -n** 或 **declare +x** 命令会移除指定环境变量的导出属性（取消导出变量），将其降级为 shell 变量，同时保留其值。

**export -f** 命令将指定的函数（第 396 页）放入环境中，使其对子进程可用。

## printentv：显示环境变量名称和值

**printentv** 实用程序显示环境变量的名称和值。当不带参数调用时，它显示所有环境变量。当带有环境变量名称调用时，它显示该变量的值。当带有不在环境中或尚未声明的变量名称调用时，它什么也不显示。你也可以使用 **export**（第 1032 页）和 **env**（下一页）来显示环境变量列表。

```shell
$ x=5                  # 不在环境中
$ export y=10          # 在环境中
$ printentv x
$ printentv y
10
$ printentv
...
SHELL=/bin/bash
TERM=xterm
USER=sam
PWD=/home/sam
y=10
...
```

## LPI env：在修改的环境中运行程序

**env** 实用程序作为当前 shell 的子进程运行一个程序，允许你修改当前 shell 导出到新创建进程的环境。有关将变量放入子进程环境中的更简单方法，请参见第 148 页。**env** 实用程序的语法如下：

```shell
env [options] [-| name=value] ... [command-line]
```

其中 *options* 是以下选项之一：

- –ignore-environment
- –i 或 –
- 使 *command-line* 在干净的环境中运行；新创建的进程无法使用任何环境变量。
- –unset=name –u *name*
- 取消设置名为 *name* 的环境变量，使其对新创建的进程不可用。

就像在 **bash** 命令行（第 148 页）上一样，可以使用*零*个或多个 *name=value* 对来设置或修改新创建进程中的环境变量，除了你不能在没有 *value* 的情况下指定 *name*。**env** 实用程序从左到右评估 *name=value* 对，因此如果 *name* 在此列表中出现了多次，最右侧的 *value* 优先。

*command-line* 是 **env** 执行的命令（包括任何选项和参数）。**env** 实用程序将第一个不包含等号的参数作为命令行的开始，并且，如果你指定一个不包含斜杠的命令（即，如果你指定一个简单的文件名），则使用 **PATH**（第 359 页）的值来定位该命令。它不适用于内置命令。

在下面的示例中，**env** 运行 **display_xx**，这是一个显示 **xx** 变量值的脚本。在命令行上，**env** 在其调用的脚本的环境中将变量 **xx** 初始化为特定值，而脚本中的 **echo** 显示 **xx** 的值。

```shell
$ cat display_xx
echo "Running $0"
echo $xx

$ env xx=remember ./display_xx
Running ./display_xx
remember
```

如果你只想为程序声明环境变量，使用以下 **bash** 语法（第 148 页）会更简单：

```shell
$ xx=remember ./display_xx
Running ./display_xx
remember
```

