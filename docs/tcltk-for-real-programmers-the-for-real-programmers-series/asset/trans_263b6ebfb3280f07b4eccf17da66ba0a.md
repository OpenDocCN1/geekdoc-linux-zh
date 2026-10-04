
# 第 12 章 编写 Tcl 扩展

`Tcl_GetStringObj` 命令可以将 `bytes` 字节放在整数指针 `objPtr` 指向的字符串中。在这种情况下，`length` 指针是必要的，它表示要从字符串复制的字节数。

### 12.1 返回结果

实现 Tcl 命令的函数可以通过以下几种方式向脚本返回结果：

- 1. 将单个值作为结果返回。
- 2. 将值列表作为结果返回。
- 3. 修改作为参数的脚本变量的内容。
- 4. 修改已有的脚本变量的内容。

在 Tcl 8.0 之前的版本中，由于所有变量都作为字符串维护，函数可以创建一个字符串来返回结果。

在 Tcl 8.0 及更高版本中，可以使用以下命令之一创建一个新对象或修改现有对象：

```
Syntax: Tcl_Obj *Tcl_NewIntObj (intValue)
Syntax: Tcl_Obj *Tcl_NewDoubleObj (doubleValue)
Syntax: Tcl_Obj *Tcl_NewStringObj (bytes, length)
```

```
Tcl_NewIntObj
创建一个带有整数值的 Tcl 对象。
```

```
Tcl_NewDoubleObj
创建一个带有双点数的 Tcl 对象。
```

```
Tcl_NewStringObj
		从字节字符串创建一个 Tcl 对象。
```

```
intValue
		分配给新对象的整数。
```

## 12.1 概述

`doubleValue` 是分配给新对象的双点数。

`bytes` 是复制到新对象的字节数组。

`length` 是复制到新对象的字节数。如果这是一个负值，将复制到第一个 NULL 字节的所有字节。

你可以使用这些命令通过改变字符串表示来修改对象的内容：

```
Syntax: void Tcl_SetIntObj (objPtr, intValue)
```

Tcl_SetIntObj
设置对象的整数表示的值。如果该对象不是整数类型，将尽可能转换为整数。

`Tcl_Obj *objPtr`
指向包含整数对象的指针。

`int intValue`
分配给此对象的整数。

```
Syntax: void Tcl_SetDoubleObj (objPtr, doubleValue)
```

Tcl_SetDoubleObj
设置对象的整数表示的值。如果该对象不是双点数类型，将尽可能转换为双点数。

`Tcl_Obj *objPtr`
指向包含双点数的对象的指针。

`double doubleValue`
分配给此对象的双点数。

对象的字符串表示可以通过多种方式修改，无论是完全替换一个新的字节字符串、追加单个字符串、从另一个对象添加字符串，或追加字符串列表。

```
Syntax: void Tcl_SetStringObj (objPtr, bytes, length)
```

```
Syntax: void Tcl_AppendToObj (objPtr, bytes, length)
```

# 第 12 章 编写 Tcl 扩展

**语法:** void Tcl_AppendObjToObj (objPtr, appendObjPtr)
**语法:** void Tcl_AppendStringsToObj (objPtr, string, ..., NULL)

Tcl_SetStringObj
重定义对象的字符串值。

Tcl_AppendToObj
向对象的字符串表示添加一个字符串。

Tcl_AppendObjectToObj
将一个对象的字符串表示添加到当前对象的字符串中。

Tcl_AppendStringsToObj
向当前对象的字符串添加一个或多个字符串。

Tcl_Obj *objPtr
指向包含字符串的指针。

`bytes`
复制到新对象的字节数组。

`length`
复制到新对象的字节数。如果这是一个负值，将复制到第一个 NULL 字节的所有字节。

`appendObjPtr`
指向包含要追加字符串的对象的指针。

`string`
以 NULL 终止的字符字符串。你不能对 `Tcl_AppendStringsToObj` 命令使用二进制字符串。

如果你希望你的函数作为命令求值的结果向脚本返回一个值（这是大多数函数返回结果的方式），你需要调用一个将返回结果设置为特定对象的函数。该对象通常是在函数内部创建的（因此引用计数为 0）。如果函数的返回值被赋值给变量，则对象的引用计数将增加；否则，该对象将被删除。

## 12.1 概述

语法: void Tcl_SetObjResult (interp, objPtr)
语法: void Tcl_SetResult (interp, string, freeProc)

Tcl_SetObjResult
将 `objPtr` 指向的对象作为命令求值的结果返回给 Tcl 解释器。如果已经定义了结果，它将被 `objPtr` 指向的对象替换。

`Tcl_Interp *interp`
指向 Tcl 解释器的指针。

`Tcl_Obj *objPtr`
指向包含整数对象的指针。

`string`
以 NULL 终止的字符串。

void (*freeProc)(char *)
释放内存的函数指针。

- TCL_STATIC: 字符串位于静态内存中。
- TCL_DYNAMIC: 字符串是动态分配的。
- TCL_VOLATILE: 字符串在易性内存中。

# 第 12 章 编写 Tcl 扩展

### 12.1 向脚本返回状态

当函数向 Tcl 解释器返回状态时，必须是 TCL_OK 或 TCL_ERROR。如果函数返回 TCL_OK，脚本将继续。

如果函数返回 TCL_ERROR，将生成错误，除非脚本使用 `catch` 命令捕获错误，否则执行将停止。

默认情况下，错误信息是产生错误的命令。你可能希望向此添加更多信息，例如文件写入失败、套接字无法连接。

你可以通过调用函数向该消息添加更多信息。

语法: Tcl_AddErrorInfo (interp, message)

```
语法: void Tcl_AddErrorInfo (interp, message)
```

Tcl_AddErrorInfo
向信息对象附加文本。该信息对象可以在 Tcl 脚本中作为全局变量 `errorInfo` 被访问。

```
语法: void Tcl_SetErrorCode (interp, ...)
```

Tcl_SetErrorCode
设置 `errorCode` 对象的值。如果对象包含列表，列表值将拼接在一起形成返回。默认情况下 errorCode 为 NONE。

## 12.1 概述

Tcl_SetErrorCode
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
