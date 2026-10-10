|  |  |  |
|---|---|---|
| ) |  |  |
| \(\cos(x)\) | The cosine of x, with x specified in radians. |  |
| \(\exp(x)\) | The exponential of x. |  |
| \(\int(x)\) | The integer part of x, truncated toward 0. |  |
| \(\log(x)\) | The natural logarithm of x. |  |
| rand( ) | A random floating-point value larger than 0 and less than 1. |  |
| \(\sin(x)\) | The sine of x, with x specified in radians. |  |
| \(\sqrt{x}\) | The square root of x. |  |
| s rand(x) | Specify a seed value for calculating random numbers. |  |

Although gawk does not have an extensive list of mathematical functions, it does provide some of the basic elements you need for standard mathematical processing. The \(\int(\)\) function produces the integer portion of a value, but it doesn't round the value. It behaves much like a floor function found in other programming languages. It produces the nearest integer to a value between the value and 0.

This means that the \(\int(\)\) function of the value 5.6 will return 5, while the \(\int(\)\) function of the value -5.6 will return -5.

The rand() function is great for creating random numbers, but you'll need to use a trick to get meaningful values. The rand() function returns a random number, but only between the values 0 and 1 (not including 0 or 1). To get a larger number, you'll need to scale the returned value.

A common method for producing larger integer random numbers is to create an algorithm that uses the rand() function, along with the \(\int(\)\) function:

```
x=\(\int(10\times\text{rand()}\)\)
```

This returns a random integer value between (and including) 0 and 9. Just substitute the 10 in the equation with the upper limit value for your application, and you're ready to go.

Be careful when using some of the mathematical functions, because