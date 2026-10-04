

## 第 12 章 编写 Tcl 扩展

```c
return(returnStructPtr);
)
```

- 1. 这部分代码实现了 `set arrayName (Index) Value` 的对应功能。
- 2. 这部分代码实现了 `arrayName(alpha) NewValue` 的对应功能。赋值给 `returnObjPtr` 的值是 `valueObjPtr` 的指针，因为 `valueObjPtr` 变量没有附加额外的处理。
- 3. 注意，你应该使用 `Tcl_DecrRefCount` 函数来释放 Tcl 对象。不要使用 `free` 函数。
- 4. `valueObjPtr` 也是在此函数中创建。`Tcl_ObjSetVar2` 调用将返回指向该对象的指针，但该对象的引用计数不会增加。

由于该对象正作为 `returnObjPtr` 返回，因此不应减少其引用计数。如果将该对象的指针传递给 `Tcl_DecrRefCount`，该对象将被销毁，导致 `returnObjPtr` 指向一个不存在的对象。当 Tcl 解释器尝试处理这个不存在的对象时，结果将非常不愉快。

## 12.4 复杂数据

如果你需要在扩展中处理复杂数据（如结构体），这里有一些选项。

- 1. 你可以在 Tcl 脚本中将结构体定义为值列表，并将其传递给扩展代码解析为结构体。
- 2. 你可以在 Tcl 脚本中使用关联数组（associative array），关联数组中的每个索引都是结构体中的一个字段。
- 3. 你可以创建一个函数，接收列表或数组格式的结构体值，将其解析为结构体，将结构放在哈希表中，并返回一个键给 Tcl 脚本供以后使用。

下面的代码段展示了如何使用 Tcl 关联数组将结构体传递到 C 代码扩展中。代码期望接收一个设置了相应索引的数组名称。数组的索引必须与结构体字段的名称相同。

### 示例 12.4-1：使用关联数组定义结构体

```c
...
Tcl_Obj      *indexPtr;
Tcl_Obj      *structElementPtr;
struct demo {
  int         firstInt;
  char        *secondString;
  double      thirdFloat;
} demo;
/* 用作数组索引的字段名称 */
char *fields[] = {"firstInt", "secondString", "thirdFloat", NULL};
/*
* 创建一个可以与 Tcl_ObjGetVar2 使用的对象，
* 以通过数组和索引名称查找对象
*/
indexPtr = Tcl_NewStringObj(fields[0], -1);
/*
* 遍历数组中的结构索引
*/
for (i=0; i<3; i++) {
  /*
   * 将索引设置为正在处理的字段
   */
  Tcl_SetStringObj(indexPtr, fields[i], -1);
  /*
   * 获取 arrayName(index) 标识的对象
   * 如果该值为 NULL，arrayName(index) 会报错。
   */
structElementPtr =
```c
Tcl_ObjGetVar2(interp, objv[2], indexPtr, 0);

