
![](img/a3d6758e6e21b80b35e1b981ecbc1234_37_0.png)

A circuit which adds four-digit binary numbers requires four full adders ganged together.

![](img/a3d6758e6e21b80b35e1b981ecbc1234_37_1.png)

This is what the adding circuits in a four-bit processor look like. Shown here is the same calculation of thirteen plus six illustrated at the beginning of this section. In binary, that is 1101 plus 0110. The resulting total is 0011. There is also an output carry value of 1. The input carry is not used here. Surprisingly enough, there is a need for it however. We will see what that is in section 3.7.

It is one of the characteristics of a four-bit processor that it adds binary numbers four bits at a time.

A computer with a four-bit processor would not be limited to small number arithmetic, but its software would need to break large numbers down into numbers no bigger than 16.

## 3.5 Sequential Circuits

In all the circuits shown so far, the output is determined by the inputs. By using the truth tables of the component gates, one can construct a truth table for the whole circuit. It might seem that this should be the case with all logic circuits. However, if an output is fed back around to an input, then a vicious circle is introduced into the process of determining the truth table. Circuits with feedback loops are called *sequential circuits*.

Circuits without feedback loops are not capable of storing logic values. The output of a Boolean circuit is a function of its inputs, its *present* inputs. That means, for example, if you tried to use a Boolean circuit as a memory, then no matter what you decided upon as the memory fetch command, this input would always produce the same output, namely the output specified by the truth table, so it would not be a true memory fetch. The output from a true memory fetch would depend upon what was stored at some time in the *past*.

Sequential circuits are important because they can store logic values.

### 3.5.1 A Flip-flop

Figure 3-6 shows an example of a circuit called a *flip-flop*. The S in the figure stands for *set* and the R stands for *reset*. The output of this circuit may be set if S = 1 and R = 0. In this case, the AND gate fed by the R input is forced to output a 0. Hence both inputs on the other AND gate are 1. Hence its output is 1 and the final output is 1.

![](img/a3d6758e6e21b80b35e1b981ecbc1234_38_0.png)

If S = 0 and R = 1, the situation is just reversed and the final output is 0.

However, if S = 1 and R = 1, the output is not determined by the truth tables. The feedback loops make that impossible. It turns out, however, that if the S = R = 1 state was entered from either the set or the reset state, then the final output is left alone. It does not change.

### 3.5.2 A Latch

Figure 3-7 shows an example of a circuit called a *latch*. This circuit stores one bit. It is called a latch because it “latches onto” a value.

![](img/a3d6758e6e21b80b35e1b981ecbc1234_38_1.png)

The *Freeze/Copy#* label in this figure uses the Intel # convention that when a signal is labeled with a meaningful word, then the meaning truthfully applies when the line is at logic 1, unless the label has a # appended, and then the opposite is the case. So the *Freeze/Copy#* label tells us that logic 1 means Freeze and logic 0 means Copy.

- When the *Freeze/Copy#* line is zero, the OR gates are opened and the circuit is turned into a flip-flop, where the input is either set or reset. The NOT gate makes the S and R inputs opposite to each other. The input value is copied to the output.
- When the *Freeze/Copy#* line becomes 1, both OR gates are forced to 1 and this freezes the output. When the output is frozen, subsequent changes in the input have no effect on the circuit. The output value remains just what it was the last time the *Freeze/Copy#* line turned from 1 to 0, i.e. the last time it froze.

That output value is in storage.

### 3.5.3 Registers

Four latches used together in parallel can store four bits. This is an example of a *register*. A four-bit register is a collection of circuits that can store four bits. Different registers in a processor do not have to store the same number of bits, but it is easier to make things work when they do. The number of bits in a “typical” register is one of the attributes of a processor which determines whether it is called a four-bit processor, an eight-bit processor, or whatever.

The contents of a four-bit register are very naturally specified using a four-digit binary number. The four-digit binary numbers are the integers from 0 through 15. An eight-bit register holds an integer from 0 through 127.

We see that the most natural way of specifying the contents of a register leaves no room for negative numbers. The representation of negative numbers will be discussed in the next section.

### 3.5.4 Bit Significance

