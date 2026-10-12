
Text::Wrap 提供了简单的折行功能来格式化字符串中的段落。

# 标准 Perl 785

# 概要

`use Text::Wrap`

```
print wrap($initial_tab, $subsequent_tab, @text);
print fill($initial_tab, $subsequent_tab, @text);
```

```
use Text::Wrap qw(wrap $columns $huge);
```

```
$columns = 132;
$huge = 'die';
$huge = 'wrap';
```

# 描述

`Text::Wrap::wrap()` 是一个非常简单的段落格式化器。它通过在单词边界换行来一次格式化一个段落。第一行（`$initial_tab`）和所有后续行（`$subsequent_tab`）的缩进独立控制。

在 `$Text::Wrap::columns` 处折行。列应设置为输出设备的完整宽度。当遇到超过 `$columns` 的单词时，它们会被拆分。之前的 `wrap()` 版本（用于 `die()`）会崩溃。要恢复旧的（崩溃的）行为，将 `$Text::Wrap::huge` 设置为 `die`。

`Text::Wrap::fill()` 是一个简单的多段格式化器。它单独格式化每个段落并在完成后将它们合并。它破坏原始文本中的任何空白。它通过寻找空白将文本拆分为段落。在其他方面，它的作用与 `wrap` 类似。

# 示例

```
print wrap("\t","This is a bit of text that forms a normal paragraph");
```

## ie::Array

该模块为绑定类（array-tying classes）提供了方法。

# 概要

```
package NewArray;
use Text::Array;
@ISA = ('Tie::Array');
```

# 附录 C

```
# 强制方法
sub TIEARRAY { ... }
sub FETCH { ... }
sub FETCHSIZE { ... }
```

```
sub STORE { ... }
# 如果元素可写则是强制
sub STORESIZE { ... }
# 如果元素可以添加/删除则是强制
```

```
# 可选方法 - 为了效率
sub CLEAR { ... }
sub PUSH { ... }
sub POP { ... }
sub SHIFT { ... }
sub UNSH { ... }
sub SPLICE { ... }
sub EXTEND { ... }
sub DESTROY { ... }
```

```
package NewStdArray;

use Text::Array;

@ISA = ('Tie::Array');
```

# 默认提供的所有方法

```
package main;

$object = tie @somearray,Tie::NewArray;
$object = tie @somearray,Tie::StdArray;
$object = tie @somearray,Tie::NewStdArray;
```

# 描述

`Tie::Array` 模块为绑定类提供了方法。请查看 `pertie` 手页获取绑定数组到包所需的函数列表。基础 `Tie::Array` 包提供了 stub `DELETE` 和 `EXTEND` 方法，并根据基本的 `FETCH`, `STORE`, `FETCHSIZE` 和 `STORESIZE` 实现了 `PUSH`, `POP`, `SHIFT`, `UNSH`, `SPLICE` 和 `CLEAR`。

`Tie::StdArray` 包为实现为内部 Perl 数组引用的绑定数组提供了高效的方法。它继承自 `Tie::Array`，应该使绑定数组的行为完全像标准数组，允许选择性地重载方法。

# 标准 Perl 模块 787

想要编写自定义绑定数组（tied arrays）的开发者，在此简要定义了所需的方法。更详细的描述和示例代码请参见 `tie` 的 man 页章节。

`TIEARRAY tie, LIST` 该类方法由 `tie @array,classname` 命令调用。它将一个数组实例与指定的类关联。`LIST` 表示完成该关联所需的额外参数（类似于 `AnyDBM::File` man 页及相关模块）。该方法应返回一个类对象，该类提供了下文中列列出的方法。

`STORE this, index, value` 该方法将数据值存储到与对象 `this` 关联的绑定数组 `index` 中。如果这导致数组变大，则应为新位置返回该类的 `undef` 映射。

`FETCH this, index` 该方法检索与对象 `this` 关联的绑定数组中 `index` 的数据。

`FETCHSIZE this` 该方法返回与对象 `this` 关联的绑定数组的项总数。（等同于 `scalar(@array)`）。

`RESIZE this, count` 该方法将与对象 `this` 关联的绑定数组的项目总数设置为 `count`。如果这导致数组变大，则应为新位置返回该类的 `undef` 映射。如果数组变小，则应删除 `count` 之外的条。

`EXTEND this, count` 这是一个信息性调用，表示数组可能会增长到 `count` 项。它可以用于优化分配。此方法不需要任何操作。

`CLEAR this` 该命令清除（移除、删除）与对象 `this` 关联的绑定数组中的所有值。

`DESTROY this` 这是一个标准的对象析构方法。

`PUSH this, LIST` 该命令将 `LIST` 中的元素附加到数组末尾。

`POP this` 该命令移除数组的最后一个元素并返回它。

# 附 C

`SHIFT this` 该命令移除数组的第一个元素（其他元素向下移动）并返回它。

`UNSHIFT this, LIST` 该命令将 `LIST` 元素插入到数组开头，移动现有元素以腾出空间。

`SPLICE this, offset, length, LIST` 该命令对数组执行等同于 `splice` 的操作。`offset` 是可选的，默认值为 0；负值从数组末尾倒数。`length` 是可选的，默认为数组的剩余部分。`LIST` 可以为空。它返回在 `offset` 处原始长度的元素列表。

# 注意事项

目前不支持 `tied @ISA`。标记修改 `@ISA` 所需的魔法项与实现 `tie` 所需的项之间存在潜在冲突。

对于 `[$` 未设置为默认值 0 时绑定数组的行为，尚未有很好的考虑。

# Tie::Handle

该模块为句柄绑定（handle-tying）类提供了一些骨架方法。

# 概要

```
package NewHandle;
require Tie::Handle;

@ISA = (Tie::Handle);

sub READ { ... } # 提供所需的方法
sub TIEHANDLE { ... } # 覆盖继承的方法

package main;

tie *FH, 'NewHandle';
```

# 描述

`Tie::Handle` 模块为句柄绑定类提供了骨架方法。`perie` man 页列出了绑定到包所需的函数列表。基础的 `Tie::Handle` 包提供了一个新方法，以及 `TIESCALAR`、`FETCH` 和 `STORE` 方法。提供新方法是为了为忘记提供 way `TIESCALAR` 方法的类提供兜底。

对于想要编写自定义绑定类的开发者，方法总结在下文中。`perlt` man 页章节记录了这些方法并带有示例代码：

`TIEHANDLE classname, LIST` 该方法由 `tie *glob, classname` 命令调用。它将一个新的全局作用符实例与指定的类关联。`LIST` 表示完成该关联所需的额外参数（类似于 `AnyDBM_File` man 页及相关模块）。

`WRITE this, scalar, length, offset` 该方法从 `offset` 开始向 `scalar` 写入 `length` 字节的数据。

`PRINT this, LIST` 该方法打印 `LIST` 中的值。

`PRINTF this, format, LIST` 该方法使用 `format` 打印 `LIST` 中的值。

`READ this, scalar, length, offset` 该方法从 `offset` 开始向 `scalar` 读取 `length` 字节的数据。

`READLINE this` 该方法读取单行。

`GETC this` 该方法获取单个字符。

`DESTROY this` 该方法释放与由 `this` 引用的绑定句柄关联的存储区域。此方法很少需要，因为 Perl 对内存的管理处理得非常好。但该选项确实存在，以防类在实例销毁时需要执行特定操作。

# Tie::Hash 和 Tie::StdHash

这些模块为哈希绑定类提供了一些骨架方法。

# 概要

```
package NewHash;
require Tie::Hash;
```

# 附 C

```
@ISA = (Tie::Hash);
```
