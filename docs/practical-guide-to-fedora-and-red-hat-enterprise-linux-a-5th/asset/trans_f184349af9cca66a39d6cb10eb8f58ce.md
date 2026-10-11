

function exchange ()
{
    temp_value=$({questions[$1]}
    questions[$1]=${questions[$2]}
    questions[$2]=$temp_value
}

ask 函数也使用了 select 结构。它读取参数中指定的问题文件，并使用该文件的内容来呈现问题、接受答案以及判断答案是否正确。（见下文代码。）

ask 函数使用文件描述符 3 从问题文件中逐行读取数据，该文件名作为参数传入，在函数中由 $1 表示。它将问题读取到 ques 变量中，将问题数量读取到 num_opts 中。该函数通过初始化为空字符串并依次追加下一个选项来构建 choices 变量。然后，它将 PS3 设置为 ques 的值，并使用 select 结构以 ques 提示用户。select 结构将用户的答案存储在 answer 中，然后函数将其与文件中的正确答案进行比对。

choices 变量的构建方式旨在避免潜在问题。假设某个答案中包含空白字符。那么它在 choices 中可能会表现为两个或多个参数。为避免此问题，请确保 choices 是一个数组变量。select 语句会完成其余的工作：

$ cat quiz
#!/bin/bash

# 移除下一行前面的 # 以开启调试功能
# set -o xtrace
#=====================
function initialize()
{
    trap 'summarize ; exit 0' INT     # 处理用户中断
    num_ques=0                        # 迄今为止提出的问题数量
    num_correct=0                     # 迄今为止答对的题目数量
    first_time=true                   # 直到提出第一个问题前都为 true
    cd ${QUIZDIR:-~/quiz} || exit 2
}
#=====================
function choose_subj ()
{
    subjects=$( (ls) )
    PS3="从上述列表中为测验选择一个主题："
    select Subject in ${subjects[@]}; do
        if [[ -z "$Subject " ]]; then
            echo "未选择主题。再见。">&2
            exit 1
        fi
        echo $Subject
        return 0
    done
}

###############
function exchange ()
{
temp_value=$\{questions[\$1]\}
questions[\$1]=$\{questions[\$2]\}
questions[\$2]=$temp_value
}

###############
function scramble ()
{
typeset -i index quescount
questions=$(\$!)
quescount=\$\{#questions[*]\}      # 元素数量
((index=quescount-1))
while [[ \$index > 0 \% ]]; do
   ((target=RANDOM \% index))
   exchange \$target \$index
   ((index -= 1))
done
}

###############
function ask ()
{
exec 3<\$1
read -u3 ques || exit 2
read -u3 num_opts || exit 2

index=0
choices=()
while (( index < num_opts )); do
    read -u3 next_choice || exit 2
    choices="\${choices[\$]}" "\$next_choice"
    ((index += 1))
done
read -u3 correct_answer || exit 2
exec 3<&-

if [[ \$first_time = true ]]; then
first_time=false
echo -e "您可以随时按下中断键退出。\n"
fi

PS3="\$ques"    "                               # 使 \$ques 成为 select 的提示符
                                   # 并添加一些空格以提高可读性。
select answer in "\${choices[\$]}"; do
   if [[ -z "\$answer" ]]; then
       echo "不是有效选择。请重新选择。
   elif [[ "\$answer" = "\$correct_answer" ]]; then
       echo "正确！"
       return 1
   else
       echo "不，答案是 \$correct_answer。"
       return 0
   fi
done
}

#===================
function summarize ()
{
    echo
    if (( num_ques == 0 )); then
        echo "您没有回答任何问题"
        exit 0
    fi

    (( percent=num_correct*100/num_ques ))
    echo "您正确回答了 $num_correct 个问题，总共有 \\
    $num_ques 个问题。"
    echo "您的得分是 $percent 百分之一。"
}

#===================
# 主程序
initialize    # 顶层设计中的第 1 步

subject=$(choose_subj)
[[ $? -eq 0 ]] || exit 2

cd $subject || exit 2
echo
scramble

for ques in ${questions[*]}; do
    ask $ques
    result=$?
    (( num_ques=num_ques+1 ))
    if [[ $result == 1 ]]; then
        (( num_correct += 1 ))
    fi
    echo
    sleep ${QUIZDELAY:=1}
done

summarize
exit 0

## 章节总结

Shell 是一种编程语言。用该语言编写的程序称为 shell 脚本，或简称为脚本。Shell 脚本提供了高级编程语言中存在的决策和循环控制结构，同时允许轻松访问系统实用程序和用户程序。Shell 脚本可以使用函数来模块化和简化复杂任务。

使用决策来选择替代方案的控制结构是 if...then、if...then...else 和 if...then...elif。case 控制结构提供了多分支选择，当希望使用简单的模式匹配语法表达替代方案时可以使用。

循环控制结构是 for...in、for、until 和 while。这些结构反复执行一个或多个任务。

**break** 和 **continue** 控制结构改变了循环内的控制流：**break** 将控制权转移出循环，而 **continue** 立即将控制权转移到循环的顶部。

Here document 允许 shell 脚本中的命令输入来自脚本本身内部。

- **文件描述符**：Bourne Again Shell 提供了操作文件描述符的能力。结合 **read** 和 **echo** 内置命令，文件描述符使 shell 脚本能够像用低级语言编写的程序一样控制输入和输出。
- **变量**：使用 *type set* 内置命令为 *bash* 变量分配属性，例如 *readonly*。Bourne Again Shell 提供了用于对变量进行模式匹配的运算符、为变量提供默认值的运算符以及评估变量长度的运算符。该 shell 还支持函数的数组变量和局部变量，并使用 *let* 内置命令以及类似于 C 编程语言表达式语法的内置整数算术功能。
- **内置命令**：Bourne Again Shell 的内置命令包括 *type*、*read*、*exec*、*trap*、*kill* 和 *getopts*。*type* 内置命令显示关于命令的信息，包括其位置；*read* 允许脚本接受用户输入。*exec* 内置命令执行命令而无需创建新进程。新命令覆盖当前进程，假设该进程具有相同的环境和 PID 号。当不需要将控制权返回给调用进程时，此内置命令执行用户程序和其他 Linux 命令。*trap* 内置命令捕获 Linux 发送给运行脚本进程的信号，并允许您在收到一个或多个信号时指定要采取的操作。您可以使用此内置命令使脚本忽略用户按下中断键时发送的信号。*kill* 内置命令允许您终止正在运行的程序。*getopts* 内置命令解析命令行参数，使编写遵循 Linux 命令行参数和选项标准约定的程序变得更加容易。
- **脚本中的实用程序**：除了使用控制结构、内置命令和函数外，shell 脚本通常调用 Linux 实用程序。例如，*find* 实用程序在搜索系统层次结构中的文件的 shell 脚本中很常见，并且可以执行从简单到复杂的各种任务。编写良好的 shell 脚本遵循标准编程实践，例如在脚本的第一行指定执行脚本的 shell、验证调用脚本时参数的数量和类型、显示标准用法消息以报告命令行错误，以及将所有信息消息重定向到标准错误。
- **表达式**：表达式有两种基本类型：算术和逻辑。算术表达式允许您对常量和变量进行算术运算，产生数值结果。逻辑（布尔）表达式比较表达式或字符串，或测试条件以产生 *true* 或 *false* 结果。与 Linux shell 脚本中的所有决策一样，*true* 状态由值零表示；*false* 则由任何非零值表示。

