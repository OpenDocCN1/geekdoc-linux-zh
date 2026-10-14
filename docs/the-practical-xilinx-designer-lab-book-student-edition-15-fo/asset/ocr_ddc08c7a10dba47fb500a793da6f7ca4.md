# Listing 6.12  VHDL code for using an XC9500 built-in D flip-flop with asynchronous clear.

```
001- -- Built-in D Flip-Flops
002-
003- LIBRARY IEEE;
004- USE IEEE.std_logic_1164.ALL;
005-
006- ENTITY bidff IS
007- PORT
008- (
009-   c: IN STD_LOGIC;       -- clock
010-   d: IN STD_LOGIC;       -- data
011-   aclr: IN STD_LOGIC;    -- active-low asynchronous clear
012-   q: OUT STD_LOGIC        -- stored data bit value
013- );
014- END bidff;
015-
016- ARCHITECTURE bidff_arch OF bidff IS
017-   COMPONENT FDPC PORT       -- interface to the built-in DFF
018-   (
019-     C: IN STD_LOGIC;
020-     CLR: IN STD_LOGIC;
021-     PRE: IN STD_LOGIC;
022-     D: IN STD_LOGIC;
023-     Q: OUT STD_LOGIC
024-   );
025-   END COMPONENT;
026-   SIGNAL aclr: STD_LOGIC;
027-   SIGNAL cb: STD_LOGIC;
028-   SIGNAL pre: STD_LOGIC;
029- BEGIN
030-   aclr <= NOT(aclr);       -- invert sense of clear
031-   cb <= NOT(c);            -- invert clock to falling edge
032-   pre <= '0';              -- disable preset
033-   u0: FDPC PORT MAP (C=>cb, D=>d, CLR=>aclr, PRE=>pre,
034-                      Q=>q);
035- END bidff_arch;
```