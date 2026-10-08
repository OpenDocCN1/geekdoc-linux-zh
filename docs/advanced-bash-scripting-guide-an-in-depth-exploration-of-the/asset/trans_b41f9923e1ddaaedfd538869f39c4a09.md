

# 高级 Bash 脚本指南

```
fi
echo -n "$a "    # 这行在 3 和 11 时不会执行
done

# 练习：
# 为什么循环会打印到 20？
echo; echo
echo 正在打印 1 到 20 的数字，但在 2 之后发生了某些情况。
######################################################

# 相同的循环，但将 'break' 替换为 'continue'。
a=0

while [ "$a" -le "$LIMIT" ]
do
    a=$((a+1))

if [ "$a" -gt 2 ]
then
    break # 跳过循环的剩余部分。
    fi
    echo -n "$a"
done

echo; echo; echo
exit 0
```

`break` 命令可选地接受一个参数。普通的 `break` 会终止它所嵌入的最内层循环，而 `break N` 则会跳出 N 级循环。

示例 11-22. 跳出多层循环

```bash
#!/bin/bash
# break-levels.sh: 跳出循环。

# "break N" 会跳出 N 级循环。

for outerloop in 1 2 3 4 5
do
    echo -n "Group outerloop: "

    for innerloop in 1 2 3 4 5
do
        echo -n "$innerloop "

        if [ "$innerloop" -eq 3 ]
then
            break 2 # 尝试看看发生了什么 # “跳出”内层和外层循环。
        fi
done
```

# 11. 循环与分支

```bash
#
echo
done
echo
exit 0
```

`continue` 命令与 `break` 类似，可选地接受一个参数。普通的 `continue` 会缩短循环中的当前迭代并开始下一次迭代。`continue N` 会终止其循环层级的所有剩余迭代，并从向上 N 级的循环开始继续迭代。

# 示例 11-23. 在更高的循环层级继续

```
#!/bin/bash
# "continue N" 命令，在第 N 级循环上继续。
for outer in I II III IV V # 外层循环
do
  echo; -n "Group outer: "
#
for inner in 1 2 3 4 5 6 7 8 9 10 # 内层循环
do
  if [ $inner -eq 4 && "$outer" = "III" ];
then
    continue 2 # 在第 2 级循环继续，即“外层循环”。
    # 将上述行替换为简单的 "continue"
    # 以观察正常的循环行为。
fi
echo -n "$inner " # 7 8 9 10 不会在 "Group III." 打印
done
#
```

done
echo; echo

# 练习：
# 在脚本中为 "continue N" 构出一个有意义的用途。
exit 0

# 示例 11-24. 在实际任务中使用 continue N

# Albert Reiner 提供了一个关于如何使用 "continue N" 的示例：
#

```
# 假设我有大量的作业需要运行，其中
## 任何数据都将在目录中具有特定命名模式的文件中
## 进行处理。那里有几台机器可以访问
## 该目录，我想将工作分配到这些
## 机器上。
# 然后我通常在每台机器上运行类似下面的 nohup 东西：
while true
```

```
do
  for n in .iso*
  do
    [ "$n" = ".iso.opts" ] && continue
    beta=${n#.iso} && continue
    [ -r .iso.$beta ] && continue
    [ -r .lock.beta ] && sleep 10 && continue
    lockfile -r0 .lock.beta | continue
    echo -n "$beta: "date"
    run-isotherm $beta
    ls -alf .iso.$beta
    [ -r .iso.$beta ] && rm -f .lock.beta
    continue 2
  break
done
exit 0
# 细节，特别是 sleep N，取决于我的
+# 应用，但通用模式是：

```bash
while true
do
  for job in (pattern)
  do
    (作业完成或正在运行) && continue
    (标记作业为已完成、运行作业、标记作业为已完成)
    continue 2
  done
  break # 或者使用类似 'sleep 600' 来避免终止。
done
```

# 此脚本只有在没有更多作业要执行时才会停止
+# （在运行时添加的作业）。通过使用
+# 适当的锁文件，可以在多台机器上并发运行
+# 而不会产生重复计算（在我的情况下运行几个
+# 小时，我真的想避免这一点）。此外，由于
+# 总是从头开始，可以在文件名中编码优先级。continue '2
+# 但你必须实际检查某些作业是否完成
+# （以便我们立即寻找下一个作业）或未完成
+# （以防我们在检查新作业之前终止或睡眠了长时间）。

> 这种新结构难以理解，且在任何有意义的语境下使用都非常棘手。最好避免使用。

# 11.4. 测试与分支

`case` 和 `select` 结构在技术上不是循环，因为它们不会迭代执行代码块。然而，循环是根据代码块顶部或底部的条件来引导程序流。

在代码块中控制程序流

case (in) esac

`case` 结构是 Shell 脚本中 C/C++ 中 `switch` 的对应物。它允许根据条件测试跳转到多个代码块之一。它作为多个 `if/else` 语句的简写形式，是创建菜单的合适工具。

```bash
case "$variable" in

  "$condition1")
    command...
    ;

  "$condition2")
    command...
    ;

esac
```

- ◇ 给变量加引号不是强制的，因为不会发生单词拆分。
- ◇ 每个测试行都以右括号 ) 结束。
- ◇ 每个条件块以双分号 ;; 结束。
- ◇ 如果条件测试为真，则执行相关命令并终止 `case` 块。
- ◇ 整个 `case` 块以 `esac`（case 的倒序写法）结束。

# 示例 11-25. 使用 case

```
#!/bin/bash
# 测试范围。

echo "按一个键:"
read Keypress

case "$Keypress" in
# 如上所述

  [a-z]) echo "小写字母"
  [A-Z]) echo "大写字母"
  [0-9]) echo "数字"
  *) echo "标点符号、空白或其他"
esac
```

# 练习：
# 修改脚本使其接受多个输入，
# 而不是在执行一次后终止。

```
#!/bin/bash
# 创建菜单

clear

echo "列表:"
echo "1) Evans"
echo "2) Jones"
echo "3) Julie"
echo "4) Morris"
echo "5) Smith"
echo "6) Zane"
echo "选择一个:"

read person

case "$person" in
  1) echo "你选择了第一个。"
  ;;
  2) echo "你选择了第二个。"
  ;;
  3) echo "你选择了第三个。"
  ;;
  4) echo "你选择了第四个。"
  ;;
  5) echo "你选择了第五个。"
  ;;
  6) echo "你选择了第六个。"
  ;;
  *) echo "你选择了无效选项。"
  ;;
esac
```

