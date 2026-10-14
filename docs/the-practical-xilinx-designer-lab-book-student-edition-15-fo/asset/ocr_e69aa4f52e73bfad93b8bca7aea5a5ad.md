# Listing 10.1 The ABEL version of the DWARF instruction decoder description. (Cont'd.)

```
131-    ld_pc=1; inc_pc=1; "increment PC to next instruction
132-    }
133-    (ir==RET) : T2 WITH
134-    { decrement stack pointer to point at return address
135-        ld_sp=1; inc_sp=0; "decrement stack pointer
136-    }
137-    (ir==RETI) : T2 WITH
138-    { decrement the stack pointer to point at the stored ACC
139-        ld_sp=1; inc_sp=0; "decrement stack pointer
140-    }
141-    (ir==JUMP) : TO WITH
142-    {
143-        addr_sel=PROGRAM; read=1; "read jump address from RAM
144-        drv_d_data=1; ld_pc=1;    "load it into program counter
145-    }
146-    ((ir==JC) & carry) : TO WITH
147-    { if carry flag is set, load PC with the jump address
148-        addr_sel=PROGRAM; read=1; "read jump address from RAM
149-        drv_d_data=1; ld_pc=1;    "load it into program counter
150-    }
151-    ((ir==JC) & !carry) : TO WITH
152-    { otherwise, step over the jump address to the next instr.
153-        ld_pc=1; inc_pc=1;
154-    }
155-    ((ir==JZ) & zero) : TO WITH
156-    { if zero flag is set, load PC with the jump address
157-        addr_sel=PROGRAM; read=1; "read jump address from RAM
158-        drv_d_data=1; ld_pc=1;    "load it into program counter
159-    }
160-    ((ir==JZ) & !zero) : TO WITH
161-    { otherwise, step over the jump address to the next instr.
162-        ld_pc=1; inc_pc=1;
163-    }
164-    (ir==LOAD_REG) : TO WITH
165-    { load ACC with data from a register
166-        pass=1; ld_acc=1; "load ACC with data from register
167-    }
168-    (ir==LOAD_INX) : TO WITH
169-    { load ACC with data whose memory address is in register
170-        addr_sel=DATA; read=1; "address memory with register value
171-        drv_d_data=1; pass=1; ld_acc=1; "store RAM data into ACC
172-    }
```