
``` 
0040151F   : 85C0                TEST EAX,EAX

00401521   : B4 00000000         MOV EDX,0

00401525   : 74 15               JE SHORT strcpy.0040153E

00401528   : C7A424 04 0E41      MOV DWORD PTR SS:[ESP+4...  ASCII "_Jv_RegisterClasses"

00401530   : B99424              MOV DWORD PTR SS:[ESP+... 

00401533   : FF15 29614000       CALL DWORD PTR DS:[46129]...  GetProcAddress

00401539   : 83EC 08             SUB ESP,8

0040153C   : 89F2                MOV EDX,EAX

0040153E   : 85D2                TEST EDX,EDX

00401540   : 74 09               JE SHORT strcpy.0040154B

00401542   : C70424 2C30A00      MOV DWORD PTR SS:[ESP]...  strcpy.0040302C

00401549   : FFD2                CALL EDX

0040154B   : C70424 601540      MOV DWORD PTR SS:[ESP],...  strcpy.00401548

00401552   : E3 29610000         CALL strcpy.00461000

00401557   : C9                   LEAVE

00401558   : C3                   RET

00401559   : 89C426 000000       LEA DS:[ESI]

00401560   : 55                   PUSH EBP

00401561   : 89E5                 ...  EBP,ESP

00401563   : 5D                   POP EBP

00401564   : C3                   RET
```

图 186: Immunity 调试器汇编窗口

右上角的窗口（图 187）包含所有寄存器，包括我们最感兴趣的两个：`ESP` 和 `EIP`。由于根据定义 `EIP` 指向下一条要执行的代码指令，它被设置为 `0x004014E0`，即汇编窗口（图 185）中高亮的指令。

![](img/ec25e59d75726b7041242a56d3376832_356_0.png)

图 187：Immunity 调试器寄存器窗口

右下角窗口（图 188）显示了栈及其内容。该视图包含四列：内存地址、该地址处的十六进制数据、数据的 ASCII 表示形式，以及一条动态注释，当可用时提供与特定栈条目相关的附加信息。数据本身（第二列）以 32 位值的形式显示，称为*双字*（`DWORD`），显示为四个十六进制字节。请注意，此窗格在栈顶显示地址 `0x0065FF84`，而这实际上正是寄存器窗口（图 187）中 `ESP` 存储的值：

![](img/ec25e59d75726b7041242a56d3376832_357_0.png)

图 188：Immunity 调试器栈窗口

最后一个窗口位于左下角，显示任意给定地址的内存内容。与栈窗口类似，它显示三列，包括内存地址以及数据的十六进制和 ASCII 表示形式。顾名思义，该窗口在搜索或分析进程内存空间中的特定值时可能很有帮助，通过右键单击窗口内容访问上下文菜单，可以不同格式显示数据。

![](img/ec25e59d75726b7041242a56d3376832_357_1.png)

图 189：Immunity 调试器数据窗口

## 10.2.3 代码导航

在映射了调试器的不同窗口后，现在是导航汇编代码的时候了。加载时，应用程序执行被暂停，调试器右下角的“Paused”字样表明了这一点。如前一节所述，调试器在程序入口点自动暂停。

我们现在可以使用 `Debug > Step into` 或 `Debug > Step over` 命令一次执行一条指令，它们的快捷键分别为 `F7` 和 `F8`。两者的区别在于，`Step into` 会跟随执行流程进入给定的函数调用，而 `Step over` 将执行整个函数并从中返回。

由于本例中的入口点与主函数的开头并不一致，我们的第一个目标是在内存中找到 `main` 函数的位置。在这个特定应用程序中，我们可以搜索进程内存空间以找到下面突出显示的错误消息，以帮助确定方位：

```c
#include <stdio.h>

#include <string.h>

int main(int argc, char *argv[])

{

    char buffer[64];

    if (argc < 2)

    {

        printf("Error - You must supply at least one argument\n");

        return 1;

    }

    strcpy(buffer, argv[1]);

    return 0;

}
```
