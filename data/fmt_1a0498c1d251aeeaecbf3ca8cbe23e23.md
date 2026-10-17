
### Options

- `-a` 将输出附加到由 `-c` 选项指定的 own 文件 `message-file` 中。如果发现两个不同的消息具有相同的集合和消息编号，则保留指定文件中的消息并丢弃输入文件中的另一个消息。

- `-b` 将提取的注释放在输出文件中相应消息之后。此选项更改了 `-s` 或 `-c` 选项的放置行为。

- `-c` `message-tag` 从输入文件中提取包含 `message-tag` 的消息注释，并以 `$` 前缀的形式作为注释写入输出文件。

- `-d` 在保留翻译的同时包含要保留的消息的原始文本。使用此选项，翻译人员可以在消息被替换为译文后仍然看到原始消息。

- `-f` 与 `-l` 或 `-r` 选项配合使用时，覆盖输入文件和项目文件。使用 `-r` 选项时，仅覆盖输入文件。

- `-g` `project-file` 生成项目文件，该文件包含输入文件中集合编号及其对应的最大消息编号的列表。

- `-l` `project-file` 如果输入文件中的消息编号为 `-1`，则根据 `project-file` 用计算出的数字替换消息编号，然后生成带有新消息编号的输入文件副本以及带有新最大消息编号的 `project-file` 副本。如果没有找到 `project-file`，则使用输入文件中的最大消息编号作为基数并生成 `project-file`。

- `-m` `prefix` 使用前缀填充消息。此选项用于测试。

- `-M` `suffix` 使用后缀填充消息。此选项用于测试。

- `-n` 在输出文件中添加注释行，指示每个提取的字符串在输入文件中对应的文件名和行号。

- `-o` `message-file` 将输出写入 `message-file`。

- `-p` `processor` 调用预处理器处理 `catgets(3)` 用的宏和定义语句。`genmsg` 首先将选项参数作为预处理器调用，然后对预处理器的输出开始标准流程。`genmsg` 为所有输入文件启动此过程。

- `-r` 将消息编号替换为 `-1`。此操作是 `-1` 选项的反操作。

- `-s` `set-tag` 从输入文件中提取包含 `set-tag` 的集合编号注释，并以 `$` 前缀的形式作为注释写入输出文件。如果你为一个编号指定了多个注释，则提取第一个并忽略其余。

- `-t` 生成长度为原始消息三倍的消息。此选项用于测试。

- `-x` 抑制关于消息、编号范围检查和冲突的警告消息。

### Operands

- `file` 一个输入源文件。

## genmsg

### Examples

假设你有以下源文件和项目文件。

```bash
castle% cat test.c

printf(catgets(catfd, 1, -1, "line too long"));

printf(catgets(catfd, 2, -1, "invalid code"));

castle% cat proj

1 10

2 20
```

命令

```bash
castle% genmsg -1 proj test.c
```

根据 `proj` 分配计算出的消息编号并生成以下文件。

```bash
test.c.msg message file

proj.new updated project file

test.c.new new source file
```

```bash
castle% cat test.c.msg
$quote"
$set 1
11 "line too long"
$set 2
21 "invalid code"
castle% cat proj.new
1 11
2 21
```

```bash
castle% cat test.c.new
printf(catgets(catfd, 1, 11, "line too long"));
printf(catgets(catfd, 2, 21, "invalid code"));
```

> 对于一个包含以下信息的 `test.c` 文件：

```bash
castle% cat test.c
/* SET: tar messages */
/* MSG: don't translate "tar". */
catgets(catfd, 1, 11, "tar: tape write error");
// MSG: don't translate "tar" and "-I".
catgets(catfd, 1, 2, "tar: missing argument for -I flag");
```

以下命令提取注释并将其写入 `test.c.msg` 输出文件。

```bash
castle% genmsg -s SET -c MSG test.c
castle% cat test.c.msg
/* SET: tar messages */
$set 1
/* MSG: don't translate "tar". */
1
"tar: tape write error"
// MSG: don't translate "tar" and "-I".
2
"tar: missing argument for -I flag"
```
