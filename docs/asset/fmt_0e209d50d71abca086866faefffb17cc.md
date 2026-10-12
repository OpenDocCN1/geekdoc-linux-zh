
- `CMP`—设置此变量时，试图减少重复的搜索结果（换句话说，在输出中只显示一次找到的字符串或命令）。

- `COMPRESS` 和 `COMPRESS_EXT`—这些设置压缩程序和扩展名；所有 `man` 页默认由 `gzip` 压缩。

- `MANSECT`—这设置 `man` 页搜索的顺序。

### `man` 中的操作键

通常，您对单个目标使用 `man` 命令，例如查找 `ls` 命令的文档：

```
man ls
```

这会返回以下输出（为简洁而截断）：

| `LS(1)` | User Commands | `LS(1)` |
|:---|:---|:---|
| **`NAME`** | `ls`--list directory contents | |
| **`SYNOPSIS`** | `ls` [OPTION]... [FILE]... | |
| **`DESCRIPTION`** | List information about the FILES (the current directory by default). Sort entries alphabetically if none of `--ctftuX` nor `-sort`. | |
| | Mandatory arguments to long options are mandatory for short options too. | |
| | `-a`, `--all` | |

当您在 `man` 页中时，包括 `ctime` 在内的几个按键可以极大帮助，它允许您在 `man` 页中向下搜索特定字符串：

```
ctime
```

这找到了字符串 `ctime` 的第一次出现。默认情况下，`man` 页中的搜索不区分大小写——例如，它既找到 `word` 也找到 `WORD`。

此外，在搜索字符串时，在找到之后，您可以按 `N` 键在 `man` 页中找到下一次出现（向下）。另外，您可以使用 `N` 键移动到前一次出现（向上）。

要在 `man` 页中移动，您可以使用两个键之一：空格键每次向下移动一屏，`Enter` 键每次向下移动一行。`B` 键每次向上移动一屏，在某些情况下 `Home` 键带您到 `man` 页的顶部。

最后，`Q` 键退出 `man` 页。（如果您暂时被困在 `man` 页中，这会显得非常没出息，如果是这样，请保持安静。）

### 从 `man` 中获取更多

许多系统管理员和用户没有将 `man` 命令扩展到前一部分提到的操作之外，错过了一些非常有用的标准命令替代方案。

例如，假设您需要有关 `crontab` 文件的更多信息，该文件在运行 `crontab -e` 命令时进行编辑。如果您只是输入

```
man crontab
```

您只会得到 `crontab (1)` `man` 页，这不是您想要的。要查看为搜索词找到的所有 `man` 页列表，请使用查找搜索功能 (`-f`)，如下所示：

```
man -f crontab
```

这返回如下所示的输出：

```
crontab (1)     --maintain crontab files for individual users (V3)
crontab (5)     --tables for driving cron
```

好多了，现在您可以指定 `crontab (5)` 页并获取正确的信息：

```
man 5 crontab
```

如果您运行 `whatis crontab` 命令，您将看到与 `man -f crontab` 输出相似，这在考试问题中出现。

`man` 命令的另一个绝佳选项是 `-k`，或关键字搜索功能，它比 `-f` 选项更具表达性和冗长性。要找到所有在描述中包含 `cron tab` 一词的 `man` 页，请使用以下命令：

```
man -k crontab
```

这返回以下输出（为简洁而截断）：

```
/etc/anacrontab (5) [anacrontab]-configuration file for anacron
anacrontab (5) --configuration file for anacron
crontab (1) --maintain crontab files for individual users (V3)
crontab (5) --tables for driving cron
```

注意，`/etc/anacrontab` 条目已包含，`anacrontab` 页也是如此。`-k` 选项不加区分地搜索搜索词的任何实例，包括作为另一术语的一部分。

正如之前的 Exam Alert 所述，如果您运行 `apropos crontab` 命令，您将看到与 `man -k crontab` 输出相似；它们实际上是相同的。

