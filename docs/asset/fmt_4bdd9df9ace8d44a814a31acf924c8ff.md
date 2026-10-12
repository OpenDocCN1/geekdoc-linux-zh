
当 `makpath` 被拒绝创建 `/a` 目录时，递归停止。返回的错误会一直传回，因此原始的 `makpath` 以非零状态退出。

## 在递归函数中使用局部变量

前面的示例忽略了你在使用递归函数时可能会遇到的一个潜在问题。在递归函数的执行期间，可能会有许多独立的函数实例同时激活。但所有这些实例都在等待它们的子调用完成。

由于函数在与调用它的 Shell 相同的环境中运行，变量在 Shell 及其调用的之间是隐式共享的。因此，函数的所有实例共享每个变量的一个副本。共享变量可能会导致副作用，而这通常不是你想要的。按照原则，你应该使用 `typeset` 将递归函数的所有变量声明为局部变量。更多信息请参阅第 1010 页。

# 测验 Shell 脚本

使用 `bash` 脚本解决以下问题：

编写一个通用的多选题测验程序。该程序应该从数据文件中获取问题，展示给用户，并跟踪正确和错误答案的数量。用户必须能够随时退出程序，并接收到目前为止的结果总结。

该程序的详细设计，甚至是问题的详细描述，取决于许多选择：程序如何知道哪些科目可以进行测验？用户如何选择科目？程序如何知道测验何时结束？程序应该每次以相同的顺序展示（对于给定科目）相同的问题，还是应该将它们打乱顺序？

当然，你可以做出许多非常好的选择来实现问题的规范。以下细节缩小了问题规范：

- 每个科目将对应主测验目录的一个子目录。该目录将由环境变量 `QUIZDIR` 命名，其默认值为 `~`。例如，你可以拥有以下对应工程、艺术和政治科目的目录：`~/engineering`、`~/art` 和 `~/politics`。如果你想让所有用户都能访问，将测验目录放在 `/usr` 中（需要 root 权限）。
- 每个科目可以有几个问题。每个问题由其科目目录中的一个文件表示。
- 代表问题的文件的第一行保存问题的文本。如果超过一行，你必须用反斜杠转义换行符。（这种设置使得使用 `read` 内置命令轻松读取单个问题）。文件的第二行指定选项数量的整数。接下来的行是选项本身。最后一行是正确答案。以下是一个示例问题文件：
```text

谁发现了杠杆原理？

4

Eclid

Archimedes

Thomas Edison

The Lever

Archimedes

```
- 程序展示科目目录中的所有问题。在任何时候，用户都可以使用 `CTRL-C` 中断测验，随后程序将总结到该点为止的结果并退出。如果用户没有中断程序，程序将在提问完所选科目的所有问题后总结结果并退出。
- 程序在展示科目中的问题之前会先对它们进行打乱处理。

以下是该程序的顶层设计：

1. 初始化。这涉及许多步骤，例如将目前已问的问题数量以及正确和错误答案的数量置零。它还设置了程序来捕获（trap）`CONTROL-C`。
2. 向用户提供科目选择并获取用户的响应。
3. 切换到相应的科目目录。
4. 确定要问的问题（即该目录下的文件名）。将它们随机随机排列。
5. 反复展示问题并要求作答，直到测验结束或被用户中断。
6. 展示结果并退出。

显然，这些步骤中的某些（如步骤 3）是简单的，而另一些（如步骤 4）是复杂的，值得单独分析。对任何复杂步骤使用函数，并使用 `trap` 内置命令处理用户中断。这里有一个带有空函数的程序框架版本：

```bash
function initialize
{
# 初始化变量。
}
```

```bash
function choose_subj
{
# 将选择写入写入标准输出。
}
```

```bash
function scramble
{
# 将问题文件的名称打乱后，
# 存储在一个名为 questions 的数组变量中。
}
```

```bash
function ask
{
# 读取问题并要求答案。
}
```

```bash
function summarize
{
# 总结结果。
}
```

```bash
function exchange ()
{
  temp_value=${questions[$1]}
  questions[$1]=${questions[$2]}
  questions[2]=$temp_value
}
```

`ask` 函数也使用了 `select` 结构。它读取参数中指定的名为问题的文件，并使用该文件的内容来展示问题、接受答案，并判断答案是否正确。（参见相关代码。）

`ask` 函数使用文件描述符 3 从问题文件中连续读取行，该文件的名称是作为参数传递的，并在函数中显示为 `$1`。它将输入读取到 `ques` 变量，并将问题数量读入 `num_opts`。该函数通过将 `choices` 变量初始化为空字符串并继继追加下一个选项来构建 `choices` 变量。它将 `PS3` 设置为 `ques` 的值，并使用 `select` 结构提示用户。`select` 结构将用户的答案存放在 `answer` 中，然后函数将其与文件中的正确答案进行比对。

`choices` 变量的构建是为了避免可能的问题。假设一个答案中包含空格——那么它在 `choices` 中可能会显示为两个或多个参数。为了避免这个问题，将 `choices` 设为一个数组变量。`select` 语句完成了其余的工作：

## cat quiz

```bash
#!/bin/bash
# 删除下面一行的 # 注释以关闭调试
# set -o xtstrace
=================
function initialize ()
{
  trap 'summarize ; exit 0' INT
  num_ques=0
  num_correct=0
  first_time=
  cd $(QUIZDIR:-~/quiz) || exit 2
}
=================
function choose_subj ()
{
  subjects=($1)
  PS3="Choose a subject for the quiz from the preceding list: "
  select Subject in ${subjects[@]}; do
    if [[ -z "$Subject" ]]; then
      echo "No subject chosen. Bye." >&2
      exit 1
    fi
    echo $Subject
    return 0
  done
}
```

# SHELL 程序 1049

```bash
==========================
function exchange () {
    temp_value=${questions[$1]}
    questions[$1]=${questions[$2]}
    questions[2]=$temp_value
}
```

```bash
==========================
function scramble () {
    typeset -i index quescount
    questions=$($(ls))
    quescount=${#questions[@]} # 元素数量
    while [[ $index > 0 ]]; do
        ((target=$((RANDOM % quescount))))
        exchange $target index
        ((index -= 1))
    done
}
```

```bash
==========================
function ask () {
    exec 3<$1
    read -u3 ques || exit 2
    read -u3 num_opts || exit 2
}
```

```bash
index=0
while [[ $index < num_opts ]]; do
    read -u3 next_choice || exit 2
    choices=("${choices[@]}" "$next_choice")
    ((index += 1))
done
read -u3 correct_answer || exit 2
```

```bash
if [[ $first_time == true ]]; then
    first_time=false
    echo -e "You may press the interrupt at any time to quit.\n"
```

```bash
PS3=\$ques " # 为 $ques 创建提示符
# # 添加一些空格以提高可读性。
select answer in "${choices[@]}"; do
    if [[ -z "$answer" ]]; then
```
