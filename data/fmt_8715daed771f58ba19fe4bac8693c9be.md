
通过向 `unzip` 指定文件，可以从 zip 归档中选择性地列出和提取文件：

```bash
me@linuxbox ~]$ unzip -l playground.zip playground/dir-087/file-Z
Archive: ../playground.zip
Length Date Time
---
0 10-05-08 09:25 playground/dir-087/file-Z
0 1 file
me@linuxbox ~]$ cd foo
me@linuxbox foo]$ unzip ../playground.zip playground/dir-087/file-Z
Archive: ../playground.zip
replace playground/dir-087/file-Z [yles], [n0], [A11], [None],
[r]ename: y
extracting: playground/dir-087/file-Z
```

像 `tar` 一样，`zip` 可以利用标准输入和输出，尽管它的实现用途没那么大。可以通过 `@` 选项将文件名列表传递给 `zip`：

```bash
me@linuxbox foo]$$ cd
me@linuxbox ~]$ find playground -name "file-A" | zip -@ file-A
```

在这里，我们找到一个匹配测试 `-name "file-A"` 的文件列表，然后将该列表管道到 `Zip` 中，创建一个包含所选文件的文件 `file-A.zip`。

`zip` 还支持将其输出写入标准输出，但它的用途有限，因为很少有程序可以使用该输出。遗憾的是，`zip` 程序不接受标准输入。这阻止了 `zip` 和 `unzip` 配合使用执行像 `tar` 那样的网络文件复制。

然而，`zip` 可以接受标准输入，因此它可以压缩其他程序的输出：

```bash
me@linuxbox ~}$ ls -l /etc/ | zip ls-etc.zip -
  adding: - (deflated 80%)
```

在这个示例中，我们将 `ls` 的输出管道到 `zip`。像 `tar` 一样，`zip` 将最后的横杠解释为“使用标准输入作为输入文件”。

当指定 `-p`（管道）选项时，`unzip` 程序允许将其输出发送到标准输出：

```bash
me@linuxbox ~}$ unzip -p ls-etc.zip | less
```

### 同步文件

保持系统备份的常用策略涉及查找源和目标之间的差异。`rsync` 检测到了变化并只复制了更新的文件，这比每次都复制所有内容要快得多。

## 18 – 备份

`rsync` 的真正益处之一是它可以通过网络复制文件。毕竟，`rsync` 中的 "r" 代表“远程”。远程复制可以通过两种方式进行。第一种是另一个安装了 `rsync` 的系统，并配合远程 shell 程序（如 `ssh`）。

等待：

我们包含了 `--delete` 选项，以删除备份驱动器上存在但源不存在的文件（这在我们第一次进行备份时无关，但在随后的复制中将有用）。

### 同步文件和目录

| `/usr/local` `remote-sys:/backup` |

为了方便网络复制，我们对命令进行了两处修改。首先，我们添加了 `-r=ssh` 选项，它指示 `rsync` 使用 `ssh` 程序作为其远程 shell。通过这种方式，我们能够使用 `ssh` 加密隧道将数据从本地系统安全地传输到远程主机。其次，我们通过在目标路径名前加上主机名（在本例中，远程主机名为 `remote-sys`）来指定远程主机。

使用 `rsync` 在网络上同步文件的另一种方法是使用 `rsync` 服务器。可以将 `rsync` 配置为以守护进程（daemon）运行并监听同步请求。这通常用于对远程系统进行镜像。例如，红帽软件（Red Hat Software）维护着一个大型开发软件包仓库——这对于软件测试人员在发行版发布周的测试阶段非常有用。由于仓库中的文件频繁变化（通常一天超过一次），因此通过定期同步来维护本地镜像，比批量拷贝仓库更为理想。其中一个仓库保存在佐治亚理工学院（Georgia Tech）；我们可以通过如下方式使用本地的 `rsync` 副本和他们的 `rsync` 服务器来镜像它：

```
@me@linuxbox ~$ mkdir fedora-devel
@me@linuxbox ~$ rsync -av --delete rsync://gtlib.gatech.edu/fedora-linux-core/development/1386/os fedora-devel
```