查看与特定字符串或命令相关的所有 `man` 页的另一种方法是使用 `-a` 选项，该选项依次加载每个找到的页。您可以按 `Q` 键退出并加载下一个可用页，直到所有找到的页用尽。例如，要查看为 `crontab` 找到的所有页，您输入以下内容：

```
man -a crontab
```

### `whatis` 与 `Apropos`？

`whatis` 和 `apropos` 命令默认显示与 `man -f` 和 `man -k` 命令相同的信息。这两个命令从 `whatis` 数据库中提取内容，有时保存在 `/usr/share/man/whatis`，但通常位于 `/var/cache/man/index.db` 文件中。

在大多数发行版中，此文件可以通过 `mkwhatis`（有时命名为 `makewhatis`）命令更新，但 Debian 不包含它。

### 附加文档

在 `/usr/share/doc` 目录树中会显示一组附加文档。在 `/usr/share/doc` 目录结构中，有时会出现以下可选目录：

- `/usr/share/doc/program1` — `program1` 的文档

- `/usr/share/doc/FAQ` — 程序的常见问题解答

- `/usr/share/doc/HTML` — HTML 格式的文档

- `/usr/share/doc/HOWTO` — 所有操作指南（`HOWTOs`）

- `/usr/share/info` — `info` 命令使用的文件

> **警告**
>
> 在考试中，`info` 命令仅短暂出现，其角色是作为 FSF（自由软件基金会）首选的文档阅读器或文档呈现方式。

### 网络与第三方文档

LPI 对第三方文档颇为重视，无论是 Linux 文档项目、新闻组还是邮件列表。

### Linux 文档项目

Linux 的主要文档站点是 Linux 文档项目（<http://www.tldp.org>）。该站点被视为引导新手的第一个去处，但许多老手也会访问该站点以寻找解决资源、学习新主题或为该项目做出贡献。

`LDP` 提供的服务包括

- `HOWTOs` — 常规 `HOWTO` 是关于 Linux 内核、网络等主题的中等到详尽的文档。`Mini-HOWTO` 是较短的，有时甚至非常简练的文档，专注于诸如三键鼠标配置等更具体的主题。

- **指南（Guides）** — 较长、更具书籍风格的文档，对特定主题（如系统管理、`bash` 脚本等）进行深度覆盖。

- `FAQs` — 关于 Linux 主题的常见问题汇总。这些比 `HOWTO` 更具互动性。然而，目前可用的这类资源很少。

> **警告**
>
> 你很可能会看到关于 `LDP` 站点 URL 的问题，代表 Web 上 Linux 信息存储库的缩写（`LDP`），以及该站点的完整名称（Linux 文档项目）的问题。

### Usenet 资源

关于 Usenet 资源，考试中的内容似乎很少，但关于 LPIC 考试与此主题相关的两件事是：

- `www.deja.com` — 这曾是允许通过搜索引擎访问 Usenet 文本的站点，这对那些无法访问新闻源的人来说非常有用。它现在是 `groups.google.com`，你可能会在考试中看到关于此资源的问题。

- `comp.os.linux` — 许多人将其视为 Linux Usenet 资源的根源，这个组是潜伏并获取大量良好信息的好地方。

> **警告**
>
> 预计会有关于这些资源的考题。彻底研究它们，在这个过程中你会学到很多关于 Linux 的知识，并在考试中表现得更好。

### 与用户沟通

系统中文档的最后部分是关于通过多个程序和文件通知用户系统事件（除了说“离开系统，它要停机了！”之外）。

### `Issue` 文件

当用户查看文本模式登录屏幕时，他们正在查看 `/etc/issue` 文件的内容。`/etc/issue` 文件通常包含如下所示类型的信息：

```
Red Hat Linux release 7.3 (Valhalla)
Kernel \r on an \m
```

用户通常看到的输出如下所示：
