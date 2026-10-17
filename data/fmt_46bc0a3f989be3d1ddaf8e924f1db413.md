
在接下来的章节中，将介绍如何利用 PHP 内部机机制来构建强大的扩展。

## 接收参数

对于语言扩展来说，最重要的问题之一就是接收和处理通过参数传递的数据。大多数扩展都是为了处理特定的输入而构建的，或需要参数执行其特定操作，而函数参数是 PHP 层级与 C 层级之间交换数据的唯一真实方式。当然，也可以通过使用定义的全局变量来交换数据，这在稍后也会讨论，但应尽一切避免这样做，因为这是一种极糟糕的实践。详情，请参阅第 1 章“开发概念”。

PHP 并没有使用任何函数声明；这就是为什么语法总是完全动态的，并且从不进行错误检查。语法正确性的检查被留给了用户代码；你可能某一次只用一个参数调用函数，下一次就用四个参数——这两种调用在语法上都是绝对正确的。

### 确定参数数量

由于 PHP 没有支持调用语法检查的正式函数定义，而且 PHP 具有变长参数特性，你有时需要确定函数被调用时传入了多少参数。在这种情况下，你可以使用 `ZEND_ARGS` 宏。在之前的 PHP 版本中，该宏根据函数的哈希表项获取函数调用时的参数数量，该项被传递给 `INTERNAL_FUNCTION_PARAMETERS` 列表。由于它现在包含了传递给函数的参数数量，`ZEND_NUM_ARGS` 已经精简为一个占位宏，参见其在 `zend_api.h` 中的定义。但使用它仍然是一个良好的习惯，以保持与调用接口未来变化的兼容。注意：该宏的旧 PHP 等效对应是 `ARG_COUNT`。

以下代码检查参数数量是否正确：

```c
if (ZEND_NUM_ARGS() != 2)
    WRONG_PARAMETER_COUNT;
```

如果调用函数时没有两个参数，它将带错误消息退出。该代码段使用了 `WRONG_PARAMETER_COUNT` 工具，该工具用于生成标准的错误消息，见图 9.4。

318 第 9 章扩展 PHP 4.0：破解 PHP 核心

图 9.4 `WRONG_PARAMETER_COUNT` 的用法。

此宏会执行默认错误消息并返回到调用者。它的定义也可以在 `zend_API.h` 中找到，看起来所示：

```c
ZEND_API void wrong_param_count(void);

#define WRONG_PARAM_COUNT { wrong_param_count(); return; }
```

如你所示，它调用了一个名为 `wrong_param_count()` 的内部函数，该函数负责打印警告。关于如何生成自定义错误消息的详情，请参见后文章节“打印信息”。

### 获取参数

在检查了参数数量后，你需要获取参数本身。这是通过 `zend_get_parameters_ex()` 实现的：

```c
zval **parameter;
```

```c
if(zend_get_parameters_ex(1, &parameter) !== SUCCESS)
    WRONG_PARAM_COUNT;
```

所有参数都存储在 `zval` 容器中，需要指向两次。上面的代码段用于获取一个参数并通过 `parameter` 指针将其供我们使用。

`zend_get_parameters_ex()` 至少接受两个参数。第一个参数是函数调用时的参数数量；这就是为什么检查正确的语法是重要的原因。第二个参数，以及所有后续参数，是指向 `zval` 指针的指针。这很困惑，`zval`；为了调整我们函数中的本地 `zval`，`zend_get_parameters_ex()` 需要一个指向它的指针。

`zend_get_parameters_ex()` 的返回值可以是 `SUCCESS` 或 `FAILURE`，表示参数处理的成功或失败。失败最可能与指定的参数数量不正确有关，在这种情况下你应该使用 `WRONG_PARAM_COUNT` 退出。

要获取多个参数，你可以使用此代码段：

```c
zval **param1, **param2, **param3, **param4;

if(zend_get_parameters_ex(4, &param1, &param2, &param3, &param4) != SUCCESS)
    return WRONG_PARAM_COUNT;
```