Because binary numbers are used to describe the contents of registers and memory locations, the numerical concept of a *significant digit* is useful in singling out individual bits of a specific storage location. For example, if a four-bit register holds the binary number 1100, then the four digits in order of significance are 1, 1, 0, and 0. So the most significant digit is 1, and the least significant digit is 0. The three most significant digits are 110. The three least significant digits are 100. Sometimes in this text, the most significant bits will be referred to as the *top* or *upper* bits and the least significant as the *bottom* or *lower* bits.

## 3.6 Negative Number Representation

The customary way to represent a negative number is to prepend a minus sign. Putting a - in front of a 3 makes a -3. This method of representing negatives is called *signed magnitude* representation. It can be implemented on the computer by allocating one bit of storage for a sign bit. To change the sign of a number that is stored using signed magnitude representation, one can simply flip the sign bit. Signed magnitude representation is not generally used for integers on the computer. The reason is that in order to do addition with signed magnitude representation, you need to do it the way it is taught to youngsters.

### 3.6.1 Signed Magnitude Addition

To add x and y:

- Case I. If x and y are both positive, just add and make your answer positive.
- Case II. If x and y are both negative, remove the negative signs, add the numbers, and tack a minus sign onto the result.
- Case III. If x and y have different signs, subtract the smaller magnitude from the larger magnitude, and if the larger magnitude had a minus sign, then tack this onto the result.

Implementing signed magnitude addition with logic circuits on a chip would be a terrible waste of transistors.

### 3.6.2 Easy Addition

The method which is actually used with logic circuits to add x and y works like this:

Pay no attention to whether x and y are positive or negative; just add them!

Such a method would seem to be no method at all. But it works. It works because a special system for representing negatives is used, and because a register has a finite size, like an odometer.

### 3.6.3 Odometer Arithmetic

An odometer is an adding machine. It adds up the miles that you drive. Mileage is always considered to have a positive value. (Would a negative value imply driving backwards, or what?) However, consider the following equation, which we would ordinarily think of as making sense only for negative numbers.

$$x + 10 = 5$$

Table 3.8. Odometer Negatives

| -1 | 99,999 |
| -2 | 99,998 |
| -3 | 99,997 |
| -4 | 99,996 |
| -5 | 99,995 |
| -6 | 99,994 |
| -7 | 99,993 |
| -8 | 99,992 |
| -9 | 99,991 |
| -10 | 99,990 |
| -11 | 99,89 |
| -12 | 99,988 |
| … | … |
| etc. | |

The obvious solution is x = -5. However, there is an odometer interpretation of this equation as well. Suppose you drive 10 miles in your car and the odometer reads 5 when you finish, then what did it read when you began? It must have read 99,995. Similarly if you have a car whose odometer reads 10 miles and you drive it 99,995 miles (1) then the odometer should read 5 miles when you finish. The point here is that 99,995 acts just like -5 when added on the odometer. Table 3.8 shows what odometer negatives look like. Notice that to get the number that works as the negative of a number x, you subtract x from 100,000.

Arithmetic on the odometer works this way because the odometer turns over at 100,000 miles. Computer registers turn over also— but not at 100,000.

### 3.6.4 Register Arithmetic

A four-bit register turns over at binary 1 0000 = 2⁴ = 16. The table of negatives for a four-bit register can easily be listed completely. See Table 3.9. The only difference between this table and the odometer table is that 16 is a lot smaller than 100,000. As with the odometer, you can use subtraction instead of the table to find the number which works as the negative of some number x. In the case of a four-bit register, you subtract x from 16 instead of from 100,000. Otherwise it is the same.

But in one respect, Table 3.9 is a little alarming. For example, it gives us the fact that 11 works the same as -5. This means we now have a serious ambiguity. If a four-bit register contains 1011, we cannot tell whether this actually means 11 or -5. Some convention is needed. The convention that is used is to take the first bit as a kind of sign bit. When the first bit is 0, the number is positive (or zero). When the first bit is 1, the number is negative. The resulting system is called the two's complement system. When the two's complement system is used, the ambiguity is

Table 3.9. Four-Bit Register Negatives (Ambiguous?)

| Decimal | Binary |
| -1 | 15 | 1111 |
| -2 | 14 | 1110 |
| -3 | 13 | 1101 |
| -4 | 12 | 1100 |
| -5 | 11 | 1011 |
| -6 | 10 | 1010 |
| -7 | 9 | 1001 |
| -8 | 8 | 1000 |
