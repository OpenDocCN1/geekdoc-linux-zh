

# 第 12 章 编写 Tcl 扩展

## 12.3 示例

```c
sprintf(errString,
  "Hashed object named \"s\" already exists.\n", hashKeyPtr);
```

```c
/* 4
 * 这两个字符串将被添加到 Tcl 脚本
 * 全局变量 errorInfo 中
 */
```

```c
Tcl_AddErrorInfo(interp, "error in Demo_CreateCmd");
Tcl_AddObjErrorInfo(interp, errString,
  strlen(errString));
```

```c
/* 5
 * 此 SetErrorCode 命令将 Tcl 脚本
 * 变量 errorCode 设置为 "5 5 5"
 */
```

```c
Tcl_SetErrorCode(interp, "5", "5", "5", (char *) NULL);
/*
 * 这定义了该子命令的返回字符串
 */
```

```c
/* 6
 * 如果我们到了这里，说明键未被使用。
 * 从对象中获取字符串表示，
 * 并创建一个可以放入哈希表的副本。
 */
```

```c
hashString = Tcl_GetStringFromObj(objv[3], &length);
hashEntryContentsPtr = (char *) malloc(length+1);
strcpy(hashEntryContentsPtr, tmpString);
```

```c
debugprint("setting: %s\n", hashEntryContentsPtr);
Tcl_SetHashValue(hashKeyPtr, hashEntryContentsPtr);
```

```c
/* 7
 * 设置返回值，清理并返回
 */
done:
if ((returnObjPtr == NULL) && (returnCharPtr != NULL)) {
    returnObjPtr = Tcl_NewStringObj(returnCharPtr, -1);
}
returnStructPtr->object = returnObjPtr;
if (returnCharPtr != NULL) {free(returnCharPtr);}
returnStructPtr;
```

- 1. 这不是 Tcl 标准的一部分。我发现在许多情况下，我需要生成执行轨迹来追踪那些每连续运行三周才会出现一次的错误。因此，我希望在每次进入函数时都能启用输出消息。
- 2. `returnStructPtr` 在处理子命令的每个函数中都进行了初始化。它将在 `Demo_Cmd` 函数返回后被释放。
- 3. 如果 `hashKeyPtr` 已经存在，则 `isNew` 将设置为零，并返回指向上一个 `hashEntryPtr` 的指针。如果你的代码通过 `Tcl_SetHashValue` 设置了此项的值，旧数据将会丢失。
- 4. 注意，此示例中的 `sprintf` 调用容易出错。如果键超过 37 个字符，它将溢出为 `errString` 分配的 80 个字符。健壮应该计数字符，为字符串分配空间，调用 `Tcl_AddError` 将错误消息拷贝到错误返回，然后释放字符串。每当调用 `Tcl_AddError` 或 `Tcl_AddObjError` 时，它会将参数随换行符追加到全局脚本变量 `errorInfo` 的末尾。
- 5. `Tcl_SetErrorCode` 函数会在参数之间添加空格，强制每个参数成为一个单词。因此，你不能使用此函数将多位错误返回的字段合并为单个数值返回。
- 6. 注意，创建子命令第三个参数中的字符串数据在插入哈希表之前会被复制到另一个内存区域。参数对象是一个临时对象，当 demo create 命令完全求完成后，它将与其数据一起被销毁。

`TclHashEntry` 结构接受一个指针作为存储的数据。它返回指针，而不是将数据拷贝到新位置。因此，从 `Tcl_GetStringVarFromObj(obj[3],...)` 返回的字符串指针在调用 `Tcl_SetHashValue(obj)` 后，命令完成后字符串将被销毁，这些内存位置中的数据可能会损坏。
- 7. 所有实现 demo 子命令的函数都遵循：测试值、在需要时设置失败值以及使用 `goto` 退出函数。也可以使用结构化编程流，但在多个测试时会变得复杂且难以追踪。

## 12.3.4.3 Demo_GetCmd

`Demo_GetCmd` 将通过 demo create 命令插入哈希表的字符串。

该函数遵循与 `Demo_CreateCmd` 相同的流程。

示例：12.3.4.3

