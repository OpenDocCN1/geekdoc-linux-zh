
7. 一个空格。

8. “`dst`” 的 `sha1`；如果是创建、未合并或“查看工作树”，则为 `0{40}`。

9. 一个空格。

10. 状态，后跟可选的“得分”数字。

11. 当使用 `-z` 选项时为制表符或 `NUL`。

12. “`src`” 的路径

13. 当使用 `-z` 选项时为制表符或 `NUL`；仅用于 `C` 或 `R` 时存在。

14. “`dst`” 的路径；仅用于 `C` 或 `R` 时存在。

15. 当使用 `-z` 选项时为 `LF` 或 `NUL`，用于终止记录。

### 可能的状态字符为：

- `A`：文件添加
- `C`：文件复制到新文件
- `D`：文件删除
- `M`：文件内容或模式的修改
- `R`：文件重命名
- `T`：文件类型的变更
- `U`：文件未合并（在你提交之前必须完成合并）
- `X`：“未知”变更类型（很可能是 bug，请报告）

状态字符 `C` 和 `R` 后面始终跟有一个得分（表示移动或复制的源和目标之间的相似度百分比）。状态字符 `M` 后面可以跟有一个得分（表示文件重写的差异百分比）。

如果文件在文件系统上是新的，并且与索引不同步，则 `<sha1>` 显示为全 0。

#### 示例：

```
:100644 100644 5be4a4.... 000000.... M file.c
```

当未使用 `-z` 选项时，路径名中的 `TAB`、`LF` 和反斜杠字符分别表示为 `\t`、`\n` 和 `\`。

## 合并的差异格式

`git-diff-tree`、`git-diff-files` 和 `git-diff --raw` 可以接受 `-c` 或 `--cc` 选项，以生成合并提交的差异输出。该输出与上述格式的区别在于：

1. 每个父提交前都有一个冒号
2. 有更多的“`src`” 模式（mode）和 “`src`” `sha1`
3. 状态是每个父提交状态字符的拼接
4. 没有可选的 “score” 数字
5. 单个路径，仅针对 “`dst`”

#### 示例：

```
::100644 100644 100644 fabadb8... cc95eb0... 4866510... MM describe.c
```

请注意，合并差异仅列出从所有父提交中修改过的文件。

## 使用 `-p` 生成补丁

当以 `-p` 选项运行 `git-diff-index`、`git-diff-tree` 或 `git-diff-files`，或者在不使用 `--raw` 选项的情况下运行 `git diff`，或者在使用 `-p` 选项的情况下运行 `git log` 时，它们不会产生上述输出；而是会产生一个补丁文件。你可以通过 `GIT_EXTERNAL_DIFF` 和 `GIT_DIFF_OPTS` 环境变量来定制此类补丁的生成。

`-p` 选项产生的输出与传统差异格式略有不同：

1. 它前面有一个 `git diff` 头部，看起来像这样：

   ```
   diff --git a/file1 b/file2
   ```

   除非涉及重命名/复制，否则 `a/` 和 `b/` 的文件名是相同的。特别是，即使是创建或删除，也不会使用 `/dev/null` 来代替 `a/` 或 `b/` 文件名。

   当涉及重命名/复制时，`file1` 和 `file2` 分别显示重命名/复制的源文件名以及重命名/复制产生的文件名称。

2. 它后面跟着一个或多个扩展头部行：

   ```
   old mode <mode> new mode <mode> deleted file mode <mode> new file mode <mode> copy from <path> copy to <path> rename from <path> rename to <path> similarity index <number> dissimilarity index <number> index <hash>..<hash> <mode>
   ```

   文件模式以 6 位八进制数打印，包括文件类型和文件权限位。

   扩展头部中的路径名不包含 `a/` 和 `b/` 前缀。

   相似性指数（similarity index）是未更改行的百分比，而不相似性指数（dissimilarity index）是更改行的百分比。它是一个向下取整的整数，后跟百分号。因此，100% 的相似性指数值保留给两个相同的文件，而 100% 的不相似性意味着旧文件中的行没有进入新文件。

   `index` 行包括更改前和更改后的 SHA-1 校验和。如果文件模式未更改，则包含 `<mode>`；否则，单独的行列出旧模式和新模式。

3. 路径名中的制表符（`TAB`）、换行符（`LF`）、双引号和反斜杠字符分别表示为 `\t`、`\n`、 `\"` 和 `\\`。如果需要此类替换，则整个路径名放在双引号中。

4. 输出中所有的 `file1` 文件都指提交前的文件，所有的 `file2` 文件都指提交后的文件。依次将每个更改应用到每个文件是不正确的。例如，此补丁将交换 `a` 和 `b`：

   ```
   diff --git a/a b/b rename from a rename to b diff --git a/b b/a rename from b rename to a
   ```

## 合并差异格式

任何生成差异的命令都可以使用 `-c` 或 `--cc` 选项，在显示合并时生成合并差异。这是使用 `git diff-tree` 或 `git diff-files` 显示合并时的默认格式。请注意，你还可以给这些任何命令提供 `-m` 选项，以强制生成与合并的单个父提交的差异。

合并差异格式看起来像这样：

```
diff --combined describe.c index fabad8b,cc95eb0..4866510 --- a/describe.c +++ b/describe.c @@@ -98,20 -98,12 +98,20 @@@ return (a_date > b_date) ? -1 : (a_date == b_date) ? 0 : 1; } - static void describe(char *arg) -static void describe(struct commit *cmit, int last_one) +static void describe(char *arg, int last_one) { + unsigned char sha1[20]; + struct commit *cmit; struct commit_list *list; static int initialized = 0; struct commit_name *n; + if (get_sha1(arg, sha1) < 0) + usage(describe_usage); + cmit = lookup_commit_reference(sha1); + if (!cmit) + usage(describe_usage); + if (!initialized) { initialized = 1; for_each_ref(get_name);
```

1. 它前面有一个 "git diff" 头部，看起来像这样（当使用 `-c` 选项时）：

   ```
   diff --combined file
   ```

   或像这样（当使用 `--cc` 选项时）：

   ```
   diff --cc file
   ```

2. 它后面跟着一个或多个扩展头部行（此示例显示了一个具有两个父提交的合并）：

   ```
   index <hash>,<hash>..<hash> mode <mode>,<mode>..<mode> new file mode <mode> deleted file mode <mode>,<mode>
   ```

   `mode <mode>,<mode>..<mode>` 行仅在至少一个 `<mode>` 与其他模式不同的情况下出现。关于检测到的内容移动（重命名和复制检测）信息的扩展头部是设计用于两个 `<tree-ish>` 之间的差异，并且不用于合并差异格式。

3. 它后面跟着两行 from-file/to-file 头部

   ```
   --- a/file +++ b/file
   ```

   类似于传统统一差异格式的两行头部，`/dev/null` 用于指示创建或删除的文件。

4. 块头部格式经过修改，以防止人们错误地将其输入到 `patch -p1` 中。合并差异格式是为了审查合并提交的更改而创建的，并不用于应用。更改类似于扩展 `index` 头部中的更改：

   ```
   @@@ <from-file-range> <from-file-range> <to-file-range> @
   ```

   合并差异格式的块头部中有（父提交数量 + 1）个 `@` 字符。
