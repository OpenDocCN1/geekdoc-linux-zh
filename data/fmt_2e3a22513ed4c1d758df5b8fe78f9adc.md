
## OSTaskkInit() 的代码如下

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
    MOV         [SP], AX;
    MOV         AX, pdata;
    MOV         [SP+2], AX;
    MOV         AX, ptos;
    MOV         [SP+4], AX;
    MOV         AX, opt;
    MOV         [SP+6], AX;
    /* 恢复寄存器 */
    POP         DI;
    POP         CX;
    POP         DX;
    POP         BX;
    POP         BP;
    POP         SI;
    POP         AX;
    POP         ES;
    POP         DS;
}
```

## OstickISR() 的代码参考

这段 `OstickISR()` 的代码在 9.7 中给出参考。

```asm
_OstickISR  PROC    FAR
;
    PUSH                        ; 保存中断任务的上下文
    PUSH                        ES
    PUSH                        DS
;
    MOV                         AX, SEG _OstickDOSCtr   ; 重载 DS
        DS, AX
;
    INC                         BYTE PTR DS:_OSIntesting  ; 通知 uC/OS-II 处于 ISR
;
    DEC                         BYTE PTR DS:_OstickDOSCtr
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