`zend_get_parameters_ex()` 仅在你尝试检索多个参数时才会进行检查。如果用五个参数调用函数，而你只通过 `zend_get_parameters_ex()` 获取了其中三个，你不会得到错误，而是会获得前三个参数。随后的 `zend_get_parameters_ex()` 调用将不会获取剩余的参数，而是会再次获取相同的参数。

### 处理变数量参数/可选参数

如果你的函数旨在接收变数量的参数，那么你描述的代码段有时并不是优解。你需要为每种可能的参数数量创建一行调用 `zend_get_parameters_ex()` 的代码，这通常是不令人满意的。

对于这种情况，你可以使用函数 `zend_get_parameters_array_ex()`，它接受要取回的参数数量以及一个用于存储它们的数组：

```c
zval **parameter_array[4];

/* 获取参数数量 */
argument_count = ZEND_NUM_ARGS();

/* 检查是否满足 (2 个参数) */
/* 以及 (4 个参数) */
if(argument_count < 2 || argument_count > 5)
    return WRONG_PARAM_COUNT;

/* 参数数量正确，，现在获取参数 */
if(zend_get_parameters_array_ex(argument_count, parameter_array) != SUCCESS)
    return WRONG_PARAM_COUNT;
```

首先，检查参数数量以确保其在范围内。之后，`zend_get_parameters_array_ex()` 填充 `parameter_array`。这种清晰的实现可以在... 中找到。

# 322 第 9 章 扩展 PHP 4.0：破解 PHP 核心

表 9.4 续

| 函数 | 描述 |
| --- | --- |
| `convert_to_double_ex(value)` | 强制转换为双精度浮点数 `double`，这是默认浮点类型。`NULL` 值、布尔值、字符串保持不变。包含数字的字符串将转换为对应的数值表示，否则结果为 `0.0`。数组为空时转换为 `0.0`，否则转为 `1.0`。 |
| `convert_to_string_ex(value)` | 强制转换为字符串。字符串保持不变。`NULL` 值转换为字符串。包含 `TRUE` 的布尔值转换为 `"1"`，否则结果为空字符串。长整型 `Longs` 和双精度 `doubles` 转换为对应的字符串表示。数组转换为字符串 `"Array"`，对象转换为字符串 `"Object"`。 |
| `convert_to_array_ex(value)` | 强制转换为数组。数组保持不变。通过将所有属性分配给数组表将对象转换为数组。所有属性名用作键，属性内容用作值。`NULL` 值转换为在键为 `.` 的元素中包含特定源值的数组。 |
| `convert_to_object_ex(value)` | 强制转换为对象。对象保持不变。通过将它们的键引入对象并将值作为对象中相应的属性内容，将 `NULL` 值转换为空对象。所有其他类型都会产生一个具有标 属性的对象，其内容为相应的源值。 |
| `convert_to_null_ex(value)` | 强制类型变为 `NULL` 值，即为空。 |

注意：你可以在附带的 CD-ROM 上的 `cross_conversion.php` 中找到该行为的演示。图 9.5 显示了输出。

# 接收参数 323

![](img/eddeabf7128be657d5f7345abdc760ac_340_0.png)

图 9.5 PHP 的交叉转换行为

在参数上使用这些函数将确保传递给你的所有数据的类型安全。如果提供的类型与所需的类型不匹配，PHP 将对结果值强制使用占位符，空字符串、数组或对象，数值为 `0`，布尔值为 `FALSE`，以确保其处于定义状态。

以下是之前讨论的示例模块的引用，它使用了以下函数：

```c
zval *__ARGS;

if((ZEND_NUM_ARGS() != 1) || (zend_get_parameters_ex(1, &parameter) != SUCCESS))
{
    WRONG_PARAM_COUNT;
}

convert_to_long_ex(*parameter);
RETURN_LONG(*parameter)->value.lval;
```

获取参数指针后，参数值被转换为长整型，整数，这同时也成了该函数的返回值。理解对值内容的访问需要对 `zval` 类型进行简短描述，其定义在列表 9.8 中。

# 列表 9.8 PHP/Zval 类型定义。

