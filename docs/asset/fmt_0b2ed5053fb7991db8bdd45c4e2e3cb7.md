
### ADD 指令形式

- `ADD r16,i8`
- `ADD m16,i8`
- `ADD r32,i18` 386+
- `ADD m32,i18` 386+
- `ADD AL,i18`
- `ADD AX,i16`
- `ADD EAX,i32` 386+

### 示例

- `ADD BX,DI` ;使用单字节操作码
- `ADD AX,0FFFF` ;使用单字节操作码
- `ADD AL,42H`
- `ADD EAX,5`
- `ADD BP,17H`
- `AND DWORD [EDI],EAX`
- `ADD WORD [BX+SI+Inset],0B80`
- `ADD WORD:[BX],`

### 说明

`ADD` 将源操作数加到目标操作数，操作完成后，结果替换目标操作数。加法操作是算术加，不考虑进位标志。若要使用进位标志进行加法，请使用 `ADC` 进位加法指令。所有受影响的标志位都根据操作设置。最重要的是，如果结果无法放入目标操作数，进位标志将设置为 1。

```
r8 = AL AH BL CH CL DL DH             r16 = AX BX CX DX BP SP SI DI
s = CS DS SS ES FS GS               r32 = EAX EBX ECX EBP ESP EDI
m8 = 8-bit memory data             m16 = 16-bit memory data
m32 = 32-bit memory data             i8 = 8-bit immediate data
i16 = 16-bit immediate data          i32 = 32-bit immediate data
d8 = 8-bit signed displacement       d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```

### AND 逻辑与运算

受影响的标志位：

- `O`: 溢出标志 (`OF`)
- `D`: 方向标志 (`DF`)
- `I`: 中断标志 (`IF`)
- `T`: 陷阱标志 (`TF`)
- `S`: 符号标志 (`SF`)
- `Z`: 零标志 (`ZF`)
- `A`: 辅助进位标志 (`AF`)
- `P`: 奇偶标志 (`PF`)
- `C`: 进位标志 (`CF`)

注：原文中表格格式较乱，此处根据汇编标志位标准含义整理。`O D I T S Z A P C` 对应具体标志位定义。

### 逻辑形式

```
AND r8,r8
AND m8,r8
AND r8,m8
AND r16,r16
AND m16,r16
AND r16,m16
AND r32,r32 386+
AND m32,r32 386+
AND r32,m32 386+
AND r8,i8
AND m8,i8
AND r16,i16
AND m16,i16
AND r32,i32 386+
AND m32,i32 386+
AND AL,i8
AND AX,i16
AND EAX,i32 386+
```

### 示例

```
AND BX, DI
AND EAX, 5
AND AX, 00FF      ;使用单字节操作码
AND AL, 42H       ;使用单字节操作码
AND DWORD [EDI], EAX
AND WORD [BX], 0DB800H
AND WORD [BP+SI], DX
```

### 说明

`AND` 对其两个操作数执行 `AND` 运算。操作完成后，结果替换目标操作数。`AND` 是按位进行的，例如源的第 0 位与目标的第 0 位进行 `AND` 运算，源的第 1 位与目标的第 1 位进行 `AND` 运算，依此类推。如果两个操作数都为 1，则 `AND` 运算结果为 1；如果任一操作数为 0，则结果为 0。注意，操作会导致辅助进位（`AF`）未定义。进位标志（`CF`）清零，其他受影响的标志位根据操作设置。

```
r8 = AL AH BL CH DL
sr = CS DS SS ES FS GS
m8 = 8-bit memory data
m32 = 32-bit memory data
i16 = 16-bit immediate data
d8 = 8-bit signed displacement
d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
r16 = AX BX CX DX 
r32 = EAX EBX ECX EBP ESP
i8 = 8-bit immediate data
i32 = 32-bit immediate data
d16 = 16-bit displacement
```

### BT 测试 (386+)

受影响的标志位：

- `O`: 溢出标志 (`OF`)
- `D`: 方向标志 (`DF`)
- `I`: 中断标志 (`IF`)
- `T`: 陷阱标志 (`TF`)
- `S`: 符号标志 (`SF`)
- `A`: 辅助进位标志 (`AF`)
- `P`: 奇偶标志 (`PF`)
- `C`: 进位标志 (`CF`)
- `Z`: 零标志 (`ZF`)

### 合法形式

- `BT r16,r16` 386+
- `BT m16,r16` 386+
- `BT r32,r32` 386+
- `BT m32,r32` 386+
- `BT r16,i16` 386+
- `BT m16,i16` 386+
- `BT r32,i32` 386+
- `BT m32,i32` 386+

### 示例

- `BT AX,CX`
- `BT [BX-DI],DX`
- `BT AX,EAX`
- `BT EAX,ECX`

### 说明

`BT` 将左操作数中的一位复制到进位标志（`CF`），随后可以使用移位/旋转指令进行测试。复制哪一位由右操作数指定。`BT` 不改变任何操作数。当右操作数是 8 位立即数时，该值指定要复制的位数。如果立即数超过左操作数的大小，则该值对左操作数的大小取模。（这里，如果右操作数不是立即数，它指定左操作数中的偏移量。这较为复杂，请参见完整的汇编语言参考。）

