
`diff` 命令尝试确定将 `file1` 转换为 `file2` 所需的最小更改集。命令的输出显示了不同的行。上方的代码 `3d2` 表示你需要删除 `file1` 中的第三行，以便文件匹配 `file2`。`d` 表示删除（delete），`3` 表示 `file1` 的第三行，`2` 表示 `file1` 和 `file2` 在不包括第 2 行之前是相同的。代码 `2a3` 表示你需要向 `file1` 添加一行，以便文件匹配 `file2`。`a` 表示向 `file1` 添加行或多行（append）。`3` 表示要从 `file2` 添加第 3 行到 `file1`。`2` 表示该行必须在第 2 行之后添加。

# 第五章 A 节

## 使用 wc 命令

使用 `wc` 命令统计文本文件中行数 `-l`、单词数 选项 `-w` 以及字节数或字符数 选项 `-c`。你可以在命令行中指定指定所有三个选项，即 `-wc`。如果你不带选项输入命令，将按顺序看到行、单词和字符的计数。你可以使用 `wc` 命令统计新文件 `counters` 的行数。

创建一个文件并统计行数：

1. 在 `$` 命令提示符后，输入 `cat > counters` 并按回车。
2. 输入此文本，并在每行末尾按回车：
   Linux is a full featured UNIX clone.
   Linux blends the best of BSD and Sys V.
3. 输入 Ctrl+D。
4. 要查找 `counters` 中的行数，输入 `wc -l counters` 并按回车。UNIX 报告该文件包含行。
5. 要查找 `counters` 中的字节数，输入 `wc -c counters` 并按回车。UNIX 报告该文件包含 77 字节。
6. 要查找 `counters` 中的单词数，输入 `wc -w counters` 并按回车。UNIX 报告该文件包含 16 个单词。
7. 要统计 `counters` 中的单词、字符和行，输入 `wc -lwc counters` 并按回车。UNIX 报告行 (2)、单词 (16) 和字节 (77) 的计数。

## 使用处理和格式命令

除了你在第四章中使用的处理和格式命令外，你还可以使用 `sed`、`tr` 和 `pr` 命令在显示或打印数据之前编辑并转换数据的外观。

### 引入 sed

当你想要对大文件进行全局更改时，你需要一种不同于 `vi` 和 `Emacs` 等交互式编辑器的工具。另一种 UNIX 编辑器 `sed` 专为该目的设计。运行 `sed` 的最低要求是一个输入文件和一个命令。

### 高级文件处理

#### 语法

```
sed [options] 'command' file[s]
sed [options] -f file[s]
```

#### 选项

- 第一种形式允许你在命令行上指定命令。
- 第二种形式允许你指定脚本文件。

#### 使用 sed 进行处理：

1. 要创建一个新文件 `counters`，输入 `cat > counters` 并按回车。
2. 输入此文本，并在每行末尾按回车：
   Linux is a full featured UNIX clone.
   Linux blends the best of BSD and Sys V.
3. 输入 Ctrl+D。
4. 要查找 `counters` 中的行数，输入 `wc -l counters` 并按回车。UNIX 报告该文件包含两行。
5. 要查找 `counters` 中的字节数，输入 `wc -c counters` 并按回车。UNIX 报告该文件包含 77 字节。
6. 要查找 `counters` 中的单词数，输入 `wc -w counters` 并按回车。UNIX 报告该文件包含 16 个单词。
7. 要统计 `counters` 中的单词、字符和行，输入 `wc -lwc counters` 并按回车。UNIX 报告行 (2)、单词 (16) 和字节 (77) 的计数。

#### 使用 sed 删除：

1. 要创建一个新文件 `counters`，输入 `cat > counters` 并按回车。
2. 输入此文本，并在每行末尾按回车：
   Linux is a full featured UNIX clone.
   Linux blends the best of BSD and Sys V.
3. 输入 Ctrl+D。
4. 要查找 `counters` 中的行数，输入 `wc -l counters` 并按回车。UNIX 报告该文件包含两行。
5. 要删除 `counters` 中的第 3 行和第 4 行，输入 `sed '3,4d' counters` 并按回车。注意：第 3 行和第 4 行并没有真正从文件中删除，只是被过滤掉了不再显示。

