
```
NET clock    LOC=P46;
NET reset    LOC=P47;
NET csb      LOC=P65;
NET web      LOC=P63;
NET oeb      LOC=P62;
NET data0    LOC=P44;
NET data1    LOC=P43;
NET data2    LOC=P41;
NET data3    LOC=P40;
NET data4    LOC=P39;
NET data5    LOC=P37;
NET data6    LOC=P36;
NET data7    LOC=P35;
NET addr0    LOC=P75;
```

#### 列表 9.2 GNOME 微处理器的 ABEL 代码。

```
001- MODULE GNOME1
002- TITLE 'GNOME microcontroller -- V1.0'
003-
004- DECLARATIONS
005- '---- external signals ----
006- clock        PIN;                 "GNOME is synchronous
007- reset        PIN;                 zeros the internal state
008- addr14..addr0 PIN ISTYPE 'COM';   "external RAM address bus
009- data7..data0 PIN ISTYPE 'COM';    "external RAM data bus
010- csb          PIN ISTYPE 'COM';    "external RAM chip select
011- web          PIN ISTYPE 'COM';    "external RAM write control
012- oeb          PIN ISTYPE 'COM';    "external RAM read control
013- s6..s0        PIN ISTYPE 'COM';    LED digit drivers
014- '---- internal storage elements ----
015- st1..st0      NODE ISTYPE 'REG';   "GNOME internal state
016- ir7..ir0     NODE ISTYPE 'REG';   "instruction register (IR)
017- pc6..pc0     NODE ISTYPE 'REG';   "program counter (PC)
018- acc3..acc0   NODE ISTYPE 'REG';   "accumulator (ACC)
019- carry        NODE ISTYPE 'REG';   "carry flag (C)
020- zero         NODE ISTYPE 'REG';   "zero flag (Z)
021- '---- internal signals ----
022- read         NODE ISTYPE 'COM';   "1 when reading RAM
023- write        NODE ISTYPE 'COM';   "1 when writing RAM
024- sel_data_ram NODE ISTYPE 'COM';   "1 when accessing RO-R15
025- jump_pc      NODE ISTYPE 'COM';   "1 when overwriting PC
026- inc_pc       NODE ISTYPE 'COM';   "1 when incrementing PC
027- ld_ir        NODE ISTYPE 'COM';   "1 when loading IR
028- ld_ir_lsn    NODE ISTYPE 'COM';   "1 when loading LSN of IR
029- aop2..aop0   NODE ISTYPE 'COM';   "ALU operation code
030- '---- synonyms for various items ----
031- ir   = [ir7..ir0];
032- pc   = [pc6..pc0];
033- address = [addr14..addr0];
034- data = [data7..data0];
035- acc = [acc3..acc0];
036- '---- ALU operation codes ----
037- alu_op = [aop2..aop0];
038- PASS = 'b001'; "ALU passes input to output
039- ADD  = 'b010'; "ALU adds inputs
040- XOR  = 'b011'; "ALU exclusive-ORs inputs
041- AND  = 'b100'; "ALU logically ANDs inputs
042- SET_CARRY = 'b101'; "carry flag is set
```

#### 列表 9.2 GNOME 微处理器的 ABEL 代码 for the GNOME microprocessor. (续)

```
086- "address either the data or program sections of the external RAM
087- WHEN sel_data_ram THEN address:=[1,1,1,1,1,1,1,1,1,1,ir3..ir0];
088- ELSE                         address:=[0,0,0,0,0,0,0,pc6..pc0];
089- ELSE
090- data_0E := write;                         "drive RAM data bus during write ops
091- data := [0,0,0,acc3..acc0];                 "with the value in the accumulator
093- WHEN    ld_ir    THEN ir := data.PIN;       "IR<=opcode from RAM
094- ELSE WHEN ld_ir_lsn THEN
095-   { "load the lower 4 bits of IR with RAM data...
096-     [ir3..ir0] := [data3..data0].PIN
097-     [ir7..ir4] := [ir7..ir4]                "but keep the upper 4-bits of IR
098-   }
099- ELSE if ir := ir;                          "IR unchanged
101- WHEN    jmp_pc THEN pc := [ir6..ir0];       "PC<=address from opcode
102- ELSE WHEN inc_pc THEN pc := pc+1;           "increment PC
103- ELSE                  pc := pc;             "PC unchanged
105- "ALU operations
106- WHEN alu_op==ADD THEN
107-   { "add ACC, data from IR, and C and update ACC and C
108-     [carry,acc3..acc0] := [0,acc3..acc0] + [0,ir3..ir0] +
109-                            [0,0,0,0,carry];
110-     zero := zero;  "zero flag is unaffected by add operations
111-   }
112- ELSE WHEN alu_op==XOR THEN
113-   { "XOR ACC and data from IR and update the ACC but not the flags
114-     [acc3..acc0] := [acc3..acc0] $ [ir3..ir0];
115-     carry:=carry;  zero:=zero;  "flags unaffected by XOR operation
116-   }
```
