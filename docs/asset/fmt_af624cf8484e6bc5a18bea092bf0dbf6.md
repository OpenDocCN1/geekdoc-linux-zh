
```
for ((num=0; num < $Max; num++))
do
    read -p "Enter value " grade[$num]
    ((tot=$tot+${grade[$num]}))
done
echo "The average is " $avg
read -p "Do you want to continue? Y/N" Ans
((avg=0))
((tot=0))
done
```

- 4. 保存脚本并关闭编辑器。
- 5. 赋予脚本执行权限，运行脚本，并在出现提示时，输入 3 作为最大成绩数量，然后输入成绩：100, 100 和 90。
- 6. 记录结果。
- 7. 按 Y 继续。
- 8. 重新运行脚本，输入 4 作为最大成绩数量，然后输入成绩：80, 88, 90 和 77。
- 9. 记录结果。
- 10. 按 Y 继续。
- 11. 重新运行脚本，并在提示时，输入 2 作为最大成绩数量，然后输入成绩：80 和 88。
- 12. 记录结果。
- 13. 按 N 停止。
- 14. 关闭你的窗口并注销。

## 第 9 章 高级 Shell 编程

图 9–2 显示了冒泡排序运行的截图。首先显示未排序的数组，然后显示冒泡排序的过程以展示每一轮发生的情况。最后，显示排序后的数组。你可以看到在每一轮中，最大值都被移动到了它的正确位置。在第 1 次中，数字 9 被移动到最后一个。在第 2 次中，数字 8 被移动到了正确位置。在第 3 次中，数字 7 被移动到了正确位置，依此类推。在最后一次中，所有的数字都处于正确的排序顺序。

![](img/72e8a95d2755ff2622521b6d924baa27_363_0.png)

图 9-2 对10个数字进行排序

在下一个示例中，使用冒泡排序对字母表进行排序。字母根据其 ASCII 序列号排序。这被称为排序序（collating sequence）。在 ASCII 排序序中，字母 "a" 分的值比字母 "z" 低，这就是为什么字母可以排序的原因。所以，你可以说 "a" 比 "z" 低，或者 "z" 比 "a" 高。排序实际上发生在代表字母的数字上，而不是字母本身。

在 9-3 中，字母表的 26 个字母被排序了。在这里你真的能看到冒泡效应。注意每一轮中的字母 "a"。从一轮到下一轮，你可以观察字母 "a" 向数组的左侧或“上方”移动，或者更靠近下标零。在每一轮中，“最高”的字母都会向数组的右侧或底部移动。注意轮数，25 次；这等于值的个数减一。

接下来你将实现冒泡排序，对一组你可以在服装商店购买的物品列表进行排序。

## 实现冒泡排序 347

```
File  Edit  New  Terminal  Go  Help

[taddmei bin]$ bubblesort

未排序的数组

d e c b f g h i j k l m n o p t f v w l r q s u s

排序过程

Pass 1: a c d e f g h i j k l m n o p q r s t u v w x y z

Pass 2: d c b e f g h i j k l m n o p t f v w l r q s u a y z

Pass 3: c b d e f g h i j k l m n o p t f v w l r q s u a w x y z

Pass 4: b c d e f g h i j k l m n o p q r s t u v w x y z

Pass 5: a b c d e f g h i j k l m n o p q r s t u v w x y z

Pass 6: e d c b a f g h i j k l m n o p l q r s t u v w x y z

Pass 7: g e d c b a f h i j k l m n o p q r s t u v w x y z

Pass 8: f g e d c b a h i j k l m n o p q r s t u v w x y z

Pass 9: b g f e d c b a h i j k l m n o p q r s t u v w x y z

Pass 10: j i h g f e d c b a f k l m n o p q r s t u v w x y z

Pass 11: k j i h g f e d c b a f l m n o p q r s t u v w x y z

Pass 12: l k j i h g f e d c b a f m n o p q r s t u v w x y z

Pass 13: m l k j i h g f e d c b a f n o p q r s t u v w x y z

Pass 14: n m l k j i h g f e d c b a f o p q r s t u v w x y z

Pass 15: o n m l k j i h g f e d c b a f p q r s t u v w x y z

Pass 16: p o n m l k j i h g f e d c b a f q r s t u v v w x y z

Pass 17: q p o n m l k j i h g f e d c b a f r s t u v w x y z

Pass 18: r q p o n m l k j i h g f e d c b a f s t u v w x y z

Pass 19: s r q p o n m l k j i h g f e d c b a f t u v w x y z

Pass 20: t s r q p o n m l k j i h g f e d c b a f u v w x y z

Pass 21: u t s r q p o n m l k j i h g f e d c b a f v w x y z

Pass 22: v u t s r q p o n m l k j i h g f e d c b a f w x y z

Pass 23: w v u t s r q p o n m l k j i h g f e d c b a f x y z

Pass 24: x w v u t s r q p o n m l k j i h g f e d c b a f x y z

Pass 25: y w v u t s r q p o n m l k j i h g f e d c b a f z

排序后的数组

a b c d e f g h i j k l m n o p q r s t u v w x y
```

**图 3** 对26个字母进行冒泡排序

要创建冒泡排序：

1. 以用户身份登录 Linux 系统，然后打开终端窗口。
2. 在 `$HOME/bin` 中创建一个文件 `BubbleSort`。
3. 插入以下行创建 `swap` 函数：

```bash
# 冒泡排序
local T=${a[1]}
a[1]=${a[2]}
a[2]=$T
```

4. 插入以下行为数组赋值、显示输出并设置必要的变量：

```bash
# 要排序的项目
a=(...)
echo "未排序的数组"
echo "${a[@]}" # 显示数组中的所有项目
echo "排序过程"
n=${#a[@]} # 变量 "n" 等于数组元素的个数
pass=$((n - 1)) # 变量 "pass" 等于外层循环使用的元素个数
```

5. 插入以下行创建外层和内层循环：

```bash
for (( p = 1; p <= $pass; p++ ))
do
    for (( i = 0; i <= ($pass-$p)); i++ ))
    do
        if [[ ${a[$i]} > ${a[$i + 1]} ]]; # 比较相邻项目
        then
            swap $i $((i + 1)) # 如果未排序，交换相邻项目
        fi
    done
    echo "Pass $p: ${a[@]}" # 显示每一轮的数组
done
```

6. 插入以下行显示排序后的数组：

```bash
echo "排序后的数组"
echo "${a[@]}"
```

7. 保存脚本并关闭编辑器。
8. 使脚本可执行并运行脚本。数组将按顺序显示。
9. 关闭窗口并注销。

## 实现壳排序
