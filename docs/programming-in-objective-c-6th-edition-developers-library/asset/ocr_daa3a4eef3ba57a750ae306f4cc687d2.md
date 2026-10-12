```
} 
```
Program 6.3 Output
```
```
0
1
1
2
3
5
8
13
21
34
55
89
144
233
377
```
```

The first two Fibonacci numbers, called $F_{0}$ and $F_{1}$, are defined to be 0 and 1, respectively. Thereafter, each successive Fibonacci number $F_{i}$ is defined to be the sum of the two preceding Fibonacci numbers $F_{i-2}$ and $F_{i-1}$. So $F_{2}$ is calculated by adding together the values of $F_{0}$ and $F_{1}$. In the preceding program, this corresponds directly to calculating F<sub>2</sub> by adding the values F<sub>0</sub> and F<sub>1</sub>. This calculation is performed inside the for loop, which calculates the values of F<sub>2</sub> through F<sub>14</sub> (or, equivalently, F<sub>0</sub> through F<sub>12</sub>).

Fibonacci numbers actually have many applications in the field of mathematics and in the study of computer algorithms. The sequence of Fibonacci numbers historically originated from the “rabbits problem”: If you start with a pair of rabbits and assume that each pair of rabbits produces a new pair of rabbits each month, that each newly born pair of rabbits can produce offspring by the end of their second month, and that rabbits never die, how many pairs of rabbits will you have after the end of one year? The answer to this problem rests in the fact that at the end of the $n$th month, there will be a total of $F_{n+2}$ rabbits. Therefore, according to the table from Program 6.3, at the end of the twelfth month, you will have a total of 377 pairs of rabbits.

# Using an Array to Generate Prime Numbers

Now, it’s time to return to the prime number program that you developed in Chapter 5, “Making Decisions,” and see how the use of an array can help you to develop a more efficient program. In Program 5.10A, the criteria that you used for determining if a number was prime was to divide the prime candidate by all successive integers from 2 up to the number - 1. In exercise 7 in Chapter 5, you noted two inefficiencies with this approach that could easily be corrected. But even with these changes, the approach used is still not efficient. Although such questions of efficiency might not be important when dealing with a table of prime numbers up to 50, these questions do become important, for example, when you start thinking about generating a table of prime numbers up to 100,000.
An improved method for generating prime numbers involves the notion that a number is prime if it is