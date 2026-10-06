
目录名是完整路径名或`.`（单个点，表示当前目录）。

以下是可与`find`命令一起使用的项目列表：

- `-name filename`：指定要搜索的文件名（包括通配符）。你必须在引号内指定它们。也可以使用通配符范围。如果你想使用通配符，请输入`*`。如果你指定`"test[1-2]"`，你将找到所有以 test 开头且最后一位字符为 1 或 2 的文件，即`test1`和`test2`。
- `-size Number`：指定用于搜索的文件大小。指定的文件大小以块为单位。如果你想匹配小于指定大小的文件，请在大小前使用`-`（减号）；如果你想匹配大于指定大小的文件，请在大小前使用`+`（加号）。例如，`-size 5`将匹配大小为 5 块的文件（在匹配时总是会向上取整），`-size -5c`将匹配大小小于或等于 5 字节的文件，`-size +5c`将匹配大小大于 5 块的文件。
- `-size Number`：指定用于搜索的文件大小。数字末尾的`c`表示文件大小以字节为单位。如果你想匹配小于指定大小的文件，请在大小前使用`-`（减号）；如果你想匹配大于指定大小的文件，请在大小前使用`+`（加号）。例如，`-size -50c`将匹配大小小于或等于 50 字节的文件，`-size +50c`将匹配大于 50 字节的文件。
- `-prune`：限制`find`命令处理目录。默认情况下，`find`会处理所有目录和子目录。
- `-atime number`：搜索在指定 24 小时内访问过的文件。24 小时的计算方式为指定数字加 1。0 表示过去的 24 小时。
- `-mtime number`：搜索在指定 24 小时内修改过的文件。24 小时的计算方式为指定数字加 1。0 表示过去的 24 小时。
- `-ctime number`：搜索在指定 24 小时内索引节点（inode）被修改的文件。24 小时的计算方式为指定数字加 1。0 表示过去的 24 小时。
- `-type file`：搜索特定类型的文件。以下是可选类型列表：
  - `b`--块文件（Block file）
  - `c`--字符文件（Character file）
  - `d`--目录（Directory）
  - `f`--普通文件（Regular file）
  - `l`--符号链接（Symbolic link）
  - `p`--命名管道（FIFO）
  - `s`--套接字（Socket）
- `-user username`：搜索所有者匹配指定用户名的文件。
- `-perm permission`：搜索具有指定权限的文件。权限指定为三位进制。如果权限前是`-`，则与文件权限精确匹配；如果权限前是`-`，则与指定权限与。例如，如果你想搜索具有读取权限的文件，使用`perm -400`。
- `-newer filename`：搜索修改时间在该文件之后的文件。
- `-group groupname`：搜索属于指定组的文件。
- `-inum Number`：搜索索引节点匹配指定数字的文件。
- `-links Number`：搜索具有指定链接数的文件。要匹配链接数，在链接数前使用`-`（减号）；如果你想匹配大于指定链接数的文件，在链接数前使用`+`（加号）。
- `-ls`：列出当前路径的以下属性：
  - 索引节点数
  - 千字节大小（1024 字节）
  - 保护模式
  - 用户
  - 组
  - 字节大小
  - 修改时间
- `-exec command`：执行命令。对命令找到的文件列表执行命令，后面接`{ \;`（斜杠分号）。
- `-ok command`：执行命令。对命令找到的文件列表执行命令，后面接`{ \;`（斜杠分号）。
- `-u`：在执行命令前请求确认。
- `-print`：打印搜索结果输出。

这些运算符可以相互结合形成复杂的搜索标准。你可以这样组合多个运算符：

- `-a`运算符：搜索符合两个指定的文件。
- `-o`运算符：搜索满足指定条件之一的文件。
- `!`运算符：搜索不符合指定条件的文件。

示例假设当前目录下存在以下文件：

```
ls -al

total 64

drwxrwx-- 3 tester author 3072 Nov 25 00:41 .

drwxr-xr-x 36 root system 2048 Nov 23 19:51 .

--rw-r--r-- 1 tester author 0 Nov 24 14:54 .dot1

--rw-r--r-- 1 tester author 10 Nov 24 17:36 test1

drwxr-xr-x 2 tester author 512 Nov 24 17:32 test2

-r-x--r-- 1 tester author 0 Nov 24 14:58 test3

--rw-r--r-- 1 tester author 0 Nov 24 17:33 test4

--rw-r--r-- 1 tester author 15647 Nov 24 18:32 test5
```

在最简单的形式下，你可以执行以下命令来获取当前目录及其子目录中所有文件的列表。

```
find -print

./test5

./test1

./test3

./test4

./test2

./test2/test21

./test2/test22

./dot1
```

如果你想搜索当前目录下在过去 24 小时内修改过的所有文件，如下所示使用`-mtime`运算符：

```
find -mtime 0 -print

./test5

./test1

./test3

./test4

./test2

./test2/test21

./test2/test22

./dot1
```

要搜索权限为 600（仅所有者具有读和写权限）的文件，请使用`-perm`运算符执行以下命令：

```bash
find . -perm 600 -print
./test1
```

在这种情况下，权限恰好为 600 的文件会被显示。然而，如果你想搜索具有读写权限的文件，请在 600 前加一个连字符`-`执行以下命令：

