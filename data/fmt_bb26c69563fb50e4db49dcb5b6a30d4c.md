
You can combine options, depending on the command and the commands themselves. In the case of `ls`, you can combine the long and all options to obtain a long listing of all files in the sample home directory of `/Intro_to_UNIX/chap04/sample_home_dir`, as demonstrated in Figure 4.12.

```bash
// /Intro_to_UNIX/chap04/sample_home_dir$ -ls
total 16
drw-xr-x 2 book 4096 Feb 11 18:06 .
drwxr-xr-x 8 book 4096 Jan 6 17:06 ..
drwxr-r---- 1 book 562 Jan 27 15:01 .bashrc
drwxr-xr-x 1 book 563 Aug 20 2000 .login
drwxr-xr-x 1 book 0 Apr 25 2005 REGIME
drwxr-xr-x 1 book 0 Apr 23 2005 notes
// /Intro_to_UNIX/chap04/sample_home_dir$
```

图 4.12 使用带有用于长格式（详细）列出和所有文件的参数进行列表。

有时你可能希望获得一个更完整的目录列表，其中包含子目录的内容。为了实现这一点，请利用 `ls` 的 `-R`（递归）选项。为了演示，假设你想查看 `~/Intro_to_UNIX/chap04` 的递归列表。接上上一个示例，你仍然位于 `~/Intro_to_UNIX/chap04/sample_home_dir` 目录。作为移动到父目录的示例，通过输入 `cd ..` 使父目录 `~/Intro_to_UNIX/chap04` 成为当前工作目录，如图 4.13 所示。然后对新工作目录的内容进行普通列出，随后对子目录进行递归列表，如图 4.13 所示。

要更改 `~/Intro_to_UNIX/chap04/sample_home_dir` 的父目录，在本示例中，你也可以将 `~/Intro_to_UNIX/chap04` 作为 `cd` 的参数，但使用 `..` 更快也更方便。

注意递归列表会在每个子目录名称后加上一个冒号（:）。在给定的子目录之后是它的内容（换句话说，就是文件以及可能的其他子目录）。例如，`work` 目录下有一个文件（`contacts`）和两个子目录 `projectA` 和 `projectB`。在 `work/projectA` 内部有一个文件（`information`）和两个子目录（`documentation` 和 `program_code`）。

`ls` 有许多可用选项，但可能最常用的已经讨论过了。稍后描述的其他命令也是如此——当描述了这些每个命令的常用选项时。然而，特定命令可能具有你在特定情况下可能发现的其它选项。如果你想研究命令的其他选项，可以参考以 `man` pages（帮助页）形式呈现的命令在线文档，这在第 5 章中进行了描述。

# 使用模式匹配文件名

在继续学习其他基础文件和目录命令之前，看看 UNIX/Linux 如何使用各种符号匹配文件和目录名称。这些概念被用于许多命令，但目前它们在 `ls` 命令的语境下进行解释，因为你对它有了一些了解。

# UNIX/Linux 简介

```bash
/Intro-to-UNIX/chap04/sample_home_dir$ ..
/Intro-to-UNIX/chap04$ $
RENAME greeting mv_examples mytouch notes.bak work
courses full_listing misc_files myfile notes sample_home_dir
~/Intro-to-UNIX/chap04$ -lr work/
work/
total 12
-drwxrxr-x 1 book 48 Mar 27 2005 contacts
-drwxrxr-x 1 book 46 Mar 27 2005 projectA
-drwxrxr-x 1 book 46 Mar 27 2005 projectB
work/projectA:
total 12
-drwxrxr-x 1 book 46 Aug 26 2005 documentation
-rw-r--r-- 1 book 119 Mar 27 2005 information
-rw-r--r-- 1 book 406 Aug 26 2005 program_code
work/projectA/documentation:
total 0
-rw-r--r-- 1 book 104 Apr 26 2005 customer_doc
-rw-r--r-- 1 book 122 Apr 26 2005 internal_doc
work/projectA/program_code:
total 4
-rw-r--r-- 1 book 134 Apr 26 2005 main.cpp
work/projectB:
total 12
-drwxrxr-x 1 book 46 Aug 26 2005 documentation
-rw-r--r-- 1 book 125 Mar 27 2005 information
-rw-r--r-- 1 book 406 Aug 26 2005 program_code
work/projectB/documentation:
total 8
-rw-r--r-- 1 book 104 Apr 26 2005 customer_doc
-rw-r--r-- 1 book 122 Apr 26 2005 internal_doc
work/projectB/program_code:
total 4
-rw-r--r-- 1 book 134 Apr 26 2005 main.cpp
~/Intro-to-UNIX/chap04$ #
```

图 4.13 使父目录当前并执行递归列表。

在某些情况下，你可能通过部分输入名称来引用文件或目录。例如，你只知道名称的一部分，而不希望完全输入它。类似地，你可能希望一次性引用多个文件或目录。为了实现这一点，UNIX/Linux 提供了许多机制，例如你只需指定名称的开头字母即可。

## 使用通配符匹配字母、数字或符号

要匹配以特定字符开头或包含特定字符的文件或目录，你可以使用通配符 `*`（星号）来匹配任意数量的字符，使用 `?`（问号）来匹配单个字符。这些技术在 `ls`、`cp`、`mv` 等命令中非常有用。

例如，使用通配符匹配文件名，如图 4.14 所示。

```bash
~/Intro-to-UNIX/chap04$ data*
```

图 4.14 使用通配符匹配以 data 开头的文件。

为了演示，使用 `*` 匹配文件名。

```bash
~/Intro-to-UNIX/chap04$ data*
```

图 4.15 使用通配符匹配以 data 开头的文件。

要匹配以 data 开头的文件，你可以使用通配符。

```bash
~/Intro-to-UNIX/chap04$ data*
```

图 4.16 使用通配符匹配以 data 开头的文件。

```bash
~/Intro-to-UNIX/chap04$ data*
```

虽然非 UNIX/Linux 系统也使用 `*` 来指定通配符，但这些系统使用 `*` 的方式与 UNIX/Linux 的方式之间是否存在某些区别？其他系统通常使用 `*` 仅匹配文件名的一部分，例如匹配名称中点之前或点之后的部分，而将 `*` 用于匹配所有文件名和扩展名。UNIX/Linux 则没有这一限制。在 UNIX/Linux 中，`*` 会匹配目录中所有文件和/或子目录名称，无论这些名称没有点、有一个点还是有多个点。然而，`*` 不匹配文件名，即带有点命名的文件。点文件（dot file）的名称必须始终以点开头进行指定。

## 使用 ? 匹配单个字母、数字或符号

UNIX/Linux 利用 `?` 符号、数字或符号作为文件名称的通配符。当你需要将通配符匹配限制在一个非常特定的可能名称范围内时，这非常有用。例如，在子目录 `~/Intro_to_UNIX/chap04/misc_files` 中，假设你只想列出从 `file1`、`file2`、`. . . . .` 到 `file19` 的文件的完整（详细）列表（换句话说，即 `filex`，其中 `x` 代表**恰好一个**字母、数字或符号的任意匹配）。你可以通过 `?` 通配符来实现，如图 4.20 所示。
