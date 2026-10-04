

# 5.1 使用 Tcl 列表

set position 0;

```
proc getDatum { {
    global position;
    # 定义模拟随机顺序数据
    set rawDataList [list \
    [list KEY1 {First Name} Clif] \
    [list KEY2 jxd@example.com] \
    [list KEY2 {First Name} John] \
    [list KEY3 {Last Name} Doe] \
    [list KEY3 {First Name} Jane] \
    [list KEY1 Email Flynt] \
    [list KEY3 Email janed@example.com] \
    [list KEY1 clif@cflynt.com] \
    [list KEY2 {Last Name} Doe] ]

# 选择列表中的下一个项，如果未到末尾。
if {$position < [length $rawDataList]} {
    set data [lindex rawDataList $position]
    incr position
} else {
    set data ""
}

# 返回数据。
return $data;
}
```

# 创建一个空数据列表

set dataList "";

# getDatum 返回的数据是固定位置列表。
# 这些是位置的定义。

# 第 5 章：列表与数组

```
set keyIndex 0
set fieldIDIndex 1
set fieldDatumIndex 2
```

# 填充 dataList

```
while {[set data [getDatum]} != ""}
    set key [lindex $data $keyIndex]
    set fieldID [lindex $data $fieldIDIndex]
    set fieldDatum [lindex $data $fieldDatum]
```

# 如果是新键，创建一个新的子列表

```
if {[lsearch $dataList "*{KEY $key}**" == -1}
    append dataList [list [list KEY $key]]
```

# 提取此键的子列表，合并新数据，
# 并恢复列表

```
set recordLocation [lsearch $dataList "*{KEY $key}**"]
set record [lindex $dataList $recordLocation]
append record [list $fieldDatum]
set dataList [lreplace $dataList $recordLocation record]
```

# 显示原始数据

```
for {set i 0} {$i < [ength $dataList]} incr i {
    puts "$i: [lindex $dataList $i]"
```

# 获取键为 KEY1 的记录

```
set record [lindex $dataList [lsearch $dataList "*{KEY1**"]]

# 使用关联数组 (Associative Array)

# 显示来自 KEY1 记录的字段

set namePos [lsearch $record {First Name*}]
puts "First Name for record KEY1: [lindex $record $namePos]"
puts "Email Address for record KEY1: [lindex $record [lsearch $record {Email *}]]"

# 脚本输出
0: (KEY1) {First Name Clif} {Email clif@flynt.com}
1: (KEY2) {jxd@example.com} {Last Name Doe}
2: (KEY3) {Doe} {First Name Jane} {Email janed@example.com}

First Name for record KEY1: Clif
Email Address for record KEY1: clif@flynt.com

对于列表，这种技术运行良好。然而，`lsearch` 命令查找项的时间会随着项在列表中的位置而线性增加。长度超过 500 条的列表会变得明显缓慢。

数据与值的配对也可以通过关联数组完成。数组使用哈希表而不是线性查找来寻找键，因此速度不会随着记录的增加而下降。Tcl 关联数组可以像 Fortran 数组一样通过设置数值索引使用。如果你熟悉 Fortran 或 Basic 编程，可能会熟悉这样的结构：

```
C 数组                   Tcl 数组
int values[5];             set values(0) 1;
char desc[5][80];          set desc(0) "First"
```

# 关联数组

在 Tcl 中编程时，你可以使用非数值索引更高效地将值和描述链接在一起。

```
set value("First") 1;
```

由多个需要分组的项目组成通常在复合数据结构（如 C struct 或 Pascal record）中被收集。这些结构允许程序员处理单个数据实体，而不是多个事件，同时允许单独操作项。

在 struct 或 record 中分组信息在概念上是编译器强制执行的命名约定。当你定义结构时，命名成员并定义它们所需的存储空间。一旦完成，算法开发者通常不需要担心内存安排。只要可以通过名称访问，数据可以存储在内存的任何地方。

```
C 结构                   Tcl 数组
struct {
  int value;
  char desc[80];
} var;
```

```
var.value = 1;
strcpy(var.desc, "First");
```

# 5.3 新命令

这可能并不显而易见，但 Tcl 变量 `var` 像 struct 一样将描述和值分组。另一种数据结构是结构数组（Array of structs）。对于你的算法来说，这主要是一种命名约定。通过将关联数组索引视为某些字符分隔的字段列表（下面的示例使用了点），这种功能在 Tcl 中是可用的。

# 结构数组
Tcl 数组

```
struct {
  int value;
  char desc[80];
} var[5];

set var(0.value) 1
set var(0.desc) "First"
set var(1.value) 2
set var(1.desc) "Second"
```

```
var[0].value = 1;
strcpy(var[0].desc, "First");
var[1].value = 2;
strcpy(var[1].desc, "Second");
```

你可以创建命名约定来在 Tcl 中分组数据。Tcl 解释器并不要求你遵循任何命名约定，但你可以通过编写过程向包用户隐藏约定，从而强制执行约定。

在进入下一组示例之前，有一些新命令需要讨论。接下来的示例使用了 Tcl 异常处理调用 `error` 和 `catch`、文件系统交互命令 `file` 和 `glob`、检查命令 `info` 以及文件加载命令 `source`。

# 第 5 章：列表与数组

##5.3.1 Tcl 中的异常处理

Tcl 解释器在遇到异常条件时的默认操作是停止脚本执行并打印 `errorInfo` 全局变量中的数据。

修改这种行为的最简单方法是使用 `catch` 命令拦截异常。

```
语法:catch script ?varName?
```
- catch | 捕获错误条件并返回结果而不是终止脚本。
- script | 要评估的 Tcl 脚本。
- varName | 接收脚本结果的变量。

程序中某些情况下你可能想要生成异常。例如，在检查用户提供数据的有效性时，如果数据明显无效，你可能停止处理。

```
语法:error informationalString ?errorInfo? ?errorCode
```
- error | 生成错误条件。如果未捕获，则显示 `informationalString` 和堆栈跟踪并终止脚本。
- informationalString | 关于错误的信息。
- errorInfo | 初始化 `errorInfo` 字符串的字符串。注意关于错误的更多信息可能会附加到此字符串。
- errorCode | 放在全局变量 `errorCode` 中的标识错误号。

## 5.3 新命令

下一个示例显示了使用 `catch` 的某些方法，而 error 示例显示了使用 `catch` 和 `error` 命令的某些方法。

# 示例 5.3.1-1

```
#
# 如果第一个或第二个参数不是
# 数字，将生成错误。
# 如果参数有效，将调用
# error 命令来生成错误。

proc errorProc (first second) {
    # 如果 $first 不是数字或为0，这里将失败
    set dummy [expr 1/$first]

    # 这不会生成错误。
    # 如果 $second 不是数字，fail 将是非零。
    set fail [catch {expr 5 * $second} result]
    # 如果 $fail 被设置，生成错误
    if ($fail) {
        error "Bad second argument"
    }
    error "errorProc always fails" "evaluating error" 123
}
```

# 示例脚本

```
puts "调用带有 0 参数的 errorProc"
if {[catch errorProc 0 a) returnString]} {
    puts "errorProc 失败是因为：$returnString\n"
}

puts "调用带有错误第二个参数的 errorProc"
set fail [catch {errorProc 1 X} returnString]
if ($fail) {
    puts "errorProc 失败"
    puts "返回字符串:$returnString"
    puts "错误信息: $errorInfo\n"
}

puts "调用带有有效参数的 errorProc"
```

