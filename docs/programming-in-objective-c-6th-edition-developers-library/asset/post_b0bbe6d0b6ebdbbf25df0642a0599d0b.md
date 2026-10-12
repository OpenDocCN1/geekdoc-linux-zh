
## Program 7.17 Output

1

The fact that the `f` function includes a call to itself makes this function recursive.
When the function is called to calculate the factorial of 3, the value of the formal parameter `n` is set to 3. Because this value is not zero, the following program statement

`r = n * f(n - 1);`

is executed, which, given the value of `n`, is evaluated as

`3 * f(2)`

This expression specifies that the `f` function is to be called, this time to calculate the factorial of 2. Therefore, the multiplication of 3 by this value is left pending while `f(2)` is calculated.
Even though you are again calling the same function, you should conceptualize this as a call to a separate function. Each time any function is called in C—be it recursive or not—the function gets its own set of local variables and formal parameters with which to work. Therefore, the local variable `r` and the formal parameter `n` that exist when the `f` function is called to calculate the factorial of 3 are distinct from the variable `r` and the parameter `n` when the function is called to calculate the factorial of 2.
With the value of `n` equal to 2, the `f` function executes the statement

`r = n * f(n - 1);`

which is evaluated as

`2 * f(1)`

Once again, the multiplication of 2 by the factorial of 1 is left pending while the `f` function is called to calculate the factorial of 1.
With the value of `n` equal to 1, the `f` function once again executes the statement

`r = n * f(n - 1);`

which is evaluated as

`1 * f(0)`

When the `f` function is called to calculate the factorial of 0, the function sets the value of `r` to 1 and returns, thus initiating the evaluation of all of the pending expressions. So the value of `f(0)`, or 1, is returned to the calling function (which happens to be the `f` function), multiplied by 1, and assigned to `r`. This value of 1, which represents the value of `f(1)`, is then returned back to the calling function (once again the `f` function) where it is multiplied by 2, stored into `r`, and returned as the value of `f(2)`. Finally, the returned value of 2 is multiplied by 3, thus completing the pending calculation of `f(3)`. The resulting value of 6 is returned as the final result of the call to the `f` function, to be displayed by the `p` function.

In summary, the sequence of operations that is performed in the evaluation of `f` can be conceptualized as follows:

![](img/e50cb5e8cc6587186db5746e2ac19394_153_0.png)

It might be a good idea for you to trace through the operation of the `f` function with a pencil and paper. Assume that the function is initially called to calculate the factorial of 4. List the values of `n` and `r` at each call to the `f` function.

This discussion concludes this chapter on functions and variables. The program function is a powerful tool in the C programming language. Enough cannot be said about the critical importance of structuring a program in terms of small, well-defined functions. Functions are used heavily throughout the remainder of this book. At this point, you should review any topics covered in this chapter that still seem unclear. Working through the following exercises will also help reinforce the topics that have been discussed.

## Exercises

- 1. Type in and run the 17 programs presented in this chapter. Compare the output produced by each program with the output presented after each program in the text.
- 2. Modify Program 7.4 so that the value of `t` is returned by the function. Then go back to Program 4.5 and change that program so that it calls the new version of the `c` function.
- 3. Modify Program 7.8 so that the value of `e` is passed as an argument to the function. Try experimenting with different values of `e` to see the effect that it has on the value of the square root.
- 4. Modify Program 7.8 so that the value of `g` is printed each time through the `w` loop. Notice how quickly the value of `g` converges to the square root. What conclusions can you reach about the number of iterations through the loop, the number whose square root is being calculated, and the value of the initial guess?
- 5. The criteria used for termination of the loop in the `s` function of Program 7.8 is not suitable for use when computing the square root of very large or very small numbers. Rather than comparing the difference between the value of `x` and the value of `g^2`, the program should compare the ratio of the two values to 1. The closer this ratio gets to 1, the more accurate the approximation of the square root. Modify **Program 7.8** so this new termination criteria is used.
- 6. Modify **Program 7.8** so that the `⊗` function accepts a double precision argument and returns the result as a double precision value. Be certain to change the value of the variable `⊕` to reflect the fact that double precision variables are now being used.
- 7. Write a function that raises an integer to a positive integer power. Call the function `×` taking two integer arguments $x$ and $n$. Have the function return a `1`, which represents the results of calculating $x^n$.
- 8. An equation of the form $a^2$ is known as a *quadratic equation*. The values of $a$, $b$, and $c$ in the preceding example represent constant values. So $4^2$ represents a quadratic equation where $a = 4$, $b = -17$, and $c = -15$. The values of $x$ that satisfy a particular quadratic equation, known as the *roots* of the equation, can be calculated by substituting the values of $a$, $b$, and $c$ into the following two formulas: $x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$

If the value of $b^2 - 4ac$, called the *discriminant*, is less than zero, the roots of the equation, $x_1$ and $x_2$, are imaginary numbers.

Write a program to solve a quadratic equation. The program should allow the user to enter the values for $a$, $b$, and $c$. If the discriminant is less than zero, a message should be displayed that the roots are imaginary; otherwise, the program should then proceed to calculate and display the two roots of the equation. (*Note:* Be certain to make use of the `⊗` function that you developed in this chapter.)
- 9. The least common multiple (*lcm*) of two positive integers $u$ and $v$ is the smallest positive integer that is evenly divisible by both $u$ and $v$. Thus, the *lcm* of 15 and 10, written *lcm* (15, 10), is 30 because 30 is the smallest integer divisible by both 15 and 10. Write a function `1` that takes two integer arguments and returns their *lcm*. The `1` function should calculate the least common multiple by calling the `9` function from **Program 7.6** in accordance with the following identity:

![](img/e50cb5e8cc6587186db5746e2ac19394_154_0.png)
- 10. Write a function `p` that returns 1 if its argument is a prime number and returns 0 otherwise.
- 11. Write a function called `a` that takes two arguments: an integer array and the number of elements in the array. Have the function return as its result the sum of the elements in the array.
- 12. A matrix $M$ with $i$ rows, $j$ columns can be *transposed* into a matrix $N$ having $j$ rows and $i$ columns by simply setting the value of $N_{a,b}$ equal to the value of $M_{b,a}$ for all relevant values of $a$ and $b$.
    - a. Write a function `t` that takes as an argument a $4 \times 5$ matrix and a $5 \times 4$ matrix. Have the function transpose the $4 \times 5$ matrix and store the results in the $5 \times 4$ matrix. Also write a `m` routine to test the function.
    - b. Using variable-length arrays, rewrite the `t` function developed in exercise 12a to take the number of rows and columns as arguments, and to transpose the matrix of the specified dimensions.
- 13. Modify the $s$ function from **Program 7.12** to take a third argument indicating whether the array is to be sorted in ascending or descending order. Then modify the $s$ algorithm to correctly sort the array into the indicated order.
- 14. Rewrite the functions developed in the last four exercises to use global variables instead of arguments. For example, the preceding exercise should now sort a globally defined array.
- 15. Modify **Program 7.14** so that the user is asked again to type in the value of the base if an invalid base is entered. The modified program should continue to ask for the value of the base until a valid response is given.
- 16. Modify **Program 7.14** so that the user can convert any number of integers. Make provision for the program to terminate when a zero is typed in as the value of the number to be converted.
