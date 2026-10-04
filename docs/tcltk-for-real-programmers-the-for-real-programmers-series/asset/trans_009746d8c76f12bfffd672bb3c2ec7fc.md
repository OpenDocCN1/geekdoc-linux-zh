

## 3.3 Tcl 命令

get 返回此关联数组中使用的索引和值的列表。

arrayName 数组名称。

# 示例 3.3.7-2

# 数组示例

```
set fruit(apple.cost) .10
set fruit(apple.count) 5
set fruit(pear.cost) .15
set fruit(pear.count) 3
```

```
foreach item [array names fruit *cost] {
    set type [split $item "." 0]
    puts "There are ${fruit($type.count)} units in stock"
    puts "The cost is ${fruit($item)} in stock"
    puts "The ${type} inventory is worth: \
    [expr $fruit($item) * $fruit($type.count)]"
}
```

```
puts ""
puts "Indices and values of fruit:\
[array get fruit]"
```

# 脚本输出

apple 的成本是 .10
There are 5 units in stock
The apple inventory is worth: .5
pear 的成本是 .15
There are 3 units in stock
The pear inventory is worth: .45

Indices and values of fruit:
apple.count 5
apple.cost .10
pear.count 3
pear.cost .15

## 3.4 Tcl 中的输入/输出

如果不接受数据并交付结果，很难进行任何实际的编程。Tcl 将输入和输出抽象为两个输入命令和一个输出命令。通过使用这三个命令，你可以读取或写入任何文件、管道、设备或 socket。Tcl 中所有的 I/O 都是通过通道（channels）完成的。通道是一种类似于 Unix 流的抽象模型。Tcl 通道抽象扩展流层之外，包含了 socket 和管道。通道通过句柄（handles）访问，句柄被视为文件。打开通道的 Tcl 命令是 gets 和 read。这些通道在 Tcl 中预定义：

- stdin 标准输入：键盘或重定向的文件。
- stdout 标准输出：通常是屏幕。
- stderr 错误输出：通常是屏幕。注意 Windows 不区分 stdout 和 stderr。

### 3.4 输出

puts 命令将输出发送到通道。它需要一个字符串作为参数。默认情况下，此命令会在字符串末尾添加一个换行符。

```
Syntax: puts ?-noneline? ?channel? outputString
```

```
puts 将一个字符串发送到通道。
?-noneline? 不向输出中添加换行符。
?channel? 将输出发送到此通道。否则，发送到标准输出。
outputString 要发送的数据。

# 示例 3.4.1-1

```
puts "Hello, World"
puts -noneline "Hello, World"
```

## 3.4.2 输入

用于输入数据的 Tcl 命令是 gets 和 read。gets 命令将从通道中读取单行输入并去除任何换行符。gets 命令可能会返回读取的数据，也可能返回读取的字符数。read 命令将读取指定数量的字符，或者读取到数据末尾，并且始终返回数据。gets 命令最适合交互式 I/O。read 命令最适合需要读取大量文本的情况，例如文件或将有大量数据要传递给程序的 socket 连接。

Syntax: gets channelID ?varName?

-   gets 从通道中读取一行数据。
-   channelID 从此通道读取。
-   varName? 如果此变量存在，则数据将存储在该变量中，并返回读取的字符数。如果此参数不存在，则返回该行数据。

# 示例 3.4.2-1

```
% gets stdin # 用户在键盘上输入 "Hello, World"。
Hello, World
% gets stdin # 用户在键盘上输入 "Hello, World"。
Hello, World
% puts $inputStream
Hello, World
```

可以调用 read 命令从通道中读取字符，直到读取到指定数量的字符，或者读取到 read 返回文件末尾（End-of-File）。如果调用 read 命令读取指定数量的字符，但在读取请求的字符之前遇到了文件末尾，它不会产生错误。read 命令返回读取到的字符。read 命令可能会剥离最后的换行符，但默认情况下保持换行符完好。

Syntax: read channelID numBytes

-   read 从通道中读取指定数量的字符。
-   channelID 用于读取数据的通道。
-   numBytes 要读取的字节数。

Syntax: read ?-nonline channelID

-   read 从通道读取数据，直到达到文件末尾（EOF）条件。
-   ?-nonline 如果最后一个字符是换行符则将其丢弃。
-   channelID 用于读取数据的通道。

# 示例 3.4.2-2

```
# 从 stdin 读取直到遇到文件末尾
% read stdin # 用户输入 "Hello, World" 然后输入 EOF
Hello, World
```

# 从 stdin 读取 5 个字符
% read stdin 5 # 用户输入 "Hello, World"
Hello

## 3.4.3 打开通道

可以通过 open 命令或 socket 命令创建通道。open 命令可用于打开指向文件、设备或通往另一个程序的管道。socket 命令可用于打开到服务器的客户端 socket，或打开一个监听客户端的服务器 socket。

open 命令用于创建指向文件、设备或通往另一个程序的通道。

Syntax: open fileName ?access? ?permissions?

-   open 打开一个文件、设备或通往另一个程序的管道。
-   fileName 要打开的文件名。
-   access? 打开文件时的模式（例如，r, w）。
-   permissions? 如果创建了新文件，将用此设置权限。

# 示例 3.4.3-1

# 文件输出和输入示例

```
# 打开文件进行写入
set outputFile "testfile" "w"

# 向文件发送一行。
puts outputFile "This is line 1"
puts outputFile "This is line 2"
puts outputFile "This is line 3"

# 关闭文件
close $outputFile

# 重新打开文件读取
set inputFile "testfile" "r"

# 读取一行文本
set numBytes [gets $inputFile string]

# 显示读取的行
puts "Gets returned $numBytes characters in the string: $string"

# 读取文件的剩余部分
set string2 [read $inputFile]
puts "Read: $string2"

```

# 打开管道

```
# 打开到 ls 命令的管道
set pipe [open "|ls /" "r"]

# 读取 ls 命令的输出：
while {![eof $pipe]} {
    set length [gets $pipe lsLine]
    puts "$lsLine"
}
```

# 脚本输出

Gets returned 14 characters in the string: This is line 1
Read: This is line 2
This is line 3

打开管道

```
bin
boot
bsd
dev
```