#### 使用 sed 附加：

1. 要创建一个新文件 `counters`，输入 `cat > counters` 并按回车。
2. 输入此文本，并在每行末尾按回车：
   Linux is a full featured UNIX clone.
   Linux blends the best of BSD and Sys V.
3. 输入 Ctrl+D。
4. 要创建一个脚本文件 `more_stuff`，输入 `cat > more_stuff` 并按回车。
5. 输入以下文本，并在每行末尾按回车：
```
$Sa$
```
6. 按 Ctrl+D。
7. 使用 `sed` 命令运行脚本文件，输入 `sed -f more_stuff counters` 并按回车。

多年来，公司已经在 UNIX 系统上安装了它们的 RDBMS 软件包。

5. 使用 `vi` 创建文件 `stuff_replace`。在文件中插入以下 `sed` 命令：
```
s/UNIX/Linux/
s/abandoned/given up/
s/standard/regular/
```
6. 使用你在第 5 步创建的脚本文件对 `unix_stuff` 文件执行 `sed`。将 `sed` 的输出重定向到文件 `unix_stuff2`。输入 `sed -f stuff_replace unix_stuff > unix_stuff2` 并按回车。
7. 输入 `cat uniq_stuff2` 并按回车。你会看到带有 `stuff_replace` 脚本文件所指定更改的文件。

### 使用 tr 命令翻译字符

`tr` 命令从标准输入复制数据到标准输出，并根据选项和模式替换或删除字符。模式可以是字符串和字符集。

#### 语法

```
tr [options] string1 string2
```

- 在最简单的形式，`tr` 将 `string1` 中的每个字符翻译为 `string2` 中对应位置的字符。这些字符串可能需要用单引号或双引号进行“引用”。
- 最常用的两个选项是 `-d`（删除字符）和 `-s`（替换字符）。

`tr` 的一个常用用法是将小写字母转换为大写字母。你可以通过指定 `[a-z]` 为小写字母并将 `[A-Z]` 为大写字母，将 `counters` 文件中的小写字母转换为大写字母。

#### 将 counters 文件中的小写字母转换为大写字母：

- 在 `$` 命令提示符后，输入 `tr [a-z] [A-Z] < counters` 并按回车。

你会看到这些行：
```
LINUX IS A FULL FEATURED UNIX CLONE.
LINUX BLENDS THE BEST OF BSD AND SYS V.
```

你也可以使用 `tr` 命令的 `-d` 选项从输出中删除 `string1` 中找到的输入字符。当你需要从文件中删除错误字符时，这很有帮助。

从 counters 文件中删除指定的字符：

- 要从输出中删除字符“full”，输入 `tr -d "full" < counters` 并按回车。

你会看到这段文本：
Linx is a eatred o cone.
Linx bends the best BSD and Sys V.

注意，该命令删除了输出中“full”中的所有字符——每个 f、u 和 l——而不是单词“full”出现。

`tr` 命令的 `-s` 选项检查 `string1` 字符连续重复的序列。当发生这种情况时，`tr` 将重复字符序列替换为 `string2` 中对应字符的一个实例。例如，当你需要将平面文件的字段分隔符从一个字符更改另一个字符时，使用 `-s` 选项。例如，在 `zoo02` 文件中，使用 `tr` 将字段分隔符 ":" 替换为 " "首先使用 `cat` 显示文件。

#### 替换 counters 文件中的字符：

1. 在 `$` 命令提示符后，输入 `cat zoo02` 并按回车。
你会看到这段文本：
Monkeys:Bananas:2000:850.00
Lions:Raw Meat:4000:1245.50
Camels:Vegetables:2300:564.75
Elephants:Hay:120000:1105.75
2. 输入 `tr -s ":" " " < zoo02` 并按回车。
你会看到这段文本：
Monkeys Bananas 2000 850.00
Lions Raw Meat 4000 1245.50
Camels Vegetables 2300 564.75
Elephants Hay 120000 1105.75

