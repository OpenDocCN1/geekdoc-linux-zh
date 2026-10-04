

## 第 12 章 编写 Tcl 扩展

对于更复杂的情况，Tcl 库包含了一些函数，允许你使用 Tcl 哈希表来存储键值对。你的扩展可以为数据结构分配内存，定义一个键来标识该结构，然后将指向结构的指针放入哈希表中，以便通过该键进行访问。键可以是字母数字字符串，并返回给 Tcl 脚本。当 Tcl 脚本需要访问数据时，它会将键传回给扩展代码，然后由代码从哈希表中检索数据。

Tcl 哈希表由一个 `Tcl_HashTable` 结构（由你的扩展代码分配）和根据需要创建的用于存储键/值对的 `Tcl_HashEntry` 结构组成。

在使用访问哈希表条目的函数之前，你必须先初始化哈希表。一旦初始化了表，你的代码就可以从哈希表中添加、访问或删除项了。

```
语法: void Tcl_InitHashTable(tablePtr, keyType)
Tcl_InitHashTable
```

初始化哈希表。

> **Tcl_HashTable *tablePtr**
> 指向 `Tcl_HashTable` 结构的指针。在调用 `Tcl_InitHashTable` 之前必须为该结构分配空间。

> **int keyType**
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
语法: Tcl_CreateHashEntry (tablePtr, key, newPtr)
```

```
语法: Tcl_FindHashEntry (tablePtr, key)
```

```
语法: void Tcl_DeleteHashEntry (entryPtr)
```

**Tcl_CreateHashEntry**

为请求的键分配并初始化一个新的 `Tcl_HashEntry` 对象。如果之前存在该键的条目，则 `newPtr` 被设置为 `NULL`。

**Tcl_FindHashEntry**

此函数返回指向与键值关联的 `Tcl_HashEntry` 对象的指针。如果该键不在此哈希表中，则此函数返回 `NULL`。

**Tcl_DeleteHashEntry**

此函数从表中移除一个哈希表条目。在调用此函数后，如果使用该键，`Tcl_FindHashEntry` 将返回 `NULL`。这不会破坏与哈希条目关联的数据。你与哈希表交互的函数必须手动处理这一点。

## 第 12 章 编写 Tcl 扩展

**Tcl_HashTable *tablePtr**
指向 Tcl 哈希表的指针。在被这些命令使用之前，必须通过 `Tcl_InitHashTable` 初始化此表。

**char *key**
定义此条目的键。此值必须是 `Tcl_InitHashTable` 调用中描述的类型之一。

**int *newPtr**
如果创建了新条目，则此值为 1；如果已存在具有此值的键，则值为 0。

**Tcl_HashEntry *entryPtr**
指向哈希表的指针。

一个 `Tcl_HashEntry` 包含标识它的键值和一个 `Client-Data` 对象。`ClientData` 类型是一个字（word）的对象。在大多数现代机器上，它的大小与指针相同，这允许你分配任意的数据空间并将指向该空间的指针放置在 `Tcl_HashEntry` 中。

你可以使用 `Tcl_SetHashValue` 和 `Tcl_GetHashValue` 命令操作 `Tcl_HashEntry` 对象。

**语法：** ClientData TclGetHashValue (entryPtr)
**语法：** void TclSetHashValue (entryPtr, value)

**Tcl_GetHashValue**
从 `Tcl_HashEntry` 中检索数据。

**Tcl_SetHashValue**
设置 `Tcl_HashEntry` 中数据的值。

**Tcl_HashEntry *entryPtr**
指向哈希表的指针。

**ClientData value**
要放置在 `Tcl_HashEntry` 的 `clientData` 字段中的值。

下面是一个代码片段，它将创建一个哈希表、添加条目并检索数据。

## 12.1 概述

### 示例 12.1.9-1

### 示例代码片段

```c
void hashSnippet () {
    Tcl_HashTable *hashTable;
    Tcl_HashEntry *firstEntry, *secondEntry;
    int isNew;
    char *insertData, *retrievedData;
    char *key;

    key = "myKey";
    insertData = "This is data in the hashTable";
    /* 为哈希表分配空间并初始化它 */
    hashTable = (Tcl_HashTable *)malloc(sizeof(Tcl_HashTable));
    Tcl_InitHashTable(hashTable, TCL_STRING_KEYS);

    /* 在哈希表中创建一个条目 */
    firstEntry = Tcl_CreateHashEntry(hashTable, key, &isNew);
    if (isNew == 0) {
        printf("Key already exists!\n");
        return;
    }

    /*为此条目设置值 */
    Tcl_SetHashValue(firstEntry, insertData);

    /* 使用键查找条目 */
    secondEntry = Tcl_FindHashEntry(hashTable, key);
    if (secondEntry == NULL) {
        printf("Failed to find %s\n", key);
        return;
    }

    /* 从条目中提取数据 */
    retrievedData = (char *)TclGetHashValue(secondEntry);
    /* 显示数据以证明 */
    printf("Retrieved: %s\n", retrievedData);
}
```

**输出：**
```
Retrieved: This is data in the hashTable
```

## 第 12 章 编写 Tcl 扩展

```c
Retrieved: This is data in the hashTable
```

## 12.1 概述

扩展的大部分可能是已经开发并测试的库、需要测试和验证的库，或者是你为特定扩展编写的代码集。在这些情况下，你都使用上述函数来连接应用程序和解释器。

下一步是构建扩展的机制。

### 12.2.1 扩展结构概述

扩展由一个或多个源代码、头文件和一个 Makefile 组成。源代码必须包含一个初始化函数，且该函数必须符合命名规范。常见的结构是创建两个文件：一个包含初始化函数，另一个包含新命令。

## 12.2 构建扩展

所有使用 Tcl 库函数的代码都需要包含 `tcl.h`。`Tcl.h` 文件包含了与 Tcl 库交互所需的函数原型、`#define`、定义等。

### 12.2.2 命名规范

编写 Tcl 扩展涉及一些命名规范。其中某些是与 Tcl 解释器交互所必需的，另一些是为了符合其他 Tcl 扩展的外而建议的。如果你按照建议的标准编写扩展，将便于他人使用和扩展你的扩展。

这些规范在 Tcl/Tk 工程手册中有描述，该手册附在本书的光盘中。你也可以通过 FTP 从 `mirror.neoft.com` 获取 `/usr/ftp/archive0/tcl/mirror/ftp.docs/engManual.tar.Z`。在开始编写扩展之前，我建议阅读工程手册。这可以避免一些重写。

| 函数名称 | 描述 |
|---|---|
| ExtName_Init | 此函数是必须的。它通过创建持久数据对象并向 Tcl 解释器注册命令来初始化扩展。此入口点用于加载 DLL（动态链接库）或共享库时初始化扩展。大小写很重要。例如，对于名为 `ext` 的扩展，`Init` 函数应该是 `Ext_Init`。 |
| ExtName_AppInit | 此函数被调用初始化一个带有该扩展的独立 tclsh 解释器。 |

