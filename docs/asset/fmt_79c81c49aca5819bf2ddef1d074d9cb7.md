
```vhdl
082- oeb <= NOT(read); -- enable RAM drivers during RAM read operations

083- web <= NOT(write AND NOT(bufg_clock)); -- pulse write in last 1/2 of clock

-- address either the data or program sections of the external RAM
addr <= "1111111111" & curr_ir(3 DOWNTO 0) WHEN sel_data_ram='1' ELSE
"00000000" & curr_pc;

-- drive the accumulator into the RAM during write operations
-- but disable the drivers into high-impedance state at all other times
data <= "0000" & curr_acc WHEN write='1' ELSE "ZZZZZZZZ";

-- load the instruction register with a new opcode
next_ir <= data WHEN ld_ir='1' ELSE
-- or load only the lower 4 bits of the IR with new data
curr_ir(7 DOWNTO 4) & data(3 DOWNTO 0) WHEN ld_ir_lsn='1' ELSE
-- or else don't change the IR
curr_ir;

-- load the PC with an address to jump to
next_pc <= curr_ir(6 DOWNTO 0) WHEN jump_pc='1' ELSE
-- or increment the PC
curr_pc+1 WHEN inc_pc='1' ELSE
-- or else don't change the PC
curr_pc;

-- this process describes the operations of the ALU
PROCESS (alu_op,curr_zero,curr_carry,curr_acc,curr_ir,sum)
BEGIN
-- set the defaults for these signals to avoid synthesis of latches
sum <= "00000";
next_acc <= "0000";
next_carry <= '0';
next_zero <= '0';

CASE alu_op IS
WHEN ADD_OP =>
-- add acc with the lower 4 bits of the IR and the carry
sum <= ('0' & curr_acc) + ('0' & curr_ir(3 DOWNTO 0))
+ ("0000" & curr_carry);
next_acc <= sum(3 DOWNTO 0); -- ACC gets low 4 bits of sum
next_carry <= sum(4); -- carry is most sig bit of the sum
next_zero <= curr_zero; -- zero flag is not changed
WHEN XOR_OP =>
-- XOR the accumulator with the lower 4 bits of the IR
next_acc <= curr_acc XOR curr_ir(3 DOWNTO 0);
next_carry <= curr_carry; -- carry flag is not changed
next_zero <= curr_zero; -- zero flag is not changed
```
