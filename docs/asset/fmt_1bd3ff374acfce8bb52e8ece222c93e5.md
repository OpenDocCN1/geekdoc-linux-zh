
| `$HOSTTYPE` | 机器的主机类型。 |

| `$IFS` | IFS 设置。如果设置为默认值则为空。 |

| `$MACHTYPE` | 机器类型。 |

| `$OLDPWD` | 你上一个所在的目录。 |

| `$OSTYPE` | 操作系统类型。 |

| `$PATH` | 命令搜索路径。 |

| `$PIPESTATUS` | 上一个完成的管道的退出状态。 |

| `$PPID` | 当前 shell 父进程的进程 ID。 |

| `$PS1`, ..., `$PS4` | shell 的（提示符 1 到 4）格式。 |

| `$PWD` | 当前工作目录。 |

| `$RANDOM` | 0 到 2^15 之间的伪随机整数。 |

| `$SECONDS` | 脚本执行的秒数。 |

| `$UID` | 当前用户的 ID。 |

关于 shell 变量有几点需要注意。首先，你不需要手动设置、声明、删除或修改它们。无论你是否决定使用它们，它们都存在。其次，shell 变量总是全大写的。这有助于你避免用自己的变量覆盖掉其中之一。

一个好的规则是始终用小写命名你的变量。这样，每当你看到大写的变量时，就知道它是特殊的。最后，shell 变量和环境变量不是一回事。

环境变量将在第 13 章介绍。

目前，涉及 shell 变量的最深入的示例将是列出它们的值。

# 第 6 章：数组 (Arrays)

数组的使用比整数变量频繁，但它们需要考虑设置、读取和调用。

## 索引数组 (Indexed arrays)

在这种类型的数组（最常见）中，每个值都映射到一个从零开始的键。从图形上看，它如下：

```
+ animals

0 Dog

1 Bear

2 Llama

3 Parrot

4 Otter
```

数组的创建与变量创建相似。像 Bash 中的一切一样，通常有多种方法完成相同任务。数组也不例外。

## 声明 (Declaration)

```bash
array=()
declare -a array
```

`declare -a array` 声明一个空数组并将第一个值（索引 0）设置为 `value`。

一旦创建了无值的数组，可以使用以下语法修改。

## 存储值 (Storing values)

```bash
array[i]=value
array=(value1, value2, ..., valueN)
array+=(value1, value2, ..., valueN)
```

## 设置数组值

将 `array` 的 `ith` 设置为 `value`。

## 设置整个数组

将整个 `array` 设置为任意数量的值 `value1`, `value2`, ..., `valueN`，这些值按顺序从零索引。除非数组被追加，否则之前设置的数组值将丢失。

## 追加数组

将值 `value1`, `value2`, ..., `valueN` 追加到数组 `array`。

## 复合设置数组值

将索引键 `i`、`j` 和 `k` 设置为 `value1`, `value2`, ..., `valueN`。

```bash
animals[0]=Cat
```

数组。刚刚创建的数组如下：`Cat`

让我们向现有的数组添加更多值。

```bash
$ animals=("Dog" "Bear" "Llama" "Parrot" "Otter")
```

由于数组创建和赋值的方式，我们修改数组的操作实际上抹除了（unset）了之前的值，并重置了整个数组为：`animals`

- `0 Dog`
- `1 Bear`
- `2 Llama`
- `3 Parrot`
- `4 Otter`

如果我们想把 `Cat` 值加回数组

对于数组，我们可以将其追加到末尾。

```bash
$ animals+=('Cat')
```

## `animals` 数组现在看起来像这样：

```
animals

- 0 Dog

- 1 Bear

- 2 Llama

- 3 Parrot

- 4 Otter

- 5 Cat
```

如果需要更改某个数组元素，或者添加一个或多个元素，相应的语言结构允许我们进行操作。

```bash
$ animals[1]=Tiger; animals[7]=Chicken
```

这里有两个重要的点需要注意。第一是我们无意中创建了一个稀疏数组。也就是说，`animals` 数组有八个键（记住数组元素是从零开始索引的），但只有七个值。

```
animals

0 Dog

- 1 Tiger

- 2 Llama

3 Parrot

4 Otter

5 Cat

6
```

如果使用循环来计数数组元素，将会有六个位置是空的！这通常不是你想要的结果。

其次，假设你尝试使用这种语法来设置元素：

```bash
$animals([1]="tiger" [7]="chicken")
```

你将取消当前的数组并创建另一个类似于所示的数组：

```
- animals

0

1 Tiger

2

3

4

5

6

7 Chicken
```

这完全不是我们需要的！你可以尝试重新设置整个数组并确定键及其各个属性，但这样做会附加（覆盖）所有内容。

```bash
## 如果需要，则“重置”数组
$ animals=("Dog" "Bear" "Llama" "Parrot"
"Otter" "Cat")
$ animals+=([1]="Tiger" [7]="Chicken")
```

## 数组现在是：

```
animals

- 0 Dog

1 Bear-Tiger

- 2 Llama

3 Parrot

4 Otter

5 Cat

6

7 Chicken
```

