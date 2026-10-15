

# 如何在 Bash/终端（Linux）中使用 Vi 或 Vim 删除文件内容

> 原文：[`techbyexample.com/vim-delete-all-contents/`](https://techbyexample.com/vim-delete-all-contents/)

## 概述

使用下面的快捷键，可以在 Bash/终端中使用 Vi 或 Vim 删除文件的所有内容：

```text
dG
```

## 示例

让我们看一个示例。

1. 首先，让我们创建并写入一个临时文件：

```bash
echo $'This is \ntest line' > temp.txt
```

2. 让我们打印文件内容进行验证：

```text
~ $ cat temp.txt
This is
test line
```

3. 现在运行 Vi 或 Vim 命令：

```bash
~ $ vi temp.text
```

在 Vi 编辑器中，你将看到如下内容：

```text
This is
test line
~
~
"temp.txt" 2L, 19C
```

现在按下 `d`，然后按 `G`（使用 Shift 键将 `g` 转换为大写）。请注意，这些键需要一个接一个地按，而不是一起按。按下键后，内容将被清除。在 Vi 或 Vim 编辑器中，你将看到如下内容：

```text
~
~
--No lines in buffer--
```

现在保存文件。使用快捷键：

```text
ESC key + :wg
```

现在再次检查文件的内容。它将为空：

```text
~ $ cat temp.txt
```