```bash
find . -perm -600 -print
./test5
./test1
./test4
./test2
./test2/test1
./test2/test2
./dot1
```

如果你对搜索目录感兴趣，请使用`-type`操作符并执行以下命令：

```bash
find . -type d -print
./test2
```

要获取有关找到的文件的更多信息，请使用`-ls`操作符执行以下命令：

```bash
find . -ls
```

要搜索所有以 test 开头的文件，请使用`-name`操作符并执行以下命令：

```bash
find -name "test*" -print
./test5
./test1
./test4
./test2
./test2/test1
./test2/test2
```

如你所见，`find`命令遍历了子目录`test2`并获取了文件名。如果你想将搜索限制在当前目录并排除子目录，请使用`-prune`操作符并执行以下命令：

```bash
find -name "test*" -prune -print
./test5
./test1
./test4
./test2
```

要找到当前目录中比`test1`文件新的文件列表，请使用`-newer`操作符并执行以下命令：

```bash
find . -newer test1 -print
./test5
./test2/test21
```

另一方面，如果你想找到比`test1`文件旧的文件列表，请在以下命令中使用否定操作符`!`结合`-newer`操作符：

```bash
find ! -newer test1 -print
./test3
./test4
./test2
./test2/test22
./dot1
```

如果你想要所有大小恰好为 10 字节的文件列表，请使用`-size`操作符并执行以下命令：

```bash
find . -size 10c -print
./test1
```

如果你想列出所有大小小于 10 字节的文件，请执行以下命令（该命令与之前的完全相同，只是 0 前多了一个连字符）：

```bash
find . -size -10c -print
./test3
./test4
./test2/test21
./test2/test22
./dot1
```

如果你想列出所有大小为 0 的文件，请如下方式使用`-exec`参数执行`find`命令：

```bash
find -size 0c -exec ls -l {} \;
```

如果你想删除所有大小为 0 的文件，但想在实际删除之前确认，请使用`-ok`操作符执行以下命令：

```bash
find . -size 0c -ok rm \;
```

## more 命令用法

如前所述，`more`命令会在每页结束时暂停。当`more`暂停时，可以使用多个子命令来控制其后续行为。这些子命令如下：

- 空格键：向前翻页，如果未指定行数，则翻一页。
- `d`：如果未指定，则向前翻默认行数（通常为 11 行），如果指定，则按行数翻页。
- `z`：如果指定了行数，则向前翻页；否则翻一页。
- `s`：跳过指定的行数并显示一页。如果未指定，则显示下一行。
- `f`：向后跳转指定的屏幕数。如果未指定，则显示下一页。
- `b`：向后跳转指定的屏幕数。如果未指定，则显示上一页。
- `Ctrl-B`或`Ctrl-b`：向后跳转指定的屏幕数。如果未指定，则显示上一页。
- `q`：退出`more`命令行。
- `v`：调用`vi`编辑器。
- `number/expression`：搜索表达式及其指定的出现次数。如果文件中出现的次数少于指定的次数，则显示保持不变。
- `n`：正向搜索最后输入的表达式的指定出现。如果未指定次数，则搜索下一个出现处并显示屏幕。
- 输入`q`或`Q`（后按回车键）退出`more`命令。
- 输入单个句号（`.`）重复上一次执行的命令。

**示例** 假设我们在当前目录下有一个名为`file1`的文件。该文件的内容所示：

```
This is the line 1
This is the line 2
This is the line 3
This is the line 4
This is the line 5
This is the line 6
This is the line 7
This is the line 8
This is the line 9
This is the line 10
This is the line 11
This is the line 13
This is the line 14
This is the line 15
This is the line 16
This is the line 17
This is the line 18
This is the line 19
This is the line 20
This is the line 21
This is the line 23
This is the line 24
This is the line 25
```

如果你想显示`file1`，请使用以下命令：

```
more file1
```

这种方法有一个缺点，即一旦到达文件末尾，`more`命令就会退出。如果你希望在到达文件末尾时也不退出`more`命令，请使用`-w`标志。这在你查看一个正在创建的文件时特别有用。以下命令显示了`-w`标志的用法：

```
more -w file1
```

如果你想从文件的底部而不是顶部开始并向后移动，请像下面的命令一样使用`+g`标志：

```
more +g file1
```

如果你想从`file1`的第 20 行开始显示文件，请使用以下命令：

```
more +20 file1
```

如果你想显示五个文件：`file1`, `file2`, `file3`, `file4`和`file5`，请执行以下命令：

```
more file1 file2 file3 file4 file5
```

```
less
```

`less`命令是查看文件内容的命令族中的一个。它可能在所有 UNIX 系统上默认可用。它的行为与`more`命令类似。`less`命令默认允许你向文件中向前和向后移动。

以下是进入`less`命令后可以使用的子命令列表：

- `-h`显示可用子命令列表。
- 空格键或`Ctrl-v`或`Ctrl-f`向前移动一页。如果前面有数字，则向前移动指定的行数。
- 回车键或`Ctrl-n`或`Ctrl-e`或`j`向前移动 1 行。如果前面有数字，则向前移动指定的行数。
- `Ctrl-b`或`b`在文件中向后移动一屏。如果前面有数字，则向后移动指定的行数。
