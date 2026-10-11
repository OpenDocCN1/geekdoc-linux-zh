
```
$ cat data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$
$ sed '2s/dog/cat/' data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$
```

`sed` 编辑器仅根据指定的地址修改了第 2 行的文本。这是另一个示例，这次使用了一个行地址范围（第 2 行到第 3 行）：

```
$ sed '2,3s/dog/cat/' data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy dog.
$
```

如果你想将命令应用于从文本中某一点开始并持续到文本末尾的一组行，你可以使用美元符号代替最后一个地址范围数字：

```
$ sed '2,$s/dog/cat/' data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
$
```

由于你可能不知道文本中有多少行数据，美元符号通常非常有用。

### 使用文本模式过滤器

限制命令应用行的另一种方法稍微复杂一些。`sed` 编辑器允许指定一个文本模式，并将其用作过滤器来确定命令应用于哪些行。格式如下：

`/pattern/command`

你必须用前向斜杠封装你指定的模式。`sed` 编辑器仅将命令应用于包含你指定的文本模式的行。

例如，如果你只想为用户 `rich` 更改默认 shell，你可以使用 `sed` 命令：

```
$ grep '/bin/bash /etc/passwd
root:x:0:0:root:/root:/bin/bash
christine:x:1001:1001:/home/christine:/bin/bash
rich:x:1002:1002:/home/rich:/bin/bash
$
$ sed 's/rich/s/bash/csh/' /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
[...]
christine:x:1001:1001:/home/christine:/bin/bash
sshd:x:126:65534::/run/sshd:/usr/sbin/nologin
rich:x:1002:1002:/home/rich:/bin/csh
$
```

该命令仅应用于包含匹配文本模式的行。虽然使用固定的文本模式可能有助于过滤特定值，如前一个示例所示，但它在使用上有一定的局限性。`sed` 编辑器在文本模式中使用一种称为 `正则表达式` 的功能，允许你创建相当复杂的模式。

正则表达式允许你创建高级文本模式匹配公式，以匹配各种类型的数据。这些公式将一系列通配符字符、特殊字符和 `固定文本` 字符组合在一起，生成一个简洁的模式，几乎可以匹配任何文本情况。正则表达式是 shell 脚本编程中较难的部分之一，第 20 章“正则表达式”将详细介绍它们。

### 组合命令

如果你需要在一行上执行多个命令，请使用花括号将命令组合在一起。`sed` 编辑器处理列在地址行上的每个命令：

```
$ sed '{
> s/fox/toad/
> s/dog/cat/
> }' data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown toad jumps over the lazy cat.
The quick brown fox jumps over the lazy dog.
The quick brown toad jumps over the lazy cat.
$
```

两个命令都仅针对地址进行处理。当然，你可以在组合命令之前指定一个地址范围：

```
$ sed '3,${
> s/brown/green/
> s/fox/toad/
> s/lazy/sleeping/
> }' data1.txt
```

`sed` 编辑器会将所有命令应用于地址范围内的所有行。

### 删除行

文本替换命令并不是 `sed` 编辑器中唯一的命令。如果你需要删除文本流中的特定行，可以使用删除命令。

删除（`d`）命令基本上就是字面意思：它会删除任何符合所提供寻址方案（`addressing scheme`）的文本行。在使用 `d` 命令时要小心，因为如果你忘记包含寻址方案，流中的所有行都会被删除：

```
$ cat data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$
$ sed 'd' data1.txt
$ 
```

显然，当 `d` 命令与指定的地址结合使用时，它最为有用。这允许你从数据流中删除特定的文本行，可以通过行号：

```
$ cat data6.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
$
$ sed '3d' data6.txt
This is line number 1.
This is line number 2.
This is the 4th line.
$ 
```

或通过特定的行范围：

```
$ sed '2,3d' data6.txt
This is line number 1.
This is the 4th line.
$ 
```

或使用特殊的文件结束符：

```
$ sed '3,$d' data6.txt
This is line number 1.
This is line number 2.
$ 
```

`sed` 编辑器的模式匹配功能也适用于删除（`d`）命令：

```
$ sed '/number 1/d' data6.txt
This is line number 2.
This is the 3rd line.
This is the 4th line.
$ 
```

`sed` 编辑器会删除包含匹配你指定模式的文本的行。

# 注意

请记住，`sed` 编辑器不会修改原始文件。你删除的任何行只是从 `sed` 编辑器的输出中消失。原始文件仍然包含那些“已删除”的行。

你还可以使用两个文本模式来删除一行范围内的行，但这样做时要小心。你指定的第一个模式会“开启”行删除，而第二个模式会“关闭”行删除。`sed` 编辑器会删除两个指定行之间的任何行（包括指定的行）：

```
$ sed '/1/,/3/d' data6.txt
This is the 4th line.
$ 
```

此外，你必须小心，因为每当 `sed` 编辑器在数据流中检测到起始模式时，删除功能就会“开启”。这可能会产生意外的结果：

```
$ cat data7.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
This is line number 1 again; we want to keep it.
This is more text we want to keep.
Last line in the file; we want to keep it.
$ sed '/1/,/3/d' data7.txt
This is the 4th line.
$ 
```
