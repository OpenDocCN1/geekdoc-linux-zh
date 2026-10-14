# Listing 3.3 The VHDL description of the LED decoder.

```
001- -- LED Decoder for 7-segment LED
002-
003- LIBRARY IEEE;
004- USE IEEE.std_logic_1164.ALL;
005-
006- -- LED Decoder interface description
007- ENTITY leddec IS
008- PORT
009- (
010- d: IN std_logic_vector (3 DOWNTO 0); -- 4-bit hex input
011- s: OUT std_logic_vector (6 DOWNTO 0) -- 7 LED drivers
012- );
013- END leddec;
014-
015- -- LED Decoder architecture description
016- ARCHITECTURE leddec_arch OF leddec IS
017- BEGIN
018- -- for all decimal values 0-9, drive the appropriate segments
019- -- on the 7-segment LED to display the numeral
020- WITH d SELECT
021- s <= "1110111" WHEN "0000", -- display numeral '0'
022- "0000100" WHEN "0001", -- display numeral '1'
023- "1011010" WHEN "0010", -- display numeral '2'
024- "1011011" WHEN "0011", -- display numeral '3'
025- "0111010" WHEN "0100", -- display numeral '4'
026- "1101011" WHEN "0101", -- display numeral '5'
027- "1101111" WHEN "0110", -- display numeral '6'
028- "1010000" WHEN "0111", -- display numeral '7'
029- "1111111" WHEN "1000", -- display numeral '8'
030- "1111011" WHEN "1001", -- display numeral '9'
031- "0000000" WHEN OTHERS; -- blank display for non-decimals
032- END leddec_arch;
033-
```

input array [d3,d2,d1,d0] = [0,0,0,0], then the output array is set such that [s6,s5,s4,s3,s2,s1,s0] = [1,1,1,0,1,1,1].

The values of d following the WHEN keyword have to be mutually exclusive (i.e., no value can be repeated). But it is not necessary to list every possible value for d. Line 31 uses the keyword OTHERS to set [s6,s5,s4,s3,s2,s1,s0] = [0,0,0,0,0,0,0] whenever d does not match one of the values on lines 21 through 30. In effect, OTHERS matches any unspecified value of the selector.