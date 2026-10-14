
## `$MULTILINE_MATCHING`

短名: `$1`
作用域: `local` (只读)

该变量用于指示匹配是否为多行模式。

## `$SOFMT`

短名: `$1`
作用域: `local` (只读)

该变量包含了上次匹配使用的格式字符串。

## `$SOS_ERROR`

短名: `$1`
作用域: `local` (只读)

该变量包含了格式操作的错误。

## `$OUTPUT_AUTOUSH`

短名: `$1`
作用域: `local` (只读)

该变量用于自动刷新输出缓冲区。

## `$OUTPUT_FIELD_SEPARATOR`

短名: `$1`
作用域: `local` (只读)

该变量包含了输出的字段分隔符。

## `$OUTPUT_RECORD_SEPARATOR`

短名: `$1`
作用域: `local` (只读)

该变量包含了输出的记录分隔符。

## `$SPERDB`

短名: `$1`
作用域: `local` (只读)

该变量用于设置速度。

## `$PERL_VERSION`

短名: `$1`
作用域: `global` (只读)

该变量包含了 Perl 解释器的版本。

## `$POSTMATCH`

短名: `$1`
作用域: `local` (只读)

该变量包含了匹配之后的字符串部分。

## `$PREMATCH`

短名: `$1`
作用域: `local` (只读)

该变量包含了匹配之前的字符串部分。

## `$PROCESS ID`

短名: `$$`
作用域: `global` (只读)

该变量包含了当前进程的 ID。

## `$PROGRAM NAME`

短名: `$0`
作用域: `global` (只读)

该变量包含了脚本名称。

## `$REAL GROUP ID`

短名: `$>`
作用域: `global` (只读)

该变量包含了当前进程的真实组 ID。

## `$REAL USER ID`

短名: `$<`
作用域: `global` (只读)

该变量包含了当前进程的真实用户 ID。

## `$SUBSCRIPT_SEPARATOR`

短名: `@`

## `$SYSTEM_FD_MAX`

短名: `$1`
包含了系统允许的最大文件描述符数量。

## `$WARNING`

短名: `!`
作用域: `global` (只读)

该变量包含了最后的警告信息。

## `%ENV<variable_name>,<variable_name>`

该哈希允许访问。

## `%INC<file-name>,<file-load-status>`

该哈希包含了加载模块的信息。

## `$SIG<signal_name>,<signal_value>`

该变量允许设置和检查信号处理程序。

## `@ARGV`

短名: `@ARGV`
作用域: `global` (只读)

该数组包含了传递给脚本的命令行参数。

## `@INC`

短名: `@INC`
作用域: `global` (只读)

该数组包含了包含模块的路径。

## 第 13 章 -- 特殊变量

作用域：本地化

此变量提供了对脚本所使用的 Perl 可执行文件的访问。

示例：

```
print "Executable name of Perl is: \$X\n";
```

## `$FORMAT_FORMFEED`

短名称：`$^L`
作用域：全局到全局文件句柄
文件句柄调用：`format_formfeed FILEHANDLE EXPR`

当你使用 Perl 格式命令时，可以指定格式来处理文本的居中和其他格式。另一个额外选项是指定在文件输出的页面之间插入的精确代码。默认值是换页符 (`\f`)，但该值可以被更改。

示例：

```
if ($^L = '\f')
{
    print "The formfeed character is the default break between pages.\n";
}
```

`$^L` 变量在 Perl 4 中不可用。

## `$FORMAT_LINES_LEFT`

短名称：`$-`
作用域：本地
文件句柄调用：`format_lines_left FILEHANDLE EXPR`

当你使用 Perl 格式命令时，此计数器（存在于每个关联格式的文件句柄中）每行都会递减，直到达到零，此时会生成新页面。你可以手动将此变量设置为零，以强制在输出中分页。

示例：

```
format EG_FORMAT =
@<<<<<<<< @@@>>>>>> ^||||||
$one,    $two,    $three  $fitme
.
open(EG_FORMAT,">-");
```

## `$FORMAT_LINES_PER_PAGE`

短名称：`=$=`
作用域：本地
文件句柄调用：`format_lines_per_page FILEHANDLE EXPR`

每个格式句柄都有关联的每页行数，你可以通过此变量访问并更改它。
示例：

```
select (EG_FORMAT);
$one = 'Left';
$two = 'Center';
$three = 'Right';
$fitme = "";
write;
$one = $$;n
$two = $$;n
$three = $$;n
write;
select(STDOUT);
```

## `$FORMAT_LINE_BREAK_CHARACTERS`

短名称：`$:`
作用域：本地化
文件句柄调用：`format_line_break_characters FILEHANDLE EXPR`

当你使用格式代码向格式化区域输出值时

```
^|||||||||||
```

（或其他其它多行格式），换行符决定了字符串如何拆分成行以适应格式化空间。默认情况下，合法的换行符是空格、连字符和换行。

示例：

```
select(EG_FORMAT);
$: = ' \n-';
$one = 1;
$two = 2;
$three = 3;
$fitme = "One-One-One-One-One-One";n;
write;
write;
select(STDOUT);
```

## `$FORMAT_NAME`

短名称：`$~`
作用域：本地
文件句柄调用：`format_name FILEHANDLE EXPR`

每个格式都有一个名称，该名称也可以文件句柄的名称。你可以通过此变量直接访问该名称。
示例：

```
select(EG_FORMAT);
$one = ~;
$two = ~;
$three = ~;
write;
select(STDOUT);
```

## `$FORMAT_PAGE_NUMBER`

短名称：`$%`
作用域：始终全局
文件句柄调用：`format_page_number FILEHANDLE EXPR`

因为每个格式可以产生多页输出，此计数器仅对它们进行计数。
示例：

```
select (EG_FORMAT);
$one = ~;
$two = ~;
$three = ~;
write;
select (STDOUT);
```

## `$FORMAT_TOP_NAME`

短名称：`$^`

作用域：始终全局

文件句柄调用：`format_top_name FILEHANDLE EXPR`

每个格式都可以有一个关联的格式，该格式在每次生成新页面时都会复制。（没有等效的页脚脚）。默认情况下，这些具有与基础格式相同的名称并带有 _TOP 后缀，尽管可以设置任何名称。

示例：

```
format EG_TOP = =
[Sample Page Header]
To the left In the center To the right
--------------------------------------
.
open(EG_FORMAT,">-");
select(EG_FORMAT);
$- = 0;
$^ = EG_TOP;
$one = '111';
$two = '222';
$three = '333';
$fitme = ""
write;
write;
write;
select (STDOUT);
```

## `$INPLACE_EDIT`

短名称：`$I`
作用域：本地化

Perl 被用于编辑文件，有时该文件本身也是输出文件（结果替换原始文件）。在这种情况下，你可以（通过命令行选项）指定在编辑过程中创建的临时文件所使用的后缀。你可以通过此变量在脚本内部设置或简单地访问此值。
示例：

```
$^I=bak;
print "Tmp file extension when editing in place... $^I\n";
```

## `$INPUT_LINE_NUMBER`

短名称：`$.`
中间名称：`$NR`
作用域：本地化（只读）
文件句柄调用：`input_line_number HANDLE EXPR`

此变量计算来自输入文件的行数，并在文件关闭时重置。该变量跨所有输入文件中累加计数（因为这些文件没有被显式关闭）。
示例：

```
print "The last file read had $. lines\n";
```
