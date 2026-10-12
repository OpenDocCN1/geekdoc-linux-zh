
not evenly divisible by any other prime number. This stems from the fact that any nonprime integer can be expressed as a multiple of prime factors. (For example, 20 has the prime factors 2, 2, and 5.) You can use this added insight to develop a more efficient prime number program. The program can test if a given integer is prime by determining if it is evenly divisible by any other previously generated prime. By now the term “previously generated” should trigger in your mind the idea that an array must be involved here. You can use an array to store each prime number as it is generated.

As a further optimization of the prime number generator program, it can be readily demonstrated that any nonprime integer n must have as one of its factors an integer that is less than or equal to the square root of n. This means that it is only necessary to determine if a given integer is prime by testing it for even divisibility against all prime factors up to the square root of the integer.

Program 6.4 incorporates the previous discussions into a program to generate all prime numbers up to 50.

## Program 6.4 Revising the Program to Generate Prime Numbers, Version 2

Click here to view code image

```
#
#
/
i
{
```

```
}
```

## Program 6.4 Output

Click here to view code image

```
2
```

The expression

```
p
```

is used in the innermost for loop as a test to ensure that the value of p does not exceed the square root of p. This test comes directly from the discussions in the previous paragraph. (You might want to think about the math a bit.)

**Program 6.4** starts by storing 2 and 3 as the first two primes in the array p. This array has been defined to contain 50 elements, even though you obviously don’t need that many locations for storing the prime numbers. The variable p is initially set to 2, which is the next free slot in the p array. A for loop is then set up to run through the odd integers from 5 to 50. After the Boolean variable i is set to true, another for loop is entered. This loop successively divides the value of p by all of the previously generated prime numbers that are stored in the array p. The index variable i starts at 1 because it is not necessary to test any values of p for divisibility by p (which is 2). This is true because our program does not even consider even numbers as possible primes. Inside the loop, a test is made to see if the value of p is evenly divisible by p, and if it is, then i is set false. The for loop continues execution so long as the value of i is true and the value of p does not exceed the square root of p.

After exiting the for loop, a test of the i flag determines whether to store the value of p as the next prime number inside the p array.

After all values of p have been tried, the program displays each prime number that has been stored inside the p array. The value of the index variable i varies from 0 through p - 1 because p was always set pointing to the next free slot in the p array.

## Initializing Arrays

Just as you can assign initial values to variables when they are declared, so can you assign initial values to the elements of an array. This is done by simply listing the initial values of the array, starting from the first element. Values in the list are separated by commas and the entire list is enclosed in a pair of braces.

The statement

```
Click here to view code image
```

declares an array called c to contain five integer values and initializes each of these elements to zero. In a similar fashion, the statement

```
Click here to view code image
```

sets the value of i to 0, i to 1, i to 2, and so on.

Arrays of characters are initialized in a similar manner; thus the statement

```
Click here to view code image
```

defines the character array l and initializes the five elements to the characters ' ', ' ', ' ', ' ', and ' ', respectively.

It is not necessary to completely initialize an entire array. If fewer initial values are specified, only an equal number of elements are initialized. The remaining values in the array are set to zero. So the declaration

initializes the first three values of s to 1, 3, and 5, and sets the remaining 497 elements to zero.

By enclosing an element number in a pair of brackets, specific array elements can be initialized in any order. For example,

```
Click here to view code image
    for
```

initializes the s array to the same values as shown in the previous example. And the statements

```
Click here to view code image
    int
```

define a 10-element array and initialize the last element to the value of x (or to 1), and the first three elements to 1, 2, and 3, respectively.

Unfortunately, C does not provide any shortcut mechanisms for initializing array elements. That is, there is no way to specify a repeat count, so if it were desired to initially set all 500 values of s to 1, all 500 would have to be explicitly spelled out. In such a case, it is better to initialize the array inside the program using an appropriate for loop.

Program 6.5 illustrates two types of array-initialization techniques.

## Program 6.5 Initializing Arrays

```
Click here to view code image
```

```
#

i
{
```

## Program 6.5 Output

```
Click here to view code image
```

```
a
a
a
a
a
a
a
a
```

In the declaration of the array a, the first five elements of the array are initialized to the square of their element number (for example, element number 3 is set equal to $3^{2}$ or 9). The first for loop shows how this same type of initialization can be performed inside a loop. This loop sets each of the elements 5 through 9 to the square of its element number. The second for loop simply runs through all 10 elements to display their values at the terminal.

## Character Arrays

The purpose of Program 6.6 is to simply illustrate how a character array can be used. However, one point is worthy of discussion. Can you spot it?

**Program 6.6 Introducing Character Arrays**

*Click here to view code image*

```
```
#
i
{

}
```
```

**Program 6.6 Output**

H

The most notable point in the preceding program is the declaration of the character array w. There is no mention of the number of elements in the array. The C language allows you to define an array without specifying the number of elements. If this is done, the size of the array is determined automatically based on the number of initialization elements. Because Program 6.6 has six initial values listed for the array w, the C language implicitly dimensions the array to six elements.

This approach works fine so long as you initialize every element in the array at the point that the array is defined. If this is not to be the case, you must explicitly dimension the array.

In the case of using index numbers in the initialization list, as in

*Click here to view code image*

for

the largest index number specified sets the size of the array. In this case, s is set to contain 100 elements, based on the largest index value of 9 that is specified.

## Base Conversion Using Arrays

The next program further illustrates the use of integer and character arrays. The task is to develop a program that converts a positive integer from its base 10 representation into its equivalent representation in another base up to base 16. As inputs to the program, you specify the number to be converted and also the base to which you want the number converted. The program then converts the keyed-in number to the appropriate base and displays the result.

The first step in developing such a program is to devise an algorithm to convert a number from base 10 to another base. An algorithm to generate the digits of the converted number can be informally stated as follows: A digit of the converted number is obtained by taking the modulo of the number by the base. The number is then divided by the base, with any fractional remainder discarded, and the process is repeated until the number reaches zero.

The outlined procedure generates the digits of the converted number starting from the rightmost digit. See how this works in the following example. Suppose you want to convert the number 10 into base 2. *Table 6.1* shows the steps that would be followed to arrive at the result.

| Number | Number Modulo 2 | Number / 2 |
|:-------|:----------------|:-----------|
| 10     | 0               | 5          |
| 5      | 1               | 2          |
| 2      | 0               | 1          |
| 1      | 1               | 0          |

*Table 6.1 Converting an Integer from Base 10 to Base 2*

The result of converting 10 to base 2 is, therefore, seen to be 1010, reading the digits of the “Number Modulo 2” column from the bottom to the top.

To write a program that performs the preceding conversion process, you must take a couple of things into account. First, the fact that the algorithm generates the digits of the converted number in reverse order is not very nice. You certainly can’t expect the user to read the result from right to left, or from the bottom of the page upward. Therefore, you must correct this problem. Rather than simply displaying each digit as it is generated, you can have the program store each digit inside an array. Then, when you’ve finished converting the number, you can display the contents of the array in the correct order.

Second, you must realize that you specified for the program to handle conversion of numbers into bases up to 16. This means that any digits of the converted number that are between 10 and 15 must be displayed using the corresponding letters, A through F. This is where our character array enters the picture.

Examine Program 6.7 to see how these two issues are handled. This program also introduces the type qualifier `c`, which is used for variables whose value does not change in a program.

```
Program 6.7 Converting a Positive Integer to Another Base
*Click here to view code image*
```

```
/
#
```
