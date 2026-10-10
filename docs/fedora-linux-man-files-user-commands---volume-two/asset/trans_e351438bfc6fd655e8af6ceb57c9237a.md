

## 合并的差异格式

`git-diff-tree`、`git-diff-files` 和 `git-diff --raw` 可以接受 `-c` 或 `--cc` 选项，以生成合并提交的差异输出。该输出与上述格式的区别在于：

1. 每个父提交前都有一个冒号
2. 有更多的“src” 模式（mode）和 “src” sha1
3. 状态是每个父提交状态字符的拼接
4. 没有可选的 “score” 数字
5. 单个路径，仅针对 “dst”

示例：
`::100644 100644 100644 fabadb8... cc95eb0... 4866510... MM describe.c`

请注意，合并差异仅列出从所有父提交中修改过的文件。

## 使用 -p 生成补丁

当以 `-p` 选项运行 `git-diff-index`、`git-diff-tree` 或 `git-diff-files`，或者在不使用 `--raw` 选项的情况下运行 `git diff`，或者在使用 `-p` 选项的情况下运行 `git log` 时，它们不会产生上述输出；而是会产生一个补丁文件。你可以通过 `GIT_EXTERNAL_DIFF` 和 `GIT_DIFF_OPTS` 环境变量来定制此类补丁的生成。

`-p` 选项产生的输出与传统差异格式略有不同：

1. 它前面有一个 `git diff` 头部，看起来像这样：

   ```
   diff --git a/file1 b/file2
   ```

   除非涉及重命名/复制，否则 a/ 和 b/ 的文件名是相同的。特别是，即使是创建或删除，也不会使用 /dev/null 来代替 a/ 或 b/ 文件名。

   当涉及重命名/复制时，file1 和 file2 分别显示重命名/复制的源文件名以及重命名/复制产生的文件名称。

2. 它后面跟着一个或多个扩展头部行：

   ```
   old mode <mode> new mode <mode> deleted file mode <mode> new file mode <mode> copy from <path> copy to <path> rename from <path> rename to <path> similarity index <number> dissimilarity index <number> index <hash>..<hash> <mode>
   ```

   文件模式以 6 位八进制数打印，包括文件类型和文件权限位。

   扩展头部中的路径名不包含 a/ 和 b/ 前缀。

   相似性指数（similarity index）是未更改行的百分比，而不相似性指数（dissimilarity index）是更改行的百分比。它是一个向下取整的整数，后跟百分号。因此，100% 的相似性指数值保留给两个相同的文件，而 100% 的不相似性意味着旧文件中的行没有进入新文件。

   index 行包括更改前和更改后的 SHA-1 校验和。如果文件模式未更改，则包含 <mode>；否则，单独的行列出旧模式和新模式。

3. 路径名中的制表符（TAB）、换行符（LF）、双引号和反斜杠字符分别表示为 \t、\n、\" 和 \\。如果需要此类替换，则整个路径名放在双引号中。

4. 输出中所有的 file1 文件都指提交前的文件，所有的 file2 文件都指提交后的文件。依次将每个更改应用到每个文件是不正确的。例如，此补丁将交换 a 和 b：

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

   `mode <mode>,<mode>..<mode>` 行仅在至少一个 <mode> 与其他模式不同的情况下出现。关于检测到的内容移动（重命名和复制检测）信息的扩展头部是设计用于两个 <tree-ish> 之间的差异，并且不用于合并差异格式。

3. 它后面跟着两行 from-file/to-file 头部

   ```
   --- a/file +++ b/file
   ```

   类似于传统统一差异格式的两行头部，/dev/null 用于指示创建或删除的文件。

4. 块头部格式经过修改，以防止人们错误地将其输入到 patch -p1 中。合并差异格式是为了审查合并提交的更改而创建的，并不用于应用。更改类似于扩展 index 头部中的更改：

   ```
   @@@ <from-file-range> <from-file-range> <to-file-range> @
   ```

   合并差异格式的块头部中有（父提交数量 + 1）个 @ 字符。

与传统的 *统一* 差异格式不同，后者显示两个文件 A 和 B，带有一个具有 -（减号 – 出现在 A 但在 B 中移除）、+（加号 – 在 A 中缺失但在 B 中添加）或 “ ”（空格 – 未更改）前缀的列，此格式将两个或多个文件 file1、file2,... 与一个文件 X 进行比较，并显示 X 与每个 fileN 的不同之处。输出行的每个 fileN 都添加了一列，以说明 X 的行与其不同之处。N 列中的 - 字符表示该行出现在 fileN 中，但未出现在结果中。N 列中的 + 字符表示该行出现在结果中，而 fileN 没有该行（换句话说，从该父提交的角度看，该行被添加了）。

在上面的示例输出中，函数签名从两个文件更改（因此两个 - 表示从 file1 和 file2 移除，加上 ++ 表示添加的一行不出现在 file1 或 file2 中）。此外，其他八行与 file1 相同，但不出现在 file2 中（因此以 + 为前缀）。

当由 `git diff-tree -c` 显示时，它将合并提交的父提交与合并结果进行比较（即 file1..fileN 是父提交）。当由 `git diff-files -c` 显示时，它将两个未解决的合并父提交与工作树文件进行比较（即 file1 是阶段 2，也称为“我们的版本”，file2 是阶段 3，也称为“他们的版本”）。

## 其他差异格式

`--summary` 选项描述新添加、删除、重命名和复制的文件。

`--stat` 选项在输出中添加了图表。这些选项可以与其他选项（例如 -p）结合使用，旨在供人类阅读。

当显示涉及重命名或复制的更改时，`--stat` 输出通过合并路径名的公共前缀和后缀紧凑地格式化路径名。例如，将 `arch/i386/Makefile` 移动到 `arch/x86/Makefile` 并修改 4 行的更改将显示如下：

```
arch/{i386 => x86}/Makefile | 4 +--
```

`--numstat` 选项提供数值信息，但设计用于更容易的机器处理。`--numstat` 输出中的条目看起来像这样：

```
1 2 README 3 1 arch/{i386 => x86}/Makefile
```

即，从左到右：

1. 添加的行数；
2. 制表符；
3. 删除的行数；
4. 制表符；
5. 路径名（可能包含重命名/复制信息）；
6. 换行符。

当 `-z` 输出选项生效时，输出格式化如下：

```
1 2 README NUL 3 1 NUL arch/i386/Makefile NUL arch/x86/Makefile NUL
```

即：

1. 添加的行数；
2. 制表符；
3. 删除的行数；
4. 制表符；
5. 一个 NUL（仅在重命名/复制时存在）；
6. 前像路径名；
7. 一个 NUL（仅在重命名/复制时存在）；
8. 后像路径名（仅在重命名/复制时存在）；
9. 一个 NUL。

在重命名情况下，前像路径名前的额外 NUL 是为了让读取输出的脚本能够判断当前读取的记录是单路径记录还是重命名/复制

