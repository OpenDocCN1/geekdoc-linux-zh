
## 3.2 Data Types

With Tcl 8.0, lists and strings are treated differently within the interpreter. If you are dealing with data as a list, it's more efficient to use the list commands. If you are dealing with data as a string, it's better to use the string commands.

The commands that manipulate lists and strings will be discussed later.

### 3.2.3 Associative Arrays

The associative array is an array that uses a string to index the array elements, instead of a numeric index the way C, Fortran, and Basic implement arrays. For example, price(apple) and price(pear) would be associative array variables that could contain the price of an apple or pear.

Example 3.2.3-1

```
set price(apple) .10
price is an associative array. The variable referenced by the index apple is set to .10.
```

```
set price(pear) .15
price is an associative array. The variable referenced by the index pear is set to .15.
```

```
set quantity(apple) 20
quantity is an associative array. The variable referenced by the index apple is set to 20.
```

```
set discount(12) .0.95
discount is an associative array. The variable referenced by the index 12 is set to 0.95.
```

### 3.2.4 Handles

Tcl uses handles to refer to certain special-purpose objects. These handles are returned by the Tcl command that creates the object and can be used to access and manipulate the object. When you open a file, a handle is returned for accessing file. The graphic objects created by a wish script are also accessed via handles, which will be discussed in the wish tutorial.

Types of handles include:

- channel: A handle that references an I/O device such as a file, serial port, or TCP socket. A channel is returned by an open socket call and can be an argument to a puts, read, close, flush or gets call.
- graphic: A handle that refers to a graphic object created by a wish command. This handle is used to modify or query an object.
- http: A handle that references data returned by an http::geturl operation. An http handle can be used to access the data that was returned from the http::geturl command or otherwise manipulate the data.

## 3.3 Tcl Commands

Tcl has a rich set of commands. This section will introduce a subset of those commands. Most of these commands will be used in the examples in the next few chapters. With these few commands you can start writing useful Tcl programs.

### 3.3.1 Assigning Values to Variables

The command to define the value of a variable is set. It allocates space for a variable and a set of data and assigns the data to variable.

Syntax: `set varName ?value?`

- set: Define the value of a variable.
- varName: The name of the variable to define.
- value: The data to assign to the variable.

If set is invoked with two arguments, the first argument will be treated as the variable name and the second as a value to assign to that variable.

If set is invoked with a single argument, then that argument must be a variable name and the value of that variable is returned.

Set always returns the value of the variable.

Example 3.3.1-1

```
% set x 1
1
% set x
1
% set y
can't read "y": no such variable
```

### 3.3.2 Math Operations

Math operations are performed using the `incr` and `expr` commands. The `incr` command provides a fast method of incrementing the value of an integer, and the `expr` command provides an interface to a general-purpose calculation engine.

The `incr` command will add an integer value to a variable. The value may be positive or negative, thus allowing the `incr` command to perform a decrement operation. The `incr` command is used primarily to adjust loop variables.

**Syntax:** `incr varName ?incrValue?`

- incr: Add a value (default 1) to a variable.
- varName: The name of the variable to increment. NOTE: This is a variable name, not a value. Do not start the name with a $. This variable must contain an integer value, not a floating-point value.
- incrValue?: The value to increment the variable by. May be a negative number. This value must be an integer, not a floating-point value.

Example 3.3.2-1

```
% set x 4
4
% incr x
5
% incr x -3
2
```

The expr command is a general-purpose calculation command that will perform arbitrarily complex math operations. Unlike most Tcl commands, expr does not expect a fixed number of arguments. It can be invoked with the arguments grouped as a string or as individual values and operators. Arguments to expr may be grouped with parentheses to control the order of math operations.

The expr command can also evaluate boolean expressions and is used to test conditions by the Tcl branching and looping commands.

**Syntax:** `expr mathExpression`

Tcl commands support these math operations (grouped in decreasing order of precedence):

- ~ ! Unary minus, unary plus, bitwise NOT, logical NOT
- / % Multiply, divide, remainder
- + Add, subtract
- << >> Left shift, right shift
- > <= Less, greater than, less than or equal, greater than or equal
- != Equality, inequality
- & Bitwise AND
- ^ Bitwise exclusive OR
- | Bitwise OR
- && Logical AND. Produces a 1 result if both operands are nonzero, 0 otherwise.
- || Logical OR. Produces a 0 result if both operands are zero, 1 otherwise.
- x?y:z If-then-else, as in C If x evaluates to nonzero, then the result is the value of y. Otherwise, the result is the value of z. The x operand must have a numeric value. The y and z operands may be variables or Tcl commands.

Note that the bitwise operations are valid only if the arguments are integers (not floating-point or scientific notation).

The expr command also supports these math functions and conversions: 

### Trigonometric Functions

- cosine: arccosine: hyperbolic cosine: cos(radians) acos(float) cosh(radian)
- sin: arcsin: hyperbolic sin: sin(radians) asin(float) sinh(radian)
- tangent: arctangent: hyperbolic tangent: tan(radians) atan(float) tanh(radian)
- Euclidean distance: ratio: hypot(float) atan2(float)

### Exponential Functions

- natural log: base 10: log(float) log10(float)
- power: exp(float)

### Conversion Functions

- Largest integer less than a float: floor(num)
- Smallest integer greater than: ceil(num) own- remainder: fmod(num)
- absolute value: abs(num)
- convert to float: double(num)
- convert to int: int(num)

### Random Numbers

- seed: srand(num)
- generate random: rand()

### 3.3.3 Choices

Tcl supports a simple choice command (if) and a multiple choice command (switch).

The if command tests a condition, and if that condition is true, the script associated with it is evaluated.

Syntax:

```
if {testExpression1} {
  body1
} elseif {testExpression2} {
  body2
  ...
} else {bodyN}?
```

Determine whether a code body should be evaluated based on the results of a test. If the test returns true, the first body is evaluated. If the test is false and a body of code exists after the else, then that code will be evaluated.

testExpression1 If this expression evaluates to true, the first body is evaluated. The expression must be in a form acceptable to expr. These forms include

- An arithmetic comparison {$a < 2}
- A string comparison {$string != "OK"}
- The results of a command [eof $inputFile]
- A variable with a numeric {$AnalysisResult} value. Zero (0) is considered false, and nonzero values are true.

body1 The body of code to evaluate if the first test evaluates as true.

elseif If testExpression1 is false, evaluate testExpression2.

testExpression2 A second test to evaluate if the first test evaluates to false.

body2 The body of code to evaluate if the second test evaluates as true.

?else bodyN If all evaluate false, this body of code will be evaluated.