```c
typedef pval zval;
typedef struct _zval_struct zval;
typedef union _zval_value {
    long lval;
    /* long value */
    double dval;
    /* double value */
    struct {
        char *val;
        int len;
    } str;
    HashTable *ht;
    /* hash table value */
    struct {
        zend_class_entry *ce;
        HashTable *properties;
    } obj;
} zval_value;
```

实际上，`pval`，在 `php.h` 中定义只是 `zval`，在 `zend.h` 中定义的别名，而 `zval` 又引用了 `_zval_struct`。这是一个非常有趣的结构。`_zval_struct` 是“主”结构，包含了值结构、类型和引用信息。子结构 `zval_value` 是一个包含值内容的联合体。根据变量的类型，你将必须访问此联合体的不同成员。关于这两种结构的描述，请参阅表 9.5、9.6 和 9.7。

# 表 9.5 Zend zval 结构

| 条目 | 描述 |
| --- | --- |
| `value` | 包含该变量内容的联合体。描述请参见表 9.6。 |
| `type` | 包含该变量的类型。可用类型列表请参见表 9.7。 |

# 接收参数 325

| 条目 | 描述 |
| --- | --- |
| `is_ref` | `0` 意味着该变量不是引用；`1` 意味着该变量是另一个变量的引用。 |
| `refcount` | 该变量存在的引用数。对于对该变量中存储值的每一个新引用，此计数器加 `1`。每丢失一个引用，此计数器减 `1`。当引用计数达到 `0` 时，不再存在对该值的引用，这会导致该值的自动释放。 |

表 9.6 Zend zvalue_value 结构

| 条目 | 描述 |
| --- | --- |
| `lval` | 如果变量类型为 `IS_LONG`、`IS_BOOLEAN` 或 `IS_RESOURCE`，则使用此属性。 |
| `dval` | 如果变量类型为 `IS_DOUBLE`，则使用此属性。 |
| `str` | 此结构用于访问类型为 `IS_STRING` 的变量。成员 `len` 字符串长度；成员 `val` 指向字符串本身。`Zend` 使用 C 字符串；此时字符串长度包含一个尾随 `0x0`。 |
| `ht` | 如果变量是数组，此条目指向哈希表条目。 |
| `obj` | 如果变量类型为 `IS_OBJECT`，则使用此属性。 |

表 9.7 Zend 变量类型常量

| 常量 | 描述 |
| --- | --- |
| `IS_NULL` | 表示 `NULL`，空值。 |
| `IS_LONG` | 长整型，整数值。 |
| `IS_DOUBLE` | 双精度，浮点数值。 |
| `IS_STRING` | 字符串。 |
| `IS_ARRAY` | 表示数组。 |
| `IS_OBJECT` | 一个对象。 |
| `IS_BOOL` | 一个布尔值。 |
| `IS_RESOURCE` | 一个资源，关于资源的讨论，请参见下文相应章节。 |
| `IS_CONSTANT` | 常量，定义值。 |

# 326 第 9 章 扩展 PHP 4.0：破解 PHP

要访问长型 `zval->value.lval`，访问双精度使用 `zval->value.dval`，以此此类推。由于所有值都存储在联合体中，尝试用错误的联合体成员访问数据会导致无意义的输出。访问数组和对象要复杂一些，稍后会讨论。

### 处理通过引用传递的参数

如果你的函数接收了你打算修改的引用参数，你需要采取一些预防措施。

我们还没有说的是，在目前出现的情况下，你无法访问任何指定传递给你的函数参数的 `zval` 容器。当然，你可以更改在函数内部创建的任何 `zval` 容器，但你不能更改任何引用 Zend 内部数据的 `zvals`！

我们一直专门使用所谓的 *ex() API。你可能注意到，我们使用的 API 用 `zend_get_parameters_ex()` 替换了 `zend_get_parameters()`，用 `convert_to_long_ex()` 替换了 `convert_to_long()` 等。*ex() 函数构成了所谓的“权衡” API。它们比旧 API 速度更快，但权衡仅用于提供只读访问。

