
## Listing 6.15 VHDL code for a 3-bit counter built from toggle flip-flops.

```
001- -- Toggle Flip-Flop Counter
002-
003- LIBRARY IEEE;
004- USE IEEE.std_logic_1164.ALL;
005-
006- ENTITY tglcnt IS
007- PORT
008- (
009- c: IN STD_LOGIC; -- clock
010- aclr: IN STD_LOGIC; -- asynchronous active-high clear
011- t0: BUFFER STD_LOGIC; -- counter bit 0
012- t1: BUFFER STD_LOGIC; -- counter bit 1
013- t2: BUFFER STD_LOGIC; -- counter bit 2
014- );
015- END tglcnt;
016-
017- ARCHITECTURE tglcnt_arch OF tglcnt IS
018- COMPONENT IBUF PORT(I:IN STD_LOGIC;
019- O:OUT STD_LOGIC); END COMPONENT;
020- COMPONENT BUFG PORT(I:IN STD_LOGIC;
021- O:OUT STD_LOGIC); END COMPONENT;
022- SIGNAL c_in, c_buf: STD_LOGIC;-- buffered clock signals
023- BEGIN
024- u0: IBUF PORT MAP(I=>c, O=>c_in); --bring in clock through IBUF
025- u1: BUFG PORT MAP(I=>c_in, O=>c_buf); -- route it to clock buffer
026-
027- bit0: PROCESS (c_buf,t0,aclr) --process for counter LSB
028- BEGIN
029- IF aclr='1' THEN -- async clear bit if clear is high
030- t0 <= '0';
031- -- toggle the bit on the rising edge of the clock
032- ELSIF (c_buf'event AND c_buf='1') THEN
033- t0 <= NOT t0;
034- END IF;
035- END PROCESS bit0;
036-
037- bit1: PROCESS (t0,t1,aclr) --process for middle counter bit
038- BEGIN
039- IF aclr='1' THEN
040- t1 <= '0';
041- -- toggle this bit when the LSB toggles from 0 to 1
042- ELSIF (t0'event AND t0='1') THEN
043- t1 <= NOT t1;
044- END IF;
045- END PROCESS bit1;
046-
047- bit2: PROCESS (t1,t2,aclr) -- process for counter MSB
048- BEGIN
049- IF aclr='1' THEN
050- t2 <= '0';
051- -- toggle the MSB when the middle bit toggles from 0 to 1
052- ELSIF (t1'event AND t1='1') THEN
053- t2 <= NOT t2;
054- END IF;
055- END PROCESS bit2;
056-
057- END tglcnt_arch;
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_211_0.png)

## Figure 6.13 Simulated waveforms 3-bit counter built from toggle flip-flops.

The following sequence of commands will step the downloaded design through the same set of states as the simulation:

| Command | ACLR | C | LED S2 (T2) | LED S1 (T1) | LED S0 (T0) |
|---|---|---|---|---|---|
| XSPORT 10 | 1 | 0 | Dark (0) | Dark (0) | Dark (0) |
| XSPORT 00 | 0 | 0 | Dark (0) | Dark (0) | Dark (0) |
| XSPORT 01 | 0 | 1 | Bright (1) | Bright (1) | Bright (1) |
| XSPORT 00 | 0 | 0 | Bright (1) | Bright (1) | Bright (1) |
| XSPORT 01 | 0 | 1 | Bright (1) | Bright (1) | Dark (0) |
| XSPORT 00 | 0 | 0 | Bright (1) | Bright (1) | Dark (0) |
| XSPORT 01 | 0 | 1 | Bright (1) | Dark (0) | Bright (1) |
| XSPORT 00 | 0 | 0 | Bright (1) | Dark (0) | Dark (0) |
| XSPORT 01 | 0 | 1 | Bright (1) | Dark (0) | Dark (0) |
| XSPORT 00 | 0 | 0 | Bright (1) | Dark (0) | Dark (0) |
| XSPORT 01 | 0 | 1 | Dark (0) | Bright (1) | Bright (1) |
| XSPORT 00 | 0 | 0 | Dark (0) | Bright (1) | Bright (1) |
| XSPORT 01 | 0 | 1 | Dark (0) | Bright (1) | Dark (0) |
| XSPORT 00 | 0 | 0 | Dark (0) | Bright (1) | Dark (0) |
| XSPORT 01 | 0 | 1 | Dark (0) | Dark (0) | Bright (1) |
| XSPORT 00 | 0 | 0 | Dark (0) | Dark (0) | Bright (1) |
| XSPORT 01 | 0 | 1 | Dark (0) | Dark (0) | Dark (0) |
| XSPORT 00 | 0 | 0 | Dark (0) | Dark (0) | Dark (0) |
| XSPORT 01 | 0 | 1 | Bright (1) | Bright (1) | Bright (1) |
| XSPORT 00 | 0 | 0 | Bright (1) | Bright (1) | Bright (1) |
| XSPORT 01 | 0 | 1 | Bright (1) | Bright (1) | Dark (0) |
| XSPORT 00 | 0 | 0 | Bright (1) | Bright (1) | Dark (0) |
| XSPORT 10 | 1 | 0 | Dark (0) | Dark (0) | Dark (0) |

## Projects

- 1. Change the edge-triggered DFF so it has an asynchronous preset input that sets it to a logic 1.
- 2. Do a unit-delay simulation of the edge-triggered DFF. Do you see where the setup and hold times arise?
- 3. Use the schematic editor to re-create the toggle counter. (The D flip-flop is symbol FD in the SC Symbols window.)
- 4. Build a shift-register consisting of a string of seven D flip-flops, each of whose output attaches to the input of the next flip-flop. All the flip-flops receive the same clock. Create a user-constraints file for the XS40 or XS95 Board that assigns the clock input and the input of the initial D flip-flop in the string to pins that are driven by B0 and B1 of the XSPORT command. Also assign the outputs of the flip-flops to pins that drive the LED segments. Download the circuit to your board and use XSPORT to display different patterns on the LED segments. Could you use the outputs of the shift-register flip-flops to drive logic inputs to other circuits? If so, does the shift register give you a way to test other circuits with more than eight inputs that exceed the I/O capabilities of the PC parallel port?
- 5. Build a counter that “walks” around the LED digit by lighting each segment one at a time.
