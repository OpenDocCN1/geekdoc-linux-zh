```
BL __2printf
LDR RI, [SP,#0x38+var_30]
ADR R0, aHourD ; "Hour: %d\n"
BL __2printf
LDR RI, [SP,#0x38+var_34]
ADR R0, aMinutesD ; "Minutes: %d\n"
BL __2printf
LDR RI, [SP,#0x38+var_38]
ADR R0, aSecondsD ; "Seconds: %d\n"
BL __2printf
ADD SP, SP, #0x34
POP [PC]
```

# Optimizing Xcode 4.6.3 (LLVM) (Thumb-2 mode)

通过分析调用函数的函数名称（例如本例的localtime_r 函数）。IDA能够“识别”返回值为结构体数据，并能够结构体中的字段重新标注名称。

指令清单21.10 Optimizing Xcode 4.6.3 (LLVM) (Thumb-2 mode)

```
var_38 = -0x38
var_34 = -0x34

PUSH [R7,LR]
MOV R7, SP
SUB SP, SP, #0x30
MO R0, #0 ; time t *
BLX _time
ADD R1, [SP,#0x38+var_34] ; struct tm *
STR R0, [SP,#0x38+var_38]
MOV R0, SP ; time t *
BLX _localtime_r
LDR R1, [SP,#0x38+var_34.tm_year]
MOV R0, 0xF44 ; "Year: %d\n"
ADD R0, PC ; char *
ADDW R1, R1, #0x76C
BLX _printf
LDR R1, [SP,#0x38+var_34.tm_mon]
MOV R0, 0x0F3A ; "Month: %d\n"
ADD R0, PC ; char *
BLX _printf
LDR R1, [SP,#0x38+var_34.tm_mday]
MOV R0, 0x0F35 ; "Day: %d\n"
ADD R0, PC ; char *
BLX _printf
LDR R1, [SP,#0x38+var_34.tm_hour]
MOV R0, 0x0F2E ; "Hour: %d\n"
ADD R0, PC ; char *
BLX _printf
LDR R1, [SP,#0x38+var_34.tm_min]
```