由于 Zend 在内部处理引用，不同的变量可能会引用同一个值。对 `zval` 的写入访问需要该容器是隔离的，意味着它没有被其他容器引用。如果一个 `zval` 被其他容器引用且你更改了内容，它们也将同样指向更改后的值。`zend_get_parameters_ex()` 不关心这种情况，它只是简单地返回指向所需容器的指针。在传统 API 中，`zend_get_parameters()` 内部会立即检查引用的值。如果它发现有引用，它会创建一个新的、隔离的 `zval` 容器，将引用数据拷贝到这个新空间，然后返回指向新隔离值的指针。这种操作被称为 `zval` 分离，或 `pval` 分离。*ex() API 不执行 `zval` 分离，它快得多，同时禁用了写入访问。

# 接收参数 327

然而，更改参数需要写入访问。Zend 以特殊方式处理这种情况：当参数通过引用传递给函数时，它执行自动 `zval` 分离。这意味着当你在 PHP 中这样调用函数时，Zend 会自动将 `$parameter` 作为隔离值传递，使其处于写入安全状态：

```c
my_function(&$parameter);
```

但普通参数并非如此！其他未通过引用传递的参数处于只读状态——这要求你处理的是引用——否则可能会产生意外的结果。要检查引用引用传递，可以使用 `PassedByReference()` 函数。该函数接收两个参数：第一个是函数的 `ht` 值，第二个是从左到右数的测试参数编号，如列表 9.9 和图 9.6 所示，完整源码见 CD-ROM。

9.9 测试引用参数传递

```c
zval **parameter;
```

```c
if((ZEND_NUM_ARGS() != 1) || (zend_get_parameters_ex(1, &parameter) != SUCCESS))
{
    WRONG_PARAM_COUNT;
}
```

```c
/* 检查引用传递的参数 */
if(!PassedByReference(ht, 1))
{
    zend_error(E_WARNING, "Parameter wasn't passed by reference");
    RETURN_NULL();
}
```

```c
/* 更改参数 */
(*parameter)->type = IS_LONG;
(*parameter)->value.lval = 10;
```

# 328 第 9 章：扩展 PHP 4.0：破解 PHP Core

![](img/eddeabf7128be657d5f7345abdc760ac_345_0.png)

图 9.6 测试引用传递。

### 确保其他参数的写入安全

你可能会遇到这种情况：需要访问一个通过 `zend_get_parameters_ex()` 获取但并非通过引用传递的参数。在这种情况下，你可以使用 `SEPARATE_ZVAL` 宏，它会对提供的容器进行 `zval` 分离。新生成的 `zval` 将从内部数据中解离，并且仅具有局部作用域，这意味着它的更改或销毁不会影响脚本上下文中的全局变化：

```c
zval *parameter;
```

```c
/* 获取参数 */
zend_get_parameters_ex(1, &parameter);
```

```c
/* 在此阶段，<parameter> 仍然连接到
* Zend 的内部数据缓冲区 */
```

```c
/* 使 <parameter> 写入安全 */
SEPARATE_ZVAL(parameter);
```

```c
/* 现在可以安全地修改 <parameter> */
/* 而不会引起全局变化
*/
```

`SEPARATE_ZVAL` 使用 `emalloc` 来分配新的 `zval` 容器，这意味着即使你没有释放这部分内存，它也会在脚本结束时自动销毁。然而，大量调用此操作而不释放生成的容器，将会占用你的 RAM。

注意：由于你可以轻松绕过“传统”API，使用 `zend_get_parameters()` 等缺乏写入访问的问题，该 API 似乎已经过时，本章将不再进一步讨论。

### 创建变量

当从扩展通过 PHP 脚本交换数据时，最重要的问题之一就是变量的创建。本节将介绍如何处理 PHP 支持的变量类型。

### 概述

为了创建可以通过执行脚本从“外部”可见的变量，你需要分配一个新的 `zval` 容器，用该容器填充有意义的值，并将其引入 Zend 的内部符号表。这个基本过程适用于所有变量：

- `new_variable;`

```c
/* 分配并初始化新容器 */
MAKE_STD_ZVAL(new_variable);
```

```c
```