在这个示例中，我们使用了远程 `rsync` 服务器的 URI，它由协议（`rsync://`）、远程主机名（`rsync.gtlib.gatech.edu`）以及仓库路径组成。

### 总结

我们查看了 Linux 和其他 Unix 类操作系统上常用的压缩和归档程序。对于文件归档，`tar`/`gzip` 组合是 Unix 类系统上的首选方法，而 `zip`/`unzip` 则用于与 Windows 系统的互操作性。最后，我们查看了 `rsync` 程序（我的个人喜爱），它对于跨系统高效同步文件和目录非常有用。

### 扩展阅读

- 此处讨论的所有命令的手页（man pages）非常详尽，并包含了实用的示例。此外，GNU 项目为其版本的 `tar` 提供了一份良好的在线手册。可以在这里找到：

`http://www.gnu.org/software/tar/manual/index.html`

## 19 – 正则表达式

在接下来的章节中，我们将介绍用于处理文本的工具。正如我们所见，文本数据在所有 Unix 类系统（如 Linux）中都起着重要作用。在充分理解这些工具提供的所有功能之前，我们必须首先检查与这些工具最复杂用法密切相关的技术——正则表达式。

当我们熟悉了命令行提供的许多功能和设施时，我们遇到了一些真正深奥的特性和命令，例如 shell 扩展和引用、键盘快捷键以及命令历史，更不用说 `vi` 编辑器了。正则表达式延续了这种“传统”，并且可能是（可以争论的）所有特性中最深奥的一个。这并不是并不是说学习它们所花费的时间是不值得的。恰恰相反，良好的理解将使我们能够完成令人惊叹的壮举，尽管它们的全部价值可能不会立即显而易见。

### 什么是正则表达式？

简单来说，正则表达式是用于识别文本中模式的符号表示法。在某些方面，它们类似于 shell 使用通配符匹配文件名和路径名的方法，但规模要大得多。正则表达式被许多命令行工具和编程语言支持，以便解决文本处理问题。然而，为了让事情更复杂化，并不是所有的正则表达式都是相同的；它们在不同工具和不同编程语言之间略有不同。对于我们的讨论，我们将限制在 POSIX 标准描述的正则表达式上（大多数命令行工具都使用该标准），而不是编程语言中的正则表达式。

### grep

我们将用于处理正则表达式的主程序是老牌 `grep`。“`grep`”这个名字实际上源于短语“global regular expression print（全局正则表达式打印）”，所以我们可以看到 `grep` 与正则表达式是有某种关系的。从本质上说，`grep` 在文件中搜索指定正则表达式的出现情况，并将任何包含匹配项的行输出到标准输出。

## 19 – 正则表达式

到目前为止，我们一直配合字符串使用 `grep`，如下所示：

```
me@linux ~] ls /usr/bin | grep zip
```

这将列出 `/usr/bin` 目录下所有名称包含子字符串 `"zip"` 的文件。

`grep` 程序以这种方式接受选项和参数：

`grep [options] regex [file...]`

其中 `regex` 是正则表达式。

以下是常用 `grep` 选项列表：

| 选项 | 说明 |

| --- | --- |

| `-i` | 忽略大小写。不区分大写和小写字母。也可以指定 `--ignore-case`。 |

| `-V` | 反转匹配。通常情况下，`grep` 打印包含匹配的行。此选项导致 `grep` 打印不包含匹配的每一行。也可以指定 `--invert-match`。 |

| `-c` | 打印匹配次数（如果也指定了 `-v` 选项则打印非匹配次数）而不是行本身。也可以指定 `--count`。 |

| `-l` | 打印包含匹配项的每个文件名，而不是行本身。也可以指定 `--files-with-matches`。 |

| `-L` | 类似于 `-l` ，但打印不包含匹配项的文件名。也可以指定 `--files-without-match`。 |

| `-n` | 在每个匹配行前加上该行在文件中的行号。也可以指定 `--line-number`。 |

| `-h` | 多文件搜索时抑制文件名的输出。也可以指定 `--no-filename`。 |

为了更充分地探索 `grep`，让我们创建一些文本文件进行搜索：
