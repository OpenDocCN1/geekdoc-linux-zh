
# PARAMETERS AND VARIABLES

Shell variables were introduced on page 312. This section adds to the previous coverage with a discussion of array variables, global versus local variables, special and positional parameters, and expansion of null and unset variables.

# ARRAY VARIABLES

The Bourne Shell supports one-dimensional array variables. The subscripts are integers with zero-based indexing (i.e., the first element of the array has the subscript `(0)`). The following format declares and assigns values to an array:

```
name=(element1 element2 ...)
```

The following example assigns four values to the array:

```bash
$ NAMES=(max helen sam zach)
```

You reference a single element of an array as follows:

```
$ echo ${NAMES[2]}
```

The subscripts `[*]` and `[@]` both extract the entire array but work differently when used within double quotation marks. An `@` produces an array that is a duplicate of the original array; `*` produces a single element of an (or a plain variable) that holds all the elements of the array separated by the first character in `IFS` (normally a space). In the following example, the array `A` is filled with `NAMES` using `*`, and `B` is filled using `@`. The `declare` builtin uses the `-a` option displays the values of the array (and reminds you that bash uses zero-based indexing):

```
$ declare -a ${NAMES[0]}
$ declare -b ${NAMES[0]}
declare - A='${NAMES[0]=max helen sam zach'
declare - B='${[0]=max" [1]=helen" [2]=sam" [3]=zach"
declare -a NAMES='${*}=max" [1]=helen" [2]=sam" [3]=zach"
```

The same operator, when given the index of an array element instead of `*`, returns the length of that element:

```
$ echo ${NAMES[1]}
5
```

You can use a subscript on the left side of an assignment statement to replace a selected element in an array:

```
$ NAMES[1]-max
$ echo ${NAMES[@*]}
max max sum each
```

# 变量的局部性

默认情况下，变量对于声明它们所在的进程是局部的。因此，除非显式将变量设为全局，否则 shell 脚本无法访问你在登录 shell 中声明的变量。在 `bash` 中，`export` 使变量对子进程可见。

`export` 一旦你使用 `export` 并变量名作为参数，shell 会将变量的值放在子进程的调用环境中。这种按值传递为每个进程提供了一个变量的副本供其使用。

以下 `extent1` 脚本为名为 `cheese` 的变量赋值为 `american`，然后显示其文件名 (`extent1`) 和 `cheese` 的值。`extent1` 脚本声明了一个 `cheese` 变量并显示它的值。当 `subtest` 完成时，它会将控制权返回给正在执行 `extent1` 的父进程。此时，`extent1` 显示原始 `cheese` 变量的值。

```
$ cat extent1
cheese-american
subtest
echo extent1 1: "cheese"
echo extent1 2: "cheese"
$ cat subtest
echo subtest 1: "cheese"
cheese=swiss
echo subtest 2: "cheese"
$ extent1
extent1 1: american
subtest 1: swiss
subtest 2: swiss
extent1 2: american
```

`subtest` 脚本从未从 `extent1` 接收 `cheese` 的值，而 `extent1` 也从未丢失该值。在 `bash` 中——与现实世界不同——子进程永远影响其父进程的属性。当进程尝试显示未声明变量的值时（如 `subtest` 所示），进程不会显示任何内容；未声明变量的值为空字符串。

以下 `extend2` 脚本与 `extend1` 相同，但它使用 `export` 使 `cheese` 对 `subtest` 脚本可用：

在这里，子进程继承了 `cheese` 的值 `american`，并在显示该值后将其副本改为 `swiss`。当控制权返回父进程时，父进程的 `cheese` 副本保留了其原始值：`american`。

内置命令可以可选地包含赋值：

```
export cheese=american
```

上述语句等同于以下两个语句：

```
cheese=american
export cheese
```

虽然很少这样做，但你可以在赋值之前对变量进行导出。在更改其值后，你不需要对已经导出的变量再次导出。

# 函数

由于函数在调用它们的 shell 相同的环境中运行，变量在 shell 和其调用的函数之间是隐式共享的。

```
$ function name () {
echo $myname
myname=zach
}
```

# 参数与变量

Shell 变量是在第 312 页引入的。本节通过对数组变量、全局与局部变量、特殊和位置参数以及空变量和未设置变量的讨论，补充了之前的内容。

# 数组变量

Bourne Shell 支持一维数组变量。下标是从 0 开始的整数（即数组的第一个元素的下标为 `(0)`）。使用以下格式声明并为数组赋值：

```
name=(element1 element2 ...)
```

以下示例为数组分配了四个值：

```bash
$ NAMES=(max helen sam zach)
```

你通过以下方式引用数组的单个元素：

```
$ echo ${NAMES[2]}
```

下标 `[*]` 和 `[@]` 都能提取整个数组，但在双引号内使用时工作方式不同。`@` 产生原始数组的副本数组；`*` 产生一个单一元素（或普通变量），它包含由 `IFS` 中的第一个字符（通常是空格）分隔的数组所有元素。在接下来的示例中，数组 `A` 使用 `*` 填充 `NAMES`，而 `B` 则使用 `@` 填充。`declare` 内置命令使用 `-a` 选项显示数组的值（并提醒你 `bash` 使用从 0 开始的索引）：

```
$ declare -a ${NAMES[0]}
$ declare -b ${NAMES[0]}
declare - A='${NAMES[0]=max helen sam zach'
declare - B='${[0]=max" [1]=helen" [2]=sam" [3]=zach"
declare -a NAMES='${*}=max" [1]=helen" [2]=sam" [3]=zach"
```

同一个操作符，当给定数组元素的索引而非 `*` 时，它会返回该元素的长度：

```
$ echo ${NAMES[1]}
5
```

你可以在赋值语句的左侧使用下标来替换数组中的选定元素：

```
$ NAMES[1]-max
$ echo ${NAMES[@*]}
max max sum each
```
