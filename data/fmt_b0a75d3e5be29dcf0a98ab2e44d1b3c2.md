
* `CmdReturn` *Demo_GetstrCmd()-

* demonstrates retrieving a structure pointer from a hash

* table, and stuffing that into a list.

*/

- Arguments

  - `objv[0]`: "demo"

  - `objv[1]`: "getstr"

  - `objv[2]`: `hash_Key`

- Results

  - No changes to hash table. Returns saved value, or sets error.

- Side Effects:

  - None

```c
CmdReturn *Demo_GetStrCmd (ClientData info,
    Tcl_Interp *interp,
    int objc,
    Tcl_Obj *objv[]) {
    Tcl_HashEntry *hashEntryPtr;
    CmdReturn *returnStructPtr;
    char *returnCharPtr;
    Tcl_Obj *returnObjPtr;
    Tcl_Obj *listPtrPtr[3];
    char *hashKeyPtr;
    struct demo {
        int firstInt;
        char *secondString;
        double thirdFloat;
    } *demoStruct;
    debugprint("Demo_GetCmd called with %d args\n", objc);

    /*
     * Allocate the space and initialize the return structure.
     */

    returnStructPtr = (CmdReturn *)malloc(sizeof(CmdReturn));
    returnStructPtr->status = TCL_OK;
    returnStructPtr->object = NULL;
    returnCharPtr = NULL;
    returnObjPtr = NULL;

    /*
     * Get the argument
     * And the attempt to extract that from the table.
     * If returned entry is NULL, key is not in the table.
     */

    hashKeyPtr = Tcl_GetStringFromObj(objv[2], NULL);
    hashEntryPtr = Tcl_CreateHashEntry(demo_hashtblPtr, hashKeyPtr, &isNew);
    if (!isNew) {
        char errString[80];
        sprintf(errString, "Hashed object named \"%s\" already exists.\n", hashKeyPtr);
        Tcl_AddObjError(interp, errString, strlen(errString));
        returnStructPtr->status = TCL_ERROR;
        goto done;
    }

    /*
     * If we are here, then the key is unused.
     * Get the string representation from the object,
     * and make a copy that can be placed into the hash table.
     */

    tmpString = Tcl_GetStringFromObj(objv[3], &length);
    hashEntryContentsPtr = (char *) malloc(length+1);
    strcpy(hashEntryContentsPtr, tmpString);
    debugprint("setting: %s\n", hashEntryContentsPtr);
    Tcl_SetHashValue(hashEntryPtr, demoStruct);
done:
    if ((returnObjPtr == NULL) && (returnCharPtr != NULL)) {
        returnObjPtr = Tcl_NewString(returnCharPtr, -1);
    }
    returnStructPtr->object = returnObjPtr;
    if (returnCharPtr != NULL) {
        free(returnCharPtr);
    }
    return returnStructPtr;
}
```

# 第 12 章 编写 Tcl 扩展

## 12.4 复杂数据

## 12.5 脚本

Tcl 扩展可以用于多种目的，包括：
- 为现有库添加图形功能
- 为 Tcl 解释器添加新功能
- 从库进行快速原型开发

Tcl 扩展必须包含：
- `ExtName_Init` 函数
- 实现每个 Tcl 命令的代码

Tcl 扩展还应该包含：
- 一个名为 `extName.h` 的头文件
- 一个 `Makefile`

Tcl 扩展可以包含其他文件，以使其代码更具维护性和模块化。

新的 Tcl 命令通过以下方式定义：

```c
语法: int Tcl_CreateObjCommand (interp, cmdName, func, clientData)
```
