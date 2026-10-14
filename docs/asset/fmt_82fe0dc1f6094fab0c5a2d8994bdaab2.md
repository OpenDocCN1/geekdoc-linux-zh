
3. 树结构的第三层包含系统中两个用户 `smith` 和 `chang` 的登录目录。`smith` 和 `chang` 在登录后就是在这些目录中开始工作的。

4. 图中第四层显示了 `chang` 登录目录下的三个目录：`plans`、`report` 和 `payroll`。

5. 树结构的第五层同时包含文件和子目录。`plans` 目录包含四个文件，每个季度一个。`report` 目录包含三个文件，组成一份报告的三个部分。第五层还有两个子目录 `regular` 和 `contract`，它们进一步组织了 `payroll` 目录中的信息。

较高层的目录通常称为父目录。例如，在图 2–1 中，目录 `plans`、`report` 和 `payroll` 都以 `chang` 作为它们的父目录。

路径名指定文件系统中目录或文件的位置。例如，当你想从处理目录 X 中的文件 A 改为处理目录 Y 中的文件 B 时，你需要输入文件 B 的路径名。操作系统随后会使用该路径名在文件系统中搜索，直到找到文件 B 为止。

路径名由一系列用斜杠（`/`）分隔的目录名组成，并以目录名或文件名结尾。路径名中的第一个元素指定系统从哪里开始搜索，最后一个元素指定搜索的目标。以下路径名基于图 2–1：

```
/usr/chang/report/part3
```

第一个斜杠（`/`）表示根目录，并指明搜索的起点。路径名的其余部分表示搜索将进入 `usr` 目录，然后进入 `chang` 目录，接着进入 `report` 目录，最后到达 `part3` 文件。

无论你是要更改当前目录、将数据发送到文件，还是将文件在文件系统中从一个位置复制或移动到另一个位置，你都要使用路径名来指明要操作的对象。

以斜杠（`/`）（表示根目录的符号）开头的路径名称为完整路径名或绝对路径名。你也可以将完整路径名视为文件或目录的完整名称。无论你在文件系统的哪个位置工作，都可以通过指定完整路径名来找到文件或目录。

文件系统还允许你使用相对路径名。相对路径名不以表示根目录的 `/` 开头，因为它们是相对于当前目录的。

你可以通过以下几种方式指定相对路径名：

- 作为当前目录中某个文件的名称。
- 作为以当前目录下一级目录名称开头的路径名。
- 作为以 `..`（点点，即父目录的相对路径名）开头的路径名。
- 以 `.`（点，表示当前目录）开头的路径名。这种相对路径名表示法在你想在当前目录中运行自己的操作系统命令版本时很有用（例如 `./ls`）。

每个目录至少包含两个条目：`..`（点点）和 `.`（点）。

例如在图 2-2 中，如果你的当前目录是 `chang`，那么 `contract` 目录中文件 `1Q` 的相对路径名为 `payroll/contract/1Q`。通过将此相对路径名与同一文件的完整路径名 `/user/chang/payroll/contract/1Q` 进行比较，你可以看到使用相对路径名意味着更少的输入和更大的便利性。

#### Figure 2-2: Relative and Full Pathnames

![](img/47f3b48f0999ddf70574ce85cbaaf942_46_0.png)

```
------ = Relative pathname

..... = Full pathname
```

在 C shell 以及 Korn 或 POSIX shell 中，你也可以在相对路径名的开头使用波浪号（`~`）。单独使用的波浪号字符指定用户的登录（主）目录。后面跟有用户名的波浪号字符指定同一系统上另一用户的登录（主）目录。

例如，要指定你自己的登录目录，使用单独的波浪号。要指定用户 `chang` 的登录目录，指定 `~chang`。

有关使用相对路径名的更多信息，请参阅第 4 章。

> **Note**
>
> 如果你的系统上有其他用户，你可能能够或不能够访问他们的文件和目录，这取决于为其设置的权限。有关文件和目录权限的更多信息，请参阅第 5 章。此外，你的系统可能包含可能影响对文件和目录访问的增强安全功能。如果是这样，请向你的系统管理员咨询详情。

### 2.4 Specifying Files with Pattern Matching

命令通常将文件名作为参数。要使用多个不同的文件名作为命令的参数，你可以像以下示例那样输入每个文件的全名：

```
$ ls file1 file2 file3
```

然而，如果文件名具有共同的模式（在此示例中为文件前缀），shell 可以匹配该模式，生成这些名称的列表，并自动将它们作为参数传递给命令。

星号（`*`），有时被称为 **wildcard**，匹配任何字符字符串。在以下示例中，`ls` 命令查找当前目录中包含文件前缀的每个文本文件的名称：

```
$ ls file*
```

`file*` 匹配以 `file` 开头并以任何其他字符字符串结尾的任何文件名。shell 将匹配此模式的每个文件名作为 `ls` 命令的参数传递。

因此，你不必输入（甚至记住）每个文件的全名即可将其用作参数。两个命令（`ls` 并输入所有文件名以及 `ls file*`）做的是同一件事——它们将目录中具有文件前缀的所有文件作为参数传递给 `ls` 命令。

模式匹配的一般规则有一个例外。当文件名的第一个字符是句点时，你必须显式匹配该句点。例如，`ls *` 显示当前目录中所有不以句点开头的文件的名称。命令 `ls -a` 显示所有文件名，以句点开头的文件和所有其他文件。

此限制可防止 shell 自动匹配相对目录名。这些是 `.`（点，表示当前目录）和 `..`（点点，表示父目录）。有关相对目录名的更多信息，请参阅第 4 章。

如果模式不匹配任何文件名，shell 会显示一条消息，告知你未找到匹配项。

除了星号（`*`）之外，操作系统 shell 还提供其他匹配字符模式的方法。表 2-1 总结了所有模式匹配字符并提供示例。

#### Table 2-1: Pattern-matching Characters

| Character | Action |
|---|---|
| `*` | Matches any string, including the null string. For example, `th*` matches `th`, `theodore`, and `theresa`. |
| `?` | Matches any single character. For example, `304?b` matches `304Tb`, `3045b`, `304Bb`, or any other string that begins with `304`, ends with `b`, and has one character in between. |
| `[...]` | Matches any one of the enclosed characters. For example, `[AGX]*` matches all file names in the current directory that begin with A, G, or X. |
| `[..]` | Matches any character that falls within the specified range, as defined by the current locale. For more information on locale, see Appendix C. For example, `[T-W]*` matches all file names in the current directory that begin with T, U, V, or W. |
| `[!...]` | Matches any single character except one of those enclosed. For example, `[!abyz]*` matches all file names in the current directory that begin with any character except a, b, y, or z. This pattern matching is available only in the Bourne, Korn, and POSIX shells. |

An internationalized operating system provides the additional pattern-matching features described in Table 2-2.

#### 表2-2：国际化模式匹配字符

| 字符 | 操作 |
|---|---|
| `[[::class:]]` | 用括号冒号分隔符括起来的字符类名称匹配命名类中的任何字符集。支持的类有 `alpha`、`upper`、`lower`、`digit`、`alnum`、`xdigit`、`space`、`print`、`punct`、`graph` 和 `cntrl`。例如，`alpha` 字符类名称表示您要匹配当前区域设置定义的任何字母字符（大写和小写）。如果您运行的是基于美国的区域设置，则 `alpha` 匹配字母表中的任何字符（`A-Z`，`a-z`）。 |
