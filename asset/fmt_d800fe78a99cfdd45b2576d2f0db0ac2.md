
## 高级 Bash 脚本指南

### 第 26 章 数组

**数组基础**

```bash
array0=( first second third )
array1=( ' ') # "array1" 有一个空元素
array2=() # 没有元素... "array2" 是空的。

echo "Elements in array0: ${array0[0]}"
echo "Elements in array1: ${array1[0]}"
echo "Elements in array2: ${array2[0]}"

echo "Length of first element in array0: ${array0[0]}"
echo "Length of first element in array1: ${array1[1]}"
echo "Length of first element in array2: ${array2[2]}"

echo "Number of elements in array0: ${array0[@]}" # 3
echo "Number of elements in array1: ${array1[*]}" # 1 (意外！)
echo "Number of elements in array2: ${array2[*]}" # 0

exit 0 # 感谢，C.
```

`$array_name[@]` 和 `$array_name[*]` 之间的关系类似于 `@@` 和 `$*` 之间。这种强大的数组表示法有很多用途。

**数组操作**

```bash
# 复制数组。
array2=("array1[@]}")
# 或者
array2="${array1[*]}"

# 向数组添加元素。
array=("${array[0]}) "new element"
# 或者
array[${#array[*]*}="new element"

# 感谢，C.
```

`array=element1 element2 ... elementN` 初始化操作，通过命令替换的帮助，使得将文本内容加载到数组中成为可能。

**示例 26-4. 冒泡排序**

```bash
#!/bin/bash

filename=sample_file

# cat sample_file
# 1 a b c
# 2 d e f g

declare -a array1

array1=$(cat "$filename" | tr '\n' ' ') # 将文件名的内容加载到 array1。
# 输出文件到标准输出。
# 将文件中的换行符更改为空格。

echo ${array1[@]} # 列出数组。
```

**示例 26-5. 质数筛**

```bash
# ... (逻辑继续)

initialize ()
{
# 初始化数组。

i=$LOWER_LIMIT
until [ "$i" -gt "$UPPER_LIMIT" ]
do
  Primes[i]=$PRIME
  let i += 1
done
  # 假设所有数组元素都是有罪的（质数）
  # 直到被证明无罪。
}

print_primes ()
{
# 打印 Primes[] 数组中标记为质数的元素。

i=$LOWER_LIMIT
until [ "$i" -gt "$UPPER_LIMIT" ]
do

  if [ "${Primes[i]}" -eq "$PRIME" ]
then
    printf "%8d" "$i"
    # 每个数字留出 8 个空格可以形成整齐的列。
  fi
done

let i += 1
}

sift ()
{
# 筛选掉非质数。

let i=$LOWER_LIMIT+1
# 我们知道 1 是质，所以从 2 开始。

until [ "$i" -gt "$UPPER_LIMIT" ]
do

  if [ "${Primes[i]}" -eq "$PRIME" ]
# 不要去处理已经筛选过的数字（已标记为非质数）。
then

    t=$i
    while [ "$t" -le "$UPPER_LIMIT" ]
do
      let t += $i
      Primes[t]=$NON_PRIME
      # 将所有倍数标记为非质数。
done
  fi
done
}

let "i += 1"
)

# 顺序调用函数。
initialize
sift
print_primes
# 这就是他们说的结构化编程。

echo

exit 0

#------------------------------------
# 下以下代码将不会执行。

# 这个由 Stephanie Chazelas 改进的筛法版本
# 执行速度较快。

# 必须带有命令行参数调用（质数范围）。
UPPER_LIMIT=$1    # 来自命令行。
let SPLIT=UPPER_LIMIT/2    # 到最大数字的一半。

Primes=(' $(seq $UPPER_LIMIT) )

i=1
until [[ ((i += 1) > SPLIT ]]; # 只需检查到一半。
do
  if [[ -n ${Primes[$i]} ]]];
  then
    t=$i
    until (( ((t += i) > UPPER_LIMIT ))
    do
      Primes[t]=
    done
  fi
done
echo ${Primes[*]}
exit 0
```

将此基于数组的质数生成器与不使用数组的替代方案进行比较。参见示例 A-14。

---

数组在某种程度上可以模拟 Bash 无原生支持的数据结构。

**示例 26–6. 模拟推入栈**

