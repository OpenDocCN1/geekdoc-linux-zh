

# 第 12 章 编写 Tcl 扩展

```c
hashKeyPtr, "\", (char *) NULL);
returnStructPtr->status = TCL_ERROR;
gone done;
)
/* 2
 * 获取存储在哈希表中的指针
 * 并释放它。然后删除哈希表项。
 */
hashEntryContentsPtr =
    (char *)Tcl_GetHashValue(hashEntryPtr);
    free(hashEntryContentsPtr);
Tcl_DeleteHashEntry(hashEntryPtr);
done:
    if ((returnObjPtr == NULL) && (returnCharPtr != NULL)) {
        returnObjPtr = Tcl_NewStringObj(returnCharPtr, -1);
    }

returnStructPtr->object = returnObjPtr;
    if (returnCharPtr != NULL){free(returnCharPtr);}

    returnStructPtr;
```

- 1. 此函数允许解释器设置 `errorInfo` 和 `errorCode` 值。字符串“找不到哈希对象...”将作为命令的结果返回，并放入 `errorInfo` 变量中。
- 2. 存储在哈希表中的数据是指向在 `Demo_CreateCmd` 函数中创建的字符串的指针。一旦删除 `Tcl_HashEntry`，除非有其他代码引用它，否则该指针将成为孤儿。在本示例中，没有其他代码使用该指针，因此必须释放内存。

## 12.3.4.5 Demo_SetCmd

`Demo_SetCmd` 演示了如何在调用脚本中创建或修改数组变量。默认情况下，变量将被设置为调用 `demo set` 命令所在的作用域内。如果在过程（procedure）内部调用 `demo set`，则该变量仅在过程过程执行期间存在。Tcl 解释器会在过程完成后处理变量释放。

`Demo_SetCmd` 使用 `Tcl_ObjSetVar2` 函数来设置数组变量的值。`Tcl_ObjSetVar2` 和 `Tcl_ObjGetVar2` 函数允许 C 代码获取或设置 Tcl 脚本变量的值。

`Tcl_ObjSetVar2` 和 `Tcl_ObjGetVar2` 是 Tcl 解释器用于访问脚本变量的函数。Tcl 解释器支持脚本的任何行为也适用于使用这些函数的 C 代码。

你可以通过 `flags` 参数如下修改这些命令的行为：

- 当访问现有变量时，`Tcl_ObjGetVar2` 命令首先尝试在本地过程作用域中查找变量。如果失败，它会在当前命名空间中查找使用 `variable` 命令定义的变量。最后，它会在全局作用域中查找。
- `Tcl_ObjSetVar2` 函数默认会覆盖变量的现有值。默认不会将新数据追加到现有变量。
- 引用数组时，数组名和索引是在单独的对象中引用的。默认情况下，你无法使用具有 `name(index)` 表示的对象来引用数组项。

```c
Syntax: Tcl_Obj *Tcl_ObjSetVar2 (interp, id1Ptr, id2Ptr, newValPtr, flags)
```

```c
Syntax: Tcl_Obj *Tcl_ObjGetVar2 (interp, id1Ptr, id2Ptr, flags)
```

```c
Syntax: char *Tcl_SetVar2 (interp, name1, name2, newstring, flags)
```

```c
Syntax: char *Tcl_GetVar2 (interp, name2, name1, flags)
```

`Tcl_ObjSetVar2` 创建或修改 Tcl 变量。所引用变量的值将被设置为 `newValPtr` 的值。`Tcl_Obj` 指针是指向新对象的指针。如果访问 `newValPtr` 触发的事件修改了 `newValPtr` 的内容，则它可能不是指向 `newValPtr`。这发生在你使用 `trace` 命令观察变量时。请参阅第 15.1 节关于使用 `trace` 的讨论，并在在线帮助中阅读关于 `trace` 命令以了解如何发生这种情况。

### Tcl_ObjGetVar2

返回一个 Tcl 对象，其值由 `id1Ptr` 和 `id2Ptr` 中的字符串值标识。

### Tcl_SetVar2

创建或修改脚本变量。所引用变量的值将被设置为 `newstring`。此函数返回一个指向新值的 `char *`。此函数用于比 8.0 旧的 Tcl 版本。

