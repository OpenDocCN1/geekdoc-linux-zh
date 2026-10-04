

## 12.3 示例

3. Microsoft VC++ 对将动态加载的代码规定了一些约定。如果你的扩展程序只需要在 Unix 或 Macintosh 上编译，你可以删除此部分并简化函数原型。

4. `CmdReturn` 结构体并不是 Tcl 标准的一部分。我使用它是为了允许实现子命令的函数能够向实现主命令的函数返回一个状态和一个 `Tcl_Obj`。`status` 字段可以赋值为值 `TCL_OK` 或 `TCL_ERROR`。如果函数没有返回值，则 `object` 字段可以为 `NULL`，或者是一个指向 `Tcl_Obj` 的指针。

如果你发现其他更符合你需求的约定，请随时使用它们来替代。

5. 源代码文件中函数的函数原型。源文件中定义的所有函数也应在此处进行定义。

## 12.3.2 demoInit.c

`demoInit.c` 文件是扩展程序所需的文件之一。至少，此文件必须定义 `Demo_Init` 函数，如下所示（并在下文中进行了讨论）：

示例 12.3.2-1

```c
demoInit.c
#include "demoInt.h"

/* CVS Revision Tag */
#define DEMOINIT_REVISION $Revision: 1.2 $
/*
----------------------------------------------------------------------
* Demo_Init
*
* 从 demoAppInit() 调用，如果这是一个独立的
* shell；当包被编译成二进制包时，在加载包时调用。
*
* 结果:
* 一个标准的 Tcl 结果。
*
* 侧影响:
* 创建一个哈希表。
* 添加新命令。
* 为 demo_version 和 demoInit_revision 创建新的 Tcl 全局变量。
*--------------------------------------------------------------------------------------
```

```c
int Demo_Init(Tcl_Interp *interp) {
    /* interp      当前解释器。 */
    /* 1
     * 如果此应用程序需要在哈希表中
     * 存储任何数据，则初始化哈希表。
     */
    Demo_InitHashTable();
    /* 2
     * 为此扩展程序定义的命令
     * 调用 Tcl_CreateCommand
     */
    Tcl_CreateObjCommand(interp, "demo", Demo_Cmd,
        (ClientData) NULL, NULL);
    /* 3
     * 为 pkg_mkIndex 定义索引的包
     */
    Tcl_PkgProvide(interp, "demo", DEMO_VERSION);
    /* 4
     * 为此包定义版本
     */
    Tcl_SetVar((Tcl_Interp *) interp, "demo_version",
        DEMO_VERSION, TCL_GLOBAL_ONLY);

    /* 5
    * 不是强制要求。我喜欢将源代码
    * 修订版本作为 Tcl 变量可用。
    * 当你可以跟踪发布版本中所有文件的
    * 所有修订版本时，跟踪 bug 会更容易。
    */
    Tcl_SetVar((Tcl_Interp *) interp, "demoInit_revision",
        DEMOINIT_REVISION, TCL_GLOBAL_ONLY);
    /* 6
    */
    return TCL_OK;
}
```

Tcl 允许任何包创建自己的哈希表数据库来存储和检索任意数据。如果包需要与脚本共享持久性信息，它可能需要将该数据保存在哈希表中，并向脚本返回一个键以标识引用的是哪些数据。哈希表将在与表交互的函数中详细讨论。

- 2. `TCreateObjCommand` 函数创建一个 Tcl 命令 `demo`，并声明在评估此命令时调用函数 `Demo_Cmd`。
- 3. `Tcl_PkgProvide` 命令声明此包名为 `demo`，并且它是由 `DEMO_VERSION` 定义的版本。`DEMO_VERSION` 定义在 `demoInt.h` 中。
- 4. `Tcl_SetVar` 命令定义了一个全局 Tcl 变量 `demo_version` 作为此包的版本号。此定义允许脚本检查已加载的 `demo` 包的版本号。
- 5. 这不是 Tcl 标准的一部分。我的倾向是在每个模块中包含源代码修订字符串，以便于确定链接到包中的所有代码版本。我发现，当我处于项目的冲刺阶段并每天向测试人员发布多个版本时，这一点尤为重要，因为他们试图告诉我在哪个版本的代码上观察到了什么行为。
- 6. 最后，返回 `TCL_OK`。这些函数调用都不应失败。

## 12.3.3 demoCmd.c

`demoCmd.c` 文件是你大部分扩展程序代码所在的地方。对于小型扩展，此文件将包含实现你的包功能的所有代码。

`Demo_CmdFromObj` 函数引入了几个新的 Tcl 库函数。

`Tcl_GetIndexFromObj` 函数在单词列表中搜索目标单词。该函数将返回匹配目标单词的单词索引。此函数用于从子命令列表中提取目标单词或其缩写。

**语法：int Tcl_GetIndexFromObj (interp, tblPtr, flags, index)**

- `interp`: 解释器。
- `tblPtr`: 以空结尾的字符串列表。
- `flags`: 定义允许的匹配。如果是 `TCL_EXACT`，只返回精确匹配。
- `index`: 接收索引的指针。
- `msg`: 定义在 `tablePtr` 中的字符串。

```c
demoCmd.c
#include "demoInt.h"

/* 1
* 定义子命令
* 注意：顺序很重要。
* 这些是子命令。
*/
static char *subcommands[] = {
    "create", "set", "get", "debug", "destroy", NULL;
}

/* 2
* 这些定义子命令的位置。
*/
#define M_create 0
#define M_set 1
#define M_get 2
#define M_debug 3
#define M_destroy 4

/* 3
* CmdDefinition 结构描述了子命令
* 期望的参数数量（包括命令），
* 以及当参数超出范围时返回的使用消息。
*/
typedef struct cmd_Def {
char *usage;
int minArgCnt;
int maxArgCnt;
} cmdDefinition;

static cmdDefinition definitions[5] = {
{"create key raw_message", 4, 4},
{"set arrayName index", 5, 5},
{"get key ", 3, 3},
{"debug level", 3, 3},
{"destroy key", 3, 3}
};

/* 4
* 如果 demoDebugPrint != 0，则 debug 将打印
* 信息。该值通过子命令设置。
*/
int demoDebugPrint = 0;

/* 5
*-
--------------------------------------
*-
* Demo_Cmd --
* Demo_Cmd 被调用以处理 "demo" Tcl 命令。
* 它将解析子命令，并执行请求的操作。
*/

```c
int Demo_Cmd(ClientData demo,
    Tcl_Interp *interp,
    int objc,
    Tcl_Obj *objv[]) {
    /* ClientData demo,
    /* 使用。 */
    /* Tcl_Interp *interp;
    /* 当前解释器。 */
    /* int objc;
    /* 参数数量。 */
    /* Tcl_Obj *CONST objv[];
    /* 参数对象。 */
    int cmdnum;
    int result;
Tcl_Obj *returnValue;
Cmd_Return *returnStruct;
ClientData *info;
    /*
    * 初始化返回值
    */
    returnValue = NULL;
    returnStruct = NULL;
    /* 6
    * 检查是否至少有一个子命令，
    * 否则返回错误和使用消息
    */
    if (objc < 2) {
        Tcl_WrongNumArgs(interp, 1, objv,
            "subcommand ?options?");
        return TCL_ERROR;
    }
    /* 7
    * 在子命令列表中查找此 demo 子命令。
```

