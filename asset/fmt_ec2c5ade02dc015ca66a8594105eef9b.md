
`wc [-clw] [--bytes] [--chars] [--lines] [--words] [file ...]`

### 重要标志和选项

- `-c`/`--bytes`/`--chars`：仅显示字节数。
- `-l`/`lines`：仅显示行数。
- `-w`/`words`：仅显示单词数。

结果按顺序显示：字符、单词、行。值用空格分隔。

## whereis

尝试定位一个多个命令的二进制文件、源代码和 man 页文件。

```
whereis [-bms] [-Bms directory ... -f] file ...
```

- `-b`：仅搜索二进制文件。
- `-B directory ... -f`：仅在指定的目录下搜索二进制文件。`f` 标志用于分隔目录列表结束与文件参数列表的开始。
- `-m`：仅搜索 man 页。
- `-M directory -f`：仅在指定的目录下搜索 man 页。`f` 标志用于分隔目录列表结束与文件参数列表的开始。
- `-s`：仅搜索源代码。
- `-S directory ... -f`：仅在指定的目录下搜索源代码。`f` 标志用于分隔目录列表结束与文件参数列表的开始。

`whereis` 命令至少会在以下目录搜索其尝试定位的程序：

```
/bin
/usr/bin
/etc
/usr/etc
/sbin
/usr/sbin
/usr/games/bin
/usr/emacs/etc
/usr/lib/emacs/19.22/etc
/usr/lib/emacs/19.23/etc
/usr/lib/emacs/19.24/etc
/usr/lib/emacs/19.25/etc
/usr/lib/emacs/19.26/etc
/usr/lib/emacs/19.27/etc
/usr/lib/emacs/19.28/etc
/usr/lib/emacs/19.29/etc
/usr/lib/emacs/19.30/etc
/usr/Tex/bin
/usr/tex/bin
/usr/interviews/bin/LINUX
/usr/bin/X11
/usr/X11/bin
/usr/X11R5/bin
/usr/X11R6/bin
/usr/X386/bin
/usr/local/bin
/usr/local/etc
/usr/local/sbin
/usr/local/games
/usr/local/games/bin
/usr/local/emacs/etc
/usr/local/Tex/bin
/usr/local/tex/bin
/usr/local/bin/X11
/contrib/hosts
/include/g++
```

## which

### 描述

显示一个或多个程序的完整路径。只有在 `PATH` 环境变量指定的程序会被显示。

### 语法

```
which program ...
```

### 重要标志和选项

无

## whoami

### 描述

显示有效用户 ID。

### 语法

```
whoami
```

### 重要标志和选项

无

## ypdomainname

### 描述

显示系统的域名。

### 语法

```
ypdomainname
```

### 重要标志和选项

无

## zcat

解压一个多个压缩文件并将结果输出到标准输出。如果未指定文件，则对标准输入进行操作。

### 语法

```
zcat [-f] [file ...]
```

### 重要标志和选项

- `-f`,`--force`：即使对应文件已存在也强制解压，将被解压后的文件覆盖。

## zgrep

在多个压缩文件中搜索指定的模式。

### 语法

```
zgrep [options] pattern file ...
```

### 重要标志和选项

无

### 说明

有关可能的项列表和语法，请参阅 `grep` 命令。

## zip

从一个多个文件和目录创建 ZIP 存档。

### 语法

```
zip [-eff] [zipfile ...]
```

### 重要标志和选项

- `@`：接受标准输入的文件列表。
- `-e`：密码后加密存档。
- `-f`：只有当文件比存档中的文件新时才替换存档中的项。
- `-F`：修复存档。
- `-g`：将文件添加到现有存档。
- `-m`：将文件移动到存档，一旦进入存档即从原始位置删除。
- `-r`：递归处理目录，将子目录中的所有文件添加到存档。
- `-S`：包含存档中的隐藏文件。
- `-u`：如果文件更新或不存在，则替换存档中的项。

### 说明

`zip` 命令提供了许多对程序行为有用的其他选项。参阅 `zip` man 页面。

## zipgrep

使用 `egrep` 在 ZIP 存档的多个文件中搜索模式。如果未指定存档文件，则搜索存档中的所有文件。

### 语法

```
zipgrep [options] pattern zipfile ...
```

### 重要标志和选项

无

### 说明

关于 `egrep` 和 `zipgrep` 的语法，请参阅 `egrep` 命令。

## zipinfo

### 描述

显示 ZIP 存档的详情，包括加密状态、压缩类型、创建存档的操作系统等。默认情况下，存档中的每个文件单独列出。如果未指定文件，则处理标准输入。

### 语法

```
zipinfo [-lm] zipfile [file ...]
```

### 重要标志和选项

- `-1`：分行列出所有文件名。
- `-2`：列出文件名，包括尾和注释。
- `-l`：以长格式列表（类似于 -1）。
- `-M`：以类似于 more 的方式显示信息。

## zmore

每次屏幕显示压缩文本文件的内容，允许像 `more` 命令一样进行搜索。如果未指定文件，将使用标准输入。

### 语法

```
zmore [file ...]
```

### 重要标志和选项

无

### 说明

查看 `zmore` 页面以获取查看文件时可完整命令列表。

## znew

将压缩文件 `(.Z)` 转换为 gzip 使用的格式 `(.gz)`。如果未指定文件，则处理标准输入。

### 语法

```
znew [-fKt] [file ...]
```
