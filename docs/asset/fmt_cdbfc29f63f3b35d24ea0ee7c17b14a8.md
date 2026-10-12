
然后，`NOTECHOING` 模块为其同名为 `Echo` 的接口提供了一个独立的命名空间：

```
module NOTECHOING {
    interface Echo {
        void noecho (in ECHOING::input str);
    }
};
```

注意，当我们使用局限于 `ECHOING` 模块的输入类型时，我们需要通过前缀 `ECHOING::` 来指明它是从该命名空间导入的。这与 `C++` 管理对外部命名空间的引用的方式类似。

在示例示例中，有两个名为 `Echo` 的接口，还有一个名为 `echo` 的操作符。通过在不同的模块中仔细地应用，这些接口被确立为不同的。

## 陷阱 (Pitfalls)

注意不要粗率使用大小写。`CORBA` 假设它被用于对大小写不敏感的语言，因此以不区分大小写的方式处理标识符。如果你创建了仅在大小写上不同的声明，`IDL` 编译器应该指示这是一个错误。

在编写代码时，请记住你将使用什么语言来为 `CORBA` 服务创建客户端。如果该语言以特定方式解释下划线字符，那么最好不要使用它们。在没有原生对象系统的 `C` 语言中，语言映射构造通过使用下划线连接片段来为对象构造名称。例如，在 `C` 中，`noecho` 操作符可能会被命名为 `NOTECHOING_Echo_noecho`。

## 接口 (Interfaces)

接口用于将相关数据结构和操作组合在一起。

对于 `DVD` 应用，在 `DVD` 模块内一组合理的接口看起来是：

```
module DVD {
    interface MEMBERSHIP ( // 操作 DVD Store 成员的方法 );
    interface TITLING ( // 操作 DVD Store 标题的方法 );
    interface DISKS ( // 操作 DVD 磁盘的方法 );
    interface RENTAL ( // 处理磁盘租用和归还的方法 );

    interface RESERVATIONS ( // 管理预订标题的方法 );
    interface UTILITIES ( // 其他不适合放在其他地方的方法 );
    interface FACTORY ( // 提供对其他接口访问权限的基接口 );
);
};
```

每个接口都提供一个对象引用。我们将通过设置一个基础 `FACTORY` 接口（该接口包含返回其他接口引用的操作），来控制 `DVD` 应用中这些引用的建立以及它们如何传递给客户端。`FACTORY` 可以被用作安全工具，只有在确认请求者已通过身份验证后，才响应客户端请求返回引用。将一个接口嵌套在另一个接口内部是不有效的，模块也不能嵌套在另一个模块内部。

## 基本数据类型

`CORBA` 定义了一系列基本数据类型，这些类型是按照通用数据表示 (`CDR`) 格式在 `ORB` 之间传输的数据的基本组件。下表显示了 `CORBA` 数据类型：

| IDL 类型 | 描述 |

|---|---|

| short | 16 位整数 |

| long | 32 位整数 |

| long long | 64 位整数 |

| unsigned short | 无符号 16 位整数 |

| unsigned long | 32 位无符号整数 |

| unsigned long long | 无符号 64 位整数 |

| float | 32 位 IEEE 浮点数 |

| double | 64 位 IEEE 浮点数 |

| char | 8 位字符 |

| wchar | 16 位字符 |

| boolean | 取 TRUE 或 FALSE 的布尔类型 |

| octet | 不受通信影响的透明字符类型 |

| any | 可以表示任何基本类型或构造类型 |

大多数类型与 `C` 和 `C++` 中提供的类型非常相似。值得详细说明的是较为独特的 `octet` 类型，它是一个 8 位字符类型，用于传输本应保持原封的二进制数据。如果你在基于 `ASCII` 的 `UNIX` 系统和使用 `EBCDIC` 的 `IBM AS/400` 系统之间使用 `char` 类型传输文本数据，自动从源原生格式转换为目标原生格式将是一个很好的主意。另一方面，如果你想让数据完全保持不变，则使用 `octet`。

## 模板类型 (Template Types)

这些是大小可变的类型。

### 序列 (Sequences)

