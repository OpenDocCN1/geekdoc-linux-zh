through 31. If n is negative, its value is negated before the modulus operator is applied. This is done because C does not define the sign of the result of applying the modulus operator to a negative value. Your machine can produce either a positive or negative result. By negating the value first, you ensure the result is positive. You then apply the unary minus operator to the result to turn it negative again; that is, within the range of values −31 through 0.

If the adjusted shift count is 0, the function simply assigns v to r. Otherwise, it proceeds with the rotation.

An n-bit rotation to the left is divided into three steps by the function. First, the n leftmost bits of v are extracted and shifted to the right. This is done by shifting v to the right by the size of an int (in our case, 32) minus n. Next, v is shifted n bits to the left, and finally, the extracted bits are ORed back in. A similar procedure is followed to rotate v to the right.

In the my function, note the use of hexadecimal notation for a change. The first call to the r function specifies that the value of w is to be rotated eight bits to the left. As can be seen from the program’s output, the hexadecimal value 0deef00ab is returned by the r function, which is in fact abcd0eef00 rotated to the left eight bits.

The second call to the r function has the effect of rotating the value of w 16 bits to the right.

The next two calls to the r function do similar things with the value of w and are fairly self-explanatory. The next-to-last call to r specifies a rotate count of 0. The program’s output verifies that in such a case the function simply returns the value unchanged.

The final call to r specifies a left rotate 44 places. This has the net effect of rotating the value left 12 bits (44 % 32 is 12).

# Bit Fields

With the bit operators discussed previously, you can proceed to perform all sorts of sophisticated operations on bits. Bit operations are frequently performed on data items that contain packed information. Just as a § can be used to conserve memory space on some computers, so can you pack information into the bits of a byte or word if you do not need to use the entire byte or word to represent the data. For example, flags that are used for a Boolean true or false condition can be represented in a single bit on a computer. Declaring a c variable that will be used as a flag uses eight bits (one byte) on most computers, and a _ variable is likely to use eight bits as well. In addition, if you need to store many flags inside a large table, the amount of memory that is wasted could become significant.

Two methods are available in C that can be used to pack information together to make better use of memory. One way is to simply represent the data inside a normal int, for example, and then access the desired bits of the int using the bit operators described in the previous sections. Another way is to define a structure of packed information using a C construct known as a bit field.

To illustrate how the first method can be used, suppose you want to pack five data values into a word because you have to maintain a very large table of these values in memory. Assume that three of these data values are flags, which you call f1, f2, and f3; the fourth value is an integer called t, which ranges from 1 to 2; and the final value is an integer called i, which ranges from 0 to 1.

Storing the values of the flags f1, f2, and f3 only requires three bits of storage, one bit for the