# Listing 9.2  ABEL code for the GNOME microprocessor. (Cont’d.)

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

117- ELSE WHEN alu_op==PASS THEN
118-   { "pass data from the IR into the ACC but leave flags alone
119-     [acc3..acc0] := [ir3..ir0]; carry:=carry; zero:=zero;
120-   }

121- ELSE WHEN alu_op==AND THEN
122-   { "AND ACC and data from IR and update the zero flag
123-     zero := !(acc3&ir3 # acc2&ir2 # acc1&ir1 # acc0&ir0);
124-     [acc3..acc0] := [acc3..acc0];  "don't change the accumulator
125-     carry := carry;                         carry unaffected by AND operation
126-   }

127- ELSE WHEN alu_op==SET_CARRY THEN
128-   { "set carry flag to 1 but leave ACC and Z unchanged
```