```
r8 = AL AH BL CH DL          r16 = AX BX CX DX
sr = CS DS SS ES FS GS            r32 = EAX EBX ECX EBP ESP 
m8 = 8-bit memory data               m16 = 16-bit memory data
m32 = 32-bit memory data             i8 = 8-bit immediate data
i16 = 16-bit immediate data        i32 = 32-bit immediate data
d8 = 8-bit signed displacement      d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```

### CALL 调用过程

受影响的标志位：

- 无直接标志位影响（除了调用过程本身可能带来的副作用，但 `CALL` 指令本身不修改 `OF, DF, IF, TF, SF, PF, AF, ZF, CF`，尽管 `RET` 会恢复标志）。原文标注 `<无>`。

### 合法形式

```
CALL <near label>
CALL <far label>
CALL r16
CALL m16
CALL r32 386+
CALL m32 386+
```

### 示例

```
CALL InsideMySegment   ;InsideMySegment 是近标签
CALL OutsideMySegment ;OutsideMySegment 是远标签
CALL BX
CALL EDX
CALL WORD [BX+DI+1]   ;调用 [BX+DI+1] 处的近地址
CALL DWORD [BX+DI+1]  ;调用 [BX+DI+1] 处的32 位地址
```

### 说明

`CALL` 跳转到过程地址。在跳转之前，`CALL` 将自身之后的指令地址压栈。这允许 `RET` 指令（另见）将返回地址弹出到 `CS:IP` 或 `IP`（取决于是近调用还是远调用），从而返回到 `CALL` 指令之后的指令。

除了常见的定义的标签，`CALL` 还可以跳转到 16 位通用寄存器内的近地址，以及位于内存中的地址。这些在“合法形式”列中显示为 `m16` 和 `m32`。`CALL m16` 和 `CALL m32` 用于创建过程地址跳转表。

`CALL` 指令有很多变体，用于处理操作系统的保护机制。此处未涵盖这些内容，更多信息请参见高级或完整的汇编语言参考。

```
r8 = AL AH BH CH CL DH          r16 = AX BX CX DX BP SI
sr = CS DS SS ES FS GS            r32 = EAX EBX ECX EBP ESI EDI
m8 = 8-bit memory data               m16 = 16-bit memory data
m32 = 32-bit memory data             i8 = 8-bit immediate data
i16 = 16-bit immediate data        i32 = 32-bit immediate data
d8 = 8-bit signed displacement      d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```

### CLC 清零进位标志 (CF)

受影响的标志位：

- `C`: 进位标志 (`CF`) 被清零
- 其他标志位不变

### 汇编形式

```
CLC <无>
```

### 示例

```
CLC
```

### 说明

`CLC` 仅仅将进位标志（`CF`）设置为清零（0）状态。在工作开始前进位标志必须已知清零状态的情况下 `CLC`，例如在使用 `RCL` 和 `RCR` 指令旋转一系列字或字节时。它也可以在从过程返回之前将 `CF` 置于已知状态，以指示过程的成功或失败。

### CLD 清除方向标志 (DF)

影响的标志：

- `DF`: 方向标志 (`DF`) 被清零
- 其他标志位不变

合法格式：

```
CLD <none>
```

示例：

```
CLD
```

备注：

`CLD` 将方向标志 (`DF`) 设置为清除 (0)。这将影响重复字符串指令（如 `STOS`、`SCAS` 和 `MOVS`）执行的调整。通常，当 `DF = 0` 时，目标指针增加；当 `DF = 1` 时，减少。它通过 `STD` 指令设置为 1。

```
r8 = AL AH BL BH CL CH DL DH r16 = AX BX CX DX BP SP SI DI

sr = CS DS SS ES FS GS               r32 = EAX EBX ECX EBP ESP ESI EDI

m8 = 8位内存数据             m16 = 16位内存数据

m32 = 32位内存数据             i8 = 8位立即数

i16 = 16位立即数         i32 = 32位立即数

d8 = 8位符号位移     i16 = 16位符号位移

d32 = 32位无符号位移
```

### CMP 算术比较

影响的标志：

- `OF`, `DF`, `IF`, `TF`, `SF`, `ZF`, `AF`, `PF`, `CF`: 根据比较结果设置（类似于 `SUB` 但不存储结果）

合法格式：

- `CMP r8,r8`
- `CMP m8,r8`
- `CMP r8,m8`
- `CMP r16,r16`
- `CMP m16,r16`
- `CMP r16,m16`
- `CMP r32,r32` 386+
- `CMP m32,r32` 386+
- `CMP r32,m32` 386+
- `CMP r8,i8`
- `CMP m8,i8`
- `CMP r16,i16`
- `CMP m16,i16`
- `CMP r32,i32` 386+
- `CMP m32,i32` 386+
- `CMP r16,i8`
- `CMP m16,i8`
- `CMP r32,i8` 386+
- `CMP m32,i8` 386+
- `CMP AL,i8`
- `CMP AX,i16`
- `CMP EAX,i32` 386+

