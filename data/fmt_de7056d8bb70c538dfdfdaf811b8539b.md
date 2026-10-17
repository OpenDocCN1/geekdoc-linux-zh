
#### 列表 10.2 DWARF 指令解码器描述的 VHDL 版本。（续）

```vhdl
031-     drv_d_reg: OUT STD_LOGIC; -- 1 when D bus driven by register

032-     ld_reg: OUT STD_LOGIC; -- 1 when loading a register

033-     ROA: OUT STD_LOGIC; -- 1 forces A reg address to 0

034-     ROB: OUT STD_LOGIC; -- 1 forces B reg address to 0

035-     set_cry: OUT STD_LOGIC; -- 0=reset carry; 1=set carry

036-     alu_cry: OUT STD_LOGIC; -- 1 when ALU operation updates carry

037-     ld_cry: OUT STD_LOGIC; -- 1 when changing carry flag

038-     ld_z: OUT STD_LOGIC; -- 1 when changing zero flag

039-     add: OUT STD_LOGIC; -- 0=XOR; 1=ADD

040-     pass: OUT STD_LOGIC; -- 0=adder output; 1=operand passes thru

041-     ld_acc: OUT STD_LOGIC; -- 1 when changing accumulator

042-     set_iflag: OUT STD_LOGIC; -- 1 when setting interrupt flag

043-     clr_iflag: OUT STD_LOGIC; -- 1 when clearing interrupt flag

044-     clr_intrpt: OUT STD_LOGIC -- 1 when clearing interrupt flip-flop

045- );

046- END dwarf_vhdl;

047-

048- ARCHITECTURE dwarf_arch OF dwarf_vhdl IS

049- -- DWARF internal state

050- SIGNAL curr_st, next_st: STD_LOGIC_VECTOR (2 DOWNTO 0);

051-

052- -- DWARF control section states ----

053- CONSTANT R0: STD_LOGIC_VECTOR (2 DOWNTO 0) := "000";-- reset state 0

054- CONSTANT R1: STD_LOGIC_VECTOR (2 DOWNTO 0) := "001";-- reset state 1

055- CONSTANT T0: STD_LOGIC_VECTOR (2 DOWNTO 0) := "011";-- fetch state

056- CONSTANT T1: STD_LOGIC_VECTOR (2 DOWNTO 0) := "010";--

057- CONSTANT T2: STD_LOGIC_VECTOR (2 DOWNTO 0) := "110";--

058- CONSTANT T3: STD_LOGIC_VECTOR (2 DOWNTO 0) := "100";--

059- CONSTANT I1: STD_LOGIC_VECTOR (2 DOWNTO 0) := "111";-- interrupt state

060-

061- -- memory regions ----

062- CONSTANT PROGRAM: STD_LOGIC_VECTOR (1 DOWNTO 0) := "11"; -- program region

063- CONSTANT DATA: STD_LOGIC_VECTOR (1 DOWNTO 0) := "00"; -- data region

064- CONSTANT STACK: STD_LOGIC_VECTOR (1 DOWNTO 0) := "01"; -- stack region

065-

066- -- DWARF instruction opcodes ----

067- CONSTANT STORE_REG: STD_LOGIC_VECTOR (4 DOWNTO 0) := "00000";

068- CONSTANT STORE_INX: STD_LOGIC_VECTOR (4 DOWNTO 0) := "00001";

069- CONSTANT STORE_DIR: STD_LOGIC_VECTOR (4 DOWNTO 0) := "00010";

070- CONSTANT STORE_IND: STD_LOGIC_VECTOR (4 DOWNTO 0) := "00011";

071- CONSTANT LOAD_REG: STD_LOGIC_VECTOR (4 DOWNTO 0) := "00100";

072- CONSTANT LOAD_INX: STD_LOGIC_VECTOR (4 DOWNTO 0) := "00101";

073- CONSTANT LOAD_DIR: STD_LOGIC_VECTOR (4 DOWNTO 0) := "00110";

074- CONSTANT LOAD_IND: STD_LOGIC_VECTOR (4 DOWNTO 0) := "00111";

075- CONSTANT LOAD_IMM: STD_LOGIC_VECTOR (4 DOWNTO 0) := "01000";

076- CONSTANT IN_REG: STD_LOGIC_VECTOR (4 DOWNTO 0) := "01100";

077- CONSTANT OUT_OP: STD_LOGIC_VECTOR (4 DOWNTO 0) := "01101";

078- CONSTANT XOR_OP: STD_LOGIC_VECTOR (4 DOWNTO 0) := "10000";

079- CONSTANT ADD_OP: STD_LOGIC_VECTOR (4 DOWNTO 0) := "10001";

080- CONSTANT TEST: STD_LOGIC_VECTOR (4 DOWNTO 0) := "10010";

081- CONSTANT CLEAR_C: STD_LOGIC_VECTOR (4 DOWNTO 0) := "10100";

082- CONSTANT SET_C: STD_LOGIC_VECTOR (4 DOWNTO 0) := "10101";

083- CONSTANT JC: STD_LOGIC_VECTOR (4 DOWNTO 0) := "11000";

084- CONSTANT JZ: STD_LOGIC_VECTOR (4 DOWNTO 0) := "11001";

086- CONSTANT JUMP: STD_LOGIC_VECTOR (4 DOWNTO 0) := "1010";

087- CONSTANT JSR: STD_LOGIC_VECTOR (4 DOWNTO 0) := "1011";

088- CONSTANT RET: STD_LOGIC_VECTOR (4 DOWNTO 0) := "1100";

089- CONSTANT RETI: STD_LOGIC_VECTOR (4 DOWNTO 0) := "1101";

090-

091- BEGIN

092-

093- PROCESS(clock,curr_st,reset)

094- BEGIN

095- IF reset='1' THEN -- async reset to reset state

096- curr_st <= R0;

097- ELSIF (clock'event AND clock='1') THEN

098- curr_st <= next_st; -- go to next controller state on rising edge

099- END IF;

100- END PROCESS;

101-

102- PROCESS(curr_st,ir,carry,zero,iflag,intrpt)

103- BEGIN

104- -- set defaults of all control outputs to prevent latch synthesis

105- read<='0';

106- write <= '0';

107- addr_sel <= PROGRAM;

108- inc_pc <= '0';

109- ld_pc <= '0';

110- clr_pc <= '0';

111- inc_sp <= '0';
```
