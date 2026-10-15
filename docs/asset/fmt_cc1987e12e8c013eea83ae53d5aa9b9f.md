
# 资源管理器匹配规则

决定哪个资源数据库条目匹配给定查询的算法是资源管理的核心。所有查询必须完整指定所需资源的名称和类（除非不允许字符 `*` 和 `?`）。该库在全名或类中支持多达 100 个组件。资源以仅部分指定的名称和类存储在数据库中。

全名和类名从左到右（从层次结构的最高层到最低层）扫描，一次处理一个组件。在每一层，确定每个匹配条目的对应组件/或绑定，并根据优先级规则比较这些匹配组件和绑定。每条规则在移动到下一层之前应用，直到某条规则选择了一个条目优于所有其他条目。规则按优先级排序如下：

- 包含匹配组件（无论名称）的条目
- 具有匹配类的条目优先级高于同时具有匹配类的条目和使用字符 `?` 匹配的条目。
- 具有匹配类的条目优先级高于使用字符 `?` 匹配的条目。
- 由紧密绑定（tight binding）引导的条目优先级高于松散绑定（loose binding）引导的条目。

为了说明这些规则，考虑以下资源数据库条目：

```
xmhPaned*activeForeground:      red (条目 A)
*incorporate.Foreground:             blue (条目 B)
xmh.toc*Command*activeForeground:      green (条目 C)
xmh.toc?.Foreground:               white (条目 D)
xmh.toc*Command.activeForeground:      black (条目 E)
```

考虑对资源的查询：

```
xmh.toc.messagefunctions.incorporate.activeForeground (name)
Xmh.Paned.Box.Command.Foreground (class)
```

在第一层（`xmh`, 规则），规则 1 消除了条目 B。在第二层（`toc`, `Paned`），规则 2 消除了条目 A。在第三层（`messagefunctions`, `Box`），没有条目被消除。在第四层（`incorporate`, `Command`），规则 2 消除了条目 D。在第五层（`activeForeground`, `Foreground`），规则 3 消除了条目 C。

# Quarks

资源管理器的大部分工作涉及将名称、类和表示类型定义为字符串常量。然而，在资源管理器中始终引用字符串可能会很慢，因为它在许多工具包中被频繁使用。为了解决这个问题，在许多资源管理器函数中，字符串的简写代替了字符串。可以进行简单的比较，而不是字符串比较。字符串的简写称为 quark，其类型为 `XrmQuark`。在某些情况下，你可能希望分配一个没有字符串等价物的 quark。

quark 之于字符串就像原子之于字符串，但它的使用局限于你的应用程序。要分配一个新的 quark，使用 `XrmQuark`。

```
XrmQuark Xrmark();
```

`XrmQuark` 函数分配一个保证代表资源管理器已知字符串的 quark。名称和表示类型被 typedef 为 `XrmQuark`。

```
typedef XrmQuark XrmName;
typedef XrmQuark XrmClass;
typedef XrmQuark XrmRepresentation;
```

# 资源管理器函数

```
#define NULLQUARK ((XrmQuark) 0)
```

列表表示为空终止的 quark 数组。数组的大小必须容纳组件。

```
typedef XrmQuarkList XrmNameList;
typedef XrmQuarkList XrmClass;
```

将字符串转换为 quark 使用 `XrmStringToark` 或 `XrmPermStringToark`。

```
#define XrmStringName(string) XrmStringToark(string)
#define XrmStringToClass(string) XrmStringToark(string)
#define XrmStringToRepresentation(string) XrmStringToark(string)
```

```
XrmQuark XrmStringToark(string);
```

`string` 指定所需的等效字符串。这些函数可将 quark 表示转换为字符串。指向的字符串可能会被修改。返回的字符串与传递给字符串-quark 例程的原始字符串字节相等。如果该 quark 没有字符串，`XrmQuarkToString` 返回 `NULL`。对于给定的 quark，如果 `XrmStringToToString` 返回非 `NULL` 值，未来的调用将返回相同的值（相同的地址）。

将 quark 转换为字符串，使用 `XrmStringToToString`。

```
#define XrmNameToString(name) XrmQuarkToString(name)
#define XrmClassToString(class) XrmQuarkToString(class)
#define XrmRepresentationToString(type) XrmQuarkToString(type)
```

```
char *XrmStringToToString(quark);
```

将具有一个或多个组件的字符串转换为 quark 列表，使用 `XrmStringToQuarkList`。

```
#define XrmStringToNameList(str, name) XrmStringToQuarkList((str), (name))
#define XrmStringToClassList(str, class) XrmStringToQuarkList((str), (class))
```

```
void XrmStringToQuarkList(string, quarks_return);
```

`string`  
指定要分配 quark 列表的字符串。

`quarks_return`  
返回 quark 列表。调用者在调用 `XrmStringToQuarkList` 之前必须为 quarks 分配足够的空间。

`XrmStringToQuarkList` 函数将以空字符终止的字符串（通常是全限定名）转换为 quark 列表。该字符串必须是有效的资源名称（`ResourceName`）格式（见第 15.1 节）。如果字符串未处于主机可移植字符编码（Host Portable Character Encoding）中，则转换结果取决于具体实现。

绑定列表（binding list）类型为 `XrmBindingList`，指示名称或类列表的组件是紧密绑定还是松散绑定（即是否指定了中间组件的通配符）。

```
typedef enum {XrmBindingTightly
```

`XrmBindingTightly` 表示组件之间用句号分隔，`XrmBindingLoosely` 表示组件之间用星号分隔。

要将一个或多个组件转换为绑定列表和 quark 列表，请使用 `XrmStringToBindingQuarkList`。

```
XrmStringToBindingQuarklist(string, bindings_return, quarks_return);
```

`string`  
指定要分配 quark 列表的字符串。

`bindings_return`  
返回绑定列表。调用者在调用 `XrmStringToToBindingQuarkList` 之前必须为绑定列表分配足够的空间。

`quarks_return`  
返回 quark 列表。调用者在调用 `XrmStringToToBindingQuarkList` 之前必须为 quarks 列表分配足够的空间。

列表中的组件名称用句号或星号字符分隔。该字符串必须是有效资源名称（`ResourceName`）格式（见第 15.1 节）。如果字符串不以句号或星号开头，则假设该绑定是如此。例如，字符串 `*a.b*c` 变为：

```
quarks:          a       b       c
bindings:        loose tight loose
```

# 创建和存储数据库

资源数据库是一个不透明类型 `XrmDatabase`。每个数据库值都存储在 `XrmValue` 结构中。该结构由大小、地址和表示类型组成。大小以字节为单位。表示类型是您存储由某些应用程序定义类型标记的数据的方法（例如，字符串 `"font"` 或 `"color"`）。它与 C 数据类型或其类无关。`XrmValue` 结构定义如下：

```
typedef struct {
    unsigned int size;
    XPointer addr;
} XrmValue, *XrmValuePtr;
```

要初始化资源管理器，请使用 `XrmInitialize`。

```
void XrmInitialize(XrmInitialize());
```
