

```
exit_on_signal_SIGINT () {
    echo "Script interrupted." 2>&1
    exit 0
}

exit_on_signal_SIGTERM () {
    echo "Script terminated." 2>&1
    exit 0
}

trap exit_on_signal_SIGINT SIGINT
trap exit_on_signal_SIGTERM SIGTERM

for i in {1..5}; do
    echo "Iteration $i of 5"
    sleep 5
done
```

该脚本包含两个 trap 命令，每个信号各一个。每个 trap 反过来指定一个 shell 函数，在接收到特定信号时执行该函数。请注意，每个信号处理函数中都包含 exit 命令。如果没有 exit，脚本在完成函数后会继续执行。

当用户在执行此脚本期间按下 CTRL-C 时，结果如下所示：

```
[me@linuxbox ~]$ trap-demo2
Iteration 1 of 5
Iteration 2 of 5
^CScript interrupted.
```

## 临时文件

脚本中包含信号处理程序的一个原因是为了删除脚本在执行期间可能创建的用于保存中间结果的临时文件。命名临时文件有一定的技巧。传统上，类 Unix 系统上的程序会在 /tmp 目录中创建临时文件，/tmp 是一个用于此类文件的共享目录。然而，由于该目录是共享的，这会带来一定的安全问题，特别是对于以超级用户权限运行的程序。除了为系统所有用户公开的文件设置适当的权限这一显而易见的步骤外，给临时文件一个不可预测的文件名也很重要。这可以避免一种称为 *temp race attack* 的攻击。一种创建不可预测但仍具描述性的名称的方法是这样做：

```
tempfile=/tmp/$(basename $0).$$.$RANDOM
```

这将创建一个由程序名称、其进程 ID（PID）以及一个随机整数组成的文件名。需要注意的是，`$RANDOM` shell 变量返回的值仅在 1–32767 范围内，在计算机术语中这不是一个很大的范围，因此变量的单个实例不足以抵御有决心的攻击者。

更好的方法是使用 `mktemp` 程序（不要与 `mktemp` 标准库函数混淆）来命名并创建临时文件。`mktemp` 程序接受一个用作构建文件名的模板作为参数。模板应包含一系列 x 字符，它们将被相应数量的随机字母和数字替换。x 字符序列越长，随机字符序列就越长。以下是一个示例：

```
tempfile=$(mktemp /tmp/foobar.$$.XXXXXXXXXX)
```

这会创建一个临时文件并将其名称赋给变量 `tempfile`。模板中的 x 字符会被随机字母和数字替换，因此最终的文件名（在此示例中，还包括特殊参数 `$$` 的展开值以获得 PID）可能类似于这样：

```
/tmp/foobar.6593.UOZuvM6654
```

对于由普通用户执行的脚本，避免使用 */tmp* 目录并在用户的主目录内创建临时文件目录可能是明智的，使用如下代码行：

```
[[ -d $HOME/tmp ]] || mkdir $HOME/tmp
```

## 使用 wait 进行异步执行

有时希望同时执行多个任务。我们已经看到所有现代操作系统至少是多任务的，如果不是多用户的话。脚本可以构建成多任务行为。

通常这涉及启动一个脚本，该脚本反过来启动一个或多个子脚本以执行额外任务，同时父脚本继续运行。然而，当一系列脚本以这种方式运行时，保持父进程和子进程协调可能会出现问题。也就是说，如果父进程或子进程依赖于对方，并且一个脚本必须等待另一个脚本完成其任务后才能完成自己的任务，该怎么办？

bash 有一个内置命令可以帮助管理此类异步执行。wait 命令会导致父脚本暂停，直到指定的进程（即子脚本）完成为止。为了演示这一点，我们需要两个脚本。第一个是父脚本。

```
#!/bin/bash

# async-parent: Asynchronous execution demo (parent)

echo "Parent: starting..."

echo "Parent: launching child script..."
async-child &
pid=$!
echo "Parent: child (PID= $pid) launched."

echo "Parent: continuing..."
sleep 2

echo "Parent: pausing to wait for child to finish..."
wait "$pid"
```

