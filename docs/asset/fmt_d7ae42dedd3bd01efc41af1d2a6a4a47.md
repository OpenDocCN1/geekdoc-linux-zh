
### 清单 593 - 使用 John the Ripper 变换密码

由于对密码进行了多次变换，生成的文件包含超过 46,000 个密码条目。其中一个密码是 `"Nanobot93"`，与我们在假设评估中之前发现的密码相匹配。根据对 MegaCorp One 密码政策的假设，此词表可以在字典攻击中产生结果。

虽然这个演示过于简化，但它是一个很好的例子，说明了密码分析如何有助于整体密码攻击的成功。

#### 19.1.1.1 练习

*（此练习不需要提交报告）*

1. 使用 `cewl` 从您的公司、学校或最喜欢的网站生成自定义词表并检查结果。您的任何密码是否出现在结果中？

## 19.2 暴力破解词表

与字典攻击相反，*暴力破解密码攻击*会计算并测试构成密码的每一个可能的字符组合，直到找到正确的那个。虽然这听起来像是一种保证结果的简单方法，但它极其耗时。根据密码的长度和复杂度以及测试系统的计算能力，暴力破解一个强密码可能需要很长时间，甚至数年。

我们还可以结合这两个概念，创建*暴力破解词表*，即包含所有匹配特定模式的密码的字典文件。

例如，考虑一个揭示非常具体的密码强制策略的场景，如清单 594 所示：

```bash
kali@kali:~$ cat dumped.pass.txt

david: Abc5#123

mike: Jud()666

Judy: H0l&278
```

### 列表 594 · 密码转储示例

观察这些密码，我们注意到密码结构中存在以下模式：

```
[大写字母] [2 个小写字母] [2 个特殊字符] [3 个数字]
```

### 列表 595 · 密码结构

基于这一知识，创建一个包含所有符合此模式的可能的密码的词表将非常有帮助。Kali Linux 自带的 `Crunch`（557）是一个强大的词表生成器，可以处理这项任务。

首先，我们必须描述需要 `crunch` 复制的模式，为此我们将使用占位符来代表特定类型的字符：

| **占位符** | **字符映射** |
| :-------------: | :-----------------------: |
|        @        | 小写字母字符 |
|        ,        | 大写字母字符 |
|        %        | 数字字符         |
|        ^        | 包括空格在内的特殊字符 |

### 列表 596 · 字符映射格式

为了生成符合我们要求的词表，我们将指定单词的最小和最大长度为八个字符（`8 8`），并使用 `-t ,@%^%%` 描述我们的规则模式。

```bash
kali@kali:~$ crunch 8 8 -t ,@%^%%
Crunch will now generate the following amount of data: 17226237600 bytes
164282 MB
160 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 19140264000
Aaa!!000
Aaa!!001
Aaa!!002
Aaa!!003
Aaa!!004
...
```

### 列表 597 · 使用 crunch 生成密码列表

命令按预期工作，但如前所述，输出将占用 160 GB 的庞大磁盘空间！请记住，暴力破解技术优先考虑密码覆盖率，而牺牲速度，在本例中还包括磁盘空间。

我们还可以使用 `crunch` 定义字符集。例如，我们可以创建一个暴力破解词表，考虑到长度为四到六个字符（`4 6`）的密码，仅包含字符 `0-9` 和 `A-F`（`0123456789ABCDEF`），并且我们将输出写入文件（`-o crunch.txt`）。

```bash
kali@kali:~$ crunch 4 6 0123456789ABCDEF -o crunch.txt
Crunch will now generate the following amount of data: 124059648 bytes
118 MB
0 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 17891328
crunch: 100% completed generating output
kali@kali:~$ head crunch.txt
0000
0001
0002
0003
0004
0005
0006
0007
0008
```

### 列表 598 - 使用 crunch 以特定字符集生成密码

请注意，文件输出大小比之前的示例小得多，主要原因是密码长度较短以及字符集有限。然而，词表文件令人印象深刻，包含超过 1700 万个密码：

```bash
kali@kali:~$ wc -l crunch.txt
17891328 crunch.txt
```

### 列表 599 - 统计生成的密码数量

此外，我们可以根据预定义的字符集（如 `/usr/share/crunch/charset.lst` 中定义的那些）生成密码。例如，我们可以指定字符集文件的路径（`-f /usr/share/crunch/charset.lst`）并选择混合字母集 `mixalpha`，它包含所有小写和大写字母：

```bash
kali@kali:~$ crunch 4 6 -f /usr/share/crunch/charset.lst mixalpha -o crunch.txt
Crunch will now generate the following amount of data: 140712849920 bytes
134193 MB
131 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 20158125312
```