如你所见，对数组上执行的每个操作保持谨慎的记录是非常关重要的，以确保结果恰好且精确符合你预期的操作。

注意，添加用户输入的信息是一个简单的重定向问题。在下面的代码中，一个之前输入的用户句子通过“此处字符串”（here string）重定向到数组中。句子将根据默认 `IFS` 设置进行分割，除非在任何情况下另有确定。在这里，记录重定向以及其他操作的工作方式是类似的。

```bash
$ sentence="I'm a user-inputted sentence!"
$ read -a words <<< $sentence
```

让我们将数组“重置”为之前无意创建的数组，并弄如何从中读取值。

```bash
$ animals=("Dog" "Tiger" "Llama" "Parrot" "Otter" "Cat" " "Chicken")
```

从数组中读取因素就像对该数组执行边界扩展。

**获取值的用法**

```bash
${array[i]}
${array[@]} "${array[@]}"
${array[*]} "${array[*]}"
${array[@]:offset:num}
"${array[@]:offset: num }"
```

## `${array[*]:offset:num}`

`"${array[*]:offset:num}"` 描述 展开值

展开为索引数组 `array` 的第 `i` 个值。负数从最高索引键开始倒数计数。

**批量展开值**

展开为数组中的所有值。如果使用双引号，它将展开为数组中每个单独加引号的值。

**批量展开值**

展开为数组中的所有值。如果使用双引号，它将展开为整体加引号的数组所有值。

**子数组展开**

展开从 `offset` 开始的 `num` 个数组值。适用上述相同的引号规则。

读取单个数组元素就像读取字符串中的单个字符，不同的是，对于数组，你应该确定要读取的关键值。

```bash
$ echo "${animals[3]}"
Parrot
```

## 显示 `Parrot` 是因为它与键值 3 相关，而不是 `animals` 数组的第三个元素！

显示 `creatures` 数组的每个元素可以通过几种方式实现，每种方式都有细微的独特。这在起初可能会令人困惑，因为策略的重复结果显示几乎完全相同。

```bash
$ echo "${animals[]]}"
Dog Tiger Llama Parrot Otter Cat Chicken
$ echo "${animals[]]}"
Dog Tiger Llama Parrot Otter Cat Chicken
$ echo "${animals[]]}"
Dog Tiger Llama Parrot Otter Cat Chicken
$ echo "${animals[]]}"
Dog Tiger Llama Parrot Otter Cat Chicken
```

上述主要的区别在于当数组被引用时，`Cat` 和 `Chicken` 属性之间额外的空格（即我们稀疏数组中缺失的第六个元素）。如果我们使用循环，观察结果的变化：

```bash
$ for elem in \${animals[@]}; do echo "\$elem"; done
Dog
Tiger
Llama
Parrot
Otter
Cat
Chicken

# for elem in \${animals[@]}; do
# 产生与上面完全相同的输出
```

## 引用数组显示确实存在差异。`@` 方法产生每个单独的值，经过单词分割并单独加引号。通配符 `*` 产生一个长字符串，其中任何额外的空格（即我们稀疏数组中缺失的元素）都会被截断。

```bash
$ for elem in \${animals[@]}; do echo "\$elem"; done
Dog
Tiger
Llama
Parrot
Otter
Cat
Chicken

$ for elem in \${animals[@]}
the animals array looks like:
0 Dog
1 Tiger
2 Llama
3 Parrot
4 Otter
5 Cat
6
7 Chicken
```

数组通过通过取消（unset）来删除。

## 删除

| 用法 | 描述 |
| :--- | :--- |
| `unset -v array` | 删除数组。 |
| `unset -v array[@]` | 删除数组。 |
| `unset -v array[i]` | 从数组删除第 `i` 个值。 |

## 关联数组

与索引数组（使用从零开始递增的键）不同，关联数组使用字符串标签来关联值。

```
string label
string1
string2
...
anotherstring3
```

```bash
$ unset -v 'animals[2]'
echo "${animals[0]}"
Dog Tiger Parrot Cat Chicken
$ unset -v 'animals'
echo "${animals[0]}"
```

### 扩展值

展开为数组字符串索引的元素，`array`。

### 批量扩展值

展开为数组中的所有值。如果使用双引号，则展开为数组中每个值都被单独引号。输出顺序为随机。

### 批量扩展值

展开为数组中的所有值。如果使用双引号，则展开为数组中所有值的整体引号。输出顺序为随机。

### 元数据用法

```
${#array[str]}
${#array[@]}
${#array[*]}
${!array[@]}
${!array[*]}
```

### 删除

| 使用 |
| :--- |
| `unset -v array` |
| `unset -v array[@]` |
| `unset -v array[*]` |
| `unset -v array[str]` |
| `unset -v array` |
| `unset -v array[@]` |
| `unset -v array[*]` |

### 描述

- **字符串长度**：展开为由 `str` 索引的元素的字符串长度。
- **数组值**：展开为数组中值的数量。
- **数组索引**：展开为数组中的字符串标签。

### 描述

- **擦除数组**：完全删除数组，`array`。
- **擦除数组**：完全删除数组，`array`。删除数组值会从数组中删除由 `str` 索引的元素。

