
# Chapter 6: ADVANCED VARIABLE USAGE

```
[6040]: i=3 j=5
[6041]: (( i += j )) ; print i=$i
i=8
[6042]: (( i %= j )) ; print i=$i
i=3
[6043]: (( i <<= 5 )) ; print i=$i
i=96
[6044]:
```

The expression i += j is equivalent to i = i + j. You can use this sort of typing shortcut for all arithmetic operators whenever the right-hand side of an assignment can be written with the variable on the left-hand side as the first operand.

- **i) What does the % operator compute?**
Answer: The remainder when you divide the first operand by the second.

In line 6042, the right-hand side is equivalent to 8%5 (because the value of i was changed in line 6041), so the result is 3 because 8 divided by 5 has a quotient of 1 (which is discarded) and a remainder of 3.

> This “remainder operator” is usually called the modulus operator, or modulo, and is shortened to mod.

- **j) What does the << operator compute?**
Answer: It shifts the bits to the left the number of positions specified.

This is one of several “bit manipulation” operators. Others include >> (shift right), & (bit-wise and), | (bit-wise or), ^ (bit-wise exclusive or), and - (bit-wise negation, also known as one's complement). You usually use these operators when you read data from some sort of device that uses a non-standard data encoding scheme and you need to convert it into values that you can work with your programs.

The value printed after line 6043, 96, is equal to the value of i times 2⁵ Each position you shift the bits in an integer to the left doubles its value, so shifting 5 positions doubles the value 5 times, which is the same as 2⁵ The bit manipulation operators work only on variables of integer.

## Lab 6.1: Typed Variables and Scope

### LAB 6.1

```
unset m
i=3 j=5
m=i*j
(( k = m )); print m=$k
```

- **k) What is the difference between referencing the m inside double parentheses and outside them in the print command?**
Answer: Your interaction should look like the following:
[6044]: unset m
[6045]: i=3 j=5
[6046]: m=i*j
[6047]: (( k = m )); print m=$k
m=i*j k=1
[6048]:

Because m is a string, line 6046 assigns a string value to it. However, inside double parentheses on line 6047, the shell interprets that value as an arithmetic expression and assigns the value 3*5 to k. Because multiplication and modulus operators have the same precedence, the shell evaluates them left-to-right so the value is 5 modulo 5. Outside the arithmetic expression, the print command shows that a reference to m is the string i*j, but k has arithmetic value of 1.

> If you have declared a variable to be an integer or float, then you don't need double parentheses to assign the value of an expression to it. If a numeric variable is on the left of equal sign, the shell will treat variable names on the right side as references to the variables, even without dollar signs in front of them, and it will evaluate any values that look like expressions as well.

![](img/694fa9f0320e707804a4c650b96a09b4_303_0.png)

Thus, in this case, line 6046 could have been k=m; print m=$k, with the same result. Avoid using this tip unless you are doing a long sequence of calculations where (i) it is clear that you are doing arithmetic computations rather than string manipulations and (ii) the double parentheses would create a lot of clutter, which can make code difficult to read, too.

## Chapter 6: ADVANCED VARIABLE USAGE

```
float x=3 y=5 z=7
(( x = sqrt(2) ))
(( y = log(100000)/log(10) ))
(( z = cos(3.14159) ))
print x=$x y=$y z=$z
```

- **1) What did you observe?**
Answer: Your interaction should look like the following:
[6048]: float x = sqrt(2)
[6049]: (( y = log(100000)/log(10) ))
[6050]: (( z = cos(3.14159) ))
[6052]: print x=$x y=$y z=$z
x=1.41421356 y=5 z=-1

First, you can see that x gets the square root of 2 and gets displayed with ten digits of precision. Next, the fact that y gets the value 5 indicates that the shell computes logarithms using base e (natural logs, or ln). Computing ln(100000)+ln(10) is the same as computing log10(100000). Finally, the value printed for cos(π) is -1, which indicates that the shell requires you to give the angle for the trigonometric functions in radians, not degrees. (The cosine of π radians is negative one, but the cosine of π degrees would have been +0.998.)

## 6.1.3 ANSWERS

Run the following command:
print -- $((sqrt(2))

- **a) What printed?**
Answer: Your interaction should look like the following:
[6053]: print -- $((sqrt(2)))
1.41421356237
[6054]:

## Lab 6.1: Typed Variables and Scope

### LAB 6.1

It's always a good idea to put double dashes before the arguments of a print command, especially when the first value is an arithmetic expansion. If the result of the expansion is negative, the initial minus sign will erroneously indicate an option parameter if you don't put in the double dashes. Of course, the sqrt() function won't generate a negative result, but it's a good idea to put in the double dashes all the time.

![](img/694fa9f0320e707804a4c650b96a09b4_305_0.png)

The value printed is the square root of 2, with 12 digits of precision.

```
readonly float two_pi=$(( 2 * 3.141592654 ))
float theta=180
print -- $( cos(theta))
```

- **b) What printed?**
Answer: Your interaction should look like the following:
[6054]: readonly float two_pi=$(( 2 * 3.141592654 ))
[6055]: float theta=180
[6056]: print -- $( cos(theta))
[6057]: -1

- **c) What did the first command do?**
Answer: The first command declared two_pi to be a float.

- **d) What happens if you try to run the following command?**
two_pi=3.14159264
Answer: The shell prints an error message saying two_pi is read only.

## Chapter 6: ADVANCED VARIABLE USAGE

It is actually an alias for typeset -r. Because float is also an alias for typeset, m=i*j k=1.

> If you declare a variable to be read-only, it becomes a "constant," and you eliminate the chance that you might accidentally change its value.

![](img/694fa9f0320e707804a4c650b96a09b4_306_0.png)

Read-only variables are not absolutely constant. If you declare a variable that the shell changes, such as SECONDS, to be read-only, you can't change it anymore, but the shell itself can.

```
float x=3 y=5 z=7
```

- **e) What two values are the same, and why?**
Answer: Your interaction should look like the following:
[6057]: float x=3 y=5 z=7
[6058]: (( x = sqrt(2) )) (( y = log(100000)/log(10) )) (( z = cos(3.14159) ))
[6059]: print x=$x y=$y z=$z
11.832159662 5.916097983 2.958039892 11.832159597

The first and fourth numbers have the same value. The first one is the value of the last (rightmost) assignment in the arithmetic expansion, and the fourth is the value of z, which is the variable that received the result of that same assignment.

- **f) If the two values are the same, why did they print differently?**
Answer: They are the same value, but they are printed with different numbers of digits because z is declared as a float, but the expression does not have an associated precision.

# FOR EXAMPLE

You can control the number of digits used to print the value of a variable using the typeset command, but you don't have any way to control the precision when printing the results of arithmetic expansions when you,
