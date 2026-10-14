

## 第9.3节 GNOME 微处理器的 VHDL 代码

```vhdl
044-
045- -- control signals
046- SIGNAL read: STD_LOGIC;                 -- 1 when reading RAM
047- SIGNAL write: STD_LOGIC;                -- 1 when writing RAM
048- SIGNAL sel_data_ram: STD_LOGIC;         -- 1 when accessing R0-R15
049- SIGNAL jump_pc: STD_LOGIC;              -- 1 when overwriting PC
050- SIGNAL inc_pc: STD_LOGIC;               -- 1 when incrementing PC
051- SIGNAL ld_ir: STD_LOGIC;                -- 1 when loading IR
052- SIGNAL ld_ir_lsn: STD_LOGIC;            -- 1 when loading LSN of IR
053- SIGNAL sum: STD_LOGIC_VECTOR (4 DOWNTO 0);  -- for adder output
054- SIGNAL alu_op: STD_LOGIC_VECTOR (2 DOWNTO 0); -- ALU operation code
055-
056- -- possible ALU opcodes
057- CONSTANT PASS_OP: STD_LOGIC_VECTOR (2 DOWNTO 0) := "001"; -- in to out
058- CONSTANT ADD_OP: STD_LOGIC_VECTOR (2 DOWNTO 0) := "010"; -- add inputs
059- CONSTANT XOR_OP: STD_LOGIC_VECTOR (2 DOWNTO 0) := "011"; -- XOR inputs
060- CONSTANT AND_OP: STD_LOGIC_VECTOR (2 DOWNTO 0) := "100"; -- test input=0
061- CONSTANT SET_CARRY_OP: STD_LOGIC_VECTOR (2 DOWNTO 0) := "101"; -- set C
062- CONSTANT CLR_CARRY_OP: STD_LOGIC_VECTOR (2 DOWNTO 0) := "110"; -- clear C
063-
064- -- possible instruction opcodes
065- CONSTANT CLEAR_C: STD_LOGIC_VECTOR (7 DOWNTO 0) := "00000000";
066- CONSTANT SET_C:   STD_LOGIC_VECTOR (7 DOWNTO 0) := "00000001";
067- CONSTANT SKIP_C:  STD_LOGIC_VECTOR (7 DOWNTO 0) := "00000010";
068- CONSTANT SKIP_Z:  STD_LOGIC_VECTOR (7 DOWNTO 0) := "00000011";
069- CONSTANT LOAD_IMM: STD_LOGIC_VECTOR (3 DOWNTO 0) := "0001";
070- CONSTANT ADD_IMM: STD_LOGIC_VECTOR (3 DOWNTO 0) := "0010";
071- CONSTANT STORE_DIR:STD_LOGIC_VECTOR (3 DOWNTO 0) := "0011";
072- CONSTANT LOAD_DIR: STD_LOGIC_VECTOR (3 DOWNTO 0) := "0100";
073- CONSTANT ADD_DIR: STD_LOGIC_VECTOR (3 DOWNTO 0) := "0101";
074- CONSTANT XOR_DIR: STD_LOGIC_VECTOR (3 DOWNTO 0) := "0110";
075- CONSTANT TEST_DIR: STD_LOGIC_VECTOR (3 DOWNTO 0) := "0111";
076- CONSTANT JUMP:    STD_LOGIC                := '1';
077-
078- BEGIN
079-
080- -- external RAM control signals
081- csb <= '0'; -- always keep the RAM selected
082- oeb <= NOT(read); -- enable RAM drivers during RAM read operations
083- web <= NOT(write AND NOT(bufg_clock)); -- pulse write in last 1/2 of clock
084-
085- -- address either the data or program sections of the external RAM
086- addr <= "1111111111" & curr_ir(3 DOWNTO 0) WHEN sel_data_ram='1' ELSE
087- "00000000" & curr_pc;
088-
089- -- drive the accumulator into the RAM during write operations
090- -- but disable the drivers into high-impedance state at all other times
091- data <= "0000" & curr_acc WHEN write='1' ELSE "ZZZZZZZZ";
092-
093- -- load the instruction register with a new opcode
094- next_ir <= data WHEN ld_ir='1' ELSE
095- -- or load only the lower 4 bits of the IR with new data
096- curr_ir(7 DOWNTO 4) & data(3 DOWNTO 0) WHEN ld_ir_lsn='1' ELSE
097- -- or else don't change the IR
098- curr_ir;
099-
100- -- load the PC with an address to jump to
101- next_pc <= curr_ir(6 DOWNTO 0) WHEN jump_pc='1' ELSE
102- -- or increment the PC
103- curr_pc+1 WHEN inc_pc='1' ELSE
104- -- or else don't change the PC
105- curr_pc;
106-
107- -- this process describes the operations of the ALU
108- PROCESS (alu_op,curr_zero,curr_carry,curr_acc,curr_ir,sum)
109- BEGIN
110- -- set the defaults for these signals to avoid synthesis of latches
111- sum <= "00000";
112- next_acc <= "0000";
113- next_carry <= '0';
114- next_zero <= '0';
115-
116- CASE alu_op IS
117- WHEN ADD_OP =>
118- -- add acc with the lower 4 bits of the IR and the carry
119- sum <= ('0' & curr_acc) + ('0' & curr_ir(3 DOWNTO 0))
120- + ("0000" & curr_carry);
121- next_acc <= sum(3 DOWNTO 0); -- ACC gets low 4 bits of sum
122- next_carry <= sum(4); -- carry is most sig bit of the sum
123- next_zero <= curr_zero; -- zero flag is not changed
124- WHEN XOR_OP =>
125- -- XOR the accumulator with the lower 4 bits of the IR
126- next_acc <= curr_acc XOR curr_ir(3 DOWNTO 0);
127- next_carry <= curr_carry; -- carry flag is not changed
128- next_zero <= curr_zero; -- zero flag is not changed
```
