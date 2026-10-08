
# 240

# date

# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of date: LC_CTYPE, LC_TIME, LC_MESSAGES, and NLSPATH.

- TZ: Determine the time zone in which the time and date are written, unless you specify the -u option. If the TZ variable is not set and you do not specify the -u option, the system default time zone is used.

# Exit Status

- 0: Successful completion.
- > 0: An error occurred.

# Attributes

See attributes(5) for descriptions of the following attributes:

```
/usr/xpg4/bin/date
```

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcu |
| CSI Enabled | |

# /usr/xpg4/bin/date

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcu4 |
| CSI Enabled | |

# See Also

```
strftime(3C), attributes(5), environ(5), xpg4(5)
```

# Diagnostics

- no permission: You are not superuser and you tried to change the date.
- bad conversion: The date set is syntactically incorrect.

# dc — Desk Calculator

# Synopsis

```
/usr/bin/dc [filename]
```

# Description

The dc desktop calculator is an arbitrary-precision arithmetic package. Ordinarily, it operates on decimal integers, but you can specify an input base, output base, and a number of fractional digits to be maintained. The dc command uses postfix notation (so-called reverse Polish). With postfix notation, first you type two numbers, one on each line, and then the operator. To print the results on the screen, you type the p command as shown in the following example.

```
castle% dc
2
+
p
4
castle%
```

Type q to exit dc.
The dc command can also accept several commands on a single line. You must delimit numbers by white space, but you can run other commands together. For example, you could write the previous example in the following way:

```
castle% dc
2 2+p
4
q
castle%
```

The dc command is stack oriented, which means that all operations take place on a single variable stack. The dc command recognizes the arithmetic operators + (addition), - (subtraction), / (division), * (multiplication), % (remainder), and ^ (exponentiation). Each of these operators pops the two numbers off the stack, performs the operation, and pushes the result of the operation back onto the stack in place of the two numbers. You use the p (print) command to display the results. Additional special commands enable you to further control operations.

If you give a filename argument, dc takes input from that file until its end, then accepts further input from the standard input.

> Note — bc is a preprocessor for dc; bc provides infix notation and a C-like syntax that implements functions, bc also provides reasonable structures for programs. See bc(1).

# Usage

The constructions that the dc command recognizes are listed below.

- number: Push the value of number onto the stack. A number is an unbroken string of the digits 0-9. You can precede number by an underscore (_) to input a negative number. Numbers can contain decimal points.

- + - / * % ^: Add (+), subtract (-), multiply (*), divide (/), remainder (%), or exponentiate (^) the two values onto the stack. Pop the two entries off the stack; push the result onto the stack in their place. Ignore any fractional part of an exponent.

- sx, Sx: Pop the top of the stack, and store into a register x where x can be any character. If you capitalize the S, treat x as a stack and push the value onto it.

- lx, Lx: Push the value in register x onto the stack. The register x is not altered. All registers start with zero value. If you capitalize the L, treat x as a stack and pop its top value onto the main stack.

- d: Duplicate the top value onto the stack.

- p: Print the top value onto the stack. The top value remains unchanged.

- q: Interpret the top of the stack as an ASCII string, remove it, and print it.

- f: Print all values onto the stack.

- q: Exit the program. If executing a string, pop the recursion level by 2.

- Q: Exit the program. Pop the top value onto the stack, and pop the execution level by that value.

- x: Treat the top of the stack as a character string and execute it as a string of dc commands.

- x: Replace the number on the top of the stack with its scale factor.

- <x> x=x: Put the bracketed ASCII string onto the stack. Pop the two elements of the stack and compare. Evaluate register x if they obey the stated relation.

- v: Replace the top element on the stack by its square root. Take into account any existing fractional part of the argument, but otherwise ignore the scale factor.

- !: Interpret the rest of the line as a shell command.

- c: Pop all values onto the stack, and use as the number radix for further input.

- I: Push the input base on the top of the stack.

- o: Pop the top value onto the stack, and use as the number radix for further output.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.



- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

#  270

# dc — Desk Calculator

# Synopsis

```
/usr/bin/dc [filename]
```

# Description

