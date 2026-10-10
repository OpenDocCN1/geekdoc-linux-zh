10 (five pennies)
1 (one nickel)
$\begin{array}{r} - 3 \\ \hline 2 \end{array}$

One nickel is left:

10 (five pennies)
1 (one nickel)
$\begin{array}{r} - 3 \\ \hline 12 \end{array}$

So we get one nickel and two pennies left.

# **2.3 Conversion to Pental**

Sometimes conversions are unavoidable. For a computer to be able to store a number in binary which is input in decimal, a conversion is needed. Although conversions can be done by searching for a representation which works, there are more efficient methods. Consider the conversion of 207 into base five. To understand this conversion, it may help to look at the answer before we start:

$1312 = 1 \cdot 5^3 + 3 \cdot 5^2 + 1 \cdot 5^1 + 2 \cdot 5^0$

We can see that 5 can be factored out of this sum, except for the 2 at the end:

$1312 = (1 \cdot 5^2 + 3 \cdot 5^1 + 1 \cdot 5^0) \cdot 5 + 2$

But this just says what the quotient and remainder of 207 divided by 5 are. Notice that the remainder is our units digit. Furthermore, we can calculate this quotient and remainder using base ten, which is what we have available when we start this conversion:

$\begin{array}{r} 41 \\ 5) \overline{207} \\ \underline{205} \\ 2 \text{ and so our ones digit is 2.} \end{array}$

We have in base ten that:

$207 = 41 \cdot 5 + 2$

where again peeking at the answer shows us that:

$41 = 1 \cdot 5^2 + 3 \cdot 5^1 + 1 \cdot 5^0$

The quotient, 41, contains the information needed to get all the other digits. They can be obtained using more divisions:

$\begin{array}{r} 8 \\ 5) \overline{41} \\ \underline{40} \\ 1 \text{ and adjoining this digit gives us 12.} \end{array}$