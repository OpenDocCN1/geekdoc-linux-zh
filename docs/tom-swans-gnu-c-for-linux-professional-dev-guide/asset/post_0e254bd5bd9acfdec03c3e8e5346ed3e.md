
## MULTIPLE ASSIGNMENTS

When you need to initialize several variables to the same value, you can use statements such as the following:

```
int A, B, C;
A = B = C = 451;
```

That sets A, B, and C to 451. This isn't a special form of syntax, but simply a result of the way C++ evaluates expressions. Because the expression (A = B) equals the value assigned to A, the preceding statement is evaluated as though written using parentheses to group each subexpression:

```
( A = ( B = ( C = 451 ) ) );
```

> Note
> Unlike most operators, the assignment operator's associativity is right to left. For this reason, expressions such as A = B = C set B and A equal to C's value, in that order.

## SHORTHAND ASSIGNMENTS

Assignment statements sometimes do more work than necessary. The following statement refers to A twice:

```
A = A + 45;
```

You can write that same statement more concisely using the shorthand operator += this way:

```
A += 45;
```

Functionally, the two statements are equivalent. However, the second is potentially more efficient, especially if A is a complex expression—a calculated address, for example, or a position in an array returned by a function. (More on such cases in future chapters, especially Chapter 10, "Creating and Calling Functions.") C and C++ provide several other shorthand assignment operators, all of which reduce longhand expressions in this form:

```
i = i op j;
```

to the more concisely written

```
i op= j;
```

The full set of assignment operators is *=, /=, +=, -=, %=, <<=, >>=, &=, ^=, and |=. They are all near the bottom of the precedence order list (see Appendix B), so that any expressions on each side are fully evaluated before the shorthand operators are applied. Following are a few samples of shorthand assignment statements with the equivalent longhand expressions shown in comments:

```
count += 10;  // count = count + 10
count *= 2;   // count = count * 2
count /= 3;   // count = count / 3
count %= 16;  // count = count % 16
```

## THE MIN AND MAX OPERATORS

Newer releases of ANSI C++ compilers, including GNU C++, add two additional operators that many programmers don’t even know exist. Use the lesser-of and greater-of operators to compare two values, usually in an assignment. They are also known as the min and max operators. For example, given two integers value1 and value2 (they can be values of other fundamental types), the following statement assigns the lesser value to result:

```
result = value1 <? value2; // Assign lesser value to result
```

Similarly, the following statement assigns the greater of the two values to result:

```
result = value1 >? value2; // Assign greater value to result
```

The order of variables in the expressions to the right of the assignment doesn’t matter. If value1 equals value2, result is set to that value.

## SUMMARY

All expressions have values. Even a simple variable name such as counter is an expression that has a value. With operators, programs create complex expressions that perform calculations and comparisons. Use parentheses to group subexpressions and force a different evaluation order. In the absence of parentheses, C++ evaluates expressions based on operator precedence and associativity, as detailed in Appendix B.

For more information on subjects introduced in this chapter, turn to the following chapters:

- Chapter 9, “Controlling Program Flow”
- Chapter 10, “Creating and Calling Functions”
- Chapter 11, “Managing Memory with Pointers”
- Chapter 22, “Mastering the Standard string Class”
- Appendix B, “C++ Operator Precedence and Associativity”

## CHAPTER 8

### Controlling Input and Output

It might surprise you that C++ has no native capabilities for input and output (I/O). The same is true of C. In both languages, I/O is provided strictly by library functions. For instance, to read and write data in C++ programs—whether to and from the console, or in a disk file—you must include the iostream.h header file and link the program to the compiled I/O stream library.

Not having I/O facilities built into a programming language might seem to be a drawback, but because I/O in C and C++ is provided by compiled libraries, programmers who develop code for embedded systems or for special-purpose computers are free to devise their own I/O functions and techniques. This fact makes C and C++ well suited to low-level programming. However, most software application developers might as well take advantage of the standard libraries. They have been tweaked to the hilt by GNU's authors, and it would be difficult to outdo their efforts.

This chapter explains how to read and write fundamental data objects and strings using C++ I/O streams, and how to format strings to produce good-looking output.

### INTRODUCING C++ I/O STREAMS

An I/O stream object behaves much like the standard input and output file streams that are familiar to C programmers. But rather than call a standard library function such as puts(), C++ programs use the "put-to" operator (<<) for output and the "get-from" operator (>>) for input operations. For example, in C++, to write a program's title string to the standard output, you can use a statement such as

```
cout << "Fishbowl Screen Saver by Grouper Tom" << endl;
```

You've seen similar statements many times so far in this book. However, the cout object also provides functions you can call to perform many different tasks. To write a single character variable c to the standard output, you can use the statements:

```
char c = 'p';
cout.put(c);
```

The put() function is a member of the cout object's class—a new concept that you learn more about in Chapter 12, "Introducing the Class." To call an object's member function, type a period after the object name followed by the function to call. The function is called in reference to its object, in this case, cout.

Similarly, to read a character from the standard input, use the input stream object, cin, along with the get-from operator, >>. This statement reads one character from the standard input into a char variable c:

```
char c;
cin >> c;
```

Notice that the put-to and get-from operators seem to point to their targets. As you can with cout, you can call a member function in reference to cin. For example, the following performs the identical task as the preceding statement:

```
cin.get(c);
```
