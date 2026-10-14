
## Listing 6.10 Behavioral VHDL code for a D flip-flop with asynchronous clear.

```
001- -- edge-triggered D flip-flop with asynchronous clear
002-
003- LIBRARY IEEE;
004- USE IEEE.std_logic_1164.ALL;
005-
006- ENTITY msdac IS
007- PORT
008- (
009- c: IN STD_LOGIC; -- clock
010- d: IN STD_LOGIC; -- data input
011- aclrb: IN STD_LOGIC; -- active-low asynchronous clear
012- sq: BUFFER STD_LOGIC; -- data output
013- sqb: OUT STD_LOGIC -- inverted data output
014- );
015- END msdac;
016-
017- ARCHITECTURE msdac_arch OF msdac IS
018- BEGIN
019- PROCESS (c,d,aclrb)
020- BEGIN
021- IF aclrb='0' THEN -- asynch clear takes precedence
022- sq <= '0';
023- ELSIF (c'event AND c='0') THEN -- over falling clock edge
024- sq <= d;
025- END IF;
026- END PROCESS;
027- sqb <= sq; -- generate the inverted output
028- END msdac_arch;
029-
```

NET sq LOC=P25; # S0 LED segment
NET sqb LOC=P26; # S1 LED segment
NET mq LOC=P24; # S2 LED segment (not used in VHDL version)
NET mqb LOC=P20; # S3 LED segment (not used in VHDL version)

Or use the following constraints for the XS95 Board:

```
NET c LOC=P46; # B0 argument of XSPORT
NET d LOC=P47; # B1 argument of XSPORT
NET aclrb LOC=P48; # B2 argument of XSPORT
NET sq LOC=P21; # S0 LED segment
NET sqb LOC=P23; # S1 LED segment
NET mq LOC=P19; # S2 LED segment (not used in VHDL version)
NET mqb LOC=P17; # S3 LED segment (not used in VHDL version)
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_203_0.png)

Figure 6.11 Simulated waveforms for a D flip-flop with asynchronous clear.

After compiling and downloading the MSDFAC design to an XS40 or XS95 Board, the following sequence of commands should give you the indicated results:

| Command | ACLRB | D | C | LED SO (SQ) |
|---|---|---|---|---|
| XSPORT 101 | 1 | 0 | 1 | ??? |
| XSPORT 110 | 1 | 1 | 0 | Bright (1) |
| XSPORT 010 | 0 | 1 | 0 | Dark (0) |
| XSPORT 011 | 0 | 1 | 1 | Dark (0) |
| XSPORT 010 | 0 | 1 | 0 | Dark (0) |

These results show the flip-flop reacts to the asynchronous clear without the need for a clock edge and that the clear input has priority over the data input.

## Built-In D Flip-Flops

We have built some flip-flops with various capabilities using basic logic gates. But an edge-triggered DFF takes at least 2 macrocells or LUTs even if we use the condensed form of Listing 6.2. To improve the utilization of resources in its FPLDs, XILINX has included built-in flip-flops in both its XC95108 CPLD and XC4005XL FPGA. Now all we have to do is learn how to use them with ABEL.

Listing 6.11 replicates the functions of our edge-triggered DFF with asynchronous clear. Line 8 declares the actual D flip-flop and gives it the name Q. The use of the type REG instead of COM distinguishes Q as a registered output rather than a combinatorial output like we have always used.

On line 12, the flip-flop is loaded with the value on the D input. Note the use of the := instead of =. The := implies that the Q output will only take on the value of the D input when a transition occurs on the clock input.

Line 13 specifies which signal serves as the clock input that controls the loading of the Q output. We have chosen to connect the inversion of C to the clock input of the Q DFF. This connection is specified by using the .CLK signal extension. Using the inverted C input makes the output of the Q flip-flop change on negative-going edges of the C input. (The normal operation of the built-in flip-flops is to change states on the rising edge.)

Line 14 specifies that the inversion of the ACLRB input is attached to the asynchronous clear input of the built-in flip-flop. The inversion is necessary because the built-in DFF is cleared when its asynchronous clear input is high, but we want the clearing to occur when ACLRB is low.

## Listing 6.11 ABEL code for using a built-in D flip-flop with asynchronous clear.

```
001- MODULE BIDFF
002- TITLE 'using a built-in DFF'
003-
004- DECLARATIONS
005- C PIN; "clock input
006- D PIN; "D input
007- ACLRB PIN; "clear input
008- Q PIN ISTYPE 'REG'; "DFF
009-
010- EQUATIONS
011- 0 := D; "connect to the D input of the DFF
012- Q.CLK = !C; "connect the clock with inversion
013- Q.ACLR = !ACLRB; "connect the asynchronous clear
014-
015- END BIDFF
```

In VHDL we really do not have to do anything special to make use of the built-in flip-flops of the XC9500 or XC4000 chips. The Foundation Series synthesis tools can automatically extract the latches implied by the behavioral VHDL code and create a netlist which uses the built-in flip-flops. But if you did want to explicitly use a built-in DFF, then Listing 6.12 shows how to do it for the XC9500. The interface to the FDPC flip-flop contained in every XC9500 macrocell is declared as a component on lines 17 through 24 of the bidff ARCHITECTURE block. The FDPC module is a DFF which changes state on the rising edge of the clock (C). A logic 1 on the CLR or PRE input will clear or set the flip-flop, respectively.
