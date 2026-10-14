
语法: `void Tcl_SetObjResult(interp, objPtr)`

语法: `void Tcl_SetResult(interp, string, freeProc)`

`Tcl_SetObjResult`

将 `objPtr` 指向的对象作为命令求值的结果返回给 Tcl 解释器。如果已经定义了结果，它将被 `objPtr` 指向的对象替换。

`Tcl_Interp *interp`

指向 Tcl 解释器的指针。

`Tcl_Obj *objPtr`

指向包含整数对象的指针。

`string`

以 NULL 终止的字符串。

`void (*freeProc)(char *)`

释放内存的函数指针。

- `TCL_STATIC`: 字符串位于静态内存中。
- `TCL_DYNAMIC`: 字符串是动态分配的。
- `TCL_VOLATILE`: 字符串在易性内存中。

# 第 12 章 编写 Tcl 扩展

## 12.1 向脚本返回状态

当函数向 Tcl 解释器返回状态时，必须是 `TCL_OK` 或 `TCL_ERROR`。如果函数返回 `TCL_OK`，脚本将继续。

如果函数返回 `TCL_ERROR`，将生成错误，除非脚本使用 `catch` 命令捕获错误，否则执行将停止。

默认情况下，错误信息是产生错误的命令。你可能希望向此添加更多信息，例如文件写入失败、套接字无法连接。

你可以通过调用函数向该消息添加更多信息。

语法: `Tcl_AddErrorInfo(interp, message)`

```
语法: void Tcl_AddErrorInfo(interp, message)
```

`Tcl_AddErrorInfo`

向信息对象附加文本。该信息对象可以在 Tcl 脚本中作为全局变量 `errorInfo` 被访问。

```
语法: void Tcl_SetErrorCode(interp, ...)
```

`Tcl_SetErrorCode`

设置 `errorCode` 对象的值。如果对象包含列表，列表值将拼接在一起形成返回。默认情况下 `errorCode` 为 `NONE`。

## 12.1 概述

`Tcl_SetErrorCode`

将 `errorCode` 变量设置为拼接后的字符串。

`Tcl_Interp *interp`

指向 Tcl 解释器的指针。

`char *message`

附加到 `errorInfo` 全局变量的消息。该字符串末尾会附加一个换行符。

`Tcl_Obj *objPtr`

指向包含错误代码对象的指针。

`char *element`

错误代码部分的 ASCII 字符串表示。

如果发生系统错误，你的函数可以使用 `Tcl_PosixError` 从 C 语言全局变量 `errno` 设置 `errorCode` 变量。此命令的行为在不同平台上略有不同。在使用之前，你应该检查你所在平台和 Tcl 版本的在线文档。

### 12.1.9 处理持久数据

在某些情况下，扩展需要维护一份独立于求值脚本的持久数据副本，允许脚本描述它需要交互的数据。例如，文件指针必须一直维护到文件关闭，并且 Tcl 脚本可能会同时打开多个文件，访问一个文件后再访问另一个。

如果你的扩展的数据需求非常简单，分配一个数组并在必要时将其分配给脚本可能足够了。例如，如果你编写了一个与特定硬件接口的扩展，并且系统中永远只有一个此类设备，你可以将控制结构声明在你的 C 代码中为静态全局变量。

# 第 12 章 编写 Tcl 扩展

对于更复杂的情况，Tcl 库包含了一些函数，允许你使用 Tcl 哈希表来存储键值对。你的扩展可以为数据结构分配内存，定义一个键来标识该结构，然后将指向结构的指针放入哈希表中，以便通过该键进行访问。键可以是字母数字字符串，并返回给 Tcl 脚本。当 Tcl 脚本需要访问数据时，它会将键传回给扩展代码，然后由代码从哈希表中检索数据。

Tcl 哈希表由一个 `Tcl_HashTable` 结构（由你的扩展代码分配）和根据需要创建的用于存储键/值对的 `Tcl_HashEntry` 结构组成。

在使用访问哈希表条目的函数之前，你必须先初始化哈希表。一旦初始化了表，你的代码就可以从哈希表中添加、访问或删除项了。

