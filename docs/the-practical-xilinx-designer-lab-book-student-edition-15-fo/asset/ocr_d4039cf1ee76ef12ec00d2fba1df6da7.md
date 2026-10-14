# Listing 4.7  8-bit adder VHDL code modified to get an input through the MD0 pin of the XC4005XL FPGA.

```
```vhdl
001-- 8-bit Adder
002-
003- LIBRARY IEEE,xse;
004- USE TEE.std_logic_1164.ALL;
005- USE xse.adder.ALL;
006-
007- -- byte-wide adder interface description
008- ENTITY byteadd IS
009- PORT (
010- a: IN STD_LOGIC_VECTOR (7 DOWNTO 0);-- adder byte
011- b: IN STD_LOGIC_VECTOR (7 DOWNTO 0);-- adder byte
012- cin: IN STD_LOGIC;-- carry input
013- sum: OUT STD_LOGIC_VECTOR (7 DOWNTO 0);-- sum byte
014- cout: OUT STD_LOGIC;-- carry output
015- );
016- END byteadd;
017-
018- -- 8-bit adder architecture (generated structural)
019- ARCHITECTURE byteadd_arch OF byteadd IS
020- -- local signal arrays
021- SIGNAL a: STD_LOGIC_VECTOR (8 DOWNTO 0);
022- SIGNAL bib: STD_LOGIC_VECTOR (7 DOWNTO 0); -- intermediate bus
023- SIGNAL tmp: STD_LOGIC;
024- COMPONENT MDO PORT(MD0: OUT std_logic); END COMPONENT;
025- COMPONENT IBUF PORT(I: IN std_logic; O: OUT std_logic); END COMPONENT;
026- END COMPONENT;
027- BEGIN
028- bib(7 DOWNTO 3) <= b(7 DOWNTO 3);
029- bib(1 DOWNTO 0) <= b(1 DOWNTO 0);
030- u0: MDO PORT MAP(MD0=>tmp);-- connect MD0 input to tmp
031- u1: IBUF PORT MAP(I=>tmp, O=>bib(2)); -- tmp to intermediate bus
032- c(0)<=cin;
033- -- for-loop will generate 8 full-adder bits and hook them together
034- lbl0: FOR i IN 0 TO 7
035- GENERATE
036- lbl1: fulladd PORT MAP
037- (
```
```