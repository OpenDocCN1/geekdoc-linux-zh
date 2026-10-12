
```bash
echo "Not a valid choice. Please choose again."
elif [[ "$answer" = "$correct_answer" ]]; then
    echo "Correct!"
    return 1
else
    echo "No, the answer is $correct_answer."
    return 0
fi
done
```

```bash
############################
function summarize () {
    echo
    if (( num_ques == 0 )); then
        echo "You did not answer any questions"
        exit 0
    fi
    if (( percent=num_correct*100/num_ques )); then
        echo "You answered $num_correct questions correctly, out of $num_ques total questions."
        echo "Your score is $percent percent."
    fi
}
############################
# 主程序
initialize
subject=$(choose_subj)
[[ $? -eq 0 ]] || exit 2
cd "$subject" || exit 2
echo
scramble
for ques in ${questions[*]}; do
    ask "$ques"
    result=$((num_ques=num_ques+1))
    if [[ $result == 1 ]]; then
        ((num_correct += 1))
    fi
    echo
    sleep ${QUIZDELAY:-1}
done
summarize
exit 0
```

# 章节总结

Shell 是一种编程语言。用这种语言编写的程序称为 shell 脚本，或简称为脚本。Shell 脚本提供了高层编程语言中的决策和循环控制结构，同时允许方便地访问系统实用和用户程序。Shell 脚本可以使用函数对复杂任务进行模块化和简化。

## 控制结构
使用决策选择替代方案的控制结构包括 `if...then`、`if...then...else` 以及 `if...then...elif`。`case` 控制结构提供了多路分支，当想要使用简单的模式匹配语法来表示备选方案时可以使用。

## 循环控制结构
包括 `for...in`、`for`、`until` 和 `while`。这些结构重复地执行一个或多个任务。

# 章节总结 1051

使用决策选择替代方案的控制结构是 `if...then`、`if...then...else` 以及 `if...then...elif`。`case` 控制结构提供了多路分支，当想要使用简单的模式匹配语法来表示备选方案时可以使用。

循环控制结构是 `for...in`、`for`、`until` 和 `while`。这些结构重复地执行一个或多个任务。

## 文件描述符
使用文件描述符 `3` 从问题文件中连续读取行，该文件的名称是通过参数传递的，并在函数中显示为 `$1`。它将输入读取到 `ques` 变量，并将问题数量读入 `num_opts`。函数通过将 `choices` 变量初始化为空字符串并继继追加下一个选项来构建 `choices` 变量。它使用 `select` 结构来提示用户。`choices` 变量的构建是为了避免一个潜在的问题。假设一个答案中包含空格——那么它在 `choices` 中可能会显示为两个或多个参数。为了避免这个问题，将 `choices` 设为一个数组变量。`select` 语句完成了其余的工作：

`choices` 变量的构建是为了避免一个潜在的问题。假设一个答案中包含空格——那么它在 `choices` 中可能会显示为两个或多个参数。为了避免这个问题，将 `choices` 设为一个数组变量。`select` 语句完成了其余的工作：

a. 执行此脚本时，你收到了什么错误信息？重写该脚本以防止错误发生，同时确保输出仍然发送到它们。

b. 在同一目录下多次运行此脚本可能会有什么问题？讨论解决该问题的方案。

9. 阅读 `hash` 手册或页面，尝试一些实验，并回答以下问题：

a. 你如何导出一个函数？

b. 内置命令 `hash` 的作用？

c. 如果 `exec` 的参数不是可执行文件，会发生什么？

10. 使用 `find` 工具执行以下任务：

a. 列出工作目录及所有子目录下在过去一天内修改过的文件。

b. 列出你对系统具有读取权限且大于 1 兆字节的文件。

c. 从以你的家目录为根的目录结构中删除所有名为 `core` 的文件。

d. 列出工作目录中所有以 `.` 结尾的文件数量。

e. 列出你对根文件具有读取权限且在过去 30 天内修改过的文件。

11. 写一个短脚本，告诉你作为脚本参数传入的两个文件的权限是否相同。如果两个文件的权限相同，则输出公共权限字段；否则，输出每个文件名及其随后的权限字段。（提示：尝试使用 `cut` 工具。）

12. 写一个脚本，接受一个目录名称作为参数，并在以该目录为根的文件层次结构中搜索零长度文件。如果没有命令行选项，则打印文件名；让脚本在显示文件名后向用户请求确认，并在收到肯定的确认后删除该文件。命令行上的 `-f`（强制）选项表示脚本应该显示文件名，但在删除文件前不询问确认。

## 高级练习

13. 写一个脚本，它接受一个由冒号分隔的项列表，并将这些项每行一个输出到标准输出（不带冒号）。

14. 将第 13 题编写的脚本通用，使得分隔列表项的字符作为参数传递给函数。如果没有此参数，分隔符应默认为冒号。

15. 写一个函数 `funload`，它接受单个参数，即包含其他函数的文件。`funload` 的目的是使文件中的所有函数在当前 shell 中可用；也就是说，`funload` 从命名的文件中加载函数。为了找到该文件，`funload` 通过环境变量 `FUNPATH` 搜索逗号分隔的目录列表。假设 `FUNPATH` 的格式与 `PATH` 相同，搜索 `FUNPATH` shell 搜索 `PATH` 变量。

16. 重写 `bundle`（第 102 页），使脚本创建一个最优文件名列表。如果在命令行上给了一个或多个文件名，则应重新创建这些文件；否则，shell 存档中的所有文件都应重新创建。例如，假设所有扩展名为 `.c` 的文件都被到一个名为 `rshell` 的存档中，你想解包文件 `test1.c` 和 `test2.c`。以下命令链接这些文件：

```bash
$ bash rcshell test1.c test2.c
```

17. `Links` 脚本（第 977 页）无法找到哪种链接？

18. 原则上，递归永远不是必要的。它可以被迭代结构（如 `while` 或 `until`）所取代。将 `花费`（第 1042 页）重写为非递归函数。你更倾向于哪个版本？

19. 列表主要通过在每个列表元素之间放置冒号（`:`）来存储在环境变量中（`PATH` 变量的值就是一个例子）。你可以通过将元素连接到列表前端向此类列表添加元素，如：

```bash
PATH=/opt/bin:$PATH
```

如果元素已经在列表中，则在列表中会有两个副本。写一个 shell 函数 `addenv`，它接受两个参数：(1) shell 变量的名称和 (2) 一个要加在列表前的字符串，仅当该字符串不是列表中的元素时，才将其前置。例如，调用

```bash
addenv /opt/bin
```