```c
Demo_GetCmd
--------------------------------------------
/* CmdReturn *Demo_GetCmd()--
* 从哈希表中检索值
* 返回哈希表中请求项的值
*
* 参数
* obj[0]: "demo"
* obj[1]: "get"
* obj[2]: hash Key

* 结果
* 哈希表没有变化。返回值或错误。
*
* 影响
* 无

```c
CmdReturn *Demo_GetCmd (ClientData info,
    Tcl_Interp *interp,
    int obj,
    Tcl_Obj *objv[]) {
    Tcl_HashEntry *hashEntryPtr;
    CmdReturn *returnStructPtr;
    char *returnCharPtr;
    Tcl_Obj *returnObjPtr;
    char *hashKeyPtr;
    
    debugprint("Demo_GetCmd called with %d args\n", obj);
    /*
    * 分配空间并初始化结构。
    */
    returnStructPtr = (CmdReturn *) malloc(sizeof(CmdReturn));
    returnStructPtr->status = TCL_OK;
    returnStructPtr->object = NULL;
    returnCharPtr = NULL;
    returnObjPtr = NULL;
    /*
    * 从参数获取键，
    * 尝试从哈希表中提取该项。
    * 如果返回的项为 NULL，则该键不在表中。
    */
    hashKeyPtr = Tcl_GetStringFromObj(obj[2], NULL);
    hashEntryPtr = Tcl_FindHashEntry(demo_hashtbl, hashKeyPtr);
    if (hashEntryPtr == (Tcl_HashEntry *) NULL) {
        char errString[80];
        Tcl_Obj *errorCodePtr;
        /*
        * 从整数定义错误码，
        * 设置 errorCode。
        */
        errorCodePtr = Tcl_NewIntObj(5);
        Tcl_SetObjErrorCode(interp, errorCodePtr);
        /*
        * 此字符串将放在全局变量
        * errorInfo 中
        */
        sprintf(errString, "%s does not exist.", hashKeyPtr);
        Tcl_AddErrorInfo(interp, errString);
        /*
        * 此字符串将作为命令的结果返回。
        */
        Tcl_AppendResult(interp, "cannot find hashed object \"", (char *) NULL);
        returnStructPtr->status = TCL_ERROR;
        goto done;
    }
    /*
    * 如果我们到了这里，说明搜索成功，我们可以
    * 从哈希项中提取数据并返回。
    */
    returnCharPtr = (char *) Tcl_GetHashValue(hashEntryPtr);
    debugprint("returnString: %s\n", returnCharPtr);

done:
  if ((returnObjPtr == NULL) && (returnCharPtr != NULL)) {
    returnObjPtr = Tcl_NewStringObj(returnCharPtr, -1);
  }
  returnStructPtr->object = returnObjPtr;
  if (returnCharPtr != NULL) {free(returnCharPtr);}
  returnStructPtr;
```

- 1. `Demo_GetCmd` 使用 `Tcl_SetErrorCode` 函数设置全局脚本变量 `errorCode`。此函数将 `errorCodePtr` 赋值给错误码。它没有拷贝对象。
- 2. 字符指针 `returnCharPtr` 将指向存储在哈希表中的字符串。这不是数据的。当使用 `Tcl_NewStringObj(returnCharPtr, -1)` 函数创建 `returnObjPtr` 时，数据会被复制。

## 12.3.4 Demo_DestroyCmd

`Demo_DestroyCmd` 函数将从哈希表中移除项并释放与之相关的内存。此示例使用了另一种设置返回的方法。默认行为是将全局脚本变量 `errorInfo` 设置为与函数返回相同的字符串，并将 `errorCode` 值设置为 `NONE`。此函数仅允许这种情况发生。

示例：12.3.4.4-1

Demo_DestroyCmd

```c
/* CmdReturn *Demo_DestroyCmd ()--
* 演示破坏哈希表项。
* 参数
* objv[0]: "demo"
* objv[1]: "destroy"
* objv[2]: hash Key
*
* 结果
* 删除哈希表项并释放与存储的哈希对象相关的内存。
*
* 影响
* 无
*/
CmdReturn *Demo_DestroyCmd (ClientData info,
    Tcl_Interp *interp,
    int objc,
    Tcl_Obj *objv[]) {
    Tcl_HashEntry *hashEntryPtr;
    CmdReturn *returnStructPtr;
    char *returnCharPtr;
    Tcl_Obj *returnObjPtr;
    char *hashEntryContentsPtr;
    char *hashKeyPtr;

    debugprint("Demo_DestroyCmd called with %d args\n", obj);
    /*
    * 分配空间并初始化返回结构。
    */
    returnStructPtr = (CmdReturn*) malloc(sizeof(CmdReturn));
    returnStructPtr->status = TCL_OK;
    returnStructPtr->object = NULL;
    returnCharPtr = NULL;
    returnObjPtr = NULL;
    /*
    * 从参数提取字符串表示，
    * 作为哈希表的键。
    */
    hashKeyPtr = Tcl_GetStringFromObj(objv[2], NULL);
    hashEntryPtr = Tcl_FindHashEntry(demo_hashtbl, hashKeyPtr);

    /*
    * 如果 hashEntryPtr 返回 NULL，则该键不在
    * 表中。返回错误。
    */
    if (hashEntryPtr == (Tcl_HashEntry *) NULL) {
        /*
        * Tcl_AppendResult 设置此命令的返回。
        * 脚本全局变量 errorInfo 也会被
        * 设置为此字符串。
        * 脚本全局变量 errorCode 将设置为
        * "NONE"
        */
        Tcl_AppendResult(interp,
"cannot find hashed object \"");
    }
```

