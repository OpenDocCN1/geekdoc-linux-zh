
## Listing 5.5 VHDL code for a 4-bit carry-lookahead adder (LKADD.VHD).

```vhdl
-- Look-ahead Adder

LIBRARY IEEE;
USE IEEE.std_logic_1164.ALL;

-- Look-ahead Adder interface description
ENTITY lkadd IS
    PORT
    (
        a: IN STD_LOGIC_VECTOR (3 DOWNTO 0); -- 4-bit addend
        b: IN STD_LOGIC_VECTOR (3 DOWNTO 0); -- 4-bit addend
        cin: IN STD_LOGIC; -- input carry
        sum: OUT STD_LOGIC_VECTOR (3 DOWNTO 0); -- 4-bit sum
        cout: OUT STD_LOGIC -- carry output
    );
END lkadd;

-- Look-ahead Adder architecture description
ARCHITECTURE lkadd_arch OF lkadd IS
    -- signal vectors for transferring the carry-propagate,
    -- carry-generate, and carry signals between the adder stages
    SIGNAL g: STD_LOGIC_VECTOR (3 DOWNTO 0); -- carry-generate
    SIGNAL p: STD_LOGIC_VECTOR (3 DOWNTO 0); -- carry-propagate
    SIGNAL c: STD_LOGIC_VECTOR (3 DOWNTO 0); -- carry
BEGIN
    PROCESS (a,b,cin,g,p,c)
    BEGIN
        -- use a FOR loop to iteratively connect the logic operations
        -- for the carry-generate, carry-propagate, and sum signals
        FOR i IN 0 TO 3
        LOOP
            g(i) <= a(i) AND b(i);
            p(i) <= a(i) XOR b(i);
            sum(i) <= p(i) XOR c(i);
        END LOOP;
        -- compute the carry bits for each stage of the adder
        c(0) <= cin;
        c(1) <= g(0) OR (p(0) AND c(0));
        c(2) <= g(1) OR (p(1) AND g(0)) OR
                (p(1) AND p(0) AND c(0));
        c(3) <= g(2) OR (p(2) AND g(1)) OR
                (p(2) AND p(1) AND g(0)) OR
                (p(2) AND p(1) AND p(0) AND c(0));
        cout <= g(3) OR (p(3) AND g(2)) OR
                (p(3) AND p(2) AND g(1)) OR
                (p(3) AND p(2) AND p(1) AND g(0)) OR
                (p(3) AND p(2) AND p(1) AND p(0) AND c(0));
    END PROCESS;
END lkadd_arch;
```

## Projects

1. Compile the 8-bit ripple-carry adder from the previous chapter. Create a simple input pattern that will make the adder exhibit its worst-case delay when a clock waveform is input to the adder as $c_{in}$. Simulate the adder and observe the delay. Download the adder to your XS40 or XS95 Board and measure the delay with an oscilloscope.

2. Design an 8-bit carry-lookahead adder using the 4-bit carry-lookahead module. Apply the same input pattern to this adder. Simulate the adder and observe the worst-case delay. Download the adder to your XS40 or XS95 Board and measure the delay with an oscilloscope. Compare the worst-case delay and size of this adder with the ripple-carry adder (use the report file). Does a faster design take more space in your FPGA?

## Flip-Flops

### Objectives

- Show how flip-flops work.
- Show the different types of flip-flops.
- Show how a counter is built from flip-flops.

### Discussion

So far we have experimented with combinational circuits that generate their outputs in response only to the current input. When the input changes, the output immediately changes (after some gate delay, of course). Combinational circuits have no way to remember what has happened before; they are creatures of the present.

This chapter will introduce you to sequential circuits. Sequential circuits are able to remember what has happened to them and can use it to alter their future behavior. A counter is an example of a sequential circuit because it remembers its current value and can add one to it to get to its next value. The current value of the counter is referred to as its state. The current state determines what the next state of the counter will be. For example, if the counter currently stores the number five, then the next time the counter is commanded to increment it will store the value six. The change in state from five to six is called a state transition.

The concept of state is easy to understand, but we do not know enough yet to build a counter. We must start with something simpler. The simplest sequential circuit is an S-R flip-flop (SRFF). An SRFF can remember whether a single bit is one or zero. This single-bit memory can be used as the basis of all other sequential circuits.

The operation of an SRFF is shown in Figure 6.1a. The SRFF is built from two 2-input NAND gates, each of whose outputs is fed back to one of the inputs of the other gate. The remaining inputs of the NAND gates are labeled /S and /R, while the outputs are labeled Q and /Q. In Figure 6.1a, both /S and /R are held at +5 V while Q = 1 and /Q = 0. Note that with /S = 1 and /Q = 0, the Q output should be 1 since one of the inputs to its NAND gate is low. Note also that with
