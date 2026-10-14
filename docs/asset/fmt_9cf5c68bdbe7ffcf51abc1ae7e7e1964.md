
此函数从数组中取出左侧元素并返回，同时数组减少一个元素。如果没有指定数组，在非子程序环境下使用 Perl 脚本的参数 `$ARGV`；否则，使用传递给子程序的参数数组 `@_`。如果数组为空，则返回未定义。

# 示例

```
print("shift ()");

while ($arg = shift) {

print($arg, ' ');
}

print("\n");
```

## shmctl

### 合规性

### 语法

```
类别 列表运算符 (System V)
参数 id, cmd, arg
返回值 value
```

### 定义

此函数等同于 UNIX `shmctl()` 函数，并执行共享内存控制操作。

## shmget

### 合规性

### 语法

```
类别 列表运算符 (System V)
参数 key,size, flags
返回值 value
```

### 定义

此函数等同于 UNIX `shmget()` 函数并返回共享内存 ID。

## shmread

### 合规性

### 语法

```
类别 列表运算符 (System V)
参数 id, var. pos, size
返回值 value
```

### 定义

此函数等同于 UNIX `shread()` 函数并从共享内存 ID 读取数据。

## shmwrite

### 合规性

### 语法

```
类别 列表运算符 (System V)
参数 id, string, pos, size
返回值 value
```

### 定义

此函数等同于 UNIX `shmwrite()` 函数并向共享内存 ID 写入数据。

## shutdown

### 合规性

### 语法

```
类别 列表运算符 (socket)
参数 socket, how
返回值 1 (true) '' (false)
```

### 定义

此函数等同于 UNIX `shutdown()` 函数并关闭 socket。

## sin

### 合规性

### 语法

```
类别 命名一元运算符 (numeric)
参数 expression
参数 none
返回值 numeric
```

### 定义

此函数返回表达式以弧度为单位的的正弦值。如果没有显式参数，则使用 `$_`。

### 示例

```
print("sin() ",sin(4), "\n");
```

## sleep

### 合规性

### 语法

具命名一元运算符 (process)

参数 expression

参数无

返回值 numeric

### 定义

此函数使当前进程休眠 expression 中指定的秒数（如果未指定，它将无限睡眠，但如果程序编写了信号处理，则可能会被信号唤醒）。

### 示例

```
print("sleep() ",sleep(5),"\n");
```

## socket

### 合规性

### 语法

Category 列表运算符 (socket)

参数 socket, domain, type, protocol

返回值 value

## 第 15 章 -- 函数列表

### 定义

此函数等同于 UNIX socket() 系统调用，它会打开一个指定类型的 socket 并将其附加到文件句柄上。

## socketpair

### 合规性

### 语法

```
Category 列表运算符 (socket)
参数 socket1, socket2, domain, type, protocol
返回值 value
```

### 定义

此函数等同于 UNIX socket() 系统调用，在指定的域内创建一对无名的 socket。

## sort

### 合规性

### 语法

```
Category 列表运算符 (list)
参数 subname list
参数 block list
参数 list
返回值 list
```

### 定义

此函数对列表进行排序并返回排序后的列表。可以通过可选的子程序或参数指定 sort 方法。接受两个参数（作为包变量 `$a $b` 传递）的子程序如果根据使用的任何标准第一个小于或等于第二个，则返回 TRUE。同样可以指定一个块（匿名子程序）来执行此函数。默认排序顺序基于标准的字符串比较。

## 第 15 章 -- 函数列表

### 示例

```
@a = ("z","w","r","i","b","a");

print("sort()",sort(@a),"\n");
```

## splice

### 合规性

### 语法

```
Category 列表运算符 (array)

参数 array, offset, length, list
参数 array, offset, length
参数 array, offset

返回值 list
```

### 定义

此函数从数组中删除由 offset 和 length 指定的元素，并用最后一个参数提供的列表中的元素替换它们。返回被删除的元素列表。如果未指定长度，则从 offset 到数组末尾的所有项将被删除。

### 示例

```
@a = ("a","e","i","o","u");

print("splice()",splice(@a,0,3,"A","E","I"));
```

## split

### 合规性

### 语法

```
Category 列表运算符 (pattern)
```

参数 /pattern/,expression,limit

参数 /pattern/,expression

参数 /pattern/

参数无

返回值 list

```

### 定义

此函数管理字符串，将 expression 指定的字符串（如果未指定则使用 `$_`）分割为由分隔符模式表示的字符串数组（如果模式没有指定空白，则将其作为默认值）。可选的 limit 限制了返回元素的数量。负数限制没有影响。

如果不在列表上下文中，返回找到的元素数量。在标量上下文中，它返回元素数量并将数组放入 @ 中（将 @_ 的数组作为结果已废弃）。

### 示例

```
print("split() ",split(:/,"1:2:3:4:5","\n"))
```

## sprintf

### 合规性

### 语法

```
Category 列表运算符 (string)

参数 format, list

返回值 string
```

### 定义

这等同于 C 语言的 `sprintf()` 调用。格式是一个带有元字符的字符串，用于指定后续有多少个值/变量以及如何在结果字符串中表示这些值。这实现了浮点数和整数的显式格式化（同时也允许二进制、十六进制和八进制格式）。

### 示例

```
print("sprintf() ",sprintf("%0d \n",9,"\n"))
```

## sqrt

### 合规性

### 语法

具命名一元运算符 (numeric)
参数 expression
返回值 numeric

### 定义

此函数返回计算表达式并寻找其平方根的结果。

### 示例

```
print("sqrt()",sqrt(4),"\n");
```

## srand

### 合规性

### 语法

具命名一元运算符 (numeric)
参数 expression
参数无
返回值 1 (true) '' (false)

### 定义

此函数使用 `rand()` 数字为伪随机数生成算法设置种子。为了随机化可能的序列，每次调用脚本时都应该将种子设置为不同的值。当未提供 expression 时，默认行为是使用调用 `time()` 的结果。这不是一种随机脚本的安全方法，因为可以预测将返回什么序列。

注意，当使用 `rand()` 使用一组伪随机数据时，可以通过简单的设置和保存种子来重复生成相同的数据。恢复种子并调用 `rand()` 将再次产生相同的序列。

### 示例

```
srand(26);

print("rand", rand()," ");

srand(26);

print(rand()," (should produce the same \"random\" number twice) \n");
```

## stat

### 合规性

### 语法

| Category 列表运算符 (files) |
| 参数 handle |
| 参数 expression |
| 参数无 |
| 返回值 list |

### 定义

此函数返回句柄指向的文件统计信息。注意，像 `stat()` 一样，它可以接受一个特殊参数。

### 示例

```
($device, $inode, $mode, $nlink, $uid, $gid,$rdev, $size,$atime,$mtime,$ctime,$blocks) = stat("/etc/passwd");

print("stat(),"n");
```

## study

### 合规性

### 语法

```
具命名一元运算符 (pattern)

参数 scalar

参数无

返回值 1 (true) '' (false)
```
