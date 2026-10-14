# Listing 4.6 VHDL code for iteratively-instantiating a full adder component to create an 8-bit adder.

```
001- -- 8-bit Adder
002- -- page 98
003-
004- LIBRARY IEEE;
005- USE IEEE.std_logic_1164.ALL;
006- USE xse.adder.ALL;-- access the adder package in the XSE library
007-
008- -- byte-wide adder interface description
009- ENTITY byteadd IS
010- PORT (
011- a: IN STD_LOGIC_VECTOR (7 DOWNTO 0);-- addend byte
012- b: IN STD_LOGIC_VECTOR (7 DOWNTO 0);-- addend byte
013- cin: IN STD_LOGIC;-- carry input bit
014- sum: OUT STD_LOGIC_VECTOR (7 DOWNTO 0);-- sum byte
015- cout: OUT STD_LOGIC;-- carry output bit
016- );
017- END byteadd;
018-
019- -- 8-bit adder architecture (generated structural)
020- ARCHITECTURE byteadd_arch OF byteadd IS
021- -- local signal array to transfer carry bits between adder stages
022- SIGNAL c: STD_LOGIC_VECTOR (8 DOWNTO 0);
023- BEGIN
024- c(0)<=cin;-- initialize first carry signal to carry input value
025- -- for-loop will generate 8 full-adder bits and hook them together
026- lb10: FOR i IN 0 TO 7
027- GENERATE
028- lb1: fulladd PORT MAP
029- (-- connect the adder bit I/O to I/O of the 8-bit adder
030- input0=>a(i), -- addend inputs connected to i'th bit of the
031- input1=>b(i), -- a and b addend input arrays
032- carry_input=>c(i), -- carry input feeds i'th carry signal
033- sum=>sum(i), -- sum connects to the i'th sum output
034- carry_output=>c(i+1)-- carry output becomes the input
035- );-- to the next stage of the adder
036- END GENERATE;
037- cout<=c(8);-- last bit of carry array drives carry output
038- END byteadd_arch;
```

inputs to the fulladd module are a(0), b(0), c(0) (which was connected to the carry input on line 24), and the module's sum and carry outputs are connected to sum(0) and c(1), respectively. The c(1) array element connects the carry