
## 访问时间测试

有几个选项用于测试 `access time`（访问时间），即文件最后一次被读取或写入的时间。`-anewer` 选项检查一个文件的访问时间是否比指定文件更近。`-atime` 测试文件被访问了多少天前。`-amin` 以分钟为单位检查访问时间。

同样，你可以使用 `-cnewer`、`-ctime` 和 `-cmin` 检查 inode 更改时间。inode 时间通常（但不总是）代表文件创建的时间。你可以使用 `-newer`、`-mtime` 和 `-mmin` 检查 `modified time`（修改时间），即文件最后一次被写入的时间。

要查找未在超过一天时间内更改的文件：

```
$ find . -name "*.sh" -type f -mtime +0
./archive/old_orders.txt
```

要查找在过去 10 到 60 分钟内被访问过的文件：

```
$ find . -name "*.txt" -type f -amin +9 -amin -61
./orders.txt
./advocacy/linux.txt
```

## 文件大小测试

`-size` 选项测试文件大小。默认测量单位是 512 字节块，这对许多用户来说反直觉，且是常见的错误来源。与具有不同时间测量选项的时间测量选项不同，要更改 `size` 的测量单位，必须在数值后跟随 `b (bytes)`、`c (characters)`、`k (kilobytes)` 或 `w (16-bit words)`。没有 `m (megabytes)`。与时间测量一样，数值可以有减号 (`-`) 来测试小于指定大小的文件，或加号 (`+`) 来测试更大的文件。

例如，使用此命令查找大于 1MB 的日志文件：

```
$ find . -type f -name "*.log" -size +1024k
./logs/giant.log
```

## 输出与执行

`find` 将匹配的路径显示在标准输出上。历史上，必须使用 `-print` 选项。现在，对于大多数类 Unix 操作系统（包括 `Linux`），打印输出是默认行为。如果兼容性是个问题，请在 `find` 参数末尾添加 `-print`。

要对成功匹配执行不同的操作，请使用 `-exec`。`-exec` 选项在每个匹配的文件上运行一个程序。这通常与 `rm` 结合使用以删除匹配文件，或与 `grep` 结合使用以进一步测试文件是否包含特定模式。通过一对花括号（`{}`）将文件名插入到命令中，并且命令以一个转义的分号结尾。（如果分号未转义，shell 会将其解释为 `find` 命令的结束，而不是命令的一部分。）

```
$ find . -type f -name "*.txt" -exec grep Table {} \;
Pine Round Table,375.99,1,757
Pine Round Table,375.99,1,757
```

可以指定多个操作。要在 `grep` 匹配后显示文件名，请包含 `-print`。

```
$ find . -type f -name "*.txt" -exec grep Table {} \; -print
./orders.txt
Pine Round Table,375.99,1,757
./archive/old_orders.txt
```

`find` 期望 `{}` 单独出现（即周围有空格）。它不能与其他字符组合，例如尝试形成新的路径名。

对于大量文件，`-exec` 选项可能速度较慢：命令必须在每个匹配项上执行。当可以选择将结果管道传输到第二个命令时，执行速度比使用 `-exec` 时显著更快。管道通过两个命令而不是数百或数千个命令生成结果。

`-ok` 选项的工作方式与 `-exec` 相同，除了它会交互式地验证是否应该运行该命令。

```
$ find . -type f -name "*.txt" -ok rm {} \;
< rm ... ./orders.txt > ? n
< rm ... ./advocacy/linux.txt > ? n
< rm ... ./advocacy/old_orders.txt > ? n
```

`-ls` 操作选项以更多细节列出匹配文件。`find` 为每个匹配文件运行 `ls -dils`。

```
$ find . -type f -name "*.txt" -ls
243000    4 -rw-rw-r--   1 kburtch    kburtch       592 May 17 14:41 ./orders.txt
114683    0 -rw-rw-r--   1 kburtch    kburtch         0 May 17 14:41 ./advocacy/1
```

## 排序

`Linux` 的 `sort` 命令用于对单个文件或多个文件进行排序。文件可以显式命名，也可以通过重定向标准输入进行排序。`sort` 的开关与其他命令（如 `grep` 或 `cut`）完全不同。`sort` 是最后几个支持长选项版本的命令之一；因此，这里使用的是短选项。即便如此，常用选项的开关也与其他 `Linux` 命令不同。

要正确地对文件进行排序，`sort` 命令需要知道排序键，即每行中决定行顺序的字符。对于排序而言，键以外的任何内容都会被忽略。默认情况下，整行被视为键。

`-f`（合并大小写）开关执行不区分大小写的排序（不像许多其他 `Linux` 命令那样使用 `-i` 开关）。

```
$ sort -f orders.txt
Bar Stool,45.99,1,756
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Bunk Bed,705.99,1,757
Cedar Armoire,825.99,1,757
Cedar Toy Chest,65.99,1,757
Chair - Rocking,287.99,1,757
Garden Bench,149.99,1,757
Grandfather Clock,2045.99,1,756
Lawn Chair,55.99,1,756
Mahogany Writing Desk,463.99,1,756
Pine Round Table,375.99,1,757
Queen Bed,925.99,1,757
Reclining Chair,1599.99,1,757
Rocking Chair,287.99,1,757
Six-drawer Dresser,525.99,1,757
Small Bookcase Oak Veneer,205.99,1,756
Two-drawer Nightstand,125.99,1,757
Victorian-style Sofa,1225.99,1,757
Walnut TV Stand,388.99,1,756
```

`-r`（反向）开关会反转排序顺序。

```
$ head orders.txt | sort -f -r
Two-drawer Nightstand,125.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Six-drawer Dresser,525.99,1,757
Reclining Chair,1599.99,1,757
Queen Bed,925.99,1,757
Pine Round Table,375.99,1,757
Cedar Toy Chest,65.99,1,757
Bunk Bed,705.99,1,757
Bookcase Oak Veneer,205.99,1,756
Birchwood China Hutch,475.99,1,756
```

如果只使用行的一部分作为键，则使用 `-k`（键）开关来确定使用哪些字符。字段分隔符是任何一组空格或制表符字符，但你可以使用 `-t` 开关更改此设置。

要对订单文件的前 10 行按第二个及后续字段进行排序，请使用以下命令：

```
$ head orders.txt | sort -f -t, -k2
Two-drawer Nightstand, 125.99, 1,756
Reclining Chair, 1599.99, 1,757
Bookcase Oak Veneer, 205.99, 1,756
Small Bookcase Oak Veneer, 205.99, 1,756
Pine Round Table, 375.99, 1,757
Birchwood China Hutch, 475.99, 1,756
Six-drawer Dresser, 525.99, 1,757
Cedar Toy Chest, 65.99, 1,757
Bunk Bed, 705.99, 1,757
Queen Bed, 925.99, 1,757
```

键的位置后可以跟随结束位置，用逗号分隔。例如，要仅根据第二个字段进行排序，请使用键 `-k 2,2`。

如果字段编号包含小数部分，则它表示键开始的该字段中的字符。字段中的第一个字符为 `1`。第一个字段始终从行首开始。例如，要忽略第一个字符进行排序，请指定键从第一个字段的第二个字符开始。
