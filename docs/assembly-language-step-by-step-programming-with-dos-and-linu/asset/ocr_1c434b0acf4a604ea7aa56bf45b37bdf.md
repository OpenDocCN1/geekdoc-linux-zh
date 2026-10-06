# # IMUL Signed Integer Multiplication

# ## Flags affected:

```
O D I T S Z A P C  OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
*               IF: Interrupt flag ZF: Zero flag CF: Carry flag
```

# ## Legal forms:

```
IMUL r8
IMUL m8
IMUL r16
IMUL m16
IMUL r32        386+
IMUL i32         386+
IMUL r16,i8      286+
IMUL r16,i16     286+
IMUL r32,i8      386+
IMUL r32,i16     386+
IMUL r16,r16     386+
IMUL r16,m16     386+
IMUL r32,r32     386+
IMUL r32,m32     386+
IMUL r16,r18     286+
IMUL r16,m18     286+
IMUL r16,r16,i16 286+
IMUL r16,m16,i16 286+
IMUL r32,r32     386+
IMUL r32,m32     386+
IMUL r32,r32,i32 386+
IMUL r32,m32,i32 386+
```

# ## Examples:

```
IMUL CH          ; AL * CH --> AX
IMUL BX          ; AX * BX --> DX:AX
IMUL ECX         ; EAX * ECX --> EDX:EAX
IMUL WORD [BX+DI]; DS * [BX+DI] --> DX:AX
IMUL EAX,ECX     ; EAX * ECX --> EAX
IMUL ECX,EAX, 15 ; EAX * 15 --> ECX
```

# ## Notes:

In its oldest, single-operand form (on all processors), IMUL multiplies its operand by AL, AX, or EAX, and the result is placed in AX, in DX:AX, or in EDX:EAX. If IMUL is given an 8-bit operand (either an 8-bit register or an 8-bit memory operand), the results will be placed in AX. This means that AH will be affected, even if the results fit entirely in AL.