我们首先声明一个关联数组 `stringarr` 并设置几个属性。重复显示展示告诉我们这些属性确实被存起来了。注意它们是如何不规则地返回的？它们并不是按字母顺序排列的！

```bash
$ declare -A stringarr
$ stringarr([weather])="sunny" [temp]="86" [skies]="clear" [activity]="hiking"
$ echo "${stringarr[*]}"
86 sunny hiking clear
```

接下来，我们添加一个字符串名称并检查它是否无疑已被添加。

```bash
$ stringarr[companion]="black lab"
$ for elem in "${stringarr[@]}"; do echo "$elem"; done
86
sunny
black lab
hiking
clear
```

取消设置和添加值显示了关联数组元数据恢复是如何工作的。

```bash
$ unset -v stringarr[temp]
$ echo "stringarr has ${#stringarr[@]} elements."
stringarr has 4 elements.
$ stringarr[season]="autumn"
$ echo "now it has ${#stringarr[@]} elements."
now it has 5 elements.
```

就像字段展示一样，关联数组的字符串标记被有效地恢复并显示，首先作为独立的清单显示，其次作为与其已存储值的值的组合清单显示。

```bash
$ echo "${#stringarr[@]} preferences are set: ${!stringarr[@]}"
5 preferences are set: weather companion activity skies season
```

# 第 7 章：特殊字符

Bash 的一些特殊字符——具有字面意思之外含义的字符——已经介绍，例如双引号和美元符号，但还有更多。虽然不详尽，但大部分已记录在下方。

## 基础

| 字符 | 描述 |
| :--- | :--- |
| `#` | 注释。以 hash 开头的行将不会执行。 |
| `" "` | 空格。Bash 使用空格（例如空格、制表符和换行符）执行单词拆分。 |
| `&` | 后台运行。使前面的命令在后台运行。 |
| `;` | 命令分隔符。允许在同一行放置另一个命令。 |

## 逻辑

| 字符 | 描述 |
| :--- | :--- |
| `&&` | 逻辑与运算符。如果运算符前后的两个条件都为真，则返回成功。 |
| `\|\|` | 逻辑或运算符。如果运算符前后的任意一个条件为真，则返回成功。合法的 AND 管理非常类似于你在其他编程语言或设备/PC/原理课程中学学的逻辑。如果且仅当第一个任务有效完成，它将执行后续任务。Bash 通过检查命令的退出码来判断赋值是否有效完成。稍后在帮助中会给出退出码的详细说明。目前，你真正需要知道的是退出码为 0 表示有效，为其他任何值（通常为 1）表示假。 |

```bash
$ sleep 5 && echo "5 sec pause"
5 sec pause
$ touch newfile && vi newfile
$ mkdir newdir && cd newdir
newdir $
```

逻辑 OR 运算符的工作与 AND 运算符完全相反。当且仅当第一个任务没有成功完成时（即其错误代码不等于 0），它会执行第二个任务。

在这两种情况下，可以将各种 AND 和 OR 组合在一起。

```bash
$ cd somedir || mkdir somedir && cd somedir
bash: cd: somedir: No such file or directory
somedir $
```

尽管这不是良好的实践，但退出码的读取始终是最后一次。这可能会导致意外的行为。

```bash
$ cd otherdir && myscript || echo "Couldn't make a new script file!"
bash: cd: otherdir: No such file or directory
Couldn't make a new script file!
```

等一下！Bash 在任何时候都没有尝试创建文档 `myscript`。它所的是尝试切换到 `otherdir`，但由于索引不存在而失败了。退出码被设置为 1（令人失望），这使得它跳过了 `touch` 操作。当它看到 OR 运算符时，它根据理由执行了那里的命令。

## 目录遍历

| 字符 | 描述 |
| :--- | :--- |
| `~` | 代表主目录。 |
| `.` | 代表当前目录。 |
| `..` | 代表父目录。 |
| `/` | 分隔文件名的组件。 |

## 引用

| 字符 | 描述 |
| :--- | :--- |
| `\` | 转义后续字符并使其以字面形式处理。 |
| `""` | 允许对长命令进行换行拆分。 |

### 全引用

单引号内的特殊字符失去含义并变为字面量。对内容不进行单词拆分。

### 部分引用

双引号内的特殊字符失去含义，但参数扩展、算术扩展和命令替换除外。对内容不进行单词拆分。虽然已经介绍了引用，但有必要再次强调：如果其他都失败了，任何情况下都使用双语句字符串！

```bash
$ filename=pet list
No command 'list' found, did you mean:
Command 'klist' from package heimdall
clients (universe)
$ echo $filename
```

哎。引用处理了这个问题。

```bash
$ echo $filename
pet list
```

但请记住，在发生单词拆分的地方字符串都应该被引用。

```bash
$ touch filename
$ ls
list pet
$ touch 'filename'
$ ls
list pet pet list
$ rm filename
$ ls
pet list
$ rm 'filename'
$ ls
```

双美元符号 (`&&`) 会扩展为当前 shell 的循环 ID。
