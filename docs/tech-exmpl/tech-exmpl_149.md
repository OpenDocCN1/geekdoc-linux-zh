

# 如何在使用 vi 或 vim（Linux）编辑器时通过行号跳转到特定行

> 原文：[`techbyexample.com/goto-line-number-vi-vim/`](https://techbyexample.com/goto-line-number-vi-vim/)

## 概述

通常，在使用 `vi` 或 `vim` 打开 Linux 文件时，文件是没有行号显示的。要跳转到某一行，首先需要显示行号。可以使用以下命令在 `vi` 或 `vim` 编辑器中显示行号：

```bash
:set nu + Enter key
```

一旦在编辑器中显示了行号，就可以在编辑器中输入以下命令来跳转到特定的行号：

```bash
:n + Enter key
```

其中 `n` 是你想要跳转到的行号。让我们来看一个例子。

## 示例

以下是一个示例，展示如何首先显示行号，然后跳转到特定行：

1. 创建一个包含一些内容的临时文件：

```text
this is line 1
this is line 2
this is line 3
this is line 4
```

2. 使用 `cat` 命令检查临时文件的内容：

```bash
~ $ cat temp.txt
this is line 1
this is line 2
this is line 3
this is line 4
```

3. 使用 `vi` 或 `vim` 打开临时文件，然后输入 `:set nu`，再按 `Enter` 键。这将在打开的编辑器中显示行号，如下所示：

```text
1 this is line 1
2 this is line 2
3 this is line 3
4 this is line 4
~
~
~
~
:set nu
```

4. 使用 `:n` 后跟 `Enter` 键跳转到特定行号，其中 `n` 是你想要跳转到的行号。这里使用 `:3` 跳转到第 `3` 行。输入 `:3` 后不要忘记按 `Enter` 键。你会看到编辑器中的光标位于第 3 行：

```text
1 this is line 1
2 this is line 2
3 this is line 3
4 this is line 4
~
~
~
~
:3
```

用户可以使用上述方法访问、更新或删除所需的行。操作完成后，可以使用 `:q!` 关闭文件而不保存更改，或者使用 `:wq` 关闭文件并保存更改。

