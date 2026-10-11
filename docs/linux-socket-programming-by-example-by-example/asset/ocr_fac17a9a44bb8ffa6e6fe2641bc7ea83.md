# Table 11.3: Advanced RPN Server Functions

| Function | Argument | Description |
| :--- | :--- | :--- |
| gcd | N/A | Compute the greatest common divisor between the top two numbers on the stack. The result replaces the top two numbers on the stack. |
| seed | N/A | Use the value on top of the stack as a random number seed value. There is no result pushed onto the stack. |
| random | N/A | Use the value on the top of the stack to act as the largest value + 1 for the random number to be generated. The random result replaces the input value on the stack. |
| tprime | N/A | Test the top stack value to see if it is a prime number. The second-to-last number on the top of the stack indicates how many tests to apply. A typical value is 25. The result replaces the two input values on the stack. A result of 1 indicates that the number is probably prime, while 0 indicates that the number is not prime. |
| genprime | N/A | Generate a prime number, using the top of the stack as a "maximum random number + 1" value (see random). The second-to-last number on the stack indicates the number of tests to perform (typically 25). The generated result replaces the top two values. |
| swap | N/A | Swap the top two values on the stack. Useful for exchanging two numbers. |
| dup | N/A | Duplicate the top value on the stack. |

The use of the seed and random functions require a bit of explanation. The seed function allows you to predictably seed a random number generator. This is important if you want to reproduce a set of random numbers for subsequent tests. For example:

![](bbox=[0.07, 0.66, 0.17, 0.77])

```
```
#:1000
0:
seed
0:
#:3000
0:
random
0:
dump
0:560
```
```

This sequence seeds the random number generator with the value 1000. Later, 3000 is input to the function random which produces the random number 560. The value 3000 acts as a maximum value + 1 for the random function. With this as an input value, the random number generated could be between the values of 0 and 2999.