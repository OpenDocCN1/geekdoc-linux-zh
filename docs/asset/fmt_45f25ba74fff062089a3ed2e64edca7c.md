
## 命令行 - 输入

```
ubuntu $ | grep -r [AE]S test
```

该命令返回一个如下所示的结果。结果包含了带有 AS 或 ES 的行。

## 命令行 - 响应

```
test/test_sub/sample_2.txt:I like the GRAPES
test/test_sub/sample_2.txt:I like the BANANAS
test/test_sub/sample_2.txt:He likes the GRAPES
test/test_sub/sample_2.txt:He likes the BANANAS
test/test_sub/sample_2.txt:She likes the GRAPES
test/test_sub/sample_2.txt:She likes the BANANAS
```

### `[]` : 匹配不包含的任意内容

`[^]` 定义了匹配不包含在括号内的任意字符。例如，要搜索包含 "es" 但排除 "kes","ges" 和 "pes" 的行，请运行以下命令。

## 命令行 - 输入

```
ubuntu $ | grep -r [^kg]es test
```

结果将如下所示。

## 命令行 - 响应

```
test/sample_1.txt:I likes apples and he likes oranges
test/sample_1.txt:I likes bananas and she likes apples
test/sample_1.txt:He likes apples and she likes oranges
test/sample_1.txt:He likes bananas and I like apples
test/sample_1.txt:She likes apples and I likes oranges
test/sample_1.txt:She likes bananas and he likes apples
```

### `.` : 匹配任意内容

`.` 定义了匹配任意内容的单个字符。例如，搜索以 `.` 结尾的行。

## 命令行 - 输入

```
ubuntu $ | grep -r .
```

## 命令行 - 响应

```
test/sample_1.txt:I likes apples and he likes oranges
test/sample_1.txt:I likes bananas and she likes apples
test/sample_1.txt:He likes apples and she likes oranges
test/sample_1.txt:He likes bananas and I like apples
test/sample_1.txt:She likes apples and I likes oranges
test/sample_1.txt:She likes bananas and he likes apples
```

### `-o` 选项

当你有两个搜索标准时，可以使用 `-o` 选项连接搜索名称。它的作用类似于逻辑或（OR）函数。

如果你想查找两个不同的文件名，需要在 `-o` 选项之前和之后都添加 `-name` 选项。以下是用于搜索名为 `test` 或 `test_sub` 文档的命令示例。

## 命令行 - 输入

```bash
ubuntu | find -name test -o -name test_sub
```

## 通配符

当你忘记文件或目录的确切名称时，通配符非常有用。请参阅下一节了解如何在 `find` 命令中使用通配符。

> **通配符**
>
> 符号（或一组符号），代表其他字符

**最常用的通配符**

![](img/87e31443ff747018655a0f4f95ee6187_96_0.png)

![](img/87e31443ff747018655a0f4f95ee6187_96_1.png)

- `*`：任意单个或多个字符
- `?`：任意单个字符
- 示例：`ca*`
- `c?t`
- "cat", "can", "caterpillar", "capital", 等
- "cat", "cut", "cot", 等

通配符是一个代表其他字符的符号（或一组符号）。它通常用于替换任何字符串或字符。

## 通配符与正则表达式

通配符和正则表达式看起来相似，但它们是不同的东西。通配符字符的定义可能因软件而异，而正则表达式中元字符的定义在不同软件之间通常是相同的。

**`*`（星号）和 `?`（问号）**

- `*`（星号）和 `?`（问号）是最常用的通配符。`*` 代表任意单个或多个字符，而 `?` 代表任意单个字符。

例如，

- `ca*`: "cat", "can", "caterpillar", "capital", 等
- `c?t*`: "cat", "cut", "cot", 等

## 通配符在 Linux 中的用例

### 在命令执行中缩短文件或目录名称

你可以使用通配符来指定名称较长的文件或目录。例如，当目录下有一个名为 `wildcard_regular_expression_differences.txt` 的文件，且同一目录下没有其他以 "w" 开头的文件时，你可以使用 `w*` 来指定该文件。下面是一个使用 `w*` 指定要查找的文件名的命令示例。

## 命令行 - 输入

```bash
ubuntu $ | cat w*
```

## `find` 命令

当你忘记了文件的完整名称并想要定位它时，通配符非常有用。

例如，要搜索名称以 "sample" 开头的文档，运行以下命令。

## 命令行 - 输入

```bash
ubuntu $ | find ~ -name sample*
```

如果你在与上一节相同的目录结构中运行命令，结果将如下。

## 命令行 - 响应

```
/home/ubuntu/test/sample_1.txt
/home/ubuntu/test/test_sub/sample_2.txt
```

## `ln`（创建文件和目录的链接）

| 类型 | 命令 |
| :--- | :--- |
| 符号链接 | `ln -s [文件或目录路径] [链接名称]` |
| 硬链接 | `ln [文件或目录路径] [链接名称]` |

![](img/87e31443ff747018655a0f4f95ee6187_98_0.png)

`ln` 命令用于创建文件或目录的链接。Linux 中有两种类型的链接——**符号链接**（symbolic link）和**硬链接**（hard link）。

### 符号链接

符号链接是 Mac OS 别名或 Windows OS 快捷方式。它与原始文件或目录链接。因此，当你删除原始文件或目录时，符号链接将失效。

### 创建符号链接

要创建符号链接，请使用带有 `-s` 选项的 `ln` 命令。要查看示例，先使用 `cat` 命令创建 `file_a`。

## 命令行 - 输入

```bash
ubuntu $ | cat > file_a
```

### 命令行 - 交互

```bash
test test test
```

使用 `Ctrl+C` 退出输入模式，并运行 `ln` 命令创建一个指向 `file_a` 的符号链接。

## 命令行 - 输入

```bash
ubuntu $ | ln -s file_a file_symbolic
```

当你运行 `ls -l` 命令时，可以看到文件详细信息。第二行的第一个字母显示它是一个符号链接，你可以在名称列看到 `file_symbolic` 链接到 `file_a`。

## 命令行 - 响应

```
total 0
-rw-rw-r-- 1 ubuntu ubuntu 0 Jan 9 06:47 file_a
rwxrwxr-wx 1 ubuntu ubuntu 6 Jan 9 11:37 file_symbolic -> file_a
```

### 硬链接

硬链接的概念稍微复杂一点。在 Linux 文件系统中，每个文件的实际数据存储在硬盘上的某个位置。该位置在每个文件的 `inode` 中描述。当你为 `file_a` 创建硬链接时，该链接连接到该 inode。

### 创建硬链接

要创建硬链接，请使用 `ln` 命令。因此，当你删除原始文件或目录时，硬链接仍然存在。

## 命令行 - 输入

```bash
ubuntu $ | ln file_a file_hard
```

当你运行 `ls -l` 命令时，可以看到文件详细信息。第二行的第一个数字显示硬链接的数量。你也可以看到它是一个硬链接。

注意：Vim 有一个名为 `GVim` 的 GUI 版本，但基于 CLI 的 Vim 使用更为广泛。

# 轻量快速的文本编辑器

Vim 是一款非常轻级的软件，不会消耗大量的计算机资源。由于 Vim 大程度上通过键盘操作，因此需要花费时间掌握；然而，一旦你掌握了所有的快捷键命令，你的编码速度将会快得多。

# 如何启动 Vim？
