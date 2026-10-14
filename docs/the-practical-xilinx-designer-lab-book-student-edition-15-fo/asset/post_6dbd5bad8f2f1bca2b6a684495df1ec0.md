
## Listing 8.4: VHDL version of a 4-bit wide synchronous memory built from 4 register modules.

```
001- -- 4x4 synchronous memory
002-
003- LIBRARY IEEE, xse;
004- USE IEEE.STD_LOGIC_1164.ALL;
005- USE xse.led.ALL;          -- access the LED decoder module
006-
007- ENTITY mem2 IS
008- PORT
009- (
010- web: IN STD_LOGIC;       -- active-low write-enable
011- clk: IN STD_LOGIC;       -- master clock
012- a: IN STD_LOGIC_VECTOR (1 DOWNTO 0); -- 2-bit address bus
013- inp: IN STD_LOGIC_VECTOR (3 DOWNTO 0); -- 4-bit input bus
014- outp: BUFFER STD_LOGIC_VECTOR (3 DOWNTO 0); -- 4-bit output bus
015- s: OUT STD_LOGIC_VECTOR (6 DOWNTO 0) -- LED outputs
016- );
017- END mem2;
018-
019-
020- ARCHITECTURE mem2_arch OF mem2 IS
021-
022- -- components and signals for buffering clock
023- COMPONENT IBUF PORT(I: IN STD_LOGIC; O: OUT STD_LOGIC); END COMPONENT;
024- COMPONENT BUFG PORT(I: IN STD_LOGIC; O: OUT STD_LOGIC); END COMPONENT;
025- SIGNAL in_clk, buf_clk: STD_LOGIC;
026-
027- -- components/signals for bringing in the special-purpose mode pin signals
028- COMPONENT md0 PORT(MD0: OUT STD_LOGIC); END COMPONENT;
029- COMPONENT md2 PORT(MD2: OUT STD_LOGIC); END COMPONENT;
030- SIGNAL MD0in, MD0out, MD2out: STD_LOGIC;
031- SIGNAL inbus: STD_LOGIC_VECTOR (3 DOWNTO 0);
032-
033- -- signals for the individual 4-bit registers that are in the memory
034- SIGNAL rga: STD_LOGIC_VECTOR (3 DOWNTO 0); -- register a
035- SIGNAL rgb: STD_LOGIC_VECTOR (3 DOWNTO 0); -- register b
036- SIGNAL rgc: STD_LOGIC_VECTOR (3 DOWNTO 0); -- register c
037- SIGNAL rgd: STD_LOGIC_VECTOR (3 DOWNTO 0); -- register d
038- SIGNAL w: STD_LOGIC_VECTOR (3 DOWNTO 0); -- active-low write-enables
039- SIGNAL w0,w1,w2,w3: STD_LOGIC; -- individual active-low write-enables
040-
041- BEGIN
042-
043- u0: md0 PORT MAP(MD0=>MD0in);      -- connect the mode inputs to
044- u1: md2 PORT MAP(MD2=>MD2in);      -- the bus feeding the registers
045- u2: IBUF PORT MAP(I=>MD0in, O=>MD0out);
046- u3: IBUF PORT MAP(I=>MD2in, O=>MD2out);
047- inbus <= MD2out & MD0out & inp(1 DOWNTO 0); -- group signals into inbus
048-
049- w <= "1110" WHEN (a="00") AND (web='0') ELSE
050-       "1101" WHEN (a="01") AND (web='0') ELSE
051-       "1011" WHEN (a="10") AND (web='0') ELSE
052-       "0111" WHEN (a="11") AND (web='0') ELSE
053-       "1111";
054- w0 <= w(0);
055- w1 <= w(1);
056- w2 <= w(2);
057- w3 <= w(3);
058-
059- -- buffer the input clock
060- u4: IBUF PORT MAP(I=>clk, O=>in_clk);
061- u5: BUFG PORT MAP(I=>in_clk, O=>buf_clk);
062-
063- -- this process loads the selected reg on the rising clock edge
064- PROCESS (buf_clk,w0,w1,w2,w3,inp)
065- BEGIN
066- IF(buf_clk'EVENT AND buf_clk='1') THEN
067-   IF w0='0' THEN
068-     rga <= inbus;
069-   END IF;
070-   IF w1='0' THEN
071-     rgb <= inbus;
072-   END IF;
073-   IF w2='0' THEN
074-     rgc <= inbus;
075-   END IF;
076-   IF w3='0' THEN
077-     rgd <= inbus;
078-   END IF;
079- END IF;
080- END PROCESS;
081-
082- outp <= rga WHEN a="00" ELSE    -- select one of the four
083-         rgb WHEN a="01" ELSE    -- registers and output
084-         rgc WHEN a="10" ELSE    -- its value on the output bus
085-         rgd;
086-
087- -- display the output value on the LED display
088- u6: leddcd PORT MAP (d=>outp,s=>s);
089-
090- END mem2_arch;
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_304_0.png)

### Figure 8.20 Simulated waveforms for a synchronous memory.

Both the XS95 and XS40 Board implementations will work the same way. Some examples of the actions that can be performed with the synchronous memory are as follows:

| Action | XSPORT Command Sequence |
|---|---|
| Write location 1 (01) with 7 (0111) | XSPORT 01110100<br>XSPORT 01110101 |
| Write location 3 (11) with 10 (1010) | XSPORT 10101100<br>XSPORT 10101101 |
| Read location 0 (00) | XSPORT 0011 |
| Read location 2 (10) | XSPORT 1011 |

The MEM2 design uses 51 macrocells of an XC95108 CPLD. Since the LED decoder uses 7 macrocells, the 4×4 memory must use the other 51 − 7 = 44 macrocells. This is a large fraction of the total resources of the CPLD. Obviously, you cannot build a very large memory using the techniques shown in this or the previous section.

## Using Built-In Memory

To allow designers to use larger amounts of memory in their designs, the XC4000 series of FPGAs is equipped with internal RAMs. Since the LUTs in FPGAs are essentially RAMs which store the logic truth-tables (refer back to Figure 2.6), it is reasonable to allow the designer to use these RAMs for general-purpose data storage. Each CLB in an XC4000 FPGA has 2 LUTs that can be used as RAMs (Figure 2.7). Each 4-input LUT has room to store 2⁴=16 bits, so a single CLB can store 32 bits of data. The data can be organized as a 16×2 RAM, a 32×1 RAM, or dual 16×1 RAMs.