### 使用 pr 命令格式化你的输出

`pr` 命令以分页的形式在标准输出上打印指定的文件。如果你不指定任何文件，或者指定文件名为 "-"，它将读取标准输入。

#### 高级文件处理

默认情况下，`pr` 将指定的文件格式化为每页 66 行的单列页。每页都有五行页头，默认包含当前文件名、其最后修改日期、当前页码以及一个由空行组成的五行页脚。

#### 语法

```
pr [options] [file...]
```

#### 解析

- 最常用的三个选项是 `-h`（页头格式），允许你自定义页头行；`-d`，输出双倍空格；以及 `-l n`，设置每页行数。

使用 `pr` 格式化 `unix_stuff` 文件。使用管道运算符 (`|`) 将输出发送到 `more`，这样输出屏幕就不会快速闪过。

#### 格式化文件：

你会看到这段文本：
```
99-11-22 02:35
Page 1
UNIX Files & Databases
```
尽管 UNIX 支持其他数据库系统，但 UNIX 从未放弃过使用平面文件的想法。平面文件是基于标准 ASCII 的纯文本。平面文件可以被任何操作系统读取。

现在你可以输入命令，但添加 `-l 23` 选项将每页行数限制为 23。因为显示器上的标准行数是 24，所以你不需要将输出重定向到屏幕保持。

- 输入 `pr -l 23 -h "UNIX Files & Databases" unix_stuff` 并按回车。

你会看到这段文本：
```
99-11-22 02:35
UNIX Files & Databases
```
尽管 UNIX 支持其他数据库系统，但 UNIX 从未放弃过使用平面文件的想法。平面文件是基于标准 ASCII 的纯文本。平面文件可以被任何操作系统读取。

## 第5章，A节

### 总结

| 命令 | 目的 | 选项 |
| :--- | :--- | :--- |
| comm | 比较两个文件 | -s |
| diff | 比较两个文件 | -l |
| grep | 选择行 | -i |
| pr | 格式化文件 | -h, -d |
| sed | 编辑文本 | -f |
| tr | 翻译字符 | -d, -s |
| wc | 计数数量 | -c, -l |

### 复习

1. `pr` 命令产生
   a. cat 输出
   b. less 的输出
   c. 分页输出到
   d. 分页输出到标准输出
2. `tr` 命令复制
   a. 输入到文件
   b. 输出到文件
   c. 输入来自文件
   d. 输出来自文件
3. `diff` 命令报告
   a. 唯一行
   b. 之间的
   c. 行中的
   d. 行中的
4. `comm` 命令处理
   a. 同时处理两个文件
   b. 一个文件
   c. 多个文件
   d. 行中的
5. `-h` 选项是
   a. 页头格式
   b. 页头行
   c. 输出双倍空格
   d. 每页行数
6. 哪些命令的输出会将每个冒号替换为空格？
   a. sed ":" < filename
   b. tr -s ":" " "
   c. awk -F: ' '
   d. tr -s ":" filename
7. 哪些命令的输出将删除所有冒号？
   a. sed -d ":" < filename
   b. tr -d ":" <filename
   c. tr -d: filename
   d. tr -d " " filename
8. 在 `sed` 中，使用该选项添加新行。
   a. /a
   b. $/a
   c. add
   d.
9. 哪些命令将文件中的字符转换为大写？
   a. tr [a-z] [A-Z] < filename
   b. tr "[a-z]" "[A-Z]" < filename
   c. tr "[A-Z]" "[a-z]" < filename
   d.
10. 管道运算符 (`|`) 用于
    a. 重定向输出到文件
    b. 重定向输出到屏幕
    c. 重定向输入来自文件
    d. 将一个命令的输出重定向到另一个命令的
11. 命令 `Bob* /home/jill/members` 执行什么
    a. 搜索当前目录下所有以 Bob 开头且包含 /home/jill/members 字符串的文件。显示这些行。
    b. 搜索文件 /home/jill/members 中包含 Bob 后跟任何字符的行。显示这些行。
    c. 将所有以 Bob 开头的的文件存储在 /home/jill/members 文件中。
    d. 以上都不是。
