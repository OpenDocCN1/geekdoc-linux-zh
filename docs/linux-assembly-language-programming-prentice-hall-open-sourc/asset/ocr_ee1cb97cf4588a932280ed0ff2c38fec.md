![](bbox=[0.055, 0.03, 0.683, 0.195])

A circuit which adds four-digit binary numbers requires four full adders ganged together.

![](bbox=[0.055, 0.254, 0.825, 0.414])

This is what the adding circuits in a four-bit processor look like. Shown here is the same calculation of thirteen plus six illustrated at the beginning of this section. In binary, that is 1101 plus 0110. The resulting total is 0011. There is also an output carry value of 1. The input carry is not used here. Surprisingly enough, there is a need for it however. We will see what that is in section 3.7.

It is one of the characteristics of a four-bit processor that it adds binary numbers four bits at a time.

A computer with a four-bit processor would not be limited to small number arithmetic, but its software would need to break large numbers down into numbers no bigger than 16.

# 3.5 Sequential Circuits

In all the circuits shown so far, the output is determined by the inputs. By using the truth tables of the component gates, one can construct a truth table for the whole circuit. It might seem that this should be the case with all logic circuits. However, if an output is fed back around to an input, then a vicious circle is introduced into the process of determining the truth table. Circuits with feedback loops are called *sequential circuits*.

Circuits without feedback loops are not capable of storing logic values. The output of a Boolean circuit is a function of its inputs, its *present* inputs. That means, for example, if you tried to use a Boolean circuit as a memory, then no matter what you decided upon as the memory fetch command, this input would always produce the same output, namely the output specified by the truth table, so it would not be a true memory fetch. The output from a true memory fetch would depend upon what was stored at some time in the *past*.

Sequential circuits are important because they can store logic values.

# 3.5.1 A Flip-flop

Figure 3-6 shows an example of a circuit called a *flip-flop*. The S in the figure stands for *set* and the R stands for *reset*. The output of this circuit may be set if S = 1 and R = 0. In this case, the AND gate fed by the R input is forced to output a 0. Hence both inputs on the other AND gate are 1. Hence its output is 1 and the final output is 1.