```bash
#!/bin/bash
# stack.sh: 推入栈模拟

# 类似于 CPU 栈，推入栈按顺序存储数据项
# 但按反序释放它们，即后进先出。

BP=100            # 栈数组的基指针。
                   # 从元素 100 开始。
SP=$BP           # 栈指针。
                   # 将其初始化为栈的“基底”（底部）。
Data=             # 栈位置的内容。
                   # 必须使用局部变量，
                   # 因为函数返回范围有限制。
declare -a stack

push() {
  if [ -z "$1" ]  # 将项目推入栈。
  then
    return
  fi

  let SP --= 1      # 增加栈指针。
  stack[$SP]=$1
  return
}

pop() {           # 从栈中弹出项目。
  Data=            # 清空数据项。
  if [ "$SP" -eq "$BP" ]  # 栈为空？
  then
    return
  fi
  # 这也防止了 SP 超过 100，
  # 防止栈溢出。
  Data=${stack[$SP]}
  let SP += 1       # 增加栈指针。
  return
}

status_report() {
  # 找出正在发生什么。
  echo "------------------------------------------------"
  echo "报告"
  echo "栈指针 = $SP"
  echo "刚刚从栈中弹出 \"$Data\"。"
  echo "------------------------------------------------"
  echo
}

# ==================================================
# 现在，来玩点点。
echo

# 看看是否能从空栈弹出任何东西。
pop
status_report

echo

push garbage
pop
status_report # 垃圾进，垃圾出。
value1=23; push $value1
value2=skidoo; push $value2
value3=FINAL; push $value3

pop # FINAL
status_report
pop # skidoo
status_report
pop # 23
status_report # 后进先出！

echo

# 注意栈指针如何每次 push 都会递减
# + 每次 pop 都会增加。

====================================================
```

**练习：**

- 1) 修改 `push()` 函数，允许在单次调用中向栈推入多个元素。
- 2) 修改 `pop()` 函数，允许在单次调用中从栈弹出多个元素。
- 3) 以此脚本为起点，编写一个基于栈的计算器。

对数组“脚本”进行精妙操作可能需要中间变量。对于涉及这些的项目，再次考虑更强大的语言，例如 `Perl` 或 `C`。

**示例 26–7. 复杂的数组应用：探索一个奇特的序列**

```bash
#!/bin/bash

# Hofstadter 著名的“Q-序列”:
# Q(1) = 1
# Q(2) = 1
# Q(n) = Q(n-1) + Q(n-2), 对于 n>2
# 这是一个“混沌”序列，具有奇异且不可预测的行为。
# 该序列的前 20 项为：
# 1 2 3 4 5 6 8 8 9 10 11 12

LIMIT=100 # 要计算的项数
LINEWIDTH=20 # 每行的项数

Q[1]=1 # 序列的第一项。
Q[2]=1 # 序列的第二项。

for ((n=3; n<LIMIT; n++))
do
  Q[n]=$(( Q[n-1] + Q[n-2] ))
  echo -n "${Q[n]} "
  if [ $((n % LINEWIDTH)) -eq 0 ]; # 格式化输出。
  then
    echo
  fi
done

# 迭代实现 Q-序列作为练习。
警告：递归实现此序列非常耗时。
```

`Bash` 仅支持一维数组，但通过小技巧允许模拟多维数组。

**示例 26–8. 模拟二维数组，然后倾斜它**

```bash
#!/bin/bash

# 模拟二维数组

# 二维数组按顺序存储。

Rows=5

Columns=5

declare -a alpha      # 无必要的声明。

load_alpha ()
{
    local rc=0
    local index
    local row=0
}while [ "$row" -lt "$Rows" ];
do
    # 按行输出
    # 列在变化
    local column=0
    while [ "$column" -lt "$Columns" ];
    do
        let index=$(row * Rows + column)
        echo -n "${alpha[$index]}"  # alpha[row][column]
        let "column += 1"
    done
    let "row += 1"
done

# 更简单的等价方法
# echo ${alpha[*]} | xargs -n $Columns

filter () {
    echo -n ""      # 过滤负数组索引。
    #               提供了倾斜。
}

if [[ "$1" -ge 0 && "$1" -lt "$Rows" && "$2" -ge 0 && "$2" -lt "$Columns" ]];
then
let index=$1 * Rows + "$2"
# 现在，打印旋转后的。
echo -n "${alpha[$index]}"  # alpha[row][column]
fi

rotate () # 将数组绕其左下角旋转。
local row
local column
for ((row = Rows; row > -Rows; row-- ))  # 反向遍历数组
  for ((column = 0; column < Columns; column++))
  do
    if [ "$row" -ge 0 ]
    then
      let t1=$column $row
      let t2=$column
    else
      let t1=$column
      let t2=$column + $row
    fi
    filter $t1 $t2  # 过滤掉负数组索引。
  done
  echo; echo
done

# 数组旋转灵感来自《哥德尔、埃舍尔、巴赫：永恒的金织》中的示例（第 143-146 页）。
#（参见参考文献）。

--------------------------------------

load_alpha      # 加载数组。

print_alpha     # 打印它。

rotate          # 逆时针旋转 45 度。

--------------------------------------

exit 0
```

