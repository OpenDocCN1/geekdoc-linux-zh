
129- WHEN PASS_OP =>
130-     -- 将 IR 的低 4 位传递到 ACC
131-     next_acc <= curr_ir(3 DOWNTO 0);
132-     next_carry <= curr_carry;-- 标志位未改变
133-     next_zero <= curr_zero;-- 零标志位未改变
134- WHEN AND_OP =>
135-     -- 测试未屏蔽位位置中 ACC 的零值
136-     next_acc <= curr_acc;-- ACC 未改变
137-     next_carry <= curr_carry;-- 进位未改变
138-     -- 如果 ACC 在 IR 为 1 的位置上有零，则置零标志
139-     next_zero <= NOT( (curr_acc(3) AND curr_ir(3))
140-                     OR (curr_acc(2) AND curr_ir(2))
141-                     OR (curr_acc(1) AND curr_ir(1))
142-                     OR (curr_acc(0) AND curr_ir(0)));
143- WHEN SET_CARRY_OP =>
144-     -- 置位进位位
145-     next_acc <= curr_acc;-- ACC 未改变
146-     next_carry <= '1';-- 置位进位位
147-     next_zero <= curr_zero;-- 零标志位未改变
148- WHEN CLR_CARRY_OP =>
149-     -- 清除进位位
150-     next_acc <= curr_acc;-- ACC 未改变
151-     next_carry <= '0';-- 清除进位位
152-     next_zero <= curr_zero;-- 零标志位未改变
153- WHEN OTHERS =>
154-     -- 对未定义的 ALU 操作码不执行任何操作
155-     next_acc <= curr_acc;
156-     next_carry <= curr_carry;
157-     next_zero <= curr_zero;
158- END CASE;
159- END PROCESS;
160- 
161- -- 该进程描述 GNOME 状态机的转换
162- -- 并设置在每个状态中激活的控制信号
163- PROCESS(curr_st,curr_carry,curr_zero,curr_ir)
164- BEGIN
165-     -- 将这些信号的默认值设置为避免综合出锁存器
166-     sel_data_ram <= '0';
167-     read <= '0';
168-     write <= '0';
169-     ld_ir <= '0';
170-     ld_ir_lsn <= '0';
171-     inc_pc <= '0';
172- jump_pc <= '0';
173- alu_op <= "000";
174- next_st <= FETCH;
175- CASE curr_st IS
176-     WHEN FETCH => -- 从外部 RAM 获取指令
177-         sel_data_ram <= '0'; -- 选择指令 RAM
178-         read <= '1'; -- 从 RAM 读取
179-         ld_ir <= '1'; -- 用新操作码加载指令寄存器
180-         inc_pc <= '1'; -- 将 PC 递增到下一条指令
181-         next_st <= DECODE; -- 然后解码新操作码
182-     WHEN DECODE =>
183-         -- 解码指令。实际上，此状态用于
184-         -- 从外部 RAM 的数据区读取直接寻址操作数并将其存储在 IR 的低 4 位中。
185-         IF curr_ir(7 DOWNTO 4)=LOAD_DIR THEN
186-             sel_data_ram <= '1'; -- 选择数据 RAM
187-             read <= '1'; -- 使能 RAM 读取
188-             ld_ir_lsn <= '1'; -- 加载 IR 的低 4 位
189-         END IF;
190-         IF curr_ir(7 DOWNTO 4)=ADD_DIR THEN
191-             sel_data_ram <= '1';
192-             read <= '1';
193-             ld_ir_lsn <= '1';
194-         END IF;
195-         IF curr_ir(7 DOWNTO 4)=XOR_DIR THEN
196-             sel_data_ram <= '1';
197-             read <= '1';
198-             ld_ir_lsn <= '1';
199-         END IF;
200-         IF curr_ir(7 DOWNTO 4)=TEST_DIR THEN
201-             sel_data_ram <= '1';
202-             read <= '1';
203-             ld_ir_lsn <= '1';
204-         END IF;
205-         next_st <= EXECUTE; -- 然后执行指令
206-     WHEN EXECUTE => -- 执行指令。
207-         IF curr_ir=CLEAR_C THEN
208-             alu_op <= CLR_CARRY_OP; -- 清除进位标志
209-         END IF;
210-         IF curr_ir=SET_C THEN
211-             alu_op <= SET_CARRY_OP; -- 置位进位标志
212-         END IF;
213-         IF curr_ir=SKIP_C THEN -- 跳过下一条指令
214-          inc_pc <= curr_carry; -- 如果进位标志被置位
215-          END IF;
216-          IF curr_ir=SKIP_Z THEN  -- 跳过下一条指令
217-              inc_pc <= curr_zero; -- 如果零标志被置位
218-          END IF;
219-          IF curr_ir(7 DOWNTO 4)=LOAD_IMM THEN -- 用立即数加载 ACC
220-              alu_op <= PASS_OP; -- 来自 IR 低 4 位的数据
221-          END IF;
222-          IF curr_ir(7 DOWNTO 4)=ADD_IMM THEN -- 将低 4 位的
223-              alu_op <= ADD_OP;     -- IR 加到 ACC
224-          END IF;
225-          IF curr_ir(7)=JUMP THEN-- 跳转到 IR
226-              jump_pc <= '1';-- 低 7 位中的地址
227-          END IF;
228-          IF curr_ir(7 DOWNTO 4)=STORE_DIR THEN -- 将 ACC 写入 RAM
229-              sel_data_ram <= '1';
230-              write <= '1';
231-          END IF;
232-          IF curr_ir(7 DOWNTO 4)=LOAD_DIR THEN -- 用从 RAM 读取的数据加载 ACC
233-              alu_op <= PASS_OP;-- 
234-          END IF;
235-          IF curr_ir(7 DOWNTO 4)=ADD_DIR THEN -- 将 RAM 数据
236-              alu_op <= ADD_OP;     -- 加到 ACC
237-          END IF;
238-          IF curr_ir(7 DOWNTO 4)=XOR_DIR THEN -- 将 RAM 数据与 ACC
239-              alu_op <= XOR_OP;     -- 进行异或
240-          END IF;
241-          IF curr_ir(7 DOWNTO 4)=TEST_DIR THEN -- 用从 RAM 读取的数据屏蔽 ACC
242-              alu_op <= AND_OP;     -- 并在所有位 =0 时置位
243-          END IF;               -- 零标志
244-          next_st <= FETCH;-- 执行完成，所以去取指
245-      WHEN OTHERS =>
246-  END CASE;
247- END PROCESS;
248-
249- -- 生成低偏斜时钟信号
250- buf1: IBUF PORT MAP(I=>clock, O=>buf_clock);
251- buf2: BUFG PORT MAP(I=>buf_clock, O=>bufg_clock);
252-
253- -- 该进程在时钟上升沿更新所有这些信号
254- PROCESS (bufg_clock,reset)
255- BEGIN
256- -- 异步复位 GNOME 微型计算机的状态
## Listing 9.3 VHDL code for the GNOME microprocessor. (Cont’d.)
