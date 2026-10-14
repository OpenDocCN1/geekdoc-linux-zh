# Listing 9.2 ABEL code for the GNOME microprocessor. (Cont’d.)

```
171- (ir==CLEAR_C) : FETCH WITH alu_op = CLR_CARRY;
172- (ir==SET_C) : FETCH WITH alu_op = SET_CARRY;
173- (ir==SKIP_C) : FETCH WITH WHEN carry THEN inc_pc = 1;
174- (ir==SKIP_Z) : FETCH WITH WHEN zero THEN inc_pc = 1;
175- (ir==LOAD_IMM) : FETCH WITH alu_op = PASS;
176- (ir==ADD_IMM) : FETCH WITH alu_op = ADD;
177- (ir==JUMP) : FETCH WITH jump_pc = 1;
178- (ir==STORE_DIR) : FETCH WITH {sel_data_ram; write=1;}
179- (ir==LOAD_DIR) : FETCH WITH alu_op = PASS;
180- (ir==ADD_DIR) : FETCH WITH alu_op = ADD;
181- (ir==XOR_DIR) : FETCH WITH alu_op = XOR;
182- (ir==TEST_DIR) : FETCH WITH alu_op = AND;
183- endcase;
184-
185- TRUTH_TABLE "LED displays the value in the accumulator"
186- (acc -> {s6, s5, s4, s3, s2, s1, s0})
187- 0 -> [1, 1, 1, 0, 1, 1, 1];
188- 1 -> [0, 0, 1, 0, 0, 1, 0];
189- 2 -> [1, 0, 1, 1, 1, 0, 1];
190- 3 -> [0, 1, 0, 1, 0, 1, 1];
191- 4 -> [1, 1, 1, 0, 1, 0, 1];
192- 5 -> [1, 1, 0, 1, 0, 1, 1];
193- 6 -> [1, 1, 0, 1, 1, 1, 1];
194- 7 -> [1, 0, 1, 0, 0, 1, 0];
195- 8 -> [1, 1, 1, 1, 1, 1, 1];
196- 9 -> [1, 1, 1, 1, 0, 1, 1];
197- 10-> [1, 1, 1, 1, 1, 1, 0];
198- 11-> [0, 1, 0, 1, 1, 1, 1];
199- 12-> [1, 1, 0, 0, 1, 0, 1];
200- 13-> [0, 0, 1, 1, 1, 1, 1];
201- 14-> [1, 1, 0, 1, 1, 0, 1];
202- 15-> [1, 1, 0, 1, 1, 0, 0];
203-
204- END GNOME1
```

NET addr1 LOC=P79;
NET addr2 LOC=P82;
NET addr3 LOC=P84;
NET addr4 LOC=P1;
NET addr5 LOC=P3;
NET addr6 LOC=P83;
NET addr7 LOC=P2;
NET addr8 LOC=P56;