示例：

- `CMP BX, DI`
- `CMP EAX,5`
- `CMP AX,0FFFFH` ;使用单字节操作码
- `CMP AL,42H` ;使用单字节操作码
- `CMP BP,17H`
- `CMP WORD [BX+SI+Offset],5`
- `CMP WORD ES:[BX],08B00H`

备注：

`CMP` 比较两个操作数，并设置标志以指示比较结果。目标操作数不受影响。操作本身等于目标操作数减去源操作数且不借位（`SUB`），但结果不会替换目标。通常，`CMP` 后跟着一个条件跳转指令；例如，`JE` 在操作数相等时跳转；`JNE` 在不相等时跳转；以此此类推。

```
r8 = AL AH BL BH CL CH DL DH

r16 = AX BX CX DX BP SI DI

sr = CS DS SS ES ES FS GS

r32 = EAX EBX ECX EDX EBP ESP ESI EDI

m8 = 8位内存数据

m16 = 16位内存数据

m32 = 32位内存数据

i8 = 8位立即数

i16 = 16位立即数

i32 = 32位立即数

d8 = 8位符号位移

d16 = 16位符号位移

d32 = 32位无符号位移
```

### DEC 操作数递减

影响的标志：

- `OF`, `DF`, `IF`, `TF`, `SF`, `ZF`, `AF`, `PF`: 根据操作结果设置
- `CF`: 不受影响

合法格式：

- `DEC m8`
- `DEC m16`
- `DEC m32`
- `DEC r8`
- `DEC r16`
- `DEC r32`

示例：

- `DEC AL`
- `DEC CX`
- `DEC BYTE [BP]` ;递减 [BP] 处的字节
- `DEC WORD [BX]` ;递减 [BX] 处的字
- `DEC DWORD [EDX]` ;递减 [EDX] 处的双字

备注：

段寄存器不能用 `DEC` 递减。所有半寄存器（`r8`）操作码均为 2 字节，所有 16 位寄存器（`r16`）操作码均为 1 字节。如果你递减一个仅包含低位的寄存器，请使用 16 位操作码以节省字节。对于所有操作内存的指令，必须使用大小指定符，如 `BYTE`、`WORD` 和 `DWORD`。

```
r8 = AL AH BL BH CL CH DL DH

r16 = AX BX CX DX BP SI DI

sr = CS DS SS ES FS GS               r32 = EAX EBX ECX EBP ESI EDI

m8 = 8位内存数据                  m16 = 16位内存数据

m32 = 32位内存数据               i8 = 8位立即数

i16 = 16位立即数             i32 = 32位立即数

d8 = 8位符号位移        d16 = 16位符号位移

d32 = 32位无符号位移
```

### IMUL 有符号乘法

影响的标志：

- `OF`, `DF`, `IF`, `TF`, `SF`, `ZF`, `AF`, `PF`, `CF`: 根据操作结果设置

合法格式：

- `IMUL r8`
- `IMUL m8`
- `IMUL r16`
- `IMUL m16`
- `IMUL r32` 386+
- `IMUL i32` 386+
- `IMUL r16,i8` 286+
- `IMUL r16,i16` 286+
- `IMUL r32,i8` 386+
- `IMUL r32,i16` 386+
- `IMUL r32,i32` 386+
- `IMUL r16,m16` 286+
- `IMUL r16,i16` 286+
- `IMUL r16,i16` 386+
- `IMUL r32,r32` 386+
- `IMUL r32,m32` 386+
- `IMUL r32,i32` 386+

示例：

```
IMUL CH          ; AL * CH --> AX

IMUL BX          ; AX * BX --> DX:AX

IMUL ECX         ; EAX * ECX --> EDX:EAX

IMUL WORD [BX+DI]; DS * [BX+DI] --> DX:AX

IMUL EAX,ECX     ; EAX * ECX --> EAX

IMUL ECX,EAX,ECX ; EAX * ECX --> ECX
```

备注：

在最旧的单操作数格式（所有处理器上），`IMUL` 将其操作数与 `AL`、`AX` 或 `EAX` 相乘，结果放在 `AX`、`DX:AX` 或 `EDX:EAX`。如果给 `IMUL` 一个 8 位操作数（8 位寄存器或 8 位内存操作数），结果将放在 `AX`。这意味着即使结果完全位于 `AL`，`AH` 也会受到影响。同样，如果 `IMUL` 使用 16 位操作数，结果将放在 `DX:AX`，即使整个结果可以放入 `AX`！请记住 `IMUL` 在 16 位时影响 `DX`，32 位时影响 `EDX`。

在双三操作数格式中，结果替换第一个操作数的内容。在双操作数格式中，两个操作数相乘，结果替换第一个操作数。这与大多数算术和逻辑指令相似。在三操作数格式中，第二个和第三个操作数相乘，结果替换第一个操作数。

注意，对于双三操作数格式，结果可能无法完全放入目标寄存器。使用这些格式时，如果结果完全符合目标寄存器，`CF` 和 `OF` 标志都将置零（清除）。在不确定结果可能取值的范围内，最好使用原始格式。
