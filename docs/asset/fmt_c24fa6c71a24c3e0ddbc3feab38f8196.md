
7. 一个空格。

8. “`dst`” 的 `sha1`；如果是创建、未合并或“查看工作树”，则为 `0{40}`。

9. 一个空格。

10. 状态，后跟可选的“得分”数字。

11. 制表符，或者当使用 `-z` 选项时为 `NUL`。

12. “`src`” 的路径。

13. 制表符，或者当使用 `-z` 选项时为 `NUL`；仅当状态为 `C` 或 `R` 时存在。

14. “`dst`” 的路径；仅当状态为 `C` 或 `R` 时存在。

15. `LF`，或者当使用 `-z` 选项时为 `NUL`，用于终止记录。

可能的状态字母包括：

- `A`：添加文件
- `C`：将文件复制到新文件
- `D`：删除文件
- `M`：修改文件的内容或模式
- `R`：重命名文件
- `T`：更改文件的类型
- `U`：文件未合并（在提交之前必须完成合并）
- `X`：“未知”更改类型（很可能是 bug，请报告）

状态字母 `C` 和 `R` 始终后跟一个得分（表示移动或复制的源和目标之间的相似度百分比）。状态字母 `M` 可能后跟一个得分（表示文件重写的差异百分比）。

如果文件在文件系统上是新的，且与索引不同步，则 `<sha1>` 显示为全 0。

示例：

```
:100644 100644 5be4a4... 000000... M  file.c
```

当不使用 `-z` 选项时，路径名中的 `TAB`、`LF` 和反斜杠字符分别表示为 `\t`、`\n` 和 `\`。

## 合并的差异格式

`git-diff-tree`、`git-diff-files` 和 `git diff --raw` 可以接受 `-c` 或 `--cc` 选项，以生成合并提交的差异输出。输出与上述格式在以下方面有所不同：

1. 每个父版本都有一个冒号
2. 有更多个 “`src`” 模式和一个 “`src`” `sha1`
3. 状态是每个父版本的状态字符连接而成
4. 没有可选的 “score”（得分）数字
5. 单个路径，仅针对 “`dst`”

示例：

```
::100644 100644 100644 fabadb8... cc95eb0... 4866510... MM  describe.c
```

请注意，*combined diff*（合并差异）仅列出相对于所有父版本有修改的文件。

### 使用 `-p` 生成补丁

当 `git-diff-index`、`git-diff-tree` 或 `git-diff-files` 带有 `-p` 选项运行时，`git diff` 不带有 `--raw` 选项，或 `git log` 带有 `-p` 选项时，它们不会产生上述描述的输出；相反，它们会生成一个补丁文件。您可以通过 `GIT_EXTERNAL_DIFF` 和 `GIT_DIFF_OPTS` 环境变量来自定义此类补丁的创建。

`-p` 选项产生的内容与传统差异格式略有不同：

1. 它以 “git diff” 头开始，看起来像这样：

```
diff --git a/file1 b/file2
```

`a/` 和 `b/` 文件名相同，除非涉及重命名/复制。特别是，即使是创建或删除，也不会用 `/dev/null` 替代 `a/` 或 `b/` 文件名。

当涉及重命名/复制时，`file1` 和 `file2` 分别 *显示* 重命名/复制的源文件名和重命名/复制生成的文件名。

2. 它后跟一行或多行扩展头信息：

```
old mode <mode>
new mode <mode>
deleted file mode <mode>
new file mode <mode>
copy from <path>
copy to <path>
rename from <path>
rename to <path>
similarity index <number>
dissimilarity index <number>
index <hash>..<hash> <mode>
```

文件模式以 6 位八进制数打印，包括文件类型和文件权限位。

扩展头中的路径名不包含 `a/` 和 `b/` 前缀。

相似度指数（similarity index）是未更改行的百分比，差异指数（dissimilarity index）是更改行的百分比。这是一个向下取整的整数，后跟一个百分号。因此，相似度指数值 100% 保留给两个相等的文件，而 100% 的差异意味着旧文件中的任何一行都没有进入新文件。

索引行包括更改前后的 `SHA-1` 校验和。如果文件模式没有更改，则包括 `<mode>`；否则，单独的指示行指示旧模式和新模式。

3. 路径名中的 `TAB`、`LF`、双引号和反斜杠字符分别表示为 *‘t’*、*‘n’*、**”** 和 *\*。如果需要这种替换，则整个路径名将被放在双引号中。

4. 输出中所有的 `file1` 文件指提交前的文件，而所有的 `file2` 文件指提交后的文件。依次将每个更改应用到每个文件是不正确的。例如，这个补丁会交换 a 和 b：

```
diff --git a/a b/b
rename from a
rename to b
diff --git a/b b/a
rename from b
rename to a
```

## 合并差异格式

任何生成差异的命令都可以接受 `-c` 或 `-cc` 选项，在显示合并时生成合并差异。这是使用第 (1) 项或第 (1) 项显示合并时的默认格式。请注意，您也可以向这些命令中的任何一个提供 `-m` 选项，以强制生成与合并的各个父版本的差异。

合并差异格式看起来像这样：

```
diff --combined describe.c
index fabadb8,cc95eb0..4866510
--- a/describe.c
+++ b/describe.c
@@@ -98,20 -98,12 +98,20 @@@
 return (a_date > b_date) ? -1 : (a_date == b_date) ? 0 : 1; }
 - static void describe(char *arg)
 -static void describe(struct commit *cmit, int last_one)
 ++static void describe(char *arg, int last_one)
 {
 + unsigned char sha1[20];
 + struct commit *cmit;
 struct commit_list *list;
 static int initialized = 0;
 struct commit_name *n;
 + if (get_sha1(arg, sha1) < 0)
 + usage(describe_usage);
 + cmit = lookup_commit_reference(sha1);
 + if (!cmit)
 + usage(describe_usage);
 + if (!initialized) {
 initialized = 1;
 for_each_ref(get_name);
```

1. 它以 “git diff” 头开始，看起来像这样（当使用 `-c` 选项时）：

```
diff --combined file
```

或像这样（当使用 `-cc` 选项时）：

```
diff --cc file
```

2. 它后跟一行或多行扩展头信息（此示例显示一个带有两个父版本的合并）：

```
index <hash>,<hash>..<hash>
mode <mode>,<mode>..<mode>
new file mode <mode>
deleted file mode <mode>,<mode>
```

只有当至少一个 `<mode>` 与其他模式不同时，`mode <mode>,<mode>..<mode>` 行才会出现。检测内容移动（重命名和复制检测）的扩展头信息被设计用于两个 `<tree-ish>` 的差异比较，并且不用于合并差异格式。

3. 它后跟两行的 from-file/to-file 头信息

```
diff --combined a/file b/file
```

类似于传统统一差异格式的两行头信息，使用 `/dev/null` 来指示创建或删除的文件。

4. 块头格式经过修改，以防止人们不小心将其输入 `patch -p1`。合并差异格式是为审查合并提交的更改而创建的，并非旨在用于应用。该更改与扩展索引头中的更改类似：

```
@@@ <from-file-range> <from-file-range> <to-file-range> @@@
```

合并差异格式的块头中有（父版本数量 + 1）个 `@` 字符。
