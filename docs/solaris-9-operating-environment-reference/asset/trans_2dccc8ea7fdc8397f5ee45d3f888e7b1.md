

# 1298

它们已附加。它们通过字段开始（field-start）、字段结束（field-end）或两者指定了这种效果。如果任何修饰附加到字段开始或字段结束，则任何选项都不适用于其中任何一个。

当存在多个键字段时，后面的键只有在前面的键比较相等后才会进行比较。除非指定了 -u 选项，否则另有比较，排序将按照未出现 -d、-f、-i、-n 或 -k 参数的状态（但如果你指定了 -r，则 -r 仍然有效，并包含比较行段中的所有字节）。

以下表示法定义了一个键字段，它从 `field-start` 开始并在 `field-end` 结束（包含该位置），除非 `field-start` 超过了行尾或 `field-end` 的位置，在这种情况下，键字段为空。

```
-k field-start[type] [,field-end[type]]
```

缺少 `field-end` 意味着行的最后一个字符。

一个字段由非分离字符的最长序列组成，在没有指定 `-t` 的情况下，由任何之前的分隔符组成。

`keydef` 选项的字段开始部分形式为：
field-number{.first-character}

字段以及字段内的字符从 1 开始计数。`field-number` 和 `first-character` 被解释为正整数，指定作为键部分的第一个字符。如果省略 `.first-character`，默认是字段的第一个字符。

`keydef` 选项的字段结束部分形式为：
field-start{.last-character}

上述 `field-number` 和 `last-character` 被解释为非负整数，指定作为键部分的最后一个字符。如果 `last-character` 结果为 0 或省略，默认是 `field-number` 指定字段的最后一个字符。

如果 `-o` 类型修饰有效，字段内的字符从字段中的第一个空白字符开始计数（这分别适用于 `first-character` 和 `last-character`）。

以下语法已废弃：
+pos1[-pos2]

它提供了等同于 `-k keydef`的功能。

`pos` 和 `pos2` 的形式为 `m` 后跟一个或多个字段中的第 `n+1` 个字符。由 `+m.n` 指定的位置解释为字段中的第 `n+1` 个字符。如果 `-b` 选项有效，`n` 从字段中的第一个空白字符开始计数；`+m.0` 指向字段中的第一个空白字符。

由 `-m.n` 指定的位置解释为字段（包括分隔符在内）的第 `n` 个字符。如果 `-b` 选项有效，`n` 从字段中的最后一个空白字符开始计数；`-m.1` 指向字段中的第一个空白字符。

完全指定的 `+pos1 -pos2` 带有 `T` 和 `U` 修饰符的形式为：
```
+w.XT -Y.zu
```

等同于：*

# sort

# 1299

未定义（z=0 且包含 b -t）
-k w+1.x+1T,y.OU（否则 z=0）
-k w+1.x+1T,y+1.ZU（z > 0）

实现 sort 键（`-k` 选项和废弃的 `+pos1 -pos2`）在命令行顺序中是显著的。如果你没有指定 `sort` 键，则使用整行的默认排序键。

# 操作数

file 要排序、合并或检查的文件路径。如果你没有指定文件或文件操作数为 `-`，则使用标准输入。

# 用

参见 `largefile(5)` 以了解 sort 在遇到大于或等于 2GB（2^31字节）的文件时的行为。

# 示例

以下示例使用 `sort -M` 命令按月份排序文件。注意列表中不是月份的名字，那些与月份字母相同的名称会干扰 sort 命令。它们与月份按字母顺序排序，并被推到列表顶部。

```
castle% cat sortmonth
Janice
Maris
March
July
February
December
April
January
Ray
Fred
Juno
castle% sort -M sortmonth
Fred
Ray
Janice
January
February
March
Maris
April
June
Juno
July
December
castle%
```

以下示例显示了名为 `sortnum` 的文件的内容，不使用 `-n` 选项进行排序，然后使用 `-n` 选项进行排序。

# 1300 sort

```
castle% cat sortnum
2000
1998
1999
1
10
40
20
3
2
```