二维数组本质上等同于一维数组，但具有额外的地址模式，可以通过“行”和“列”位置来引用和操作单个元素。

欲了解模拟二维数组的更详尽的示例，请参见示例 A–8。

### 第 27 章：文件

#### 启动文件

这些文件包含了作为用户 `shell` 运行的 `Bash` 以及在系统初始化后调用的所有 `Bash` 脚本可用的别名和环境变量。

| 文件路径 | 说明 |
| :--- | :--- |
| `/etc/profile` | 系统级默认设置，主要设置环境（所有 `Bourne` 类型的 `shell`，不包括 `Bash` [56]） |
| `/etc/bashrc` | `Bash` 的系统级函数和别名 |
| `$HOME/.bash_profile` | 用户特定的 `Bash` 环境变量默认设置，位于每个用户的家目录中（是 `/etc/profile` 的本地对应项） |
| `$HOME/.bashrc` | 用户特定的 `Bash` 初始化文件，位于每个用户的家目录中（是 `/etc/bashrc` 的本地对应项）。只有交互式 `shell` 和用户脚本会读取此文件。请参见附录 G 中的示例 `.bashrc` 文件。 |

#### 注销文件

| 文件路径 | 说明 |
| :--- | :--- |
| `$HOME/.bash_logout` | 用户特定的指令文件，位于每个用户的家目录中。当退出登录 (`Bash`) `shell` 时，将执行此文件中的命令。 |

### 第 28 章：/dev 和 /proc

`Linux` 或 `UNIX` 机器通常有两个特殊用途目录：`/dev` 和 `/proc`。

#### 28.1. /dev

`/dev` 目录包含了硬件中可能存在也可能不存在物理设备的条目。[57]。如简单的 `df` 命令所示，包含挂载文件系统的硬设备分区在 `/dev` 中有相应条目。

```bash
bash$ df
```

| Filesystem | 1k-blocks | Used | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/sda` | 495876 | 222748 | 247527 | 48% | `/` |
| `/dev/hdb1` | 50755 | 3887 | 44248 | 9% | `/boot` |
| `/dev/hda8` | 367013 | 13262 | 334803 | 4% | `/home` |
| `/dev/hda5` | 171416 | 112624 | 503704 | 70% | `/usr` |

其中，`/dev` 目录还包含回环设备（loopback devices），例如 `/dev/loop0`。回环设备是一种技巧，允许普通文件像块设备一样被访问。[158] 这允许在一个大文件中挂载整个文件系统。请参见示例 13-6 和示例 13-5。

`/dev` 中的一些伪设备具有其他特殊用途，例如 `/dev/null`、`/dev/zero` 和 `/dev/urandom`。

#### 28.2. /proc

`/proc` 目录实际上是一个伪文件系统，`/proc` 目录中的文件镜像了运行中的系统和内核进程，并包含了关于它们的信息和统计数据。

```bash
bash$ cat /proc/devices

Character devices:

1 mem
2 pty
3 ttyp
4 tty
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts
162 raw
254 pcmcia

Block devices:

1 ramdisk
```

```bash
bash$ cat /proc/interrupts

CPU0
0: 84505 XT-PIC timer
1: 3375 XT-PIC keyboard
2: 0 XT-PIC cascade
5: 1 XT-PIC soundblaster
8: 1 XT-PIC rtc
12: 4231 XT-PIC PS/2 Mouse
14: 109373 XT-PIC ide0
NMI: 0
ERR: 0
```

```bash
bash$ cat /proc/partitions

major | #blocks | name | rio | rmerge | rest | ruse | wo | wmerge | wsect | using | run | aveq |
```