12. 哪个命令在屏幕上显示当前目录下名称包含 "jimmy" 的文件名？
    a. ls l grep jimmy
    b. ls l sort jimmy
    c. ls l tr jimmy
    d. sed jimmy | ls

### 练习

- 14. `wc` 命令统计
  a. 单词
  b. 行
  c. 字符
  d. 以上所有

# 探索性练习

- 1. 创建一个新文件 `your_list`，并在文件中输入以下行：
Radio
Camera
Boat
使用 `sed` 命令选项将这些行加到 `your_list` 的末尾：
Television
Computer
Stereo
- 2. 使用 `tr` 命令删除 `/etc/passwd` 文件中的所有冒号，并将结果显示在屏幕上。
- 3. 将 `your_list` 文件中的单词 "Radio" 替换为 "Canoe"，并将显示结果发送到标准输出。
- 4. 使用 `cat` 命令创建文件 `animals`，其中包含以下行：
Dog
Cat
Horse
Frog
接下来，使用 `sed` 命令将单词 "Cat" 改为 "Kitten"。
- 5. 在你在探索练习 4 中创建的文件上编写并运行一个 `sed` 脚本。脚本应将 "Dog" 改为 "Puppy"，并将 "Frog" 改为 "Tadpole"。

## 课程 B

### 目标

学习本节后，你应该能够：
- 设计一个新的文件处理应用程序
- 设计并创建文件以实现该应用程序
- 使用 `awk` 生成格式化输出
- 使用 `cut`、`sort` 和 `join` 组织和转换特定的文件信息
- 开发自定义 shell 脚本来提取合并文件数据
- 测试单个 shell 脚本，并将所有脚本合并成最终的 shell 程序

## 使用 UNIX 文件处理工具创建应用程序

### 设计一个新的文件处理应用程序

开发新应用程序最重要的阶段是创建设计。设计定义了应用程序产生所需的信息。设计还定义了如何将这些信息组织成文件、记录和字段，这些都是逻辑结构，因为每个结构都代表一个逻辑实体，例如工资文件、员工薪酬记录或员工社会安全字段。文件由记录组成，记录由字段组成。

现在你准备好为 Dominion Consulting 公司创建“程序员活动状态报告”了。该报告将显示程序员的姓名以及每个程序员负责的项目数量。从设计和创建包含记录和字段的文件开始，然后使用高级的文件处理命令来选择、处理和格式化报告中的信息。

### 设计记录

设计阶段的第一项任务是定义记录中的字段。这些定义以记录布局的形式出现，通过名称和数据类型（如数值或非数值）来标识每个字段。定义设计文件，仅存储与记录主要目的相关的字段。例如，Dominion Consulting 公司需要两个文件：一个用于程序员信息，另一个用于项目信息。在程序员记录中包含一个程序员姓名的字段，在项目文件记录中包含一个项目描述字段。不要在项目文件中存储程序员姓名，即使程序员可能被分配到该项目中。相反，不要在程序员文件中存储项目名称。

只为记录的必要字段分配所需的空间可以保持记录简洁明了。短记录就像短句一样，更容易理解。同样地，你的应用程序越简单，性能就越好。然而，请确保包含一个能够唯一标识文件中每条记录的字段。例如，程序员记录包含一个程序员编号字段，以区分可能同名的程序员。

注意：程序员文件记录中的程序员编号字段应该是数值。在唯一标识记录时，数值字段优于非数值字段，因为计算机解释数字的速度比非数值字段快。项目记录可以使用非数值项目代码来唯一标识每个项目记录，因为 Dominion 的项目代码包含字母和数字（如 EA-100）。

### 通过键链接文件

多个文件通过“键”连接——“键”是每个链接文件都共享的公共字段。设计阶段的另一个重要任务是计划一种连接文件的方法（如果需要）。例如，程序员-项目应用程序使用程序员编号将程序员与项目文件链接。在项目记录中添加程序员编号字段，将程序员与项目连接起来。
