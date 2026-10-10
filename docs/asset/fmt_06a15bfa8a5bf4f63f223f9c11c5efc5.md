
```
+ \!regexec( regexp, two->ptr, 1, &regexpmatch, 0); ... - hit = !\!regexec( regexp, mf2.ptr, 1, &regexpmatch, 0);
```

虽然 `git log -G"regexec(regexp)"` 会显示此提交，但 `git log -S"regexec(regexp)"`—pickaxe-regex 不会显示（因为该字符串的出现次数没有变化）。有关更多信息，请参见 *pickaxe* 条目中的 (7)。

## --pickaxe-all

当 `-S` 或 `-G` 找到更改时，显示该更改集的所有更改，而不仅仅是包含 `<string>` 更改的文件。

## --pickaxe-regex

将传递给 `-S` 的 `<string>` 视为扩展的 POSIX 正则表达式进行匹配。

## -O<orderfile>

按照 `<orderfile>` 中指定的顺序输出补丁，该文件每行包含一个 shell 通配符模式。这会覆盖 `diff.orderFile` 配置变量（参见 (1)）。要取消 `diff.orderFile`，请使用 `-O/dev/null`。

## -R

交换两个输入；即，显示从索引或磁盘文件到树内容的差异。

## --relative[=<path>]

当从项目的子目录运行时，可以使用此选项告知排除该目录外的更改，并显示相对于该目录的路径名。如果您不在子目录中（例如在裸仓库中），可以通过提供 `<path>` 作为参数来指定使输出相对于哪个子目录。

## -a, --text

将所有文件视为文本。

## --ignore-space-at-eol

忽略行尾（EOL）处的空白变更。

## -b, --ignore-space-change

忽略空白数量的变更。这会忽略行尾的空白，并将所有其他由一个或多个空白字符组成的序列视为等价。

## -w, --ignore-all-space

在比较行时忽略空白。即使一行有空格而另一行没有，也会忽略这些差异。

## --ignore-blank-lines

忽略所有行都是空行的更改。

## --inter-hunk-context=<lines>

显示差异块之间的上下文，最多到指定的行数，从而融合彼此接近的差异块。

## -W, --function-context

显示更改周围的整个函数。

## --ext-diff

允许执行外部差异辅助工具。如果您使用 (5) 设置了外部差异驱动，则需要将此选项与 (1) 及相关选项一起使用。

## --no-ext-diff

禁止使用外部差异驱动。

## --textconv, --no-textconv

允许（或禁止）在比较二进制文件时运行外部文本转换过滤器。有关详细信息，请参见 (5)。由于文本转换过滤器通常是一向转换，因此生成的差异适合人工阅读，但无法应用。因此，文本转换过滤器默认仅对 (1) 和 (1) 启用，而对 (1) 或差异管道命令不启用。

## --ignore-submodules[=<when>]

在差异生成中忽略子模块的更改。`<when>` 可以是 “none”、“untracked”、“dirty” 或 “all”，其中 “all” 是默认值。使用 “none” 时，如果子模块包含未跟踪或已修改的文件，或其 HEAD 与超级项目中记录的提交不同，则认为该子模块已修改，并且可以用于覆盖 (1) 或 (5) 中 ignore 选项的任何设置。当使用 “untracked” 时，子模块是

## 生成器与补丁

当子模块仅包含未跟踪内容时，不被视为“脏”（但它们仍会被扫描以查找已修改的内容）。使用 "dirty" 会忽略子模块工作树中的所有更改，仅显示存储在主项目中的提交的更改（这是 1.7.0 之前的行为）。使用 "all" 会隐藏对子模块的所有更改。

- `--src-prefix=<prefix>`

  显示给定的源前缀，而不是 "a/"。

- `--dst-prefix=<prefix>`

  显示给定的目标前缀，而不是 "b/"。

- `--no-prefix`

  不显示任何源或目标前缀。

有关这些常用选项的更详细解释，请参阅 (7)。

## 使用 -p 生成补丁

当 "git-diff-index"、"git-diff-tree" 或 "git-diff-files" 带有 -p 选项运行，或 "git diff" 不带 --raw 选项，或 "git log" 带有 "-p" 选项时，它们不会生成上述描述的输出生；相反，它们会生成一个补丁文件。你可以通过 `GIT_EXTERNAL_DIFF` 和 `GIT_DIFF_OPTS` 环境变量自定义此类补丁的创建。

-p 选项生成的内容与传统 diff 格式略有不同：

1. 它前面有一个类似于这样的 "git diff" 头部：

   ```
   diff --git a/file1 b/file2
   ```

   除非涉及重命名/复制，否则 a/ 和 b/ 文件名是相同的。特别地，即使是创建或删除，也不会用 /dev/null 代替 a/ 或 b/ 文件名。

   当涉及重命名/复制时，file1 和 file2 分别显示重命名/复制的源文件名和重命名/复制生成的文件名。

2. 它后面跟有一行或多行扩展头部行：

   ```
   old mode <mode> new mode <mode> deleted file mode <mode> new file mode <mode> copy from <path> copy to <path> rename from <path> rename to <path> similarity index <number> dissimilarity index <number> index <hash>..<hash> <mode>
   ```

   文件模式以 6 位八进制数打印，包括文件类型和文件权限位。

   扩展头部中的路径名不包含 a/ 和 b/ 前缀。

   相似度指数是未更改行的百分比，非相似度指数是已更改行的百分比。它是一个向下取整的整数，后跟百分号。因此，相似度指数的值 100% 保留给两个相等的文件，而 100% 非相似度意味着旧文件中的任何一行都没有进入新文件。

   index 行包括更改前和更改后的 SHA-1 校验和。如果文件模式未更改，则包含 `<mode>`；否则，单独的行指示旧模式和新模式。

3. 路径名中的 TAB、LF、双引号和反斜杠字符分别表示为 `\t`、`\n`、 `\"` 和 `\\`。如果需要此类替换，则整个路径名会被放在双引号中。

4. 输出中的 file1 文件均指提交前的文件，而 file2 文件均指提交后的文件。将每个更改按顺序应用于每个文件是不正确的。例如，此补丁将交换 a 和 b：

   ```
   diff --git a/a b/b rename from a rename to b diff --git a/b b/a rename from b rename to a
   ```

## 组合 DIFF 格式

任何生成 diff 的命令都可以接受 -c 或 --cc 选项，以在显示合并时生成组合 diff。这是在显示 (1) 或 (1) 中的合并时的默认格式。注意，你也可以给这些命令中的任何一个提供 -m 选项，以强制生成与合并的单个父级的 diff。

组合 diff 格式看起来像这样：

```
diff --combined describe.c index fabad8b,cc95eb0..4866510 --- a/describe.c +++ b/describe.c @@@ -98,20 -98,12 +98,20 @@@ return (a_date > b_date) ? -1 : (a_date == b_date) ? 0 : 1; } - static void describe(char *arg) -static void describe(struct commit *cmit, int last_one) +static void describe(char *arg, int last_one) { + unsigned char sha1[20]; + struct commit *cmit; struct commit_list *list; static int initialized = 0; struct commit_name *n; + if (get_sha1(arg, sha1) < 0) + usage(describe_usage); + cmit = lookup_commit_reference(sha1); + if (!cmit) + usage(describe_usage); + if (!initialized) { initialized = 1; for_each_ref(get_name);
```

1. 它前面有一个 "git diff" 头部，看起来像这样（当使用 -c 选项时）：

   ```
   diff --combined file
   ```
