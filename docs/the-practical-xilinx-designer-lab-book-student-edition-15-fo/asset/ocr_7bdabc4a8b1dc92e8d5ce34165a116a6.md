# Listing 10.1 The ABEL version of the DWARF instruction decoder description. (Cont'd.)

```
044- "..... synonyms for various items .....
045- ir = [ir7..ir0];
046- addr_sel = [addr_sel1..addr_sel0];
047- "..... DWARF control section states .....
048- controller_state = [st2..st0];
049- RO,R1 = 'b000','b001';
050- TO,T1,T2,T3 = 'b011','b010','b110','b100'; "normal instruction states
051- I1 = 'b111'; "interrupt handling state
052- "..... memory regions .....
053- PROGRAM = 'b11'; "memory region for program opcodes & operands
054- DATA = '^b00'; "memory region for data values
055- STACK = 'b01'; "memory region for stack
056- X = .X.; "synonym for DON'T-CARE
057- "..... DWARF instruction opcodes .....
058- STORE_REG = [0,0,0,0,X,X,X];
059- STORE_INX = [0,0,0,0,1,X,X];
060- STORE_DIR = [0,0,0,1,0,X,X];
061- STORE_IND = [0,0,0,1,1,X,X];
062- LOAD_REG = [0,0,1,0,0,X,X];
063- LOAD_INX = [0,0,1,0,1,X,X];
064- LOAD_DIR = [0,0,1,1,0,X,X];
065- LOAD_IND = [0,0,1,1,1,X,X];
066- LOAD_IMM = [0,1,1,0,0,X,X];
067- IN_REG = [0,1,1,0,0,X,X];
068- OUT = [0,1,1,0,1,X,X];
069- XOR = [1,0,0,0,0,X,X];
070- ADD = [1,0,0,0,1,X,X];
071- TEST = [1,0,0,1,0,X,X];
072- CLEAR_C = [1,0,1,0,0,X,X];
073- SET_C = [1,0,1,1,0,X,X];
074- JC = [1,1,0,0,0,X,X];
075- JZ = [1,1,0,0,1,X,X];
076- JUMP = [1,1,0,1,0,X,X];
077- JSR = [1,1,0,1,1,X,X];
078- RET = [1,1,1,0,0,X,X];
079- RETI = [1,1,1,0,1,X,X];
080-
081- EQUATIONS
082-
083- controller_state.CLK = clock; "synchronously clock state machine
084- controller_state.ACLR = reset; "reset state machine
085-
```