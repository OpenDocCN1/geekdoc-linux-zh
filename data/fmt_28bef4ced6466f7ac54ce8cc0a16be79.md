
`Crack7` 被编写为使用`libdes`。因此，如果你打算使用这个实用程序，你可能希望先按照*准备 Crack*中第 320 页关于`crypt(3)`的描述编译`libdes`。如果你不想使用`libdes`，请通过注释掉对`libdes`的引用并取消注释对`crypt`的引用来修改`extra`子目录中的`Makefile`。一旦你根据自己的需要修改了`Makefile`，切换到`extra`子目录并执行`make`来构建暴力破解程序。然后如示例 12-16 所示运行`Crack7`。你多久能看到`guest1`作为`guest`账户的密码？

### 示例 12-16 运行 Crack7

```
# cd /usr/src/c50a/extra
# ./Crack7 S2v0Sq2Oxx1U2
make: Nothing to be done for `all'.
brute: ciphertext: S2v0Sq2Oxx1U2
brute: set 0: a-z0-9 -> '0123456789abcdefghijklmnopqrstuvwxyz'
brute: ciphertext: S2v0Sq2Oxx1U2
brute: set 0: a-z0-9 -> '0123456789abcdefghijklmnopqrstuvwxyz'
brute: set 1: a-z0-9 -> '0123456789abcdefghijklmnopqrstuvwxyz'
..
.. <大量输出被省略> ...
brute: guessed S2v0Sq2Oxx1U2 == 'guest1'
```

## Crack 规则

`Crack`用于改变（或者，正如`Alec Muffett`在他的文档中亲切地称之为“mangle”）`Crack`字典中单词的规则，由`dict/dictrun.conf`文件控制。我们之前在第 317 页的表 12.3 中提到了这个文件。

默认`dictrun.conf`文件的部分列表在示例 12-17 中提供。当`cracker`程序运行时，它按给定顺序处理此文件。该文件中的条目有三种格式：

- `dictionary-tag::rulefile`

- `dictionary-tag::!command`

- `::!command`

我们之前在第 321 页的 Crack 字典中查看过字典标签，发现它们定义在`conf/dictgrps.conf`文件中。此外，我们在那里注意到`Crack`构建两个内部字典——`gecos`和`gcperm`。

### 示例 12-17 部分 dictrun.conf 文件

```
###
# 首先，'total feedback' 运行。
###
: |awk -F ' {print $NF}' run/F-merged | sort | uniqi 2>/dev/null
###
# 对字典应用连续的 conf/rules.foo 文件
###
gecos:conf/rules.fast
gcos:conf/rules.basic
gecos:conf/rules.perm1
gecos:conf/rules.perm2
gecos:conf/rules.prefix
....
<文件的其余部分被省略>
gcperm:conf/rules.perm3
gcperm:conf/rules.perm4

1:conf/rules.fast
1:conf/rules.basic
1:conf/rules.perm1
1:conf/rules.perm2
1:conf/rules.prefix
1:conf/rules.suffix

# 这是一个有趣的：
# 使用 'sed' 从字典 '1' 中选择并将 "two" 修改为 "2"
1: | sed -ne 's/two/2/gp'

....
<文件的其余部分被省略>

