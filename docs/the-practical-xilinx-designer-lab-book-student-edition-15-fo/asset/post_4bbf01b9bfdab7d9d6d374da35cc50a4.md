
Patterns, such as a 7-segment LED decoder. State Diagrams are useful for specifying designs with complex state machines.

Following the Declarations section, the design section is delimited by using the keyword Equations, Truth_Table, or State_Diagram. State diagrams and truth tables using sequential logic will need an accompanying equations section to define clock signals as well. These keywords must be used when switching between the three design methods.

## Equations

Equation design entry primarily consists of assignment statements. These can be combinatorial assignments (=), or registered assignments using the delay operator (:=). All registered equations using the delay operator (:=) will behave as being implemented as an edge triggered flip-flop. Therefore, they must also have a clock associated with the signal name. This is done by using the .clk dot extension.

For example:

```
my_registered_node := my_input;
my_registered_node.clk = my_clk;
```

This is logically equivalent to describing the same logic with detailed dot extensions as follows.

```
my_registered_node.d = my_input;
my_registered_node.clk = my_clk;
```

Using equations to specify a design is similar to programming in other languages, except the context of the equations are evaluated in parallel rather than sequentially. In the following example, the order in which the equations are written is only important in programming languages.

In ABEL, all of the equations are evaluated concurrently, thus, the order in which they are presented is not important.

For example, in a normal programming language such as C, the code:

```
x = x + 1;
total = total +x;
```

is not the same as

```
total = total + x;
x = x+1;
```

```
22  [.C.] -> [ 3, 3];
23  [.C.] -> [ 4, 6];
24  [.C.] -> [ 5, 10];
25  [.C.] -> [ 6, 15];
26  [.C.] -> [ 7, 21];
27

28  END
```

The beginning of this design (as for all ABEL designs) defines the module name. Following the module name are the declarations of the module. On line 3, the clock input is defined. On line 4, the nodes that will contain the information for x are declared as an 8-bit register. Line 5 declares the output pins for total, an 8-bit register. On line 7 and 8, the 8 bits are renamed to a single variable name, allowing the equations to be written quickly and clearly. Line 10 is an ABEL compiler directive which limits the lookahead carry chain of the adder to 4 bits. On line 12, the EQUATIONS keyword signifies the end of the Declarations section and the beginning of the logic descriptions.

Every register must have a clock associated with it and in this design, line 13 specifies that the x and total registers are clocked by the input myclock. The actual logic assignments on lines 15 and 16 determine how the registers are affected when myclock goes high. At the rising clock edge, x (after clock) will get the value of x (before clock) + 1, and total (after clock) will get the value of total (before clock) + x (before clock). Figure B.2 shows a block diagram of the circuit described by this code.

![](img/5124daf79d2807d81e49f49c22f1f8c1_439_0.png)

**Figure B.2**  Block Diagram

## Test Vectors

Test vectors are also included at the end of this design. These test vectors show the expected values of the output for each rising clock signal, and are extremely useful for verifying the design. Test vectors are also included in the JEDEC programming file which can be used in the XC9500 family to perform an INTEST operation through the JTAG port.

## Dot Extensions

Dot extensions, illustrated in Figure B.3, give more control over the implementation of the design. Dot extensions such as .AP or .AR are used to specify asynchronous preset and asynchronous reset for flip-flops. Other common dot extensions are .OE used to specify the output enable, and .PIN used with bi-directional signals. For a complete set of supported dot extensions, please refer to the documentation for the particular version of ABEL being used.

![](img/5124daf79d2807d81e49f49c22f1f8c1_440_0.png)

Figure B.3 Directly Supported ABEL Dot Extensions

## Logical Operators

Logical operators allow the user to manipulate signals logically and can be applied to both signals and sets. When applied to sets, they are applied bitwise, and the sets must be the same size.

The operators are shown in Table B.1.

## Arithmetic Operators

Arithmetic and relational operators can be used on sets to quickly generate adders, counters, and comparators. Large arithmetic functions, such as adders and magnitude comparators, will generate very wide equations to implement the carry look ahead signals. In order to control the width of these lookahead carry equations, the compiler directive, @carry, can be used. For example, @carry 4, would limit the carry chain to 4-bits. An 8-bit adder therefore, would
