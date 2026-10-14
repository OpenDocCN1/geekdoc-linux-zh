0..3 and bits 4..7 using two of the 4-bit parity circuits. Then, compute the total parity of the 8-bit number using the following table:

| Parity 0..3 | Parity 4..7 | Parity 0..7 |
|---|---|---|
| Even | Even | Even |
| Odd | Even | Odd |
| Even | Odd | Odd |
| Odd | Odd | Even |

Assuming that parity circuits output a logic 1 whenever the parity is odd and a 0 when parity is even, the above table can be re-written as follows:

| Parity 0..3 | Parity 4..7 | Parity 0..7 |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 1 | 0 |

This is just the truth table for an XOR gate. So the circuit for an 8-bit parity detector now looks like the one of Figure 4.2(a).

Now the question naturally arises: "So how do I build the 4-bit parity circuits that I just used in the 8-bit circuit?" Well that is easy: build a couple of 2-bit parity generators and connect their outputs to an XOR gate (see Figure 4.2(b)). Carrying the reasoning further shows that the 2-bit parity generators are just single XOR gates. The total 8-bit even-parity generator is shown in Figure 4.2(c).

The problem decomposition has given us a hierarchy: at the bottom level are 2-bit parity generators (a.k.a. XOR gates), followed by 4-bit parity generators at the next hierarchical level, topped off by an 8-bit parity generator at the top level.

How would we describe this hierarchy and these modules in ABEL? That is all shown in Listings 4.1, 4.2, and 4.3. The module names, module instantiation names, and module input/output names used in the ABEL code are listed in Figure 4.2.

# 2-bit even-parity generator (Listing 4.1):

The MODULE keyword (line 1) starts the definition of the 2-bit parity generator module, followed by the name of the module (evpar2). Line 2 uses the INTERFACE keyword to define a parenthesized list of inputs (b0 and b1) and a single output (par). In this case, the INTERFACE keyword is used to define the external interface of this module for those modules that will use it. The two inputs and the output are