# 生成一个耗时的字典 'a' -> 'zzzzzzzz' - 缓慢！
#: | perl -e '$$="a"; print $$+;\n' while (length($$) < 9);'
```

语法`dictionary-tag::rulefile`使由`dictionary-tag`标识的字典组中的每个单词都按照`rulefile`中给出的规则进行变形（规则文件在下一节中讨论）。在示例 12-17 中，我们看到代表性样本`1:conf/rules.fast`，这导致标记为`1`的字典组中的所有单词按照`$CRACK_HOME/conf/rules.fast`中找到的规则进行变化。

语法`dictionary-tag::command`使由`dictionary-tag`标识的字典组中的每个单词按照`::`后面的命令进行变化。在示例 12-17 中，我们看到代表性样本：

```
1: | sed -ne 's/two/2/gp'
```

这导致字典组`1`中的每个单词都通过`sed`脚本进行变形（该脚本将单词 "two" 替换为 "2"）。

最后，语法`::command`为`cracker`程序提供猜测流。在示例 12-17 中，我们看到代表性样本：

```
: |awk -F ' {print $NF}' run/F-merged | sort | uniqi 2>/dev/null
```

这会导致`cracker`检查先前猜测过的密码（有关`run/r5-merged`及其他运行时文件的讨论，请参阅第 326 页的*“优雅终止破解”*）。

请注意，第 331 页示例 12-17 中的最后两行建议使用`Perl`脚本执行对长度不超过 8 个字符的所有可能字母排列进行搜索。

通常，如果您需要对字典单词执行多个字符替换、排列或其他变体，请在`dictrun.conf`文件中使用`sed`或`perl`或其他类似实用程序。虽然这类变体也可以在规则文件中实现，但通常将这些类型的变体配置在`dictrun.conf`文件中可能更简单。另一方面，如果您希望对字典单词执行单字符操作，则需要使用规则文件。

### 规则文件

标准`Crack`发行版中包含大量规则文件。您可以在`conf`子目录中找到它们，它们都以`rules`为前缀命名（本节末尾讨论的`globrule.conf`是一个显著的例外），以方便使用。我们在示例 12-17 中看到了一些这些文件的引用。

在示例 12-18 中，我们看到了规则文件的一个代表性实例——在本例中为`rules.permi`。在此文件中，我们看到了一系列相似的规则。例如，条目`/is1i1`表示，如果单词中出现了字符`i`，则将单词中所有的`1`替换为字符`i`，并将单词中的所有其他字符设置为小写。

#### 示例 12-18 rules.permi 文件

```
/asa2l
/asa4l
/osa3l
/hsh4l
/is1i1
/oso0l
/sss5l
```

在表 12.5 中，我们展示了规则文件的一般语法。该语法相当晦涩，需要一些时间才能熟悉。

#### 表 12.5 规则文件语法

| 运算符 | 描述 |
| :--- | :--- |
| `:` 或空格 | 无操作（no-op）指示符。用于提高规则文件中的清晰度。当看到单词“space”时，实际上使用的是空格键，而非该单词本身。`:` 与之等效，并增加了视觉清晰度。 |
| `?c` | 指定字符类。参见第 334 页的表 12.7。 |
| `^x` | 将字符 `x` 作为前缀添加到单词。 |
| `$x` | 将字符 `x` 作为后缀添加到单词。 |
| `r` | 反转单词中字符的顺序。 |
| `u` | 强制将单词中所有字母字符大写。 |
| `l` | 强制将单词中所有字母字符小写。 |
| `p` | 根据英语语法规则将单词变为复数形式。 |
| `c` | 将单词的第一个字符大写，并将所有其他字符设置为小写。 |
| `C` | 将单词的第一个字符设置为小写，并将剩余字符设置为大写。 |
| `t` | 更改单词中每个字符的大小写。 |
| `d` | 将单词的副本附加到其自身。 |
| `†` | 反转单词并将其附加到自身。 |
| `sxy` 或 `s?cy` | 将字符 `x` 的每个实例替换为字符 `y`，或将单词中找到的字符类 `c` 中的每个字符替换为字符 `y`。 |
| `/x` 或 `/?c` | 除非字符 `x` 出现在单词中，或字符类 `c` 中的一个或多个字符出现在单词中，否则拒绝该单词。 |
| `\x` 或 `\?c` | 如果包含字符 `x` 或字符类 `c` 中的一个或多个字符，则拒绝该单词。 |
| `<n` | 除非单词长度小于 `n` 个字符，否则拒绝该单词。 |
| `>n` | 除非单词长度大于 `n` 个字符，否则拒绝该单词。 |
| `xm` | 从字符 `n` 开始提取单词中长度为 `m` 的子字符串。 |
| `onx` | 将字符 `x` 替换为单词中的第 `n` 个字符。不会执行边界检查，因此仅在适当的情况下与 `<` 或 `>` 一起使用此选项。 |
| `inx` | 在单词的第 `n` 个位置插入字符 `x`，并将所有其他字符向右移动一个位置。 |
| `=nx` 或 `=n?c` | 除非第 `n` 个字符是 `x` 或属于类 `c` 的成员，否则拒绝该单词。 |
