
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

# 第 12 章 编写 Tcl 扩展

```c
Retrieved: This is data in the hashTable
```

## 12.1 概述

扩展的大部分可能是已经开发并测试的库、需要测试和验证的库，或者是你为特定扩展编写的代码集。在这些情况下，你都使用上述函数来连接应用程序和解释器。

下一步是构建扩展的机制。

### 12.2.1 扩展结构概述

扩展由一个或多个源代码、头文件和一个 `Makefile` 组成。源代码必须包含一个初始化函数，且该函数必须符合命名规范。常见的结构是创建两个文件：一个包含初始化函数，另一个包含新命令。

## 12.2 构建扩展

所有使用 Tcl 库函数的代码都需要包含 `tcl.h`。`Tcl.h` 文件包含了与 Tcl 库交互所需的函数原型、`#define`、定义等。

### 12.2.2 命名规范

编写 Tcl 扩展涉及一些命名规范。其中某些是与 Tcl 解释器交互所必需的，另一些是为了符合其他 Tcl 扩展的外而建议的。如果你按照建议的标准编写扩展，将便于他人使用和扩展你的扩展。

这些规范在 Tcl/Tk 工程手册中有描述，该手册附在本书的光盘中。你也可以通过 FTP 从 `mirror.neoft.com` 获取 `/usr/ftp/archive0/tcl/mirror/ftp.docs/engManual.tar.Z`。在开始编写扩展之前，我建议阅读工程手册。这可以避免一些重写。

| 函数名称 | 描述 |
|---|---|
| `ExtName_Init` | 此函数是必须的。它通过创建持久数据对象并向 Tcl 解释器注册命令来初始化扩展。此入口点用于加载 DLL（动态链接库）或共享库时初始化扩展。大小写很重要。例如，对于名为 `ext` 的扩展，`Init` 函数应该是 `Ext_Init`。 |
| `ExtName_AppInit` | 此函数被调用初始化一个带有该扩展的独立 `tclsh` 解释器。 |

# 第 12 章 编写 Tcl 扩展

| 函数名称 | 描述 |
| :--- | :--- |
| `extName_command NameCmd` | 这些入口是可选的，但这是由 Tcl 脚本求值 `commandName` 命令时，被调用的 C 代码所采用的命名约定。 |

| 文件 | 描述 |
| :--- | :--- |
| `extNameInt.h` | 该文件是必须的。它将包含 `#include` 语句、`#define` 语句、数据结构定义以及该扩展程序代码中使用的函数原型。 |
| | 该文件供包内部使用。它将被所有扩展程序代码文件包含。 |
| `extNameInit.c` | 该文件是必须的。它将包含 `ExtName_Init` 函数。如果你的应用程序很简单，它可能还会包含实现扩展的 C 语言函数。 |
| `extNameCmd.c` | 该文件是可选的。如果 Tcl 和 C 代码之间的接口代码很大，你可能希望从 `extNameInit.c` 文件中分离出在 Tcl 解释器中创建新命令的代码，并将其放在单独的文件中。 |
| `extNameCmdAL.c` `extNameCmdMZ.c` | 这些文件是可选的。如果你有一个非常大的扩展程序，将实现命令的函数拆分为较小的文件可以使代码更容易易读。这里使用的一种约定是将以字母 A 到某些其他字母开头的命令放在一个文件中，而将以断点字母之后的某个字符开头的命令放在另一个文件中。 |

## 12.2 编译扩展程序

这些文件是可选的。如果你的扩展程序包含可以接受多个子命令的命令，或者如果该命令是通过多个函数实现的，那么将实现命令的函数拆分到单独的文件中可以使代码更容易易读。因此，实现 `foo` 命令的函数将位于 `extFoo.c` 中，而实现 `bar` 命令的函数将位于 `extBar.c` 中。

`extNameCommand.c`

当你完成扩展程序的编译时，将为你的扩展程序创建一个以下格式之一的文件。
- `extName.dll`
- `ibextName.so`
- `extName.shlb`
- `extNameCFM68K.shlb`

Tcl 解释器将使用扩展程序的 `extName` 部分来寻找默认的 `ExtName_Init` 函数。

如果你无法遵循此扩展文件的命名约定，可以通过如下在 `load` 命令中声明扩展程序名称来强制 Tcl 解释器找到初始化函数：

`load wrongname.dll myextension`

不遵循扩展文件的命名约定将无法使用 `pkg_mkIndex` 构建 `tclIndex` 文件，但如有必要，你可以使用文本编辑器构建索引行。

# 第 12 章 编写 Tcl 扩展

## 12.3 示例

本节将构建一个简单的扩展程序，以演示本章讨论的机制。在 CD-ROM 上你将找到演示代码、来自 Sun 的示例扩展包，以及一个 `dummyTclExtension` 工具包，该工具包包含一个创建一个与示例扩展类似的骨架扩展的 Tcl 脚本。

此示例遵循了 CD-ROM 上的《Tcl/Tk 工程手册》中的编码标准。在手册未定义标准的地方，我会注明该约定是我个人的，而不是 Tcl 标准。否则，其命名约定是由 Tcl 社区定义的。

此演示扩展程序不执行任何计算。它只是展示了如何构建扩展程序，以及如何使用哈希函数获取并返回数据。

演示包实现了一个 Tcl 命令以及该命令内部的五个子命令。

子命令是 `debug`、`create`、`get`、`destroy` 和 `set`。

语法：`demo debug level`

`demo debug` 在 C 代码中设置一个静态全局变量，用于开启或关闭内部调试输出。

`level` 分配给该变量的级别。零将禁用调试输出，非零值将启用该输出。

语法：`demo create key raw_message`

`demo create` 创建一个哈希表条目。

`key` 该哈希表条目的键。

`raw_message` 分配给此哈希的字符串。

语法：`demo get key`

`demo get` 从哈希表中检索条目的值并返回与该键关联的字符串。

`key` 要返回的条目的键。

**语法：** `demo destroy key`

`demo destroy` 删除哈希表中的一个条目。

`key` 标识要删除哪个条目的键。

**语法：** `demo set arrayName index`

`demo set` 如何设置关联数组中值的示例。它将 `index` 设置为请求的值，并将数组的索引 `alpha` 设置为值 `NewValue`。索引 `alpha` 和值 `NewValue` 在 `Demo_SetCmd` 程序中硬编码。

此子命令执行等同于以下 C 代码：