```
castle% sort sortnum
1
10
1998
1999
2
20
2000
3
40
```

```
castle% sort -n sortnum
1
2
3
10
20
40
1998
1999
2000
castle%
```

以下示例展示了非废弃和废弃的指定指定方法，有助于理解两种形式之间的关系。以下任何命令都会以第二个字段作为键对 `infile` 内容进行排序。

```
castle% sort -k 2,2 infile
castle% sort +1 -2 infile
castle% sort -k 2,2 kookaburra-1
```

吃掉他能看到的所有糖果。笑吧，kookaburra，笑吧，kookaburra。停下，kookaburra，停下，kookaburra。他是森林里快乐的国王。kookaburra 坐在老胶胶树上。kookaburra 坐在老胶胶树上。那里给我留一些。生活必须是快乐的。
castle%

# sort

# 1301

以下任何命令都会以反序排序 `infile` 和 `infile2` 的内容，将输出放在 `outfile` 中并将第二个字段的第二个字符作为排序键（假设第二个字段的第一个字符是字段

```
castle@ sort -r -o outfile -k 2.2.2 infile infile2
castle@ sort -r -o outfile +1.1 -1.2 infile infile2
castle@ sort -r -o outfile -k 2.2.2 kookaburra-1
castle@ cat outfile
```

生活必须是快乐的。
给我留一些。kookaburra 坐在老胶胶树上。kookaburra 坐在老胶胶树上。他是森林里快乐的国王。停下，kookaburra，停下，kookaburra。吃掉他能看到的所有糖果。笑吧，kookaburra，笑吧，kookaburra。

+8 给我留一些。
7 停下，kookaburra，停下，kookaburra。
6 吃掉他能看到的所有糖果。
5 kookaburra 坐在老胶胶树上。
4 生活必须是快乐的。
3 笑吧，kookaburra，笑吧，kookaburra。
2 他是森林里快乐的国王。
1 kookaburra 坐在老胶胶树上。

以下任何命令都会对 `infile` 和 `infile2` 的内容进行排序，第二个字段的第二个字符作为排序键（当 `-b` 类型有效时）。

```
castle@ sort -k 2.2b, 2.2b infile2
castle@ sort +1.1b -1.2b infile infile2
castle@ sort -k 2.2b, 2.2b kookaburra-1
```

生活必须是快乐的。
给我留一些。kookaburra 坐在老胶胶树上。kookaburra 坐在老胶胶树上。他是森林里快乐的国王。停下，kookaburra，停下，kookaburra。吃掉他能看到的所有糖果。笑吧，kookaburra，笑吧，kookaburra。

如果 `-o` 或 `b` 类型修饰有效，字段内的字符从字段中的第一个空白字符开始计数（这分别适用于 `first-character` 和 `last-character`）。

castle@

以下任何命令都会将 `passwd(4)` 文件（用户数据库）按数字用户 ID（第三个冒号分隔的字段）进行排序。

```
castle sort -t : -k 3
```

以下任何命令都会打印已排序的 `infile` 的行，抑制具有相同第三字段的所有重复行。

```
castle sort -um -k 3.1,3.0 infile
castle sort -um +2.0 -3.0 infile
```

castle sort -um -k 3.1,3.0 kookaburra-1
ookaburra 坐在老胶胶树上。
他是森林里快乐的国王。笑吧，kookaburra，笑吧，kookaburra。
生活必须是快乐的。

kookaburra 坐在老胶胶树上。
吃掉他能看到的所有糖果。
停下，kookaburra，停下，kookaburra。
那里给我留一些。

# 环境变量

参见 `environ(5)` 以了解影响 sort 执行的以下环境变量的描述：LC_COLLATE, LC_MESSAGES, NLSPATH。

+   LC_TYPE 确定将文本字节序列解释为字符的区域（例如参数和输入文件中的单字节与多字节字符）以及 -b、-d、-f、-i 和 -n 选项的行为分类。

+   LC_NUMERIC 确定 -n 选项中基数字符和千位分隔符的定义。

