
```asm
CMP                         BYTE PTR DS:_OstickDOSCtr, 0

        SHORT _OstickISR           ; 每 11 ticks (-199.9 Hz)，进入 DOS

    JNE

    MOV                         BYTE PTR DS:_OstickDOSCtr, 11

        081H                        ; 进入 DOS 的滴答 ISR

    CMP

        SHORT _OstickISR2

_OstickISR:

    MOV                         AL, 20H                     ; 将 EOI 代码移入 AL。

        DX, 20H                     ; DX 中 259 PIC 的地址。

    OUT                         DX, AL                      ; 如果未处理 DOS，则向 PIC 发送 EOI。

_OstickISR2:

    CALL                        FAR PTR _OstickTime      ; 处理系统滴答

    CALL                        FAR PTR _OSIntEnt         ; 通知 uC/OS-II ISR 结束

;

    POP                         DS

    POP                         ES

    POPA

;

    IRET                        ; 返回到中断任务

_OstickISR  ENDP
```

# 列表 9.6, `OstickISR()`

你可以在 9.7 中通过不对滴答率从 18.2048 Hz 增加到 200 Hz 来简化它。9.7 所示伪代码包含了 ISR 需要采取的步骤。ISR 仍然需要在当前任务的栈 L 上保存所有寄存器 L.9(7)，并增加 `OSIntesting` L.9(7)。接下来，调用 DOS 滴答处理程序 L.9(3)。注意，不需要清除发生的中断，因为这是由 DOS 滴答程序处理的。当我们调用 `OSTimeTick()` 时，µC/OS-II 可以更新所有等待时间过期或挂起事件但带有超时的任务 L.9(4)。当你调用 `OSIntEnt()` L.9 (5)。最后，恢复处理器寄存器 L.9(6)，ISR 通过执行 `IRET` 指令返回到中断源 L.9(7)。注意，如果你要使用此版本的代码，**绝对不能**通过调用 `PC_SetTickRate()` 来更改滴答率。你还需要将配置常量 `OS_TICKS_PER_SEC`（参见 `OS_CFG.H`）从 200 更改为 181！

```c
void OSTickISR (void)
{
    Save processor registers;               (1)
    OSIntNesting++;                         (2)
    Chain into DOS by executing an 'INT 81H' instruction;   (3)
    OSTimeTick();                          (4)
    OSIntExit();                            (5)
    Restore processor registers;           (6)
    Execute a return from interrupt instruction IRET;   (7)
}
```

### 列表 9.7, 18.2 Hz `OSTickISR()` 的伪代码

`OSTickISR()` 的新代码看起来如 9.8 所示。

```asm
_OstickISR  PROC                    ; 保存中断任务的上下文
    PUSH        FAR
    PUSH        ES
    PUSH        DS
    MOV         AX, SEG _OSIntNesting  ; 重载 DS
    MOV         DS, AX
    INC         BYTE PTR _OSTickISR     ; 通知 UC/OS-II 处于 ISR
    INT         08H                     ; 进入 DOS 的滴答 ISR
    CALL        FAR PTR _OSTimeTick     ; 处理系统滴答
    CALL        FAR PTR _OSIntExit      ; 通知 UC/OS-II ISR 结束
    POP         DS                      ; 恢复中断任务的上下文
    POP         ES
    POP         POPA
    IRET
_OstickISR  ENDP
```

### 列表 9.8, 18.2 Hz 版本的 `OSTickISR()`

## 9.05 `OS_CPU.C`

µC/OS-II 端口需要你编写六个函数：

```c
OSTaskStkInit ()
OSTaskCreate ()
OSTaskDelHook ()
OSTaskSwHook ()
OSTaskStatHook ()
OSTimeHook ()
```

真正需要的函数只有 `OSTaskStkInit()`。其他五个函数必须声明，但内部不需要包含任何代码。我没有在 `OS_CPU.C` 的这五个函数中放入任何代码，因为假设它们是由用户定义的。为此，定义常量 `OS_HOOKS_EN`（参见 `OS_CFG.H`）为 0。在 `OS_CPU.C` 中，你需要将 `OS_HOOKS_EN` 设置为 1。

### 9.05.01 `OS_CPU.C`, `OSTaskStkInit()`

此函数由 `OSTaskCreate()` 和 `OSTaskCreateExt()` 调用，以初始化任务栈，如果发生了中断且所有处理器寄存器都推入了该栈。图 9-7 显示 `OSTaskStkInit()` 将放在正在创建的任务上。注意，图没有显示调用 `OSTaskStkInit()` 代码的栈帧，而是正在创建的任务的栈帧。

# 低内存

Simulate PUSH DS
Simulate PUSH ES

| DS = Current DS |
| :--- |
| ES | 0x4444 |
| DI | 0x3333 |
| SI | 0x2222 |
| BP | 0x1111 |
| SP | 0x0000 |
| BX | 0xBBBB |
| DX | 0xDDDD |
| CX | 0xCCCC |
| AX | 0xAAAA |
| OFF task |
| SEG task |
| SW = 0x0202 |
| OFF task |
| SEG task |
| OFF pdata |
| SEG pdata |

栈顶

Simulate PUSHA

栈增长

Simulate Interrupt

ptos

Simulate call to task

# 高内存

# 图 9-7, 栈增长

状态字 `SW` 和任务地址被放在栈上。当你创建一个任务时，`OSTCreate()` 使用数据指定任务的起始位置。`OSTaskInit()` 需要额外的参数，但在 µC/OS-II 中它永远不能返回，因为这里的情况不明确。`SW` 初始化为 `0x202`。这将允许任务在启动时启用。你可以通过将 `SW` 设置为 `0x002` 在禁用中断的情况下启动所有任务。µC/OS-II 没有选项可以选择性地在某些任务启动时启用并在另一些任务启动时禁用中断。换句话说，所有任务都在禁用中断的情况下启动。

```c
void OSTaskkInit(void *task, void *pdata, void *ptos, uint16 opt);
```

### 9.9, `OSTaskkInit()`

`OSTaskkInit()` 的代码如下。

```c
void OSTaskkInit (void *task, void *pdata, void *ptos, uint16 opt)
{
    /* 保存任务栈帧 */
    PUSH        DS;
    PUSH        ES;
    PUSH        AX;
    PUSH        SI;
    PUSH        BP;
    PUSH        BX;
    PUSH        DX;
    PUSH        CX;
    PUSH        DI;
    /* 设置栈帧 */
    MOV         AX, task;
```