if (structElementPtr == NULL) {
    Tcl_AppendResult(interp,
        "Array ", fields[i],
        " is not defined ", (char *) NULL);
    returnStructPtr->status = TCL_ERROR;
    goto done;
}
/*
* 这种奇特的方式确定正在处理的结构体元素，
* 但循环中可以工作。
* 如果对象中有非法值，解释器会自动设置错误返回。
*/
switch (i) {
    case 0: {
    int t;
    if (TCL_OK !=
        Tcl_GetIntFromObj(interp,
            structElementPtr, &t)) {
        returnStructPtr->status = TCL_ERROR;
        goto done;
    } else {
        demoStruct->firstInt = t;
    }
    break;
    case 1: {
    char *t;
    if (NULL == (t = Tcl_GetStringFromObj(structElementPtr, NULL))) {
        returnStructPtr->status = TCL_ERROR;
        goto done;
    } else {
        demoStruct->secondString = (char *)malloc(strlen(t)+1);
        strcpy(demoStruct->secondString, t);
    }
    break;
    case 2: {
    double t;
    if (TCL_OK !=
        Tcl_GetDoubleFromObj(interp,
            structElementPtr, &t)) {
            returnStructPtr->status = TCL_ERROR;
            goto done;
    } else {
        demoStruct->thirdFloat = t;
    }
    break;
}
}
```c
printf("demoStruct values: %d\n%s\n%f\n",
    demoStruct->firstInt, demoStruct->secondString, demoStruct->thirdFloat);
```

#### 脚本

```tcl
set struct(firstInt) "12"
set struct(secondString) "Testing"
set struct(thirdFloat) "34.56"
```

#### 脚本输出
```
demoStruct values:
12
Testing
34.560000
```

下一个示例演示了一对使用列表定义结构体元素并将其保存在哈希表中的函数。这些函数实现了 demo 扩展实现了 list 和 getstr。

这些函数引入了 Tcl 列表对象。Tcl 列表对象是一个包含指向其他对象的指针集合。Tcl 库中有几个命令可以操作列表对象。此示例仅引入了应用程序所需的几个函数。

**语法：** `int Tcl_ListLength (interp, listPtr, length)`

**Tcl_ListLength**
将列表长度（元素个数而非字符串长度）放在 `length` 参数中。该函数返回 Tcl_OK 或 TCL_ERROR。
`Tcl_Interp *interp` Tcl 解释器的指针。
`Tcl_Obj *listPtr` 列表对象的指针。
`int *length` 接收列表长度的指针。

**语法：** `int Tcl_ListObjIndex (interp, listPtr, index, elementPtr)`

**Tcl_ListObjIndex**
将索引标识的对象放在 `elementPtr` 变量。该函数返回 Tcl_OK 或 TCL_ERROR。
`Tcl_Interp *interp` Tcl 解释器的指针。
`Tcl_Obj *listPtr` 列表对象的指针。
`int index` 要返回的列表元素索引。
`Tcl_Obj **elementPtr` 将由索引设置的 Tcl_Obj 指针地址。

**语法：** `Tcl_Obj* Tcl_NewListObj (count, objv)`

**Tcl_NewListObj**
返回一个新 Tcl_Obj 列表对象的指针，指向 obj 数组中的每个对象。
`int count` obj 数组定义的对象数量。
`Tcl_Obj *objv[]` 将包含在列表 Tcl 对象指针数组。

### 示例 12.4-2：列表到结构体的示例

```c
/*
* CmdReturn *Demo_ListstrCmd (ClientData info,
* 接收一个键和一个数据项列表，将用于填充预定义的结构体。
* 新填充的结构体指针保存在哈希表中，通过 'key_Value' 引用。
*
* 参数:
* objv[0] "demo"
* objv[1] "liststr"
* objv[2] key_Value
* objv[3] structure_List
*
* 结果:
* 将结构体指针放在哈希表中。
*
* 影响:
* 无
*/
CmdReturn *Demo_ListstrCmd (ClientData info,
Tcl_Interp *interp,
int objc,
Tcl_Obj *objv[] {
    Tcl_HashEntry *hashEntryPtr;
    CmdReturn *returnStructPtr;
    char *returnCharPtr;
    Tcl_Obj *returnObjPtr;
    Tcl_Obj *listElementPtr;
```

```c
int listlen;
int isNewPtr;
int length;
char *tmpString;
int i;
char *hashEntryContentsPtr;
char *hashKeyPtr;

struct demo {
    int firstInt;
    char *secondString;
    double thirdFloat;
} *demoStruct;
```

```c
debugpr("Demo_ListstrCmd called with %d args\n", objc);
/* 分配空间并初始化返回结构。 */
returnStructPtr = (CmdReturn *) malloc(sizeof (CmdReturn));
returnStructPtr->status = TCL_OK;
returnStructPtr->object = NULL;
returnCharPtr = NULL;
returnObjPtr = NULL;
```

```c
/* 为结构体分配空间 */
demoStruct = (struct demo *) malloc(sizeof(struct demo));
/* 获取列表长度，然后遍历它。 */
tcl_ListObjLength(interp, objv[3], &listlen);
for(i=0; i< listlen; i++) {
    /* 从列表指针提取列表元素 */
    tcl_ListObjIndex(interp, objv[3], i, &listElementPtr);
    debugpr("Position: %d : Value: %s\n",
        i, Tcl_GetStringFromObj(listElementPtr, NULL));
}
```