```
语法: void Tcl_InitHashTable(tablePtr, keyType)
Tcl_InitHashTable
```

初始化哈希表。

> **`Tcl_HashTable *tablePtr`**
>
> 指向 `Tcl_HashTable` 结构的指针。在调用 `Tcl_InitHashTable` 之前必须为该结构分配空间。
>
> **`int keyType`**
>
> Tcl 哈希表可以使用三种类型的键之一来访问存储在哈希表中的数据。`keyType` 可接受的值：

```
TCL_STRING_KEYS
```

哈希表将使用以 NULL 结尾的字符串作为键。这是最常用的哈希键类型。`Tcl_Obj` 对象的字符串表示可以用作键，这使得从脚本将值传递给 Tcl 哈希表函数变得非常简单。

## 12.1 概述

### TCL_ONE_WORD_KEYS

哈希表将使用单个单词值作为键。请注意，如果该单词是一个指针，则使用指针的值作为键，而不是指针所引的数据。

### positiveInteger

如果使用正整数作为 `keyType`，则键将是一个包含所述数量数量整数的数组。这允许将复杂的二进制数据结构用作键。请注意，用作键的结构大小必须相同。

哈希表一旦初始化完成，就可以使用 `Tcl_CreateHashEntry`、`Tcl_FindHashEntry` 和 `Tcl_DeleteHashEntry` 命令来查询或从哈希表中移除条目。

```
语法: Tcl_CreateHashEntry(tablePtr, key, newPtr)
```

```
语法: Tcl_FindHashEntry(tablePtr, key)
```

```
语法: void Tcl_DeleteHashEntry(entryPtr)
```

**`Tcl_CreateHashEntry`**

为请求的键分配并初始化一个新的 `Tcl_HashEntry` 对象。如果之前存在该键的条目，则 `newPtr` 被设置为 `NULL`。

**`Tcl_FindHashEntry`**

此函数返回指向与键值关联的 `Tcl_HashEntry` 对象的指针。如果该键不在此哈希表中，则此函数返回 `NULL`。

**`Tcl_DeleteHashEntry`**

此函数从表中移除一个哈希表条目。在调用此函数后，如果使用该键，`Tcl_FindHashEntry` 将返回 `NULL`。这不会破坏与哈希条目关联的数据。你与哈希表交互的函数必须手动处理这一点。

# 第 12 章 编写 Tcl 扩展

**`Tcl_HashTable *tablePtr`**

指向 Tcl 哈希表的指针。在被这些命令使用之前，必须通过 `Tcl_InitHashTable` 初始化此表。

**`char *key`**

定义此条目的键。此值必须是 `Tcl_InitHashTable` 调用中描述的类型之一。

**`int *newPtr`**

如果创建了新条目，则此值为 1；如果已存在具有此值的键，则值为 0。

**`Tcl_HashEntry *entryPtr`**

指向哈希表的指针。

一个 `Tcl_HashEntry` 包含标识它的键值和一个 `Client-Data` 对象。`ClientData` 类型是一个字（word）的对象。在大多数现代机器上，它的大小与指针相同，这允许你分配任意的数据空间并将指向该空间的指针放置在 `Tcl_HashEntry` 中。

你可以使用 `Tcl_SetHashValue` 和 `Tcl_GetHashValue` 命令操作 `Tcl_HashEntry` 对象。

**语法：** `ClientData TclGetHashValue(entryPtr)`

**语法：** `void TclSetHashValue(entryPtr, value)`

**`Tcl_GetHashValue`**

从 `Tcl_HashEntry` 中检索数据。

**`Tcl_SetHashValue`**

设置 `Tcl_HashEntry` 中数据的值。

**`Tcl_HashEntry *entryPtr`**

指向哈希表的指针。

**`ClientData value`**

要放置在 `Tcl_HashEntry` 的 `clientData` 字段中的值。

下面是一个代码片段，它将创建一个哈希表、添加条目并检索数据。

## 12.1 概述

### 示例 12.1.9-1

### 示例代码片段
