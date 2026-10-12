
### 3.4.2 交换文件

交换到文件通常比交换到原始分区慢，因此这不是推荐的持久技术。然而，如果临时需要更多交换空间，创建交换文件是一个快速修复方法。你可以拥有多达 8 个交换文件，每个大小可达 16 MB。以下是制作交换文件的步骤：

- 创建一个指定大小的交换文件：

```
dd if=/dev/zero of=/swapfile bs=1024 count=8192
```

`dd` 命令物理上创建了 `swapfile`，块大小（`bs`）为 1024，块数（`count`）为 8192，总大小约为 8 MB。（在上面的示例中，输入文件 (`if`) 是 `/dev/zero`，输出文件 (`of`) 是 `/swapfile`。）

- 使用命令格式化文件：

```
mkswap /swapfile
```

- 使用命令启用交换：

```
swapon /swapfile
```

如果你需要禁用交换，可以使用：

```
swapoff /swapfile
```

## 3.5 Shell

### 3.5.1 什么是 Shell？

Shell 是用户和操作系统内核之间的接口程序。它接收用户的命令并将其传递给内核。Linux 中有很多类型的 Shell。最常见的有 `bash` (Bourne Again Shell)、`csh` (C shell)、`tcsh` (enhanced C shell) 和 `ksh`。

### 3.5.2 我如何编写 Shell 脚本？

Shell 脚本是由 Shell 执行的包含一系列命令的文本文件。脚本通常具有 `.sh` 扩展名，但这不是要求的。创建脚本，你可以使用任何文本编辑器如 `vi` 或 `nano`。

例如，创建一个名为 "untar" 的脚本来提取压缩包：

```bash
#!/bin/bash
echo this is the script $0
echo untarring the file $1
# this calls tar with options -xvzf (extract, verbose, filter through gzip, input filename)
tar -xvzf $1
```

脚本的第一行以 `#!`（称为 shebang）开头，这是特殊的——它告诉 shell 该用什么程序来解释脚本。在示例中，脚本由 `bash` shell `/bin/bash` 解释。第一行必须以 `#!` 开头，否则脚本将无法运行（文件将被视为纯文本文件）。

脚本中的 `$0`, `$1`, `$2` ... 是传递给脚本的参数。例如，如果我运行带有七个参数的脚本 "myscript："

```
myscript a b c d e f g
```

那么 `$0` 在 "myscript" 内部的值为 "myscript"，`$1` 将拥有值 "a"，`$2` 为 "b"，`$3` 将是 "c"，以此类推。

在我示例脚本的第二行和第三行中，`echo` 命令在屏幕上打印该行之后的所有内容，将 `$0` 和 `$1` 扩展为传递给脚本参数的值。第四行是我写给自己的注释，用来提醒我想要实现的目标，以防我以后需要修改脚本。第五行执行实际工作。

一旦脚本编写完成，我为文件所有者添加执行权限：

```
chmod u+x untar
```

这样我的脚本就可以使用了：

```
./untar my_tar.tar.gz
```

Linux 脚本功能非常丰富、灵活、强大，且可能很复杂。然而，为常见任务编写简单的自动化脚本并不需要特殊知识。你只需要将一组常用的命令一个一个地组合到一个文件中即可。我使用脚本是因为我太懒了，不想又一遍地输入相同的组命令。

## 3.6 简单编程

### 3.6.1 如何编写一个简单的 Python 程序？

与编写 shell 脚本非常相似。创建/编辑一个包含你的 Python 程序的文本文件：

```
pico try_python
```

输入一些简单的 python 代码查看它是否可以运行：