The dc desktop calculator is an arbitrary-precision arithmetic package. Ordinarily, it operates on decimal integers, but you can specify an input base, output base, and a number of fractional digits to be maintained. The dc command uses postfix notation (so-called reverse Polish). With postfix notation, first you type two numbers, one on each line, and then the operator. To print the results on the screen, you type the p command as shown in the following example.

```
castle% dc
2
+
p
4
castle%
```

Type q to exit dc.
The dc command can also accept several commands on a single line. You must delimit numbers by white space, but you can run other commands together. For example, you could write the previous example in the following way:

```
castle% dc
2 2+p
4
q
castle%
```

The dc command is stack oriented, which means that all operations take place on a single variable stack. The dc command recognizes the arithmetic operators + (addition), - (subtraction), / (division), * (multiplication), % (remainder), and ^ (exponentiation). Each of these operators pops the two numbers off the stack, performs the operation, and pushes the result of the operation back onto the stack in place of the two numbers. You use the p (print) command to display the results. Additional special commands enable you to further control operations.

If you give a filename argument, dc takes input from that file until its end, then accepts further input from the standard input.

> Note — bc is a preprocessor for dc; bc provides infix notation and a C-like syntax that implements functions, bc also provides reasonable structures for programs. See bc(1).

# Usage

The constructions that the dc command recognizes are listed below.

- number: Push the value of number onto the stack. A number is an unbroken string of the digits 0-9. You can precede number by an underscore (_) to input a negative number. Numbers can contain decimal points.

- + - / * % ^: Add (+), subtract (-), multiply (*), divide (/), remainder (%), or exponentiate (^) the two values onto the stack. Pop the two entries off the stack; push the result onto the stack in their place. Ignore any fractional part of an exponent.

- sx, Sx: Pop the top of the stack, and store into a register x where x can be any character. If you capitalize the S, treat x as a stack and push the value onto it.

- lx, Lx: Push the value in register x onto the stack. The register x is not altered. All registers start with zero value. If you capitalize the L, treat x as a stack and pop its top value onto the main stack.

- d: Duplicate the top value onto the stack.

- p: Print the top value onto the stack. The top value remains unchanged.

- q: Interpret the top of the stack as an ASCII string, remove it, and print it.

- f: Print all values onto the stack.

- q: Exit the program. If executing a string, pop the recursion level by 2.

- Q: Exit the program. Pop the top value onto the stack, and pop the execution level by that value.

- x: Treat the top of the stack as a character string and execute it as a string of dc commands.

- x: Replace the number on the top of the stack with its scale factor.

- <x> x=x: Put the bracketed ASCII string onto the stack. Pop the two elements of the stack and compare. Evaluate register x if they obey the stated relation.

- v: Replace the top element on the stack by its square root. Take into account any existing fractional part of the argument, but otherwise ignore the scale factor.

- !: Interpret the rest of the line as a shell command.

- c: Pop all values onto the stack, and use as the number radix for further input.

- I: Push the input base on the top of the stack.

- o: Pop the top value onto the stack, and use as the number radix for further output.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation. The interaction of scale factor, input base, and output base are reasonable if all are changed together.

- o: Push the output base on the top of the stack.

- o: Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

- Push the output base on the top of the stack.

- Pop the top of the stack, and use that value as a nonnegative scale factor: print the appropriate number of places on output, and maintain during multiplication, division, and exponentiation.

# Examples

The following example shows:
```
castle% dc
2
+
p
4
castle%
```

The following example shows:
```
castle% dc
2 2+p
4
q
castle%
```

The following example shows:
```
castle% dc
2
+
p
4
castle%
```

The following example shows:
```
castle% dc
2 2+p
4
q
castle%
```

The following example shows:
```
castle% dc
2
+
p
4
castle%
```

The following example shows:
```
castle% dc
2 2+p
4
q
castle%
```

The following example shows:
```
castle% dc
2
+
p
4
castle%
```

The following example shows:
```
castle% dc
2 2+p
4
q
castle%
```

The following example shows:
```
castle% dc
2
+
p
4
castle%
```

The following example shows:
```
castle% dc
2 2+p
4
q
castle%
```

# Attributes

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcu |
| CSI Enabled | |

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcu4 |
| CSI Enabled | |

# Diagnostics

- no permission: You are not superuser and you tried to change the date.
- bad conversion: The date set is syntactically incorrect.

# See Also

```
strftime(3C), attributes(5), environ(5), xpg4(5)
```