### Tcl_GetVar2

返回由 `name1` 和 `name2` 中的字符串值标识的变量或数组的字符串值。此函数用于比 8.0 旧的 Tcl 版本。

### Tcl_Interp *interp

指向 Tcl 解释器的指针。

### Tcl_Obj *id1Ptr

包含 Tcl 变量名称的对象。这可以是简单变量或数组名。

### Tcl_Obj *id2Ptr

如果此不为 `NULL`，它包含数组变量的索引。如果此不为 `NULL`，`id1Ptr` 必须包含数组变量名。

### char *name1

引用简单 Tcl 字符串变量或关联数组的字符串。

### char *name2

如果此不为 `NULL`，它是数组变量的索引。如果此不为 `NULL`，`name1` 必须包含数组变量名。

### Tcl_Obj *newValPtr

指向对象的指针，其新值将被赋值给 `id1Ptr` 和 `id2Ptr` 描述的变量。

### char *newstring

包含新值的字符串，该新值将被赋值给 `name1` 和 `name2` 描述的变量。

int flags

`flags` 参数用于调整这些命令的行为。

- `TCL_GLOBAL_ONLY`: 设置此标志会导致变量仅位于全局作用域，而不是过程作用域。
- `TCL_NAMESPACE_ONLY`: 设置此标志会导致变量仅位于当前命名空间，而不是过程作用域。
- `TCL_LEAVE_ERR_MSG`: 设置此标志在出错时会将错误消息放在解释器中。
- `TCL_APPEND_VALUE`: 设置此标志会将新值追加到现有值而不是覆盖它。
- `TCL_LIST_ELEMENT`: 设置此标志会将新值转换为有效的列表元素而不是覆盖它。
- `TCL_PARSE_INDEX`: 设置此标志，`id1Ptr` 对象将作为索引而不是使用 `id2Ptr` 作为值。

## 示例 12.3.4.5 Demo_SetCmd

```c
/*
* CmdReturn *Demo_SetCmd
* 演示数组
* Arguments
* objv[0]: "demo"
* objv[1]: "set"
* objv[2]: arrayName
* objv[3]: Index
* objv[4]: Value
* Results
* 设置 arrayName(index) 为值
* 也会 arrayName(alpha) 为 "NewValue"
* 返回 "NewValue"
* Side Effects:
* 无
*/
CmdReturn *Demo_SetCmd (ClientData info,
    Tcl_Interp *interp,
    int objc,
    Tcl_Obj *objv[]) {
    Tcl_Obj *returnObjPtr;
    Tcl_Obj *indexObjPtr;
    Tcl_Obj *arrayObjPtr;
    Tcl_Obj *valueObjPtr;
    CmdReturn *returnStructPtr;
    printf("Demo_SetCmd called with %d args\n", objc);

    /*
    * 分配空间并初始化返回结构。
    */
    returnStructPtr = (CmdReturn *) malloc(sizeof(CmdReturn));
    returnStructPtr->status = TCL_OK;
    returnObjPtr = NULL;

    /* 1
    * 使用 Tcl_ObjSetVar2 将数组元素 "Index" 设置为
    * "Value"
    */
    arrayObjPtr = objv[2];
    Tcl_ObjSetVar2(interp, arrayObjPtr, objv[3], objv[4], 0);

    /* 2
    * 创建两个新对象以设置索引 "alpha"的值。
    */
    indexObjPtr = Tcl_NewStringObj("alpha", -1);
    valueObjPtr = Tcl_NewStringObj("NewValue", -1);
    returnObjPtr = Tcl_ObjSetVar2(interp, arrayObjPtr,
    indexObjPtr, valueObjPtr, 0);

    returnStructPtr->status = TCL_OK;
    returnStructPtr->object = returnObjPtr;

    /* 3
    * 通过减少引用计数删除临时对象
    * 对象管理器会在引用计数变为 0 时释放它们
    * 以及关联内存。
    */
    Tcl_DecrRefCount(indexObjPtr);

    /* 4
    * 不要删除 valueObjPtr - 它是 returnObjPtr
    * 对象。如果你清除它，任务核心将转储，
    * 然后使用它。
    * Tcl_DecrRefCount(valueObjPtr);
    */
    return returnStructPtr;
}
```