序列是变长向量。它们可以包含任何元素类型。它们的大小可以是无界的，允许你传递无限数量的字符串值：

```
sequence<string> message;
```

或者，限制为某些元素数量：

```
sequence<char, 80> line;
```

### 字符串和 wstrings

字符串就像 `C` 字符串；它是变长度的终止字符向量（`char` 类型）。`wstrings` 通过使用 `wchar` 宽字符扩展了这一点，设计用于具有多字节字符的语言。

它们等同于序列 `sequence<char>`，但被建立为一个独立类型，因为某些语言环境提供了专门处理字符串的函数。

### fixed

`fixed` 类型是 `CORBA 2.3` 中的新类型，尚未普遍实现。它提供了一种用于存储最多 31 位固定小数点的数值的数据类型。这类似于 `COBOL` 中使用的 `PIC` 数据类型，并可以用于支持 `SQL` 中提供的 `MONEY` 数据类型。

这种类型在金融应用程序中特别有用，因为应用程序需要提供一致的舍入策略以及对精度的处理。

```
fixed<10,2> total:
```

`COBOL` 和 `Ada` 都提供了固定小数类型；在其他语言中，需要 `IDL` 语言映射在本地“语言”中提供表示。

在 `C` 语言中，这种表示方式并不自然；`ORB` 编译器生成：

```
CORBA_unsigned_short_digits;
CORBA_short_scale;
CORBA_char_value(6);
) CORBA_fixed_10,2;
```

这表示一种每字节两个数字的压缩格式，这需要使用函数来处理值，而不是使用普通的算术运算。

# 构造类型

构造类型是由更基础的类型构造的。它们可以包含本身也是构造类型的元素。

## typedef

`typedef` 的工作与 `C` 语言中的 `typedef` 关键字类似。

```
typedef long dvdidt;
typedef fixed<10,2> money;
```

这声明了一个名为 `dvdidt` 的构造类型，用于存储 32 位整数值，以及一个 `money` 数据类型，包含十位数，其中两位是小数。

## 结构

结构类似于 `C` 结构体，尽管语法略有不同。

```
struct dvdiddis (
  dvdidt diskid;
  TITLING::titlet titleid;
);
```

在这个示例中，结构的名称为 `dvdiddis`，结构组件 `diskid` 使用之前声明的 `dvdidt` 类型声明，因此是一个 32 位符号整数。

结构组件 `titleid` 使用类型 `titlet` 声明，该类型定义在命名空间 `TITLING` 中。这说明了如何使用命名空间来引用在单独接口中声明的“外部”类型。

## 枚举

这些类似于 `C/C++` 的枚举类型：

```
enum movierat { G, PG13, NC17, R, NR, XXX };
```

注意，没有办法指定起始值，就像你在 `C` 或 `C++` 中可能做的那样；这意味着没有一种可移植的方法可以在客户端和服务器之间交换枚举序数值；你必须使用枚举器本身。这种限制是刻意为，因为某些语言支持不涉及任何数字的枚举。例如，在 `Common Lisp` 映射中，枚举器直接表示为符号，因此：

```lisp
(setf ratings-list (:G :PG13 :NC17 :R :NR :XXX))
```

在示例应用程序中，我们不会使用这个枚举，因为会将应用程序锁定在一组固定的电影分级中。相反，值存储在表中，以便在以后进行修改，而无需更改接口。

# 第 20 章

## 数组

数组提供了具有固定数量元素的向量。你可以声明一维数组：

```
typedef char line[80];
```

也可以声明多维数组：

```
typedef double bezier[3][3];
```

## 联合体

`IDL` 联合体与 `C/C++` 对应物的区别在于，它们要求是区分的（discriminated），允许单个成员有多个分支标签，并支持默认分支：

```
union pCode switch(Country) { /* 国际邮编 */
case USA: /* 如 75063-2921 */
long main;
short sub;
case Canada: /* 如 KOA 2NO */
char p1;
short p2;
char p3;
short p4;
char p5;
short p6;
default:
string pcode;
```

这个示例提供了国际邮编的表示，允许格式根据 `Country` 字段的值随国家变化。它考虑了加拿大和美国的特殊格式，并将其他国家的字段留为通用字符串。

## 操作
