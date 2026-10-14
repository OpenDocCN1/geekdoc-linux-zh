# Listing 6.2　VHDL code for a simple SR flip-flop.

```
001- -- S-R Flip-Flop
002-
003- LIBRARY IEEE;
004- USE IEEE.std_logic_1164.ALL;
005-
006- ENTITY srff1 IS
007- PORT
008- (
009-   sb: IN STD_LOGIC;    -- active-low set input
010-   rb: IN STD_LOGIC;    -- active-low reset input
011-   q: BUFFER STD_LOGIC; -- data output
012-   qb: BUFFER STD_LOGIC -- inverted data output
013- );
014- END srff1;
015-
016- ARCHITECTURE srff1_arch OF srff1 IS
017- BEGIN
018-   q  <= (NOT sb AND qb);  -- cross-coupled NAND gates
019-   qb <= (NOT rb AND q);
020- END srff1_arch;
```

![](bbox=[0.311, 0.515, 0.927, 0.798])

**Figure 6.8**　Simulated waveforms for a simple SR flip-flop.